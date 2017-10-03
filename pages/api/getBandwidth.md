---
title: getBandwidth
keywords: api
sidebar: api_sidebar
permalink: getBandwidth.html
folder: api
toc: false
---



Returns the current and limit bandwidth values.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
getBandwidth
```



### Success Response in JSON

``` 
{
"data":{
    "current":{
    "in":111880.0459,
    "out":147.8026
	},
    "max":{
    "in":0.0000,
    "out":0.0000
    }
},
"description":"Bandwidth in B\/s",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse
  - current – The current bandwidths
    - in – The inbound bandwidth
    - out – The outbound bandwidth
  - max – The maximum bandwidths
    - in – The inbound limit
    - out - The outbound limit
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## **Related Links**

- [setBandwidthLimit](setBandwidthLimit.html)