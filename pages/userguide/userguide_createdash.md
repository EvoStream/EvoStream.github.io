---
title: Create DASH Stream
keywords: dash
sidebar: userguide_sidebar
permalink: userguide_createdash.html
folder: userguide
toc: true
---

Create Dynamic Adaptive Streaming over HTTP (DASH) out of an existing H.264/AAC stream. DASH was developed by the Moving Picture Experts Group (MPEG) to establish a standard for HTTP adaptive-bitrate streaming that would be accepted by multiple vendors and facilitate interoperability.



## How To

### Single Stream

**General Format:**

```
createDASHStream localstreamnames=<localstreamname> bandwidths=<bandwidth> targetFolder=<target_folder_path> groupname=<groupname>
```

- **For Windows:**

  ```
  createDASHStream localstreamnames=myStream bandwidths=51265536 targetfolder=C:\EvoStream\evo-webroot groupname=myDASHGroup
  ```


- **For Linux Package:**

  ```
  createDASHStream localstreamnames=myStream bandwidths=51265536 targetfolder=/var/evo-webroot groupname=myDASHGroup
  ```

- **For Linux Archive:**

  ```
  createDASHStream localstreamnames=myStream bandwidths=51265536 targetfolder=/path_to_evo-webroot groupname=myDASHGroup
  ```

To make the call easier, a **relative path** can be used:

```
createDASHStream localstreamnames=myStream bandwidths=51265536 targetfolder=../evo-webroot groupname=myDASHGroup
```

The created files will automatically save in the `targetFolder` path.

```
evo-webroot:                           --> targetfolder
myDASHroup                             --> groupname
- myStream                             --> localstreamname
-- audio                               --> audio_folder
--- 51265536                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> audio_segment_file
---- segment_XXXXX.m4s                 --> audio_segment_file
-- video                               --> video_folder
--- 51265536                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> video_segment_file
---- segment_XXXXX.m4s                 --> video_segment_file
- manifest.mpd                         --> masterplaylist_file
```



### Multiple Streams

To use multiple `localStreamNames` using one **createDASHStream** command do the following:

**General Format:**

```
createDASHStream localstreamnames=<localstreamname1>,<localstreamname2>,<localstreamnameX> bandwidths=<bandwidth1,bandwidth2,bandwidthX> targetFolder=<target_folder_path> groupname=<groupname>
```

- **For Windows:**

  ```
  createDASHStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=C:\EvoStream\evo-webroot groupname=myDASHGroup
  ```

- **For Linux Package:**

  ```
  createDASHStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=/var/evo-webroot groupname=myDASHGroup
  ```

- **For Linux Archive:**

  ```
  createDASHStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=/path_to_evo-webroot groupname=myDASHGroup
  ```

To make the call easier, a **relative path** can be used:

```
createDASHStream localstreamnames=myStream1,myStream2 bandwidths=10000000,20000000 targetfolder=../evo-webroot groupname=myDASHGroup
```

The created files will automatically save in the `targetFolder` path.

```
evo-webroot:                           --> targetfolder
myDASHroup                             --> groupname
- myStream1                            --> localstreamname_1
-- audio                               --> audio_folder
--- 10000000                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> audio_segment_file
---- segment_XXXXX.m4s                 --> audio_segment_file
-- video                               --> video_folder
--- 10000000                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> video_segment_file
---- segment_XXXXX.m4s                 --> video_segment_file
- myStream2                            --> localstreamname_2
-- audio                               --> audio_folder
--- 20000000                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> audio_segment_file
---- segment_XXXXX.m4s                 --> audio_segment_file
-- video                               --> video_folder
--- 20000000                           --> bitrate_folder
---- seg_init.mp4                      --> initialization_segment
---- segment_0.m4s                     --> video_segment_file
---- segment_XXXXX.m4s                 --> video_segment_file
- manifest.mpd                         --> masterplaylist_file
```



## JSON CLI Response

**API Call:**

```
createDASHStream localstreamnames=testpullstream targetfolder=../evo-webroot groupname=dash
```

**JSON Response:**

```
Command entered successfully!
DASH stream created

    groupName: dash
    localStreamNames:
      -- testpullStream
    manifestName: manifest.mpd
    playlistType: appending
    targetFolder: ../evo-webroot
```



## Playing a DASH Manifest File

The corresponding link to play this stream would then be:

**General Format:**

```
http://<EMS_IP_Address:<Web_Server_Port>/<DASH_groupname>/<manifest_filename>
```

**Sample URL:**

- **Single Stream**

  ```
  http://192.168.2.34:8888/myHDSGroup/manifest.mpd
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



## Automatic DASH

The EMS can be configured to automatically create a DASH stream for every new inbound stream. The details for the DASH creation are placed in the `config.lua` file instead of as parameters to the `createDASHStream` API call.

```
autoDASH=
{
    targetFolder= "..\\evo-webroot",
},

```

To enable automatic DASH section in the `config.lua` file needs to be enabled and modified. See configuration [here](userguide_config.html#autoDASH/HLS/HDS/MSS).

------

## Related Links:

- [createDASHStream API](api_createDASHStream.html) 
- [Adding HTTP Streams](userguide_add.html#adding-http-streams)
- [DASH Upload Service](evowebservices_DASHupload.html)