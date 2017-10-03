---
title: setLogLevel
keywords: api
sidebar: api_sidebar
permalink: setLogLevel.html
folder: api
toc: false
---

Change the log level for all log appenders. Default value in the system is set in the config.lua file, which is usually set to 6.



## API Parameter Table

| Parameter Name |  Type   | Mandatory | Default Value | Description                      |
| :------------: | :-----: | :-------: | :-----------: | -------------------------------- |
|     level      | integer |   true    |    *null*     | A value between **-1** and **6** |



## API Call Template

``` 
setLogLevel level=1
```

This sets the log level to 1. It means it will only output the error logs.



### Success Response in JSON

``` 
{
"data":null,
"description":"Log level is set",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – Nothing to parse for this command


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- Log Levels:
  - 0 – Fatal
  - 1 – Error
  - 2 – Warning
  - 3 – Info
  - 4– Debug
  - 5 – Fine
  - 6 – Finest




## **Related Links**

- [logAppenders](userguide_configlua.html#logappenders)