---
title: createHLSStream
keywords: api
sidebar: api_sidebar
permalink: createHLSStream.html
folder: api
toc: false
---

Create a HTTP Live Stream (HLS) out of an existing H.264/AAC stream.  HLS is used to stream live feeds to iOS devices such as iPhones and iPads. 



## API Parameter Table

|    Parameter Name    |  Type   | Mandatory |              Default Value               | Description                              |
| :------------------: | :-----: | :-------: | :--------------------------------------: | ---------------------------------------- |
|   localStreamNames   | string  |   true    |                  *null*                  | The stream(s) that will be used as the input. This is a comma-delimited list of active stream names (local stream names) |
|     targetFolder     | string  |   true    |                  *null*                  | The folder where all the *.ts/*.m3u8 files will be stored. This folder must be accessible by the HLS clients. It is usually in the web-root of the server |
|      keepAlive       | boolean |   false   |                 1 *true*                 | If **true**, the EMS will attempt to reconnect to the stream source if the connection is severed |
| overwriteDestination | boolean |   false   |                 1 *true*                 | If **true**, it will force overwrite of destination files |
| staleRetentionCount  | integer |   false   | *if not specified, it will have the value of playlistLength* | The number of old files kept besides the ones listed in the current version of the playlist. Only applicable for **rolling** playlists |
| createMasterPlaylist | boolean |   false   |                 1 *true*                 | If **true**, a master playlist will be created |
|  cleanupDestination  | boolean |   false   |                0 *false*                 | If **true**, all *.ts and *.m3u8 files in the target folder will be removed before HLS creation is started |
|      bandwidths      | integer |   false   |                    0                     | The corresponding bandwidths for each stream listed in `localStreamNames`. Again, this can be a comma-delimited list |
|      groupName       | string  |   false   | *it will be a random name in the form of hls_group_xxxx* | The name assigned to the HLS stream or group. If the `localStreamNames` parameter contains only one entry and `groupName` is not specified,`groupName` will have the value of the input stream name |
|     playlistType     | string  |   false   |                appending                 | Either **appending** or **rolling**. Appending playlist will create a playlist continuously while rolling playlist will depend on the playListLength. |
|    playlistLength    | integer |   false   |                    10                    | The number of fragments before the server starts to overwrite the older fragments. Used only when `playlistType` is **rolling**. Ignored otherwise |
|     playlistName     | string  |   false   |              playlist.m3u8               | The file name ofthe playlist (*.m3u8)    |
|     chunkLength      | integer |   false   |                    10                    | The length (in seconds) of each playlist element (*.ts file). Minimum value is 1 (second) |
|    maxChunkLength    | integer |   false   |                    0                     | This parameter represents the maximum length, in seconds, the EMS will allow anysingle chunk to be. This is primarily in the case of `chunkOnIDR=true`where the EMS will wait for the next key-frame. If the `maxChunkLength` is less than `chunkLength`, the parameter shall be ignored |
|    chunkBaseName     | string  |   false   |                 segment                  | The base name used to generate the *.ts chunks |
|      chunkOnIDR      | boolean |   false   |                 1 *true*                 | If **true**, chunking is performed ONLY on IDR. Otherwise, chunking is performed whenever chunk length is achieved |
|       drmType        | string  |   false   |                   none                   | Sets the type of DRM encryption to use.  Options are: **none** (no encryption), **evo** (AES Encryption),**SAMPLE-AES** (Sample-AES), **verimatrix**(Verimatrix DRM). For Verimatrix DRM, the “drm” section of the config.lua file must be active and properly configured |
|     AESKeyCount      | integer |   false   |                    5                     | Specifies the number of keys that will be automatically generated and rotated over while encrypting this HLS stream |
|      audioOnly       | boolean |   false   |                0 *false*                 | Specifies if the resulting stream will be audio only. A value of 1(true) will result in a stream without video |
|      hlsResume       | boolean |   false   |                0 *false*                 | If **true**, HLS will resume in appending segments to previously created childplaylist even in cases of EMS shutdown or cut off stream source |
|    cleanupOnClose    | boolean |   false   |                0 *false*                 | If **true**, corresponding HLS files to a stream will be deleted if the said stream is removed or shut down or disconnected |
|     useByteRange     | boolean |   false   |                0 *false*                 | If **true**, will use the EXT-X-BYTERANGE feature of HLS (version 4 and up) |
|      fileLength      | integer |   false   |                0 *false*                 | When using `useByteRange=1`, this parameter needs to be set too. This will be the size of file before chunking it to another file, this replace the`chunkLength` in case of EXT-X-BYTERANGE, since `chunkLength` will be the byte range chunk |
|    useSystemTime     | boolean |   false   |                0 *false*                 | If **true**, uses UTC in playlist time stamp otherwise will use the local server time |
|      offsetTime      | integer |   false   |                    0                     |                                          |
|     startOffset      | integer |   false   |                    0                     | A parameter valid only for HLS v.6 onwards. This will indicate the start offset time (in seconds) for the playback of the playlist |





## API Call Template

``` 
createHLSStream localStreamname=<localStreamName> targetfolder=<webrootFolder> groupname=<groupName>
```



### Sample API Call

``` 
createHLSStream localstreamnames=testpullStream targetfolder=../evo-webroot groupname=testHLS playlisttype=rolling
```



### Success Response in JSON

``` 
{
"data":{
    "AESKeyCount":5,
    "audioOnly":false,
    "bandwidths":[128],
    "chunkBaseName":"segment",
    "chunkLength":10,
    "chunkOnIDR":true,
    "cleanupDestination":false,
    "cleanupOnClose":false,
    "configIds":[7],
    "createMasterPlaylist":true,
    "drmType":"none",
    "fileLength":0,
    "groupName":"testHLS",
    "hlsResume":false,
    "hlsVersion":3,
    "keepAlive":true,
    "localStreamNames":["testpullStream"],
    "maxChunkLength":0,
    "offsetTime":0,
    "overwriteDestination":true,
    "playlistLength":10,
    "playlistName":"playlist.m3u8",
    "playlistType":"rolling",
    "staleRetentionCount":10,
    "startOffset":0,
    "targetFolder":"..\/evo-webroot",
    "useByteRange":false,
    "useSystemTime":false
},
"description":"HLS stream created",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - AESKeyCount - the number of keys that will be automatically generated and rotated over while encrypting this HLS stream
  - audioOnly - If true, the EMS will only stream audio
  - bandwidths – An array of integersspecifying the bandwidths used for streaming
  - chunkBaseName– The base name or prefix used for naming the output HLS chunks
  - chunkLength – The length (in seconds) of each playlist element (.ts files)
  - chunkOnIDR – If **true**, chunking was made on IDR boundary
  - cleanupDestination – If **true**, HLS files at the target folder were deleted before HLS creation began
  - cleanupOnClose - If **true**, corresponding hls files to a stream will be deleted if the stream is disconnected
  - configIDs – The configuration IDs for this command
  - createMasterPlaylist–If **true**, a master playlist is created
  - drmType - The type of DRM encryption used
  - fileLength - The size of file before chunking it to another file, this replace the `chunkLength` in case of **EXT-X-BYTERANGE**
  - groupName –  The name of the target folder where HLS files will be created
  - hlsResume – If **true**, will resume in appendingsegments to previously created child playlist even in cases of EMS shutdown or cut off stream source
  - hlsVersion – The configured HLS version
  - keepAlive–  If **true**, the stream will attempt to reconnect if the connection is severed
  - localStreamNames– An array of local names for the streams
  - maxChunkLength - The maximum length the EMS willallow any single chunk to be
  - offsetTime - ??
  - overwriteDestination –  If **true**, forced overwrite was enabled during HLS creation
  - playlistLength – The number of elements in the playlist. Useful only for rolling playlistType
  - playlistName– The file name of the playlist (*.m3u8)
  - playlistType – Either **appending** or **rolling**
  - staleRetentionCount – The number of old files kept besides the ones listed in the current version of the playlist. Only applicable for **rolling** playlist
  - startOffset - Indicates the start offset time (in seconds) for the playback of the playlist
  - targetFolder–The folder where all the .ts /.m3u8 files are stored
  - useByteRange - Enables the use the **EXT-X-BYTERANGE** feature of HLS (version 4 and up)
  - useSystemTime - Determine what time stamp is used in playlist
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- Make sure that **HLS version** is properly configured in config.lua before running EMS
- If you wan't your playlist to start at the very beginning, issue the `createHLSStream` first before `pullStream` command
- If using autoHLS, take note that the following parameter values will not be modified:
  - keepAlive - will always be false
  - cleanupDestination - will always be true
  - createMasterPlaylist - will always be false
  - overwriteDestination - will always be true
  - playlistType - will always be "rolling"

------
## Related Links

- [hlsVersion](userguide_configlua.html#hlsversion)
- [Adding Streams](userguide_add.html#adding-http-streams)
- [Create HLS Stream](userguide_createhls.html)
- [autoHLS](userguide_configlua.html#autodashhlshdsmss)
