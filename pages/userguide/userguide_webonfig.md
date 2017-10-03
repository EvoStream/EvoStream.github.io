---
title: webconfig.lua
keywords: webconfig
sidebar: userguide_sidebar
permalink: userguide_webconfig.html
folder: userguide
toc: true
---

This is the main configuration file of the EvoStream Web Server (EWS). This file sets the locations of important web server files/folders such as the web root folder, server key & certificate, white list, black list, logs, etc. This is where other web server settings are defined, including HTTP port, group name aliasing, SSL mode, connection/memory limits, mime types, etc.

**Contents:**

- configuration – This is the entire structure for all configuration needed by the EWS Server.

```
configuration =
  {
      logAppenders
      {
          -- content removed for clarity
      },
      applications =
      {
          -- content removed for clarity
      }
}
```

**webServer Configuration Structure Table:**

|     Key      |  Type  | Mandatory | Description                              |
| :----------: | :----: | :-------: | ---------------------------------------- |
| logAppenders | object |    yes    | Will hold a collection of log appenders. Each log message will be sent to each of the log appenders enumerated in this configuration section. |
| applications | object |    yes    | Will hold a collection of loaded applications. Besides that, it will also hold some other values. |

When the web server starts, the following sequence of operations is performed:

- The `logAppenders` value is read. This is where all log appenders are configured and brought up to running state. Depending on the collection of your log appenders, you may (not) see further log messages.

- The `applications` valueis taken into consideration. After this stage completes, all the applications are fully functional and the server is online and ready to do stuff.

  ​

## logAppenders

the configuration for the web server logs and log files

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
			type="delayedFile",
			level=6,
			fileName="..\\logs\\evo-webserver",
			newLineCharacters="\n",
			fileHistorySize=100,
			fileLength=1024*1024,
			singleLine=true
		},
	},
```
This section contains a list of log appenders. The entire collection of appenders listed in this section is loaded inside the logger at config-time. All log messages will be than passed to all these log appenders. Depending on the log level, an appender may (or may not) log the message. “Logging” a message means “saving” it on the specified “media” (in the example below we have a console appender and a file).

**webServer logAppenders Structure Table:**

|        Key        |  Type   | Mandatory | Description                              |
| :---------------: | :-----: | :-------: | ---------------------------------------- |
|       name        | string  |    yes    | The name of the appender. It is usually used inside pretty print routines. |
|       type        | string  |    yes    | The type of the appender. It can be “console”, “coloredConsole” or “file”. Types “console” and “coloredConsole” will output to the console. The difference between them is that “coloredConsole” will also apply a color to the message, depending on the log level. Quite useful when eye-balling the console. Type “file” log appender will output everything to the specified file. |
|       level       | number  |    yes    | The log level used. The values are presented just below. Any message having a log level less or equal to this value will be logged. The rest are discarded. (**Log levels:** 0 FATAL, 1 ERROR, 2 WARNING, 3 INFO, 4 DEBUG, 5 FINE, 6 FINEST, -1 disable logs) |
|     fileName      | string  |    yes    | If the type of appender is a file, this will contain the path of the file. |
| newLineCharacters | string  |    no     | Newline character used in the file appender. |
|  fileHistorySize  | number  |    no     | The maximum number of log files to be retained. The oldest log file will be deleted first if this number is exceeded. |
|    fileLength     | number  |    no     | Buffer size of the file appender.        |
|    singleLine     | boolean |    no     | If yes, multi-line log messages are merged into one line. |



## applications

This section is where all the applications inside the server are placed. It holds the attributes of each application that the server will use to launch them. Each application may have specific attributes that it requires to execute its own functionality.



### rootDirectory

The folder containing applications subfolders. If this path begins with a “/” or “" (depending on the OS), then is treated as an absolute path. Otherwise is treated as a path relative to the run-time directory (the place where you started the server).

```
rootDirectory="./",
```

**Type:** String

**Mandatory:** Yes



### name

the name of the web server application

```
name="webserver",
```

**Type:** String

**Mandatory:** Yes



### description

the description of the web server application

```
description="Built-In Web Server",
```

**Type:** String

**Mandatory:** No

### port

the port where the web server listens

```
port=8888,
```

**Type:** Number

**Mandatory:** Yes



### emsPort

the port where the web server communicates with the ems

```
emsPort=1113,
```

**Note:** should match config.lua's **inboundBinVariant** acceptor

**Type:** Number

**Mandatory:** Yes



### bindToIP

the specific IP to use when the host has multiple Ethernet cards

```
bindToIP="",
```

**Type:** String

**Mandatory:** No



### sslMode

the configuration of the ssl when using the web server

```
sslMode="disabled", 
```

**Type:** String

**Mandatory:** No

**Accepted values:**

- disabled - uses HTTP

- enabled - forces use of HTTPS

- automatic - checks for HTTP first, falls back to HTTPS otherwise




### sslKeyFile

the path of the SSL key file

```
sslKeyFile="..\\config\\server.key",
```

**Type:** String

**Mandatory:** No



### sslCertFile

the path of the SSL certificate file

```
sslCertFile="..\\config\\server.cert",
```

**Type:** String

**Mandatory:** No



### useIPV6

enables use of IP version 6 if true

```
useIPV6=false,
```

**Type:** Boolean

**Mandatory:** No



### enableIPFilter

if true, will read the blacklist and whitelist files

```
enableIPFilter=false,
```

**Type:** Boolean

**Mandatory:** No



### whitelistFile

the path of the whitelist file

```
whitelistFile="..\\config\\whitelist.txt",
```

**Type:** String

**Mandatory:** No



### blacklistFile

the path of the blacklist file

```
blacklistFile="..\\config\\blacklist.txt",
```

**Type:** String

**Mandatory:** No



### hasGroupNameAliases

enables or disables group name aliases. This protects HTTP streaming variants (HLS, HDS, MSS, DASH, media files) from direct access

```
hasGroupNameAliases=false,
```

**Type:** Boolean

**Mandatory:** No



### webRootFolder

the location of the webroot folder

```
webRootFolder="..\\evo-webroot",
```

**Note:** take note of the ports being used when using other webroot

**Type:** String

**Mandatory:** Yes



### enableRangeRequests

will enable trigger to use the seek bar in forwarding or rewinding streams

```
enableRangeRequests=true,
```

**Type:** Boolean

**Mandatory:** No



### mediaFileDownloadTimeout

a media file download session is ended when there is no subsequent request after X seconds

```
mediaFileDownloadTimeout=30,
```

**Type:** Number

**Mandatory:** Yes



### supportedMimeTypes

this section is used to indicate file extension associations to mime types.

```
	supportedMimeTypes=
			{
				-- non-streaming
				{	
					extensions="mp4,mp4v,mpg4",
					mimeType="video/mp4",
					streamType="",
					isManifest=false,
				},
				{
					extensions="flv",
					mimeType="video/x-flv",
					streamType="",
					isManifest=false,
				},
				-- streaming
				{
					extensions="m3u,m3u8",
					mimeType="audio/x-mpegurl",
					streamType="hls",
					isManifest=true,
				},
				{
					extensions="ts",
					mimeType="video/mp2t",
					streamType="hls",
					isManifest=false,
				},
				{
					extensions="aac",
					mimeType="audio/aac",
					streamType="hls",
					isManifest=false,
				},
				{
					extensions="f4m",
					mimeType="application/f4m+xml",
					streamType="hds",
					isManifest=true,
				},
				{
					extensions="ismc,isma,ismv",
					mimeType="application/octet-stream",
					streamType="mss",
					isManifest=true,
				},
				{
					extensions="fmp4",
					mimeType="video/mp4",
					streamType="mss",
					isManifest=false,
				},
				{
					extensions="mpd",
					mimeType="application/dash+xml",
					streamType="dash",
					isManifest=true,
				},
				{
					extensions="m4s",
					mimeType="video/mp4",
					streamType="dash",
					isManifest=false,
				},
				{ -- needed for supporting adobe player's crossdomain.xml
					extensions="xml",
					mimeType="application/xml",
					streamType="",
					isManifest=false,
				},
			},
