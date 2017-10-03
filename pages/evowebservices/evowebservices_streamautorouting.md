---
title: Stream AutoRouting
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_streamautorouting.html
folder: evowebservices
toc: false
---



This web service automatically forwards a stream to another EMS via RTMP. When a new stream is brought into the EMS, either by issuing a `pullStream` or by pushing a stream into the EMS host, this web service issues an API command to automatically forward that stream to another EMS.

The AutoRouting web service has two configuration values which can be set in the config.ini file.

1. **token**. If the token is defined, and not empty, the AutoRouting web service will only forward streams to the destination that have the “token” as part of their localStreamName.

2. **destination_uri.** The address of the computer you wish to forward the streams to.

   ```
       "StreamAutoRouter": {
           "plugin_switch": "enabled",
           "parameters": {
               "token": "stream",
               "destination_uri": "192.168.2.3"
           }
       },  

   ```

In this configuration, all the localstreamnames with “**stream**” in the host EMS will forward the stream to the destination URI which is the *192.168.2.3*.

To verify, do `listStreams` on the destination server. You should see all the streams pushed to the destination.​
