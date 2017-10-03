---
title: getConnectionInfo
keywords: api
sidebar: api_sidebar
permalink: getConnectionInfo.html
folder: api
toc: false
---



Returns a detailed set of information about a connection.



## API Parameter Table

| **Parameter Name** |  Type   | **Mandatory** | **Default Value** | **Description**                          |
| :----------------: | :-----: | :-----------: | :---------------: | ---------------------------------------- |
|         id         | integer |     true      |      *null*       | The uniqueId of the connection. Usually a value returned by `listStreamsIds` |



## API Call Template

``` 
getConnectionInfo id=<id>
```



### Sample API Call

```
getConnectionInfo id=144
```



### Success Response in JSON

``` 
{
    "data":{
        "carrier":null,
        "stack":[
            {
                "applicationId":1,
                "creationTimestamp":1338633696196.6460,
                "id":144,
                "isEnqueueForDelete":false,
                "queryTimestamp":1338658491380.7349,
                "type":"TMR"
            }
        ]
    },
    "description":"Connection information",
    "status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse.
  - carrier - Details about the connection itself
  - stack - details about what internal resources are using the connection
    - applicationId - the ID of the internal application using the connection
    - creationTimeStamp - The time (in UNIX seconds) when the application started using the connection
    - Id - The unique ID for this stack relation
    - isEnqueForDelete - Internal flag used for cleanup
    - queryTimeStamp - The time (in UNIX seconds) when this data was populated
    - type - A descriptor for how the application is using the connection
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [listConnections](listConnections.html)