---
title: Pull a Stream
keywords: pullstream
sidebar: userguide_sidebar
permalink: userguide_pullstream.html
folder: userguide
toc: true
---

The EMS provides an extremely robust platform for stream protocol re-encapsulation. That is, the EMS will allow the translation from one streaming protocol to another protocol, allowing the reach to a wide range of video/audio clients, regardless of how the video/audio source is configured.

The first step to achieve protocol re-encapsulation is to get the original stream into the EMS. The most common method for doing this is by using the “**Pull a Stream**” mechanism, but other systems can also push a stream into the EMS.

The `pullStream` API provides a way to tell the EMS to retrieve an existing stream.



## How To

Below are the examples of how to pull a stream in different formats:

### RTMP stream

```
pullStream uri=rtmp://<STREAM_ADDRESS> localStreamName=RTMPTest
```



### RTSP stream

```
pullStream uri=rtsp://<STREAM_ADDRESS> localStreamName=RTSPTest
```



### RTP - UDP stream

```
pullStream uri=rtp://<STREAM_ADDRESS> localStreamName=RTPTest isAudio=0 spsBytes=Z0LAHpZiA2P8vCAAAAMAIAAABgHixck= ppsBytes=aMuMsg==
```



### MPEG-TS stream

#### UDP MPEG-TS stream

```
pullStream uri=dmpegtsudp://<STREAM_ADDRESS>:<PORT> localStreamName=TSTest
```

This can be used for multicast streams as well. If the address of the stream is in the IP Multicast range, the EMS will automatically join the multicast group so that it can pull the stream.

#### TCP MPEG-TS

```
pullStream uri=dmpegtstcp://<STREAM_ADDRESS>:<PORT> localStreamName=TSTest
```

**Note:**

The “**d**” in front of mpegts ( **d**mpegts) in the URIs above refers to “deep parsing”. Using the URI, the inbound MPEG-TS stream can be re-encapsulated into other protocols such RTMP or RTSP. If the only output format will be MPEG-TS (e.g. EMS is used as an MPEG-TS pass-through), then mpegtsudp and mpegtstcp can be used as the URI protocol specifier. This will speed the transfer of the MPEG-TS streams since no parsing will occur.



### LOCAL SDP FILE

EMS is also capable in pulling an Session Description Protocol (SDP) file. An SDP is a format for describing the initialization parameters of streaming media sessions. SDP does not deliver media itself but is used for negotiation between end points of media type, format, and all associated properties.

```
pullStream uri=file://<FILEPATH>/FILENAME.sdp localStreamName=sdpFileTest
```

**Note:**

The SDP must reside in the file system accessible by EMS.



## JSON CLI Response

**API Call:**

```
pullstream uri=rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 localStreamname=testpullstream
```

**JSON Response:**

```
Command entered successfully!
Stream rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 enqueued for p
ulling

    configId: 1
    forceTcp: false
    keepAlive: true
    localStreamName: testpullstream
    uri:
      fullUri: rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4
      port: 1935
      scheme: rtmp
```



## Playing a Pulled Steam

Once a stream has been added to EMS, it can be accessed in a variety of ways. Through the streaming protocol translation offered by EMS, it is just a matter of requesting the stream in the format that the target player can accept, and the EMS will take care of the rest.

The basic commands in playing a pulled stream in EMS are the following:

- **RTMP**

  The format of the RTMP URI is as follows:

  ```
  rtmp[t|s]://[username[:password]@]ip[:port]/<appName>/<stream_name>
  ```

  As an example, to play an RTMP stream, use the following URI in the Flash enabled player:

  ```
  rtmp://<EMS_IP_ADDRESS>/live/localStreamName
  ```

- **RTMP**

  The format of the RTSP URI is as follows:

  ```
  rtsp://[username[:password]@]ip[:port]/[ts|vod|vodts]/<stream_name or MP4 file name>
  ```

  **Note:**

  The command is very similar to RTMP, except for the absence of the “appName” field.

  As an example, to play an RTSP stream, the following URI in an RTSP enabled player can be used:

  ```
  rtsp://<EMS_IP_ADDRESS>:5544/localStreamName
  ```

  By default, the EMS will send the video/audio payload data via RTP. If MPEG-TS is needed instead, simply specify it in the request URI:

  ```
  rtsp://<EMS_IP_ADDRESS>:5544/ts/localStreamNam
  ```

------

## Related Links:

- [pullStream API](api_pullStream.html)
- [Adding Inbound Streams](userguide_add.html#adding-inbound-live-streams)
- [Stream AutoRouting Service](evowebservices_streamautorouting.html)