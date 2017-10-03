---
title: Event Definitions
keywords: events
sidebar: api_sidebar
permalink: eventdefinition.html
folder: api
toc: true
---


## Stream Events

### inStreamCreated, outStreamCreated, streamCreated

A new inbound, outbound or neutral stream has been created.

```
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
```

- appName – Name of the application using the stream
- audio – Statistics about the audio stream
- bandwidth – Bandwidth of the stream
- connectionType – Connection type used by stream
- creationTimestamp – Epoch time stamp when the stream was created (msec since 1/1/70)
- ip – IP address used by the stream
- nearIP – The address of the host computer
- farIP – The IP of the stream source
- name – Name assigned to the stream
- port – Port used by the stream
- nearPort – The port used by the host computer
- farPort – the port used by the stream source
- pullSettings – `pullstream` settings. *Only present for inbound streams that are pulled via the pullStream API command*
- queryTimestamp – Epoch time stamp when the stream was queried (msec since 1/1/70)
- record – Record settings for the stream
- type – Protocol type (see Table of Protocol Types)
- typeNumeric – Protocol type in decimal
- uniqueId – Stream ID
- upTime – Stream duration in milliseconds
- video – Statistics about the video stream



### inStreamClosed, outStreamClosed, streamClosed

An inbound, outbound or neutral stream has been closed

```
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
```

- appName – Name of the application using the stream
- audio – Statistics about the audio stream
- bandwidth – Bandwidth of the stream
- connectionType – Connection type used by stream
- creationTimestamp – Epoch time stamp when the stream was created (msec since 1/1/70)
- ip – IP address used by the stream
- nearIP – The address used by the host computer
- farIP – the adress used by the stream source
- name – Name assigned to the stream
- port – Port used by the stream
- nearPort – The port used by the host computer
- farPort – the port used by the stream source
- queryTimestamp – Epoch time stamp when the stream was queried (msec since 1/1/70)
- record – Record settings for the stream
- type – Protocol type (see Table of Protocol Types below)
- typeNumeric – Protocol type in decimal
- uniqueId – Stream ID
- upTime – Stream duration in milliseconds
- video – Statistics about the video stream



### inStreamCodecsUpdated, outStreamCodecsUpdated, streamCodecsUpdated

A new inbound, outbound or neutral stream has been identified with a specific codec.

```
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
```

- appName – Name of the application using the stream.
- audio – Statistics about the audio stream.
- bandwidth – Bandwidth of the stream.
- connectionType – Connection type used by stream.
- creationTimestamp – Epoch time stamp when the stream was created (msec since 1/1/70)
- ip – IP address used by the stream
- nearIP – The address used by the host computer
- farIP – the address used by the stream source
- name – Name assigned to the stream
- port – Port used by the stream
- nearPort – The port used by the host computer
- farPort – the port used by the stream source
- pullSettings – `pullstream` settings. *Only present for inbound streams that are pulled via the pullStream API command*
- queryTimestamp – Epoch time stamp when the stream was queried (msec since 1/1/70)
- record – Record settings for the stream
- type – Protocol type (see Table of Protocol Types below)
- typeNumeric – Protocol type in decimal
- uniqueId – Stream ID
- upTime – Stream duration in milliseconds
- video – Statistics about the video stream



### audioFeedStopped, videoFeedStopped

Event triggered when an audio or video packet is lost

```
audioFeedStopped

videoFeedStopped

```

- streamId – The stream ID
- localStreamName – Name of the stream which lost the audio



### playlistItemStart, firstPlaylistItemStart, lastPlaylistItemStart

These events are created when an RTMP playlist item starts to play

```
firstPlaylistItemStart
PID: 10796
playlistName: stream.lst

playlistItemStart
PID: 10796
playlistName: stream.lst

lastPlaylistItemStart
PID: 12268
playlistName: stream.lst
```

- PID: the process ID
- playlistName - the playlist file name



## Adaptive Streaming / File-based Streaming Events

