---
title: Blacklisting
sidebar: userguide_sidebar
permalink: userguide_blacklisting.html
folder: userguide
toc: false
---

Blacklisting allows you to limit access to your EMS. This will affect anything that accesses the web port which is by default **8888**. This feature works with the two configuration files which are the [blacklist.txt](userguide_blacklist.html) and [whitelist.txt](userguide_whitelist.html)



## How To

1. Check if blacklist and whitelist configration in webconfig.lua is enabled

   ```
   enableIPFilter=true,
   whitelistFile="..\\config\\whitelist.txt",
   blacklistFile="..\\config\\blacklist.txt",
   ```

   **Note**: `enableIPFilter` is false in default

   ​

2. Add IP addresses to blacklist and whitelist text files

   **Example:** 

   ***blacklist.txt***

   ```
   192.168.2.3
   192.168.2.4
   192.168.2.5
   192.168.2.6
   192.168.2.7
   192.168.2.8
   192.168.2.9
   192.168.2.10
   ```

   ***whitelist.txt***

   ```
   192.168.2.11
   192.168.2.12
   192.168.2.13
   ```

3. Run EMS

   In this example, only IP addresses listed in the whitelist.txt will be granted access to the web server port of EMS, the rest are blacklisted. See the implementation below.

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

## Notes

- You can use IPv6 in this list

------

## Related Links

- [blacklist.txt](userguide_blacklist.html)
- [whitelist.txt](userguide_whitelist.html)