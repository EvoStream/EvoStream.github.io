---
title: Configuring and Receiving Event Notifications
keywords: events
sidebar: userguide_sidebar
permalink: userguide_confevents.html
folder: userguide
toc: false
---

EMS generates notifications based upon events that occur at runtime. These events are formatted as HTTP calls and can be delivered to any address and port desired.

Event Notifications are enabled by default and are configured to send to the local web services provided within your EMS installation. The Web Services are **disabled** by default, and so do not take any action on the events. Please review the EvoStream Web Services documentation for instructions on enabling and working with each of the web services.

Additional Event Notification destinations can be enabled (or disabled) by modifying the EMS config file: `config.lua`.

To enable Event Notifications you will need to Enable/Uncomment the *eventLogger* section of the config.lua file. Comments in LUA are specified by either a `--` for a single line, or denoted by a `--[[` to start a comment block and a `]]--` to end a comment block. By default the eventLogger section is commented out using block style comments, so you will need to remove both the `--[[` and `]]--`strings. See the Configuration Files section for more information.