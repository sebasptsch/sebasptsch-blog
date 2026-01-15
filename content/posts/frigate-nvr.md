---
date: 2026-01-15
draft: false
title: Making Analogue Cameras Smart with Frigate NVR and Home Assistant 
categories: [Self-Hosting, Open Source, Programming]
tags: [Frigate, Home Assistant, Machine Vision, Machine Learning]
---

A couple of years ago I setup Frigate NVR for the first time with just a couple of Raspberry Pi based cameras and a simple Coral USB Accelerator. Since then it's gotten a lot more refined, supporting a wide variety of different machine learning acceleration platforms and architectures.

Recently I setup Frigate on a disused Intel NUC mini pc running an 8th Generation i7 processor, certainly not lacking power but with no provisions for dedicated machine learning hardware acceleration.

The two DVRs that the cameras were attached to were simple off-the-shelf systems that supported up to eight cameras each, analog or IP. 

In total there are about twelve cameras who's feeds are passed to frigate via the DVR's RTSP streaming functionality exposing both a full-resolution main stream (720p) and a low-quality sub-stream (360p). Because of the low resolution of the cameras it drastically reduced the performance requirements and the i7 was able to support motion and object detection on the cameras provided there wasn't motion in all of them simultaneously. 

Setting up all the cameras and their re-streams was really simple, first setting up the re-streaming in the go2rtc section of the configuration file and then specifying the go2rtc stream as the primary stream for each camera.

Because of the low resolution of the cameras the 500GB internal storage was able to last about a day and a half of constant recording on all cameras before older footage started having to be deleted.

After spinning up an instance of the Home Assistant container and the Mosquitto MQTT server I installed the Frigate integration from the Home Assistant Community Store (HACS) and was able to setup notifications and alerts for person or car detection. Additionally setting up Picture Cards for the camera snapshots was extremely helpful to see a preview image of the last detection of a specific camera.

If you buy dedicated hardware to use with Frigate's hardware accelerated machine learning it also adds the ability to use [Enrichments](https://docs.frigate.video/configuration/hardware_acceleration_enrichments), additional machine learning models for different purposes like Face or License Plate Recognition.

These different enrichments can also be used in Home Assistant automations in conjunction with presence detection.

Together Home Assistant and Frigate are a perfect pair and a great solution to either modernising an old DVR or bringing advanced functionality to a cheap NVR that doesn't have object recognition capabilities.