### hlsChunkCreated, hdsChunkCreated, mssChunkCreated, dashChunkCreated

Event triggered when an HLS/HDS/MSS/DASH chunk file was opened on disk.

```
hlsChunkCreated
/evo-webroot/hls/stream1/segment_1362025844863_1362025844863\_14.ts

hdsChunkCreated
evo-webroot/hds/stream1/f4vSeg1-Frag1

mssChunkCreated
/evo-webroot/mss/stream1/video/524288/1413797685000.m4s

dashChunkCreated
/evo-webroot/dash/stream1/video/229376/1416464032000.fmp4
```

**file** – Name of the HLS/HDS/MSS/DASH chunk file that was opened



### hlsChunkClosed, hdsChunkClosed, mssChunkClosed, dashChunkClosed

Event triggered when an HLS/HDS/MSS/DASH chunk file was closed on disk.

```
hlsChunkClosed
/evo-webroot/hls/stream1/segment_1362025844863_1362025844863_14.ts

hdsChunkClosed
/evo-webroot/hds/stream1/f4vSeg1-Frag1

mssChunkClosed
/evo-webroot/mss/stream1/video/524288/1413797685000.m4s

dashChunkClosed
/evo-webroot/dash/stream1/video/229376/1416464032000.fmp4
```

**file** – Name of the HLS/HDS/MSS/DASH chunk file that was closed.



### hlsChunkError, hdsChunkError, mssChunkError, dashChunkError

Event triggered when an error occurs while writing an HLS/HDS/MSS/DASH chunk file.

```
Could not write video sample to /evo-webroot/hls/stream1/
segment_1362025844863_1362025844863_14.ts
```

- error – description of the error encountered



### hlsChildPlaylistUpdated, hdsChildPlaylistUpdated

Event triggered when an HLS or HDS stream specific playlist file was modified

```
hlsChildPlaylistUpdated
/evo-webroot/hls/stream1/playlist.m3u8

hdsChildPlaylistUpdated
/evo-webroot/hds/stream1/stream1.f4m
```

**file** – Name of the HLS or HDS playlist that was updated



### hlsMasterPlaylistUpdated, hdsMasterPlaylistUpdated

Event triggered when an HLS or HDS group playlist file was modified

```
hlsMasterPlaylistUpdated
/evo-webroot/hls/playlist.m3u8

hdsMasterPlaylistUpdated
/evo-webroot/hds/stream1.f4m
```

**file** – Name of the HLS or HDS playlist that was updated



### mssPlaylistUpdated, dashPlaylistUpdated

Event triggered when an MSS/DASH stream specific playlist file was modified

```
mssPlaylistUpdated
/evo-webroot/mss/stream1/manifest.f4m

dashPlaylistUpdated
/evo-webroot/dash/stream1/manifest.mpd
```

**file** – Name of the MSS/DASH manifest that was updated



### recordChunkCreated, recordChunkClosed, recordChunkError

Event triggered when a new record fragment has been opened, completed and ready on disk, or failed due to a write error

```
/media/record/stream1_part0008.mp4
```

**file** – Name of the record fragment that was opened, closed, or had a write error



## Web Server Events

### streamingSessionStarted

This event is created right after an HTTP streaming session has started.

- clientIP – Address of connecting client
- sessionID – Internal ID
- playlist – The playlist file
- startTime – Time session started



### streamingSessionEnded

This event is created right after an HTTP streaming session has stopped.

- clientIP – Address of connecting client
- sessionID – Internal ID
- playlist – The playlist file
- startTime – Time session started
- stopTime – Time session stopped


### fileDownloaded

This event is created right after an HTTP file download has completed.

- clientIP – Address of connecting client.
- mediaFile – The path to the media file.
- startTime – Time session started.
- elapsed – The number of seconds since the session started



## API Based Events

### cliRequest

The EMS has received a Runtime API command.

- command – The CLI command received by the EMS
- parameters – Optional parameters for the CLI command

