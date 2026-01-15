---
title: Async Generators for Paged APIs
date: 2026-01-15
draft: true
tags: [Web Development, Open Source, TypeScript]
categories: [Web Development, Programming]
---

There's one JavaScript feature that's not often talked about but enables heaps of advanced functionality, specifially around streaming data in both frontend and backend codebases.

That's Async Generators. 

It's a feature that was first introduced in ES2017/ES8 but remains largely outside the scope of knowledge of many developers. 

However, if you have an application that deals with streaming data using GraphQL or transferring data over websockets you may have come across generator functions before.

## Defining an async iterator

```ts
function* returnDemo() {
    return "Hello World";
}
```

What seperates generators from typical async functions however is how their values are able to be accessed. If you wanted to access the return value of `returnDemo` you can't simply do this:

```ts
const helloWorldText = returnDemo();
console.log(helloWorldText) // [object Generator]
```

Instead of getting back the returned text you would get back the signature of any generator function you create, an instance of `Generator`.

In order to get our value back from our iterator function you have to access it as an iterator using the following context:

```ts
const helloWorldGenerator = returnDemo();

const firstReturnedValue = helloWorldGenerator.next().value;

console.log(firstReturnedValue); // "Hello World" 
```

## Yield

The real utility of an async generator comes when you return a stream of values using the `yield` syntax as follows:

```ts
function* incrementingGenerator() {
    yield "One";
    yield "Two";
    yield "Three"
}
```

In this example more than one value is returned from the function when it's executed and this can be iterated through to get all the values.

```ts
console.log(incrementingGenerator.next().value); // "One"
console.log(incrementingGenerator.next().value); // "Two"
console.log(incrementingGenerator.next().value); // "Three"
```

An alternative syntax for this would be using a `for const` loop like so:

```ts
for await (const value of incrementingGenerator()) {
    console.log(value);
}

// "One"
// "Two"
// "Three"
```

Functionally this allows a developer to pipe the result of one function to the next without waiting for the first function to finish returning absolutely all of it's data first.

## Practical Example

As described in the introduction async iterables can be used to stream data between functions and provide a great interface with which to do so. 

One real-world use case that I implemented was the synchronisation of Google Calendar events using the incremental syncing API to a Postgres Database. 

As events are pulled from Google on a page-by-page basis they're `yielded` from the calendar synchronisation function and taken in by the database writing and filtering logic.

This can be seen here: [Student Attendance System](https://github.com/Team3132/attendance/blob/0c9c8c783de274163e1899ff12a3e2b1740ce877/src/server/services/calalendarSync.service.ts).

```ts
let cachedSyncToken: string | null = null;

const client = new google.auth.JWT({
    email: env.GOOGLE_CLIENT_EMAIL,
    key: env.GOOGLE_PRIVATE_KEY,
    scopes: ["https://www.googleapis.com/auth/calendar.readonly"],
  });

const calendar = google.calendar({
    version: "v3",
    auth: client,
});

const incrementalSync = async function* (
  syncToken?: string,
) {
  /** The google calendar parameters */
  const params: calendar_v3.Params$Resource$Events$List = {
    calendarId: env.GOOGLE_CALENDAR_ID,
    showDeleted: true,
    singleEvents: true,
    syncToken,
  };

  const [responseData, error] = await trytm(calendar.events.list(params));

  const { kv } = getServerContext();

  if (error) {
    if (error instanceof Common.GaxiosError && error.status === 410) {
      // Sync token is invalid, need to do a full sync
      cachedSyncToken = null;
      return incrementalSync();
    }

    throw error;
  }

  const initialData = responseData.data;

  if (initialData.items) {
    yield initialData.items;
  }

  if (initialData.nextSyncToken) {
    cachedSyncToken = initialData.nextSyncToken;
    eventLogger.debug("Updated sync token", initialData.nextSyncToken);
  }

  /** The page token */
  let pageToken: string | undefined;

  if (initialData.nextPageToken) {
    pageToken = initialData.nextPageToken;
  }

  while (pageToken) {
    const [response, error] = await trytm(
      calendar.events.list({
        ...params,
        pageToken,
      }),
    );

    if (error) {
      if (error instanceof Common.GaxiosError && error.status === 410) {
        // Sync token is invalid, need to do a full sync
        cachedSyncToken = null;
        return incrementalSync();
      }

      throw error;
    }

    const data = response.data;

    // If there are items yield them
    if (data.items) {
      yield data.items;
    }

    // If there is a next page token, update the page token
    // If there is no next page token, set the page token to undefined
    pageToken = data.nextPageToken ?? undefined;

    // If the sync token is present, update it
    if (data.nextSyncToken) {
      cachedSyncToken = data.nextSyncToken;
    }
  }
};
```

The above function, `incrementalSync` defines an Async Generator that returns calendar events by the page to be added or deleted from the database. 

If we were to take an approach using a typical async function we would have to wait for the entire function to finish collecting events into an array before we could start processing them.

This use case demonstrates exactly why Async Iterators can be so useful in processing or handling large amounts of data.

Now, in our database writing code we can simply call:

```ts

for await (const events of incrementalSync(cachedSyncToken)) {
    // write to database (an asynchronous opperation)
}
```