---
title: listTimers
keywords: api
sidebar: api_sidebar
permalink: listTimers.html
folder: api
toc: false
---

This function lists currently active timers.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listTimers
```



### Success Response in JSON

``` 
{
  "data":[
    {
      "timerId":8,
      "triggerCount":141,
      "value":10
    }
  ],
  "description":"List of armed timers",
  "status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - timerId – The ID of the timer added
  - triggerCount – The number of times the timer triggered since it was added
  - value – The time value for the timer 
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Related Links

- [setTimer](setTimer.html)
- [removeTimer](removeTimer.html)