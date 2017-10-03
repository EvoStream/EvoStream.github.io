---
title: isStreamRunning
keywords: api
sidebar: api_sidebar
permalink: isStreamRunning.html
folder: api
toc: false
---

Checks a specific stream if it is running or not.



## API Parameter Table



| Parameter Name  |  Type   | Mandatory | Default Value | Description                              |
| :-------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
|       id        | integer |   true    |    *null*     | The **configID** of the stream to check. |
| localStreamName | string  |   true    |    *null*     | The name of the stream to check.         |

## API Call Template

``` 
isStreamRunning id=<configId>
```

OR

``` 
isStreamRunning localStreamName=<localStreamName>
```



### Sample API Call

``` 
isStreamRunning localStreamName=testpullStream
```



### Success Response in JSON

**If running:**

``` 
"data":{
	"Running":true
},
"description":"Stream status:",
"status":"SUCCESS"
```

**If not running:**

``` 
"data":{
	"Running":false
},
"description":"Stream status:",
"status":"SUCCESS"
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse.
  - Running - tells whether the stream is active **true** or **false**
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- Either add the parameter **id** or **localStreamName** in the API call


------

## Related Links

- [listStreams](listStreams.html)
- [listStreamsIds](listStreamsIds.html)
- [listConfig](listConfig.html)