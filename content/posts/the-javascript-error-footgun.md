---
date: 2026-01-26
draft: false
title: The JavaScript (and TypeScript) Error Footgun
categories: [Programming]
tags: [JavaScript, Frontend]
---

If you've developed code in JavaScript or TypeScript for any length of time you'll inevitably have encountered issues with error handling. If you haven't here's a simple example of what the typically error handling flow is meant to look like:

```js
try {
    functionThatThrows();
} catch (error) {
    console.error(error)
}
```

On first glance it looks pretty standard, you create a simple `try-catch` block and wrap your error-throwing code with it. This is the only way to handle errors for synchronous and asynchronous code in JavaScript. 

The first issue is one inherit in JavaScript itself, a lack of types. You've got no way to know if a function throws an error in the first place unless it was documented in comments or somewhere else.

There's no way to tell if `functionThatThrows` actually throws an error or not, much less what that error would look like. 

The other issue we encounter is when we want to use the data returned from an error-throwing function somewhere in the code:

```js
try {
    const functionResult = functionThatThrows();
} catch (error) {
    console.error(error)
}
```

All of a sudden any code that uses the return value of our throwing function needs to be inside the `try` block of the `try-catch`. If we want to handle each error differently we end up with a heavily indented, poorly formatted section of code that would look something like this:

```js
try {
    const firstFunctionResult = firstFunctionThatThrows();

    try {
        const secondFunctionResult = secondFunctionThatThrows();
    } catch (differentError) {
        console.error("different error", differentError)
    }
} catch (error) {
    console.error("original error", error)
}
```

Frankly that entire block of code is an absolute mess in terms of error handling. TypeScript doesn't change anything this example either, it doesn't infer what types of errors are thrown or if errors are thrown at all.

This is where a snippet from this [Github project](https://github.com/bdsqqq/try) comes in useful:

```ts
async function trytm<T>(promise: Promise<T>): Promise<[T, null] | [null, Error]> {
    try {
        const data = await promise;
        return [data, null];
    } catch (throwable) {
        if (throwable instanceof Error) return [null, throwable];

        throw throwable;
   }
}
```

Whilst it doesn't solve the problem of JavaScript and it's errors not being typed it does solve one aspect of that, inescapable tree of try-catch blocks. 

```js
const [data, error] = await trytm(thowingAsyncFunction())

if (error) {
    console.error("error thrown (and handled)", error)
    throw new Error("Some function threw an error", {
        cause: error
    })
}

console.log(data) // Known to be safe and not nested in a big tree
```

This small utility makes handling any errors in your application easier and more readable which, if you've ever seen how Golang applications handle errors this may be familiar.

Unless you start using packages like [`neverthrow`](https://github.com/supermacro/neverthrow) or the [`effect`](https://effect.website/docs) library it's impossible to have any sort of strictly typed errors that are taken for granted in other languages.

Errors in JavaScript are a [footgun](https://en.wiktionary.org/wiki/footgun), a functionality black-box that leads to more issues further down the road.