---
layout: post
title:  "EMS API Definitions"
date:   2016-01-11 20:00:00 +0800
categories: jekyll update
---

# Table of Contents

1. Document Definitions
2. Overview
3. Run-Time API
   1. Accessing the Runtime API
      - ASCII
      - HTTP
      - PHP and JavaScript
      - JSON
   2. Configuring and Receiving Event Notifications
      - Sinks
   3. User Defined Variables
   4. Streams vs Stream Configs and API Command Return Values
      - Stream Configs
      - Streams
4. EvoStream Media Server API
   1. Streams
      - pullStream
      - pushStream
      - createHLSStream
      - createHDSStream
      - createMSSStream
      - createDASHStream
      - record
      - transcode
   2. Aliasing
      - listStreamsIds
      - getStreamInfo
      - listStreams
      - getStreamsCount
      - shutdownStream
      - listConfig
      - removeConfig
      - addStreamAlias
      - listStreamAliases
      - removeStreamAlias
      - flushStreamAliases
      - addGroupNameAlias
      - flushGroupNameAliases
      - getGroupNameByAlias
      - listGroupNameAliases
      - removeGroupNameAlias
      - listHttpStreamingSessions
      - createIngestPoint
      - removeIngestPoint
      - listIngestPoints
      - startwebrtc
      - stopwebrtc
      - addGroupNameAlias
      - flushGroupNameAliases
      - getGroupNameByAlias
      - listGroupNameAliases
      - removeGroupNameAlias
      - listHttpStreamingSessions
   3. Utility and Feature API Functions
      - launchProcess
      - setTimer
      - listTimers
      - removeTimer
      - generateLazyPullFile
      - generateServerPlaylist
      - insertPlaylistItem
      - uploadMedia
      - getMetadata
      - pushMetadata
      - shutdownMetadata
      - listStorage
      - addStorage
      - removeStorage
      - setAuthentication
      - setLogLevel
      - version
      - quit
      - help
      - shutdownServer
   4. Connections
      - listConnectionsIds
      - getConnectionInfo
      - listConnections
      - clientsConnected
      - httpClientsConnected
      - getExtendedConnectionCounters
      - resetMaxFdCounters
      - resetTotalFdCounters
      - getConnectionsCount
      - getConnectionsCountLimit
      - setConnectionsCountLimit
      - getBandwidth
      - SetBandwidthLimit
   5. Services
      - listServices
      - createService
      - enableService
      - shutdownService
5. EMS Event Notification System
   1. Stream Event Definitions
      - inStreamCreated, outStreamCreated, streamCreated
      - inStreamClosed, outStreamClosed, streamClosed
      - inStreamCodecsUpdated, outStreamCodecsUpdated, streamCodecsUpdated
      - audioFeedStopped
      - videoFeedStopped
   2. Adaptive Streaming/File-based Streaming Events
      - hlsChunkCreated, hdsChunkCreated, mssChunkCreated, dashChunkCreated
      - hlsChunkClosed, hdsChunkClosed, mssChunkClosed, dashChunkClosed
      - hlsChunkError, hdsChunkError, mssChunkError, dashChunkError
      - hlsChildPlaylistUpdated, hdsChildPlaylistUpdated
      - hlsMasterPlaylistUpdated, hdsMasterPlaylistUpdated
      - mssPlaylistUpdated, dashPlaylistUpdated
   3. Web Server Events
      - streamingSessionStarted
      - streamingSessionEnded
      - fileDownloaded
   4. API Based Events
      - cliRequest
      - cliResponse
      - processStarted, processStopped
      - timerCreated
      - timerTriggered
      - timerClosed
   5. Connection Based Events
      - protocolRegisteredToApp
      - protocolUnregisteredFromApp
      - carrierCreated
      - carrierClosed
   6. Application Based Events
      - applicationStart, applicationStop
      - serverStarted
      - serverStopped
   7. Web Server Events
      - streamingSessionStarted
      - streamingSessionEnded
      - fileDownloaded
   6. Event Table of Protocol Types

# Document Definitions

