---
title: Push a Stream
keywords: pushstream
sidebar: userguide_sidebar
permalink: userguide_pushstream.html
folder: userguide 
toc: true
---

Steps on how to do the actual stream push needs to be consulted with the stream source, as every system has different ways of accomplishing this.

## How To

Below are the examples of how to push a stream in different formats:

### RTMP stream

```
pushStream uri=rtmp://DestinationAddress localStreamName=SomeLocalStreamName
```



### RTSP stream

```
pushStream uri=rtsp://DestinationAddress:port localStreamName=SomeLocalStreamName
```



### MPEG-TS stream

MPEG-TS streams, in general, don't have the concept of a stream identifier (name). The EMS will assign a name to an inbound MPEG-TS stream for internal uses, but outside of the EMS, that name is not used. To obtain an MPEG-TS stream from the EMS, it must be first pushed out to the network.

Sample commands to do this are:

```
pushStream uri=mpegtsudp://DestinationAddr localStreamName=SomeLocalStream
```

or

```
pushStream uri=mpegtstcp://DestinationAddr localStreamName=SomeStream
```




## JSON CLI Response

**API Call:**

```
pushStream uri=rtmp://192.168.2.105/live localStreamName=testpullstream targetStreamName=testpushstream 
```

**JSON Response:**

```
Command entered successfully!
Local stream testpullstream enqueued for pushing to rtmp://192.168.2.105/live as
 testpushstream

    configId: 2
    forceTcp: false
    keepAlive: true
    localStreamName: testpullstream
    targetStreamName: testpushstream
    targetStreamType: live
    targetUri:
      fullUri: rtmp://192.168.2.105/live
      port: 1935
      scheme: rtmp
```



## Playing a Pushed Steam

Playing a pushed stream is similar in playing a pulled stream. 

The basic commands in playing a pushed stream in EMS are the following:

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

------

## Related Links:

- [pushStream API](api_pushStream.html)
- [Send Stream To Facebook](userguide_send.html#facebook-live)
- [Send Stream To Youtube](userguide_send.html#youtube-live)
- [Stream Load Balancer Service](evowebservices_streamloadbalancer.html)