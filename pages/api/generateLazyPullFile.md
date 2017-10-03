---
title: generateLazyPullFile
keywords: api
sidebar: api_sidebar
permalink: generateLazyPullFile.html
folder: api
toc: false
---



Will create a VOD file which contains details of the stream to be pulled when the file is requested.



## API Parameter Table

|    Parameter Name     |  Type   |                Mandatory                 |        Default Value        | Description                              |
| :-------------------: | :-----: | :--------------------------------------: | :-------------------------: | ---------------------------------------- |
|          uri          | string  |                   true                   |           *null*            | The URI of the external stream. Can be RTMP, RTSP or unicast/multicast (d) mpegts |
|      pathToFile       | string  |                   true                   |           *null*            | The path where the file will be saved, with a “.vod” extension. |
|       forceTcp        | boolean |                  false                   |          1 *true*           | If **true** and if the stream is RTSP, a TCP connection will be forced.  Otherwise the transport mechanism will be negotiated (UDP or TCP) |
|         tcUrl         | string  |                  false                   |    *zero-length string*     | When specified, this value will be used to set the TC URL in the initial RTMP connect invoke |
|        pageUrl        | string  |                  false                   |    *zero-length string*     | When specified, this value will be used to set the originating web page address in the initial RTMP connect invoke |
|        swfUrl         | string  |                  false                   |    *zero-length string*     | When specified, this value will be used to set the originating swf URL in the initial RTMP connect invoke |
|      rangeStart       | integer |                  false                   |             -2              | For RTSP and RTMP connections.  A value from which the playback should start expressed in seconds. There are 2 special values: **-2** and **-1**. For more information, please read about start/len parameters [here:](http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.html]) |
|       rangeEnd        | integer |                  false                   |             -1              | The length in seconds for the playback. **-1** is a special value. For more information, please read about start/len parameters [here:][http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.htm] |
|          ttl          | integer |                  false                   | *operating system supplied* | Sets the IP_TTL (Time to Live) option on the socket |
|          tos          | integer |                  false                   | *operating system supplied* | Sets the IP_TOS (Type of Service) option on the socket |
| rtcpDetectionInterval | integer |                  false                   |             10              | How much time (in seconds) should the server wait for RTCP packets before declaring the RTSP stream as a RTCP-less stream |
|   emulateUserAgent    | string  |                  false                   |     *EvoStream message*     | When specified, this value will be used as the user agent string. It is meaningful only for RTMP |
|        isAudio        | boolean |    trueif uri is RTP, otherwise false    |          1 *true*           | If **true** and if the stream is RTP, it indicates that the currently pulled stream is an audio source. Otherwise the pulled source is assumed as a video source |
|    audioCodecBytes    | string  | true if uri is RTP and isAudio is true, otherwise false |    *zero-length string*     | The audio  codec setup of this RTP stream if it is audio. Represented as hex format  without `0x` or `h`. *For example:  audioCodecBytes=1190* |
|       spsBytes        | string  | true if uri is RTP and isAudio is false, otherwise false |    *zero-length string*     | The video SPS  bytes of this RTP stream if it is video. It should be base 64 encoded. |
|       ppsBytes        | string  | true if uri is RTP and isAudio is false, otherwise false |    *zero-length string*     | The video PPS bytes of this RTP stream if it is video. It should be base 64 encoded |
|         ssmIp         | string  |                  false                   |    *zero-length string*     | The source IP from source-specific-multicast. Only usable when doing UDP based pull |
|       httpProxy       | string  |                  false                   |    *zero-length string*     | This parameter has two valid values: **IP:Port** – This value combination specifies an RTSP HTTP Proxy from which the RTSP stream should be pulled from **Self** - Specifying “self” as the value implies pulling RTSP over HTTP |
|    sendRenewStream    | boolean |                  false                   |          0 *false*          | If **true**, the server will send RenewStream via SET_PARAMETER when a new client connects. Only valid for RTSP URIs |
|       keepAlive       | boolean |                  false                   |          0 *false*          | If value is **true**, source stream will not shutdown even after all clients have hung up |



## API Call Template