| TERM     | DEFINITION                                                                                                                                                                                                                                                                                                                                 |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **DASH** | Dynamic Adaptive Streaming over HTTP. HTTP adaptive bitrate streaming defined by ISO.                                                                                                                                                                                                                                                      |
| **EMS**  | EvoStream Media Server                                                                                                                                                                                                                                                                                                                     |
| **EWS**    | EvoStream Web Server                                                                                                                                                                                                                                                                                                                       |
| **ERS**    | EvoStream Rendezvous Server                                                                                                                                                                                                                                                                                                                |
| **HDS**    | HTTP Dynamic Streaming. HTTP adaptive bitrate streaming defined by Adobe.                                                                                                                                                                                                                                                                  |
| **HLS**    | HTTP Live Stream. HTTP adaptive bitrate streaming defined by Apple.                                                                                                                                                                                                                                                                        |
| **HTTP**   | Hyper-Text Transfer Protocol. The basic protocol used for web-page loading and web browsing. Also used for tunneling by many protocols. TCP based.                                                                                                                                                                                         |
| **IDR**    | Instantaneous Decoding Refresh – This is a specific packet in the H.264 video encoding specification. It is a full snapshot of the video at a specific instance (one full frame). Video players require an IDR frame to start playing any video. "Frames" that occur between IDR Frames are simply offsets/differences from the first IDR. |
| **JSON**   | JavaScript Object Notation                                                                                                                                                                                                                                                                                                                 |
| **Lua**    | A lightweight multi-paradigm programming language                                                                                                                                                                                                                                                                                          |
| **MSS**    | Microsoft Smooth Streaming. HTTP adaptive bitrate streaming defined by Microsoft.                                                                                                                                                                                                                                                          |
| **RTCP**   | Real Time Control Protocol – An protocol that is typically used with RTSP to synchronize two RTP streams, often audio and video streams                                                                                                                                                                                                    |
| **RTMP**   | Real Time Messaging Protocol – Used with Adobe Flash players                                                                                                                                                                                                                                                                               |
| **RTMPT**  | Real Time Messaging Protocol Tunneled – Essentially RTMP over HTTP                                                                                                                                                                                                                                                                         |
| **RTP**    | Real-time Transport Protocol – A simple protocol used to stream data, typically audio or video data.                                                                                                                                                                                                                                       |
| **RTSP**   | Real Time Streaming Protocol – Used with Android devices and live streaming clients like VLC or Quicktime. RTSP does not actually transport the audio/video data, it is simply a negotiation protocol. It is normally paired with a protocol like RTP, which will handle the actual data transport.                                        |
| **swfURL** | Used in the RTMP protocol, this field is used to designate the URL/address of the Adobe Flash Applet being used to generate the stream (if any).                                                                                                                                                                                           |
| **tcURL**  | Used in the RTMP protocol, this field is used to designate the URL/address of the originating stream server.                                                                                                                                                                                                                               |
| **TOS**    | Type of Service. This is a field in IPv4 packets used by routers to determine how traffic should be dispersed, usually for prioritizing packets.                                                                                                                                                                                           |
| **TTL**    | Time To Live. This is a field in Ipv4 packets used by routers to determine how many gateways/routers the packet should be able to pass through.                                                                                                                                                                                            |
| **URI**    | Universal Resource Identifier. The generic form of a URL. URI's are used to specify the location and type of streams.                                                                                                                                                                                                                      |
| **URL**    | Uniform Resource Locator. This is a specific form of the URI used for web browsing (http://ip/page).                                                                                                                                                                                                                                       |
| **VOD**    | Video On Demand                                                                                                                                                                                                                                                                                                                            |

# Overview

This document describes the Application Programming Interface (API) and the Event Notification System presented by the EvoStream Media Server (EMS). The API provides the ability to manipulate the server at runtime. The server can be told to retrieve or create new streams, return information on streams and connections, or even start or stop functional services. The Event Notification System provides a means for the EMS to alert users of certain events that occur within the EMS, such as a new stream is created, a stream has been dropped, server stopped, etc. The EvoStream Media Server API and Event Notification System allows users to tightly integrate with the server without having to write native plugins or modules.

# Run-Time API

While the EMS has a "great" User Interface, users typically interact with the EMS through the Run-Time API. This API, which is used by the UI, provides a whole suite of ways to interact with the EMS. It can be used to create custom User Interfaces, hook the EMS up to existing systems, integrate it with other pieces of software and much more!

## Accessing the Runtime API

### ASCII

The ASCII interface is often the first interface used by users. It can be accessed easily through the telnet application (available on all operating systems) or through common scripting languages.

To access the API via the telnet interface, a telnet application will need to be launched on the same computer that the EMS is running on. The command to open telnet from a command prompt should look something like the following:

    telnet localhost 1112

**Note:**

***Turning Telnet Feature On***

Telnet may need to be enabled using Windows® operating systems. To do this, go to the *Control Panel -> Programs -> Turn Windows Features on and off*. Turn the Telnet Client program on.

Please also note that on Windows®, the default telnet behavior will need to be changed. The local echo and new line mode should be set for proper behavior. Once telnet is launched, exit the telnet session by typing `CTRL`+`]`. Then enter the following commands:

    set localecho
    set crlf

To return to the Windows® telnet session, press `Enter` or `Return` key.

Once the telnet session is established, type out the desired commands which will be immediately executed on the server after the Enter/Return key is pressed.

An example of a command request and response from a telnet session would be the following:

**Request**  

    version

**Response**

    {"data":{"banner":"EvoStream Media Server (www.evostream.com) version 1.7.0. build 4153 with hash: c50ee04ec98886ed1f54d599355e04346bf50df0 on branch: develop - PacMan|m|-(built on 2015-11-03T01:50:37.000)","branchName":"develop","buildDate":1446515437,"buildNumber":"4153","codeName":"PacMan|m|","hash":"c50ee04ec98886ed1f54d599355e04346bf50df0","releaseNumber":"1.7.0."},"description":"Version","status":"SUCCESS"}

-	**JSON PARSER**

When using the regular ASCII interface, it may be necessary to use a JSON interpreter so that responses can be more human-readable. JSON parsers are available online.


### ASCII CLI

    telnet localhost 1222

This is the user friendly version of the ASCII telnet interface. It offers a readable response without having to parse the JSON results. To access this interface from the command prompt, execute the following:

However, since the objective of this interface is simplicity, there are some parameters that are not included on the display. Thus, for advanced usages and/or configurations, it is better to use the regular ASCII telnet interface.

An example of a command request and response from an ASCLII CLI telnet session would be the following:

**Request**  

    version

**Response**

    Command entered successfully!
    Version
      banner: EvoStream Media Server (www.evostream.com) version 1.7.0. build 4153 with hash: 4ab5d9145ae3b4b3dfeb3af5ce6890f015824974 on branch: develop - PacMan|m| - (built on 2015-11-06T08:24:32.000)
      buildDate: 2015-11-03T01:50:37.000
      buildNumber: 4153
      codeName: PacMan|m|
      releaseNumber: 1.7.0.

### HTTP

To access the API via the HTTP interface, simply make an HTTP request on the server using any browser with the command to be executed. By default, the port used for these HTTP requests is **7777**. The HTTP interface port can be changed in the main configuration file used by the EMS (config.lua).

A general http format request would be the following:

    http://[EMS IP]_[API]

An example of a command request and response from an HTTP session would be the following:

**Request**

    http://localhost:7777/version

**Response**


    {"data":{"banner":"EvoStream Media Server (www.evostream.com) version 1.7.0. build 4153 with hash: c50ee04ec98886ed1f54d599355e04346bf50df0 on branch: develop - PacMan|m|-(built on 2015-11-03T01:50:37.000)","branchName":"develop","buildDate":1446515437,"buildNumber":"4153","codeName":"PacMan|m|","hash":"c50ee04ec98886ed1f54d599355e04346bf50df0","releaseNumber":"1.7.0."},"description":"Version","status":"SUCCESS"}

All of the API functions are available via HTTP, but the request must be formatted slightly different if parameters are included. To make an API call over HTTP, the parameters to be used should be in base64 format.

    http://IP/[API]?params=([base64 encoded parameters])

Sampling a **pullstream** command:

- Type in the parameters first:

        (firstParam=XXX secondParam=YYY…)
        (uri=rtsp://localhost:5544/vod/mp4.bunny.mp4 localStreamName=bunny)

- Convert the parameters using a base64 encoder:

  **Converted parameter:**

        dXJpPXJ0c3A6Ly9sb2NhbGhvc3Q6NTU0NC92b2QvbXA0LmJ1bm55Lm1wNCBsb2NhbHN0cmVhbW5hbWU9YnVubnkp

- The corresponding request in HTTP format would be:

      http://localhost:7777/pullstream?params= dXJpPXJ0c3A6Ly9sb2NhbGhvc3Q6NTU0NC92b2QvbXA0LmJ1bm55Lm1wNCBsb2NhbHN0cmVhbW5hbWU9YnVubnkp

-	**Base64**

  A group of similar binary-to-text encoding schemes that represent binary data in an [ASCII](https://en.wikipedia.org/wiki/ASCII) string format by translating it into a [radix](https://en.wikipedia.org/wiki/Radix)-64 representation. There are available base64 encoders online to get the encoded result.

-	**PHP and JavaScript**

  PHP and JavaScript functions are also provided. These functions simply wrap the HTTP interface calls and can be found in the EMS Web UI directory.

-	**Securing the API**

  By default, the ASCII API is protected and access from any outside computer is prohibited. This can of course be modified within the config.lua file, but keeping this restriction is recommended for maintaining server security.

The HTTP based API is also restricted by default to only local access. However, unlike the ASCII API interface, there are often good reasons to expose the HTTP API. To secure the HTTP based API in this case, you will enable Proxy Authentication on the EWS (details found in the EWS section of this doc). This will enforce that a valid username and password be provided for each and every API call made, ensuring on authorized access to the EMS API.

## Configuring and Receiving Event Notifications

The EvoStream Media Server (EMS) generates notifications based upon events that occur at runtime. These events are formatted as HTTP calls and can be delivered to any address and port desired.

Event Notifications are **disabled** by default and must be enabled by modifying the EMS config file: config.lua.

To enable Event Notifications you will need to Enable/Uncomment the *eventLogger* section of the config.lua file. *Comments in LUA are specified by either a `--` for a single line, or denoted by a `--[[` to start a comment block and a `]]--` to end a comment block. By default the eventLogger section is commented out using block style comments, so you will need to remove both the* `--[[` *and* `]]--` *strings.* See the Configuration Files section for more information.

### Sinks

Sinks are defined as "a specific destination for events" and can be of two types: "file" and "RPC". File sinks simply write events to a file, as defined by the "filename" parameter. This works much like a system logger. Users can choose the format of the output between JSON, XML, W3C and text. JSON and XML will be formatted as JSON and XML respectively and each event will be written to a single line. This is done for ease of parsing. The W3C formatted file is compliant with the requirement of having space or tab-delimited columns. In addition, it has a header line that is commented out (#) that indicates the names of the columns. As with JSON and XML, each event is also written to a single line. The Text format writes to the event file in a way that is easy to read, where events are on multiple lines. *The file sink is* _ **off** _ *by default,* but can be turned on by creating the sink in the config.lua file.

To receive HTTP based Event Notifications, an RPC type sink must be defined (and is by default). The URL parameter defines the location that will be called with each event. The URL can be a specific web service script or just an IP and port on which you are listening. RPC sinks have the option of one of three serializer types, or in other words, the way the data will be formatted within the HTTP post: JSON, XML, XMLRPC. XMLRPC events will be formatted as XML using a traditional XML-RPC schema. The XML serializer type will use an XML schema that is more condensed and specific to the EMS Event Notification System. The JSON serializer type will have the same schema as XML, but will be formatted as JSON.

For any Sink, users can define an array of *enabledEvents*. When this array is present, ONLY the events listed will be sent to that sink. If this array is not present, ALL events will be sent to the sink. The full list of events can be found later in this document.

## User Defined Variables

While the EMS provides an extensive set of API functions, there may be times where the variables provided are not sufficient, or where you may need extra information to be associated with individual streams. To support these needs, the EMS API implements User Defined Variables. User Defined Variables can be used with any API function where information is maintained by the EMS (i.e. pulling a stream, creating a timer, starting a transcode job, etc.).

To specify a User Defined Variable, you simply need to append a '_' to the beginning of your variable name. The User Defined variables are reported back whenever you get information about the command: listStreams, listConfig, Event Notifications, etc.

Some common use cases for User Defined Variables are as follows:

- Setting a timer to stop a stream after a set period of time

        setTimer value=120 _streamName=MyStreamsetTimer value=120 _streamID=5

        pullstream uri=rtmp://192.168.1.5/live/myStream localstreamname=test1 _myID=5 _myName=secretSquirrel

These commands will fire a timer event after 120 seconds with the set stream name or stream id respectively.

- Attach a custom identifier to a local stream
- Set a custom value on a pushed stream

        pushstream uri=rtmp://192.168.1.5/live/myStream localstreamname=test1 _myID=5 _myName=secretSquirrel

## Streams vs Stream Configs and API Command Return Values

Issuing commands to the EvoStream Media Server is an Asynchronous event. This means that a successfully issued command will not actually be executed immediately. It will instead be Queued for execution. While this generally transparent for the user, there is an important ramification of this reality:

**When the EMS returns SUCCESS for an issued API command, this only means that the command was successfully QUEUED. IT DOES NOT MEAN THAT THE COMMAND WAS SUCCESSFULLY EXECUTED!**

For example, a pullStream command may return SUCCESS, but the stream may not have actually been pulled!

More details on why this occurs follows.

### Stream Configs

When an API command is issued, it creates a Stream Config entry. Each Stream Config is a list of parameters which instructs EMS to take an action. As a result of that action, a stream may be born. At the time at which the command is executed (stream config is created), there is absolutely no guarantee that the action will indeed spawn a stream. There is a very good reason for this behavior. The action itself doesn't solely depend on EMS. In the case of **pullStream,** the success of the command greatly depends on the distant party being invoked to send the stream in question. If that distant party doesn't do that, then the stream can't be created. To summarize, stream config is only the blueprint of the future stream, nothing less, and nothing more.

Stream Configs also have a unique, monotonically increasing ID. This is completely different from the "stream id". When listConfig is used, it will output the format described in the "API Definiion.pdf". Notice the configId value for each node. The listing of the configurations also contains the current status of the stream and the previous status. Finally, removeConfig can be used to terminate a configuration and the corresponding stream (if ever spawned)

### Streams

Streams are the active streams currently managed by EMS. They may or may not have an associated config. That is because the stream could be pushed/pulled into/from EMS by a distant party, without any execution of a pushStream/pullStream command. For example, an Adobe flash application does a "publish" or a "play". However, when a stream is born due to a pullStream/pushStream/etc API command, that stream Will have an associated config. listStreams will list all streams regardless of their nature: pulled/pushed by EMS or from 3rd party apps like explained in the Adobe example above. When a stream is actively pushed/pulled by EMS, the node describing that stream will also contain a sub node with the configuration (the stream config explained above). shutdownStream, as the name implies, acts on a stream, not on a stream config. That is why you can't do a shutdownStream on a stream name which is not present BUT was configured. The permanently=1 parameter is provided to save an extra call to removeConfig call, but, again, that is only making sense when the stream is active. The streams information returned by listStreams contains a unique id for each and every stream node. That is what we refer to as "stream id".

**To summarize the above:** _ **streamID** _ **is different from** _ **configID** _ **because they signify two different kinds of entities.**

# EvoStream Media Server API

The EMS API can be broken down into a few groups of functionality. The first group, and the one most often used, is Stream Manipulation. The other groups are Connection Details and Services which are discussed later in the document.

Each API function is listed along with its mandatory and optional parameters. Examples of each interface can be found after the description of function parameters.

**PLEASE NOTE:**

**All Boolean parameters are set using 1 for true and 0 for false!**

**Default values of parameters shown in parentheses or italicized are just remarks.**

**Special Parameter:**

There is a special parameter that can be used in all API commands:

commandID - If set to any value, the corresponding message will have a parameter responseId set to the same value. This is used to match the responses to the corresponding commands.

To use, simply add commandID=<value> as an additional parameter

| API                                     | APIcommand [someParameters] commandID=0101   |
|-----------------------------------------|----------------------------------------------|
| JSON Response                           | {"data":{…"description":"*API description*", |
| "responseId" :"0101","status":"SUCCESS" |                                              |


## Streams

Streams are considered to be the actual video and/or audio feeds that are coming from, or going to, the EMS. Streams can be sent over a wide variety of protocols. The following functions are provided to manipulate and query Streams:

**IMPORTANT:** All Stream Names are **case sensitive** for all API functions!

### pullStream

This will try to pull in a stream from an external source. Once a stream has been successfully pulled it is assigned a "local stream name" which can be used to access the stream from the EMS.

This function has the following parameters:

| **Parameter Name**    | **Mandatory**                                            | **Default Value**         | **Description**                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------|----------------------------------------------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| uri                   | true                                                     | *(null)*                  | The URI of the external stream. Can be RTMP, RTSP or unicast/multicast (d) mpegts.                                                                                                                                                                                                                                                                                                         |
| keepAlive             | false                                                    | 1 *(true)*                | If keepAlive is set to 1, the server will attempt to reestablish connection with a stream source after a connection has been lost. The reconnect will be attempted once every second.                                                                                                                                                                                                      |
| localStreamName       | false                                                    | *(computed)*              | If provided, the stream will be given this name. Otherwise, a fallback technique is used to determine the stream name (based on the URI)                                                                                                                                                                                                                                                   |
| forceTcp              | false                                                    | 1 *(true)*                | If 1 and if the stream is RTSP, a TCP connection will be forced. Otherwise the transport mechanism will be negotiated (UDP or TCP).                                                                                                                                                                                                                                                        |
| tcUrl                 | false                                                    | *(zero-length string)*    | When specified, this value will be used to set the TC URL in the initial RTMP connect invoke                                                                                                                                                                                                                                                                                               |
| pageUrl               | false                                                    | *(zero-length string)*    | When specified, this value will be used to set the originating web page address in the initial RTMP connect invoke.                                                                                                                                                                                                                                                                        |
| swfUrl                | false                                                    | *(zero-length string)*    | When specified, this value will be used to set the originating swf URL in the initial RTMP connect invoke                                                                                                                                                                                                                                                                                  |
| rangeStart            | false                                                    | *-2*                      | For RTSP and RTMP connections. A value from which the playback should start expressed in seconds. There are 2 special values: -2 and -1. For more information, please read about start/len parameters here: [http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.html](http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.html) |
| rangeEnd              | false                                                    | *-1*                      | The length in seconds for the playback. -1 is a special value. For more information, please read about start/len parameters here: [http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.html](http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.html)                                                                           |
| ttl                   | false                                                    | operating system supplied | Sets the IP_TTL (time to live) option on the socket                                                                                                                                                                                                                                                                                                                                       |
| tos                   | false                                                    | operating system supplied | Sets the IP_TOS (Type of Service) option on the socket                                                                                                                                                                                                                                                                                                                                    |
| rtcpDetectionInterval | false                                                    | 10                        | How much time (in seconds) should the server wait for RTCP packets before declaring the RTSP stream as a RTCP-less stream                                                                                                                                                                                                                                                                  |
| emulateUserAgent      | false                                                    | *(EvoStream message)*     | When specified, this value will be used as the user agent string. It is meaningful only for RTMP.                                                                                                                                                                                                                                                                                          |
| isAudio               | true if uri is RTP, otherwise false                      | *1 (true)*                | If 1 and if the stream is RTP, it indicates that the currently pulled stream is an audio source. Otherwise the pulled source is assumed as a video source.                                                                                                                                                                                                                                 |
| audioCodecBytes       | true if uri is RTP and isAudio is true, otherwise false  | *(zero-length string)*    | The audio codec setup of this RTP stream if it is audio. Represented as hex format without '0x' or 'h'. (For example: audioCodecBytes=1190)                                                                                                                                                                                                                                                |
| spsBytes              | true if uri is RTP and isAudio is false, otherwise false | *(zero-length string)*    | The video SPS bytes of this RTP stream if it is video. It should be base 64 encoded.                                                                                                                                                                                                                                                                                                       |
| ppsBytes              | true if uri is RTP and isAudio is false, otherwise false | *(zero-length string)*    | The video PPS bytes of this RTP stream if it is video. It should be base 64 encoded.                                                                                                                                                                                                                                                                                                       |
| ssmIp                 | false                                                    | *(zero-length string)*    | The source IP from source-specific-multicast. Only usable when doing UDP based pull                                                                                                                                                                                                                                                                                                        |
| httpProxy             | False                                                    | *(zero-length string)*    | This parameter has two valid values:                                                                                                                                                                                                                                                                                                                                                       |

1.	IP:Port – This value combination specifies an RTSP HTTP Proxy from which the RTSP stream should be pulled from
2.	self – Specifying "self" as the value implies pulling **RTSP over HTTP**. | | sendRenewStream | | | |

The EMS provides several shorthand User Agent strings (not case-sensitive) for convenience:

| **emulateUserAgent**      | **Resolves as..**                                                         |
|---------------------------|---------------------------------------------------------------------------|
| emulateUserAgent=evo      | EvoStream Media Server ( [www.evostream.com](http://www.evostream.com/)\) |
| emulateUserAgent=FMLE     | FMLE/3.0 (compatible; FMSc/1.0)"                                          |
| emulateUserAgent=wirecast | Wirecast/FM 1.0 (compatible; FMSc/1.0)"                                   |
| emulateUserAgent=flash    | MAC 11,3,300,265                                                          |

An example of the pullStream interface is:

    pullStream uri=rtsp://AddressOfStream keepAlive=1 localStreamname=RTSPtest

    rtsp://AddressOfEMS:5544/RTSPtest

    pullStream uri=rtmp://AddressOfStream keepAlive=1 localStreamname=RTMPtest

Then, to access that stream via a flash player, the following URI can be used:

    rtmp://AddressOfEMS/live/RTMPtest

| API           | pullstream uri=rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 localStreamname=testpullstream                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"audioCodecBytes":"","configId":1,"emulateUserAgent":"EvoStream Media Server (www.evostream.com) player","forceTcp":false,"httpProxy":"","isAudio":true,"keepAlive":true,"localStreamName":"testpullstream","operationType":1,"pageUrl":"","ppsBytes":"","rangeEnd":-1,"rangeStart":-2,"rtcpDetectionInterval":10,"sendRenewStream":false,"spsBytes ":"","ssmIp":"","swfUrl":"","tcUrl":"","tos":256,"ttl":256,"uri":{"document":"mp4:sintel.mp4","documentPath":"\/cfx\/st\/","documentWithFullParameters":"mp4:sintel.mp4","fullD ocumentPath":"\/cfx\/st\/mp4:sintel.mp4","fullDocumentPathWithParameters":"\/cfx\/st\/mp4:sintel.mp4","fullParameters":"","fullUri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cf x\/st\/mp4:sintel.mp4","fullUriWithAuth":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","host":"s2pchzxmtymn2k.cloudfront.net","ip":"54.239.131.57","original Uri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","parameters":{},"password":"","port":1935,"portSpecified":false,"scheme":"rtmp","userName":""}},"description":"Stream rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4 enqueued for pulling","status":"SUCCESS"} |

The JSON response for pullStream contains the following details:

-	data – The data to parse.
	-	audioCodecBytes - The audio codec setup of this RTP stream if it is audio
	-	configID – The configuration ID for this command
	-	emulateUserAgent – This is the string that the EMS uses to identify itself with the other server. It can be modified so that EMS identifies itself as, say, a Flash Media Server
	-	forceTcp – Whether TCP MUST be used, or if UDP can be used
	-	httpProxy - May either be IP:Port combination or self
	-	isAudio - Indicates if the currently pulled stream is an audio source
	-	keepAlive – If true, the stream will attempt to reconnect if the connection is severed
	-	localStreamName – The local name for the stream
	-	operationType – The type of operation
	-	pageUrl – A link to the page that originated the request (often unused)
	-	ppsBytes - The video PPS bytes of this RTP stream if it is video
	-	rangeEnd - The length in seconds for the playback
	-	rangeStart - A value from which the playback should start expressed in seconds
	-	rtcpDetectionInterval – Used for RTSP. This is the time period the EMS waits to determine if an RTCP connection is available for the RTSP/RTP stream. (RTSP is used for synchronization between audio and video).
	-	sendRenewStream – If 1, the server will send RenewStream via SET_PARAMETER when a new client connects
	-	spsBytes - The video SPS bytes of this RTP stream if it is video
	-	ssmIp - The source IP from source-specific-multicast
	-	swfUrl – The location of the Flash Client that is generating the stream (if any)
	-	tcUrl – An RTMP parameter that is essentially a copy of the URI
	-	tos – Type of Service network flag
	-	ttl – Time To Live network flag
	-	uri – Contains key/value pairs describing the source stream's URI
	-	document – The document name of the source stream
	-	documentPath – The document path of the source stream
	-	documentWithFullParameters – The document name with parameters of the source stream
	-	fullDocumentPath - The document path of the destination stream
	-	fullDocumentPathWithParameters - The document path with parameters of the destination stream
	-	fullParameters – The parameters for the source stream's URI
	-	fullUri – The full URI of the source stream
	-	fullUriWithAuth – The full URI with authentication of the source stream
	-	host – Name of the source stream's host
	-	ip – IP address of the source stream's host
	-	originalUri – The source stream's URI where it was generated
	-	parameters – Parameters for the source stream's URI (if any)
	-	password – Password for authenticating the source stream (if required).
	-	port – Port used by the source stream.
	-	portSpecified – True if the port for the source stream is specified.
	-	scheme – The protocol used by the source stream.
	-	userName – The user name for authenticating the source stream (if required).
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### pushStream

This will try to push a local stream to an external destination. The pushed stream can only use the RTMP, RTSP or MPEG-TS unicast/multicast protocol. This function has the following parameters:

| **Parameter Name**     | **Mandatory** | **Default Value**         | **Description**                                                                                                                                                                                                                                                            |
|------------------------|---------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| uri                    | true          | *(null)*                  | The URI of the destination point (without stream name).                                                                                                                                                                                                                    |
| localStreamName        | true          | *(computed)*              | If provided, the stream will be given this name. Otherwise, a fallback technique is used to determine the stream name (based on the URI).                                                                                                                                  |
| tos                    | false         | operating system supplied | Sets the IP_TOS (Type of Service) option on the socket.                                                                                                                                                                                                                   |
| keepAlive              | false         | 1 *(true)*                | If keepAlive is set to 1, the server will attempt to reestablish connection with a stream source after a connection has been lost. The reconnect will be attempted once every second.                                                                                      |
| targetStreamName       | false         | *(null)*                  | The name of the stream at destination. If not provided, the target stream name will be the same as the local stream name.                                                                                                                                                  |
| targetStreamType       | false         | Live                      | It can be one of following: live, record, append. It is meaningful only for RTMP.                                                                                                                                                                                          |
| emulateUserAgent       | false         | *(EvoStream message)*     | When specified, this value will be used as the user agent string. It is meaningful only for RTMP.                                                                                                                                                                          |
| rtmpAbsoluteTimestamps | false         | *0 (false)*               | Forces the timestamps to be absolute when using RTMP                                                                                                                                                                                                                       |
| swfUrl                 | false         | *(zero-length string)*    | When specified, this value will be used to set the originating swf URL in the initial RTMP connect invoke                                                                                                                                                                  |
| pageUrl                | false         | *(zero-length string)*    | When specified, this value will be used to set the originating web page address in the initial RTMP connect invoke.                                                                                                                                                        |
| tcUrl                  | false         | *(zero-length string)*    | When specified, this value will be used to set the TC URL in the initial RTMP connect invoke                                                                                                                                                                               |
| ttl                    | false         | operating system supplied | Sets the IP_TTL (Time To Live) option on the socket.                                                                                                                                                                                                                      |
| sendChunkSizeRequest   | false         | *1 (true)*                | Sets whether the RTMP stream will or will not send a "Set Chunk Length" message. This is significant when pushing to Akamai's new RTMP HD ingest point where this parameter should be set to 0 so that Akamai will not drop the connection.                                |
| useSourcePts           | false         | *0 (false)*               | When value is 1 (true), timestamps on source inbound RTMP stream are passed directly to the outbound (pushed) RTMP streams. This affects only pushed Outbound Net RTMP with net RTMP source. This parameter overrides the value of the config.lua option of the same name. |

An example of the pullStream interface is:

    pushStream uri=rtmp://DestinationAddress keepAlive=1 localStreamname=pushtest

| API           | pushStream uri=rtmp://127.0.0.1 localStreamName=testpullStream targetStreamName=testpushStream                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"configId":6,"emulateUserAgent":"EvoStream Media Server (www.evostream.com)","forceTcp":false,"httpProxy":"","keepAlive":true,"localStreamName":"testpullStream","operationType":2,"pageUrl":"","rtmpAbsoluteTimestamps":false,"sendChunkSizeRequest":true,"swfUrl":"","targetStreamName":"testpushStream","targetStreamType":"live","targetUri":{"document":"","documentPath":"\/","documentWithFullParameters":"","fullDocumentPath":"\/","fullDocumentPathWithParameters":"\/","fullParameters":"","fullUri":"rtmp:\/\/127.0.0.1","fullUriWithAuth":"rtmp:\/\/127.0.0.1","host":"localhost","ip":"127.0.0.1","originalUri":"rtmp:\/\/localhost","parameters":{},"password":"","port":1935,"portSpecified": false,"scheme":"rtmp","userName":""},"tcUrl":"","tos":256,"ttl":256,"useSourcePts":false},"description":"Local stream testpullStream enqueued for pushing to rtmp:\/\/localhost as testpushStream","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	configID – The configuration ID for this command
	-	emulateUserAgent – This is the string that the EMS uses to identify itself with the other server. It can be modified so that EMS identifies itself as, say, a Flash Media Server.
	-	forceTcp – Whether TCP MUST be used, or if UDP can be used.
	-	httpProxy - May either be IP:Port combination or self
	-	keepAlive – If true, the stream will attempt to reconnect if the connection is severed.
	-	localStreamName – The local name for the stream.
	-	operationType – The type of operation
	-	pageUrl – A link to the page that originated the request (often unused).
	-	rtmpAbsoluteTimeStamps – If true, forces the timestamps to be absolute when using RTMP
	-	sendChunkSizeRequest – Indicates whether the RTMP stream will or will not send a "Set Chunk Length" message
	-	swfUrl – The location of the Flash Client that is generating the stream (if any).
	-	targetStreamName – The name of the stream at destination.
	-	targetStreamType – One of following: `live`, `record`, `append`. Useful only for RTMP.
	-	targetUri – Contains key/value pairs describing the destination stream's URI
	-	document – The document name of the destination stream
	-	documentPath – The document path of the destination stream
	-	documentWithFullParameters – The document name with parameters of the destination stream
	-	fullDocumentPath – The document path of the destination stream
	-	fullDocumentPathWithParameters – The document path with parameters of the destination stream
	-	fullParameters – The parameters for the destination stream's URI.
	-	fullUri – The full URI of the destination stream.
	-	fullUriWithAuth – The full URI with authentication of the destination stream.
	-	host – The name of the destination stream's host.
	-	ip – The IP address of the destination stream's host.
	-	originalUri – The destination stream's URI where it was generated.
	-	parameters – Parameters for the destination stream's URI.
	-	password – Password for authenticating the destination stream (if required).
	-	port – Port used by the destination stream.
	-	portSpecified – True if the port for the destination stream is specified.
	-	scheme – The protocol used by the destination stream.
	-	userName – The user name for authenticating the destination stream (if required).
	-	tcUrl – An RTMP parameter that is essentially a copy of the URI.
	-	tos – Type of Service network flag.
	-	ttl – Time To Live network flag.
-	description – Describes the result of parsing/executing the command.
	-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### createHLSStream

Create an HTTP Live Stream (HLS) out of an existing H.264/AAC stream. HLS is used to stream live feeds to iOS devices such as iPhones and iPads.

This function has the following parameters:

| **Parameter Name**   | **Mandatory** | **Default Value**                                              | **Description**                                                                                                                                                                                                                                                                     |
|----------------------|---------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| localStreamNames     | true          | *(null)*  | The stream(s) that will be used as the input. This is a comma-delimited list of active stream names (local stream names). |
| targetFolder         | true          | *(null)*  | The folder where all the \*.ts/\*.m3u8 files will be stored. This folder must be accessible by the HLS clients. It is usually in the web-root of the server.  |
| keepAlive            | false         | 1 *(true)* | If true, the EMS will attempt to reconnect to the stream source if the connection is severed.  |
| overwriteDestination | false         | 1 *(true)*  | If true, it will force overwrite of destination files.  |
| staleRetentionCount  | false         | *(if not specified, it will have the value of playlistLength)* | The number of old files kept besides the ones listed in the current version of the playlist. Only applicable for rolling playlists.  |
| createMasterPlaylist | false         | 1 *(true)*  | If true, a master playlist will be created.  |
| cleanupDestination   | false         | 0 *(false)*  | If 1 (true), all \*.ts and \*.m3u8 files in the target folder will be removed before HLS creation is started. |
| bandwidths           | false         | 0  | The corresponding bandwidths for each stream listed in localStreamNames. Again, this can be a comma-delimited list. |
| groupName            | false         | *(it will be a random name in the form of hls_group_xxxx)*   | The name assigned to the HLS stream or group. If the localStreamNames parameter contains only one entry and groupName is not specified, groupName will have the value of the input stream name. |
| playlistType         | false         | appending  | Either `appending` or `rolling`. |
| playlistLength       | false         | 10  | The length (number of elements) of the playlist. Used only when playlistType is `rolling`. Ignored otherwise. |
| playlistName         | false         | playlist.m3u8  | The file name of the playlist (\*.m3u8). |
| chunkLength          | false         | 10                                                             | The length (in seconds) of each playlist element (\*.ts file). Minimum value is 1 (second).                                                                                                                                                                                         |
| maxChunkLength       | false         | 0                                                              | This parameter represents the maximum length, in seconds, the EMS will allow any single chunk to be. This is primarily in the case of chunkOnIDR=true where the EMS will wait for the next key-frame.If the maxChunkLength is less than chunkLength, the parameter shall be ignored |
| chunkBaseName        | false         | segment | The base name used to generate the \*.ts chunks. |
| chunkOnIDR           | false         | 1 *(true)* | If true, chunking is performed ONLY on IDR. Otherwise, chunking is performed whenever chunk length is achieved. |
| drmType              | false         | None | Sets the type of DRM encryption to use. Options are: none (no encryption), evo (AES Encryption), verimatrix (Verimatrix DRM).For Verimatrix DRM, the "drm" section of the config.lua file must be active and properly configured. |
| AESKeyCount          | false         | 5 | Specifies the number of keys that will be automatically generated and rotated over while encrypting this HLS stream. |
| audioOnly            | false         | 0 *(false)* | Specifies if the resulting stream will be audio only. A value of 1(true) will result in a stream without video.  |
| hlsResume            | false         | 0 *(false)* | If 1 (true), HLS will resume in appending segments to previously created child playlist even in cases of EMS shutdown or cut off stream source.  |
| useByteRange         | .             | .          | .          |
| fileLength           | .             | .          | .          |

An example of the createHLSStream interface is:

The corresponding link to use on an iOS device to pull this stream would then be:

    createHLSStream localstreamnames=hlstest bandwidths=128 targetfolder=/MyWebRoot/ groupname=hls playlisttype=rolling playlistLength=10 chunkLength=5

    http://My_IP_or_Domain/hls/playlist.m3u8

In other words: `http://<my_web_server>/<HLS_group_name>/<playlist_file_name>`

| API           | createHLSStream localstreamnames=testpullStream bandwidths=128 targetfolder=../evo-webroot groupname=hls playlisttype=rolling                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"AESKeyCount":5,"audioOnly":false,"bandwidths":[128],"chunkBaseName":"segment","chunkLength":10,"chunkOnIDR":true,"cleanupDestination":false,"cleanupOnClose":false,"configIds":[7],"createMasterPlaylist":true,"drmType":"none","fileLength":0,"groupName":"hls","hlsResume":false,"hlsVersion":3,"keepAlive":true,"localStreamNames":["testpullStream"],"maxChunkLength":0,"offsetTime":0,"overwriteDestination":true,"playlistLength":10,"playlistName":"playlist.m3u8","playlistType":"rolling","staleRetentionCount":10,"startOffset":0,"targetFolder":"..\/evo-webroot","useByteRange":false,"useSystemTime":false},"description":"HLS stream created","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	AESKeyCount - the number of keys that will be automatically generated and rotated over while encrypting this HLS stream
	-	audioOnly - If true, the EMS will only stream audio
	-	bandwidths – An array of integers specifying the bandwidths used for streaming.
	-	chunkBaseName – The base name or prefix used for naming the output HLS chunks.
	-	chunkLength – The length (in seconds) of each playlist element (.ts files)
	-	chunkOnIdr – If true, chunking was made on IDR boundary.
	-	cleanupDestination – If true, HLS files at the target folder were deleted before HLS creation began.
	-	cleanupOnClose - If true, corresponding hls files to a stream will be deleted if the stream is disconnected
	-	configIDs – The configuration IDs for this command
	-	createMasterPlaylist – If true, a master playlist is created.
	-	drmType - The type of DRM encryption used
	-	fileLength - ??
	-	groupName – The name of the target folder where HLS files will be created.
	-	hlsResume – If true,will resume in appending segments to previously created child playlist even in cases of EMS shutdown or cut off stream source
	-	hlsVersion – The configured HLS version
	-	keepAlive – If true, the stream will attempt to reconnect if the connection is severed.
	-	localStreamNames – An array of local names for the streams.
	-	maxChunkLength - The maximum length the EMS will allow any single chunk to be
	-	offsetTime - ??
	-	overwriteDestination – If true, forced overwrite was enabled during HLS creation.
	-	playlistLength – The number of elements in the playlist. Useful only for `rolling` playlistType.
	-	playlistName – The file name of the playlist (\*.m3u8).
	-	playlistType – Either `appending` or `rolling`.
	-	staleRetentionCount – The number of old files kept besides the ones listed in the current version of the playlist. Only applicable for rolling playlists.
	-	startoffset - ??
	-	targetFolder – The folder where all the \*.ts/\*.m3u8 files are stored.
	-	useByteRange - ??
	-	useSystemTime- ??
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### createHDSStream

Create an HDS (HTTP Dynamic Streaming) stream out of an existing H.264/AAC stream. HDS is used to stream standard MP4 media over regular HTTP connections. HDS is a new technology developed by Adobe in response to HLS from Apple.

This function has the following parameters:

| **Parameter Name**   | **Mandatory** | **Default Value**                                            | **Description**                                                                                                                                                                                 |
|----------------------|---------------|--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| localStreamNames     | true          | *(null)*                                                     | The stream(s) that will be used as the input. This is a comma-delimited list of active stream names (local stream names).                                                                       |
| targetFolder         | true          | *(null)*                                                     | The folder where all the manifest (\*.f4m) and fragment (f4v\*) files will be stored. This folder must be accessible by the HDS clients. It is usually in the web-root of the server.           |
| bandwidths           | false         | 0                                                            | The corresponding bandwidths for each stream listed in localStreamNames. Again, this can be a comma-delimited list.                                                                             |
| chunkBaseName        | false         | f4v                                                          | The base name used to generate the fragments. The default value follows this format: f4vSeg1-FragXXX.                                                                                           |
| chunkLength          | false         | 10                                                           | The length (in seconds) of fragments to be made. Minimum value is 1 (second).                                                                                                                   |
| chunkOnIDR           | false         | 1 *(true)*                                                   | If true, chunking is performed ONLY on IDR. Otherwise, chunking is performed whenever chunk length is achieved.                                                                                 |
| groupName            | false         | *(it will be a random name in the form of hds_group_xxxx)* | The name assigned to the HDS stream or group. If the localStreamNames parameter contains only one entry and groupName is not specified, groupName will have the value of the input stream name. |
| keepAlive            | false         | 1 *(true)*                                                   | If true, the EMS will attempt to reconnect to the stream source if the connection is severed.                                                                                                   |
| manifestName         | false         | defaults to stream name                                      | The manifest file name.                                                                                                                                                                         |
| overwriteDestination | false         | 1 *(true)*                                                   | If true, it will allow overwrite of destination files.                                                                                                                                          |
| playlistType         | false         | appending                                                    | Either `appending` or `rolling`.                                                                                                                                                                |
| playlistLength       | false         | 10                                                           | The number of fragments before the server starts to overwrite the older fragments. Used only when playlistType is `rolling`. Ignored otherwise.                                                 |
| staleRetentionCount  | false         | If not specified, it will have the value of playlistLength   | How many old files are kept besides the ones present in the current version of the playlist. Only applicable for rolling playlists.                                                             |
| createMasterPlaylist | false         | 1 *(true)*                                                   | If true, a master playlist will be created.                                                                                                                                                     |
| cleanupDestination   | false         | 0 *(false)*                                                  | If 1 (true), all manifest and fragment files in the target folder will be removed before HDS creation is started.                                                                               |

An example of the createHDSStream interface is:

    createHDSStream localstreamnames=hdstest bandwidths=128 targetfolder=/MyWebRoot/ groupname=hds rolling=true rollingLimit=10 chunkLength=5

    http://My_IP_or_Domain/hds/manifest.f4m

The corresponding link to use on an HDS player (e.g. OSMF) to pull this stream would then be:

In other words: `http://<my_web_server>/<HDS_group_name>/<manifest_file_name>`

| API           | createHDSStream localstreamnames=testpullStream targetfolder=../evo-webroot groupname=hds playlisttype=rolling                                                                                                                                                                                                                                                                                                                                  |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"bandwidths":[0],"chunkBaseName":"f4v","chunkLength":10,"chunkOnIDR":true,"cleanupDestination":false,"configIds":[9],"createMasterPlaylist":true,"groupName":"hds","keepAlive":true,"localStreamNames":["testpullStream"],"manifestName":"","overwriteDestination":true,"playlistLength":10,"playlistType":"rolling","staleRetentionCount":10,"targetFolder":"..\/evo-webroot"},"description":"HDS stream created","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	bandwidths – An array of integers specifying the bandwidths used for streaming.
	-	chunkBaseName – The base name or prefix used for naming the output HDS chunks.
	-	chunkLength – The length (in seconds) of each playlist element (.f4m files).
	-	chunkOnIdr – If true, chunking was made on IDR boundary.
	-	cleanupDestination – If true, HDS files at the target folder were deleted before HDS creation began.
	-	configIds - The configuration IDs for this command
	-	createMasterPlaylist – If true, a master playlist is created.
	-	groupName – The name of the target folder where HDS files will be created.
	-	keepAlive – If true, the stream will attempt to reconnect if the connection is severed.
	-	localStreamNames – An array of local names for the streams.
	-	manifestName – The file name of the manifest file (\*.f4m). If blank, defaults to stream name.
	-	overwriteDestination – If true, overwriting of destination files during HDS creation is allowed.
	-	playlistLength – The number of fragments before the server starts to overwrite the older fragments. Useful only for `rolling` playlistType.
	-	playlistType – Either `appending` or `rolling`.
	-	staleRetentionCount – The number of old files kept besides the ones listed in the current version of the playlist. Only applicable for rolling playlists.
	-	targetFolder – The folder where all the manifest (\*.f4m) and fragment (f4v\*) files are stored.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### createMSSStream

Create a Microsoft Smooth Stream (MSS) out of an existing H.264/AAC stream. Smooth Streaming was developed by Microsoft to compete with other adaptive streaming technologies.

This function has the following parameters:

| **Parameter Name**   | **Mandatory** | **Default Value**                                            | **Description**                                                                                                                                                                                 |
|----------------------|---------------|--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| localStreamNames     | true          | *(null)*                                                     | The stream(s) that will be used as the input. This is a comma-delimited list of active stream names (local stream names).                                                                       |
| targetFolder         | true          | *(null)*                                                     | The folder where all the manifest and fragment files will be stored. This folder must be accessible by the MSS clients. It is usually in the web-root of the server.                            |
| bandwidths           | false         | 0                                                            | The corresponding bandwidths for each stream listed in localStreamNames. Again, this can be a comma-delimited list.                                                                             |
| groupName            | false         | *mss_group_xxxx (random)*                                  | The name assigned to the MSS stream or group. If the localStreamNames parameter contains only one entry and groupName is not specified, groupName will have the value of the input stream name. |
| playlistType         | false         | Appending                                                    | Either `appending` or `rolling`                                                                                                                                                                 |
| playlistLength       | false         | 10                                                           | The number of fragments before the server starts to overwrite the older fragments. Used only when playlistType is 'rolling'. Ignored otherwise.                                                 |
| manifestName         | false         | 'manifest.ismc'                                              | The manifest file name                                                                                                                                                                          |
| chunkLength          | false         | 10                                                           | The length (in seconds) of fragments to be made.                                                                                                                                                |
| chunkOnIDR           | false         | 0 *(false)*                                                  | If 1 (true), chunking is performed ONLY on IDR. Otherwise, chunking is performed whenever chunk length is achieved.                                                                             |
| keepAlive            | false         | 1 *(true)*                                                   | If 1 (true), the EMS will attempt to reconnect to the stream source if the connection is severed.                                                                                               |
| overwriteDestination | false         | 1 *(true)*                                                   | If 1 (true), it will allow overwrite of destination files.                                                                                                                                      |
| staleRetentionCount  | false         | *If not specified, it will have the value of playlistLength* | How many old files are kept besides the ones present in the current version of the playlist. Only applicable for rolling playlists.                                                             |
| cleanupDestination   | false         | 0 *(false)*                                                  | If 1 (true), all manifest and fragment files in the target folder will be removed before MSS creation is started.                                                                               |

An example of the createMSSStream interface is:

    createMSSStream localstreamnames=msstest bandwidth=128 targetfolder=/MyWebRoot/ groupname=group1 chunkLength=10

To playback the created MSS stream, use a Smooth Streaming player such as one of the following:

-	[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)
-	[http://playready.directtaps.net/pr/doc/slee/](http://playready.directtaps.net/pr/doc/slee/)

    http://My_IP_or_Domain/group1/manifest

Enter the following stream URL:

In other words: `http://<my_web_server>/<MSS_group_name>/<manifest_file_name>`

| API           | createMSSStream localstreamnames=testpullStream targetfolder=../evo-webroot groupname=mss                                                                                                                                                                                                                                                                                                                                                      |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"bandwidths":[0],"chunkLength":10,"chunkOnIDR":true,"cleanupDestination":false,"configIds":[10],"groupName":"mss","isLive":"true","ismType":"ismc","keepAlive":true,"localStreamNames":["testpullStream"],"manifestName":"manifest.ismc","overwriteDestination":true,"playlistLength":10,"playlistType":"appending","staleRetentionCount":10,"targetFolder":"..\/evo-webroot"},"description":"MSS stream created","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	bandwidths – An array of integers specifying the bandwidths used for streaming.
	-	chunkLength – The length (in seconds) of each playlist element (.ismc files)
	-	chunkOnIdr – If true, chunking was made on IDR boundary.
	-	cleanupDestination – If true, MSS files at the target folder were deleted before MSS creation began.
	-	configIds - The configuration IDs for this command
	-	groupName – The name of the target folder where MSS files will be created.
	-	isLive - ??
	-	keepAlive – If true, the stream will attempt to reconnect if the connection is severed.
	-	localStreamNames – An array of local names for the streams.
	-	manifestName – The file name of the manifest file. If blank, defaults to 'manifest'.
	-	overwriteDestination – If true, overwriting of destination files during MSS creation is allowed.
	-	playlistLength – The number of fragments before the server starts to overwrite the older fragments. Useful only for `rolling` playlistType.
	-	playlistType – Either `appending` or `rolling`.
	-	staleRetentionCount – The number of old files kept besides the ones listed in the current version of the manifest. Only applicable to rolling playlist type.
	-	targetFolder – The folder where all the manifest and chunk files are stored.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### createDASHStream

Create Dynamic Adaptive Streaming over HTTP (DASH) out of an existing H.264/AAC stream. DASH was developed by the Moving Picture Experts Group (MPEG) to establish a standard for HTTP adaptive-bitrate streaming that would be accepted by multiple vendors and facilitate interoperability.

This function has the following parameters:

| **Parameter Name**   | **Mandatory** | **Default Value**                                            | **Description**                                                                                                                                                                                  |
|----------------------|---------------|--------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| localStreamNames     |               |                                                              |                                                                                                                                                                                                  |
|                      | true          | *(null)*                                                     | The stream(s) that will be used as the input. This is a comma-delimited list of active stream names (local stream names).                                                                        |
| targetFolder         | true          | *(null)*                                                     | The folder where all the manifest and fragment files will be stored. This folder must be accessible by the DASH clients. It is usually in the web-root of the server.                            |
| bandwidths           | false         | 0                                                            | The corresponding bandwidths for each stream listed in localStreamNames. Again, this can be a comma-delimited list.                                                                              |
| groupName            | false         | *dash_group_xxxx (random)*                                 | The name assigned to the DASH stream or group. If the localStreamNames parameter contains only one entry and groupName is not specified, groupName will have the value of the input stream name. |
| playlistType         | false         | appending                                                    | Either `appending` or `rolling`                                                                                                                                                                  |
| playlistLength       | false         | 10                                                           | The number of fragments before the server starts to overwrite the older fragments. Used only when playlistType is 'rolling'. Ignored otherwise.                                                  |
| manifestName         | false         | 'manifest.mpd'                                               | The manifest file name                                                                                                                                                                           |
| chunkLength          | false         | 10                                                           | The length (in seconds) of fragments to be made.                                                                                                                                                 |
| chunkOnIDR           | false         | 1 *(true)*                                                   | If 1 (true), chunking is performed ONLY on IDR. Otherwise, chunking is performed whenever chunk length is achieved.                                                                              |
| keepAlive            | false         | 1 *(true)*                                                   | If 1 (true), the EMS will attempt to reconnect to the stream source if the connection is severed.                                                                                                |
| overwriteDestination | false         | 1 *(true)*                                                   | If 1 (true), it will allow overwrite of destination files.                                                                                                                                       |
| staleRetentionCount  | false         | *If not specified, it will have the value of playlistLength* | How many old files are kept besides the ones present in the current version of the playlist. Only applicable for rolling playlists.                                                              |
| cleanupDestination   | false         | 0 *(false)*                                                  | If 1 (true), all manifest and fragment files in the target folder will be removed before DASH creation is started.                                                                               |
| dynamicProfile       | false         | *1 (true)*                                                   | Set this parameter to 1 (default) for a live DASH, otherwise set it to 0 for a VOD.                                                                                                              |

An example of the createDASHStream interface is:

    createDASHStream localstreamnames=dashtest bandwidth=128 targetfolder=/MyWebRoot/ groupname=group1 rolling=true rollingLimit=10 chunkLength=10

To playback the created DASH stream, use a DASH player such as the following:

    http://digitalprimates.net/dash/dashTest.html

This player is the most stable for EMS DASH playback but it doesn't support live profile for EMS DASH.

Enter the following stream URL:

    http://My_IP_or_Domain/group1/manifest.mpd

In other words: `http://<my_web_server>/<dash_group_name>/<manifest_file_name>`

An alternative DASH player, GPAC Osmo4, can be downloaded from here:

[http://gpac.wp.mines-telecom.fr/downloads/gpac-nightly-builds/](http://gpac.wp.mines-telecom.fr/downloads/gpac-nightly-builds/)

This player supports MPEG-DASH live profile for EMS DASH.

Another DASH player, Dash.as, can be downloaded from here:

[https://github.com/castlabs/dashas](https://github.com/castlabs/dashas)

| API           | createDASHStream localstreamnames=testpullStream targetfolder=../evo-webroot groupname=dash                                                                                                                                                                                                                                                                                                                                           |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"bandwidths":[0],"chunkLength":10,"chunkOnIDR":true,"cleanupDestination":false,"configIds":[11],"dynamicProfile":true,"groupName":"dash","keepAlive":true,"localStreamNames":["testpullStream"],"manifestName":"manifest.mpd","overwriteDestination":true,"playlistLength":10,"playlistType":"appending","staleRetentionCount":10,"targetFolder":". .\/evo-webroot"},"description":"DASH stream created","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	bandwidths – An array of integers specifying the bandwidths used for streaming.
	-	chunkLength – The length (in seconds) of each playlist element (.mpd files)
	-	chunkOnIdr – If true, chunking was made on IDR boundary.
	-	cleanupDestination – If true, DASH files at the target folder were deleted before DASH creation began.
	-	configIds - The configuration IDs for this command
	-	dynamicProfile – Tells if the DASH stream is a live or VOD
	-	groupName – The name of the target folder where DASH files will be created.
	-	keepAlive – If true, the stream will attempt to reconnect if the connection is severed.
	-	localStreamNames – An array of local names for the streams.
	-	manifestName – The file name of the manifest file. If blank, defaults to 'manifest'.
	-	overwriteDestination – If true, overwriting of destination files during DASH creation is allowed.
	-	playlistLength – The number of fragments before the server starts to overwrite the older fragments. Useful only for `rolling` playlistType.
	-	playlistType – Either `appending` or `rolling`.
	-	staleRetentionCount – The number of old files kept besides the ones listed in the current version of the manifest. Only applicable to rolling playlist type.
	-	targetFolder – The folder where all the manifest and chunk files are stored.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### record

Records any inbound stream. The record command allows users to record a stream that may not yet exist. When a new stream is brought into the server, it is checked against a list of streams to be recorded.

Streams can be recorded as FLV files, MPEG-TS files or as MP4 files.

| **Parameter Name**  | **Mandatory** | **Default Value** | **Description**                                                                                                                                                                            |
|---------------------|---------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| localStreamName     | true          | *(null)*          | The name of the stream to be used as input for recording.                                                                                                                                  |
| pathToFile          | true          | *(null)*          | Specify path and file name to write to.                                                                                                                                                    |
| type                | false         | mp4               | "ts", "mp4" or "flv".                                                                                                                                                                      |
| overwrite           | false         | 0 *(false)*       | If false, when a file already exists for the stream name, a new file will be created with the next appropriate number appended. If 1 (true), files with the same name will be overwritten. |
| keepAlive           | false         | 1 *(true)*        | If 1 (true), the server will restart recording every time the stream becomes available again.                                                                                              |
| chunkLength         | false         | 0 *(disabled)*    | If non-zero the record command will start a new recording file after ChunkLength seconds have elapsed                                                                                      |
| waitForIDR          | false         | 1 (*true)*        | This is used if the recording is being chunked. When true, new files will only be created on IDR boundaries                                                                                |
| winQtCompat         | false         | 0 *(false)*       | Mandates 32bit header fields to ensure compatibility with Windows QuickTime.                                                                                                               |
| dateFolderStructure | false         | 0 *(false)*       | If set to 1 (true), folders will be created with names in YYYYMMDD format. Recorded files will be placed inside these folders based on the date they were created.                         |

An example of the record interface is:

    record localStreamName=video1 pathtofile=/recording/path type=mp4 overwrite=1

This records the local stream named video1 to directory /recording/path in mp4 format with overwrite enabled.

| API           | record localStreamName=testpullstream pathtofile=../media/testRecord type=mp4 overwrite=1                                                                                                                                                                                                                                                                                                                                 |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"chunkLength":0,"computedPathToFile":"..\/media\/testRecord.mp4","configId":12,"dateFolderStructure":false,"hasAudio":true,"keepAlive":true,"localStreamName":"testpullstream","mp4BinPath":"..\\evo-mp4writer.exe","operationType":7,"overwrite":true,"pathToFile":"..\/media\/testRecord ","preset":0,"type":"mp4","waitForIDR":false,"winQtCompat":true},"description":"Recording Stream","status":"SUCCESS"} |

The JSON response contains the following details about recording a stream:

-	data – The data to parse.
	-	chunkLength - The length (in seconds) of each playlist element
	-	computedPathToFile – The path and file name of the recorded stream
	-	configID – The configuration ID for this command
	-	dateFolderStructure – If true, will organize record chunks by date
	-	hasAudio – Indicates if the recorded stream has audio, false if none
	-	keepAlive – If true, the stream will attempt to reconnect if the connection is severed.
	-	localStreamName – The local name for the stream.
	-	mp4BinPath-??
	-	operationType – The type of operation
	-	overwrite – If true, files with the same name will be overwritten.
	-	pathToFile – Path to the folder where recorded files will be written.
	-	preset - ??
	-	type – Type of file for recording. Either `flv`,`ts`, or 'mp4'.
	-	waitForIDR – If true, new files will only be created on IDR boundaries
	-	winQtCompat – If true, andates 32bit header fields to ensure compatibility with Windows QuickTime
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### transcode

This function changes the compression characteristics of an audio and/or video stream. This function allows you to change the resolution of a source stream, change the bitrate of a stream, change a VP8 or MPEG2 stream into H.264 and much more. This function will also allow users to create overlays on the final stream as well as crop streams.

**Transcoding requires SIGNIFICANT computing resources and will severely impact performance. A general guideline is that you can accomplish one transcoding job per CPU core for HD streams.**

**IMPORTANT NOTES:**

-	For any parameter that is pluralized, you may specify one value, or multiple. Multiple values must be separated by only a comma (comma-delimited). Specifying multiple values indicates multiple new streams will be created.
-	There must be the same number of values for all pluralized parameters. Oder is important: all first values are grouped together to make the first stream, all second parameters are grouped to make the second stream, etc…
-	Video related parameters are ignored if the parameter _ **videoBitrates** _ is not specified.
-	Audio related parameters are ignored if the parameter _ **audioBitrates** _ is not specified.

This function has the following parameters:

| **Parameter Name**          | **Mandatory** | **Default Value**                | **Description**                                                                                                                                                                                                                                              |
|-----------------------------|---------------|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| source                      | true          | *(null)*                         | Can be a URI or a local stream name from EMS.                                                                                                                                                                                                                |
| destinations                | true          | *(null)*                         | The target URI(s) or stream name(s) of the transcoded stream. If only a name is given, it will be pushed back to the EMS.                                                                                                                                    |
| targetStreamNames           | false         | transcoded_xxxx (timestamp)     | The name of the stream(s) at destination(s). If not specified, and a full URI is provided to destinations, name will have a time stamped value.                                                                                                              |
| groupName                   | false         | transcoded_group_xxxx (random) | The group name assigned to this process. If not specified, groupName will have a random value.                                                                                                                                                               |
| videoBitrates               | false         | input video's bitrate            | Target output video bitrate(s) (in bits/s, append 'k' to value for kbits/s). Accepts the value 'copy' to copy the input bitrate. An empty value passed would mean no video.                                                                                  |
|                             |               |                                  |                                                                                                                                                                                                                                                              |
| videoSizes                  | false         | input video's size               | Target output video size(s) in wxh (width x height) format. IE: 240x480                                                                                                                                                                                      |
| videoAdvancedParamsProfiles | false         | *(null)*                         | Name of video profile template that will be used. See the contents of 'evo-avconv-presets' folder for sample file presets.                                                                                                                                   |
| audioBitrates               | false         | input audio's bitrate            | Target output audio bitrate(s) (in bits/s, append 'k' to value for kbits/s). Accepts the value 'copy' to copy the input bitrate. An empty value passed would mean no audio.                                                                                  |
| audioChannelsCounts         | false         | input audio's channel count      | Target output audio channel(s) count(s). Valid values are 1 (mono), 2 (stereo), and so on. Actual supported channel count is dependent on the number of input audio channels.                                                                                |
| audioFrequencies            | false         | input audio's frequency          | Target output audio frequency(ies) (in Hz, append 'k' to value for kHz).                                                                                                                                                                                     |
| audioAdvancedParamsProfiles | false         | *(null)*                         | Name of audio profile template that will be used.                                                                                                                                                                                                            |
| overlays                    | false         | *(null)*                         | Location of the overlay source(s) to be used. These are transparent images (normally in PNG format) that have the same or smaller size than the video. Image is placed at the top-left position of the video.                                                |
| croppings                   | false         | *(null)*                         | Target video cropping position(s) and size(s) in 'left : top : width : height' format (e.g. 0:0:200:100. Positions are optional (200:100 for a centered cropping of 200 width and 100 height in pixels). Values are limited to the actual size of the video. |
| keepAlive                   | false         | 1 *(true)*                       | If keepAlive is set to 1, the server will restart transcoding if it was previously activated.                                                                                                                                                                |

An example of the transcode command is:

    transcode source=rtmp://<RTMP server>/live/streamname groupName=group videoBitrates=200k destinations=stream1

    transcode source=rtmp://<RTMP server>/live/streamname groupName=group videoBitrates=100k,200k,300k destinations=stream100,stream200,stream300

**Transcode Examples:**

To transcode an RTMP source into different video bitrates and send back to EMS

    transcode source=stream1 groupName=group audioBitrates=copy audioChannelsCounts=1 destinations=rtmp://<RTMP server 2> targetStreamNames=streamMono

To transcode an existing EMS stream into a different audio channel count and send to an RTMP server

    transcode source=file://C:\videos\test.mp4 groupName=group videoBitrates=100k audioBitrates=copy destinations=file://C:\videos\out.mp4

To use files as input and/or output

    transcode source=rtsp://<RTSP server>/live/streamname groupName=group videoBitrates=copy videoSizes=360x200 $EMS_RTSP_TRANSPORT=tcp

To force TCP for inbound RTSP

    removeConfig groupName=group

To stop a running transcoding process(es)

**Transcoding Customizations:**

    transcoder = { scriptPath="emsTranscoder", srcUriPrefix="rtsp://localhost:5544/", dstUriPrefix="-f flv tcp://localhost:6666/" },

To configure the transcoder script settings, edit the file **config.lua** and edit the following entries as needed:

To change the location of the actual trancoder binary, edit the file **emsTranscoder.sh** (linux/unix) and **emsTranscoder.cmd** (windows); and change the following line:

    TRANSCODER_BIN=/usr/bin/evo-avconv (linux/unix)

or

    set TRANSCODER_BIN=..\evo-avconv.exe (windows)

| API           | transcode source=rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 groupName=group videoBitrates=200k destinations=stream1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"audioAdvancedParamsProfiles":["na"],"audioBitrates":["na"],"audioChannelsCounts":["na"],"audioFrequencies":["na"],"croppings":["na"],"destinations":["stream1"],"dstUriPrefix":"-f flv tcp:\/\/localhost:6666\/","emsTargetStreamName":"stream1","fullBinaryPath":"C:\\EvoStream\\emsTranscoder.bat","groupName":"group","keepAlive":true,"localStreamName":"","overlays":["na"],"source":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","srcUriPrefix":"rtsp:\/\/localhost:5544\/","targetStreamNames":["stream1"],"videoAdvancedParamsProfiles":["na"],"videoBitrates":["200k"],"videoSizes":["na"]},"description":"Transcoding successfully started.","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	audioAdvancedParamsProfiles - An array of strings specifying the name of profile presets to be used for audio
	-	audioBitrates - An array of integers for target audio output bitrates
	-	audioChannelsCounts - An array of values for the target number of audio channels
	-	croppings - An array of values for the target cropping positions and size
	-	destinations - An array of target URIs or stream names
	-	dstUriPrefix - Default destination if destination is a stream name
	-	emsTargetStreamName - Target stream name used internally by EMS
	-	fullBinaryPath - Actual location of the transcoder binary
	-	groupName - Name of the group associated with this transcoding process
	-	keepAlive - Transcoding will restart if previously activated
	-	localStreamName - Actual EMS stream name of source (if given)
	-	overlays - An array of locations for the images to be used as overlays
	-	source - The actual stream/file to be used as input for transcoding
	-	srcUriPrefix - Default source if given source is a stream name
	-	targetStreamNames - An array of the target stream names to be used at the destination
	-	videoAdvancedParamsProfiles - An array of strings specifying the name of profile presets to be used for video
	-	videoBitrates - An array of values for target video output bitrates
	-	videoSizes - An array of values for target video sizes
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### listStreamsIds

Get a list of IDs for every active stream.

This function has no parameters.

| API           | listStreamsIds                                                                 |
|---------------|--------------------------------------------------------------------------------|
| JSON Response | {"data":[205,206,207],"description":"Available stream IDs","status":"SUCCESS"} |

A JSON message will be returned containing the IDs of the active streams:

-	data – Contains an array of IDs (integers) for the active streams.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### getStreamInfo

Returns a detailed set of information about a stream

| **Parameter Name** | **Mandatory** | **Default Value**         | **Description**                                                                                                                                                                                     |
|--------------------|---------------|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                 | true          | *(null)*                  | The uniqueId of the stream. Usually a value returned by listStreamsIDs. This parameter is not mandatory but either this or the localStreamName should be present to identify the particular stream. |
| localStreamName    | true          | "" *(zero length String)* | The name of the stream. This parameter is not mandatory but either this or the id should be present to identify the particular stream.                                                              |

| API           | getStreamInfo id=1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"appName":"evostreamms","audio":{"bytesCount":168860,"codec":"AAAC","codecNumeric":4702111241970122752,"droppedBytesCount":0,"droppedPacketsCount":0," packetsCount":521},"bandwidth":0,"connectionType":1,"creationTimestamp":14480039 54598.3130,"farIp":"54.239.131.151","farPort":1935,"ip":"192.168.2.35","name":"t estpullstream","nearIp":"192.168.2.35","nearPort":1299,"outStreamsUniqueIds":null,"pageUrl":"","port":1299,"processId":12848,"processType":"origin","pullSetting s":{"_callback":*null*,"audioCodecBytes":"","configId":1,"emulateUserAgent":"EvoSt ream Media Server (www.evostream.com) player","forceTcp":false,"httpProxy":"","isAudio":true,"keepAlive":true,"localStreamName":"testpullstream","operationType":1,"pageUrl":"","ppsBytes":"","rangeEnd":-1,"rangeStart":-2,"rtcpDetectionInterv al":10,"sendRenewStream":false,"spsBytes":"","ssmIp":"","swfUrl":"","tcUrl":"","tos":256,"ttl":256,"uri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:s intel.mp4"},"queryTimestamp":1448003961907.7310,"serverAgent":"FMS\/3,5,7,7009","swfUrl":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","tcUr l":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","type":"INR ","typeNumeric":5282249572905648128,"uniqueId":1,"upTime":7309.4180,"video":{"bytesCount":825054,"codec":"VH264","codecNumeric":6217274493967007744,"droppedByte sCount":0,"droppedPacketsCount":0,"height":306,"level":30,"packetsCount":291,"profile":66,"width":720}},"description":"Stream information","status":"SUCCESS"} |

The JSON response contains the following details about a given stream:

-	data – The data to parse.
	-	appName - ??
	-	audio – stats about the audio portion of the stream.
	-	bytesCount - Total amount of audio data received.
	-	codec - ??
	-	codecNumeric - ??
	-	droppedBytesCount - The number of video bytes lost
	-	droppedPacketsCount – The number of lost audio packets.
	-	packetsCount – Total number of audio packets received.
	-	bandwidth – The current bandwidth utilization of the stream.
	-	connectionType - ??
	-	creationTimestamp – The UNIX timestamp for when the stream was created. UNIX time is expressed as the number of seconds since the UNIX Epoch (Jan 1, 1970).
	-	farIp - The IP address of the distant party
	-	farPort - The port used by the distant party
	-	ip - IP address of the source stream's host
	-	name – the "localStreamName" for this stream.
	-	nearIp - The IP address used by the local computer
	-	nearPort - The port used by the local computer
	-	outStreamsUniqueIDs – *For pulled streams*. An array of the "out" stream IDs associated with this "in" stream.
	-	pageUrl - A link to the page that originated the request (often unused).
	-	port - The port bound to the service
	-	processID - ??
	-	preocessType - ??
	-	pullSettings/pushSettings – Not present for streams requested by a 3rd party (IE player/client). A copy of the parameters used in the **pullStream** or **pushStream** command.
	-	_callback - ??
	-	audioCodecBytes - The audio codec setup of this RTP stream if it is audio
	-	configId – The identifier for the pullPushConfig.xml entry.
	-	emulateUserAgent – The string that the EMS uses to identify itself with the other server. It can be modified so that EMS identifies itself as, say, a Flash Media Server.
	-	forceTcp – Whether TCP MUST be used, or if UDP can be used.
	-	httpProxy - May either be IP:Port combination or self
	-	isAudio - Indicates if the currently pulled stream is an audio source
	-	keepAlive – If true, the stream will try to reconnect if the connection is severed.
	-	localStreamName – Same as the above "name" field.
	-	operationType – The type of operation
	-	pageUrl – A link to the page that originated the request (often unused).
	-	ppsBytes - The video PPS bytes of this RTP stream if it is video
	-	rangeEnd - The length in seconds for the playback
	-	rangeStart - A value from which the playback should start expressed in seconds
	-	rtcpDetectionInterval – Used for RTSP. This is the time period the EMS waits to determine if an RTCP connection is available for the RTSP/RTP stream. (RTSP is used for synchronization between audio and video).
	-	sendRenewStream - If 1, the server will send RenewStream via SET_PARAMETER when a new client connects
	-	spsBytes - The video SPS bytes of this RTP stream if it is video
	-	swfUrl – The location of the Flash Client that is generating the stream (if any)
	-	tcUrl – An RTMP parameter that is essentially a copy of the URI
	-	tos – Type of Service network flag
	-	ttl – Time To Live network flag
	-	uri – The parsed values of the source streams URI
	-	queryTimestamp – The time (in UNIX seconds) when the information in this request was populated.
	-	serverAgent - ??
	-	swfUrl - The location of the Flash Client that is generating the stream (if any)
	-	tcUrl - An RTMP parameter that is essentially a copy of the URI
	-	type – The type of stream this is. The first two characters are of most interest:
	-	char 1 = I for inbound, O for outbound.
	-	char 2 = N for network, F for file.
	-	char 3+ = further details about stream.
	-	example: INR = Inbound Network Stream (a stream coming from the network into the EMS).
	-	typeNumeric - ??
	-	uniqueId – The unique ID of the stream (integer).
	-	upTime – The time in seconds that the stream has been alive/running for.
	-	video – Stats about the video portion of the stream.
	-	bytesCount - Total amount of video data received.
	-	codec - ??
	-	codecNumeric - ??
	-	droppedBytesCount – The number of video bytes lost.
	-	droppedPacketsCount – The number of lost video packets.
	-	height - The video stream's pixel height
	-	level - ??
	-	packetsCount – Total number of video packets received.
	-	profile - ??
	-	width - The video stream's pixel width
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### listStreams

Provides a detailed description of all active streams.

| **Parameter Name**     | **Mandatory** | **Default Value** | **Description**                                                                             |
|------------------------|---------------|-------------------|---------------------------------------------------------------------------------------------|
| disableInternalStreams | false         | *1 (true)*        | If this is 1 (true), internal streams (origin-edge related) are filtered out from the list. |

| API           | listStreams                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":[{"appName":"evostreamms","audio":{"bytesCount":727893,"codec":"AAAC","codecNumeric":4702111241970122752,"droppedBytesCount":0,"droppedPacketsCount":0,"packetsCount":2243},"bandwidth":0,"connectionType":1,"creationTimestamp":14480 05740350.4519,"edgePid":0,"farIp":"54.239.131.224","farPort":1935,"ip":"192.168. 2.35","name":"testpullstream","nearIp":"192.168.2.35","nearPort":1607,"outStream sUniqueIds":*null*,"pageUrl":"","port":1607,"processId":12848,"processType":"origi n","pullSettings":{"_callback":*null*,"audioCodecBytes":"","configId":1,"emulateUs erAgent":"EvoStream Media Server (www.evostream.com) player","forceTcp":false,"httpProxy":"","isAudio":true,"keepAlive":true,"localStreamName":"testpullstream","operationType":1,"pageUrl":"","ppsBytes":"","rangeEnd":-1,"rangeStart":-2,"rtcp DetectionInterval":10,"sendRenewStream":false,"spsBytes":"","ssmIp":"","swfUrl":"","tcUrl":"","tos":256,"ttl":256,"uri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\ /cfx\/st\/mp4:sintel.mp4"},"queryTimestamp":1448005784755.9919,"serverAgent":"FM S\/3,5,7,7009","swfUrl":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:si ntel.mp4","tcUrl":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.m p4","type":"INR","typeNumeric":5282249572905648128,"uniqueId":36,"upTime":44405.5400,"video":{"bytesCount":4881934,"codec":"VH264","codecNumeric":62172744939670 07744,"droppedBytesCount":0,"droppedPacketsCount":0,"height":306,"level":30,"pac ketsCount":1255,"profile":66,"width":720}}],"description":"Available streams","status":"SUCCESS"} |

The JSON response contains the following details about each stream:

-	data – The data to parse.
	-	appName - ??
	-	audio – stats about the audio portion of the stream.
	-	bytesCount – Total amount of audio data received.
	-	codec - ??
	-	codecNumeric - ??
	-	droppedBytesCount - The number of video bytes lost
	-	droppedBytesCount – The number of audio bytes lost.
	-	droppedPacketsCount – The number of lost audio packets.
	-	packetsCount – Total number of audio packets received.
	-	bandwidth – The current bandwidth utilization of the stream.
	-	connectionType - ??
	-	canDropFrames – *Outstreams only*. Flag set by client allowing for dropped frames/packets.
	-	creationTimestamp – The UNIX timestamp for when the stream was created. UNIX time is expressed as the number of seconds since the UNIX Epoch (Jan 1, 1970).
	-	edgePid – Internal flag used for clustering.
	-	farIp - The IP address of the distant party
	-	farPort - The port used by the distant party
	-	ip - IP address of the source stream's host
	-	inStreamUniqueID – *For pushed streams.* The id of the source stream.
	-	name – the "localstreamname" for this stream.
	-	nearIp - The IP address used by the local computer
	-	nearPort - The port used by the local computer
	-	outStreamsUniqueIDs – *For pulled streams.* An array of the "out" stream IDs associated with this "in" stream.
	-	pageUrl - A link to the page that originated the request (often unused).
	-	port - The port bound to the service
	-	processId - ??
	-	processType - ??
	-	pullSettings/pushSettings – *Not present for streams requested by a 3__rd* *party (IE player/client).* A copy of the parameters used in the **pullStream** or **pushStream** command.
	-	configId – The identifier for the pullPushConfig.xml entry.
	-	emulateUserAgent – The string that the EMS uses to identify itself with the other server. It can be modified so that EMS identifies itself as, say, a Flash Media Server.
	-	forceTcp – Whether TCP MUST be used, or if UDP can be used.
	-	httpProxy - May either be IP:Port combination or self
	-	isAudio - Indicates if the currently pulled stream is an audio source
	-	keepAlive – If true, the stream will try to reconnect if the connection is severed
	-	localStreamName – Same as the above "name" field.
	-	operationType – The type of operation
	-	pageUrl – A link to the page that originated the request (often unused).
	-	ppsBytes - The video PPS bytes of this RTP stream if it is video
	-	rangeEnd - The length in seconds for the playback
	-	rangeStart - A value from which the playback should start expressed in seconds
	-	rtcpDetectionInterval – Used for RTSP. This is the time period the EMS waits to determine if an RTCP connection is available for the RTSP/RTP stream. (RTSP is used for synchronization between audio and video).
	-	sendRenewStream - If 1, the server will send RenewStream via SET_PARAMETER when a new client connects
	-	spsBytes - The video SPS bytes of this RTP stream if it is video
	-	ssmIp - The source IP from source-specific-multicast
	-	swfUrl – The location of the Flash Client that is generating the stream (if any).
	-	tcUrl – An RTMP parameter that is essentially a copy of the URI.
	-	tos – Type of Service network flag.
	-	ttl – Time To Live network flag.
	-	uri – The parsed values of the source streams URI.
	-	queryTimestamp – The time (in UNIX seconds) when the information in this request was populated.
	-	serverAgent - ??
	-	swfUrl - The location of the Flash Client that is generating the stream (if any)
	-	tcUrl - An RTMP parameter that is essentially a copy of the URI
	-	type – The type of stream this is. The first two characters are of most interest:
	-	char 1 = I for inbound, O for outbound.
	-	char 2 = N for network, F for file.
	-	char 3+ = further details about stream.
	-	example: INR = Inbound Network Stream (a stream coming from the network into the EMS).
	-	typeNumeric - ??
	-	uniqueId – The unique ID of the stream (integer).
	-	uptime – The time in seconds that the stream has been alive/running for.
	-	video – Stats about the video portion of the stream.
	-	bytesCount – Total amount of video data received.
	-	codec - ??
	-	codecNumeric - ??
	-	droppedBytesCount – The number of video bytes lost.
	-	droppedPacketsCount – The number of lost video packets.
	-	height – The video stream's pixel height.
	-	level - ??
	-	packetsCount – Total number of video packets received.
	-	profile - ??
	-	width - The video stream's pixel width.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### getStreamsCount

Returns the number of active streams.

This function has no parameters.

| API           | getStreamsCount                                                                     |
|---------------|-------------------------------------------------------------------------------------|
| JSON Response | {"data":{"streamCount":1},"description":"Active streams count","status":"SUCCES S"} |

A JSON message will be returned giving the number of active streams:

-	data – The data to parse.
	-	streamCount – The number of active streams.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### shutdownStream

Terminates a specific stream. When permanently=1 is used, this command is analogous to removeConfig

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value**         | **Description**                                                                                                                                                                                                                                                     |
|--------------------|---------------|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                 | True          | *0*                       | The uniqueId of the stream that needs to be terminated. The stream ID's can be obtained using the listStreams command. This parameter is not mandatory but either this or localStreamName should be present to identify the particular stream.                      |
| localStreamName    | true          | "" *(zero length String)* | The name of the inbound stream which you wish to terminate. This will also terminate any outbound streams that are dependent upon this input stream. This parameter is not mandatory but either this or the id should be present to identify the particular stream. |
| permanently        | false         | 1 *(true)*                | If true, the corresponding push/pull configuration will also be terminated. Therefore, the stream will NOT be reconnected when the server restarts.                                                                                                                 |

    shutdownstream id=55 permanently=1

An example of the shutdownStream interface is:

This will shut down the stream with id of 55 and remove its push/pull configuration.

| API           | shutdownstream id=55                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"protocolStackInfo":{"carrier":{"farIP":"54.239.131.57","farPort":1935,"id":601,"nearIP":"192.168.2.35","nearPort":2326,"rx":3077367,"tx":3653,"type":"IOHT_TCP_CARRIER"},"stack":[{"applicationId":0,"creationTimestamp":1448008702269.8640,"id":794,"isEnqueueForDelete":false,"queryTimestamp":1448008724139.1150," type":"TCP"},{"applicationId":1,"creationTimestamp":1448008702269.8640,"id":795,"isEnqueueForDelete":false,"queryTimestamp":1448008724139.1150,"rxInvokes":31,"serverAgent":"FMS\/3,5,7,7009","streams":[{"appName":"evostreamms","audio":{"bytesCount":348883,"codec":"AAAC","codecNumeric":4702111241970122752,"droppedBytesCo unt":0,"droppedPacketsCount":0,"packetsCount":1068},"bandwidth":0,"connectionTyp e":1,"creationTimestamp":1448008702871.8989,"farIp":"54.239.131.57","farPort":1935,"ip":"192.168.2.35","name":"testpullstream","nearIp":"192.168.2.35","nearPort ":2326,"outStreamsUniqueIds":[91],"pageUrl":"","port":2326,"processId":12848,"processType":"origin","pullSettings":{"_callback":*null*,"audioCodecBytes":"","configId":1,"emulateUserAgent":"EvoStream Media Server (www.evostream.com) player","forceTcp":false,"httpProxy":"","isAudio":true,"keepAlive":true,"localStreamName":"testpullstream","operationType":1,"pageUrl":"","ppsBytes":"","rangeEnd":-1,"rangeStart":-2,"rtcpDetectionInterval":10,"sendRenewStream":false,"spsBytes":"","ssmIp":"","swfUrl":"","tcUrl":"","tos":256,"ttl":256,"uri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4"},"queryTimestamp":1448008724139.1150,"serverAgent":"FMS\/3,5,7,7009","swfUrl":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","tcUrl":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","type":"INR","typeNumeric":5282249572905648128,"uniqueId":95,"upTime":21267.2161,"video":{"bytesCount":2698244,"codec":"VH264","codecNumeric":6217274493967007744,"droppedBytesCount":0,"droppedPacketsCount":0,"height":306,"level":30,"packetsCount":596,"profile":66,"width":720}}],"txInvokes":7,"type":"OR"}]},"streamInfo":{*--Same with streams group*}}},"description":"Stream closed","status":"SUCCESS"} |

The JSON response contains the following details about the stream being shut down:

-	data – The data to parse.
	-	protocolStackInfo – Contains key/value pairs describing the protocol stack used by the stream.
	-	carrier – Details about the connection itself.
		-	farIP – The IP address of the distant party
		-	farPort – The port used by the distant party
		-	nearIP – The IP address used by the local computer
		-	nearPort – The port used by the local computer
		-	rx – Total bytes received on this connection.
		-	tx – Total bytes transferred on this connection.
		-	type – The connection type (TCP, UDP) .
	-	stack[1] – Describes the farthest protocol primitive.
		-	applicationID – the ID of the internal application using the connection.
		-	creationTimestamp – The time (in UNIX seconds) when the application started using the connection.
		-	id – The unique ID for this stack relation.
		-	isEnqueueForDelete – Internal flag used for cleanup.
		-	queryTimestamp – The time (in UNIX seconds) when this data was populated.
		-	type – A descriptor for how the application is using the connection.
	-	stack[2] – Describes the next protocol primitive.
		-	applicationId – the ID of the internal application using the connection.
		-	creationTimestamp – The time (in UNIX seconds) when the application started using the connection.
		-	id – The unique ID for this stack relation.
		-	isEnqueueForDelete – Scheduled for deletion.
		-	queryTimestamp – The time (in UNIX seconds) when this data was populated.
		-	rxInvokes – Number of received RTMP function invokes.
		-	streams[1]
			-	audio – Stats about the audio portion of the stream.

				-	bytesCount – Total amount of audio data received.
				-	droppedBytesCount – The number of audio bytes lost.
				-	droppedPacketsCount – The number of lost audio packets.
				-	packetsCount – Total number of audio packets received.

			-	bandwidth – The current bandwidth utilization of the stream.
			-	canDropFrames – *Outstreams only*. Flag set by client allowing for dropped frames/packets.
			-	creationTimestamp – The time (in UNIX secs) when the stream was created.
			-	inStreamUniqueId – *For pushed streams.* The id of the source stream.
			-	name – the "localstreamname" for this stream.
			-	queryTimestamp – The time (in UNIX secs) when this data was populated.
			-	type – The type of stream this is. See **getStreamInfo** for details.
			-	uniqueId – The unique ID of the stream (integer).
			-	upTime – The time in seconds that the stream has been alive/running for.
			-	video
				-	bytesCount – Total amount of video data received.
				-	droppedBytesCount – The number of video bytes lost.
				-	droppedPacketsCount – The number of lost video packets.
				-	packetsCount – Total number of video packets received.
		-	streams[2]
			-	bandwidth – The current bandwidth utilization of the stream.
			-	creationTimestamp – The time (in UNIX secs) when the stream was created.
			-	name – the "localstreamname" for this stream.
			-	outStreamsUniqueIDs – *For pulled streams.* An array of the "out" stream IDs associated with this "in" stream.
			-	queryTimestamp – The time (in UNIX secs) when this data was populated.
			-	type – The type of stream this is. See **getStreamInfo** for details.
			-	uniqueId – The unique ID of the stream (integer).
			-	uptime – The time in seconds that the stream has been alive/running for.
		-	txInvokes – Number of sent RTMP function invokes.
		-	type – A descriptor for how the application is using the connection.
	-	streamInfo
	-	bandwidth – The current bandwidth utilization of the stream.
	-	creationTimestamp – The time (in UNIX seconds) when the stream was created.
	-	name – the "localstreamname" for this stream.
	-	outStreamsUniqueIds – *For pulled streams.* An array of the "out" stream IDs associated with this "in" stream.
	-	queryTimestamp – The time (in UNIX seconds) when this data was populated.
	-	type – The type of stream this is. See **getStreamInfo** for details.
	-	uniqueId – The unique ID of the stream (integer).
	-	upTime – The time in seconds that the stream has been alive/running for.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### listConfig

Returns a list with all push/pull configurations.

Whenever the pullStream or pushStream interfaces are called, a record containing the details of the pull or push is created in the pullpushconfig.xml file. Then, the next time the EMS is started, the pullpushconfig.xml file is read, and the EMS attempts to reconnect all of the previous pulled or pushed streams.

This function has no parameters.

| API           | listConfig                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"dash":\[*details of dash streams*],"hds":\[*details of hds streams*],"hls":\[*details of hls streams*],"mss":\[*details of mss streams*],"process":\[*details of on process streams*],"pull":\[*details of pulled streams*],"push":\[*details of pushed streams*],"record":\[*details of recorded streams*],"webrtc":\[*details of webRTC streams*]},"description":"Run-time configuration","status":"SUCCESS"} |

