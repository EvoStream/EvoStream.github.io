---
title: getInboundStreamsCount
keywords: api
sidebar: api_sidebar
permalink: getInboundStreamsCount.html
folder: api
toc: false
---

Returns the number of active inbound streams.



## API Parameter Table

This function has no parameter.



## API Call Template

``` 
getInboundStreamsCount
```



### Success Response in JSON

``` 
{
"data":{
  "inboundStreamsCount":3
  },
  "description":"Active inbound streams",
  "status":"SUCCESS" 
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - inboundStreamsCount - the number of active inbound streams


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [listInboundStreams](listInboundStreams.html)
- [listInboundStreamNames](listInboundStreamNames.html)