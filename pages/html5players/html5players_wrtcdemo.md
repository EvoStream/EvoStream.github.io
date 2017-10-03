---
title: Playing Videos Using evoplayers.html
keywords: webrtc
sidebar: html5players_sidebar
permalink: html5players_wrtcdemo.html
folder: html5players
toc: false
---



1. To play streams from EMS using webRTC, the following command needs to be executed first on EMS. See `startWebRTC`API [here](api/startWebRTC.html):

   ```
   startwebrtc ersip=54.174.188.145 ersport=4545 roomid=MyRoom
   ```

   **Note:** The room name should be unique as much as possible, especially when using the public ERS to prevent room name conflicts. If the room name is already taken, EMS would return an error on the console logs to indicate such scenario.

   ​

2. Access the test page `demo/evoplayers.html`

   ```
   http://<WEBSERVER_IP_ADDRESS>/demo/evoplayers.html
   ```

3. Enter the **EMS IP**, **Room Name** and **Stream Name** 

4. Hit **Play** to start streaming!

   ![](images/html5/webrtc.jpg)




**Note:**

There are two players available for WebRTC. You can stream the same source or stream two different sources at the same time!



## Related Links

- [Starting WebRTC](api/startWebRTC.html)
- [Stopping WebRTC](stopWebRTC.html)

