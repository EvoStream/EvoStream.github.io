---
title: getLicenseId
keywords: api
sidebar: api_sidebar
permalink: getLicenseId.html
folder: api
toc: false
---

Returns the License ID of the License being used.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
getLicenseId
```



### Success Response in JSON

``` 
{
"data":{
"licenseId":"544247f0f6cca957"
},
"description":"getLicenseId",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse
  - licenseId - the ID of the license
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.
