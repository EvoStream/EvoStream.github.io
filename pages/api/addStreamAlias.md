---
title: addStreamAlias
keywords: api
sidebar: api_sidebar
permalink: addStreamAlias.html
folder: api
toc: false
---



Allows you to create secondary name(s) for internal streams. Once an alias is created the localstreamname cannot be used to request playback of that stream. Once an alias is used (requested by a client) the alias is removed. Aliases are designed to be used to protect/hide your source streams.





## API Parameter Table



| Parameter Name  |  Type   | Mandatory |  Default Value   | Description                              |
| :-------------: | :-----: | :-------: | :--------------: | ---------------------------------------- |
| localStreamName | string  |   true    |      *null*      | The original stream name                 |
|    aliasName    | string  |   true    |      *null*      | The alias alternative to the `localStreamName` |
|  expirePeriod   | integer |   false   | -600 *(10 mins)* | The expiration period for this alias. Negative values will be treated as one-shot but no longer than the absolute positive value in seconds, 0 means it will not expire, positive values mean the alias can be used multiple times but expires after this many seconds. The default is -600 (one-shot, 10 mins) |



## API Call Template

``` 
addStreamAlias localStreamName=<localStreamName> aliasName=<aliasName>
```



### Sample API Call

``` 
addStreamAlias localStreamName=testpullStream aliasName=testStreamAlias expirePeriod=0
```

Stream with “**testpullStream**” as `localStreamName` will have an alias of “**testStreamAlias**”.



### Success Response in JSON

``` 
{
"data":{
    "aliasName":"testAlias",
    "expirePeriod":0,
    "localStreamName":"testpullStream"
},
"description":"Alias applied",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse.
  - aliasName – The alias alternative to the `localStreamName`
  - expirePeriod – The expiration period for the alias
  - localStreamName – The original stream name
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.




##Alias in VOD

You can also set an alias for the VOD streams:

```
addStreamAlias localStreamName=mp4:myfile.mp4 aliasName=myVODalias expirePeriod=0
```

Media file with “**myfile.mp4**” filename will have an alias of “**myVODalias**”

------

## Notes

- **hasStreamAliases** in config.lua should be **TRUE**
- If you will use VOD as a stream source, you need to issue the VOD's alias first or else the file will not be seen by EMS


------

## Related Links

- [hasStreamAliases](userguide_configlua.html#hasstreamaliases)
- [listStreamAliases](listStreamAliases.html)
- [removeStreamAlias](removeStreamAlias.html)
- [flushStreamAliases](flushStreamAliases.html)

