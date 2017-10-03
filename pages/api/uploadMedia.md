---
title: uploadMedia
keywords: api
sidebar: api_sidebar
permalink: uploadMedia.html
folder: api
toc: false
---

Creates an acceptor which receives an HTTP POST binary upload. The acceptor will be opened on a specified port and the uploaded media file will be written on a specified directory. The acceptor then waits for an HTTP POST from a client with the media file as payload. The media file is then written on the specified location in the server.



## API Parameter Table

| Parameter Name |  Type   | Mandatory | Default Value | Description                              |
| :------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
|      port      | integer |   true    |    *null*     | The port value to bind on                |
|  targetFolder  | string  |   true    |    *null*     | The folder where the binary upload will be serialized |



## API Call Template

``` 
uploadMedia port=<portNumber> targetFolder=<targetFolder>
```



### Sample API Call

``` 
uploadMedia port=3333 targetFolder=../media
```



### Success Response in JSON

``` 
{
"data":{
    "ip":"0.0.0.0",
    "port":3333,
    "targetFolder":"..\/media"
},
"description":"Media upload acceptor configuration.",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - ip – The IP referring to the EMS, normally 0.0.0.0
  - port – The specified port number where the acceptor will wait for HTTP POSTs
  - targetFolder – The specified folder where the media file will be written


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- The sending client must conform to the following:
  - It must send the data by way of HTTP POST
  - The POST request must be in http/1.1 format
  - A StreamName must be provided in the POST line. This will then be the filename of the media file (mp4) when written. (e.g., *POST /mystreamname HTTP/1.1\r\n*)
  - Content-type must be set to *video/mp4* or *application/octet-stream*
  - Content-length must be used. This function is intended for uploading VOD MP4 so the EMS will expect that the size of the file is already known


