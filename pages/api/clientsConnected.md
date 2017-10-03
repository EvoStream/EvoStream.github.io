---
title: clientsConnected
keywords: api
sidebar: api_sidebar
permalink: clientsConnected.html
folder: api
toc: false
---



Returns all the clients currently utilizing the EMS.



## API Parameter Table

| **Parameter Name** |  Type  | **Mandatory** | **Default Value** | **Description**                          |
| :----------------: | :----: | :-----------: | :---------------: | ---------------------------------------- |
|  localStreamName   | string |     false     |      *null*       | The name of the particular stream. If this parameter is specified, the command will return the number of clients connected which use that stream |



## API Call Template

``` 
clientsConnected
```



### Sample API Call

```
clientsConnected
```

```
clientsConnected localStreamName=testpullStream
```



### Success Response in JSON

``` 
{
"data":{
    "outboundCount":3
},
"description":"EMS outbound client connections count",
"status":"SUCCESS"
}
```

```
{
"data":{
		"outboundCount":1
},
"description":"EMS outbound client connections count for the corresponding localstreamname: testpullStream",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse.
  - outboundCount – The number of client connections
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.


------

## Related Links

- [httpClientsConnected](httpClientsConnected.html)

