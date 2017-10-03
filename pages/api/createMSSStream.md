---
title: createMSSStream
keywords: api
sidebar: api_sidebar
permalink: createMSSStream.html
folder: api
toc: false
---



Create a Microsoft Smooth Stream (MSS) out of an existing H.264/AAC stream. Smooth Streaming was developed by Microsoft to compete with other adaptive streaming technologies.



## API Parameter Table

|    Parameter Name    |  Type   | Mandatory |              Default Value               | Description                              |
| :------------------: | :-----: | :-------: | :--------------------------------------: | ---------------------------------------- |
|   localStreamNames   | string  |   true    |                  *null*                  | The stream(s) that will be used as the input. This is a comma-delimited list of active stream names (local stream names) |
|     targetFolder     | string  |   true    |                  *null*                  | The folder where all the manifest and fragment files will be stored. This folder must be accessible by the MSS clients. It is usually in the web-root of the server |
|      bandwidths      | integer |   false   |                    0                     | The corresponding bandwidths for each stream listed in `localStreamNames`. Again, this can be a comma-delimited list |
|      groupName       | string  |   false   |        *mss_group_xxxx (random)*         | The name assigned to the MSS stream or group. If the `localStreamNames` parameter contains only one entry and groupName is not specified,  `groupName` will have the value of the input stream name |
|     playlistType     | string  |   false   |                Appending                 | Either **appending** or **rolling**. Appending playlist will create a playlist continuously while rolling playlist will depend on the playListLength. |
|    playlistLength    | integer |   false   |                    10                    | The number of fragments before the server starts to overwrite the older fragments. Used only when`playlistType` is **rolling**. Ignored otherwise |
|     manifestName     | string  |   false   |              manifest.ismc               | The manifest file name                   |
|     chunkLength      | integer |   false   |                    10                    | The length (in seconds) of fragments to be made |
|      chunkOnIDR      | boolean |   false   |                0 *false*                 | If **true**, chunking is performed ONLY on IDR. Otherwise, chunking is performed whenever chunk length is achieved |
|      keepAlive       | boolean |   false   |                 1 *true*                 | If **true**, the EMS will attempt to reconnect to the stream source if the connection is severed |
| overwriteDestination | boolean |   false   |                 1 *true*                 | If **true**, it will allow overwrite of destination files |
| staleRetentionCount  | integer |   false   | *If not specified, it will have the value of playlistLength* | How many old files are kept besides the ones present in the current version of the playlist. Only applicable for **rolling** playlists |
|  cleanupDestination  | boolean |   false   |                0 *false*                 | If **true**, all manifest and fragment files in the target folder will be removed before MSS creation is started |
|       ismType        | string  |   false   |                   ismc                   | Either **ismc** for serving content to client or **isml** for serving content to smooth server |
|        isLive        | boolean |   false   |                 1 *true*                 | If **true**, creates a live MSS stream, otherwise set to **0** for **VOD** |
|   publishingPoint    | string  |   false   |                  *none*                  | This parameter is needed when `ismType=isml`, it is the REST URI where the mss contents will be ingested |
|      ingestMode      | string  |   false   |                  single                  | Either **single** for a non looping ingest or **loop** for looping an ingest |



## API Call Template

``` 
createMSSStream localStreamname=<localStreamName> targetfolder=<webrootFolder> groupname=<groupName>
```



### Sample API Call

``` 
createMSSStream localstreamnames=testpullStream targetfolder=../evo-webroot groupname=testMSS playlisttype=rolling
```



### Success Response in JSON

``` 
{
"data":{
    "bandwidths":[0],
    "chunkLength":10,
    "chunkOnIDR":true,
    "cleanupDestination":false,
    "configIds":[10],
    "groupName":"mss",
    "ingestMode":"single",
    “isLive”:”true”,
    "ismType":"ismc",
    "keepAlive":true,
    "localStreamNames":["testpullStream"],
    "manifestName":"manifest.ismc",
    "overwriteDestination":true,
    "playlistLength":10,
    "playlistType":"appending",
    "publishingPoint":"http://192.168.2.35:88/liveingest.isml",
    "staleRetentionCount":10,
    "targetFolder":"..\/evo-webroot"
},
"description":"MSS stream created",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - bandwidths – An array of integers specifying the bandwidths used for streaming
  - chunkLength – The length (in seconds) of each playlist element (.ismc files)
  - chunkOnIdr – If **true**, chunking was made on IDR boundary
  - cleanupDestination – If **true**, MSS files at the target folder were deleted before MSS creation began
  - configIds - The configuration IDs for this command
  - groupName – The name of the target folder where MSS files will be created
  - ingestMode – The type of ingest
  - isLive - Creates a live MSS stream, otherwise set to **0** for **VOD**
  - keepAlive – If **true**, the stream will attempt to reconnect if the connection is severed
  - localStreamNames – An array of local names for the streams
  - manifestName – The file name of the manifest file. If blank, defaults to ‘**manifest’**
  - overwriteDestination – If **true**, overwriting of destination files during MSS creation is allowed
  - playlistLength – The number of fragments before the server starts to overwrite the older fragments. Useful only for **rolling** playlist
  - playlistType – Either **appending** or **rolling**
  - publishingPoint - It is the REST URI where the mss contents will be ingested
  - staleRetentionCount – The number of old files kept besides the ones listed in the current version of the manifest. Only applicable to **rolling** playlist
  - targetFolder – The folder where all the manifest and chunk files are stored
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- If you wan't your playlist to start at the very beginning, issue the `createMSSStream` first before `pullStream` command
- If using autoMSS, take note that the following parameter values will not be modified:
  - keepAlive - will always be false
  - cleanupDestination - will always be true
  - createMasterPlaylist - will always be false
  - overwriteDestination - will always be true
  - playlistType - will always be "rolling"

------

## Related Links

- [Adding Streams](userguide_add.html#adding-http-streams)
- [Create MSS Stream](userguide_createmss.html)
- [autoMSS](userguide_configlua.html#autodashhlshdsmss)
