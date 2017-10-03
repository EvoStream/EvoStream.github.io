---
title: addGroupNameAlias
keywords: api
sidebar: api_sidebar
permalink: addGroupNameAlias.html
folder: api
toc: false
---



This command creates secondary name(s) for group names. Once an alias is created the group name cannot be used to request HTTP playback of that stream. Once an alias is used (requested by a client) the alias is removed. Aliases are designed to be used to protect/hide your source streams.





## API Parameter Table



| Parameter Name |  Type  | Mandatory | Default Value | Description                             |
| :------------: | :----: | :-------: | :-----------: | --------------------------------------- |
|   groupName    | string |   true    |    *null*     | The original group name                 |
|   aliasName    | string |   true    |    *null*     | The alias alternative to the group name |



## API Call Template

``` 
addGroupNameAlias groupName=<groupName> aliasName=<groupAliasName>
```



### Sample API Call

``` 
addGroupNameAlias groupName=testAliasGroupName aliasName=testGroupAlias
```



### Success Response in JSON

``` 
"data":{
	"aliasName":"testGroupAlias",
	"cliProtocolId":97,
	"edges":[
	],
	"edgesCount":0,
	"groupName":"testAliasGroupName",
	"lastUpdate":1442374870,
	"operation":"addGroupNameAlias",
	"result":true,
	"uniqueRequestId":2
},
"description":"Alias applied to group name",
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

- **hasGroupNameAliases** in webconfig.lua should be **TRUE**

------

## Related Links

- [hasGroupNameAliases](userguide_webconfig.html#hasgroupnamealiases)
- [listGroupNameAliases](listGroupNameAliases.html)
- [removeGroupNameAliases](removeGroupNameAliases.html)
- [flushGroupNameAliases](flushGroupNameAliases.html)
