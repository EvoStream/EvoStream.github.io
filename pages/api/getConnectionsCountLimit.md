---
title: getConnectionsCountLimit
keywords: api
sidebar: api_sidebar
permalink: getConnectionsCountLimit.html
folder: api
toc: false
---



Returns the limit of concurrent connections. This is the maximum number of connections an EMS instance will allow at one time.





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
getConnectionsCountLimit
```



### Success Response in JSON

``` 
{
"data":{
    “cuurent”:3
    "limit":0
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

## **Related Links**

- [setConnectionsCountLimit](setConnectionsCountLimit.html)
- [getConnectionsCount](getConnectionsCount.html)

