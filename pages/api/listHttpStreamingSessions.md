---
title: listHttpStreamingSessions
keywords: api
sidebar: api_sidebar
permalink: listHttpStreamingSessions.html
folder: api
toc: false
---

This command lists all currently active HTTP streaming sessions.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listHttpStreamingSessions
```



### Success Response in JSON

``` 
{
  "data": [
    {
    "clientIP": "127.0.0.1",
    "elapsedTime": 33,
    "sessionId": 1,
    "startTime": "2014-12-17T18-31-13",
    "targetFolder": "C:\\xampp\\htdocs\\hls_group\\mystream"
    }
  ],
  "description":"Currently open HTTP streaming sessions",
  "status":"SUCCESS"
}
```



#### JSON Response

- data– The data to parse
  - clientIP – The IP address of the connected client
  - sessionId – An internal ID for the session
  - startTime – The timestamp when the session started
  - elapsedTime – The number of seconds since the session started
  - targetFolder – The current folder used as the source for HTTP streaming

- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## **Related Links**

- [httpClientsConnected](httpClientsConnected.html)