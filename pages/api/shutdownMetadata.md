---
title: shutdownMetadata
keywords: api
sidebar: api_sidebar
permalink: shutdownMetadata.html
folder: api
toc: false
---

Stops a metadata pseudo-stream. This command shuts down all multiple pull streams that were issued for a given `localStreamName`.



## API Parameter Table

| Parameter Name  |  Type  | Mandatory | Default Value | Description                              |
| :-------------: | :----: | :-------: | :-----------: | ---------------------------------------- |
| localStreamName | string |   true    |    *null*     | Metadata associated with this incoming stream name |



## API Call Template

``` 
shutdownMetadata localStreamName=<localStreamName>
```



### Sample API Call

``` 
shutdownMetadata localStreamName=testpullStream
```



### Success Response in JSON

``` 
{
"data":{
    "localStreamName":"testpullStream",
    "streamName":"testpullStream",
    "type":"vmf"
},
"description":"Shutdown Metadata Push Stream", 
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - localStreamName – Name of the stream to which the associated metadata will be sent
  - streamName – Name of the stream to which the associated metadata will be sent
  - type – The type of stream


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## **Related Links**

- [pushMetadata](pushMetadata.html)
- [getMetadata](getMetadata.html)