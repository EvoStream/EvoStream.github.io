---
title: setBandwidthLimit
keywords: api
sidebar: api_sidebar
permalink: setBandwidthLimit.html
folder: api
toc: false
---



Enforces a limit on input and output bandwidth.



## API Parameter Table

| Parameter Name |  Type   | Mandatory | Default Value | Description                              |
| :------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
|       in       | integer |   true    |    *null*     | Maximum input bandwidth. **0** means disabled. CLI connections are not affected |
|      out       | integer |   true    |    *null*     | Maximum output bandwidth. **0** means disabled. CLI connections are not affected. |





## API Call Template

``` 
setBandwidthLimit in=<maximumInputValue> out=<maximumOutputValue>
```



### Sample API Call

```
setBandwidthLimit in=400000 out=300000
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
    "in":400000.0000,
    "out":300000.0000
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

## Related Links

- [getBandwidth](getBandwidth.html)
- [Configuring Bandwidth Limits](userguide_bandwidthlimits.html)