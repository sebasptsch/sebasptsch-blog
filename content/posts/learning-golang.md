---
title: "Learning Go as a JavaScript Developer"
date: 2025-09-25
draft: false
categories: [Programming]
tags: [Go, Golang, JavaScript, Programming]
---

I've been working with JavaScript and its ecosystem for several years now, primarily focusing on web development with libraries like React and experimenting with different runtime environments like Node.js and Bun. Recently, I decided to expand my programming skills by learning Go (Golang), a statically typed, compiled language known for its simplicity and performance.

## Why Go?

Given my interest in web development and developing efficient backend services, Go seemed like a natural choice coming from JavaScript. I first considered learning Go after seeing that Microsoft was porting the TypeScript compiler to Go. There are many different projects in the JavaScript ecosystem that use a faster compiled language for the massive performance improvements. For example, the Deno JavaScript runtime is built using Rust and the Bun runtime uses Zig. Coming from languages like JavaScript and TypeScript I was curious to see how Go handled concurrency and multithreading, as these are areas where JavaScript often meets limitations.

## Getting Started

Often when people ask me how they should get started with a new programming language I tell them to choose a small project that they can build and make discoveries along the way. The first project that I decided to build was a service that stored a record of a recurring webhook task and executed it based on a cron schedule. I wanted to build something that was simple in requirements but would actually result in a service that I (or others) could use. It involved GoORM for it's SQLite database interactions, the cron package for scheduling tasks, and GraphQL for the API. You can find the project on [here](https://github.com/sebasptsch/go-cron-webhooks).

After getting the basics of the language and it's features down I decided that more in-depth knowledge of the language and how it handled concurrency was needed. For this I followed a well-established LinkedIn learning course called "Learning Go" by David Gassner. The course addressed the core aspects of the language from scratch and also covered some of the more advanced features like goroutines and channels. I found the course to be very informative and it helped me solidify my understanding of Go's concurrency model.

## Key Takeaways

1. **Simplicity and Performance**: Go's syntax is clean and straightforward, making it easy to read and write. The performance benefits of a compiled language were immediately noticeable, especially in tasks that required concurrency.

2. **Concurrency Model**: Go's approach to concurrency with goroutines and channels is powerful and intuitive. It allows for efficient handling of multiple tasks simultaneously without the complexity often associated with multithreading in other languages.

3. **Standard Library**: Go's standard library is extensive and well-designed, providing robust tools for tasks like HTTP handling, file I/O, and more. This reduces the need for third-party libraries for many common tasks.

4. **Tooling**: The Go toolchain is excellent, with built-in support for formatting, testing, and dependency management. This makes it easy to maintain code quality and manage projects.

## Conclusion

Go as a language like many other compiled languages has advantages over it's interpreted counterparts in terms of performance and efficiency. Having the ability to create an application that's fast and memory efficient is a great skill to have as a developer. Having a solid understanding of both JavaScript and Go opens up a wide range of possibilities for building modern web applications and services. I'm excited to continue exploring Go and applying it to real-world projects in the future.