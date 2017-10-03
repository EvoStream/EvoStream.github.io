---
title: createDASHStream
keywords: api
sidebar: api_sidebar
permalink: createDASHStream.html
folder: api
toc: false
---



Create Dynamic Adaptive Streaming over HTTP (DASH) out of an existing H.264/AAC stream. DASH was developed by the Moving Picture Experts Group (MPEG) to establish a standard for HTTP adaptive-bitrate streaming that would be accepted by multiple vendors and facilitate interoperability.



## API Parameter Table

|    Parameter Name    |  Type   | Mandatory |              Default Value               | Description                              |
| :------------------: | :-----: | :-------: | :--------------------------------------: | ---------------------------------------- |
|   localStreamNames   | string  |   true    |                  *null*                  | The stream(s) that will be used as the input. This is a comma-delimited list of active stream names (local stream names) |
|     targetFolder     | string  |   true    |                  *null*                  | The folder where all the manifest and fragment files will be stored. This folder must be accessible by the DASH clients. It is usually in the web-root of the server |
|      bandwidths      | integer |   false   |                    0                     | The corresponding bandwidths for each stream listed in `localStreamNames`. Again, this can be a comma-delimited list |
|      groupName       | string  |   false   |        *dash_group_xxxx (random)*        | The name assigned to the DASH stream or group. If the `localStreamNames` parameter contains only one entry and `groupName` is not specified, `groupName` will have the value of the input stream name |
|     playlistType     | string  |   false   |                appending                 | Either **appending** or **rolling**. Appending playlist will create a playlist continuously while rolling playlist will depend on the playListLength. |
|    playlistLength    | integer |   false   |                    10                    | The number of fragments before the server starts to overwrite the older fragments. Used only when `playlistType` is **rolling**. Ignored otherwise |
|     manifestName     | string  |   false   |               manifest.mpd               | The manifest file name                   |
|     chunkLength      | boolean |   false   |                    10                    | The length (in seconds) of each fragment. Minimum value is 1 (second) |
|      chunkOnIDR      | boolean |   false   |                 1 *true*                 | If **true**, chunking is performed ONLY on IDR. Otherwise, chunking is performed whenever chunk length is achieved |
|      keepAlive       | boolean |   false   |                 1 *true*                 | If **true**, the EMS will attempt to reconnect to the stream source if the connection is severed |
| overwriteDestination | boolean |   false   |                 1 *true*                 | If **true**, it will allow overwrite of destination files |
| staleRetentionCount  | boolean |   false   | *If not specified, it will have the value of playlistLength* | How many old files are kept besides the ones present in the current version of the playlist. Only applicable for **rolling** playlists |
|  cleanupDestination  | boolean |   false   |                0 *false*                 | If **true**, all manifest and fragment files in the target folder will be removed before DASH creation is started |
|    dynamicProfile    | boolean |   false   |                 *1 true*                 | Set this parameter to **1** (default) for a live DASH, otherwise set it to **0** for a VOD |





## API Call Template

``` 
createDASHStream localStreamname=<localStreamName> targetfolder=<webrootFolder> groupname=<groupName>
```



### Sample API Call

``` 
createDASHStream localstreamnames=testpullStream targetfolder=../evo-webroot groupname=testDASH
```



### Success Response in JSON

``` 
{
"data":{
    "bandwidths":[0],
    "chunkLength":10,
    "chunkOnIDR":true,
    "cleanupDestination":false,
    "configIds":[11],
    "dynamicProfile":true,
    "groupName":"testDASH",
    "keepAlive":true,
    "localStreamNames":["testpullStream"],
    "manifestName":"manifest.mpd",
    "overwriteDestination":true,
    "playlistLength":10,
    "playlistType":"appending",
    "staleRetentionCount":10,
    "targetFolder":". .\/evo-webroot"
},
"description":"DASH stream created",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse.
  - bandwidths – An array of integers specifying the bandwidths used for streaming
  - chunkLength – The length (in seconds) of each playlist element (.mpd files)
  - chunkOnIdr – If **true**, chunking was made on IDR boundary
  - cleanupDestination – If **true**, DASH files at the target folder were deleted before DASH creation began
  - configIds - The configuration IDs for this command
  - dynamicProfile – Tells if the DASH stream is a **live** or **VOD**
  - groupName – The name of the target folder where DASH files will be created
  - keepAlive – If **true**, the stream will attempt to reconnect if the connection is severed
  - localStreamNames – An array of local names for the streams
  - manifestName – The file name of the manifest file. If blank, defaults to **manifest**
  - overwriteDestination – If **true**, overwriting of destination files during DASH creation is allowed
  - playlistLength – The number of fragments before the server starts to overwrite the older fragments. Useful only for rolling playlist
  - playlistType – Either **appending** or **rolling**
  - staleRetentionCount – The number of old files kept besides the ones listed in the current version of the manifest. Only applicable to **rolling** playlist
  - targetFolder – The folder where all the manifest and chunk files are stored
- description – Describes the result of parsing/executing the command.
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- If you wan't your playlist to start at the very beginning, issue the `createDASHStream` first before `pullStream` command
- If using autoDASH, take note that the following parameter values will not be modified:
  - keepAlive - will always be false
  - cleanupDestination - will always be true
  - createMasterPlaylist - will always be false
  - overwriteDestination - will always be true
  - playlistType - will always be "rolling"

------

## Related Links

- [Adding Streams](userguide_add.html#adding-http-streams)
- [Create DASH Stream](userguide_createdash.html)
- [autoHLS](userguide_configlua.html#autodashhlshdsmss)