```

**webServer supportedMime Types Structure Table:**

|    Key     |  Type   | Mandatory | Description                              |
| :--------: | :-----: | :-------: | ---------------------------------------- |
| extensions | string  |    yes    | File extensions to be associated.        |
|  mimeType  | string  |    yes    | The mime type associated with the specified file extensions. |
| streamType | string  |    no     | The type of HTTP stream.                 |
| isManifest | boolean |    no     | Indicates if a file is a manifest used with the HTTP streaming variant. |



### includeResponseHeaders

this section indicates additional headers to be included in the response

```
includeResponseHeaders=
			{
				{
					header="Access-Control-Allow-Origin",
					content="*",
					override=true,
				},
				{
					header="User-Agent",
					content="Evostream",
					override=false,
				},
			},
```

**webServer includeResponseHeaders Structure Table:**

| Key      | Type    | Mandatory | Description                              |
| -------- | ------- | --------- | ---------------------------------------- |
| header   | string  | yes       | The response header.                     |
| content  | string  | yes       | The value particular to the response header. |
| override | boolean | No        | Indicates if the header should be overridden if the existing header has this already included. |



### apiProxy

Proxy authentication provides a way to secure the HTTP based EMS API. All API commands will first pass through the EWS, which will validate the provided username and password, and then pass the commands to the EMS for processing. API command return values will be routed back to the caller appropriately.

To enable Proxy Authentication you will open the *webconfig.lua* config file and uncomment the “apiProxy” section near the bottom of the file.

```
apiProxy=
			{
				authentication="basic", -- none, basic			
				pseudoDomain="<domain>",
				address="127.0.0.1",
				port=7777,
				userName="<username>",
				password="<password>",
			},
```
**apiProxy Structure Table:**

|      Key       |  Type  | Mandatory | Description                              |
| :------------: | :----: | :-------: | ---------------------------------------- |
| authentication | object |    yes    | The type of authentication. Currently, there are only 2 available values: “basic” which is basic HTTP authentication that uses a username and password; and “none” which disables authentication. |
|  pseudoDomain  | object |    yes    | The domain name or folder                |
|    address     | number |    yes    | The address using the inboundHTTPJsonCLI |
|      port      | number |    yes    | Port, referring to the config.lua’s acceptors for inboundHTTPJsonCLI |
|    userName    | string |    No     | Basic authentication username            |
|    password    | string |    No     | Password for the userName                |

See [Using API Proxy Authentication]().



### auth

The authentication settings for the EMS Web UI. This is disabled for non-Amazon EMS packages.

```
auth=
{
	{
		domain="EMS_Web_UI", --the domain folder
     	 digestFile="../evo-webroot/EMS_Web_UI/settings/passwords/.htdigest", --relative path to digest file
     	 enable=false,
	},
},
```
To enable the EMS Web UI Authentication you will open the webconfig.lua configuration file and change “enable” value to “true”.

|    Key     |  Type   | Mandatory | Description                              |
| :--------: | :-----: | :-------: | ---------------------------------------- |
|   domain   | object  |    yes    | The domain name or folder                |
| digestFile | object  |    yes    | The relative path to digest file         |
|   enable   | boolean |    yes    | Tells if the authentication is enabled or disabled |

If enabled, the Authentication window will open if the EMS Web UI is accessed.