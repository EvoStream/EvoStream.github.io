---
title: removeConfig
keywords: api
sidebar: api_sidebar
permalink: removeConfig.html
folder: api
toc: false
---

This command will both stop the stream and remove the corresponding configuration entry. This command is the same as performing `shutdownStream permanently=1`.



## API Parameter Table



|  Parameter Name   |  Type   | Mandatory | Default Value | Description                              |
| :---------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
|        id         | integer |   true    |    *null*     | The configId of the configuration that needs to be removed. ConfigId’s can be obtained from the `listConfig` interface. Removing an inbound stream will also automatically remove all associated outbound streams. |
|     groupName     | string  |   false   |    *null*     | The name of the group that needs to be removed (applicable to HLS, HDS and external processes). *Mandatory only if the id parameter is not specified.* |
| removeHlsHdsFiles | boolean |   false   |   0 *false*   | If **true** and the stream is HLS or HDS, the folder associated with it will be removed |



## API Call Template

``` 
removeConfig id=<configId>
```

OR

``` 
removeConfig groupName=<groupName>
```



### Sample API Call

``` 
removeConfig id=555
```



### Success Response in JSON

``` 
{
"data":{
    *..remove details for clarity*
    },
    "description":"Configuration terminated",
    "status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse.
  - configId – The identifier for the pullPushConfig.xml entry
  - Other fields present are dependent on stream type
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- The config ID shown by the listConfig command is not the same as the stream ID shown by the listStreams command. The `removeConfig` command uses the config ID, not the stream ID.




## Related Links

- [listConfig](listConfig.html)
- [getConfigInfo](getConfigInfo.html)