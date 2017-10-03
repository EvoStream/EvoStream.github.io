---
title: WebSocket Metadata
keywords: websocket
sidebar: html5players_sidebar
permalink: html5players_wsmetadata.html
folder: html5players
toc: false
---

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

**Where:**

​	ip - the IP where the service is located. A value of 0.0.0.0 means all interfaces and all IPs

​	port - port number that the service will listen to

​	protocol - the protocol stack handled by the ip:port combination

​	streamname - the streamname where the metadata will be sent. if disabled, will match to all incoming streams



## Sending Metadata

- **Using GET**

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


​	For the FMP4 Player, a Web Sockets acceptor is defined in `config.lua`:

​		

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

For convenience, a demo page is already available upon installation: `..\evo-webroot\demo\evowsvideo.html` Another option for playback is using http://ers.evostream.com:5050/demo/evoplayersv5.html. 