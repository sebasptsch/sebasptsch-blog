---
title: My Home Assistant Setup
date: 2025-11-05
draft: false
categories: [Home Automation]
tags: [Home Assistant, Home Automation, Smart Home, ESPHome, Z-Wave, Zigbee]
---

I've been using Home Assistant for several years now, since before there was a Android Mobile app (2019) and I can say that it's been an incredible journey with each update to the project bringing new features and maturity to the platform.

There are a couple things which really contributed to my experience with Home Assistant, primarily the extensive catalog of integrations and the integration of non-Home Assistant devices through ESPHome, Z-Wave, and Zigbee.

## Hardware

I began running Home Assistant on a Raspberry Pi 3b+ using the Home Assistant OS image and moved between different platforms over the years. Currently my instance is running on a Raspberry Pi 4b with 4GB of RAM, which whilst not the fastest when compiling firmware for ESPHome devices, it has been reliable and sufficient for my needs.

When using a Raspberry Pi it comes highly reccommended to use an external storage device, NVMe or Sata SSD connected to the Pi via USB. Given how much information Home Assistant stores, including logs, databases, and media files, an external SSD helps improve performance and reliability compared to using a standard microSD card.

## Protocols and Platforms

My Home Assistant setup utilises a number of different protocols and platforms to manage various smart home devices:
- **Zigbee**: For Zigbee I use a CC2652 based USB router made by [TubesZB](https://tubeszb.com/). At the time this was one of the best options available for Zigbee connectivity, offering strong performance over cheap USB sticks.
- **Z-Wave**: For Z-Wave I have a Zooz USB Stick Z-Wave 700 series. Although I don't have any Z-Wave devices at the moment, I wanted to future-proof my setup in case I decide to add any in the future.
- **ESPHome**: My favourite platform for new smart home devices. I have 8 ESPHome based devices around my home, primarily consisting of energy monitoring smart plugs along with a [standing desk controller](https://upsy-desky.tjhorner.dev/docs/introduction) and an RGBW light bulb. ESPHome makes it incredibly easy to create custom firmware for ESP8266 and ESP32 based devices, allowing for deep integration with Home Assistant.
- **Wi-Fi Devices**: Probably the most expansive of all my devices are all my Wi-Fi connected devices. This includes smart lights, plugs, cameras, and sensors from various manufacturers. Home Assistant's extensive integration support allows me to connect and manage all these devices seamlessly.

## Automations and Scenes

I've only barely scratched the surface of Home Assistant's automation capabilities. Using the mobile and other presence detection methods to adjust lighting and send context-aware notifications. 

My most used automations automate my desk setup, using Wake-on-LAN to turn on my PC when I arrive home and subsequently turning off my monitor and PC to conserve energy when I leave.

## Conclusion

Overall, my Home Assistant setup has been a rewarding experience, allowing me to create a smart home that is tailored to my needs. The flexibility and extensibility of Home Assistant, combined with the power of ESPHome, Z-Wave, and Zigbee, have made it possible to build a cohesive and efficient smart home ecosystem. I'm excited to continue exploring new devices and automations as the platform evolves.
