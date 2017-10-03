---
title: ingestpoints.xml
keywords: ingestpoints
sidebar: userguide_sidebar
permalink: userguide_ingestpoints.html
folder: userguide
toc: false
---

The file where the ingest points are saved. This should be set to true when ingest point will be used.

```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
</MAP>
```



If `hasIngestPoints` is set to true in config.lua and an ingest is ceated on API call, it will be listed in this file.

**API call:**

```
createIngestPoint privateStreamName=theIngestPoint1 publicStreamName=Stream1

createIngestPoint privateStreamName=theIngestPoint2 publicStreamName=Stream2

createIngestPoint privateStreamName=theIngestPoint3 publicStreamName=Stream3

createIngestPoint privateStreamName=theIngestPoint4 publicStreamName=Stream4

createIngestPoint privateStreamName=theIngestPoint5 publicStreamName=Stream5
```



**ingestpoints.xml**

```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
    <STR name="theIngestPoint1">Stream1</STR>
    <STR name="theIngestPoint2">Stream2</STR>
    <STR name="theIngestPoint3">Stream3</STR>
    <STR name="theIngestPoint4">Stream4</STR>
    <STR name="theIngestPoint5">Stream5</STR>
</MAP>
```