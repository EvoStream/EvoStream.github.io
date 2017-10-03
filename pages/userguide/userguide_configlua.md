---
title: config.lua
keywords: configuration
sidebar: userguide_sidebar
permalink: userguide_configlua.html
folder: userguide
toc: true
---

This is the main configuration file for the EMS. This file defines all of the startup parameters used by the server, including the location and names of all of the other configuration files. If you wish to change the name of any of the subsequent configuration files, you can do so here. This file is also just a command-line parameter to the EMS executable. The run-scripts provided with the EMS distribution use this file by default. If you want to change the location or name of this file you can simply modify the run scripts to use a different file.

The EMS configuration file, config.lua, is a hierarchical data structure of assignments (key names with values). It is sent as a parameter when running the EvoStream server. The format is as follows:

- **`<keyname>= <value>`**

  where `value` could be any of the following types:

  - string = series of alpha numeric characters (should be enclosed in double quotes)

    ```
    Example:	pushPullPersistenceFile="..\\config\\pushPullSetup.xml",
    ```

  - number = digits

    ```
    ​```
    Example:	streamsExpireTimer=10,
    ​```
    ```

  - array = list of values (separated by comma and is grouped by braces {}, each value enclosed in double quotes)

    ```
    Example:	aliases = {“flvplayback1”, “vod1”, “live”}
    ```

    ​


- **`<keyname>= <object>`**

  where `object`is a list of assignments enclosed by braces {}

  ```
  configurations =
  {
      daemon = "true",
      pathSeparator = "/",
      logAppenders = {...},
      applications = {...}
  }
  ```

  **Note:** 

  If you modify this file and the server then fails to start, you have made an error. You can either roll-back your changes or you can use the `--use-implicit-console-appender` command line parameter to get extra debug information about what failed during startup.

  - For Linux Package:

    ```
    cd /usr/bin/evostreamms –use-implicit-console-appender /etc/evostreamms/config.lua
    ```

    - For Linux Archive:

      ```
      cd EMS_INSTALL_DIRECTORY
      ./evostreamms --use-implicit-console-appender ../config/config.lua
      ```

    - For Windows:

      ```
      cd EMS_INSTALL_DIRECTORY
      evostreamms --use-implicit-console-appender config\config.lua
      ```

  **Where:**

  EMS_INSTALL_DIRECTORY is the `bin` directory within the EvoStream Media Server Archive directory.

  1. The “daemon” value is read. The server now will either fork to become daemon or continue as is in console mode.
  2. The “logAppenders” value is read. This is where all log appenders are configured and brought up to running state. Depending on the collection of your log appenders, you may (not) see further log messages.
  3. The “applications” value is taken into consideration. Up until now, the server doesn't do much. After this stage completes, all the applications are fully functional and the server is online and ready to do stuff.



## daemon

For Linux only. If **true** means the server will start in daemon mode. **false** means it will start in console mode (nice for development).

**Type:** Boolean

**Mandatory:** Yes

```
daemon = false,
```



## instancesCount

For Linux only.  The number of virtual instances of EMS server where load balancing will be performed. If this item is missing, it will be replaced by 0, disabling multiple instances. If its value is -1, it will be replaced by the number of CPUs, enabling one or more additional instances.

**Type:** Number

**Mandatory:** Yes

```
instancesCount=-1
```



## pathSeparator

This value will be used by the server to compose paths (like media files paths). Examples: on UNIX-like systems this is / while on windows is . Special care must be taken when you specify this value on windows because \ is an escape sequence for Lua so the value should be “\”.

**Type:** String

**Mandatory:** Yes

```
pathSeparator="/",
```



## logAppenders

This section contains a list of log appenders. The entire collection of appenders listed in this section is loaded inside the logger at config-time. All log messages will be than passed to all these log appenders. Depending on the log level, an appender may (or may not) log the message. “Logging” a message means “saving” it on the specified “media” (in the example below we have a console appender and a file).

**Type:** Object

**Mandatory:** Yes

