# PineCube

This repo is a collection of my thoughts and bring up of the Pine Cube. 


## Getting it to boot

### Pin out 
The schematics don't have alternate modes listed for the debug header. UART2 is implied to be the default. On their Wiki, there is a pinout with Alt functions. 

### Making SD card

Building seems to be not well supported, but I'm not sure if this is out of date or not. Need to look it up. 

The information provided by Pine was to use buildroot- https://wiki.pine64.org/wiki/PineCube#How_to_compile

This seemed to build fine. SD card was imaged. The serial port was on UART0. 
uBoot was reached and got to a log in prompt, but an error kept on spitting out (need to redo to check). 

Gave up with this for now. 

PineCube wiki breifly points to https://github.com/danielfullmer/pinecube-nixos

I downloaded the prebuilt and imaged my SD card. This booted fine, and no errors printed! 

SSH is active also. 

## Streaming video

Pine Wiki talks about gstreamer a lot. 

Nixos repo has an FFMPEG example using RTMP. I don't have a server I can easily use, but managed to get RTP video working using the following (heavily influenced by Daniel Fullmer's example)

```
media-ctl --set-v4l2 '"ov5640 1-003c":0[fmt:UYVY8_2X8/640x480@1/15]'
ffmpeg -s 640x480 -r 5 -i /dev/video0 -sdp_file v.sdp -f rtp "rtp://192.168.0.114:5004"
```
SCP the SDP file off the Pine Cube. 
Open up VLC, File -> Open and browse to the SDP file. 

Video should appear! 

## Next steps

 [] Build uboot, kernel and RFS. Check support for this chip. Workout why Buildroot doesn't work
 [] Get RTSP working
 [] Test IR mode
 [] Get WiFi working
 
