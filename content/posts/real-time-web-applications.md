---
title: Real Time Web Applications
date: 2025-11-05
draft: false
categories: [Web Development]
tags: [Real Time, Web Applications, WebSockets, SSE, WebRTC, GraphQL]
---

As part of my involvement in the UTS Programmers' Society in 2024 and 2025 I've had the opportunity to work on several real-time web applications. These projects have given me hands-on experience with various technologies and architectures that enable real-time communication between clients and servers, inspiring my interest in [WebRTC](/posts/go2rtc-for-3dprinters), WebSockets, and Server-Sent Events (SSE).

## Technologies Explored

Throughout these projects, I've explored a range of technologies that facilitate real-time interactions:
- **tRPC**: A library that facilitates type-safe communication between client and server applications (provided they're both written in TypeScript). It allows for seamless integration of real-time features using WebSockets.
- **WebSockets**: A protocol that enables two-way communication between a client and server over a single, long-lived connection. This is particularly useful for applications that require instant updates, such as the Programmers' Society [Club Voting System](https://github.com/ProgSoc/ClubVotingSystem) and [FuzzJudge](https://github.com/ProgSoc/FuzzJudge), a real-time competitive programming platform with live score updates.
- **Server-Sent Events (SSE)**: A technology that allows servers to push updates to clients over HTTP. This is useful for applications that need to send real-time updates without requiring full-duplex communication.
- **WebRTC**: A technology that enables peer-to-peer communication between browsers. I've used WebRTC in projects like [go2rtc-for-3dprinters](/posts/go2rtc-for-3dprinters) to facilitate real-time video streaming from 3D printer cameras.
- **GraphQL Subscriptions**: An extension of GraphQL that allows clients to subscribe to real-time updates from the server. This is useful for applications that require dynamic data updates and can be integrated with WebSockets for efficient communication.

## Projects

The primary projects I've worked on that utilize these technologies include:
- [**Club Voting System**](https://github.com/ProgSoc/ClubVotingSystem): A web application that allows members of the UTS Programmers' Society to vote on club matters in real-time. The system uses tRPC and WebSockets to provide instant feedback on voting results.
- [**FuzzJudge**](https://github.com/ProgSoc/FuzzJudge): A competitive programming platform that provides real-time score updates and feedback to participants. The application leverages GraphQL Subscriptions over WebSockets to deliver live score updates during contests.

## Conclusion

Having to solve challenges involving long-lived connections, data synchronization, and real-time user interactions has been extremely interesting. By exploring some of the different technologies prevalent in real-time web applications, I've taught myself a lot about how to build responsive and interactive web applications that can handle real-time data efficiently as well as the trade-offs involved in choosing one technology over another based on the specific requirements of a project.