```
logAppenders=
	{
		{
			name="console appender",
			type="coloredConsole",
			level=6
		},
		{
			name="file appender",
			type="file",
			level=6,
			fileName="..\\logs\\evostream",
			newLineCharacters="\n",
			fileHistorySize=100,
			fileLength=1024*1024,
			singleLine=true,
			clearLogsOnStart=false
		},
	},
```

**logAppenders Structure Table**

|        Key        |  Type   | Mandatory | Description                              |
| :---------------: | :-----: | :-------: | ---------------------------------------- |
|       name        | string  |    yes    | The name of the appender. It is usually used inside pretty print routines. |
|       type        | string  |    yes    | The type of the appender. Types `console` and `coloredConsole` will output to the console. The difference between them is that `coloredConsole` will also apply a color to the message, depending on the log level. Quite useful when eye-balling the console. Type `file` log appender will output everything to the specified file. |
|       level       | number  |    yes    | The log level used. The values are presented just below. Any message having a log level less or equal to this value will be logged. The rest are discarded. (**Log levels:** 0 FATAL, 1 ERROR, 2 WARNING, 3 INFO, 4 DEBUG, 5 FINE, 6 FINEST, -1 disable logs) |
|     fileName      | string  |    yes    | If the type of appender is a file, this will contain the path of the file. |
| newLineCharacters | string  |    no     | Newline character used in the file appender. |
|  fileHistorySize  | number  |    no     | The maximum number of log files to be retained. The oldest log file will be deleted first if this number is exceeded. |
|    fileLength     | number  |    no     | Buffer size of the file appender.        |
|    singleLine     | boolean |    no     | If yes, multi-line log messages are merged into one line. |
| clearLogsOnStart  | boolean |    no     | If **true**, the EMS should go through the destination folder for log files and delete all files named "*.log" excluding the current .log files. For file appender only. |

**Note:** When daemon mode is set to true, all console appenders will be ignored..



## applications

Will hold a collection of loaded applications. Besides that, it will also hold few other values.

**Type:** Object

**Mandatory:** Yes



Below are the objects inside applications:



### rootDirectory

The folder containing applications subfolders. If this path begins with a “/” or “" (depending on the OS), then is treated as an absolute path. Otherwise is treated as a path relative to the run-time directory (the place where you started the server).

**Type:** String

**Mandatory:** Yes

```
rootDirectory="./",
```



### appDir

Combined with rootDirectory to form a default base directory for non-absolute paths.

**Type:** String

**Mandatory:** Yes

```
appDir="./",
```



### name

The name of the server. Could be the name of the company, organization etc.

**Type:** String

**Mandatory:** No

```
name="evostreamms",
```



### description

The description of the "name".

**Type:** String

**Mandatory:** No

```
description="EVOSTREAM MEDIA SERVER",
```



### default

Selects default application

**Type:** Boolean

**Mandatory:** Yes

```
default=true,
```



### pushPullPersistenceFile

The path of the pushPull configuration file.

**Type:** String

**Mandatory:** Yes

```
pushPullPersistenceFile="..\\config\\pushPullSetup.xml",
```



### authPersistenceFile

The path of the authentication file

**Type:** String

**Mandatory:** Yes

```
authPersistenceFile="..\\config\\auth.xml",
```



### connectionsLimitPersistenceFile

The path of the connection limit file

**Type:** String

**Mandatory:** Yes

```
connectionsLimitPersistenceFile="..\\config\\connlimits.xml",
```



### bandwidthLimitPersistenceFile 

The path of the bandwidth limit file

**Type:** String

**Mandatory:** Yes

```
bandwidthLimitPersistenceFile="..\\config\\bandwidthlimits.xml",
```



### ingestPointsPersistenceFile

The path of the ingest points file

**Type:** String

**Mandatory:** Yes

```
ingestPointsPersistenceFile="..\\config\\ingestpoints.xml",
```



### streamsExpireTimer

The number of seconds the EMS will wait for audio/video data from a connected stream before timing out

**Type:** Number

**Mandatory:** Yes

```
streamsExpireTimer=10,
```



