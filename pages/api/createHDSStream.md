---
title: createHDSStream
keywords: api
sidebar: api_sidebar
permalink: createHDSStream.html
folder: api
toc: false
---

Create an HDS (HTTP Dynamic Streaming) stream out of an existing H.264/AAC stream. HDS is used to stream standard MP4 media over regular HTTP connections. HDS is a new technology developed by Adobe in response to HLS from Apple.



## API Parameter Table

|    Parameter Name    |  Type   | Mandatory |              Default Value               | Description                              |
| :------------------: | :-----: | :-------: | :--------------------------------------: | ---------------------------------------- |
|   localStreamNames   | string  |   true    |                  *null*                  | The stream(s) that will be used as the input. This is a comma-delimited list of active stream names (local stream names) |
|     targetFolder     | string  |   true    |                  *null*                  | The folder where all the manifest (*.f4m) and fragment (f4v*) files will be stored. This folder must be accessible by the HDS clients. It is usually in the web-root of the server |
|      bandwidths      | integer |   false   |                    0                     | The corresponding bandwidths for each stream listed in `localStreamNames`. Again, this can be a comma-delimited list |
|    chunkBaseName     | string  |   false   |                   f4v                    | The base name used to generate the fragments. The default value follows this format: **f4vSeg1-FragXXX** |
|     chunkLength      | integer |   false   |                    10                    | The length (in seconds) of fragments to be made. Minimum value is **1** (second) |
|      chunkOnIDR      | boolean |   false   |                 1 *true*                 | If **true**, chunking is performed ONLY on IDR. Otherwise, chunking is performed whenever chunk length is achieved |
|      groupName       | string  |   false   | *(if not specified, it will be a random name in the form of hds_group_xxxx)* | The name assigned to the HDS stream or group. If the `localStreamNames` parameter contains only one entry and `groupName` is not specified,`groupName` will have the value of the input stream name |
|      keepAlive       | boolean |   false   |                 1 *true*                 | If true, the EMS will attempt to reconnect to the stream source if the connection is severed |
|     manifestName     | string  |   false   |    *defaults to stream name if false*    | The manifest file name                   |
| overwriteDestination | boolean |   false   |                 1 *true*                 | If **true**, it will allow overwrite of destination files |
|     playlistType     | string  |   false   |                appending                 | Either **appending** or **rolling**. Appending playlist will create a playlist continuously while rolling playlist will depend on the playListLength. |
|    playlistLength    | integer |   false   |                    10                    | The number of fragments before the server starts to overwrite the older fragments. Used only when`playlistType` is **rolling**. Ignored otherwise |
| staleRetentionCount  | integer |   false   | *If not specified, it will have the value of playlistLength* | How many old files are kept besides the ones present in the current version of the playlist. Only applicable for **rolling** playlists |
| createMasterPlaylist | boolean |   false   |                 1 *true*                 | If **true**, a master playlist will be created |
|  cleanupDestination  | boolean |   false   |                0 *false*                 | If **true**, all manifest and fragment files in the target folder will be removed before HDS creation is started |

## API Call Template

``` 
createHDSStream localStreamname=<localStreamName> targetfolder=<webrootFolder> groupname=<groupName>
```



### Sample API Call

``` 
createHDSStream localstreamnames=testpullStream targetfolder=../evo-webroot groupname=testHDS playlisttype=rolling
```



### Success Response in JSON

``` 
{
"data":{
    "bandwidths":[0],
    "chunkBaseName":"f4v",
    "chunkLength":10,
    "chunkOnIDR":true,
    "cleanupDestination":false,
    "configIds":[9],
    "createMasterPlaylist":true,
    "groupName":"testHDS",
    "keepAlive":true,
    "localStreamNames":["testpullStream"],
    "manifestName":"",
    "overwriteDestination":true,
    "playlistLength":10,
    "playlistType":"rolling",
    "staleRetentionCount":10,
    "targetFolder":"..\/evo-webroot"
},
"description":"HDS stream created",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - bandwidths – An array of integers specifying the bandwidths used for streaming
  - chunkBaseName – The base name or prefix used for naming the output HDS chunks
  - chunkLength – The length (in seconds) of each playlist element (.f4m files)
  - chunkOnIdr – If **true**, chunking was made on IDR boundary
  - cleanupDestination – If **true**, HDS files at the target folder were deleted before HDS creation began
  - configIds - The configuration IDs for this command
  - createMasterPlaylist – If **true**, a master playlist is created
  - groupName – The name of the target folder where HDS files will be created
  - keepAlive – If **true**, the stream will attempt to reconnect if the connection is severed
  - localStreamNames – An array of local names for the streams
  - manifestName – The file name of the manifest file (*.f4m). If blank, defaults to stream name
  - overwriteDestination – If **true**, overwriting of destination files during HDS creation is allowed
  - playlistLength – The number of fragments before the server starts to overwrite the older fragments. Useful only for **rolling** playlist
  - playlistType – Either **appending** or **rolling**
  - staleRetentionCount – The number of old files kept besides the ones listed in the current version of the playlist. Only applicable for **rolling** playlist
  - targetFolder – The folder where all the manifest (*.f4m) and fragment (f4v*) files are stored
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------
## Notes

- If you wan't your playlist to start at the very beginning, issue the `createHDSStream` first before `pullStream` command
- If using autoHDS, take note that the following parameter values will not be modified:
  - keepAlive - will always be false
  - cleanupDestination - will always be true
  - createMasterPlaylist - will always be false
  - overwriteDestination - will always be true
  - playlistType - will always be "rolling"

------

## Related Links

- [Adding Streams](userguide_add.html#adding-http-streams)
- [Create HDS Stream](userguide_createhds.html)
- [autoHDS](userguide_configlua.html#autodashhlshdsmss)
