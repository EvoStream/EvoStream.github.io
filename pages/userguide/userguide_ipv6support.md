---
title: Using IPv6
keywords: demo
sidebar: userguide_sidebar
permalink: userguide_ipv6support.html
folder: userguide
toc: false
---

EMS can now support IP version 6!

Simply change the IP address binding in config.lua and webconfig .lua to a v6 IP address format, restart EMS then you can now use IPv6!

*Sample changes:*

```
-- RTMP and clustering
				{
					ip="::",
					port=1935,
					protocol="inboundRtmp",
				},
				{
					ip="::",
					port=1936,
					protocol="inboundRtmp",
					clustering=true
				},
				{
					ip="::",
					port=1113,
					protocol="inboundBinVariant",
					clustering=true
				},
```

**Notes:**

- Replace **127.0.0.1** to **::**
- Use **[ipv6:port]** when using ipv6 in URLs 
- EMS resolves address "**localhost**" into "**127.0.0.1**" 
- If an EMS services is bound to a v6 address,  your command should also use v6
- When performing a `pullStream` command on a v6 address please ensure that there is a service bound to a corresponding v6 address

