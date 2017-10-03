---
title: Create HLS Stream
keywords: hls
sidebar: userguide_sidebar
permalink: userguide_createhls.html
folder: userguide
toc: true
---

Create an HTTP Live Stream (HLS) out of an existing H.264/AAC stream.  HLS is used to stream live feeds to iOS devices such as iPhones and iPads. Please see `createHLSStream` [API](api_createHLSStream.html) for more details.



## How To

### Single Stream

**General Format:**

```
createHLSStream localstreamnames=<localstreamname> targetFolder=<target_folder_path> groupname=<groupname>

```

- **For Windows:**

  ```
  createHLSStream localstreamnames=myStream targetfolder=C:\EvoStream\evo-webroot groupname=myHLSGroup
  ```


- **For Linux Package:**

  ```
  createHLSStream localstreamnames=myStream targetfolder=/var/evo-webroot groupname=myHLSGroup
  ```

- **For Linux Archive:**

  ```
  createHLSStream localstreamnames=myStream targetfolder=/path_to_evo-webroot groupname=myHLSGroup
  ```

To make call easier, a **relative path** can be used:

```
createHLSStream localstreamnames=myStream targetfolder=../evo-webroot groupname=myHLSGroup
```

The created files will automatically save in the `targetFolder` path.

```
evo-webroot:                           --> targetfolder
myHLSGroup                             --> groupname
- myStream                             --> localstreamname
-- segmentfile_1.ts                    --> segment_file
-- segmentfile_2.ts                    --> segment_file
-- segmentfile_X.ts                    --> segment_file
-- playlist.m3u8                       --> childplaylist_file
- playlist.m3u8                        --> masterplaylist_file

```



### Multiple Stream

To use multiple `localStreamNames` using one **createHLSStream** command do the following:

**General Format:**

```
createHLSStream localstreamnames=<localstreamname1>,<localstreamname2>,<localstreamnameX> targetFolder=<target_folder_path> groupname=<groupname>

```

- **For Windows:**

  ```
  createHLSStream localstreamnames=myStream1,myStream2  targetfolder=C:\EvoStream\evo-webroot groupname=myHLSGroup
  ```

- **For Linux Package:**

  ```
  createHLSStream localstreamnames=myStream1,myStream2  targetfolder=/var/evo-webroot groupname=myHLSGroup
  ```

- **For Linux Archive:**

  ```
  createHLSStream localstreamnames=myStream1,myStream2  targetfolder=/path_to_evo-webroot groupname=myHLSGroup
  ```

To make the call easier, a **relative path** can be used:

```
createHLSStream localstreamnames=myStream1,myStream2  targetfolder=../evo-webroot groupname=myHLSGroup
```

The created files will automatically save in the `targetFolder` path.

```
evo-webroot:                           --> targetfolder
myHLSGroup                             --> groupname
- myStream1                            --> localstreamname_1
-- segmentfile_1.ts                    --> segment_file
-- segmentfile_2.ts                    --> segment_file
-- segmentfile_X.ts                    --> segment_file
-- playlist.m3u8                       --> childplaylist_file_1
- myStream2                            --> localstreamname_2
-- segmentfile_1.ts                    --> segment_file
-- segmentfile_2.ts                    --> segment_file
-- segmentfile_X.ts                    --> segment_file
-- playlist.m3u8                       --> childplaylist_file_2
- playlist.m3u8                        --> masterplaylist_file
```



## JSON CLI Response

**API Call:**

```
createHLSStream localstreamnames=testpullstream targetfolder=../evo-webroot groupname=hls playlisttype=rolling
```

**JSON Response:**

```
Command entered successfully!
HLS stream created

    groupName: hls
    localStreamNames:
      -- testpullStream
    playlistName: playlist.m3u8
    playlistType: rolling
    targetFolder: ../evo-webroot
```



## Playing an HLS Playlist File

The corresponding link to use on Safari or other players to play this stream would then be:

