---
title: Stream Recorder
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_streamrecorder.html
folder: evowebservices
toc: false
---



This web service tells the EMS to automatically records streams.

When a new stream is created, this web service issues an API command to automatically records the stream to an mp4 format. The user can also set how long the stream would be recorded in seconds.

The destination for the recorded file must be set in the config.ini file.

1. **file_location**. The destination location where the recorded file is saved

   **Notes:**

   - Use an absolute pathing
   - Use double slash for folder separation if using Windows OS

2. **period_time**. The period of time between pulses expressed in seconds between 1 and 86399. The maximum period_time is 86399 (24 hours).

   ```
       "StreamRecorder": {
           "plugin_switch": "enabled",
           "parameters": {
               "file_location": "C:\\EvoStream\\media",
               "period_time": 3600
           }
       },    

   ```

In this configuration, all the streams pulled by EMS will automatically be recorded in the file location indicated with a period time of 3600 seconds (60 minutes) each file as long as the plugin and or the stream is running.​
