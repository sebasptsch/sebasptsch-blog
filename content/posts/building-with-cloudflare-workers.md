---
title: Building Applications with Cloudflare Workers
date: 2026-01-14
draft: false
tags: [Web Development, Open Source, Cloudflare, TypeScript]
categories: [Web Development, Programming]
---

Needing a quick-to-prototype developer-friendly platform for my university course, I turned to Cloudflare Workers and Tanstack Start and Query. 

The task was simple enough; we needed to plan, deploy and showcase a todo app. Outside of functional requirements, it was also essential that everyone in the project was able to collaborate and test the project locally with a wide variety of skill levels and technical abilities.

Cloudflare Workers allowed us to achieve that goal in the limited timeframe that we had. It enabled us to do this using a couple of major points:

## Seamless Server Environment Emulation

By utilising the Cloudflare Vite Plugin, any of the services we used in production, including the production JavaScript environment itself, were emulated locally. This ensured that any code that we developed locally was nearly guaranteed in the Cloudflare Workers Production Environment. 

This meant that if we used any features that weren't supported by Cloudflare's runtime, we would encounter errors locally rather than once the application was deployed to production.

## Cloudflare Local Bindings

Our simple project had dependencies on a couple of different backend services, including Cloudflare's SQLite-compatible D1 Database and Cloudflare Workers KV for Key-Value storage.

Cloudflare makes it ridiculously simple to set up dependencies on their services, requiring only a couple of CLI commands to update the TypeScript definitions and start developing in no time. 

What makes Cloudflare's integration so seamless to use is that their most popular services are emulated alongside their workers JavaScript environment, meaning that features that relied on the database or key-value storage could be prototyped using a local-only database until they were ready to be deployed to production.

This meant that as each member of our team developed their own features, database migrations only ran once their code was in production without requiring a staging or experimental database environment.

The great thing about all these developer conveniences was that once they were set up, anybody could pull down the changes and run the development command (`bun dev` in this case) and have every sidecar service up and running.