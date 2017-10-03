---
title: listServices
keywords: api
sidebar: api_sidebar
permalink: listServices.html
folder: api
toc: false
---

Returns the list of available services.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listServices
```



### Success Response in JSON

``` 
{
"data":[
    {
    "acceptedConnectionsCount":1,
    "appId":1,
    "appName":"evostreamms",
    "droppedConnectionsCount":0,
    "enabled":true,
    "id":1,
    "ip":"127.0.0.1",
    "port":1112,
    "protocol":"inboundJsonCli",
    "sslCert":"",
    "sslKey":"",
    "useLengthPadding":true
    },
    --content removed for clarity
    {
    --content removed for clarity
    "protocol":"inboundLiveFlv",
    "sslCert":"",
    "sslKey":"",
    "waitForMetadata":true
    },
    --content removed for clarity
    ],
"description":"Available services",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – Provides the following information for each protocol
  - acceptedConnectionsCount – The number of active connections using the service
  - appId – The ID of the application linked to the service
  - appName – The name of the application linked to the service
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
- [enableService](enableService.html)
- [shutdownService](shutdownService.html)
- [acceptors](userguide_configlua.html#acceptors)