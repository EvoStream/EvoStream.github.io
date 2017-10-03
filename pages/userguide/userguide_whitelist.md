---
title: whitelist.txt
keywords: whitelist
sidebar: userguide_sidebar
permalink: userguide_whitelist.html
folder: userguide
toc: false
---



Defines the IP address that will have access to EMS. If a whitelist is specified, access will only be granted to that IP address that **APPEARS** on the whitelist file.

**Implementation:** 

| Blacklist | Whitelist | Is Allowed?                            |
| :-------: | :-------: | -------------------------------------- |
|   empty   |   empty   | all IPs are allowed                    |
|  x.x.x.x  |   empty   | all IPs are allowed except for x.x.x.x |
|   empty   |  y.y.y.y  | only y.y.y.y is allowed                |
|  x.x.x.x  |  y.y.y.y  | only y.y.y.y is allowed                |
|  no file  |  y.y.y.y  | only y.y.y.y is allowed                |
|  x.x.x.x  |  no file  | all IPs are allowed except for x.x.x.x |
|  no file  |  no file  | error                                  |

**Notes:**

- `enableIPFilter` should be set to `true` in webconfig.lua to be able to read the whitelist file

- `whitelistFile` code should not be commented to be able to honor the list of whitelist IP address

  ```
    enableIPFilter=true,
    whitelistFile="..\\config\\whitelist.txt",
    blacklistFile="..\\config\\blacklist.txt",
  ```

- If IP address is both on whitelist and blacklist file, EMS will treat the IP address as blacklisted



------

## Related Links

- [blacklist.txt](userguide_blacklist.html)
- [Blacklisting](userguide_blacklisting.html)