---
title: createIngestPoint
keywords: api
sidebar: api_sidebar
permalink: createIngestPoint.html
folder: api
toc: false
---



Creates an RTMP ingest point, which mandates that streams pushed into the EMS have a target stream name which matches one Ingest Point `privateStreamName`.



## API Parameter Table

|  Parameter Name   |  Type  | Mandatory | Default Value | Description                              |
| :---------------: | :----: | :-------: | :-----------: | ---------------------------------------- |
| privateStreamName | string |   true    |    *null*     | The name that RTMP Target Stream Names must match |
| publicStreamName  | string |   true    |    *null*     | The name that is used to access the stream pushed to the `privateStreamName`. The `publicStreamName` becomes the streams `localStreamName` |



## API Call Template

``` 
createIngestPoint privateStreamName=<theIngestPoint> publicStreamName=<publicStreamName>
```



### Sample API Call

``` 
createIngestPoint privateStreamName=testIngestPoint publicStreamName=testPublicStreamName
```



### Success Response in JSON

``` 
{
"data":{
    "privateStreamName":"testIngestPoint",
    "publicStreamName":"testPublicStreamName"
},
"description":"Ingest point created",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - privateStreamName –The privateStreamName which was set
  - publicStreamName – The publicStreamName which was set
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasIngestPoint** is config.lua should be set to **TRUE**
- Use the `publicStreamName` to play the stream

------

## Related Link

- [hasIngestPoints](userguide_configlua.html#hasingestpoints)
- [listIngestPoints](listIngestPoints.html)
- [removeIngestPoint](removeIngestPoint.html)
- [ingestpoints.xml](userguide_ingestpoints.html)
