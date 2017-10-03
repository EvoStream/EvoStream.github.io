---
title: help
keywords: api
sidebar: api_sidebar
permalink: help.html
folder: api
toc: false
---



This function prints out descriptions of the API in JSON format.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
help
```



### Success Response in JSON

``` 
{
“data":[
    {
    "command":"help",
    "deprecated":false,
    "description":"prints this help",
    "parameters":[]
    },
    {
    "command":"API",
    "deprecated":isdeprecated,
    "description":"API description",
    "parameters":[list of API parameters]
        {
        "defaultValue":parameter default value,
        "description":"parameter description”,
        "mandatory":ismandatoryparameter,
        "name":"parameter name"
        },
    },
    ],
"description":"Available commands",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - command – The name of a valid command.
  - deprecated – Is **true** if the command is deprecated, **false** if not
  - description – Describes the use of the command
  - parameters – Parameter settings for the command
    - defaultValue – The default value if the parameter is omitted
    - description – Describes the use of the parameter
    - mandatory – Is **true** if the parameter is mandatory, **false** if not
    - name – The name of a parameter for the command
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

