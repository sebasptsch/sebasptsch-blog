---
title: Tuning go2rtc for 3D Printing
date: 2026-04-24
draft: false
tags: [go2rtc, 3D Printing, RTSP, WebRTC, Klipper, Raspberry Pi, OctoPrint, Mainsail]
categories: ["3D Printing", "Open Source", "Tools"]
---

Since initially setting up go2rtc on my printer's attached Raspberry Pi running klipper I've been on a quest to optimise the quality of the video stream. 

# Hardware

I began by improving the physical conditions, adding a brightness-controlled LED light bar to the top of the printer's frame right next where the webcam is mounted by connecting it to a spare screw-terminal on my mainboard.

The second major physical change was the webcam itself. Initially I setup a Logitech C270 which, as far as I can tell is one of the most popular USB webcams to use due to it's low cost and 720p resolution. For me it was the logical choice at the time as I found it in a bargain bin for the low cost of $5.

Looking for a higher resolution camera that would improve my ability to spot failures remotely I ended up with a Logitech C920 Pro which has the ability to capture 1080p at 30 frames per second with software-controlled focus (which the C270 doesn't have). 

This camera upgrade combined with improved variable lighting massively improved the theoretical image quality that I was able to achieve.

# Optimising Hardware Acceleration

Having a brand new higher reo=solution presented me with a new problem. How do I stream this higher resolution?

In my [previous post](/posts/go2rtc-for-3dprinters/) I looked at using the Raspberry Pi Compute Modudule's built-in H264 hardware encoder to preserve my precious CPU utilisation. Since then I've swapped between MJPEG and transcoded H264 streams due to the seemingly low quality of encoding that I was getting.

What I ended up finding out was that I could improve the quality of my encoding by not just by telling go2rtc to use hardware but adjusting the flags on the underlying ffmpeg command.

```yaml
streams:
    c920-src: >
      exec:ffmpeg -hide_banner -v error 
      -f alsa -channels 1 -sample_rate 16000 -i default
      -f v4l2 -input_format mjpeg -video_size 1920x1080 -framerate 10 -i /dev/video0
      -c:a libopus -application:a lowdelay -min_comp 0
      -c:v h264_v4l2m2m -tune zerolatency -b:v 4M -maxrate 4M -bufsize 8M -g 30 -pix_fmt yuv420p -bf 0 -user_agent ffmpeg/go2rtc -rtsp_transport tcp
      -f rtsp {output}
```

On the seventh line (beginning with -c:v) is where the major changes have taken place.

- `-b:v 4M` adjusts the target encoder average bitrate to 4M
- `-maxrate 4M` sets the maximum tolerance around the target bitrate
- `-bufsize 8M` sets the maximum encoder buffer size to 8M
- `-g 30` adjusts the GOP (group of pictures) setting to make a keyframe every 30 frames (1 per second at 30 frames per second), good for streaming
- `-bf` adjusts the maximum number of b-frames to zero

Combining all these settings results in a high-quality stream over WebRTC encoded in H264. Right now this stream uses quite a large amount of bandwidth and along the way I'll adjust the settings to achieve a balance of quality and bandwidth.

# Refining the stream

Because this stream is intended to only be used through Mainsail, potentially with multiple clients active at once there were a couple of modifications that really improved my experience as a user.

Something that I found out that for every stream I was opening on the client it was trying to open an additional ffmpeg stream accessing the same USB device as the previous one and therefore running into errors.

The solution that I found was to create a second stream within the go2rtc config.

```yaml
streams:
    c920-src: ... # the ffmpeg process from above
    c920: ffmpeg:c920-src # copying ffmpeg process
```

Whilst not the most optimal way to architect a configuration due to the duplicate streams so long as clients connect to only `c920` it allows the stream to scale a lot better than it did before, supporting more than one simultaneous stream.

Another improvement to the streaming workflow is to use go2rtc's built-in streaming page available at `<go2rtc url>/stream.html?src=c920` within Mainsail. This hands off the negotiation of the connection to go2rtc's built-in streaming client rather than Mainsail's implementation. This gives us the advantage of having built-in stream switching should we switch the stream to MJPEG or another format.
