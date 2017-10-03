---
title: listStreamsIds
keywords: api
sidebar: api_sidebar
permalink: listStreamsIds.html
folder: api
toc: false
---

Get a list of IDs for every **active** stream.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listStreamsIds
```



### Success Response in JSON

``` 
{
"data":[205,206,207],
"description":"Available stream IDs",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – Contains an array of IDs (integers) for the active streams
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- ID's may change overtime


------

## Related Links

- [listStreams](api_listStreams.html)