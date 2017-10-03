---
title: pushStream
keywords: api
sidebar: api_sidebar
permalink: pushStream.html
folder: api
toc: false
---



This will try to push a local stream to an external destination. The pushed stream can only use the RTMP, RTSP or MPEG-TS unicast/multicast protocol. 



## API Parameter Table

|     Parameter Name     |  Type   | Mandatory |        Default Value        | Description                              |
| :--------------------: | :-----: | :-------: | :-------------------------: | ---------------------------------------- |
|          uri           | string  |   true    |           *null*            | The URI of the external stream. Can be RTMP, RTSP or unicast/multicast (d) mpegts |
|       keepAlive        | boolean |   false   |          1 *true*           | If `keepAlive` is set to **true**, the server will attempt to re-establish connection with a stream source after a connection has been lost. The reconnect will be attempted once every second |
|    localStreamName     | string  |   true    |           *null*            | The name of the stream to be pushed      |
|    targetStreamName    | string  |   false   |           *null*            | The name of the stream at destination. If not provided, the target stream name will be the same as the local stream name |
|    targetStreamType    | string  |   false   |            live             | It can be one of following: **live**, **record**, **append**. It is meaningful only for RTMP |
|         tcUrl          | string  |   false   |    *zero-length string*     | When specified, this value will be used to set the TC URL in the initial RTMPconnect invoke |
|        pageUrl         | string  |   false   |    *zero-length string*     | When specified, this value will be used to set the originating web page address inthe initial RTMP connect invoke |
|         swfUrl         | string  |   false   |    *zero-length string*     | When specified, this value will be used to set the originating swf URL in the initial RTMP connect invoke |
|          ttl           | integer |   false   | *operating system supplied* | Sets the IP_TTL (Time to Live) option on the socket |
|          tos           | integer |   false   | *operating system supplied* | Sets the IP_TOS (Type of Service) option on the socket |
|    emulateUserAgent    | string  |   false   |     *EvoStream message*     | When specified, this value will be used as the user agent string. It is meaningful only for RTMP |
| rtmpAbsoluteTimestamps | boolean |   false   |          0 *false*          | Forces the timestamps to be absolute when using RTMP |
|  sendChunkSizeRequest  | boolean |   false   |          1 *true*           | Sets whether the RTMP stream will or will not send a “Set Chunk Length” message.  This is significant when pushing to Akamai’s new RTMP HD ingest point where this parameter should be set to 0 so that Akamai will not drop the connection |
|      useSourcePts      | boolean |   false   |          0 *false*          | When value is true, timestamps on source inbound RTMP stream are passed directly to the outbound (pushed) RTMP streams. This affects only pushed Outbound Net RTMP with net RTMP source.  This parameter overrides the value of the config.lua option of the same name |
|       httpProxy        | string  |   false   |    *zero-length string*     | This parameter has two valid values: **IP:Port** – This value combination specifies an RTSP HTTP Proxy from which the RTSP stream should be pulled from **Self** - Specifying “self” as the value implies pulling RTSP over HTTP |





## API Call Template

``` 
pullStream uri=<AddressOfStream> localStreamname=<localStreamName> targetStreamName=<targetStreamName>
```



### Sample API Call

``` 
pushStream uri=rtmp://1.2.3.4/live localStreamName=testpullStream targetStreamName=testpushStream 
```



### Success Response in JSON

``` 
{
"data":{
    "configId":6,
    "emulateUserAgent":"EvoStream Media Server (www.evostream.com)",
    "forceTcp":false,
    "httpProxy":"",
    "keepAlive":true,
    "localStreamName":"testpullStream",
    "operationType":2,
    "pageUrl":"",
    "rtmpAbsoluteTimestamps":false,
    "sendChunkSizeRequest":true,
    "swfUrl":"",
    "targetStreamName":"testpushStream",
    "targetStreamType":"live",
    "targetUri":{
        "document":"",
        "documentPath":"\/",
        "documentWithFullParameters":"",
        "fullDocumentPath":"\/",
        "fullDocumentPathWithParameters":"\/",
        "fullParameters":"",
        "fullUri":"rtmp:\/\/127.0.0.1",
        "fullUriWithAuth":"rtmp:\/\/127.0.0.1",
        "host":"localhost",
        "ip":"127.0.0.1",
        "originalUri":"rtmp:\/\/localhost",
        "parameters":{
        },
        "password":"",
        "port":1935,
        "portSpecified": false,
        "scheme":"rtmp",
        "userName":""
        },
    "tcUrl":"",
    "tos":256,
    "ttl":256,
    "useSourcePts":false
},
"description":"Local stream testpullStream enqueued for pushing to rtmp:\/\/localhost as testpushStream",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response for pullStream contains the following details:

- data – The data to parse
  - configID – The configuration ID for this command
  - emulateUserAgent – This is the string that the EMS uses to identify itself with the other server.  It can be modified so that EMS identifiesitself as, say, a Flash Media Server
  - forceTcp – Whether TCP MUST be used, or if UDP can be used
  - httpProxy - May either be **IP:Port** combination or **self**
  - keepAlive – If **true**, the stream will attempt to reconnect if the connection is severed
  - localStreamName – The local name for the stream
  - operationType – The type of operation
  - pageUrl – A link to the page that originated the request (often unused)
  - rtmpAbsoluteTimeStamps – If **true**, forces the timestamps to be absolute when using RTMP
  - sendChunkSizeRequest – Indicates whether theRTMP stream will or will not send a “Set Chunk Length” message
  - swfUrl – The location of the Flash Client thatis generating the stream (if any)
  - tcUrl – An RTMP parameter that is essentially acopy of the URI
  - tos – Type of Service network flag
  - ttl – Time To Live network flag
  - targeturi – Contains key/value pairs describing the source stream’s URI
    - document – The document name of the sourcestream
    - documentPath – The document path of the sourcestream
    - documentWithFullParameters – The document name with parameters of the source stream
    - fullDocumentPath - The document path of thedestination stream
    - fullDocumentPathWithParameters - The documentpath with parameters of the destination stream
    - fullParameters – The parameters for the sourcestream’s URI
    - fullUri – The full URI of the source stream
    - fullUriWithAuth – The full URI with authenticationof the source stream
    - host – Name of the source stream’s host
    - ip – IP address of the source stream’s host
    - originalUri – The source stream’s URI where itwas generated
    - parameters – Parameters for the source stream’sURI (if any)
    - password – Password for authenticating thesource stream (if required)
    - port – Port used by the source stream
    - portSpecified – True if the port for the sourcestream is specified
    - scheme – The protocol used by the source stream
    - userName – The user name for authenticating thesource stream (if required)
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [Sending Streams](userguide_send.html)
- [Push a Stream](userguide_pushstream.html)