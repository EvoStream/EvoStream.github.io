---
title: flushGroupNameAliases
keywords: api
sidebar: api_sidebar
permalink: flushGroupNameAliases.html
folder: api
toc: false
---



This command invalidates all group name aliases.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
flushGroupNameAliases
```



### Success Response in JSON

``` 
{
"data":null,
"description":"All group name aliases are flushed",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data– Nothing to parse for this command
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasGroupNameAliases** in webconfig.lua should be **TRUE**

------

## **Related Links**

- [hasGroupNameAliases](userguide_webconfig.html#hasgroupnamealiases)
- [addGroupNameAliases](addGroupNameAliases.html)
- [getGroupNameByAlias](getGroupNameByAlias.html)
- [listGroupNameAliases](listGroupNameAliases.html)
- [removeGroupNameAliases](removeGroupNameAliases.html)