The JSON response contains the following details about the pull/push configuration:

-	data – The data to parse.
	-	hds (see fields of **createHDSStream** command)
	-	hls (see fields of **createHLSStream** command)
	-	mss (see fields of **createMSSStream** command)
	-	dash (see fields of **createDASHStream** command)
	-	pull (see fields of **pullStream** command)
	-	push (see fields of **pushStream** command)
	-	record (see fields of **record** command)
	-	status (within the stream types shown above) – array of current and previous states
	-	current/previous
		-	code – An integer representing the state of the stream.
		-	description – Describes the state of the stream.
		-	timestamp – The time (in Unix secs) the state was updated.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### getConfigInfo

Returns the information of the stream by the configId.

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                           |
|--------------------|---------------|-------------------|-----------------------------------------------------------|
| id                 | true          | *(null)*          | The configId of the configuration to get some information |

An example of the getConfigInfo interface is:

| API           | getConfigInfo id=1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"AESKeyCount":5,"audioOnly":false,"bandwidth":0,"chunkBaseName":"segment","chunkLength":10,"chunkOnIDR":true,"cleanupDestination":false,"cleanupOnClose ":false,"configId":1,"createMasterPlaylist":true,"drmType":"none","fileLength":0,"groupName":"HLS","groupTargetFolder":"..\/evo-webroot\\HLS\\","hlsResu me":false,"hlsVersion":3,"keepAlive":true,"localStreamName":"bunny","masterPlayl istPath":"..\/evo-webroot\\HLS\\playlist.m3u8","maxChunkLength":0,"offsetTim e":0,"operationType":3,"overwriteDestination":true,"playlistLength":10,"playlist Name":"playlist.m3u8","playlistType":"appending","staleRetentionCount":10,"start Offset":0,"status":{"current":{"code":0,"description":"Streaming","timestamp":1448958829,"uniqueStreamId":10},"previous":{"code":3,"description":"Connected","timestamp":1448958829,"uniqueStreamId":0}},"targetFolder":"..\/evo-webroot\\HLS\\test_sintel","timestamp":1448955776495.1621,"useByteRange":false,"useSystemTime":false},"description":"Configuration Info","status":"SUCCESS"} |

