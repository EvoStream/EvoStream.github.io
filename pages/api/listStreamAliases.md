---
title: listStreamAliases
keywords: api
sidebar: api_sidebar
permalink: listStreamAliases.html
folder: api
toc: false
---

Returns a complete list of aliases.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listStreamAliases
```



### Success Response in JSON

``` 
{
"data":[
    {
    "aliasName":"testAlias",
    "creationTime":1448267205,
    "expirePeriod":0,
    "localStreamName":"testpullStream",
    "oneShot":false,
    "permanent":false
}
],
"description":"Currently available aliases",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – Contains an array of pairs of `aliasName` and `localStreamName`
  - aliasName – The alias alternative to the `localStreamName`
  - creationTime – The time the alias is created
  - expirePeriod - The expiration period of the alias
  - localStreamName – The original stream name
  - oneShot - Determines if the alias can only be used once
  - permanent - Determines if the alias is for permanent use (unless EMS is restarted)
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasStreamAliases** in config.lua should be **TRUE**


------

## Related Links

- [hasStreamAliases](userguide_configlua.html#hasstreamaliases)
- [addStreamAlias](addStreamAlias.html)
- [removeStreamAlias](removeStreamAlias.html)
- [flushStreamAliases](flushStreamAliases.html)