``` 
generateLazyPullFile uri=<AddressOfStream> pathToFile=<filePathtoSave/fileName.vod>
```



### Sample API Call

``` 
generateLazyPullFile uri=rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 pathToFile=../media/testGenerateLazyPull.vod
```



### Success Response in JSON

``` 
{
"data":{
    "audioCodecBytes":"",
    "emulateUserAgent":"EvoStream Media Server (www.evostream.com) player",
    "forceTcp":true,
    "httpProxy":"",
    "isAudio":true,
    "keepAlive":false,
    "pageUrl":"",
    "pathToFile":"..\/media\/testGenerateLazyPull",
    "ppsBytes":"",
    "rangeEnd":-1,
    "rangeStart":-2,
    "rtcpDetectionInterval":10,
    "sendRenewStream":false,
    "spsBytes":"",
    "ssmIp":"",
    "swfUrl":"",
    "tcUrl":"",
    "tos":256,
    "ttl":256,
    "uri":{
        "document":"mp4:sintel.mp4",
        "documentPath":"\/cfx\/st\/",
        "documentWithFullParameters":"mp4:sintel.mp4",
        "fullDocumentPath":"\/cfx\/st\/mp4:sintel.mp4",
        "fullDocumentPathWithParameters":"\/cfx\/st\/mp4:sintel.mp4",
        "fullParameters":"",
        "fullUri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4",
        "fullUriWithAuth":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4",
        "host":"s2pchzxmtymn2k.cloudfront.net",
        "ip":"54.239.131.224",
        "originalUri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4",
        "parameters":{
        		},
        "password":"",
        "port":1935,
        "portSpecified":false,
        "scheme":"rtmp",
        "userName":""
        }
},
"description":"Stream parameters written to ..\/media\/testGenerateLazyPull.vod",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - audioCodecBytes - The audio codec setup of this RTP stream if it is audio. Represented as hex format without ‘0x’ or ‘h’
  - emulateUserAgent – This is the string that the EMS uses to identify itself with the other server. It can be modified so that EMS identifies itself as, say, a Flash Media Server
  - forceTcp – Whether TCP MUST be used, or if UDP can be used
  - httpProxy – May either be IP:Port combination or self
  - isAudio – Indicates that the currently pulled stream is an audio source
  - keepAlive – if true, will retain the stream in the config even if the playback stopped
  - pageUrl – A link to the page that originated the request (often unused)
  - pathToFile – The local name for the stream
  - ppsBytes – The video PPS bytes of this RTP stream if it is video
  - rangeEnd – The length in seconds for the playback
  - rangeStart – A value from which the playback should start. Applies only to RTSP and RTMP connections
  - rtcpDetectionInterval – Used for RTSP. This is the time period the EMS waits to determine if an RTCP connection is available for the RTSP/RTP stream. (RTSP is used for synchronization between audio and video)
  - sendRenewStream – Indicates if the server will send a RenewStream when a new client connects
  - spsBytes – The video SPS bytes of this RTP stream if it is video
  - ssmIp – The source IP from source-specific multicast
  - swfUrl – The location of the Flash Client that is generating the stream (if any)
  - tcUrl – An RTMP parameter that is essentially a copy of the URI
  - tos – Type of Service network flag
  - ttl – Time To Live network flag
  - uri – Contains key/value pairs describing the source stream’s URI
    - document – The document name of the source stream
    - documentPath – The document path of the source stream
    - documentWithFullParameters – The document name with parameters of the source stream
    - fullDocumentPath - The document path of the destination stream
    - fullDocumentPathWithParameters - The document path with parameters of the destination stream
    - fullParameters – The parameters for the source stream’s URI
    - fullUri – The full URI of the source stream
    - fullUriWithAuth – The full URI with authentication of the source stream
    - host – Name of the source stream’s host
    - ip – IP address of the source stream’s host
    - originalUri – The source stream’s URI where it was generated
    - parameters – Parameters for the source stream’s URI (if any)
    - password – Password for authenticating the source stream (if required)
    - port – Port used by the source stream
    - portSpecified – True if the port for the source stream is specified
    - scheme – The protocol used by the source stream
    - userName – The user name for authenticating the source stream (if required).


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

