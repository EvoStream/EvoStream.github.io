---
title: bandwidthlimits.xml
keywords: bandwidthlimits
sidebar: userguide_sidebar
permalink: userguide_bandwidthlimits.html
folder: userguide
toc: false
---

Defines the maximum amount of bandwidth you want the server to be able to use (set the instantaneous bandwidth cap).

If `enableCheckBandwidth` in config.lua is true, automatically EMS will read the bandwidths.xml file. EMS will limit all the incoming and outgoing stream dependent to the configured bandwidth range.

Default for in and out is zero (0) which means no limit.

```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
    <DOUBLE name="in">0.000</DOUBLE>
    <DOUBLE name="out">0.000</DOUBLE>
</MAP>
```

See [enableCheckBandwidth](userguide_configlua.html#enablecheckbandwidth).