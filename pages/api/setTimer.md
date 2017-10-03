---
title: setTimer
keywords: api
sidebar: api_sidebar
permalink: setTimer.html
folder: api
toc: false
---

This function adds a timer. When triggered, it will send an event to the event logger.



## API Parameter Table

| Parameter Name |  Type  | Mandatory | Default Value | Description                              |
| :------------: | :----: | :-------: | :-----------: | ---------------------------------------- |
|     value      | string |   true    |     null      | The time value for the timer. It can be either the absolute time at which the trigger will be fired **(YYYY-MM-DDTHH:MM:SS or HH:MM:SS)** or period of time between pulses expressed in seconds between **1** and **86399** (1 sec up to a day). |



## API Call Template

``` 
setTimer value=<value>
```



### Sample API Call

``` 
setTimer value=10
```

```
setTimer value=2016-10-21T07:30:00
```

```
setTimer value=07:30:00
```

### Success Response in JSON

``` 
{
  "data":{
    "timerId":8,
    "triggerCount":0,
    "value":10
  },
  "description":"Custom timer enqueued",
  "status":"SUCCESS"
}
```

```
{
  "data":{
    "timerId":9,
    "triggerCount":0,
    "value":2016-10-21T07:30:00.000
  },
  "description":"Custom timer enqueued",
  "status":"SUCCESS"
}
```

```
{
  "data":{
    "timerId":10,
    "triggerCount":0,
    "value":2016-10-13T07:30:00.000
  },
  "description":"Custom timer enqueued",
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

## Notes

- Using **HH:MM:SS** means the trigger will be done on the **current date** on the given time


------

## Related Links

- [listTimers](listTimers.html)
- [removeTimer](removeTimer.html)