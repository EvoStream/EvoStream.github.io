---
title: Accessing the Run-Time API
keywords: API
sidebar: userguide_sidebar
permalink: userguide_telnet.html
folder: userguide
toc: true
---

You can also connect to EMS using the telnet and HTTP request aside from the EMS Web UI. Below are the ways on how to connect to EMS.



## Manual Command Line

**Pre-requisite in Windows OS**

Telnet may need to be enabled using Windows OS. To enabled the feature, go to the *Control Panel -> Programs -> Turn Windows Features on and off*. Turn **ON** the Telnet Client program.

![](images/userguide/enabletelnet.jpg)

Please also note that on Windows, the default telnet behavior will need to be changed. The local echo and new line mode should be set for proper behavior. Once telnet is launched, exit the telnet session by typing `CTRL`+`]`. Then enter the following commands:

```
set localecho
set crlf
```

To return to the Windows telnet session, press **Enter** or **Return** key.



### ASCII CLI

This ASCII-based interface is often the first interface used by users. It can be accessed easily through the telnet application (available on all operating systems) or through common scripting languages.

Configuration in config.lua:

```
{
	ip="0.0.0.0",
	port=1222,
	protocol="inboundAsciiCli",
	useLengthPadding=true
},
```

To access the API via the telnet interface, a telnet application will need to be launched on the same computer that the EMS is running on. The command to open telnet from a command prompt should look something like the following:

```
telnet localhost 1222
```

Once the telnet session is established, type out the desired commands which will be immediately executed on the server after the Enter/Return key is pressed.

An example of a command request and response from a telnet session would be the following:

**Request:**

```
version
```

**Response:**

```
Command entered successfully!
Version

    banner: EvoStream Media Server (www.evostream.com) version 1.7.1 build 4491
with hash: 64b305253110afc4acd5aeaf87f0a0b0f9b53526 on branch: origin/release/1.
7.0.1 - PacMan|m| - (built for Windows-8.1-x86_64 on 2016-06-17T09:33:23.000)
    buildDate: 2016-06-17T09:33:23.000
    buildNumber: 4491
    codeName: PacMan|m|
    releaseNumber: 1.7.1
```



### ASCII JSON CLI

Accessing the API over the same Telnet interface, but by using the port **1112** will yield the same results as the ASCII CLI, but the results will all be returned formatted in JSON. This is very convenient for CGI and BASH scripting against the EMS API.

**Please note that the first character returned by the JSON response is the LENGTH of the JSON payload, allowing you to allocate properly sized structures at runtime.**

Configuration in config.lua:

```
{
	ip="0.0.0.0",
	port=1112,
	protocol="inboundJsonCli",
	useLengthPadding=true
},
```

An example of a command request/response from a telnet session would be the following:

```
telnet localhost 1112

```

An example of a command request and response from a telnet session would be the following:

**Request:**

```
version
```

**Response:**

```
{"data":{"banner":"EvoStream Media Server (www.evostream.com) version 1.7.1 build 4491 with hash:64b305253110afc4acd5aeaf87f0a0b0f9b53526 on branch: origin\/release\/1.7.0.1 - PacMan|m| - (built for Windows-8.1-x86_64 on 2016-06-17T09:33:23.000)","branchName":"origin\/release\/1.7.0.1","buildDate":"2016-06-17T09:33:23.000","buildNumber":"4491","codeName":"PacMan|m|","hash":"64b305253110afc4acd5aeaf87f0a0b0f9b53526","releaseNumber":"1.7.1"},"description":"Version","status":"SUCCESS"}
```



## HTTP JSON CLI

To access the API via the HTTP interface, simply make an HTTP request on the server using any browser with the command to be executed. By default, the port used for these HTTP requests is **7777**. The HTTP interface port can be changed in the main configuration file used by the EMS (config.lua).

Configuration in config.lua:

```
{
	ip="0.0.0.0",
	port=7777,
	protocol="inboundHttpJsonCli"
},
```

A general HTTP format request would be the following:

```
http://[EMS_IP]:7777/[API]
```

An example of a command request and response from an HTTP session would be the following:

**Request:**

```
http://localhost:7777/version

```

**Response:**

```
{"data":{"banner":"EvoStream Media Server (www.evostream.com) version 1.7.1 build 4491 with hash:64b305253110afc4acd5aeaf87f0a0b0f9b53526 on branch: origin\/release\/1.7.0.1 - PacMan|m| - (built for Windows-8.1-x86_64 on 2016-06-17T09:33:23.000)","branchName":"origin\/release\/1.7.0.1","buildDate":"2016-06-17T09:33:23.000","buildNumber":"4491","codeName":"PacMan|m|","hash":"64b305253110afc4acd5aeaf87f0a0b0f9b53526","releaseNumber":"1.7.1"},"description":"Version","status":"SUCCESS"}
```



### Using  Multiple Parameters

All of the API functions are available via HTTP, but the request must be formatted slightly different if parameters are included. To make an API call over HTTP, the parameters to be used should be in base64 format.

```
http://[EMS_IP]:7777/[API]?params=([base64_encoded_parameters])
```



#### Converting Parameters to base64 format

Sampling a `pullstream` command:

```
pullStream uri=rtsp://localhost:5544/vod/mp4.bunny.mp4 localStreamName=bunny keepAlive=1 forceTcp=1
```

1. Type in the parameters first: `uri=rtsp://localhost:5544/vod/mp4.bunny.mp4 localStreamName=bunny keepAlive=1 forceTcp=1`

2. Convert the parameters using a base64 encoder: 

   Encode [here](https://www.base64encode.org/).

   **Converted parameter:**

   ```
   dXJpPXJ0c3A6Ly9sb2NhbGhvc3Q6NTU0NC92b2QvbXA0LmJ1bm55Lm1wNCBsb2NhbFN0cmVhbU5hbWU9YnVubnkga2VlcEFsaXZlPTEgZm9yY2VUY3A9MQ==
   ```

3. The corresponding request in HTTP format would be:

   ```
   http://localhost:7777/pullstream?params= dXJpPXJ0c3A6Ly9sb2NhbGhvc3Q6NTU0NC92b2QvbXA0LmJ1bm55Lm1wNCBsb2NhbFN0cmVhbU5hbWU9YnVubnkga2VlcEFsaXZlPTEgZm9yY2VUY3A9MQ==
   ```



- **Base64**

A group of similar binary-to-text encoding schemes that represent binary data in an ASCII string format by translating it into a radix-64 representation. There are available base64 encoders online to get the encoded result.

- **PHP and JavaScript**

PHP and JavaScript functions are also provided. These functions simply wrap the HTTP interface calls and can be found in the EMS Web UI directory.

- **Securing the API**

By default, the ASCII API is protected, and access from any outside computer is prohibited. This can of course be modified within the config.lua file, but keeping this restriction is recommended for maintaining server security.

The HTTP based API is also restricted by default to only local access. However, unlike the ASCII API interface, there are often good reasons to expose the HTTP API. To secure the HTTP based API in this case, you will enable Proxy Authentication on the EWS (details found in the EWS section of this doc). This will enforce that a valid username and password be provided for each and every API call made, ensuring on authorized access to the EMS API.