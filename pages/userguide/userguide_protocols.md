---
title: Protocol Support and Specifics
keywords: API
sidebar: userguide_sidebar
permalink: userguide_protocols.html
folder: userguide
toc: true
---



This section will dive into the specific capabilities of the EvoStream Media Server. Please keep in mind that directionality is always from the perspective of the EMS. Therefore “inbound” will refer to any stream coming into the EMS and “outbound” will refer to any stream leaving the EMS.



## Real Time Messaging Protocol (RTMP)

The EMS is fully compatible with the RTMP protocol. This means that it can receive streams from Adobe’s Flash Media Live Encoder (FMLE), Wirecast, Flash Applets, and many other sources. It also enables any Flash or Adobe-Air based clients to play streams from the EMS. Some examples of clients/players that use RTMP are FlowPlayer, JWPlayer and VLC. Using RTMP, you can reach ANY Flash enabled web browser, which really means that you can reach any browser on Windows, Mac OSX and Linux.



### Ingesting RTMP

There are several ways that the EMS can use RTMP as a stream source. The first method is to use the Runtime-API to pull a stream from some source. An example of a pullstream command is as follows:

```
pullstream uri=rtmp://192.168.1.5/live/MyTestStream localStreamName=TestStream
```

This command tells the EMS to go and get **MyTestStream** from the server at **192.168.1.5**, and then name the stream locally **TestStream**. Please see `pullStream` [API](insert link here) for more information on local stream names.

The typical URI format for requesting RTMP streams is as follows:

```
rtmp://[username[:password]@]IP[:port]/<appName>/<localStreamName>
```



### Outbound RTMP (Live and VOD)

Any source stream can be played back via RTMP. Most often a user will be using a Flash based player which will make an RTMP request on the EMS. To request an RTMP stream from the EMS, you need to use a URI formatted as follows:

```
rtmp://[username[:password]@]IP[:port]/<live/vod>/<localStreamName>
```

An example of this URI may be:

```
rtmp://192.168.1.5/live/MyTestStream

```

The EMS can also PUSH streams towards another server or some other destination. The `pushStream`Runtime-API function is used to do this. An example of the `pushStream` API is as follows:

```
pushStream uri=rtmp://192.168.1.5/live/ localStreamName=MyTestStream targetStreamName=PushedStreamName
```



### RTMPT

RTMP via HTTP is supported by the EMS. RTMPT can be leveraged in exactly the same way as RTMP. You will simply need to use “RTMPT” instead of “RTMP” in the various URIs and addresses. To enable the EMS to accept requests from RTMPT clients, you must create an Acceptor (listener) in the config/config.lua file that looks like the following:

```
{
      ip="0.0.0.0",                                  
      port=8081,                                     
      protocol="inboundRtmpt"
},

```



### RTMPS

RTMP secured by SSL is supported by the EMS. RTMPS can also be leveraged in exactly the same way as RTMP. In addition to using “RTMPS” instead of “RTMP” in the various URIs and addresses, you will also need to create and specify a certificate and key to be able to “Serve” RTMPS streams.

You must create a signed certificate file using a library like OpenSSL (*.crt) and a corresponding public key file (*.pem). You must then create an Acceptor (listener) in the config/config.lua file that looks like the following:

```
{
      ip="0.0.0.0",                                  
      port=8082,                                     
      protocol="inboundRtmps",                       
      sslKey="server.key",                           
      sslCert="server.crt"                           
},

```

The paths to the sslKey and sslCert are relative to the runtime directory. It may be best to use absolute paths when specifying those files.

Again, this setup is only necessary when serving these files (clients requesting a stream via RTMPS). These keys are not used when pushing or pulling a stream since the other side of the transaction will be acting as the server and will therefore provide its own keys



### RTMP Ingest Points

When Ingest Points are active, the EMS requires streams pushed to the EMS to provide a specific Target Stream Name. This mechanism provides a robust way to allow trusted partners to easily push streams to your EMS server.

Ingest Points operate by specifying two linked values: the **privateStreamName** and the **publicStreamName**. Both the privateStreamName and the **publicStreamName** must be unique within a given EMS instance. When an RTMP stream is PUSHED to the EMS, the Target Stream Name defined within the RTMP stream must match one of the defined privateStreamNames. If a match exists, the stream is accepted and brought into the EMS. This new stream can then be accessed from the EMS using the associated publicStreamName.

To enable Ingest Points, you must set the `hasIngestPoints` parameter in the config.lua file to true:

```
hasingestpoints=true,

```

Ingest Points have a full set of API functions which must beused to add and remove Ingest Points. The API functions are listed here, but please see the [API Definition document]((insert link here)) for a full description.