**General Format:**

```
http://<EMS_IP_Address:<Web_Server_Port>/<HLS_groupname>/<Subfolder>/<playlist_filename>
```

**Sample URL:**

- **Single Stream**

  ```
  http://192.168.2.34:8888/myHLSGroup/playlist.m3u8
  ```


- **Multiple Stream**

  ```
  http://192.168.2.34:8888/myHLSGroup/myStream1/playlist.m3u8
  ```

  ```
  http://192.168.2.34:8888/myHLSGroup/myStream2/playlist.m3u8
  ```

  ```
  http://192.168.2.34:8888/myHLSGroup/myStream3/playlist.m3u8
  ```

The player will now automatically play the stream once the HLS playlist is loaded.



## DVR Playback

The EMS can support DVR functionality, allowing users to pause and resume playback of live streams. This capability is already built into the HLS protocol support. Simply use an “`appending`” playlist type or a “`rolling`” playlist with a sufficiently large `playlistLength` value.

Users may also create time-shifted content or scheduled content by doing “local pulls” of server side playlists.



## HLS Resume

In cases of server or stream restarts, the HLS will resume in appending segments to previously created playlists. This can be enabled by using the `hlsResume` parameter when invoking the `createHLSStream`API.

This parameter defaults to 0 (false).

Below is an example usage of the `createHLSStream` API command with the `hlsResume` parameter:

```
createHLSStream localstreamnames=MyStream targetFolder=/var/evo-webroot groupName=hls playlisttype=rolling hlsResume=1
```



## Audio Only HLS

The EMS supports audio-only HLS delivery.

The createHLSStream API has an `audioOnly` parameter that specifies if the resulting stream will have no video. This parameter defaults to 0 (false) if not specified.

An example `createHLSStream` command with the `audioOnly` parameter follows:

```
createHLSStream localstreamnames=MyStream targetFolder=/var/evo-webroot groupName=hls playlisttype=rolling audioOnly=1

```



## Encryption

**Note:** Encryption was supported on HLS version 5 and above.



### VeriMatrix DRM

The EMS supports Verimatrix DRM for HLS streams. To enable Verimatrix support for your HLS streams you must enable and modify the “drm” section of the config.lua file. Please see the [Configuration File]() for details on the “drm” section.

Once Verimatrix support is enabled in the config file, you can then conditionally add Verimatrix protection to your HLS streams. Simply add the drmType parameter on your `createHLSStream`  command:

```
createHLSStream localstreamnames=MyStream targetFolder=/var/evo-webroot groupName=hls playlisttype=rolling drmType=verimatrix	
```



### AES Encryption

The EMS supports AES encryption for HLS streams. To use AES encryption you must specify two values in the `createHLSStream` API command: the `drmType` and the `aesKeyCount`.

```
createHLSStream localstreamnames=MyStream targetFolder=/var/evo-webroot groupName=hls playlisttype=rolling drmType=ems aesKeyCount=5
```

- **drmType** is a string value that specifies the type of encryption to use (“ems” means the EvoStream AES encryption scheme).
- **aesKeyCount** is an integer value (defaulted to 5), which specifies how many AES keys will be generated, and rotated through, while encrypting the HLS Stream.




## Automatic HLS

The EMS can be configured to automatically create an HLS stream for every new inbound stream. The details for the HLS creation are placed in the config.lua file instead of as parameters to the `createHLSStream` API call.

```
autoHLS=
{
    targetFolder= "..\\evo-webroot",
},
```

To enable automatic HLS a section in the `config.lua` file needs to be enabled and modified. See configuration  [here](userguide_config.html#autoDASH/HLS/HDS/MSS).

------

## Related Links:

- [createHLSStream API](api_createHLSStream.html) 
- [Adding HTTP Streams](userguide_add.html#adding-http-streams)
- [HLS Upload Service](evowebservices_HLSupload.html)