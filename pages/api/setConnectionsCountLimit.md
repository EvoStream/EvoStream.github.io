---
title: setConnectionsCountLimit
keywords: api
sidebar: api_sidebar
permalink: setConnectionsCountLimit.html
folder: api
toc: false
---

This interface sets a limit on the number of concurrent connections the EMS will allow.



## API Parameter Table

| **Parameter Name** |  Type   | Mandatory | Default Value | Description                              |
| :----------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
|       count        | integer |   true    |    *null*     | The maximum number of connections allowed on this instance at one time. CLI connections are not affected |



## API Call Template

``` 
setConnectionsCountLimit count=<count>
```



### Sample API Call

```
setConnectionsCountLimit count=500
```

This sets the connection limit to 500.



### Success Response in JSON

``` 
{
"data":{
    “cuurent”:3
    "limit":500
},
"description":"Connection counters",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse
  - current – The current number of concurrent connections
  - limit – The maximum number of concurrent connections
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [getConnectionsCountLimit](getConnectionsCountLimit.html)
- [getConnectionsCount](getConnectionsCount.html)