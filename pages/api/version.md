---
title: version
keywords: api
sidebar: api_sidebar
permalink: version.html
folder: api
toc: false
---

Returns the versions for framework and this application.



## API Parameter Table

This function has no parameters.



## API Call Template

``` 
version
```



### Success Response in JSON

``` 
{
"data":{
    "banner":"EvoStream Media Server (www.evostream.com) version 1.7.0 build 4242 with hash: 86bdcde75942b25390a15a6b1de521e913182bcf - PacMan|m| - (built for Ubuntu-14.04-x86_64 on 2015-11-18T10:54:56.000)",
    "branchName":"",
    "buildDate":"2015-11-18T10:54:56.000",
    "buildNumber":"4242",
    "codeName":"PacMan|m|",
    "hash":"86bdcde75942b25390a15a6b1de521e913182bcf",
    "releaseNumber":"1.7.0"
},
"description":"version",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data– Contains an integer representing the version
  - banner – The EMS banner
  - branchName – The branch name where the package is created
  - buildDate – The build date of the released package
  - buildNumber – The build number of the released package
  - codeName – The code name of the released EMS version
  - hash – The hash of the released package
  - releaseNumber – The version of the released package
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

