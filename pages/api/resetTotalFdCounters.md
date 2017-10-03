---
title: resetTotalFdCounters
keywords: api
sidebar: api_sidebar
permalink: resetTotalFdCounters.html
folder: api
toc: false
---

Resets the cumulative totals from the Connection Counters.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
resetTotalFdCounters
```



### Success Response in JSON

``` 
{
"data":null,
"description":"Total counters are cleared",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  Nothing to parse for this command
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## **Related Links**

- [resetMaxFdCounters](resetMaxFdCounters.html)