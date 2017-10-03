---
title: pushMetadata
keywords: api
sidebar: api_sidebar
permalink: pushMetadata.html
folder: api
toc: false
---

Opens an outboundVmf TCP stream over which each modified JSON metadata object is sent.



## API Parameter Table

| Parameter Name  |  Type   | Mandatory | Default Value | Description                              |
| :-------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
| localStreamName | string  |   true    |    *null*     | Name of the stream to which the associated metadata will be sent |
|      type       | string  |   false   |      vmf      | Type of push stream                      |
|       ip        | string  |   false   |   127.0.0.1   | IP address to push to                    |
|      port       | integer |   false   |     8110      | Port to push to                          |



## API Call Template

``` 
pushMetadata localStreamName=testpullStream ip=<ipAddress> port=<portNumber>
```



### Sample API Call

``` 
pushMetadata localStreamName=testpullStream ip=192.168.0.1 port=8110
```



### Success Response in JSON

``` 
{
   "data":{
      "applicationName":"evostreamms",
      "ip":"192.168.0.1",
      "keepAlive":true,
      "localStreamName":"testpullStream",
      "name":"evostreamms",
      "port":8110,
      "protocol":"outboundVmf",
      "streamName":"testpullStream",
      "type":"vmf"
   },
   "description":"Launched Metadata Push Stream",
   "status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - applicationName – The EMS (evostreamms)
  - ip – The IP address to push to
  - keepAlive – Indicates if it will be enabled after restart
  - localStreamName – Name of the stream to which the associated metadata will be sent
  - name – Name of the application (evostreamms)
  - port – The port to push to
  - protocol – The type of stream
  - streamName – Name of the stream to which the associated metadata will be sent
  - type – The type of stream


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [getMetadata](getMetadata.html)
- [shutdownMetadata](shutdownMetadata.html)