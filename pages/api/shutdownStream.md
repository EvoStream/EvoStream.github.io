---
title: shutdownStream
keywords: api
sidebar: api_sidebar
permalink: shutdownStream.html
folder: api
toc: false
---

Terminates a specific stream. When `permanently=1` is used, this command is analogous to`removeConfig`.



## API Parameter Table

| Parameter Name  |  Type   | Mandatory |    Default Value     | Description                              |
| :-------------: | :-----: | :-------: | :------------------: | ---------------------------------------- |
|       id        | integer |   true    |         null         | The unique Id of the stream that needs to be terminated. The stream ID’s can be obtained using the `listStreams` command. This parameter is not mandatory but either this or `localStreamName` should be present to identify the particular stream |
| localStreamName | string  |   true    | *zero length string* | The name of the inbound stream which you wish to terminate. This will also terminate any outbound streams that are dependent upon this input stream. This parameter is not mandatory but either this or the id should be present to identify the particular stream |
|   permanently   | boolean |   false   |       1 *true*       | If **true**, the corresponding push/pull configuration will also be terminated. Therefore, the stream will NOT be reconnected when the server restarts |

## API Call Template

``` 
shutdownstream id=<configId>
```

OR

``` 
shutdownstream localStreamName=<localStreamName>
```



### Sample API Call

``` 
shutdownstream localStreamName=testpullStream permanently=1
```



### Success Response in JSON

