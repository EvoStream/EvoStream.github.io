---
title: listGroupNameAliases
keywords: api
sidebar: api_sidebar
permalink: listGroupNameAliases.html
folder: api
toc: false
---

Returns a complete list of aliases.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listGroupAliases
```



### Success Response in JSON

``` 
{
"data":[
    {
    "aliasName":"testGroupAlias",
    "groupName":"testAliasGroupName"
}
],
"description":"Currently available group name aliases",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data– Provides the following information for each group name alias
  - aliasName – The alias alternative to the `groupname`
  - groupName – The original group name
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasGroupNameAliases** in webconfig.lua should be **TRUE**


------

## **Related Links**

- [hasGroupNameAliases](userguide_webconfig.html#hasgroupnamealiases)
- [addGroupNameAliases](addGroupNameAliases.html)
- [getGroupNameByAlias](getGroupNameByAlias.html)
- [removeGroupNameAliases](removeGroupNameAliases.html)
- [flushGroupNameAliases](flushGroupNameAliases.html)