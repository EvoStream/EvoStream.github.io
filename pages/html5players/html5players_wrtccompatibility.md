---
title: Browser Compatibility
keywords: webrtc
sidebar: html5players_sidebar
permalink: html5players_wrtccompatibility.html
folder: html5players
toc: false
---

The following diagram shows the compatibility of various browsers with the EvoStream WebRTC feature. 

![](images/html5/proto2.png)



**Firefox Configuration Changes**

The following configuration changes must be made to Firefox before it will work with HTML5 playback and Peer to Peer:

- In the Firefox address field enter: about:config
  - Click “I’ll be careful I promise!”
- Locate the following variables and set them (double-click) as necessary to match:
  - media.mediasource.enabled = true
  - media.mediasource.whitelist = false
  - media.mediasource.mp4.enabled = true
  - media.fragmented-mp4.exposed = true
  - media.fragmented-mp4.ffmpeg.enabled = true
  - media.fragmented-mp4.gmp.enabled = true
  - media.fragmented-mp4.use-blank-decoder = false
- Restart Firefox to activate these changes




## Notes

To verify if your browser supports HTML5 player, you may check the following links:

- [https://html5test.com/](https://html5test.com/)
- [https://www.youtube.com/html5?gl=PH](https://www.youtube.com/html5?gl=PH)