``` 
{
"data":{
    "protocolStackInfo":{
    "carrier":{
    "farIP":"54.239.131.57",
    "farPort":1935,
    "id":601,
    "nearIP":"192.168.2.35",
    "nearPort":2326,
    "rx":3077367,
    "tx":3653,
    "type":"IOHT_TCP_CARRIER"
    },
    "stack":[
    {
    "applicationId":0,
    "creationTimestamp":1448008702269.8640,
    "id":794,
    "isEnqueueForDelete":false,
    "queryTimestamp":1448008724139.1150,
    "type":"TCP"
    },
    {
    "applicationId":1,
    "creationTimestamp":1448008702269.8640,
    "id":795,
    "isEnqueueForDelete":false,
    "queryTimestamp":1448008724139.1150,
    "rxInvokes":31,
    "serverAgent":"FMS\/3,5,7,7009",
    "streams":[
    {
    "appName":"evostreamms",
    "audio":{
        "bytesCount":348883,
        "codec":"AAAC",
        "codecNumeric":4702111241970122752,
        "droppedBytesCo unt":0,
        "droppedPacketsCount":0,
        "packetsCount":1068
        },
    "bandwidth":0,
    "connectionTyp e":1,
    "creationTimestamp":1448008702871.8989,
    "farIp":"54.239.131.57",
    "farPort":1935,
    "ip":"192.168.2.35",
    "name":"testpullstream",
    "nearIp":"192.168.2.35",
    "nearPort ":2326,
    "outStreamsUniqueIds":[91],
    "pageUrl":"",
    "port":2326,
    "processId":12848,
    "processType":"origin",
    "pullSettings":{
    "_callback":null,
    "audioCodecBytes":"",
    "configId":1,
    "emulateUserAgent":"EvoStream Media Server (www.evostream.com) player",
    "forceTcp":false,
    "httpProxy":"",
    "isAudio":true,
    "keepAlive":true,
    "localStreamName":"testpullstream",
    "operationType":1,
    "pageUrl":"",
    "ppsBytes":"",
    "rangeEnd":-1,
    "ran geStart":-2,
    "rtcpDetectionInterval":10,
    "sendRenewStream":false,
    "spsBytes":"",
    "ss mIp":"",
    "swfUrl":"",
    "tcUrl":"",
    "tos":256,
    "ttl":256,
    "uri":"rtmp:\/\/s2pchzxmtymn2 k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4"
    },
    "queryTimestamp":1448008724139.1150,
    "serverAgent":"FMS\/3,5,7,7009",
    "swfUrl":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net \/cfx\/st\/mp4:sintel.mp4",
    "tcUrl":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4",
    "type":"INR",
    "typeNumeric":5282249572905648128,
    "uniqueId":95,
    "upTime":21267.2161,
    "video":{
        "bytesCount":2698244,
        "codec":"VH264",
        "codecNumeric":6217274493967007744,
        "droppedBytesCount":0,
        "droppedPacketsCount":0,
        "height":306,
        "level":30,
        "packetsCount":596,
        "profile":66,
        "width":720
        }
    }
    ],
    "txInvokes":7,
    "type":"OR"
    }
    ]
    },
    "streamInfo":{
        --Same with streams group
        }
    }
},
"description":"Stream closed",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - protocolStackInfo – Contains key/value pairs describing the protocol stack used by the stream
    - carrier – Details about the connection itself
      - farIP – The IP address of the distant party
      - farPort – The port used by the distant party
      - nearIP – The IP address used by the local computer
      - nearPort – The port used by the local computer
      - rx – Total bytes received on this connection
      - tx – Total bytes transferred on this connection
      - type – The connection type (TCP, UDP)
    - stack[1] – Describes the farthest protocol primitive
      - applicationID – the ID of the internal application using the connection
      - creationTimestamp – The time (in UNIX seconds) when the application started using the connection
      - id – The unique ID for this stack relation
      - isEnqueueForDelete – Internal flag used for cleanup
      - queryTimestamp – The time (in UNIX seconds) when this data was populated
      - type – A descriptor for how the application is using the connection
    - stack[2] – Describes the next protocol primitive.
      - applicationId – the ID of the internal application using the connection
      - creationTimestamp – The time (in UNIX seconds) when the application started using the connection
      - id – The unique ID for this stack relation
      - isEnqueueForDelete – Scheduled for deletion
      - queryTimestamp – The time (in UNIX seconds) when this data was populated
      - rxInvokes – Number of received RTMP function invokes
      - streams[1]
        - audio – Stats about the audio portion of the stream
          - bytesCount – Total amount of audio data received
          - droppedBytesCount – The number of audio bytes lost
          - droppedPacketsCount – The number of lost audio packets
          - packetsCount – Total number of audio packets received
        - bandwidth – The current bandwidth utilization of the stream
        - canDropFrames – *Outstreams only*. Flag set by client allowing for dropped frames/packets
        - creationTimestamp – The time (in UNIX secs) when the stream was created
        - inStreamUniqueId – *For pushed streams.* The id of the source stream
        - name – the `localstreamname` for this stream
        - queryTimestamp – The time (in UNIX secs) when this data was populated
        - type – The type of stream this is. See `getStreamInfo` for details
        - uniqueId – The unique ID of the stream (integer)
        - upTime – The time in seconds that the stream has been alive/running for
        - video
          - bytesCount – Total amount of video data received
          - droppedBytesCount – The number of video bytes lost
          - droppedPacketsCount – The number of lost video packets
          - packetsCount – Total number of video packets received
      - streams[2]
        - bandwidth – The current bandwidth utilization of the stream
        - creationTimestamp – The time (in UNIX secs) when the stream was created
        - name – the `localStreamName` for this stream
        - outStreamsUniqueIDs – *For pulled streams.* An array of the “out” stream IDs associated with this “in” stream.
        - queryTimestamp – The time (in UNIX secs) when this data was populated.
        - type – The type of stream this is. See `getStreamInfo` for details.
        - uniqueId – The unique ID of the stream (integer)
        - uptime – The time in seconds that the stream has been alive/running for
      - txInvokes – Number of sent RTMP function invokes
      - type – A descriptor for how the application is using the connection
  - streamInfo
    - bandwidth – The current bandwidth utilization of the stream
    - creationTimestamp – The time (in UNIX seconds) when the stream was created
    - name – the `localStreamName` for this stream
    - outStreamsUniqueIds – *For pulled streams.* An array of the “out” stream IDs associated with this “in” stream
    - queryTimestamp – The time (in UNIX seconds) when this data was populated
    - type – The type of stream this is. See `getStreamInfo` for details
    - uniqueId – The unique ID of the stream (integer)
    - upTime – The time in seconds that the stream has been alive/running for


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- The stream ID shown by the `listStreams` command is not the same as the config ID shown by the `listConfig` command. The `shutdownStream` command uses the stream ID, not the config ID.


------

## Related Links

- [removeConfig](removeConfig.html)