---
title: removeStreamAlias
keywords: api
sidebar: api_sidebar
permalink: removeStreamAlias.html
folder: api
toc: false
---



Removes an alias of a stream.



## API Parameter Table

| Parameter Name |  Type  | Mandatory | Default Value | Description         |
| :------------: | :----: | :-------: | :-----------: | ------------------- |
|   aliasName    | string |   true    |    *null*     | The alias to delete |



## API Call Template

``` 
removeStreamAlias aliasName=<aliasName>
```



### Sample API Call

``` 
removeStreamAlias aliasName=testAlias
```

### Success Response in JSON

``` 
{
"data":{
	"aliasName":"testAlias"
},
"description":"Alias removed",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - ​	aliasName – The alias of the stream that was removed
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasStreamAliases** in config.lua should be **TRUE**


------

## Related Links

- [hasStreamAliases](userguide_configlua.html#hasstreamaliases)
- [addStreamAlias](addStreamAlias.html)
- [listStreamAliases](listStreamAliases.html)
- [flushStreamAliases](flushStreamAliases.html)