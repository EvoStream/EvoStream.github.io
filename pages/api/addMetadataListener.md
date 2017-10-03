---
title: addMetadataListener
keywords: api
sidebar: api_sidebar
permalink: addMetadataListener.html
folder: api
toc: false
---

Specifies a new acceptor during runtime



## API Parameter Table

| Parameter Name  |  Type   | Mandatory | Default Value | Description                              |
| :-------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
|      port       | integer |   true    |    *null*     | The port to bind on                      |
|       ip        | string  |   false   |    0.0.0.0    | The IP address to bind on                |
| localStreamName | string  |   false   |   0 ~ 0 ~ 0   | The localStreamName to bind on. The default value (0 ~ 0 ~ 0) means it will be applied on any stream |



## API Call Template

``` 
addMetadataListener port=3535
```



### Sample API Call

``` 
addMetadataListener port=3535 localstreamname=meta
```



### Success Response in JSON

``` 
{
"data":{
"acceptedConnection sCount":0,
"appId":1,
"appName":"evostreamms",
"droppedConnectionsCount":0,
"enabled ":true,
"id":1169,
"ip":"0.0.0.0",
"localStreamName":"meta",
"port":3535,
"protocol":"inboundJsonMeta"
},
"description":"Metadata listener created",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - acceptedConnectionsCount - Number of active connections
  - appId - ID of application using the service
  - appName - Application using the service
  -  droppedConnectionsCount - Number of dropped connections
  - enabled - `true` if the service is enabled, `false` if not
  - id - ID of the service
  - ip - IP address used by the service
  - localStreamName - Name of the stream to which the associated metadata will be sent
  - port - Port used by the service
  - protocol - Protocol used by the service


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [mediaStorage](userguide_confuglua.html#mediastorage)
- [listStorage](listStorage.html)
- [removeStorage](removeStorage.html)

