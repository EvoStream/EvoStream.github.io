---
title: getGroupNameByAlias
keywords: api
sidebar: api_sidebar
permalink: getGroupNameByAlias.html
folder: api
toc: false
---



This command returns the group name given the alias name.





## API Parameter Table



| Parameter Name |  Type  | Mandatory | Default Value | Description                             |
| :------------: | :----: | :-------: | :-----------: | --------------------------------------- |
|   aliasName    | string |   true    |    *null*     | The alias alternative to the group name |



## API Call Template

``` 
getGroupNameByAlias aliasName=<groupAliasName>
```



### Sample API Call

``` 
getGroupNameByAlias aliasName=testGroupAlias
```



### Success Response in JSON

``` 
"data":{
	"aliasName":"testGroupAlias",
	"cliProtocolId":97,
	"edges":[ ],
	"edgesCount":0,
	"groupName":"testAliasGroup",
	"lastUpdate":1442374870,
	"operation":"getGroupNameAlias",
	"result":true,
	"uniqueRequestId":4
},
"description":"Group name",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse.
  - aliasName – The alias alternative to the `localStreamName`
  - cliProtocolId - ??
  - edges - ??
  - edgesCount - ??
  - groupName – The assigned groupName where alias is applied
  - lastUpdate - ??
  - operation - ??
  - result - ??
  - uniqueRequestId - ??
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasStreamAliases** in config.lua should be **TRUE**

------

## Related Links

- [hasGroupNameAliases](userguide_webconfig.html#hasgroupnamealiases)
- [addGroupNameAlias](addGroupNameAlias.html)
- [listGroupNameAliases](listGroupNameAliases.html)
- [removeGroupNameAliases](removeGroupNameAliases.html)
- [flushGroupNameAliases](flushGroupNameAliases.html)

