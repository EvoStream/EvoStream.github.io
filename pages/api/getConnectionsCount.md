---
title: getConnectionsCount
keywords: api
sidebar: api_sidebar
permalink: getConnectionsCount.html
folder: api
toc: false
---

Returns the number of active connections.  This includes connections necessary for EMS operations (telnet, license manager, interface, etc.) and all connections opened by streams (RTSP-UDP-RTP ports).



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
getConnectionsCount
```



### Success Response in JSON

``` 
{
"data":{
    "count":3
},
"description":"Active connections count",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse
  - count – The number of active connections
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [setConnectionsCountLimit](setConnectionsCountLimit.html)
- [getConnectionsCountLimit](getConnectionsCountLimit.html)