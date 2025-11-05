---
title: Vaultwarden Self-Hosting Experience
date: 2025-11-05
draft: false
categories: [Self-Hosting, Tools]
tags: [Vaultwarden, Password Management, Bitwarden, Self-Hosting, Rust]
---

For almost as long as I've been self-hosting, I've been running my own instance of [Vaultwarden](https://github.com/dani-garcia/vaultwarden), previously `bitwarden-rs`. A self-contained lightweight server implementation of the Bitwarden password manager it allows me to have full control over my password data without relying on a third-party service.

## Why Self-Host?

The primary driver behind self-hosting Vaultwarden was to save on cost. Although Bitwarden has generous pricing tiers for personal use, I wanted to avoid having to pay extra money for essential features like 2FA and Passkey support. By self-hosting, I can access all these features for free while maintaining full control over my data.

## Setup and Configuration

Initially my Vaultwarden instance was set-up as a Home Assistant add-on, which was super easy to get started with. However as time went on I migrated it to a different server running Docker, which gave me more flexibility and control over the environment as well as not having to rely on my Home Assistant instance doing double-duty.

Given that Vaultwarden utilises a simple SQLite database by default and a simple configuration file it was really easy to migrate my data between instances without any issues. 

## Features and Usage

Vaultwarden supports all the core features of Bitwarden, including:
- Secure password storage
- Two-Factor Authentication (2FA)
- Password generation
- Secure notes
- Browser and mobile app integration
Additionally, Vaultwarden has support for advanced features like Passkeys, which I use regularly for any services that support them.

## Security Considerations

When self-hosting a password manager, security is paramount. There are several different services that I use to secure my Vaultwarden instance:
- **Cloudflare Tunnel**: I use Cloudflare Tunnel to securely expose my Vaultwarden instance to the internet without having to open up ports on my home network.
- **crowdsec**: I run crowdsec on my server to help protect against brute-force attacks and other malicious activity. It works by analyzing logs and blocking suspicious IP addresses.
- **Regular Backups**: I ensure that my Vaultwarden data is regularly backed up to prevent data loss in case of any issues.

## Conclusion

Overall, self-hosting Vaultwarden has been a great experience. It has allowed me to maintain control over my password data while providing all the features I need from a password manager. The ease of setup and migration, combined with the security measures I've implemented, make it a reliable and secure solution for managing my passwords.