---
title: resetMaxFdCounters
keywords: api
sidebar: api_sidebar
permalink: resetMaxFdCounters.html
folder: api
toc: false
---



Reset the maximum, or high-water-mark, from the Connection Counters





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
resetMaxFdCounters
```



### Success Response in JSON

``` 
{
"data":null,
"description":"Max counters are cleared",
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

- [resetTotalFdCounters](resetTotalFdCounters.html)