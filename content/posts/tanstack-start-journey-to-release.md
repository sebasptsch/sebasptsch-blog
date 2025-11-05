---
title: Using TanStack Start on it's Journey to Release
date: 2025-11-05
draft: false
categories: [Web Development]
tags: [TanStack, React, Web Development, Open Source]
---

The prevalence of component libraries and an increasingly large ecosystem of tools for building web applications has provided a litany of choices for developers looking to build modern web applications. 

When I started programming with React a few years ago I began making single page applications using the ever-popular `react-router` for routing between pages of my application. This didn't change much as I began to build more complex applications as it scaled well enough for my needs.

My first production application used `react-router` and `redux` and as it grew in complexity I began looking for better ways to manage data fetching and caching. This led me to discover React Query which provided a powerful and flexible way to manage server state in my application.

In late 2024 I started using TanStack Router, a new routing library from the creators of React Query. It promised superior type safety, something that `react-router` wasn't built around, along with better integration with TanStack Query. As the router project was still in development full stack examples began to appear using a work-in-progress Vite wrapper called Vinxi to help bootstrap applications quickly.

Tanstack Start popped up shortly after the release of TanStack Router as an project in the Alpha stage. It promised the same type safety as TanStack Router along with server features like API routes, server-side rendering and server functions. Given my positive experience with TanStack Router I followed the project closely as it developed towards a stable release, first with the Vinxi wrapper and later as a standalone framework built on top of Vite's plugin and environments API.

Over the past several months the dependancy on the Vinxi wrapper was removed in favour of a first-party solution built directly into TanStack Start, taking advantage of Vite's flexibility to provide a great developer experience. What this also enabled was the ability to use the Cloudflare Vite plugin to run the server-side code on a local Cloudflare Workers environment, allowing for easy testing and deployment to the Cloudflare platform with first-party support for features like Durable Objects and KV storage.

With the upcoming stable release of TanStack Start I'm looking forward to making it my go-to framework for building full stack web applications with React. The type safety, server-side features, and seamless integration with TanStack Query make it a compelling choice for modern web development and I'm excited to see how it evolves in the future.