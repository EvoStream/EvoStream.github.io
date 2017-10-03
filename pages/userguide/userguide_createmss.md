---
title: Create MSS Stream
keywords: mss
sidebar: userguide_sidebar
permalink: userguide_createmss.html
folder: userguide
toc: true
---

Create an MSS (Microsoft Smooth Streaming). From Microsoft, "If the Internet bandwidth and video rendering capability on your playback device are sufficiently high, you'll experience high-definition video playback of the sample content. You will also be able to simulate end user experiences under varying conditions by simulating drops and recoveries in bandwidth." See [more](https://www.iis.net/media/experiencesmoothstreaming).



## How To

### Single Stream

**General Format:**

```
createMSSStream localstreamnames=<localstreamname> bandwidths=<bandwidth> targetFolder=<target_folder_path> groupname=<groupname>
```

- **For Windows:**

  ```
  createMSSStream localstreamnames=myStream bandwidths=51265536 targetfolder=C:\EvoStream\evo-webroot groupname=myMSSGroup
  ```


- **For Linux Package:**

  ```
  createMSSStream localstreamnames=myStream bandwidths=51265536 targetfolder=/var/evo-webroot groupname=myMSSGroup
  ```

- **For Linux Archive:**

  ```
  createMSSStream localstreamnames=myStream bandwidths=51265536 targetfolder=/path_to_evo-webroot groupname=myMSSGroup
  ```

To make the call easier, a **relative path** can be used:

```
createMSSStream localstreamnames=myStream bandwidths=51265536 targetfolder=../evo-webroot groupname=myMSSGroup
```

The created files will automatically save in the `targetFolder` path.

```
evo-webroot:                            --> targetfolder
myMSSGroup                              --> groupname
- myStream                              --> localstreamname
-- audio                                --> audio_folder
--- 51265536                            --> bitrate_folder
---- XXXXXXXXXX000.fmp4                 --> audio_segment_file
---- XXXXXXXXXXXXX.fmp4                 --> audio_segment_file
-- video                                --> video_folder
--- 51265536                            --> bitrate_folder
---- XXXXXXXXXX000.fmp4                 --> video_segment_file
---- XXXXXXXXXXXXX.fmp4                 --> video_segment_file
- manifest.ismc                         --> manifest_file
```



### Multiple Stream

To use multiple `localStreamNames` using one **createMSSStream** command do the following:

**General Format:**

```
createMSSStream localstreamnames=<localstreamname1>,<localstreamname2>,<localstreamnameX> bandwidths=<bandwidth1,bandwidth2,bandwidthX> targetFolder=<target_folder_path> groupname=<groupname>
```

- **For Windows:**

  ```
  createMSSStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=C:\EvoStream\evo-webroot groupname=myMSSGroup
  ```

- **For Linux Package:**

  ```
  createMSSStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=/var/evo-webroot groupname=myMSSGroup
  ```

- **For Linux Archive:**

  ```
  createMSSStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=/path_to_evo-webroot groupname=myMSSGroup
  ```

To make the call easier, a **relative path** can be used:

```
createMSSStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=../evo-webroot groupname=myHDSGroup
```

The created files will automatically save in the `targetFolder` path.

```
evo-webroot:                           --> targetfolder
myMSSGroup                             --> groupname
- 10000000                             --> bitrate_folder_1
-- audio                               --> audio_folder
--- xxxxxxxxxx000.fmp4                 --> fmp4_audio_file
--- xxxxxxxxxxxxx.fmp4                 --> fmp4_audio_file
-- video                               --> video_folder
--- xxxxxxxxxx000.fmp4                 --> fmp4_video_file
--- xxxxxxxxxxxxx.fmp4                 --> fmp4_video_file
- 20000000                             --> bitrate_folder_2
-- audio                               --> audio_folder
--- xxxxxxxxxx000.fmp4                 --> fmp4_audio_file
--- xxxxxxxxxxxxx.fmp4                 --> fmp4_audio_file
-- video                               --> video_folder
--- xxxxxxxxxx000.fmp4                 --> fmp4_video_file
--- xxxxxxxxxxxxx.fmp4                 --> fmp4_video_file
- manifest.ismc                        --> manifest_file
```



## JSON CLI Response

**API Call:**

```
createMSSStream localstreamnames=testpullstream,testpullstream bandwidths=10000000,20000000 targetfolder=../evo-webroot groupname=mss playlisttype=rolling
```

**JSON Response:**

```
Command entered successfully!
MSS stream created

    groupName: mss
    localStreamNames:
      -- testpullStream
    manifestName: manifest.ismc
    playlistType: rolling
    targetFolder: ../evo-webroot
```



## Playing an MSS Manifest File

The corresponding link to play this stream would then be:

**General Format:**

```
http://<EMS_IP_Address:<Web_Server_Port>/<MSS_groupname>/<manifest_filename>
```

**Sample URL:**

- **Single Stream**

  ```
  http://192.168.2.34:8888/myMSSGroup/manifest.ismc
  ```


- **Multiple Stream**

  ```
  http://192.168.2.34:8888/myMSSGroup/myStream1/manifest.ismc
  ```

  ```
  http://192.168.2.34:8888/myMSSGroup/myStream2/manifest.ismc
  ```

  ```
  http://192.168.2.34:8888/myMSSGroup/myStream3/manifest.ismc
  ```

The player will now automatically play the stream once the MSS manifest is read.



## Automatic MSS

The EMS can be configured to automatically create an MSS stream for every new inbound stream. The details for the MSS creation are placed in the config.lua file instead of as parameters to the `createMSSStream` API call.

```
autoMSS=
{
    targetFolder= "..\\evo-webroot",
},

```

To enable automatic MSS a section in the `config.lua` file needs to be enabled and modified. See configuration [here](userguide_config.html#autoDASH/HLS/HDS/MSS).

------

- [createMSSStream API](api_createMSSStream.html) 
- [Adding HTTP Streams](userguide_add.html#adding-http-streams)