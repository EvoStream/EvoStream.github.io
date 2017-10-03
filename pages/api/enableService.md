---
title: enableService
keywords: api
sidebar: api_sidebar
permalink: enableService.html
folder: api
toc: false
---



Enable or disable a service.



## API Parameter Table

| **Parameter Name** |  Type   | **Mandatory** | **Default Value** | **Description**                          |
| :----------------: | :-----: | :-----------: | :---------------: | ---------------------------------------- |
|         id         | integer |     true      |      *null*       | The id of the service                    |
|       enable       | boolean |     true      |      *null*       | **1** to enable, **0** to disable service |



## API Call Template

``` 
enableService id=<serviceId> enable=<enableValue>
```



### Sample API Call

```
enableService id=5 enable=0
```

This **disables** the service with an id of 5.

```
enableService id=5 enable=1
```

This **enables** the service with an id of 5.



### Success Response in JSON

```
{
          "data": {
                    "data": {
                              "acceptedConnectionsCount": 3,
                              "appId": 1,
                              "appName": "evostreamms",
                              "droppedConnectionsCount": 0,
                              "enabled": true,
                              "id": 5,
                              "ip": "0.0.0.0",
                              "port": 9556,
                              "protocol": "inboundRtmp,
                              "sslCert": "",
                              "sslKey": ""
                    },
                    "description": "Status changed",
                    "status": "SUCCESS"
          }
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
  - sslCert – The SSL certificate (for some protocols only)
  - sslKey – The SSL certificate key (for some protocols only)
  - useLengthPadding – **true** if padding is enabled, **false** if not (for some protocols only)
  - waitForMetadata – **true** if metadata is required, **false** if not (for some protocols only)
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [createService](createService.html)
- [listServices](listServices.html)
- [shutdownService](shutdownService.html)
- [acceptors](userguide_configlua.html#acceptors)