### removeConfig

This command will both stop the stream and remove the corresponding configuration entry. This command is the same as performing: shutdownStream permanently=1

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                                                                                                                                                                                               |
|--------------------|---------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                 | true          | *(null)*          | The configId of the configuration that needs to be removed. ConfigId's can be obtained from the listConfig interface. Removing an inbound stream will also automatically remove all associated outbound streams.\*Mandatory only if the groupName parameter is not specified. |
| groupName          | true          | *(null)*          | The name of the group that needs to be removed (applicable to HLS, HDS and external processes). \*Mandatory only if the id parameter is not specified.                                                                                                                        |
| removeHlsHdsFiles  | false         | 0 *(false)*       | If 1 (true) and the stream is HLS or HDS, the folder associated with it will be removed.                                                                                                                                                                                      |

An example of the removeConfig interface is:

| API           | removeConfig id=555                                                                                   |
|---------------|-------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{*..remove details for clarity*},"description":"Configuration terminated","status":"SUCCESS"} |

The JSON response contains the following details about the pull/push configuration:

-	data – The data to parse.
	-	configId – The identifier for the pullPushConfig.xml entry.
	-	Other fields present are dependent on stream type.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### startwebrtc

Starts a WebRTC Signalling client to an ERS (Evostream Rendezvous Server)

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                        |
|--------------------|---------------|-------------------|--------------------------------------------------------------------------------------------------------|
| ersip              | true          | *(null)*          | IP address (xx.yy.zz.xx) of ERS                                                                        |
| ersport            | true          | *(null)*          | IP address (xx.yy.zz.xx) of ERS                                                                        |
| roomId             | true          | *(null)*          | Unique room Identifier (string) within ERS that will be used by client browsers to connect to this EMS |

