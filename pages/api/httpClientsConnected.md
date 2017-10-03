---
title: httpClientsConnected
keywords: api
sidebar: api_sidebar
permalink: httpClientsConnected.html
folder: api
toc: false
---



Returns all the clients which are currently utilizing the EWS.



## API Parameter Table

| **Parameter Name** |  Type  | **Mandatory** | **Default Value** | **Description**                          |
| :----------------: | :----: | :-----------: | :---------------: | ---------------------------------------- |
|     groupName      | string |     false     |      *null*       | The name of the particular group. If this parameter is specified, the command will return the number of clients connected which are playing streams falling under that group |



## API Call Template

``` 
httpClientsConnected
```



### Sample API Call

```
httpClientsConnected
```

```
httpClientsConnected groupName=MyGroupStream
```



### Success Response in JSON

``` 
{
"data":{
    "groupName":"",
    "httpStreamingSessionsCount":2
},
"description":"Number of clients connected to Evostream Web Server",
"status":"SUCCESS"
}
```

```
{
"data":{
    "groupName":"MyGroupStream",
    "httpStreamingSessionsCount":1
},
"description":"Number of clients connected to Evostream Web Server under groupname: MyGroupStream",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse.
  - groupName – The group name to which the clients are connected to
  - httpStreamingSessionsCount – The number of client connections
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [clientsConnected](clientsConnected.html)