- createIngestPoint
- removeIngestPoint
- listIngestPoints

Ingest Points are stored by the EMS into the **config/ingestPoints.xml** file. See [ingstpoints.xml]().





## Real Time Streaming Protocol (RTSP)

Using the RTSP protocol can many different players and servers, including the native Android media player. RTSP can be used as both a stream source and as an outbound stream protocol. There are a few variants of RTSP and so it is important to understand a little bit about the protocol itself.

RTSP itself is just a negotiation protocol. Its job is to set up and coordinate other connections which will then handle the transfer of video and audio data. Normally, the RTSP transaction will create 4 additional channels, one for audio, one for video, and then two Real Time Control Protocol (RTCP) connections for syncing the audio and video streams. This means that a typical RTSP stream has actually 5 separate connections/streams.

In addition to this setup, the audio and video streams can be transferred over a couple of different mechanisms, namely Real-time Transfer Protocol (RTP) or MPEG Transport Stream (MPEG-TS). The EMS supports all combinations of RTSP over RTP or MPEG-TS and with or without RTCP channels.

While RTCP channels are usually included in RTSP streams, they are not required components. The EMS does not, therefore, require them to be present. However, the EMS will wait for a specified amount of time when a new RTSP stream is introduced while it tries to detect an RTCP channel. During this waiting period, all packets from the RTSP stream will be dropped! This waiting period can be adjusted in the config.lua file by modifying the rtcpDetectionInterval parameter which sets the seconds to wait before starting the stream without RTCP support.



### Ingesting RTSP

There are several ways that the EMS can use RTSP as a stream source.  The first method is to use the Runtime-API to pull a stream from some source. An example of a `pullstream` command is as follows:

```
pullstream uri=rtsp://192.168.1.5/MyTestStream localStreamName=TestStream
```

This command tells the EMS to go and get **MyTestStream** from the server at **192.168.1.5**, and then name the stream locally **TestStream**. Please see `pullStream` [API](insert link here) for more information on local stream names.

The typical URI format for requesting RTSP streams is as follows:

```
rtsp://[username[:password]@]IP[:port]/<stream or sdp file name>
```

When pulling an RTSP stream via an HTTP Proxy, the `pullstream` command will be as follows:

```
pullstream uri=rtsp://[username[:password]@]HostName/StreamName httpProxy=IP[:PORT] localStreamName=TestStream
```

To pull an RTSP stream via HTTP the httpProxy parameter can again be leveraged:

```
pullstream uri=rtsp://[username[:password]@]HostName/StreamName httpProxy=self localStreamName=TestStream
```

**Note:**

The `httpProxy=self` parameter simply implies that there is NO proxy, and to pull the stream, via HTTP, directly from the specified URI.

The EMS also allows you to Push an RTSP stream into it. The EMS listens for RTSP streams on port 5544, which is NOT the default RTSP port of 554. This requires you to specify the port of 5544 when pushing streams into the EMS. The port the EMS listens on can be modified by changing the appropriate value in the config.lua file. You will need to consult the manuals for your stream source to understand how to push a stream.

The EMS can require authentication for streams that are being pushed to it. If authentication is enabled, you will need to either supply authentication details along with your pushed stream, or disable authentication for the EMS before the EMS will accept your streams. Please see the [authentication]() for more information.



### Outbound RTSP (Live and VOD)

Any source stream can be played back via RTSP. Some common RTSP players are VLC, Android Devices and Quicktime. To request an RTSP stream from the EMS, you need to use a URI formatted as follows:

```
rtsp://[username[:password]@]IP[:port]/[ts|vod|vodts]/<LocalStreamName or MP4 file name>

```

Some examples of RTSP requests are as follows:

Request a live RTSP/RTP stream:

```
rtsp://192.168.1.5:5544/MyTestStream

```

Request a live RTSP/MPEG-TS stream:

```
rtsp://192.168.1.5:5544/ts/MyTestStream

```

Request a VOD MP4 file via RTSP/RTP:

```
rtsp://192.168.1.5:5544/vod/MyMP4File.mp4

```

Request a VOD MP4 file via RTSP/MPEG-TS:

```
rtsp://192.168.1.5:5544/vodts/MyMP4File.mp4

```

For VOD requests, the file name can also include the path relative to the media folder:

```
rtsp://192.168.1.5:5544/vod/folder1/folder2/MyMP4File.mp4

```

Only MP4 files can be used for RTSP VOD playback. TS and FLV files cannot be used as sources at this time.

The EMS can also PUSH streams towards another server or some other destination. The `pushStream`Runtime-API function is used to do this. An example of the `pushStream` API is as follows:

