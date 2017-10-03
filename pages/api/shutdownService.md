---
title: shutdownService
keywords: api
sidebar: api_sidebar
permalink: shutdownService.html
folder: api
toc: false
---



Enable or disable a service.



## API Parameter Table

| **Parameter Name** |  Type   | **Mandatory** | **Default Value** | **Description**       |
| :----------------: | :-----: | :-----------: | :---------------: | --------------------- |
|         id         | integer |     true      |      *null*       | The id of the service |



## API Call Template

``` 
shutdownService id=<serviceId>
```



### Sample API Call

```
shutdownService id=5
```

This shuts down the service with an id of 5.



### Success Response in JSON

```
{
"data":{
    "acceptedConnectionsCount":0,
    "appId":1,
    "appName":"evostreamms",
    "clustering":true,
    "droppedConnectionsCount":0,
    "enabled":true,
    "id":5,
    "ip":"127.0.0.1",
    "port":1936,
    "protocol":"inboundRtmp",
    "sslCert":"",
    "sslKey":""
    },
"description":"Service 5 removed",
"status":"SUCCESS"
}
```

#### JSON Response

The JSON response contains the following details:

- data –  The data to parse.
  - acceptedConnectionsCount – The number of active connections using the service
  - appId – The ID of the application using the service
  - appName – The name of the application using the service
  - droppedConnectionsCount – The number of dropped connections
  - enabled - **true** if the service is enabled, **false** if not
  - id = ID of the service
  - ip = The IP address bound to the service
  - port – The port bound to the service
  - protocol – The protocol bound to the service
  - sslCert – The SSL certificate
  - sslKey – The SSL certificate key
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## **Related Links**

- [createService](createService.html)
- [enableService](enableService.html)
- [listServices](listServices.html)
- [acceptors](userguide_configlua.html#acceptors)