**Example:**

```
command: launchProcess
	parameters:
		fullBinaryPath: d:\demoplay.bat

```



### cliResponse

The response generated by the EMS for the last Runtime API command.

```
data:
		arguments: 
		configId: 1
		fullBinaryPath: d:\demoplay.bat
		keepAlive: true
		operationType: 6
	description: Process enqueued for start
	status: SUCCESS
```

- data – Optional data for the CLI response
- description – A description of the CLI response
- status – SUCCESS or FAIL. The result of parsing (not necessarily executing) the CLI command



### processStarted, processStopped

A process has been started/stopped at the request of the launchProcess API command.

```
arguments: 
configId: 1
	fullBinaryPath: d:\demoplay.bat
	keepAlive: true
	operationType: 6
```

- arguments – Arguments for the process just started.
- configId – The configuration ID for the process just started.
- fullBinaryPath – Full path to the binary of the process just started.
- keepAlive – If true, reconnection is attempted every second when the connection is severed.
- operationType – 0:STANDARD, 1:PUSH, 2:PULL, 3:HLS, 4:HDS, 5:RECORD, or 6:LAUNCHPROCESS.



### timerCreated

A new timer has been created via the setTimer API command

```
arguments: 
configId: 1
	fullBinaryPath: d:\demoplay.bat
	keepAlive: true
	operationType: 6
```

- timerId – The ID of the timer created
- triggerCount – The number of times the timer triggered since it was created
- value – The time value for the timer



### timerTriggered

A timer has triggered.

```
timerId: 9
triggerCount: 0
value: 100
```

- timerId – The ID of the timer that triggered
- triggerCount – The number of times the timer triggered since it was created
- value – The time value for the timer



### timerClosed

A timer has been closed and will not create any new timerTriggered events.

```
timerId: 9
triggerCount: 2
value: 100
```

- timerId – The ID of the timer closed
- triggerCount – The number of times the timer triggered since it was created
- value – The time value for the timer



## Connection Based Events

### protocolRegisteredToApp

A connection has been fully established.

```
	customParameters:
		ip: 127.0.0.1
		port: 1112
		protocol: inboundJsonCli
		sslCert: 
		sslKey: 
		useLengthPadding: true
	protocolType: IJSONCLI
```

- customParameters – Custom parameters for the protocol.
- protocolType – Protocol type (see Table of Protocol Types below).



### protocolUnregisteredFromApp

A connection has been disconnected.

```
	customParameters:
		ip: 127.0.0.1
		port: 1112
		protocol: inboundJsonCli
		sslCert: 
		sslKey: 
		useLengthPadding: true
	protocolType: IJSONCLI
```

- customParameters – Custom parameters for the protocol.
- protocolType – Protocol type (see Table of Protocol Types below).



### carrierCreated

Some IO handler, such as a TCP socket, has been created.

```

```



### carrierClosed

Some IO handler, such as a UDP socket, has been closed.

```

```



## Application Based Events

### applicationStart, applicationStop

These events are created right after the internal EMS application has started and when that application has stopped, likely indicating server shutdown.

```
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
```

- config – Configuration of the application that just started (see EMS User’s Guide for details)
- id – ID of the application that just started
- name – Name of the application that just started



### serverStarted

The server has started.

```

```



### serverStopped

The server is just about to stop.

```

```
------

## Notes:

- Make sure [eventLogger](userguide_configlua.html#eventLogger) is not commented to be able to use events.

------

## Related Links

- [Event Overview](eventoverview.html)
- [Configuring Event Notifications](eventnotification.html)
- [Event Sinks](eventsinks.html)
- [Application vs. Server Events](eventappvsserver.html)
- [Events List](eventlist.html)
- [Event Logger](userguide_configlua.html#eventLogger)
- [EvoWebservices Event](evowebservices_event.html)
- [EvoWebservices Event Configuration](evowebservices_eventconfiguration)



