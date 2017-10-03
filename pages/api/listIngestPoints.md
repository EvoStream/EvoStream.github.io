---
title: listIngestPoints
keywords: api
sidebar: api_sidebar
permalink: listIngestPoints.html
folder: api
toc: false
---



Lists the currently available Ingest Points.





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listIngestPoints
```



### Success Response in JSON

``` 
{
"data":{
    "privateStreamName":"testIngestPoint",
    "publicStreamName":"testPublicStreamName"
},
"description":"Available ingest points",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data– List of pairs
  - privateStreamName –The private stream name which was set
  - publicStreamName – The public stream name which was set
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasIngestPoints** in config.lua should be **TRUE**


------

## Related Links

- [hasIngestPoints](userguide_configlua.html#hasingestpoints)


- [createIngestPoint](createIngestPoint.html)
- [removeIngestPoint](removeIngestPoint.html)
- [ingestpoints.xml](userguide_ingestpoints.html)