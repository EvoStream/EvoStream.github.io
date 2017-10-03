---
title: flushStreamAliases
keywords: api
sidebar: api_sidebar
permalink: flushStreamAliases.html
folder: api
toc: false
---



Invalidates all streams aliases.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
flushStreamAliases
```



### Success Response in JSON

``` 
{
"data":null,
"description":"All aliases are flushed",
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

- **hasIngestPoints** in config.lua should be **TRUE**


------

## Related Links

- [hasStreamAliases](userguide_configlua.html#hasstreamaliases)
- [listStreamAliases](listStreamAliases.html)
- [removeStreamAlias](removeStreamAlias.html)
- [addStreamAliases](addStreamAlias.html)