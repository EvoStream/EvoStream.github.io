---
title: getMetadata
keywords: api
sidebar: api_sidebar
permalink: getMetadata.html
folder: api
toc: false
---

Returns the most recently received string currently cached by the Metadata Manager. The call is stateless so multiple clients may each poll for metadata with no impact on each other. This may result in getting the same string multiple times if no new string has arrived.



## API Parameter Table

| Parameter Name  |  Type   | Mandatory | Default Value | Description                              |
| :-------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
| localStreamName | string  |   true    |    *null*     | Name of the incoming stream from which the associated metadata will be returned. Default most recent |
|    streamId     | integer |   false   |       0       | Identifies the particular stream from which the associated metadata will be returned. Default most recent |
|     noWrap      | boolean |   false   |   0 *false*   | If **true**, the returned string will not have the CLI JSON wrapping |



## API Call Template

``` 
getMetadata localStreamName=<localStreamName>
```



### Sample API Call

``` 
getMetadata localStreamName=testpullStream noWrap=0
```

```
getMetadata localStreamName=testpullStream noWrap=1
```

### Success Response in JSON

``` 
{
"data":"{\"EMS\":{\"type\":\"json\",\"timestamp\":46125},\"data\":{\"lat\":\"32.809668\",\"lon\":\"-117.255317\",\"alt\":\"44.7\",\"speed\":\"20\",\"dir\":\"300\"}}",
"description":"Metadata",
"status":"SUCCESS"
}
```

```
{
"EMS":{
    "type":"json",
    "timestamp":12042
	},
"data":{
    "lat":"32.809668",
    "lon":"-117.255317",
    "alt":"44.7",
    "speed":"50",
    "dir":"300"
	}
}
```

#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - type - response type
  - timestamp -  
  - lat - latitude value
  - lon - longitude value
  - alt -altitude value
  - speed - speed value
  - dir -


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [pushMetadata](pushMetadata.html)
- [shutdownMetadata](shutdownMetadata.html)