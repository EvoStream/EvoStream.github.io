---
title: WebSocket Overview
keywords: websocket
sidebar: html5players_sidebar
permalink: html5players_wsoverview.html
folder: html5players
toc: false
---

HTML5 Web Socket technology provides socket connections between a web browser and a server, as opposed to the traditional request/response model of HTTP. With HTTP, for the server to send data the client has to initiate the communication via a request and the server will then send back a response. HTTP incurs considerable overhead which makes it not ideal for low latency applications.

With Web Sockets, a persistent connection between the client (web browser) and the server is established and either of them can start sending data anytime, thus eliminating the dependency on the client-side to initiate the request. This results in a low-latency connection providing a more “real-time” data delivery.

The EMS utilizes this technology to provide the following functions:

- Metadata Outbound Push – transmits Metadata to a browser as it is received.
- Metadata Ingest – accepts incoming Metadata.
- FMP4 Player – an acceptor which transmits a fragmented MP4 (FMP4) stream.