### rtcpDetectionInterval

The number of seconds the EMS will wait for RTCP streams in an RTSP session before continuing without them

**Type:** Number

**Mandatory:** Yes

```
rtcpDetectionInterval=15,
```



### hasStreamAliases

Enables or disables stream name aliases

**Type:** Boolean

**Mandatory:** Yes

```
hasStreamAliases=false,
```

See [addStreamAlias](addStreamAlias.html)



### hasIngestPoints

The configuration of the ingest point 

**Type:** Boolean

**Mandatory:** Yes

```
hasIngestPoints=false
```

See [createIngestPoint](createIngestPoint.html)



### validateHandshake

Set to false for old Flash players with no RTMP validation handshake

**Type:** Boolean

**Mandatory:** Yes

```
validateHandshake=false,
```



### aliases

The extension of the stream where alias can be added

**Type:** Array

**Mandatory:** Yes

```
aliases={"er", "live", "vod"},
```



### maxRtmpOutBuffer

The maximum amount of bytes the EMS will store in the output RTMP buffer

**Type:** String

**Mandatory:** Yes

```
maxRtmpOutBuffer=512*1024,
```



### maxRtspOutBuffer

The maximum amount of bytes the EMS will store in the output RTSP buffer. Only used for RTSP when the final transport is RTP over TCP

**Type:** String

**Mandatory:** Yes

```
maxRtspOutBuffer=512*1024,
```



### hlsVersion

The HLS version to be used. User should make sure of the version before creating HLS files.

**Type:** Number

**Mandatory:** Yes

```
hlsVersion=6,
```

Supported versions:

- HLS version 3
- HLS version 4
- HLS version 5
- HLS version 6