```
pushStream uri=rtsp://192.168.1.5:5544 localStreamName=MyTestStream targetStreamName=PushedStreamName
```



## MPEG Transport Stream (MPEG-TS)

The EMS fully supports MPEG2 Transport Stream over both UDP and TCP. UDP MPEG-TS streams can be unicast, broadcast or multicast. In order to receive a UDP multicast stream, you must issue a pullstream command using the **dmpegtsudp://** protocol indicator (the “d” is for deep-parse):

```
pullstream uri=dmpegtsudp://229.0.0.1:5555 localstreamname=TestTSMulticast

```

**TCP MPEG-TS** streams can also be pulled by the server by using the above command, simply replacing “**udp”** with “**tcp”**:

```
pullstream uri=dmpegtstcp://192.168.1.5:5555 localstreamname=TestTSMulticast

```

**MPEG-TS TCP** streams can also be pushed into the server, but you must first tell the EMS what ports to listen to. You can do this by creating “acceptors” in the **config.lua** file:

```
{
	ip="0.0.0.0",
	port=9998,
	protocol="inboundTcpTs"
},
{
	ip="0.0.0.0",
	port=9999,
	protocol="inboundUdpTs"
},
```

For either of these configured acceptors, a “localstreamname” variable can be added to set the name of the stream that gets pushed into the acceptor. This will limit the acceptor to just a single inbound stream (the TCP acceptor could accept many if needed) but it has the advantage of creating a known stream name.

For example, the following config will create a stream named “test1” when an MPEG-TS stream is pushed over TCP to port 9998: `{ ip="0.0.0.0", port=9998, localstreamname="test1",protocol="inboundTcpTs" },`

The EMS will need to be restarted before any changes to the config.lua file will take effect.



## HTML5 Web Sockets

HTML5 Web Socket technology provides socket connections between a web browser and a server, as opposed to the traditional request/response model of HTTP. With HTTP, for the server to send data the client has to initiate the communication via a request and the server will then send back a response. HTTP incurs considerable overhead which makes it not ideal for low latency applications.

With Web Sockets, a persistent connection between the client (web browser) and the server is established and either of them can start sending data anytime, thus eliminating the dependency on the client-side to initiate the request. This results in a low-latency connection providing a more “real-time” data delivery.

The EMS utilizes this technology to provide the following functions:

- Metadata Outbound Push – transmits Metadata to a browser as it is received.
- Metadata Ingest – accepts incoming Metadata.
- FMP4 Player – an acceptor which transmits a fragmented MP4 (FMP4) stream.

Both Metadata Outbound Push and Metadata Ingest use a **Web Sockets Metadata Acceptor**. The EMS uses this to receive and/or send metadata.

The definition for this is found in the acceptors section of the EMS configuration file (*config.lua*):

```
acceptors =
{
    -- content removed for clarity
    -- WebSockets JSON Metadata
    {
        ip="0.0.0.0",
        port=8210,
        protocol="wsJsonMeta",
        -- streamname="~0~0~0~"
    },
    -- content removed for clarity
},

```

The `streamname` parameter is optional, default will match **all** incoming streams.

```
ws://host:port/streamname

```

Use the GET format to open a websocket channel:

The `streamname` above, if not empty, will override what is specified in the acceptor definition in config.lua.

Matching JSON metadata arrives as text. Use WS.send() to input JSON metadata.

Below is a sample minimal metadata page:

```
<script>
    var ws= new WebSocket("ws://myems:8210/");
    ws.onmessage= function (msg) {
        console.log(msg.data);
    }
    Function doSend() {
        var x={fred:{wife:"Wilma",friend:"Barney"}};
        ws.send(JSON.stringify(x));
    }
</script>
<button onclick="doSend();">SEND</button>

```

For the FMP4 Player, a Web Sockets acceptor is defined in `config.lua`:

```
acceptors =
{
    -- content removed for clarity
    -- WebSockets FMP4 Fetch
    {
        ip="0.0.0.0",
        port=8410,
        protocol="inboundWSFMP4",
    },
    -- content removed for clarity
},
```

The above defines an outbound FMP4 acceptor. It does say “inbound” because the Web Socket connector is inbound, it being an acceptor.

```
ws://host:port/streamname

```

To connect, a Web Socket “GET” call is used. Following is the “GET” URI format

The *streamname* is a local stream name of a stream that is pulled in the EMS.

A sample HTML file with an FMP4 player, `evowsvideo.html`, is provided. You may use this to try out the Web Socket FMP4 functionality.

For convenience, a demo page is already available upon installation: `..\evo-webroot\demo\evowsvideo.html` Another option for playback is using `http://ers.evostream.com:5050/demo/evowsvideo.html`.





