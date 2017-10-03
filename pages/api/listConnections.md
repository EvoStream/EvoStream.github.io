---
title: listConnections
keywords: api
sidebar: api_sidebar
permalink: listConnections.html
folder: api
toc: false
---



Returns details about every active stream-related connection. This does not include other connections used for EMS operations (telnet, license manager, interface, etc.).



## API Parameter Table

|     **Parameter Name**     |  Type   | **Mandatory** | **Default Value** | **Description**                          |
| :------------------------: | :-----: | :-----------: | :---------------: | ---------------------------------------- |
| excludeNonNetworkProtocols | boolean |     false     |      *null*       | The unique Id of the connection. Usually a value returned by `listStreamsIds` |



## API Call Template

``` 
listConnections
```



### Sample API Call

```
listConnections excludeNonNetworkProtocols=0
```



### Success Response in JSON

``` 
{
"data":[
    {
    "carrier":{
    "farIP":"54.239.131.147",
    "farPort":1935,
    "id":86,
    "nearIP":"192.168.2.107",
    "nearPort":45399,
    "rx":743036,
    "tx":3621,
    "type":"IOHT_TCP_CARRIER"
    },
    "pullSettings":{},
    "stack":[
        {
        "applicationId":0,
        "creationTimestamp":1448259304659.3040,
        "id":97,
        "isEnqueueForDelete":false,
        "queryTimestamp":1448259308424.6599,
        "type":"TCP"
        },
    …
    "txInvokes":5,
    "type":"OR"
    ]
    }
],
"description":"Available connections",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse.
  - carrier – Details about the connection itself
    - farIP – The IP address of the distant party
    - farPort – The port used by the distant party
    - Id - ID of the service
    - nearIP – The IP address used by the local computer
    - nearPort – The port used by the local computer
    - rx – Total bytes received on this connection
    - tx – Total bytes transferred on this connection
    - type – The connection type (TCP, UDP)
  - pullSettings/pushSettings/hlsSettings/hdsSettings/mssSettings/dashSettings/recordSettings – A copy of the parameters used in the stream command that caused this connection to be made
    - Other fields present depend on the stream type (see `pushStream`, `pullStream`, `createHLSStream`, `createHDSStream`, `createMSSStream`, `createDASHStream`, `record` commands)
  - stack – details about what internal resources are using the connection
    - applicationID – the ID of the internal application using the connection
    - creationTimestamp – The time (in UNIX seconds) when the application started using the connection
    - id – The unique ID for this stack relation
    - isEnqueueForDelete – Internal flag used for cleanup
    - queryTimestamp – The time (in UNIX seconds) when this data was populated
    - rxInvokes – Number of received RTMP function invokes
    - streams – Details about the streams that are using the connection (see fields in`listStreams`)
    - txInvokes – Number of sent RTMP function invokes
    - type – A descriptor for how the application is using the connection
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [getConnectionInfo](getConnectionInfo.html)
- [getConnectionsCount](getConnectionsCount.html)
- [getConnectionsCountLimit](getConnectionsCountLimit.html)

