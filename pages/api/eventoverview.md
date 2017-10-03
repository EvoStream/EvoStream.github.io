---
title: Events Overview
keywords: events
sidebar: api_sidebar
permalink: eventoverview.html
folder: api
toc: false
---



The EMS Event Notification System provides an extremely powerful way of interacting with the EMS. At the basic level it allows you to easily understand and monitor the usage of your server. You can either poll and parse the log file, or simply subscribe to the HTTP based notifications sent out by the EMS. **The notifications mean that you can have a fully RESTful monitor, gathering metrics in real time!**

Beyond monitoring and gathering metrics, you can **use the Event Notification System to create custom stream processing.** If you want to automatically create HLS/HDS/MSS/DASH streams out of new inbound streams, simply call `createHLSStream`/`createHDSStream`/`createMSSStream`/`createDASHStream` in response to each “new inbound stream” event. If you want to close inbound streams when the associated outbound stream is lost, call `shutdownStream` when you receive an “outbound stream closed” event.



