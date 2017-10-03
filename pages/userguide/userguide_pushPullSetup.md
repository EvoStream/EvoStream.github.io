---
title: pushPullSetup.xml
keywords: pushPullSetup
sidebar: userguide_sidebar
permalink: userguide_pushPullSetup.html
folder: userguide
toc: false
---

This file is used by the EMS to store stream action commands that are made through the Runtime API. The most important thing to know about the pushPullSetup.xml file is that it **should not be modified manually**!. At startup, if the EMS detects that the file has been modified it will rename the file and start with a blank/fresh copy.

This file is used for internal purposes only. If, during startup, the EMS detects that changes have been made to the pushPullSetup.xml file, it will rename the existing pushPullSetup.xml file and start with a fresh configuration.

Now that the disclaimer is out of the way, it is important to understand how this file is used. When a `pullStream`, `pushStream`, `createHLSStream`, `createHDSStream`, `createMSSStream`, `createDASHStream`, `addMetadatalistner`, `record`, or `launchProcess`, or `startWebRtc` command is executed, that command is logged to this file (assuming the `keepAlive` flag is **1**, which it is by default). 

When the EMS is started, it parses this file and attempts to recreate all of the connections. These configuration entries can be removed by issuing `removeConfig` commands, or by setting the `keepAlive` flag to **0** when the initial command is made.

```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
    <STR name="checksum">b494b8cb7cc5d31ebd4af75b08819139</STR>
    <MAP isArray="true" name="dash" />
    <MAP isArray="true" name="hds" />
    <MAP isArray="true" name="hls" />
    <MAP isArray="true" name="metalistener" />
    <MAP isArray="true" name="mss" />
    <MAP isArray="true" name="process" />
    <MAP isArray="true" name="pull">
    <MAP isArray="true" name="push" />
    <MAP isArray="true" name="record" />
    <MAP isArray="false" name="serverVersion">
        <STR name="banner">EvoStream Media Server (www.evostream.com) version 2.0.0 build 5477 with hash: 373144c364458a5c0a212237a62bcf7ee5af2dfb on branch: release/2.0.0/main - QBert - (built for Microsoft Windows 10 Pro-10.0.14393-x86_64 on 2017-08-04T10:18:20.000)</STR>
        <STR name="branchName">release/2.0.0/main</STR>
        <STR name="buildDate">2017-08-04T10:18:20.000</STR>
        <STR name="buildNumber">5477</STR>
        <STR name="codeName">QBert</STR>
        <STR name="hash">373144c364458a5c0a212237a62bcf7ee5af2dfb</STR>
        <STR name="releaseNumber">2.0.0</STR>
    </MAP>
    <UINT32 name="version">26</UINT32>
    <MAP isArray="true" name="webrtc" />
</MAP>
```

------

##Notes:

- Do not modify this file or else this file will be corrupted.
- If you wish to have a “clean start” of the server, with no previous streams, you may delete this file before starting the EMS.