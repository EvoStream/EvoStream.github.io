---
title: User Defined Variables
keywords: demo
sidebar: userguide_sidebar
permalink: userguide_userdefined.html
folder: userguide
toc: false
---

While the EMS provides an extensive set of API functions, there may be times where the variables provided are not sufficient, or where you may need extra information to be associated with individual streams. To support these needs, the EMS API implements *User Defined Variables*. User Defined Variables can be used with any API function where information is maintained by the EMS (i.e. pulling a stream, creating a timer, starting a transcode job, etc.).

To specify a User Defined Variable, you simply need to append an underscore (`_`) to the beginning of your variable name. The User Defined variables are reported back whenever you get information about the command: listStreams, listConfig, Event Notifications, etc.

Some common use cases for User Defined Variables are as follows:

```
setTimer value=120 _streamName=MyStreamsetTimer value=120 _streamID=5

```

Setting a timer to stop a stream after a set period of time

```
pullstream uri=rtmp://192.168.1.5/live/myStream localstreamname=test1 _myID=5 _myName=secretSquirrel

```

These commands will fire a timer event after 120 seconds with the set stream name or stream id respectively.

1. Attach a custom identifier to a local stream

   ```
     pushstream uri=rtmp://192.168.1.5/live/myStream localstreamname=test1 _myID=5 _myName=secretSquirrel

   ```

Set a custom value on a pushed stream