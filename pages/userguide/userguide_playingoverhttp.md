---
title: Play Over HTTP
keywords: http
sidebar: userguide_sidebar
permalink: userguide_playoverhttp.html
folder: userguide
toc: true
---

The EMS now support playing your stream over HTTP! 

You stream directly in browser or add your stream in video tags.

**Note:** 

The behavior of this feature depends on the browser. It might or might not play well on some browsers.



## How To

### Check entry in Config.lua

```
{
	ip="0.0.0.0",
	port=9999,
	protocol="inboundHttpFmp4"
},
```

**Note:** You can change the port you want to use



### Play in Browser

Just place the URL below in your browser, hit **Enter**

```
http://<IPofEMS:port>/<localStreamName>
```

```
http://127.0.0.1:9999/myStream
```

![](images/userguide/playoverhttp.jpg)



### Use in Video Tags

Simply place the URL inside video tags if you want to add your stream in your HTML page

```
<video src="http://<IPofEMS:port>/localStreamName"></video>
```