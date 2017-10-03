---
title: listMetadataListeners
keywords: api
sidebar: api_sidebar
permalink: listMetadataListeners.html
folder: api
toc: false
---

Returns the list of all metadata listeners created either through the config.lua or through the `addMetadataListener` API.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listMetadataListeners
```



### Success Response in JSON

``` 
{
"data":{
"listeners":[
     {
      "acceptor":{
        "acceptedConnectionsCount":0,
          "acceptor":{
            "acceptedConnectionsCount":0,
            "acceptor":{
              "acceptedConnectionsCount":0,
              "appId":1,
              "appName":"evostreamms",
              "droppedConnectionsCount":0,
              "enabled":true,
              "id":1169,
              "ip":"0.0.0.0",
              "localStreamName":"meta",
              "port":3535,
              "protocol":"inboundJsonMeta"
               },
          "appId":1,
          "appName":"evostreamms",
          "droppedConnectionsCount":0,
          "enabled":true,
          "id":25,
          "ip":"0.0.0.0",
          "localStreamName":"meta",
          "operationType":11,
          "port":3535,
          "protocol":"inboundJsonMeta"
          },
      "appId":1,
      "appName":"evostreamms",
      "droppedConnectionsCount":0,
      "enabled":true,
      "id":25,
      "ip":"0.0.0.0",
      "localStreamName":"meta",
      "operationType":11,
      "port":3535,
      "protocol":"inboundJsonMeta"
      },
    "configId":13,
    "id":25,
    "ip":"0.0.0.0",
    "localStreamName":"meta",
    "operationType":11,
    "port":3535,
    "protocol":"inboundJsonMeta"
    },
    {
    "acceptedConnectionsCount":0,
    "appId":1,
    "appName":"evostreamms",
    "droppedConnectionsCount":0,
    "enabled":true,
    "id":11,
    "ip":"0.0.0.0",
    "port":8100,
    "protocol":"inboundJsonMeta",
    "sslCert":"",
    "sslKey":""
    }
  ]
},
"description":"Listing all the metadata listeners",
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

- [addMetadataListener](addMetadataListener.html)
- [createService](createService.html)
- [enableService](enableService.html)
- [shutdownService](shutdownService.html)
- [acceptors](userguide_configlua.html#acceptors)