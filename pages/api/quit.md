---
title: quit
keywords: api
sidebar: api_sidebar
permalink: quit.html
folder: api
toc: false
---

This function quits the ASCII Command Line Interface (CLI).



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
quit
```



### Success Response in JSON

``` 
{
"data":null,
"description":"Bye!",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – Nothing to parse for this command
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- This API is not available in EMS Web UI's API Explorer