An example of the startwebrtc interface is:

    startwebrtc ersip=52.6.14.61 ersport=3535 roomid=ThisIsATestRoomName

This will open port 3535 in IP 52.6.14.61 and will open doors for the room ID which can be accessed using the evowrtcclient.html

| API           | startwebrtc ersip=52.6.14.61 ersport=3535 roomid=ThisIsATestRoomName                                                                                                                                                                                                                           |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"configId":2,"ersip":"52.6.14.61","ersport":3535,"keepAlive":true,"name":"evostreamms","operationType":9,"roomid":"ThisIsATestRoomName","sslCert":"..\/config\/server.cert","sslKey":"..\/config\/server.key"},"description":"Started WebRTC Negotiation Service","status":"SUCCESS"} |

The JSON response contains the following details.

-	data – The data to parse.
	-	configId - The configuration ID for this command
	-	ersip – The IP address of the ERS
	-	ersport – The port of the ERS
	-	keepAlive - ??
	-	name - ??
	-	operationType – The type of operation
	-	roomId – The room identifier
	-	sslCert - The SSL certificate
	-	sslKey - The SSL key certificate
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### stopwebrtc

Stops the WebRTC Signalling client to an ERS (Evostream Rendezvous Server)

This function has no parameters

| API           | stopwebrtc                                                                                                          |
|---------------|---------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"ersip":"","ersport":0,"roomid":""},"description":"Stopped WebRTC Negotiation Service","status":"SUCCESS"} |

The JSON response contains the following details.

-	data – The data to parse.
	-	ersip – The IP address of the ERS
	-	ersport – The port of the ERS
	-	roomId – The room identifier
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.


## Aliasing

### addStreamAlias

Allows you to create secondary name(s) for internal streams. Once an alias is created the localstreamname cannot be used to request playback of that stream. Once an alias is used (requested by a client) the alias is removed. Aliases are designed to be used to protect/hide your source streams.

**Note:**

**hasStreamAliases** in config should be TRUE.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                                                                                                                                                                                                                                  |
|--------------------|---------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| localStreamName    | true          | *(null)*          | The original stream name.                                                                                                                                                                                                                                                                                        |
| aliasName          | true          | *(null)*          | The alias alternative to the localStreamName.                                                                                                                                                                                                                                                                    |
| expirePeriod       | False         | *-600 (10 mins)*  | The expiration period for this alias. Negative values will be treated as one-shot but no longer than the absolute positive value in seconds, 0 means it will not expire, positive values mean the alias can be used multiple times but expires after this many seconds. The default is -600 (one-shot, 10 mins). |

An example of the addStreamAlias interface is:

    addStreamAlias localStreamName=bunny aliasName=video1 expirePeriod=-300

| API           | addStreamAlias localStreamName=MyStream aliasName=video1 expirePeriod=-300                                                        |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"aliasName":"video1","expirePeriod":-300,"localStreamName":"MyStream"},"description":"Alias applied","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse
	-	aliasName – The alias alternative to the localStreamName
	-	expirePeriod – The expiration period for this alias
	-	localStreamName – The original stream name
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not

### listStreamAliases

Returns a complete list of aliases.

This function has no parameters.

| API           | listStreamAliases                                                                                                                                                                                           |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":[{"aliasName":"video1","creationTime":1448267205,"expirePeriod":300,"localStreamName":"MyStream","oneShot":true,"permanent":false}],"description":"Currently available aliases","status":"SUCCESS"} |

The JSON response contains the following details.

-	data – Contains an array of pairs of aliasName and localStreamName.
	-	aliasName – The alias alternative to the localStreamName.
	-	creationTime – ??
	-	expirePeriod - ??
	-	localStreamName – The original stream name.
	-	oneShot -
	-	permanent -
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### removeStreamAlias

Removes an alias of a stream.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**     |
|--------------------|---------------|-------------------|---------------------|
| aliasName          | true          | *(null)*          | The alias to delete |

An example of the removeStreamAlias interface is:

    removeStreamAlias aliasName=video1

| API           | removeStreamAlias aliasName=video1                                                             |
|---------------|------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"aliasName":"video1",}"description":"Currently available aliases","status":"SUCCESS"} |

The JSON response contains the following details.

-	data – The data to parse.
	-	aliasName – The alias of the stream that was removed.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### flushStreamAliases

Invalidates all streams aliases.

This function has no parameters.

| API           | flushStreamAliases                                                       |
|---------------|--------------------------------------------------------------------------|
| JSON Response | {"data":null,"description":"All aliases are flushed","status":"SUCCESS"} |

The JSON response contains the following details.

-	data – Nothing to parse for this command.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### addGroupNameAlias

This command creates secondary name(s) for group names. Once an alias is created the group name cannot be used to request HTTP playback of that stream. Once an alias is used (requested by a client) the alias is removed. Aliases are designed to be used to protect/hide your source streams.

**Note:**

**hasGroupNameAliases** in webconfig should be TRUE.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                          |
|--------------------|---------------|-------------------|------------------------------------------|
| groupName          | true          | *(null)*          | The original group name.                 |
| aliasName          | true          | *(null)*          | The alias alternative to the group name. |

An example of the addGroupNameAlias interface is:

    addGroupNameAlias groupName=MyGroup aliasName=mygroupalias

This sets "mygroupalias" as the alias alternative for the group name "mygroup".

| API           | addGroupNameAlias groupName=MyGroup aliasName=TestGroupAlias                                                                                                                                                                                                       |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"aliasName":"TestGroupAlias","cliProtocolId":97,"edges":[],"edgesCount":0,"groupName":"MyGroup","lastUpdate":1442374870,"operation":"addGroupNameAlias","result":true,"uniqueRequestId":2},"description":"Alias applied to group name","status":"SUCCESS" |

The JSON response contains the following details:

-	data – Provides the following information for the added group name alias:
	-	aliasName – The alias alternative to be added for the group name
	-	cliProtocolId – For internal use
	-	edges – the process IDs and stream IDs for all edge instances
	-	edgesCount – The number of edge instances
	-	groupName – The original group name
	-	lastUpdate – Timestamp
	-	operation – The command executed
	-	result – `true` if the operation succeeded, `false` if not
	-	uniqueRequestId – For internal use
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not

### flushGroupNameAliases

This command invalidates all group name aliases.

The function has no parameter.

| API           | flushGroupNameAliases                                                               |
|---------------|-------------------------------------------------------------------------------------|
| JSON Response | {"data":null,"description":"All group name aliases are flushed","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – null.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### getGroupNameByAlias

This command returns the group name given the alias name.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**          |
|--------------------|---------------|-------------------|--------------------------|
| aliasName          | true          | *(null)*          | The original group name. |

An example of the getGroupNameByAlias interface is:

| API           | getGroupNameByAlias aliasName=TestGroupAlias                                                                                                                                                                                                         |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"aliasName":"TestGroupAlias","cliProtocolId":97,"edges":[],"edgesCount":0,"groupName":"MyGroup","lastUpdate":1442374870,"operation":"getGroupNameByAlias","result":true,"uniqueRequestId":4},"description":"Group name","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – Provides the following information for the added group name alias:
	-	aliasName – The alias alternative to be added for the group name
	-	cliProtocolId – For internal use
	-	edges – the process IDs and stream IDs for all edge instances
	-	edgesCount – The number of edge instances
	-	groupName – The original group name
	-	lastUpdate – Timestamp
	-	operation – The command executed
	-	result – `true` if the operation succeeded, `false` if not
	-	uniqueRequestId – For internal use
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not


### listGroupNameAliases

This command returns a complete list of group name aliases

The function has no parameters.

| API           | listGroupAliases                                                                                                                          |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":[{"aliasName":"TestGroupAlias","groupName":"MyGroup"}],"description":"Currently available group name aliases","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – Provides the following information for each group name alias:
	-	aliasName – The alias alternative to the group name.
	-	groupName – The original group name.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### removeGroupNameAlias

This command removes the alias name of a group name.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                          |
|--------------------|---------------|-------------------|----------------------------------------------------------|
| aliasName          | true          | *(null)*          | The alias alternative to be removed from the group name. |

An example of the removeGroupNameAlias interface is:

    removeGroupNameAlias aliasName=myalias

This removes the alias name "myalias".

| API           | removeGroupNameAlias aliasName=TestGroupAlias                                                                       |
|---------------|---------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"aliasName":"TestGroupAlias""groupName":"MyGroup"},"description":"Group Alias removed","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – Provides the following information for the removed alias:
	-	aliasName – The alias alternative to the group name
	-	groupName – The original group name
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not

removeGroupNameAlias

### createIngestPoint

Creates an RTMP ingest point, which mandates that streams pushed into the EMS have a target stream name which matches one Ingest Point privateStreamName.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                                                      |
|--------------------|---------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| privateStreamName  | true          | *(null)*          | The name that RTMP Target Stream Names must match                                                                                    |
| publicStreamName   | True          | *(null)*          | The name that is used to access the stream pushed to the privateStreamName. The publicStreamName becomes the streams localStreamName |

An example of the createIngestPoint interface is:

    createIngestPoint privateStreamName=theIngestPoint publicStreamName=useMeToViewStream

| API           | createIngestPoint privateStreamName=theIngestPoint publicStreamName=useMeToViewStream                                                          |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"privateStreamName":"theIngestPoint","publicStreamName":"useMeToViewStream"},"description":"Ingest point created","status":"SUCCESS"} |

The JSON response contains the following details.

-	data – The data to parse.
	-	privateStreamName –The privateStreamName which was set.
	-	publicStreamName – The publicStreamName which was set
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### listIngestPoints

Lists the currently available Ingest Points

This function has no parameters

| API           | listIngestPoints                                                                                                                                      |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":[{"privateStreamName":"theIngestPoint ","publicStreamName":"useMeToViewStream"},],"description":"Available ingest points","status":"SUCCESS"} |

The JSON response contains the following details.

-	data – The data to parse.
	-	List of pairs:
	-	privateStreamName –The privateStreamName of the Ingest Point.
	-	publicStreamName – The publicStreamName of the Ingest Point
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### removeIngestPoint

Removes an RTMP ingest point

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                |
|--------------------|---------------|-------------------|------------------------------------------------------------------------------------------------|
| privateStreamName  | true          | *(null)*          | The Ingest Point is identified by the privateStreamName, so only that is required to delete it |

An example of the removeIngestPoint interface is:

    removeIngestPoint privateStreamName=theIngestPoint

| API           | removeIngestPoint privateStreamName=theIngestPoint                                                                                                 |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":[{"privateStreamName":"theIngestPoint ","publicStreamName":"useMeToViewStream"},],"description":"Ingest point removed","status":"SUCCESS"} |

The JSON response contains the following details.

-	data – The data to parse.
	-	privateStreamName –The privateStreamName of the deleted Ingest Point.
	-	publicStreamName – The publicStreamName of the deleted Ingest Point
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

## Utility and Feature API Functions

### launchProcess

Allows the user to launch an external process on the local machine. This can be used to do transcoding when paired with applications such as LibAVConv and FFMPEG. This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value**    | **Description**                                                                                           |
|--------------------|---------------|----------------------|-----------------------------------------------------------------------------------------------------------|
| fullBinaryPath     | true          | *(null)*             | The path to the executable                                                                                |
| keepAlive          | false         | *1 (true)*           | If the process dies for any reason, the EMS will restart the external application when keepAlive is 1.    |
| arguments          | false         | *Zero-length String* | Complete list of arguments that need to be passed to the process, **delimited by ESCAPED SPACES ("\ ").** |
| groupName          | .             | .                    | .              |
| $ENV=VALUE     | false         | *Zero-length String* | Any number of environment variables that need to be set just before launching the process |

An example of the launchProcess command is:

    launchProcess fullBinaryPath=/home/ems/ffmpeg_preset.sh arguments=10fps\ Stream1\ Stream1_10fps keepAlive=1 $SAMPLE_E_VAR=MyVal

This sample command launches a script, named ffmpeg_prest.sh, which presumably contains a shell-script that will run FFMPEG with a specific set of parameters.

The arguments field passes the three values ("10fps", "Stream1", "Stream1_10fps") to the ffmpeg_preset.sh script. In this example, these parameters might tell this hypothetical script to transcode Stream1 to be only 10 frames-per-second, and then name the resultant stream "Stream1_10fps".

The final parameter is an example for setting an environment variable (SAMPLE_E_VAR set to MyVal) on the command line prior to script/binary execution.

