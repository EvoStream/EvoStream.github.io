---
title: removeTimer
keywords: api
sidebar: api_sidebar
permalink: removeTimer.html
folder: api
toc: false
---

This function removes a previously armed timer.



## API Parameter Table

| Parameter Name |  Type   | Mandatory | Default Value | Description                       |
| :------------: | :-----: | :-------: | :-----------: | --------------------------------- |
|       id       | integer |   true    |     null      | The ID of the timer to be removed |



## API Call Template

``` 
removeTimer id=<id>
```



### Sample API Call

``` 
removeTimer id=8
```



### Success Response in JSON

``` 
{
  "data":{
    "timerId":8,
    "triggerCount":0,
    "value":10
  },
  "description":"Timer removed",
  "status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - Id – The ID of the timer added
  - triggerCount – The number of times the timer triggered since it was added
  - value – The time value for the timer (see parameter table above)


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [setTimer](setTimer.html)
- [listTimers](listTimers.html)