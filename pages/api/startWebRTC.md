---
title: startWebRTC
keywords: api
sidebar: api_sidebar
permalink: startWebRTC.html
folder: api
toc: false
---

Starts a WebRTC signalling client to an ERS (Evostream Rendezvous Server).

This will open the port in the given IP address and will open doors for the room ID which can be accessed using the evowrtcclient.html



## API Parameter Table



| Parameter Name |  Type  | Mandatory | Default Value | Description                              |
| :------------: | :----: | :-------: | :-----------: | ---------------------------------------- |
|     ersIp      | string |   true    |    *null*     | IP address (xx.yy.zz.xx) of ERS          |
|    ersPort     | string |   true    |    *null*     | Port of ERS                              |
|     roomId     | string |   true    |    *null*     | Unique room Identifier within ERS that will be used by client browsers to connect to this EMS |
|     token      | string |   false   |    *null*     | The security token to be used within ERS |



## API Call Template

``` 
startWebrtc ersip=<ERS_IPAddress> ersport=<ERS_Port> roomid=<roomID>
```



### Sample API Call

``` 
startWebrtc ersip=52.6.14.61 ersport=3535 roomid=testRoom
```



### Success Response in JSON

``` 
{
          "data": {
                    "data": {
                              "configId": 2,
                              "ers": "",
                              "ersOverSsl": false,
                              "ersip": "54.174.188.145",
                              "ersport": 4545,
                              "keepAlive": true,
                              "name": "evostreamms",
                              "operationType": 9,
                              "roomid": "testRoom",
                              "sslCert": "../config/server.cert",
                              "sslKey": "../config/server.key",
                              "token": ""
                    },
                    "description": "Started WebRTC Negotiation Service",
                    "status": "SUCCESS"
          }
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse.
  - configId - The configuration ID for this command
  - ers - 
  - ersOverSsl - The configuration of the SSL
  - ersip – The IP address of the ERS
  - ersport – The port of the ERS
  - keepAlive - If keepAlive is set to true, EMS will reconnect to ERS in the event that it gets disconnected
  - name - ??
  - operationType – The type of operation
  - roomId – The room identifier
  - sslCert - The SSL certificate
  - sslKey - The SSL key certificate
  - token - ??
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- Room ID can only be started once


------

## Related Links

- [stopWebRTC](stopWebRTC.html)
- [WebRTC Overview](html5players_wrtcoverview.html)