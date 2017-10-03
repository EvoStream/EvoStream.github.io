---
title: ERS API
keywords: html5
sidebar: html5players_sidebar
permalink: html5players_ersapi.html
folder: html5players
toc: true
---



A set of APIs are available to manage ERS and allow the actual generation and deletion of tokens and rooms. These APIs are accessible through an HTTP GET request with the following format:

```
http(s)://<ERS IP>:<ERS adminPort>/?c=<commandName>&i=<Id>

```

**Where:**

| **Field**     | **Description**                          |
| ------------- | ---------------------------------------- |
| ERS IP        | IP address of the machine hosting ERS    |
| ERS adminPort | Port number where admin APIs can be accessed |
| commandName   | Name of the actual command               |
| Id            | Value of the parameter, either token ID or room ID |

For example, an ERS running on the same machine where the request is being generated from (default setup) can use the following:

```
http://127.0.0.1:3030/?c=addToken&i=thisIsASampleToken

```

This HTTP GET request can be sent through any scripting language desired.

An example admin interface which uses Javascript to send out this request can be accessed through:

```
http://127.0.0.1:3030/ersadmin.html
```



## API LIST

### Get Version

Returns the current version of ERS.

| **Field**    | **Value** |
| ------------ | --------- |
| Command Name | version   |
| Parameter Id | (ignored) |

**API Call** 

```
http://127.0.0.1:3030/?c=version
```



### Add Token

Adds a token that can be used later by a client trying to connect with EMS.

| **Field**    | **Value**    |
| ------------ | ------------ |
| Command Name | addToken     |
| Parameter Id | < token Id > |

**API Call**

```
http://127.0.0.1:3030/?c=addToken&i=tokenId

```



### Delete Token

Deletes an existing token.

| **Field**    | **Value**    |
| ------------ | ------------ |
| Command Name | delToken     |
| Parameter Id | < token Id > |

**API Call**

```
http://127.0.0.1:3030/?c=delToken&i=tokenId

```



### List Tokens

Displays all created tokens currently active.

| **Field**    | **Value**  |
| ------------ | ---------- |
| Command Name | listTokens |
| Parameter Id | (ignored)  |

**API Call**

```
http://127.0.0.1:3030/?c=listTokens

```



### Add Room

Adds an allowed room to the list during runtime. This command also effectively prevents creation of rooms not included on the list.

| **Field**    | **Value**   |
| ------------ | ----------- |
| Command Name | addRoom     |
| Parameter Id | < room ID > |

**API Call**

```
http://127.0.0.1:3030/?c=addRoom&i=roomId

```



### Delete Room

Deletes a room added from the list.

| **Field**    | **Value**   |
| ------------ | ----------- |
| Command Name | delRoom     |
| Parameter Id | < room ID > |

**API Call**

```
http://127.0.0.1:3030/?c=delRoom&i=roomId

```



### List Rooms

Displays all rooms with their corresponding descriptions and status.

| **Field**    | **Value** |
| ------------ | --------- |
| Command Name | listRooms |
| Parameter Id | (ignored) |

**API Call**

```
http://127.0.0.1:3030/?c=listRooms
```


### Add EMS Token

Displays all rooms with their corresponding descriptions and status.

| **Field**    | **Value**      |
| ------------ | -------------- |
| Command Name | addEMSToken    |
| Parameter Id | < token name > |

**API Call**

```
http://127.0.0.1:3030/?c=addEMSToken&i=tokenName
```



### List EMS Tokens

Displays all rooms with their corresponding descriptions and status.

| **Field**    | **Value**    |
| ------------ | ------------ |
| Command Name | listEMSToken |
| Parameter Id | (ignored)    |

**API Call**

```
http://127.0.0.1:3030/?c=listEMSToken
```



### Delete EMS Token

Deletes all tokens with their corresponding descriptions and status.

| **Field**    | **Value**      |
| ------------ | -------------- |
| Command Name | delEMSToken    |
| Parameter Id | < token name > |

**API Call**

```
http://127.0.0.1:3030/?c=delEMSToken&i=tokenName
```

