---
title: Create HDS Stream
keywords: hds
sidebar: userguide_sidebar
permalink: userguide_createhds.html
folder: userguide
toc: true
---

Create an HDS (HTTP Dynamic Streaming) stream out of an existing H.264/AAC stream. HDS is used to stream standard MP4 media over regular HTTP connections. HDS is a new technology developed by Adobe in response to HLS from Apple.



## How To

### Single Stream

**General Format:**

```
createHDSStream localstreamnames=<localstreamname> targetFolder=<target_folder_path> groupname=<groupname>
```

- **For Windows:**

  ```
  createHDSStream localstreamnames=myStream targetfolder=C:\EvoStream\evo-webroot groupname=myHDSGroup
  ```


- **For Linux Package:**

  ```
  createHDSStream localstreamnames=myStream targetfolder=/var/evo-webroot groupname=myHDSGroup
  ```

- **For Linux Archive:**

  ```
  createHDSStream localstreamnames=myStream targetfolder=/path_to_evo-webroot groupname=myHDSGroup
  ```

To make the call easier, a **relative path** can be used:

```
createHDSStream localstreamnames=myStream targetfolder=../evo-webroot groupname=myHDSGroup
```

The created files will automatically save in the `targetFolder` path.

```
evo-webroot:                           --> targetfolder
myHDSGroup                             --> groupname
- myStream                             --> localstreamname
-- bootstrap                           --> boostrap_file
-- myStream1.f4m                       --> childplaylist_file
-- f4vSegXX-FragXX                     --> segment_chunk_file
- manifest.f4m                         --> masterplaylist_file
- manifest_v1.f4m                      --> masterplaylist_file
```



### Multiple Stream

To use multiple `localStreamNames` using one **createHLSStream** command do the following:

**General Format:**

```
createHDSStream localstreamnames=<localstreamname1>,<localstreamname2>,<localstreamnameX> targetFolder=<target_folder_path> groupname=<groupname>
```

- **For Windows:**

  ```
  createHDSStream localstreamnames=myStream1,myStream2  targetfolder=C:\EvoStream\evo-webroot groupname=myHDSGroup
  ```

- **For Linux Package:**

  ```
  createHDSStream localstreamnames=myStream1,myStream2  targetfolder=/var/evo-webroot groupname=myHDSGroup
  ```

- **For Linux Archive:**

  ```
  createHDSStream localstreamnames=myStream1,myStream2  targetfolder=/path_to_evo-webroot groupname=myHDSGroup
  ```

To make the call easier, a **relative path** can be used:

```
createHDSStream localstreamnames=myStream1,myStream2  targetfolder=../evo-webroot groupname=myHDSGroup
```

The created files will automatically save in the `targetFolder` path.

```
evo-webroot:                           --> targetfolder
myHDSGroup                             --> groupname
- myStream1                            --> localstreamname_1
-- bootstrap                           --> boostrap_file
-- myStream1.f4m                       --> childplaylist_file
-- f4vSegXX-FragXX                     --> segment_chunk_file
- myStream2                            --> localstreamname_2
-- bootstrap                           --> boostrap_file
-- myStream2.f4m                       --> childplaylist_file
-- f4vSegxx-Fragxx                     --> segment_chunk_file
- manifest.f4m                         --> masterplaylist_file
- manifest_v1.f4m                      --> masterplaylist_file
```



## JSON CLI Response

**API Call:**

```
createHDSStream localstreamnames=testpullstream targetfolder=../evo-webroot groupname=hds playlisttype=rolling
```

**JSON Response:**

```
Command entered successfully!
HDS stream created

    groupName: hds
    localStreamNames:
      -- testpullStream
    manifestName:
    playlistType: rolling
    targetFolder: ../evo-webroot
```



## Playing an HDS Playlist File

The corresponding link to play this stream would then be:

**General Format:**

```
http://<EMS_IP_Address:<Web_Server_Port>/<HDS_groupname>/<Subfolder>/<manifest_filename>
```

**Sample URL:**

- **Single Stream**

  ```
  http://192.168.2.34:8888/myHDSGroup/manifest.f4m
  ```


- **Multiple Stream**

  ```
  http://192.168.2.34:8888/myHDSGroup/myStream1/manifest.f4m
  ```

  ```
  http://192.168.2.34:8888/myHDSGroup/myStream2/manifest.f4m
  ```

  ```
  http://192.168.2.34:8888/myHDSGroup/myStream3/manifest.f4m
  ```

The player will now automatically play the stream once the HDS playlist is loaded.



## Automatic HDS

The EMS can be configured to automatically create an HDS stream for every new inbound stream. The details for the HDS creation are placed in the config.lua file instead of as parameters to the `createHDSStream` API call.

```
autoHDS=
{
    targetFolder= "..\\evo-webroot",
},
```

To enable automatic HDS a section in the `config.lua` file needs to be enabled and modified. See configuration [here](userguide_config.html#autoDASH/HLS/HDS/MSS).

------

## Related Links:

- [createHDSStream API](api_createHDSStream.html) 
- [Adding HTTP Streams](userguide_add.html#adding-http-streams)
- [HDS Upload Service](evowebservices_HDSupload.html)