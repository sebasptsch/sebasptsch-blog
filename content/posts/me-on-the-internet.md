---
date: 2025-09-21
draft: false
title: The Evolution of me on the Internet
categories: [Open Source, Programming]
tags: [Blogging, Internet, History]
---

Being nearly done with my university degree and looking for work I've begun to notice how many companies allow for a website or portfolio link on job applications. Before now I hadn't really upgraded my personal website since this time of year in 2022 when I decided to invest a lot of time into building a full stack website using Remix, Postgres and the Slate rich text editor, paired with oAuth through Github and Discord for authentication. Admittedly though I did sometimes post new content to that blog I never really made a habit of it, and after I lost interest in the project I let it sit dormant for a long time.

After having worked in web development for a couple years now I understand that the most complex and feature complete website is not always the best choice for a small project. Because I didn't really have the constant bandwidith to maintain the site it went years without any updates and, despite being built on popular technologies at the time it wasn't very easy to maintain. The homebrew CMS I had built wasn't very user friendly and nor was it easy to deploy updates to the site as it was a packaged docker container that needed to be rebuilt and redeployed every time I wanted to make a change that wasn't just content related.

So, after the computer that I had been hosting the site on broke down I decided to look for a new solution. I wanted something that wasn't too complex to maintain but also allowed me enough flexibility to create a new post whenever I wanted without the risk of breaking something. I had used solutions like Ghost and had heard of Wordpress before but I wanted something a lot less clunky and quick to load. I spent an afternoon looking at the different frameworks that top individual posters on Hacker News were using and eventually settled on Hugo, a static site generator built on Go that had a number of established themes and a large community.

Though Wordpress was easily the most popular platform for blogging it had a lot of bloat and security issues that I wanted to avoid. A number of the Wordpress sites that ended up having featured content on Hacker News were slow to load and often were quite outdated.

Because of my reluctance to choose a theme that might eventually become unmaintained I decided to use the PaperMod theme as it had a large number of stars on Github and was being actively maintained. The theme is very minimalistic and fast loading, with a focus on typography and readability. It also had a number of features that I wanted, such as support for tags and categories, a dark mode and a responsive design that worked well on mobile devices without too much clutter.

What I can say for certain is that it was a lot easier to deploy and maintain than my previous solution and because it outputs static HTML files I can use any static site hosting service to host my site. Because of it's accessibility I stuck with Github Pages as I was already planning to use Github for the CI/CD pipeline to automatically build and deploy the site whenever I pushed new content to the repository.

In short, I'm happy with the options and flexbility that Hugo and the PaperMod theme provide. It's a lot easier to maintain than my previous solution and allows me to focus on creating content rather than worrying about the technical details of hosting and maintaining a website. I'm hoping to make a habit of reflecting on my experiences and hobbies in the future and sharing them with others who might find them interesting or useful.

I've built and used a number of different solutions for blogging over the years, starting from simple HTML pages to GatsbyJS, NextJS, Remix and now Hugo. Each solution has had its own pros and cons, but I've learned a lot from each experience and have been able to improve my skills as a developer along the way.