For more information about HLS click [here](https://developer.apple.com/library/content/referencelibrary/GettingStarted/AboutHTTPLiveStreaming/about/about.html).



### useSourcePts

If set to true, the outbound stream will use the PTS of the source stream. Otherwise, the pushed stream will start at 0

**Type:** Boolean

**Mandatory:** Yes

```
useSourcePts=false,
```



### enableCheckBandwidth

Reads the bandwidth.xml if set to true

**Type:** Boolean

**Mandatory:** Yes

```
enableCheckBandwidth=true,
```

See [bandwidths.xml](userguide_bandwidthlimits.html)



### vodRedirectRtmpIp

The IP of the other server where EMS can get the source VOD file.

**How it works?** The local server will look for video1. When that lookup fails it will get the configuration details set to `vodRedirectRtmpIp` parameter. If there's a valid value, the local server makes a `pullStream` request on the server (vodRedirectRtmpIP value) for video1. The local server then uses that new stream resulting from the `pullStream` to serve the initial client request.

**Type:** String

**Mandatory:** No

```
vodRedirectRtmpIp="",
```

**Note:** This will only access the mediaFolder. Make sure that the VOD files are inside the mediaFolder or else, searching for the source is on loop.



### forceRtmpDatarate

Hardcodes videodatarate and audiodatarate to satisfy the requirements for some configurations.

**Type:** Boolean

**Mandatory:** Yes

```
forceRtmpDatarate=false,
```



### sendRtspRangeHeaders

Required for axis camera configuration

**Type:** Boolean

**Mandatory:** Yes

```
sendRtspRangeHeaders=false,
```



### serverNameStreamPrefix

Server name used as prefix for stream name 

**Type:** String

**Mandatory:** No

```
serverNameStreamPrefix="",
```



### runWebServer

Enables EMS Web Server on startup

**Type:** Boolean

**Mandatory:** Yes

```
runWebServer=true,
```



### runWebUI

Enables EMS Web UI on startup

**Type:** Boolean

**Mandatory:** Yes

```
runWebUI=true,
```



### mediaStorage

The configuration for the media storage

**Type:** Object

**Mandatory:** Yes

```
mediaStorage = {
				recordedStreamsStorage="../media",
				{
					description="Default media storage",
					mediaFolder="../media",
				},
			},
```

There are several uses of the media folder:

- Storage of VOD file that is used for `pullStream`
- Location of the created file using `generateLazyPull` command
- Storage of recorded streams using record command



**media Structure Table**

|          Key           |  Type  | Mandatory | Description                              |
| :--------------------: | :----: | :-------: | ---------------------------------------- |
| recordedStreamsStorage | String |   True    | The path of the media folder to be used in record streams |
|      description       | String |   False   | The description of the media storage     |
|      mediafolder       | String |   True    | The path of the media storage folder     |

 **Other optional parameters:**

|          Key          |  Type   | Mandatory | Description                              |
| :-------------------: | :-----: | :-------: | ---------------------------------------- |
|      metaFolder       | string  |   False   | The folder path of the seek and meta files generated |
|      enableStats      | boolean |   False   | The location where the EMS will create statistic, seek and meta files for each of the VOD files. The EMS must be able to write to this folder |
|   clientSideBuffer    | number  |   False   | If true, the EMS will record statistics about each VOD file played. The stats will be kept in a .stats file named the same as the media file stored in the metaFolder and will include the number of times accessed and the amount of bytes served from it |
|     keyframeSeek      | boolean |   False   | The number of seconds the EMS will buffer content when doing VOD playback for an RTMP client |
|    seekGranularity    | number  |   False   | Seeking only occurs at key-frames if true. If false, seeking may occur on inter-frame packets, which may cause garbage to be shown on the client player until a keyframe is reached |
| externalSeekGenerator | boolean |   False   | The fidelity, in seconds, of seeking for the files in this mediaFolder |

See [addStorage](addStorage.html) 



### acceptors

The “acceptors” block is found within the “applications” section named “evostreamms” in the configuration file. Each acceptor protocol used by applications is defined here. Some protocols may require additional parameters.

**Type:** Object

**Mandatory:** Yes

```
-- CLI acceptors
				{
					ip="0.0.0.0",
					port=1112,
					protocol="inboundJsonCli",
					useLengthPadding=true
				},
				{
					ip="0.0.0.0",
					port=7777,
					protocol="inboundHttpJsonCli"
				},
				{
					ip="0.0.0.0",
					port=9999,
					protocol="inboundHttpFmp4" 
				},
				{
					ip="0.0.0.0",
					port=1222,
					protocol="inboundAsciiCli",
					useLengthPadding=true
				},
```

```
-- RTMP and clustering
				{
					ip="0.0.0.0",
					port=1935,
					protocol="inboundRtmp",
				},
				{
					ip="127.0.0.1",
					port=1936,
					protocol="inboundRtmp",
					clustering=true
				},
				{
					ip="127.0.0.1",
					port=1113,
					protocol="inboundBinVariant",
					clustering=true
				},
```

```
-- RTSP
				{
					ip="0.0.0.0",
					port=5544,
					protocol="inboundRtsp",
					--[[
					multicast=
					{
						ip="224.2.1.39",
						ttl=127,
					}
					]]--
				},
```

```
-- LiveFLV ingest
				{
					ip="0.0.0.0",
					port=6666,
					protocol="inboundLiveFlv",
					waitForMetadata=true,
				},
```

```
-- Inbound TCP TS
				{
					ip="0.0.0.0",
					port=9998,
					localStreamName="testTcp",
					protocol="inboundTcpTs",
				},
```

```
-- Inbound UDP TS
				{
					ip="0.0.0.0",
					port=9898,
					localStreamName="testUcp",
					protocol="inboundUdpTs",
				},
```

```
--RTMPS
				{
					ip="0.0.0.0",
					port=4443,
					protocol="inboundRtmp",
					sslKey="/path/to/some/key",
					sslCert="/path/to/some/cert",
				},
```

```
-- JSONMETA
				{
					ip="0.0.0.0",
					port=8100,
					--streamname="test",
					protocol="inboundJsonMeta",
				},
```

```
-- WebSockets JSON Metadata
				{
					ip="0.0.0.0",
					port=8210,
					protocol="wsJsonMeta",
					-- streamname="~0~0~0~"
				},
```

```
-- WebSockets JSON Metadata over SSL
				{
					ip="0.0.0.0",
					port=8433,
					protocol="wssJsonMeta",
					-- streamname="~0~0~0~"
					sslKey="/path/to/some/key",
					sslCert="/path/to/some/cert",
				},
```

```
-- WebSockets FMP4 Fetch
				{
					ip="0.0.0.0",
					port=8410,
					protocol="inboundWSFMP4"
				},
```

```
-- WebSockets over SSL FMP4 Fetch
				--[[
				{
					ip="0.0.0.0",
					port=8420,
					protocol="inboundWSSFMP4",
					sslKey="/path/to/some/key",
					sslCert="/path/to/some/cert",
				},
```



**acceptor Structure Table:**

|   Key    |  Type  | Mandatory | Description                              |
| :------: | :----: | :-------: | ---------------------------------------- |
|    ip    | string |    yes    | The IP where the service is located. A value of 0.0.0.0 means all interfaces and all IPs. |
|   port   | string |    yes    | Port number that the service will listen to. |
| protocol | string |    yes    | The protocol stack handled by the ip:port combination. |

  The following acceptor types are supported by EMS:

| Acceptor Protocol  | Typical IP | Typical Port |    Additional Parameters    | Protocol Stack (Tags) |
| :----------------: | :--------: | :----------: | :-------------------------: | :-------------------: |
|   inboundJsonCli   | 127.0.0.1  |     1112     |      useLengthPadding       |     TCP+IJSONCLI      |
| inboundHttpJsonCli | 127.0.0.1  |     7777     |              -              | TCP+IHTT+H4C+IJSONCLI |
|  inboundAsciiCli   | 127.0.0.1  |     1222     |      useLengthPadding       |      TCP+IASCCLI      |
|    inboundRtmp     |  0.0.0.0   |     1935     |              -              |        TCP+IR         |
|    inboundRtmp     | 127.0.0.1  |     1936     |         clustering          |                       |
| inboundBinVariant  | 127.0.0.1  |     1113     |         clustering          |       TCP+BVAR        |
|    inboundRtsp     |  0.0.0.0   |     5544     |          multicast          |       TCP+RTSP        |
|   inboundLiveFlv   |  0.0.0.0   |     6666     |       waitForMetadata       |       TCP+ILFL        |
|    inboundTcpTs    |  0.0.0.0   |     9998     |       localStreamName       |        TCP+ITS        |
|    inboundUdpTs    |  0.0.0.0   |     9898     |       localStreamName       |        UDP+ITS        |
|    inboundRtmps    |  0.0.0.0   |     4443     |       sslKey, sslCert       |     TCP+ISSL+IRS      |
|  inboundJsonMeta   |  0.0.0.0   |     8100     |         streamname          |                       |
|     wsJsonMeta     |  0.0.0.0   |     8210     |         streamname          |                       |
|    wssJsonMeta     |  0.0.0.0   |     8433     | streamname, sslKey, sslCert |                       |
|   inboundWSFMP4    |  0.0.0.0   |     8410     |              -              |                       |
|   inboundWSSFMP4   |  0.0.0.0   |     8420     |       sslKey, sslCert       |                       |



**Protocol Group Table:**

|    Protocol Group    |   Tag    | Protocol Type          |
| :------------------: | :------: | ---------------------- |
|  Carrier Protocols   |   TCP    | TCP                    |
|         \|\|         |   UDP    | UDP                    |
|  Variant Protocols   |   BVAR   | Bin Variant            |
|         \|\|         |   XVAR   | XML Variant            |
|         \|\|         |   JVAR   | JSON Variant           |
|    RTMP Protocols    |    IR    | Inbound RTMP           |
|         \|\|         |   IRS    | Inbound RTMPS          |
|         \|\|         |    OR    | Outbound RTMP          |
|         \|\|         |    RS    | RTMP Dissector         |
| Encryption Protocols |    RE    | RTMPE                  |
|         \|\|         |   ISSL   | Inbound SSL            |
|         \|\|         |   OSSL   | Outbound SSL           |
|   MPEG-TS Protocol   |   ITS    | Inbound TS             |
|    HTTP Protocols    |   IHTT   | Inbound HTTP           |
|         \|\|         |  IHTT2   | Inbound HTTP2          |
|         \|\|         |   IH4R   | Inbound HTTP for RTMP  |
|         \|\|         |   OHTT   | Outbound HTTP          |
|         \|\|         |  OHTT2   | Outbound HTTP2         |
|         \|\|         |   OH4R   | Outbound HTTP for RTMP |
|    CLI Protocols     | IJSONCLI | Inbound JSON CLI       |
|         \|\|         |   H4C    | HTTP for CLI           |
|         \|\|         | IASCCLI  | Inbound ASCII CLI      |
|    RPC Protocols     |   IRPC   | Inbound RPC            |
|         \|\|         |   ORPC   | Outbound RPC           |
| Passthrough Protocol |    PT    | Passthrough            |

  ​

### autoDASH/HLS/HDS/MSS

if enabled, will automatically create the HTTP streams from the pulled entries. 

**Type:** Object

**Mandatory:** No

```
autoDASH=
			{
				targetFolder="path/to/evo-webroot",
			},
autoHLS=
			{
				targetFolder="path/to/evo-webroot",
			},
autoHDS=
			{
				targetFolder="path/to/evo-webroot",
			},
autoMSS=
			{
				targetFolder="path/to/evo-webroot",
			},
```



**Note:** You can add other parameters associated with the API. See [createDASHStream](api_createDASHStream.html),[createHLSStream](api_createHLSStream.html), [createHDSStream](api_createHDSStream.html), [createMSSStream](api_createMSSStream.html), for parameter lists but below are the parameters that **cannot be modified** using auto:

| Parameter            | Value   |
| -------------------- | ------- |
| keepAlive            | false   |
| cleanupDestination   | true    |
| createMasterPlaylist | false   |
| overwriteDestination | true    |
| playlistType         | rolling |



### authentication

The authentication settings for RTMP and RTSP protocols. For RTMP, another file, `auth.xml`, is required to enable authentication. In addition, a users file, typically named `users.lua`, provides the user names and passwords.

**Type:** Object

**Mandatory:** No

```
authentication=
			{
				rtmp=
				{
					type="adobe",
					encoderAgents=
					{
						"FMLE/3.0 (compatible; FMSc/1.0)",
						"Wirecast/FM 1.0 (compatible; FMSc/1.0)",
						"EvoStream Media Server (www.evostream.com)"
					},
					usersFile="path/to/config/users.lua",
					--verifierUri="http://authserver/verifier.php",
					--token="secretstring",					
				},
				rtsp=
				{
					usersFile="path/to/config/users.lua",
					--authenticatePlay=false,
				}
				--ws=
				--{
				--	token="",
				--},
			},
```

**authentication Structure Table:**

| Protocol  |    Parameter     | Mandatory |         Typical Setting          |
| :-------: | :--------------: | :-------: | :------------------------------: |
|   RTMP    |       type       |   true    |             “adobe”              |
|   \|\|    |  encoderAgents   |   true    |   "FMLE, Wirecast, EvoStream"    |
|   \|\|    |    usersFile     |   true    |      ”../config/users.lua”       |
|   \|\|    |   verifierUri    |   false   | "http://authserver/verifier.php" |
|   \|\|    |      token       |   false   |          "secretstring"          |
|   RTSP    |    usersFile     |   true    |      ”../config/users.lua”       |
|   \|\|    | authenticatePlay |   false   |              false               |
| WebSocket |      token       |           |           "< blank >"            |

**Notes:**

1. Authentication is disabled if the “authentication” block in the “config.lua” file is missing or incomplete. For RTMP protocol, authentication is disabled if the “auth.xml” file is missing or contains a “false” setting. For RTSP protocol, authentication is disabled if **“authenticatePlay**” in the “rtsp” block is omitted or set to “false”.
2. Scripts are available for creating certificates and keys for EMS. Please refer to our GitHub files [here](https://github.com/EvoStream/evostream_addons/tree/master/certificates_and_keys) for details.


###  

### eventLogger

Settings for the server-wide event sinks. 

**Type:** Object

**Mandatory:** No

**A. File**

```
eventLogger=
			{
				--customData=123,
				sinks=
				{
					--[=[
					{
						type="file",
						--[[
						customData=
						{
							some="string",
							number=123.456,
							array={1, 2.345, "Hello world", true, nil}
						},
						]]--
						filename="C:\\EvoStream_2.0_5477\\logs\\events.txt",
						format="text",
						--format="xml",
						--format="json",
						--format="w3c",
						--[[
						timestamp=true,
						appendTimestamp=true,
						appendInstance=true,
						fileChunkLength=43200, -- 12 hours (in seconds)
						fileChunkTime="18:00:00",
						]]--
						enabledEvents=
						{	-- common events enabled by default for eventLogger type "file":
							"inStreamCreated",
							"outStreamCreated",
							-- NOTE: add more events by copying items from the sorted list of VALID EVENTS below
						},
					},
```

**Notes:** 

1. This section is disabled by default. 

2. You can add more events in the list below.

3. The event log files will be stored in the path where EMS logs are configured

   ​

**B. RPC - Evowebservices** 

```
{
						type="RPC",
						url="http://127.0.0.1:4000/evowebservices",
						serializerType="JSON",
						enabledEvents=
						{	-- common events enabled by default for eventLogger type "RPC":
							"inStreamCreated",
							"inStreamClosed",
							"outStreamCreated",
							"outStreamClosed",
							"timerTriggered",
							"hdsMasterPlaylistUpdated",
							"hdsChildPlaylistUpdated",
							"hdsChunkClosed",
							"hdsChunkDeleted",							
							"hlsMasterPlaylistUpdated",
							"hlsChunkClosed",
							"hlsChunkDeleted",									
							"dashPlaylistUpdated",
							"dashChunkClosed",
							"dashChunkDeleted",									
						},
					},
```

**Notes:** 

1. This section is enabled by default. 
2. Replace URL depending on the evowebservices to be used (Node.js or PHP). See evowebservices user guide
3. These are the events are used by EMS webservices, no need to make any changes on this configuration




**C. RPC - WebUI** 

```
{
						type="RPC",
						url="http://127.0.0.1:4100/streams/update-list",
						serializerType="JSON",
						enabledEvents=
						{	-- common events enabled by default for eventLogger type "RPC":
							"inStreamCreated",
							"inStreamClosed",
							"outStreamCreated",
							"outStreamClosed",
							"processStarted",
							"processStopped",
							"recordChunkCreated",
							"recordChunkClosed",
							"webRtcServiceStarted",
							"webRtcServiceStopped",
						},
```

**Note:**

- These events are used by EMS Web UI, no need to make any changes on this configuration




### transcoder

The configuration for the transcoder

**Type:** Object

**Mandatory:** Yes

```
transcoder = {
				scriptPath="..\\emsTranscoder.bat",
				srcUriPrefix="rtsp://localhost:5544/",
				dstUriPrefix="-f flv tcp://localhost:6666/"
			},
```



### mp4BinPath

the path to the mp4 writer executable file

**Type:** String

**Mandatory:** Yes

```
mp4BinPath="..\\evo-mp4writer.exe",
```



### webRTC

the security configuration for the webRTC

**Type:** Object

**Mandatory:** Yes

```
webrtc = {
			sslKey="..\\config\\server.key",
			sslCert="..\\config\\server.cert",
		},
```



### drm

the configuration for the HLS security 

**Type:** Object

**Mandatory:** Yes, if HLS version 5 is used

```
drm={
			type="verimatrix",
			requestTimer=1,
			reserveKeys=10,
			reserveIds=10,
			-- urlPrefix="http://server1.evostream1.com:12684/CAB/keyfile"
			urlPrefix="http://vcas3multicas1.verimatrix.com:12684/CAB/keyfile"
	},
```