| API           | launchProcess fullBinaryPath=/home/ems/ffmpeg_preset.sh arguments=10fps\ Stream1\ Stream1_10fps keepAlive=1 $SAMPLE_E_VAR=MyVal                                                                                     |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | { "data":{ "arguments":"", "configId":1, "fullBinaryPath":"d:\\run.bat", "groupName":"process_group_UHBqMT6C", "keepAlive":true, "operationType":6 }, "description":"Process enqueued for start", "status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	arguments – Complete list of arguments that need to be passed to the process.
	-	configID – The configuration ID for this command
	-	fullBinaryPath – Full path to the binary that needs to be launched.
	-	groupName - ??
	-	keepAlive – If keepAlive is set to 1, the server will restart the process if it exits.
	-	operationType – The type of operation
	-	$<ENV>=<VALUE> – Any number of environment variables that need to be set just before launching the process.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [launchProcess](http://pastebin.com/uDxzkUFd)

### setTimer

This function adds a timer. When triggered, it will send an event to the event logger.

This function has the following parameter:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                                                                                                                                                      |
|--------------------|---------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| value              | true          | *(null)*          | The time value for the timer. It can be either the absolute time at which the trigger will be fired (YYYY-MM-DDTHH:MM:SS or HH:MM:SS) or period of time between pulses expressed in seconds between 1 and 86399 (1 sec up to a day). |

An example of setTimer interface is:

| API           | setTimer value=10                                                                                                  |
|---------------|--------------------------------------------------------------------------------------------------------------------|
| JSON Response | { "data":{ "timerId":8, "triggerCount":0, "value":10 }, "description":"Custom timer enqueued", "status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	timerId – The ID of the timer added.
	-	triggerCount – The number of times the timer triggered since it was added.
	-	value – The time value for the timer (see parameter table above).
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [setTimer](http://pastebin.com/55FMCaJM)

### listTimers

This function lists currently active timers.

This function has no parameters.

| API           | listTimers                                                                                                              |
|---------------|-------------------------------------------------------------------------------------------------------------------------|
| JSON Response | { "data":[ { "timerId":8, "triggerCount":141, "value":10 } ], "description":"List of armed timers", "status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	timerId – The ID of the timer added.
	-	triggerCount – The number of times the timer triggered since it was added.
	-	value – The time value for the timer (see parameter table above).
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [listTimers](http://pastebin.com/ekWdxNHY)

### removeTimer

This function removes a previously armed timer.

This function has the following parameter:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                    |
|--------------------|---------------|-------------------|------------------------------------|
| id                 | true          | *(null)*          | The ID of the timer to be removed. |

An example of removeTimer interface is:

| API           | removeTimer id=8                                                                                             |
|---------------|--------------------------------------------------------------------------------------------------------------|
| JSON Response | { "data":{ "timerId":8, "triggerCount":141, "value":10 }, "description":"Timer removed", "status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	timerId – The ID of the timer added.
	-	triggerCount – The number of times the timer triggered since it was added.
	-	value – The time value for the timer (see parameter table for setTimer function).
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [removeTimer](http://pastebin.com/3ukfV1jD)

### generateLazyPullFile

Will create a VOD file which contains details of the stream to be pulled when the file is requested.

This function has the following parameters:

| **Parameter Name**    | **Mandatory**                                            | **Default Value**         | **Description**                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------|----------------------------------------------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| uri                   | true                                                     | *(null)*                  | The URI of the external stream. Can be RTMP, RTSP or unicast/multicast (d)mpegts.                                                                                                                                                                                                                                                                                                          |
| pathToFile            | true                                                     | *(null)*                  | The path where the file will be saved, with a ".vod" extension.                                                                                                                                                                                                                                                                                                                            |
| forceTcp              | false                                                    | 1 *(true)*                | If 1 and if the stream is RTSP, a TCP connection will be forced. Otherwise the transport mechanism will be negotiated (UDP or TCP).                                                                                                                                                                                                                                                        |
| tcUrl                 | false                                                    | *(zero-length string)*    | When specified, this value will be used to set the TC URL in the initial RTMP connect invoke                                                                                                                                                                                                                                                                                               |
| pageUrl               | false                                                    | *(zero-length string)*    | When specified, this value will be used to set the originating web page address in the initial RTMP connect invoke.                                                                                                                                                                                                                                                                        |
| swfUrl                | false                                                    | *(zero-length string)*    | When specified, this value will be used to set the originating swf URL in the initial RTMP connect invoke                                                                                                                                                                                                                                                                                  |
| rangeStart            | false                                                    | *-2*                      | For RTSP and RTMP connections. A value from which the playback should start expressed in seconds. There are 2 special values: -2 and -1. For more information, please read about start/len parameters here: [http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.html](http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.html) |
| rangeEnd              | false                                                    | *-1*                      | The length in seconds for the playback. -1 is a special value. For more information, please read about start/len parameters here: [http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.html](http://livedocs.adobe.com/flashmediaserver/3.0/hpdocs/help.html?content=00000185.html)                                                                           |
| ttl                   | false                                                    | operating system supplied | Sets the IP_TTL (time to live) option on the socket                                                                                                                                                                                                                                                                                                                                       |
| tos                   | false                                                    | operating system supplied | Sets the IP_TOS (Type of Service) option on the socket                                                                                                                                                                                                                                                                                                                                    |
| rtcpDetectionInterval | false                                                    | 10                        | How much time (in seconds) should the server wait for RTCP packets before declaring the RTSP stream as a RTCP-less stream                                                                                                                                                                                                                                                                  |
| emulateUserAgent      | false                                                    | *(EvoStream message)*     | When specified, this value will be used as the user agent string. It is meaningful only for RTMP.                                                                                                                                                                                                                                                                                          |
| isAudio               | true if uri is RTP, otherwise false                      | *1 (true)*                | If 1 and if the stream is RTP, it indicates that the currently pulled stream is an audio source. Otherwise the pulled source is assumed as a video source.                                                                                                                                                                                                                                 |
| audioCodecBytes       | true if uri is RTP and isAudio is true, otherwise false  | *(zero-length string)*    | The audio codec setup of this RTP stream if it is audio. Represented as hex format without '0x' or 'h'. (For example: audioCodecBytes=1190)                                                                                                                                                                                                                                                |
| spsBytes              | true if uri is RTP and isAudio is false, otherwise false | *(zero-length string)*    | The video SPS bytes of this RTP stream if it is video. It should be base 64 encoded.                                                                                                                                                                                                                                                                                                       |
| ppsBytes              | true if uri is RTP and isAudio is false, otherwise false | *(zero-length string)*    | The video PPS bytes of this RTP stream if it is video. It should be base 64 encoded.                                                                                                                                                                                                                                                                                                       |
| ssmIp                 | false                                                    | *(zero-length string)*    | The source IP from source-specific-multicast. Only usable when doing UDP based pull                                                                                                                                                                                                                                                                                                        |
| httpProxy             | false                                                    | *(zero-length string)*    | This parameter has two valid values:                                                                                                                                                                                                                                                                                                                                                       |

1.	IP:Port – This value combination specifies an RTSP HTTP Proxy from which the RTSP stream should be pulled from
2.	self – Specifying "self" as the value implies pulling **RTSP over HTTP**. | | sendRenewStream | false | *0 (false)* | If sendRenewStream is 1, the server will send RenewStream via SET_PARAMETER when a new client connects. Only valid for RTSP URIs. | | keepAlive | false | *0 (false)* | If value is 1 (true), source stream will not shutdown even after all clients have hung up. |

An example of the generateLazyPullFile interface is:

    generateLazyPullFile uri=rtsp://AddressOfStream pathToFile=/MyFileDirectory/MyFile.vod

| API           | generateLazyPullFile uri=rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 pathToFile=../media/testGenerateLazyPull                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"audioCodecBytes":"","emulateUserAgent":"EvoStream Media Server (www.evostream.com) player","forceTcp":true,"httpProxy":"","isAudio":true,"keepAlive":false,"pageUrl":"","pathToFile":"..\/media\/testGenerateLazyPull","ppsBytes":"","rangeEnd":-1,"rangeStart":-2,"rtcpDetectionInterval":10,"sendRenewStream":false,"spsBytes":"","ssmIp":"","swfUrl":"","tcUrl":"","tos":256,"ttl":256,"uri":{"document":"mp4:sintel.mp4","documentPath":"\/cfx\/st\/","documentWithFullParameters":"mp4:sintel.mp4","fullDocumentPath":"\/cfx\/st\/mp4:sintel.mp4","fullDocumentPathWithParameters":"\/cfx\/st\/mp4:sintel.mp4","fullParameters":"","fullUri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","fullUriWithAuth":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","host":"s2pchzxmtymn2k.cloudfront.net","ip":"54.239.131.224","originalUri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4","parameters":{},"password":"","port":1935,"portSpecified":false,"scheme":"rtmp","userName":""}},"description":"Stream parameters written to ..\/media\/testGenerateLazyPull.vod","status":"SUCCESS"} |

The JSON response for generateLazyPullFile contains the following details:

-	data – The data to parse.
	-	audioCodecBytes - The audio codec setup of this RTP stream if it is audio. Represented as hex format without '0x' or 'h'.
	-	emulateUserAgent – This is the string that the EMS uses to identify itself with the other server. It can be modified so that EMS identifies itself as, say, a Flash Media Server.
	-	forceTcp – Whether TCP MUST be used, or if UDP can be used
	-	httpProxy – May either be IP:Port combination or self
	-	isAudio – Indicates that the currently pulled stream is an audio source
	-	keepAlive – if true, will retain the stream in the config even if the playback stopped.
	-	pageUrl – A link to the page that originated the request (often unused)
	-	pathToFile – The local name for the stream
	-	ppsBytes – The video PPS bytes of this RTP stream if it is video
	-	rangeEnd – The length in seconds for the playback
	-	rangeStart – A value from which the playback should start. Applies only to RTSP and RTMP connections.
	-	rtcpDetectionInterval – Used for RTSP. This is the time period the EMS waits to determine if an RTCP connection is available for the RTSP/RTP stream. (RTSP is used for synchronization between audio and video).
	-	sendRenewStream – Indicates if the server will send a RenewStream when a new client connects.
	-	spsBytes – The video SPS bytes of this RTP stream if it is video.
	-	ssmIp – The source IP from source-specific multicast.
	-	swfUrl – The location of the Flash Client that is generating the stream (if any).
	-	tcUrl – An RTMP parameter that is essentially a copy of the URI.
	-	tos – Type of Service network flag.
	-	ttl – Time To Live network flag.
	-	uri – Contains key/value pairs describing the source stream's URI.
	-	document – The document name of the source stream.
	-	documentPath – The document path of the source stream.
	-	documentWithFullParameters – The document name with parameters of the source stream.
	-	fullDocumentPath - The document path of the destination stream
	-	fullDocumentPathWithParameters - The document path with parameters of the destination stream
	-	fullParameters – The parameters for the source stream's URI.
	-	fullUri – The full URI of the source stream.
	-	fullUriWithAuth – The full URI with authentication of the source stream.
	-	host – Name of the source stream's host.
	-	ip – IP address of the source stream's host.
	-	originalUri – The source stream's URI where it was generated.
	-	parameters – Parameters for the source stream's URI (if any).
	-	password – Password for authenticating the source stream (if required).
	-	port – Port used by the source stream.
	-	portSpecified – True if the port for the source stream is specified.
	-	scheme – The protocol used by the source stream.
	-	userName – The user name for authenticating the source stream (if required).
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### generateServerPlaylist

Will create a server-side playlist with the specified sources.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value**      | **Description**                                                                                                               |
|--------------------|---------------|------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| sources            | true          | *(null)*               | The stream or media file source(s) to be used as input. This is a comma-delimited list of active stream names or media files. |
| pathToFile         | true          | *(null)*               | The path to the output server playlist file.                                                                                  |
| sourceOffsets      | false         | *(zero-length) string* | The corresponding offsets for the source streams/files listed in sources. This can be a comma-delimited list.                 |
| durations          | false         | *(zero-length string)* | The corresponding durations for the source streams/files listed in sources. This can be a comma-delimited list.               |

**sourceOffsets** and **durations** specify what part of the source stream/file to play for each of the items listed and for how long. The values for **sourceOffsets** and **durations** are defined specifically as follows:

-	**sourceOffsets** specifies the starting position, in seconds, for each of the source stream/file. This parameter can also be used to indicate whether the stream is live or a media file.
	-	-2 means that the EMS will look for a live stream with the source name specified. If a live stream is not found, it will attempt to play a media file with the source name. If a media file with that name and path cannot be found the EMS will wait for a live stream to become available.
	-	-1 implies that the source is explicitly a live stream. If no live stream is found, the EMS waits indefinitely if *duration* is set to -1. If *duration* is another value the EMS will wait *duration* seconds before moving to the next item in the playlist.
	-	0 or a positive number implies that the specified source is a media file. The EMS will start playback *sourceOffset* seconds from the beginning of the file. If no file is found the playlist item is skipped.
	-	Any negative number other than -1 or -2 will be assumed to be -2
-	**durations** specifies the length of the playback of each of the sources in seconds.
	-	All positive numbers will cause the EMS to play the stream/file for *duration* seconds or until the end of the media file or live stream, whichever comes first.
	-	0 means that only a single frame of the stream/file will be played.
	-	-1 means that the EMS will play a live stream until it is no longer available or a media file until its end.
	-	-2 will play media files until their end (same as -1 behavior). For live sources, it will play the live stream until that stream is no longer available. When the source stream is lost the EMS shall move to the next item in the playlist.
	-	Any negative number other than -1 or -2 will be assumed to be -2.

An example of the generateServerPlaylist interface is:

    generateServerPlaylist sources=File1.mp4,livestream1,File2.mp4,livestream1 pathToFile=/MyFileDirectory/MyPlaylist.lst sourceOffsets=0,-1,0,-1 durations=-1,60,-1,-1

| API           | generateServerPlaylist sources=bunnyA.mp4,bunnyB.mp4 pathToFile=../media/testPlaylist sourceOffsets=0,-1 durations=-1,60                                                                                                     |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"durations":[-1,60],"pathToFile":"..\/media\/testPlaylist","sourceOffsets":[0,-1],"sources":["bunnyA.mp4","bunnyB.mp4"]},"description":"Server playlist written to ..\/media\/testPlaylist.lst","status":"SUCCESS"} |

The JSON response for generateServerPlaylist contains the following details:

-	data – The data to parse
	-	durations – An array of durations for each stream/file in the list, expressed in seconds.
	-	pathToFile – The full path and filename of the playlist file.
	-	sourceOffsets – An array of offsets for each stream/file in the list.
	-	sources – An array of streams or media files.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: generateServerPlaylist

### insertPlaylistItem

Inserts a new item into an RTMP playlist. insertPlaylistItem may be called on playlists which are actively being played by one or more clients/players.

**IMPORTANT NOTES:**

-	This function does NOT modify the actual playlist file. Instead it modifies ONLY the in-memory copy of the file.
-	The sourceOffset and duration parameters behave exactly as they do when creating Playlist Files. However, they are measured in **MILLISECONDS** as opposed to seconds.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|--------------------|---------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| playlistName       | true          | *(null)*          | The name of the \*.lst file into which the stream will be inserted                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| localStreamName    | true          | *(null)*          | The name of the live stream or file that needs to be inserted. If a file is specified, the path must be relative to any of the mediaStorage locations                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| insertPoint        | false         | *-1000*           | The absolute time in milliseconds on the playlist timeline where the insertion will occur. Any negative value will be considered as "immediate", meaning it will start playing the stream being inserted the very next frame                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| sourceOffset       | false         | *-2000*           | Specifies the starting position, in milliseconds, of the source stream. This parameter can also be used to indicate whether the stream is live or recorded.-2000 means that the EMS will look for a live stream with the localStreamName specified. If a live stream is not found, it will attempt to play a media file with the localStreamName. If a media file with that name and path cannot be found the EMS will wait for a live stream to become available.-1000 implies that the localStreamName is explicitly a live stream. If no live stream is found, the EMS waits indefinitely if *duration* is set to -1. If *duration* is another value the EMS will wait *duration* seconds before moving to the next item in the playlist.0 or a positive number implies that the specified localStreamName is a media file. The EMS will start playback sourceOffset milliseconds from the beginning of the file. If no file is found the playlist item is skipped.Any negative number other than -1000 or -2000 will be assumed to be -2000 |
| duration           | false         | *-1000*           | The duration of the playback of the stream in milliseconds.-1000 means that the EMS will play a live stream until it is no longer available or a media file until its end.0 means that only a single frame of the stream will be played.All positive numbers will cause the EMS to play the stream for duration milliseconds or until the end of the media file or live stream, whichever comes first.Any negative number passed other than -1000 will be assumed to be -1000                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

An example of insertPlaylistItem interface is:

| API           | insertPlaylistItem playlistName=testInPlaylist localStreamName=testPullStream insertPoint=-1000 sourceOffset=0 duration=0                                                               |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"duration":0,"insertPoint":-1000,"localStreamName":"TestInPlaylist","playlistName":"TestPlaylist","sourceOffset":0},"description":"Playlist item inserted","status":"SUCCESS"} |

The JSON response for generateServerPlaylist contains the following details:

-	data – The data to parse
	-	duration – An array of durations for each stream/file in the list, expressed in seconds.
	-	insertPoint - The absolute time in milliseconds on the playlist timeline where the insertion will occur
	-	localStreamName – The name of the live stream or file that needs to be inserted
	-	playlistName - The name of the \*.lst file into which the stream will be inserted
	-	sourceOffsets – An array of offsets for each stream/file in the list.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### uploadMedia

Creates an acceptor which receives an HTTP POST binary upload. The acceptor will be opened on a specified port and the uploaded media file will be written on a specified directory. The acceptor then waits for an HTTP PUT from a client with the media file as payload. The media file is then written on the specified location in the server.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                        |
|--------------------|---------------|-------------------|--------------------------------------------------------|
| port               | true          | *(null)*          | The port value to bind on.                             |
| targetFolder       | true          | *(null)*          | The folder where the binary upload will be serialized. |

The sending client must conform to the following:

-	It must send the data by way of HTTP POST.
-	The POST request must be in http/1.1 format.
-	A StreamName must be provided in the POST line. This will then be the filename of the media file (mp4) when written. (e.g., *POST /mystreamname HTTP/1.1\r\n*\)
-	Content-type must be set to *video/mp4* or *application/octet-stream*.
-	Content-length must be used. This function is intended for uploading VOD MP4 so the EMS will expect that the size of the file is already known.

An example of the uploadMedia interface is:

    uploadMedia port=3333 targetFolder=/MyMediaFolder

| API           | uploadMedia port=3333 targetFolder=../media                                                                                              |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"ip":"0.0.0.0","port":3333,"targetFolder":"..\/media"},"description":"Media upload acceptor configuration.","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	ip – The IP referring to the EMS, normally 0.0.0.0.
	-	port – The specified port number where the acceptor will wait for HTTP POSTs.
	-	targetFolder – The specified folder where the media file will be written.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: uploadMedia

### getMetadata

Returns the most recently received string currently cached by the Metadata Manager. The call is stateless so multiple clients may each poll for metadata with no impact on each other. This may result in getting the same string multiple times if no new string has arrived.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                            |
|--------------------|---------------|-------------------|------------------------------------------------------------------------------------------------------------|
| localStreamName    | false         | *(null)*          | Name of the incoming stream from which the associated metadata will be returned. Default most recent.      |
| streamId           | false         | *0*               | Identifies the particular stream from which the associated metadata will be returned. Default most recent. |
| noWrap             | false         | *0 (false)*       | If true, the returned string will not have the CLI JSON wrapping.                                          |

An example of the getMetadata interface is:

    getMetadata localStreamName=test noWrap=1

| API           | getMetadata localStreamName=bunny                                                                                                                                                                                   | getMetadata localStreamName=bunny noWrap=1                                                                                      |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":"{\"EMS\":{\"type\":\"json\",\"timestamp\":46125},\"data\":{\"lat\":\"32.809668\",\"lon\":\"-117.255317\",\"alt\":\"44.7\",\"speed\":\"20\",\"dir\":\"300\"}}","description":"Metadata","status":"SUCCESS"} | {"EMS":{"type":"json","timestamp":12042},"data":{"lat":"32.809668","lon":"-117.2 55317","alt":"44.7","speed":"50","dir":"300"}} |

The JSON response contains the following details:

-	data – The data to parse.
	-	type
	-	timestamp
	-	lat
	-	lon
	-	alt
	-	speed
	-	dir
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### pushMetadata

Opens an outboundVmf TCP stream over which each modified JSON metadata object is sent.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                   |
|--------------------|---------------|-------------------|-------------------------------------------------------------------|
| localStreamName    | true          | *(null)*          | Name of the stream to which the associated metadata will be sent. |
| type               | false         | *vmf*             | Type of push stream.                                              |
| ip                 | false         | *127.0.0.1*       | IP address to push to.                                            |
| port               | false         | *8110*            | Port to push to.                                                  |

An example of the pushMetadata interface is:

    pushMetadata localStreamName=test ip=127.0.0.1 port=8110

| API           | pushMetadata localStreamName=test ip=127.0.0.1 port=8110                                                                                                                                                                                                          |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"applicationName":"evostreamms","ip":"127.0.0.1","keepAlive":true,"localStreamName":"test","name":"evostreamms","port":8110,"protocol":"outboundVmf","streamName":"test","type":"vmf"},"description":"Launched Metadata Push Stream","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	applicationName – The EMS (evostreamms).
	-	ip – The IP address to push to.
	-	keepAlive – Indicates if it will be enabled after restart.
	-	localStreamName – Name of the stream to which the associated metadata will be sent.
	-	name – Name of the application (evostreamms).
	-	port – The port to push to.
	-	protocol – The type of stream.
	-	streamName – Name of the stream to which the associated metadata will be sent.
	-	type – The type of stream.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### shutdownMetadata

Stops a metadata pseudo-stream. This command shuts down all multiple pull streams that were issued for a given localStreamName.

This function has the following parameter:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                     |
|--------------------|---------------|-------------------|-----------------------------------------------------|
| localStreamName    | true          | *(null)*          | Metadata associated with this incoming stream name. |

An example of the shutdownMetadata interface is:

    shutdownMetadata localStreamName=test

| API           | shutdownMetadata localStreamName=test                  |
|---------------|--------------------------------------------------------|
| JSON Response | {"data":{"localStreamName":"test","streamName":"test","type":"vmf" },"description":"Shutdown Metadata Push Stream", "status":"SUCCESS" } |

The JSON response contains the following details:

-	data – The data to parse.
	-	localStreamName – Name of the stream to which the associated metadata will be sent.
	-	streamName – Name of the stream to which the associated metadata will be sent.
	-	type – The type of stream.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### listStorage

Lists currently available media storage locations.

This function has no parameters.

An example of listStorage interface is:

| API           | listStorage                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":[{"clientSideBuffer":15,"description":"Default media storage","enableStats":false,"externalSeekGenerator":false,"keyframeSeek":true,"maxPlaylistFileSize":4096,"mediaFolder":"\/home\/qatest\/Desktop\/evostreamms-1.7.0.4242-x86_64-Ubuntu_14.04\/media\/","metaFolder":"\/home\/qatest\/Desktop\/evostreamms-1.7.0.4242-x86_64-Ubuntu_14.04\/media\/","name":"0x00000001","seekGranularity":1000}],"description":"Available storages","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	clientSideBuffer – How much data should be maintained on the client side when a file is played from this storage.
	-	description – Description given to this storage. Used to better identify the storage.
	-	enableStats – If true, \*.stats files are going to be generated once the media files are used.
	-	externalSeekGenerator – If true, \*.seek and \*.meta files are going to be generated by another external tool.
	-	keyframeSeek – If true, the seek/meta files are going to be generated having only keyframe seek points.
	-	mediaFolder – The path to the media folder.
	-	metaFolder – Path to the folder which is going to contain all the seek/meta files. If missing, the seek/meta files are going to be generated inside the media folder.
	-	name – Name given to this storage. Used to better identify the storage.
	-	seekGranularity – Sets the granularity for the seek files.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [listStorage](http://pastebin.com/PTukwpRE)

### addStorage

Adds a new storage location.

This function has the following parameters:

| Parameter Name        | Mandatory | Default Value | Description                                                                                                                                              |
|-----------------------|-----------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| mediaFolder           | true      | *(null)*      | The path to the media folder                                                                                                                             |
| description           | false     | *(null)*      | Description given to this storage. Used to better identify the storage                                                                                   |
| clientSideBuffer      | false     | *(null)*      | How much data should be maintained on the client side when a file is played from this storage                                                            |
| enableStats           | false     | false         | If true, \*.stats files are going to be generated once the media files are used                                                                          |
| externalSeekGenerator | false     | false         | If true, \*.seek and \*.meta files are going to be generated by another external tool                                                                    |
| keyframeSeek          | false     | false         | If true, the seek/meta files are going to be generated having only keyframe seek points                                                                  |
| metaFolder            | false     | *(null)*      | Path to the folder which is going to contain all the seek\/meta files. If missing, the seek/meta files are going to be generated inside the media folder |
| name                  | false     | *(null)*      | Name given to this storage. Used to better identify the storage                                                                                          |
| seekGranularity       | false     | 1.0000        | Sets the granularity for the seek files                                                                                                                  |

An example of listStorage interface is:

| API           | addStorage mediaFolder=C:\EvoStream\media1 description=TestStorage enableStats=1 externalSeekGenerator=1 keyframeSeek=1 metaFolder=C:\EvoStream\media1 name=TestNameStorage seekGranularity=300000                                                                                                                                              |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"clientSideBuffer":15,"description":"TestStorage","enableStats":true,"externalSeekGenerator":true,"keyframeSeek":true,"maxPlaylistFileSize":4096,"mediaFolder":"C:\\EvoStream\\media1\\","metaFolder":"C:\\EvoStream\\media1\\","name":"TestNameStorage","seek Granularity":300000},"description":"Storage created","status":"SUCCESS" |

The JSON response contains the following details:

-	data – The data to parse.
	-	clientSideBuffer – How much data should be maintained on the client side when a file is played from this storage.
	-	description – Description given to this storage. Used to better identify the storage.
	-	enableStats – If true, \*.stats files are going to be generated once the media files are used.
	-	externalSeekGenerator – If true, \*.seek and \*.meta files are going to be generated by another external tool.
	-	keyframeSeek – If true, the seek/meta files are going to be generated having only keyframe seek points.
	-	maxPlaylistFileSize - ??
	-	mediaFolder – The path to the media folder.
	-	metaFolder – Path to the folder which is going to contain all the seek/meta files. If missing, the seek/meta files are going to be generated inside the media folder.
	-	name – Name given to this storage. Used to better identify the storage.
	-	seekGranularity – Sets the granularity for the seek files.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [addStorage](http://pastebin.com/tcyQBzzW)

### removeStorage

This function removes a storage location.

This function has the following parameter:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**              |
|--------------------|---------------|-------------------|------------------------------|
| mediaFolder        | true          | *(null)*          | The path to the media folder |

An example of removeStorage interface is:

| API           | removeStorage mediaFolder=C:\EvoStream\media1                                                                                                                                                                                                                                                                                                   |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"clientSideBuffer":15,"description":"TestStorage","enableStats":true,"externalSeekGenerator":true,"keyframeSeek":true,"maxPlaylistFileSize":4096,"mediaFolder":"C:\\EvoStream\\media1\\","metaFolder":"C:\\EvoStream\\media1\\","name":"TestNameStorage","seek Granularity":300000},"description":"Storage removed","status":"SUCCESS" |

The JSON response contains the following details:

-	data – The data to parse.
	-	clientSideBuffer – How much data should be maintained on the client side when a file is played from this storage.
	-	description – Description given to this storage. Used to better identify the storage.
	-	enableStats – If true, \*.stats files are going to be generated once the media files are used.
	-	externalSeekGenerator – If true, \*.seek and \*.meta files are going to be generated by another external tool.
	-	keyframeSeek – If true, the seek/meta files are going to be generated having only keyframe seek points.
	-	maxPlaylistFileSize - ??
	-	mediaFolder – The path to the media folder.
	-	metaFolder – Path to the folder which is going to contain all the seek/meta files. If missing, the seek/meta files are going to be generated inside the media folder.
	-	name – Name given to this storage. Used to better identify the storage.
	-	seekGranularity – Sets the granularity for the seek files.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [removeStorage](http://pastebin.com/Ua7dCpQC)

### setAuthentication

Will enable/disable RTMP authentication. This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                          |
|--------------------|---------------|-------------------|------------------------------------------|
| enabled            | true          | *(null)*          | 1 to enable, 0 to disable authentication |

An example of the setAuthentication interface is:

    setAuthentication enabled=1

This enables authentication.

| API           | setAuthentication enabled=1                                                              |
|---------------|------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"enabled":true},"description":"Authentication mode updated","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	enabled – `true` if authentication is enabled, `false` if not.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [setAuthentication](http://pastebin.com/jEjG6Rrj)

### setLogLevel

Change the log level for all log appenders. Default value in the system is set in the config.lua file, which is usually set to 6.

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                           |
|--------------------|---------------|-------------------|-------------------------------------------------------------------------------------------|
| level              | true          | *(null)*          | A value between -1 and 6. 0 – Fatal1 – Error2 – Warning3 – Info4– Debug5 – Fine6 – Finest |

An example of the setLogLevel interface is:

    setLogLevel level=1

This sets the log level to 1. It means it will only output the error logs.

| API           | setLogLevel level=1                                               |
|---------------|-------------------------------------------------------------------|
| JSON Response | {"data":null,"description":"Log level is set","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – Nothing to parse for this command.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [setLogLevel](http://pastebin.com/KSPzW6ZS)

### version

Returns the versions for framework and this application

This function has no parameters.

| API           | version                                                                                                                                             |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"banner":"EvoStream Media Server (www.evostream.com) version 1.7.0 build 4242 with hash: 86bdcde75942b25390a15a6b1de521e913182bcf - PacMan |

The JSON response contains the following details:

-	data – Contains an integer representing the version.
	-	banner – The EMS banner
	-	branchName – The branch name where the package is created
	-	buildDate – The build date of the released package
	-	buildNumber – The build number of the released package
	-	codeName – The code name of the released EMS version
	-	hash – The hash of the released package
	-	releaseNumber – The version of the released package
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [version](http://pastebin.com/4cf6kgag)

### quit

This function quits the ASCII Command Line Interface (CLI)

This function has no parameters.

| API           | quit                                                  |
|---------------|-------------------------------------------------------|
| JSON Response | {"data":null,"description":"Bye!","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – Nothing to parse for this command.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [quit](http://pastebin.com/DJFVQzvG)

### help

This function prints out descriptions of the API in JSON format.

This function has no parameters.

| API           | help                                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":[{"command":"help","deprecated":false,"description":"prints this help","parameters":[]},{"command":"*API*","deprecated":*isdeprecated*,"description":"*API description*","parameters":\[*list of API parameters*]{"defaultValue":*parameter default value*,"description":"*parameter description"*,"mandatory":*ismandatoryparameter*,"name":"*parameter name*"},},],"description":"Available commands","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.

	-	command – The name of a valid command.
	-	deprecated – Is `true` if the command is deprecated, `false` if not.
	-	description – Describes the use of the command.
	-	parameters – Parameter settings for the command.

		-	defaultValue – The default value if the parameter is omitted.
		-	description – Describes the use of the parameter.
		-	mandatory – Is `true` if the parameter is mandatory, `false` if not.
		-	name – The name of a parameter for the command.

-	description – Describes the result of parsing/executing the command.

-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [help](http://pastebin.com/8nnkLPnk)

### shutdownServer

This function ends the server process, completely shutting down the EMS. This function must be called twice, once with a blank parameter, allowing you to obtain the shutdown key, and then a second time with the key, which actually causes the EMS to terminate.

| Parameter Name | Mandatory | Default Value | Description                                                                                                                                                 |
|----------------|-----------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Key            | false     | *(null)*      | The key to shutdown the server. shutdownServer must be called without the key to obtain the key and once again with the returned key to shutdown the server |

An example of the shutdownServer interface is:

    shutdownServer

| API           | shutdownServer                                                                                                         |
|---------------|------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"key":"GCY6IXniMf6NDOxY"},"description":"Call shutdownserver again with the provided key","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse
	-	key – The key that needs to be used in a subsequent call to shutdownServer.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

To shutdown the Server enter the same command with the key parameter given:

    shutdownServer key=GCY6IXniMf6NDOxY

## Connections

The Connections API functions allow the user to manipulate and query the actual network connections between the EMS and other systems or applications. The most common connections will occur between the EMS and a media player. However, there are a variety of other situations where connections can occur, such as (but not limited to) connections between two EMS instances, or an EMS and another server.

### listConnections

Returns details about every active stream-related connection. This does not include other connections used for EMS operations (telnet, license manager, interface, etc.).

| **Parameter Name**         | **Mandatory** | **Default Value** | **Description**                                                                                                      |
|----------------------------|---------------|-------------------|----------------------------------------------------------------------------------------------------------------------|
| excludeNonNetworkProtocols | false         | 1 *(true)*        | If 1 (true), all non-networking protocols will be excluded. If 0 (false), non-networking protocols will be included. |

An example of the listConnections interface is:

    listConnections excludeNonNetworkProtocols=0

This lists connections including non-networking protocols.

| API           | listConnections excludeNonNetworkProtocols=0                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":[{"carrier":{"farIP":"54.239.131.147","farPort":1935,"id":86,"nearIP":"192.168.2.107","nearPort":45399,"rx":743036,"tx":3621,"type":"IOHT_TCP_CARRIER"},"pullSettings":{},"stack":[{"applicationId":0,"creationTimestamp":1448259304659.3040,"id":97,"isEnqueueForDelete":false,"queryTimestamp":1448259308424.6599,"type":"TCP"},…"txInvokes":5,"type":"OR"]}],"description":"Available connections","status":"SUCCESS"} |

The JSON response contains the following details about each connection:

-	data – The data to parse.
	-	carrier – Details about the connection itself
	-	farIP – The IP address of the distant party.
	-	farPort – The port used by the distant party.
	-	Id - ID of the service
	-	nearIP – The IP address used by the local computer.
	-	nearPort – The port used by the local computer.
	-	rx – Total bytes received on this connection.
	-	tx – Total bytes transferred on this connection.
	-	type – The connection type (TCP, UDP) .
	-	pullSettings/pushSettings/hlsSettings/hdsSettings/mssSettings/dashSettings/recordSettings – A copy of the parameters used in the stream command that caused this connection to be made.
	-	Other fields present depend on the stream type (see **pushStream** , **pullStream** , **createHLSStream** , **createHDSStream, createMSSStream, createDASHStream, record** commands).
	-	stack – details about what internal resources are using the connection..
	-	applicationID – the ID of the internal application using the connection.
	-	creationTimestamp – The time (in UNIX seconds) when the application started using the connection.
	-	id – The unique ID for this stack relation.
	-	isEnqueueForDelete – Internal flag used for cleanup.
	-	queryTimestamp – The time (in UNIX seconds) when this data was populated.
	-	rxInvokes – Number of received RTMP function invokes.
	-	streams – Details about the streams that are using the connection (see fields in ListStreams).
	-	txInvokes – Number of sent RTMP function invokes.
	-	type – A descriptor for how the application is using the connection.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### listConnectionsIds

Returns a list containing the IDs of every active stream-related connection. This does not include other connections used for EMS operations (telnet, license manager, interface, etc.).

This interface has no parameters.

| API           | listConnectionsIds                                                                    |
|---------------|---------------------------------------------------------------------------------------|
| JSON Response | { "data":[144,186,201], "description":"Available connection IDs", "status":"SUCCESS"} |
|               |                                                                                       |

The JSON response contains the following details:

-	data – An array of connection IDs.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### getConnectionInfo

Returns a detailed set of information about a connection

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                |
|--------------------|---------------|-------------------|--------------------------------------------------------------------------------|
| id                 | true          | *(null)*          | The uniqueId of the connection. Usually a value returned by listConnectionsIds |

An example of the getConnectionInfo interface is:

    getConnectionInfo id=144

This gets connection info about a connection with id of 144.

| API           | getConnectionInfo id=144                                                                                                                                                                                                                                     |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | { "data":{ "carrier":null, "stack":[ { "applicationId":1, "creationTimestamp":1338633696196.6460, "id":144, "isEnqueueForDelete":false, "queryTimestamp":1338658491380.7349, "type":"TMR" } ] }, "description":"Connection information", "status":"SUCCESS"} |

The JSON response contains the following details about one connection:

-	data – The data to parse. See the **listConnections** command for a description of the fields
	-	carrier - Details about the connection itself
	-	stack - details about what internal resources are using the connection
	-	applicationId - the ID of the internal application using the connection
	-	creationTimeStamp - The time (in UNIX seconds) when the application started using the connection
	-	Id - The unique ID for this stack relation
	-	isEnqueForDelete - Internal flag used for cleanup
	-	queryTimeStamp - The time (in UNIX seconds) when this data was populated
	-	type - A descriptor for how the application is using the connection
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

### clientsConnected

Returns all the clients currently utilizing the EMS.

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                                                                   |
|--------------------|---------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| localStreamName    | false         | *(null)*          | The name of the particular stream. If this parameter is specified, the command will return the number of clients connected which use that stream. |

An example of the clientsConnected interface is:

    clientsConnected localStreamName=MyStream

| API           | clientsConnected                                                                                      | clientsConnected localStreamName=MyStream                                                                                                             |
|---------------|-------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"outboundCount":3},"description":"EMS outbound client connections count","status":"SUCCESS"} | {"data":{"outboundCount":0},"description":"EMS outbound client connections count for the corresponding localstreamname: MyStream","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	outboundCount – The number of client connections.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: clientsConnected

### httpClientsConnected

Returns all the clients which are currently utilizing the EWS.

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                                                                                               |
|--------------------|---------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| groupName          | false         | *(null)*          | The name of the particular group. If this parameter is specified, the command will return the number of clients connected which are playing streams falling under that group. |

An example of the httpClientsConnected interface is:

| API           | httpClientsConnected                                                                                                                            | httpClientsConnected groupName=MyGroupStream                                                                                                                                   |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"groupName":"","httpStreamingSessionsCount":2},"description":"Number of clients connected to Evostream Web Server","status":"SUCCESS"} | {"data":{"groupName":"","httpStreamingSessionsCount":2},"description":"Number of clients connected to Evostream Web Server under groupname: MyGroupStream","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse
	-	groupName – The group name to which the clients are connected to
	-	httpStreamingSessionsCount – The number of client connections
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not

### listHttpStreamingSessions

This command lists all currently active HTTP streaming sessions.

The function has no parameter.

| API           | listHttpStreamingSessions                                                                                                                                                                                                                                |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | { "data": [ { "clientIP": "127.0.0.1", "elapsedTime": 33, "sessionId": 1, "startTime": "2014-12-17T18-31-13", "targetFolder": "C:\\xampp\\htdocs\\mss_group\\mystream" } ], "description":"Currently open HTTP streaming sessions", "status":"SUCCESS"} |

The JSON response contains the following details:

-	data – Provides the following information for each group name alias:
	-	clientIP – The IP address of the connected client.
	-	sessionId – An internal ID for the session.
	-	startTime – The timestamp when the session started.
	-	elapsedTime – The number of seconds since the session started.
	-	targetFolder – The current folder used as the source for HTTP streaming.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: httpClientsConnected

### getExtendedConnectionCounters

Returns a detailed description of the network descriptors counters. This includes historical high-water-marks for different connection types and cumulative totals.

This interface has no parameters.

| API           | getExtendedConnectionCounters                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"origin":{"grandTotal":{"current":22,"inBytes":258381745,"inSpeed":0.0000,"max":24,"outBytes":350990,"outSpeed":0.0000,"total":304},"managedNonTcpUdp":{*--removed content for clarity*},"managedTcp":{*--removed content for clarity*},"managedTcpAcceptors":{*--removed content for clarity*},"managedTcpConnectors":{*--removed content for clarity*},"managedUdp":{*--removed content for clarity*},"rawUdp":{"current":0,"inBytes":0,"max":0,"outBytes":0,"total":0}},"total":22},"description":"Connection counters","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	origin
	-	grandTotal – Stats for all connections.
	-	managedNonTcpUdp – Stats for non-TCP/UDP connections.
	-	managedTcp – Stats for TCP connections.
	-	managedTcpAcceptors – Stats for TCP acceptors.
	-	managedTcpConnectors – Stats for TCP connectors.
	-	managedUdp – Stats for UDP connections.
	-	rawUdp – Stats for raw UDP.
	-	Total – Summary.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [getExtendedConnectionCounters](http://pastebin.com/nDJa6Bh1)

### resetMaxFdCounters

Reset the maximum, or high-water-mark, from the Connection Counters

This interface has no parameters

| API           | resetMaxFdCounters                                                          |
|---------------|-----------------------------------------------------------------------------|
| JSON Response | {"data":*null*,"description":"Max counters are cleared","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – Nothing to parse for this command.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [resetMaxFdCounters](http://pastebin.com/U9jsemHZ)

### resetTotalFdCounters

Reset the cumulative totals from the Connection Counters

This interface has no parameters

| API           | resetTotalFdCounters                                                          |
|---------------|-------------------------------------------------------------------------------|
| JSON Response | {"data":*null*,"description":"Total counters are cleared","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – Nothing to parse for this command
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not

A typical response in parsed JSON format is shown here: [resetTotalFdCounters](http://pastebin.com/mBNnZ319)

### getConnectionsCount

Returns the number of active connections. This includes connections necessary for EMS operations (telnet, license manager, interface, etc.) and all connections opened by streams (RTSP-UDP-RTP ports).

This interface has no parameters.

| API           | getConnectionsCount                                                              |
|---------------|----------------------------------------------------------------------------------|
| JSON Response | {"data":{"count":3},"description":"Active connections count","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	count – The number of active connections.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [getConnectionsCount](http://pastebin.com/WWTpVtVA)

### getConnectionsCountLimit

Returns the limit of concurrent connections. This is the maximum number of connections an EMS instance will allow at one time.

This interface has no parameters.

| API           | getConnectionsCountLimit                                                               |
|---------------|----------------------------------------------------------------------------------------|
| JSON Response | {"data":{"cuurent":3"limit":0},"description":"Connection counters","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	current – The current number of concurrent connections.
	-	limit – The maximum number of concurrent connections.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [getConnectionsCountLimit](http://pastebin.com/jN5Z755K)

### setConnectionsCountLimit

This interface sets a limit on the number of concurrent connections the EMS will allow.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                                                           |
|--------------------|---------------|-------------------|-----------------------------------------------------------------------------------------------------------|
| count              | true          | *(null)*          | The maximum number of connections allowed on this instance at one time. CLI connections are not affected. |

An example of the setConnectionsCountLimit interface is:

    setConnectionsCountLimit count=500

This sets the connection limit to 500.

| API           | setConnectionsCountLimit count=500                                                       |
|---------------|------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"cuurent":3"limit":500},"description":"Connection counters","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to be parsed
	-	current – The current bandwidths
	-	max – The maximum bandwidths
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not

A typical response in parsed JSON format is shown here: [setConnectionsCountLimit](http://pastebin.com/CBRnpGqi)

### getBandwidth

Returns bandwidth information: current values and limits.

This function has no parameters.

| API           | getBandwidth                                                                                                                                 |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"current":{"in":111880.0459,"out":147.8026},"max":{"in":0.0000,"out":0.0000}},"description":"Bandwidth in B\/s","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to be parsed
	-	current – The current bandwidths
	-	in – The inbound bandwidth
	-	out – The outbound bandwidth
	-	max – The maximum bandwidths
	-	in – The inbound limit
	-	out – The outbound limit
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not

A typical response in parsed JSON format is shown here: [getBandwidth](http://pastebin.com/XYWDTUnq)

### SetBandwidthLimit

Enforces a limit on input and output bandwidth.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                                                               |
|--------------------|---------------|-------------------|-------------------------------------------------------------------------------|
| in                 | true          | *(null)*          | Maximum input bandwidth. 0 means disabled. CLI connections are not affected.  |
| out                | true          | *(null)*          | Maximum output bandwidth. 0 means disabled. CLI connections are not affected. |

An example of the setBandwidthLimit interface is:

    setBandwidthLimit in=400000 out=300000

This sets the inbound bandwidth limit to 400,000, and the outbound bandwidth limit to 300,000 bytes/sec.

| API           | setBandwidthLimit in=400000 out=300000                                                                                                                 |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"current":{"in":111880.0459,"out":147.8026},"max":{"in":400000.0000,"out":300000.0000}},"description":"Bandwidth in B\/s","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to be parsed
	-	current – The current bandwidths
	-	in – The inbound bandwidth
	-	out – The outbound bandwidth
	-	max – The maximum bandwidths
	-	in – The inbound limit
	-	out – The outbound limit
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not

A typical response in parsed JSON format is shown here: [setBandwidthLimit](http://pastebin.com/2sREJFL9)

## Services

The services API functions allow the user to manipulate the Networking Services that are added to an EMS application. These services are also called acceptors.

### listServices

Returns the list of available services.

This interface has no parameters.

| API           | listServices                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":[{"acceptedConnectionsCount":1,"appId":1,"appName":"evostreamms","droppedConnectionsCount":0,"enabled":true,"id":1,"ip":"127.0.0.1","port":1112,"protocol":"inboundJsonCli","sslCert":"","sslKey":"","useLengthPadding":true},*--content removed for clarity*\{*--content removed for clarity*"protocol":"inboundLiveFlv","sslCert":"","sslKey":"","waitForMetadata":true},*--content removed for clarity*],"description":"Available services","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – Provides the following information for each protocol
	-	acceptedConnectionsCount – The number of active connections using the service
	-	appId – The ID of the application linked to the service
	-	appName – The name of the application linked to the service
	-	droppedConnectionsCount – The number of dropped connections
	-	enabled - `true` if the service is enabled, `false` if not
	-	id = ID of the service
	-	ip = The IP address bound to the service
	-	port – The port bound to the service
	-	protocol – The protocol bound to the service
	-	sslCert – The SSL certificate
	-	sslKey – The SSL certificate key
	-	useLengthPadding – `true` if padding is enabled, `false` if not (for some protocols only)
	-	waitForMetadata – `true` if metadata is required, `false` if not (for some protocols only).
-	description – Describes the result of parsing/executing the command
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not

A typical response in parsed JSON format is shown here:  [listServices](http://pastebin.com/QT34exb8)

### createService

Creates a new service.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                     |
|--------------------|---------------|-------------------|-------------------------------------|
| ip                 | true          | *(null)*          | The IP address to bind on.          |
| port               | true          | *(null)*          | The port to bind on.                |
| protocol           | true          | *(null)*          | The protocol stack name to bind on. |
| sslCert            | false         | *(null)*          | The SSL certificate to be used.     |
| sslKey             | false         | *(null)*          | The SSL certificate key to be used. |

An example of the setConnectionsLimit interface is:

    createService ip=0.0.0.0 port=9556 protocol=inboundRtmp

This creates an acceptor for every hosted IP to accept inbound RTMP requests on port 9556.

The JSON response contains the following details:

-	data – The data to parse.
	-	acceptedConnectionsCount – The number of active connections using the service.
	-	appId – The ID of the application using the service.
	-	appName – The name of the application using the service.
	-	droppedConnectionsCount – The number of dropped connections.
	-	enabled - `true` if the service is enabled, `false` if not.
	-	id = ID of the service.
	-	ip = The IP address bound to the service.
	-	port – The port bound to the service.
	-	protocol – The protocol bound to the service.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [createService](http://pastebin.com/iLexRpxV)

### enableService

Enable or disable a service.

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**                    |
|--------------------|---------------|-------------------|------------------------------------|
| id                 | true          | *(null)*          | The id of the service.             |
| enable             | true          | *(null)*          | 1 to enable, 0 to disable service. |

An example of the enableService interface is:

    enableService id=5 enable=0

This *disables* the service with an id of 5.

| API           | enableService id=5 enable=0                                                                                                                                                                                                                                                                          |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | { "data":{ "acceptedConnectionsCount":0, "appId":1, "appName":"evostreamms", "droppedConnectionsCount":0, "enabled":true, "id":5, "ip":"0.0.0.0", "port":6666, "protocol":"inboundLiveFlv", "sslCert":"", "sslKey":"", "waitForMetadata":true }, "description":"Status changed", "status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	acceptedConnectionsCount – Number of active connections.
	-	appId – ID of application using the service.
	-	appName – Application using the service.
	-	droppedConnectionsCount – Number of dropped connections.
	-	enabled - `true` if the service is enabled, `false` if not.
	-	id – ID of the service.
	-	ip – IP address used by the service.
	-	port – Port used by the service.
	-	protocol – Protocol used by the service.
	-	sslCert – The SSL certificate
	-	sslKey – The SSL certificate key
	-	waitForMedia
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [enableService](http://pastebin.com/Bxft8iMp)

### shutdownService

Terminates a service

This function has the following parameters:

| **Parameter Name** | **Mandatory** | **Default Value** | **Description**       |
|--------------------|---------------|-------------------|-----------------------|
| id                 | true          | *(null)*          | The id of the service |

An example of the shutdownService interface is:

    shutdownService id=5

This shuts down the service with an id of 5.

| API           | shutdownService id=5                                                                                                                                                                                                                                                              |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JSON Response | {"data":{"acceptedConnectionsCount":0,"appId":1,"appName":"evostreamms","clustering":true,"droppedConnectionsCount":0,"enabled":true,"id":5,"ip":"127.0.0.1","port":1936,"protocol":"inboundRtmp","sslCert":"","sslKey":""},"description":"Service 5 removed","status":"SUCCESS"} |

The JSON response contains the following details:

-	data – The data to parse.
	-	acceptedConnectionsCount – Number of active connections.
	-	appId – ID of application using the service.
	-	appName – Application using the service.
	-	droppedConnectionsCount – Number of dropped connections.
	-	enabled - `true` if the service is enabled, `false` if not.
	-	id – ID of the service.
	-	ip – IP address used by the service.
	-	port – Port used by the service.
	-	protocol – Protocol used by the service.
	-	sslCert – SSL certificate.
	-	sslKey – SSL certificate key.
-	description – Describes the result of parsing/executing the command.
-	status – `SUCCESS` if the command was parsed and executed successfully, `FAIL` if not.

A typical response in parsed JSON format is shown here: [shutdownService](http://pastebin.com/GrhXecsG)

# EMS Event Notification System

The Events created by the EMS are as follows:

| **Stream Events**          |                                                                                        |
|----------------------------|----------------------------------------------------------------------------------------|
| **inStreamCreated**        | A new inbound stream has been created                                                  |
| **outStreamCreated**       | A new outbound stream has been created                                                 |
| **streamCreated**          | A new neutral (neither in nor out) stream has been created                             |
| **inStreamClosed**         | An inbound stream has been closed                                                      |
| **outStreamClosed**        | An outbound stream has been closed                                                     |
| **streamClosed**           | A neutral stream has been closed                                                       |
| **inStreamCodecsUpdated**  | The audio and/or video codecs for this inbound stream have been identified or changed  |
| **outStreamCodecsUpdated** | The audio and/or video codecs for this outbound stream have been identified or changed |
| **streamCodecsUpdated**    | The audio and/or video codecs for this neutral stream have been identified or changed  |
| **NoAudio**                | The audio for the stream has stopped                                                   |
| **NoVideo**                | The video on the stream has stopped                                                    |

| **Adaptive Streaming/File-based Streaming Events** |                                                                 |
|----------------------------------------------------|-----------------------------------------------------------------|
| **hlsChildPlaylistUpdated**                        | Stream specific HLS playlist has been modified                  |
| **hlsMasterPlaylistUpdated**                       | HLS group playlist has been modified                            |
| **hlsChunkCreated**                                | A new HLS segment was opened on disk                            |
| **hlsChunkClosed**                                 | A new HLS segment has been completed and is ready on disk       |
| **hlsChunkError**                                  | A failure occurred when writing to an HLS segment file          |
| **hdsChildPlaylistUpdated**                        | Stream specific HDS manifest has been modified                  |
| **hdsMasterPlaylistUpdated**                       | HDS group manifest has been modified                            |
| **hdsChunkCreated**                                | A new HDS segment file has been opened                          |
| **hdsChunkClosed**                                 | A new HDS segment has been completed and is ready on disk       |
| **hdsChunkError**                                  | A failure occurred when writing to an HDS segment/fragment file |
| **mssChunkCreated**                                | A new MSS fragment file has been opened                         |
| **mssChunkClosed**                                 | A new MSS fragment has been completed and is ready on disk      |
| **mssChunkError**                                  | A failure occurred when writing to an MSS fragment file         |
| **mssPlaylistUpdated**                             | MSS manifest has been modified                                  |
| **dashChunkCreated**                               | A new DASH fragment file has been opened                        |
| **dashChunkClosed**                                | A new DASH fragment has been completed and is ready on disk     |
| **dashChunkError**                                 | A failure occurred when writing to an DASH fragment file        |
| **dashPlaylistUpdated**                            | DASH manifest has been modified                                 |
| **recordChunkCreated**                             | A new MP4 fragment file has been opened                         |
| **recordChunkClosed**                              | A new MP4 fragment has been completed and is ready on disk      |
| **recordChunkError**                               | A failure occurred when writing to an MP4 file                  |

| **Web Server Events**       |                                        |
|-----------------------------|----------------------------------------|
| **streamingSessionStarted** | A streaming session has been started   |
| **streamingSessionEnded**   | A streaming session has been completed |
| **fileDownloaded**          | A file download has been completed     |

| **API Based Events** |                                                                                             |
|----------------------|---------------------------------------------------------------------------------------------|
| **cliRequest**       | The EMS has received a Runtime API command                                                  |
| **cliResponse**      | The response generated by the EMS for the last Runtime API command                          |
| **processStarted**   | A process has been started at the request of the launchProcess API command                  |
| **processStopped**   | A process started via the launchProcess API command has been stopped                        |
| **timerCreated**     | A new timer has been created via the setTimer API command                                   |
| **timerTriggered**   | The requested timer event                                                                   |
| **timerClosed**      | Indicates the timer is no longer valid and will not create any futher timerTriggered events |

| **Connection Based Events**     |                                                                                                                 |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **protocolRegisteredToApp**     | A connection has been fully established                                                                         |
| **protocolUnregisteredFromApp** | A connection has been disconnected                                                                              |
| **carrierCreated**              | Some IO handler, such as a TCP socket, has been created. This is **not** analogous to a connection creation.    |
| **carrierClosed**               | Some IO handler, such as a UDP socket, has been closed. This is **not** analogous to a connection being closed. |

| **Application Based Events** |                                                                                                                   |
|------------------------------|-------------------------------------------------------------------------------------------------------------------|
| **applicationStart**         | The internal EMS application has started                                                                          |
| **applicationStop**          | The internal EMS application has stopped, likely indicating a shutdown is about to occur                          |
| **serverStarted**            | The EMS has fully started                                                                                         |
| **serverStopping**           | The EMS is about to shutdown. This is sent as late as possible, but clearly not after shutdown has been completed |

The data definitions for each event can be found below. The specific schema for each event will depend up on the serializerType chosen for your Event Notification Sink (defined earlier in this document).

## Stream Event Definitions

### inStreamCreated, outStreamCreated, streamCreated

A new inbound, outbound or neutral stream has been created.
  - **appName** – Name of the application using the stream.
  - **audio** – Statistics about the audio stream.
  - **bandwidth** – Bandwidth of the stream.
  - **connectionType** – Connection type used by stream.
  - **creationTimestamp** – Epoch time stamp when the stream was created (msec since 1/1/70).
  - **ip** – IP address used by the stream.
  - **nearIP** – The address of the host computer
  - **farIP** – The IP of the stream source
  - **name** – Name assigned to the stream.
  - **port** – Port used by the stream.
  - **nearPort** – The port used by the host computer
  - **farPort** – the port used by the stream source
  - **pullSettings** – Pullstream settings. _Only present for inbound streams that are pulled via the pullStream API command_
  - **queryTimestamp** – Epoch time stamp when the stream was queried (msec since 1/1/70).
  - **record** – Record settings for the stream.
  - **type** – Protocol type (see Table of Protocol Types).
  - **typeNumeric** – Protocol type in decimal.
  - **uniqueId** – Stream ID.
  - **upTime** – Stream duration in milliseconds.
  - **video** – Statistics about the video stream.

Example:

    appName: evostreamms
    audio:
      bytesCount: 0
      codec: AUNK
      codecNumeric: 4707755069515235328
      droppedBytesCount: 0
      droppedPacketsCount: 0
      packetsCount: 0
    bandwidth: 0
    connectionType: 1
    creationTimestamp: 1361182998409.229
    ip: 192.168.1.130
    name: test
    port: 49730
    pullSettings:
      audioCodecBytes:
      configId: 1
      emulateUserAgent: EvoStream Media Server (www.evostream.com) player
      forceTcp: false
      isAudio: true
      keepAlive: true
      localStreamName: test
      operationType: 1
      pageUrl:
      ppsBytes:
      rtcpDetectionInterval: 10
      spsBytes:
      ssmIp:
      swfUrl:
      tcUrl:
      tos: 256
      ttl: 256
      uri: rtmp://cp76072.live.edgefcs.net/live/MED-HQ-Flash@42814
    queryTimestamp: 1361182998424.829
    type: INR
    typeNumeric: 5282249572905648128
    uniqueId: 2
    upTime: 15.600
    video:
      bytesCount: 0
      codec: VUNK
      codecNumeric: 6220964544311721984
      droppedBytesCount: 0
      droppedPacketsCount: 0
      packetsCount: 0

### inStreamClosed, outStreamClosed, streamClosed

An inbound, outbound or neutral stream has been closed.
  - **appName** – Name of the application using the stream.
  - **audio** – Statistics about the audio stream.
  - **bandwidth** – Bandwidth of the stream.
  - **connectionType** – Connection type used by stream.
  - **creationTimestamp** – Epoch time stamp when the stream was created (msec since 1/1/70).
  - **ip** – IP address used by the stream.
  - **nearIP** – The address used by the host computer
  - **farIP** – the adress used by the stream source
  - **name** – Name assigned to the stream.
  - **port** – Port used by the stream.
  - **nearPort** – The port used by the host computer
  - **farPort** – the port used by the stream source
  - **queryTimestamp** – Epoch time stamp when the stream was queried (msec since 1/1/70).
  - **record** – Record settings for the stream.
  - **type** – Protocol type (see Table of Protocol Types below).
  - **typeNumeric** – Protocol type in decimal.
  - **uniqueId** – Stream ID.
  - **upTime** – Stream duration in milliseconds.
  - **video** – Statistics about the video stream.

Example:

    appName: evostreamms
    audio:
      bytesCount: 190351
      codec: AAAC
      codecNumeric: 4702111241970122752
      droppedBytesCount: 0
      droppedPacketsCount: 0
      packetsCount: 681
    bandwidth: 548
    connectionType: 1
    creationTimestamp: 1361182998409.229
    ip: 192.168.2.88
    name: test
    outStreamsUniqueIds:
      0: 3
    port: 49730
    pullSettings:
      audioCodecBytes:
      configId: 1
      emulateUserAgent: EvoStream Media Server (www.evostream.com) player
      forceTcp: false
      isAudio: true
      keepAlive: true
      localStreamName: test
      operationType: 1
      pageUrl:
      ppsBytes:
      rtcpDetectionInterval: 10
      spsBytes:
      ssmIp:
      swfUrl:
      tcUrl:
      tos: 256
      ttl: 256
      uri: rtmp://cp76072.live.edgefcs.net/live/MED-HQ-Flash@42814
    queryTimestamp: 1361183030139.685
    type: INR
    typeNumeric: 5282249572905648128
    uniqueId: 2
    upTime: 31730.456
    video:
      bytesCount: 2346717
      codec: VH264
      codecNumeric: 6217274493967007744
      droppedBytesCount: 0
      droppedPacketsCount: 0
      packetsCount: 1147

### inStreamCodecsUpdated, outStreamCodecsUpdated, streamCodecsUpdated

A new inbound, outbound or neutral stream has been identified with a specific codec.
  - **appName** – Name of the application using the stream.
  - **audio** – Statistics about the audio stream.
  - **bandwidth** – Bandwidth of the stream.
  - **connectionType** – Connection type used by stream.
  - **creationTimestamp** – Epoch time stamp when the stream was created (msec since 1/1/70).
  - **ip** – IP address used by the stream.
  - **nearIP** – The address used by the host computer
  - **farIP** – the address used by the stream source
  - **name** – Name assigned to the stream.
  - **port** – Port used by the stream.
  - **nearPort** – The port used by the host computer
  - **farPort** – the port used by the stream source
  - **pullSettings** – Pullstream settings. _Only present for inbound streams that are pulled via the pullStream API command_
  - **queryTimestamp** – Epoch time stamp when the stream was queried (msec since 1/1/70).
  - **record** – Record settings for the stream.
  - **type** – Protocol type (see Table of Protocol Types below).
  - **typeNumeric** – Protocol type in decimal.
  - **uniqueId** – Stream ID.
  - **upTime** – Stream duration in milliseconds.
  - **video** – Statistics about the video stream.

Example:

    appName: evostreamms
    audio:
      bytesCount: 0
      codec: AUNK
      codecNumeric: 4707755069515235328
      droppedBytesCount: 0
      droppedPacketsCount: 0
      packetsCount: 0
    bandwidth: 548
    connectionType: 1
    creationTimestamp: 1361182998409.229
    ip: 192.168.2.88
    name: test
    port: 49730
    pullSettings:
      audioCodecBytes:
      configId: 1
      emulateUserAgent: EvoStream Media Server (www.evostream.com) player
      forceTcp: false
      isAudio: true
      keepAlive: true
      localStreamName: test
      operationType: 1
      pageUrl:
      ppsBytes:
      rtcpDetectionInterval: 10
      spsBytes:
      ssmIp:
      swfUrl:
      tcUrl:
      tos: 256
      ttl: 256
      uri: rtmp://cp76072.live.edgefcs.net/live/MED-HQ-Flash@42814
    queryTimestamp: 1361182998456.029
    type: INR
    typeNumeric: 5282249572905648128
    uniqueId: 2
    upTime: 46.800
    video:
      bytesCount: 56
      codec: VH264
      codecNumeric: 6217274493967007744
      droppedBytesCount: 0
      droppedPacketsCount: 0
      packetsCount: 1

### audioFeedStopped

Event triggered when an audio packet is lost.
- streamId – The stream ID.
- localStreamName – Name of the stream which lost the audio.

### videoFeedStopped

Event triggered when a video packet is lost.
- streamId – The stream ID.
- localStreamName – Name of the stream which lost the video.


## Adaptive Streaming/File-based Streaming Events

### hlsChunkCreated, hdsChunkCreated, mssChunkCreated, dashChunkCreated

Event triggered when an HLS/HDS/MSS/DASH chunk file was opened on disk.
  - **file** – Name of the HLS/HDS/MSS/DASH chunk file that was opened.

Example for HLS:

    file: /var/evo-webroot/hls/stream1/segment_1362025844863_1362025844863_14.ts

Example for HDS:

    file: /var/evo-webroot/hds/stream1/f4vSeg1-Frag1

Example for MSS:

    file: /var/evo-webroot/mss/stream1/video/524288/1413797685000.m4s

Example for DASH:

    file: /var/evo-webroot/dash/stream1/video/229376/1416464032000.fmp4

### hlsChunkClosed, hdsChunkClosed, mssChunkClosed, dashChunkClosed

Event triggered when an HLS/HDS/MSS/DASH chunk file was closed on disk.
  - **file** – Name of the HLS/HDS/MSS/DASH chunk file that was closed.

Example for HLS:

    file: /var/evo-webroot/hls/stream1/segment_1362025844863_1362025844863_14.ts

Example for HDS:

    file: /var/evo-webroot/hds/stream1/f4vSeg1-Frag1

Example for MSS:

    file: /var/evo-webroot/mss/stream1/video/524288/1413797685000.m4s

Example for DASH:

    file: /var/evo-webroot/dash/stream1/video/229376/1416464032000.fmp4

### hlsChunkError, hdsChunkError, mssChunkError, dashChunkError

Event triggered when an error occurs while writing an HLS/HDS/MSS/DASH chunk file.
  - **error** – Description of the error encountered.

Example for HLS:

    error: Could not write video sample to /var/evo-webroot/hls/stream1/segment_1362025844863_1362025844863_14.ts

### hlsChildPlaylistUpdated, hdsChildPlaylistUpdated

Event triggered when an HLS or HDS stream specific playlist file was modified
  - **file** – Name of the HLS or HDS playlist that was updated

Example for HLS:

    file: /var/evo-webroot/hls/stream1/playlist.m3u8

Example for HDS:

    file: /var/evo-webroot/hds/stream1/stream1.f4m

### hlsMasterPlaylistUpdated, hdsMasterPlaylistUpdated

Event triggered when an HLS or HDS group playlist file was modified
  - **file** – Name of the HLS or HDS playlist that was updated

Example for HLS:

    file: /var/evo-webroot/hls/playlist.m3u8

Example for HDS:

    file: /var/evo-webroot/hds/manifest.f4m

### mssPlaylistUpdated, dashPlaylistUpdated

Event triggered when an MSS/DASH stream specific playlist file was modified
  - **file** – Name of the MSS/DASH manifest that was updated

Example for MSS:

    file: /var/evo-webroot/mss/stream1/manifest.f4m

Example for DASH:

    file: /var/evo-webroot/dash/stream1/manifest.mpd

## Web Server Events

### streamingSessionStarted

This event is created right after an HTTP streaming session has started.
  - **clientIP** – Address of connecting client.
  - **sessionID** – Internal ID.
  - **playlist** – The playlist file.
  - **startTime** – Time session started.

### streamingSessionEnded

This event is created right after an HTTP streaming session has stopped.
  - **clientIP** – Address of connecting client.
  - **sessionID** – Internal ID.
  - **playlist** – The playlist file.
  - **startTime** – Time session started.
  - **stopTime** – Time session stopped.

### fileDownloaded

This event is created right after an HTTP file download has completed.
  - **clientIP** – Address of connecting client.
  - **mediaFile** – The path to the media file.
  - **startTime** – Time session started.
  - **elapsed** – The number of seconds since the session started


## API Based Events

### cliRequest

The EMS has received a Runtime API command.
  - **command** – The CLI command received by the EMS.
  - **parameters** – Optional parameters for the CLI command.

Example:

    command: launchProcess
    parameters:
      fullBinaryPath: d:\demoplay.bat

### cliResponse

The response generated by the EMS for the last Runtime API command.
  - **data** – Optional data for the CLI response.
  - **description** – A description of the CLI response.
  - **status** – SUCCESS or FAIL. The result of parsing (not necessarily executing) the CLI command.

Example:

    data:
      arguments:
      configId: 1
      fullBinaryPath: d:\demoplay.bat
      keepAlive: true
      operationType: 6
    description: Process enqueued for start
    status: SUCCESS

### processStarted, processStopped

A process has been started/stopped at the request of the launchProcess API command
  - **arguments** – Arguments for the process just started.
  - **configId** – The configuration ID for the process just started.
  - **fullBinaryPath** – Full path to the binary of the process just started.
  - **keepAlive** – If true, reconnection is attempted every second when the connection is severed.
  - **operationType** – 0:STANDARD, 1:PUSH, 2:PULL, 3:HLS, 4:HDS, 5:RECORD, or 6:LAUNCHPROCESS.

Example:

    arguments:
    configId: 1
    fullBinaryPath: d:\demoplay.bat
    keepAlive: true
    operationType: 6

### timerCreated

A new timer has been created via the setTimer API command
  - **timerId** – The ID of the timer created.
  - **triggerCount** – The number of times the timer triggered since it was created.
  - **value** – The time value for the timer.

Example:

    timerId: 9
    triggerCount: 0
    value: 100

### timerTriggered

A timer has triggered.
  - **timerId** – The ID of the timer that triggered.
  - **triggerCount** – The number of times the timer triggered since it was created.
  - **value** – The time value for the timer.

Example:

    timerId: 9
    triggerCount: 0
    value: 100

### timerClosed

A timer has been closed and will not create any new timerTriggered events.
  - **timerId** – The ID of the timer closed.
  - **triggerCount** – The number of times the timer triggered since it was created.
  - **value** – The time value for the timer.

Example:

    timerId: 9
    triggerCount: 2
    value: 100

## Connection Based Events

### protocolRegisteredToApp

A connection has been fully established.
  - **customParameters** – Custom parameters for the protocol.
  - **protocolType** – Protocol type (see Table of Protocol Types below).

Example:

    customParameters:
      ip: 127.0.0.1
      port: 1112
      protocol: inboundJsonCli
      sslCert:
      sslKey:
      useLengthPadding: true
    protocolType: IJSONCLI

### protocolUnregisteredFromApp

A connection has been disconnected.

  - **customParameters** – Custom parameters for the protocol.
  - **protocolType** – Protocol type (see Table of Protocol Types below).

Example:

    customParameters:
      ip: 127.0.0.1
      port: 1112
      protocol: inboundJsonCli
      sslCert:
      sslKey:
      useLengthPadding: true
    protocolType: IJSONCLI

### carrierCreated

Some IO handler, such as a TCP socket, has been created.

### carrierClosed

Some IO handler, such as a UDP socket, has been closed.

## Application Based Events

### applicationStart, applicationStop

These events are created right after the internal EMS application has started and when that application has stopped, likely indicating server shutdown.
  - **config** – Configuration of the application that just started (see **EMS User's Guide** for details).
  - **id** – ID of the application that just started.
  - **name** – Name of the application that just started.

Example:

    config:
      acceptors:
        0:
          ip: 127.0.0.1
          port: 1112
          protocol: inboundJsonCli
          sslCert:
          sslKey:
          useLengthPadding: true
        1:
          ip: 0.0.0.0
          port: 7777
          protocol: inboundHttpJsonCli
          sslCert:
          sslKey:
        2:
          ip: 0.0.0.0
          port: 1935
          protocol: inboundRtmp
          sslCert:
          sslKey:
        3:
          clustering: true
          ip: 127.0.0.1
          port: 1936
          protocol: inboundRtmp
          sslCert:
          sslKey:
        4:
          clustering: true
          ip: 127.0.0.1
          port: 1113
          protocol: inboundBinVariant
          sslCert:
          sslKey:
        5:
          ip: 0.0.0.0
          port: 5544
          protocol: inboundRtsp
          sslCert:
          sslKey:
        6:
          ip: 0.0.0.0
          port: 6666
          protocol: inboundLiveFlv
          sslCert:
          sslKey:
          waitForMetadata: true
      aliases:
        0: er
        1: live
        2: vod
      appDir: C:\emsdemo\config\
      authPersistenceFile: ..\config\auth.xml
      bandwidthLimitPersistenceFile: ..\config\bandwidthlimits.xml
      connectionsLimitPersistenceFile: ..\config\connlimits.xml
      default: true
      description: EVOSTREAM MEDIA SERVER
      eventLogger:
        sinks:
          1:
            filename: ..\logs\events.txt
            format: text
            type: file
      hasStreamAliases: false
      initApplicationFunction: GetApplication_evostreamms
      initFactoryFunction: GetFactory_evostreamms
      library:
      maxRtmpOutBuffer: 524288
      mediaStorage:
        1:
          description: Default media storage
          mediaFolder: ../media
      metaFileGenerator: false
      name: evostreamms
      protocol: dynamiclinklibrary
      pushPullPersistenceFile: ..\config\pushPullSetup.xml
      rtcpDetectionInterval: 15
      streamsExpireTimer: 10
      validateHandshake: false
    id: 1
    name: evostreamms

### serverStarted

The server has started.

### serverStopped

The server is just about to stop.

## Web Server Events

### streamingSessionStarted

This event is created right after an HTTP streaming session has started.
- **clientIP** – Address of connecting client.
- **sessionID** – Internal ID.
- **playlist** – The playlist file.
- **startTime** – Time session started.

### streamingSessionEnded

This event is created right after an HTTP streaming session has stopped.
- **clientIP** – Address of connecting client.
- **sessionID** – Internal ID.
- **playlist** – The playlist file.
- **startTime** – Time session started.
- **stopTime** – Time session stopped.

### fileDownloaded

This event is created right after an HTTP file download has completed.
- **clientIP** – Address of connecting client.
- **mediaFile** – The path to the media file.
- **startTime** – Time session started.
- **elapsed** – The number of seconds since the session started

## Event Table of Protocol Types

| **Protocol Group**   | **TAG**      | **Protocol Type**      |
|----------------------|--------------|------------------------|
| Carrier Protocols    | **TCP**      | TCP                    |
|                      | **UDP**      | UDP                    |
| Variant Protocols    | **BVAR**     | Bin Variant            |
|                      | **XVAR**     | XML Variant            |
|                      | **JVAR**     | JSON Variant           |
| RTMP Protocols       | **IR**       | Inbound RTMP           |
|                      | **IRS**      | Inbound RTMPS          |
|                      | **OR**       | Outbound RTMP          |
|                      | **RS**       | RTMP Dissector         |
| Encryption Protocols | **RE**       | RTMPE                  |
|                      | **ISSL**     | Inbound SSL            |
|                      | **OSSL**     | Outbound SSL           |
| MPEG-TS Protocol     | **ITS**      | Inbound TS             |
| HTTP Protocols       | **IHTT**     | Inbound HTTP           |
|                      | **IHTT2**    | Inbound HTTP2          |
|                      | **IH4R**     | Inbound HTTP for RTMP  |
|                      | **OHTT**     | Outbound HTTP          |
|                      | **OHTT2**    | Outbound HTTP2         |
|                      | **OH4R**     | Outbound HTTP for RTMP |
| CLI Protocols        | **IJSONCLI** | Inbound JSON CLI       |
|                      | **H4C**      | HTTP for CLI           |
| RPC Protocols        | **IRPC**     | Inbound RPC            |
|                      | **ORPC**     | Outbound RPC           |
| Passthrough Protocol | **PT**       | Passthrough            |
