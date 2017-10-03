---
title: createService
keywords: api
sidebar: api_sidebar
permalink: createService.html
folder: api
toc: false
---



Creates a new service. 



## API Parameter Table

| **Parameter Name** |  Type  | **Mandatory** | **Default Value** | **Description**                    |
| :----------------: | :----: | :-----------: | :---------------: | ---------------------------------- |
|         ip         | string |     true      |      *null*       | The IP address to bind on          |
|        port        | string |     true      |      *null*       | The port to bind on                |
|      protocol      | string |     true      |      *null*       | The protocol stack name to bind on |
|      sslCert       | string |     false     |      *null*       | The SSL certificate to be used     |
|       sslKey       | string |     false     |      *null*       | The SSL certificate key to be used |



## API Call Template

``` 
createService ip=<ipAddress> port=<portNumber> protocol=<protocolName>
```



### Sample API Call

```
createService ip=0.0.0.0 port=9556 protocol=inboundRtmp
```

This will create a service called **inboundRtmp** which will use port **9556** and can be accessed by **0.0.0.0** IP.



### Success Response in JSON

```
{
"data":{
    "acceptedConnectionsCount":0,
    "appId":1,
    "appName":"evostreamms",
    "droppedConnectionsCount":0,
    "enabled":true,
    "id":974,
    "ip":"0.0.0.0",
    "port":1234,
    "protocol":"inboundRtmp"
    },
"description":"Service created",
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
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- The created service will not be added in config.lua


------

## Related Links

- [enableService](enableService.html)
- [listServices](listServices.html)
- [shutdownService](shutdownService.html)
- [acceptors](userguide_configlua.html#acceptors)