---
title: record
keywords: api
sidebar: api_sidebar
permalink: record.html
folder: api
toc: false
---



Records any inbound stream. The `record` command allows users to record a stream that may not yet exist. When a new stream is brought into the server, it is checked against a list of streams to be recorded.



## API Parameter Table



|   Parameter Name    |  Type   | Mandatory | Default Value | Description                              |
| :-----------------: | :-----: | :-------: | :-----------: | :--------------------------------------- |
|   localStreamName   | string  |   true    |    *null*     | The name of the stream to be used as input for recording |
|     pathToFile      | string  |   true    |    *null*     | Specify path and file name to write to   |
|        type         | string  |   false   |      mp4      | **TS** or **MP4** or **FLV**             |
|      overwrite      | boolean |   false   |   0 *false*   | If **false**, when a file already exists for the stream name, a new file will be created with the next appropriate number appended. If **true**, files with the same name will be overwritten |
|      keepAlive      | boolean |   false   |   1 *true*    | If **true**, the server will restart recording every time the stream becomes available again |
|     chunkLength     | integer |   false   | 0 *disabled*  | If non-zero the record command will start a new recording file after `chunkLength` seconds have elapsed |
|     waitForIDR      | boolean |   false   |   1 *true*    | This is used if the recording is being chunked. When true, new files will only be created on IDR boundaries |
|     winQtCompat     | boolean |   false   |   0 *false*   | Mandates 32bit header fields to ensure compatibility with Windows QuickTime |
| dateFolderStructure | boolean |   false   |   0 *false*   | If **true**, folders will be created with names in **YYYYMMDD** format. Recorded files will be placed inside these folders based on the date they were created |

## API Call Template

``` 
record localStreamName=<localStreamName> pathtofile=</recording/path/fileName> type=<ts/MP4/FLV>
```



### Sample API Call

``` 
record localStreamName=testpullStream pathtofile=../media/testRecord type=mp4
```



### Success Response in JSON

``` 
{
"data":{
    "chunkLength":0,
    "computedPathToFile":"..\/media\/testRecord.mp4",
    "configId":12,
    "dateFolderStructure":false,
    "hasAudio":true,
    "keepAlive":true,
    "localStreamName":"testpullstream",
    "mp4BinPath":"..\\evo-mp4writer.exe",
    "operationType":7,
    "overwrite":true,
    "pathToFile":"..\/media\/testRecord ",
    "preset":0,
    "type":"mp4",
    "waitForIDR":false,
    "winQtCompat":true
},
"description":"Recording Stream",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - chunkLength - The length (in seconds) of each playlist element
  - computedPathToFile – The path and file name of the recorded stream
  - configID – The configuration ID for this command
  - dateFolderStructure – If **true**, will organize record chunks by date
  - hasAudio – Indicates if the recorded stream has audio, false if none
  - keepAlive – If **true**, the stream will attempt to reconnect if the connection is severed
  - localStreamName – The local name for the stream
  - mp4BinPath-??
  - operationType – The type of operation
  - overwrite – If **true**, files with the same name will be overwritten
  - pathToFile – Path to the folder where recorded files will be written
  - preset - ??
  - type – Type of file for recording. Either \`**flv**\`,\`**ts**\`, or ‘**mp4’**
  - waitForIDR – If **true**, new files will only be created on IDR boundaries
  - winQtCompat – If **true**, andates 32bit header fields to ensure compatibility with Windows QuickTime
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- If you wan't your recorded file to start at the very beginning of the stream, issue the record first before `pullStream` command


------

## Related Links

- [Record a Stream](userguide_record.html)