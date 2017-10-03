---
title: blacklist.txt
keywords: blacklist
sidebar: userguide_sidebar
permalink: userguide_blacklist.html
folder: userguide
toc: false
---

Defines the IP address that will be blocked by EMS. If a blacklist is specified, access will only be granted to IP address does **NOT APPEAR** on the blacklist.



**Implementation:** 

| Blacklist | Whitelist | Allowed IPs                            |
| :-------: | :-------: | -------------------------------------- |
|   empty   |   empty   | all IPs are allowed                    |
|  x.x.x.x  |   empty   | all IPs are allowed except for x.x.x.x |
|   empty   |  y.y.y.y  | only y.y.y.y is allowed                |
|  x.x.x.x  |  y.y.y.y  | only y.y.y.y is allowed                |
|  no file  |  y.y.y.y  | only y.y.y.y is allowed                |
|  x.x.x.x  |  no file  | all IPs are allowed except for x.x.x.x |
|  no file  |  no file  | error                                  |

------

##Notes:

- `enableIPFilter` should be set to `true` in webconfig.lua to be able to read the blacklist file


- `blacklistFile` code should not be commented to be able to honor the list of blacklisted IP address

  *Entry in config.lua:*

  ```
    enableIPFilter=true,
    whitelistFile="..\\config\\whitelist.txt",
    blacklistFile="..\\config\\blacklist.txt",
  ```

- If IP address is both on whitelist and blacklist file, EMS will treat the IP address as blacklisted


------

## Related LInks

- [whitelist.txt](userguide_whitelist.html)
- [Blacklisting](userguide_blacklisting.html)