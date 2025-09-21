---
date: 2025-09-21
draft: false
title: "Self-Hosting: My Journey and Lessons Learned"
categories: [Self-Hosting, Open Source, Programming]
tags: [Self-Hosting, Home Lab, Servers, Linux, Docker, Kubernetes]
---

Over the past few years, I've embarked on a journey into the world of self-hosting, starting with a single instance of Home Assistant and gradually expanding my services to include a variety of applications. This journey has been both exciting and challenging, filled with valuable lessons learned along the way.

## Inspiration: The Self Hosted Podcast

I've been self-hosting for a number of years now, starting with one or two core programs and gradually expanding to host more than a dozen different services. A lot of my inspiration came from the Self Hosted podcast, which I discovered a few years ago. Every fortnight Chris and Alex would cover news in the open source and self-hosting world, as well as interviewing maintainers and covering new services that they had discovered. The podcast was a great way to learn about new tools whilst commuting and then arriving home to try them out. A lot of the services I run today were discovered through the podcast and I've learnt more than a few lessons from the hosts' experiences.

Sadly the last episode of the show was released in mid 2025 at episode 150, but the archive of episodes is still available and I often find myself going back to listen to older episodes when I'm looking for new ideas or inspiration. I'm sad to see it go but it definitely inspired me to start my own self-hosting journey and keep exploring new tools and services.

## The Beginning: Home Assistant

My self-hosting journey began with Home Assistant, a very versatile platform for smart home automation. Initially it was setup on a Raspberry Pi 3B+ which was a great way to get started without too large of an investment, letting me take advantage of the numerous integrations to control the existing smart devices in my home. Eventually Home Assistant came to live on a Raspberry Pi 4 with a 128GB Sata SSD out of an old laptop which made a huge difference in performance and reliability. So far Home Assitant has been running on that device for a couple years now without any issues.

## Expanding Services

After getting comfortable with Home Assistant I aquired an old computer from a friend that wasn't using it any more. It had a 128GB Sata SSD and 8GB of RAM which while probably not the most power efficient option was a great way to get started with hosting more services. I installed Ubuntu Server on the machine and began exploring different applications which would be useful to host myself. One of the longest running services that I ran across multiple machines was a Vaultwarden instance for password management. Having a huge array of clients and browser extensions for the first party Bitwarden service it was a no-brainer to host my own instance to avoid the subscription fees and have more control over my data. It's simple setup and low resource usage (built on Rust btw) made it a great choice for self-hosting.

Over time I kept adding new services as I discovered them with a couple making their way into my regular workflow. 

One service that became a staple of my setup was Jellyfin, a media server that allowed me to stream my personal collection of movies and the collection of DVDs that that had been sitting in storage for years. The Jellyfin ecosystem has grown a lot since I started using it with the number of new clients, plugins and integrated services making it easier and more accessible to use. The quasi-recent (at the time of writing) addition of integrated Intro-Skipping was amazing as it didn't rely on a database of known intros but instead used audio fingerprinting to detect the intro and skip it. This made it easy to use with any show without having to rely on a third party database.

## Access: Private and Public

One of the largest challenges I faced when building out the services I used was making them available outside of my home network. I wanted to be able to access services like Jellyfin and Vaultwarden whilst I wasn't at home but was reluctant to expose them to the internet without some form of verification. My go-to solution for enabling access through my home router was Cloudflare Tunnels which allowed me to run a single client application on my server that would create a secure tunnel to Cloudflare's network. This meant that I could take advantage of Cloudflare's DDoS protection and SSL termination without having to expose my home IP address or manage SSL certificates myself.

For Jellyfin I wasn't able to use tunnels (at least on the free plan) so I used Tailscale to create a VPN between my client devices and my home network. Because each device on a Tailscale network is given a unqiue IP address that could only be accessed by other devices on the same account it meant that I could securely access my Jellyfin server without having to expose it to the internet. I was able to take advantage of this private IP and wildcard DNS records to create a subdomain for my Jellyfin server that would only be accessible when connected to the Tailscale network. This made it easy for anyone I shared my Jellyfin server with via Tailscale to access it without having to worry about security or exposing my home network.

## Authentication

As my collection of services grew I ran into a bit of friction with having to manage so many different accounts and passwords. I experimented with solutions like Authentik but found it to be too complex and too resource intensive for my small scale setup. Instead I opted for a more lightweight solution with Authelia and LLDAP. Whilst Authelia didn't have the UI driven setup that Authentik was able to boast it had a well documented configuration file and examples for nearly all the services I was running. Though the user interface seemed incomplete the backend was solid and reliable, allowing for different access rules for different IP address ranges, setup of 2FA and integration with LDAP for user management.

## Email

A couple times I had a go at setting up my own email server using solutions like Mail-in-a-Box, Mailu and Mailcow. Each solution did end up working after a bit of trial and error but as anyone who you ask about hosting their own email server will tell you it's a pain to maintain and keep secure. It's a lottery whether or not your IP address is in a block list somewhere or whether Outlook or GMail will accept your emails. After a lot of frustration I ended up paying for the yearly plan for fastmail.com which has an extremely developer-friendly platform and great support for custom domains. 

## Lessons Learned

The most important lesson I've learned from my self-hosting journey is to keep things simple. Whilst it may seem easy at the time to roll a new service whenever you feel when it breaks you'll be the one who has to fix it. A balance of cloud and self-hosted services is what I ended up settling on. For services that I use daily and need to be reliable (email, password management) I opted for paid services that I could trust to be available and secure. For services that I use less frequently or for personal projects (media server, home automation) I opted for self-hosting which gave me more control and flexibility.

Overall, my self-hosting journey has been a rewarding experience that has taught me a lot about Linux, networking and system administration. While there have been challenges along the way, the satisfaction of running my own services and having control over my data has made it all worthwhile. I'm excited to continue exploring new tools and services in the future and see where my self-hosting journey takes me next.