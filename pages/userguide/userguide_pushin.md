---
title: Push-in a Stream
keywords: push-in
sidebar: userguide_sidebar
permalink: userguide_pushIn.html
folder: userguide 
toc: true
---

EMS is capable of receiving streams that are pushed to it from other servers. An RTMP listener is available on port **1935** , an RTSP listener on **5544** and a LiveFLV listener on port **6666**.



##How To

Steps on how to do the actual stream push needs to be consulted with the stream source, as every system has different ways of accomplishing this.



##Push-In Authentication

For security, EMS has an option to require all streams which are pushed into the server be authenticated using authentication details that are specified in `config.lua` and `users.lua`. By default, the authentication configuration is disabled.

To enable authentication in the EMS the following should be set:

**Note:**

All documents can be found inside the `../config` folder

1. Set the boolean value in `auth.xml` to true

   ```
    <BOOL name="">true</BOOL>

   ```

2. Remove comments (`--[[` .. `]]--`) in authentication in `config.lua` and configure the parameters to be used

   ```
    --[[ //remove
    authentication=
    {
   				rtmp=
   				{
   					type="adobe",
   					encoderAgents=
   					{
   						"FMLE/3.0 (compatible; FMSc/1.0)",
   						"Wirecast/FM 1.0 (compatible; FMSc/1.0)",
   						"EvoStream Media Server (www.evostream.com)"
   					},
   					usersFile="/<path_to>/users.lua",
   					--verifierUri="http://authserver/verifier.php",
   					--token="secretstring",
   				},
   				rtsp=
   				{
   					usersFile="/<path_to>/users.lua",
   					--authenticatePlay=false,
   				},
    },  
    ]]-- //remove
   ```

**Authentication Parameters** 

| Protocol |  Parameter Name  | Description                              |
| :------: | :--------------: | ---------------------------------------- |
|   RTMP   |       type       | The RTMP type                            |
|   \|\|   |  encoderAgents   | The encoder agent to be used             |
|   \|\|   |    usersFile     | The path of the users file               |
|   \|\|   |   verifierUri    | The external URL of the verifier. Should return 200 OK to indicate success, otherwise, failure |
|   \|\|   |      token       | The token used for security              |
|   RTSP   |    usersFile     | The path of the users file               |
|   \|\|   | authenticatePlay | If set to true, it will prompt for a username and password window when stream is requested for playback |



**Add Users in users.lua**

The configurations in the `users.lua` will serve as the username and password that needs to be inputted in the authentication window if authenticatePlay is set to true.

```
users=
{
  USER_A="12345678",
}
realms=
{
  {
    name="EVOSTREAM stream router",
    method="Digest",
    users={
      "USER_A",
    },
  },
}

```

**Note:** Multiple users may add in this section. Just add entries under each user entry.

```
users=
{
  USER_A="12345678",
  USER_B="87654321",
}
realms=
{
  {
    name="EVOSTREAM stream router",
    method="Digest",
    users={
      "USER_A",
      "USER_B",
    },
  },
}
```

------

## Related Links:

- [pushStream API](api_pushStream.html)
- [Send Stream To Facebook](userguide_send.html#facebook-live)
- [Send Stream To Youtube](userguide_send.html#youtube-live)