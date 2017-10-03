---
title: Configuring Event Notifications
keywords: events
sidebar: api_sidebar
permalink: eventnotification.html
folder: api
toc: false
---

Events can be sent to multiple destinations, or “sinks”, at the same time. A “sink” can be either a file or a network destination. Multiple sinks can be enabled at the same time, allowing you to both log events and receive them in your web service(s). These sinks can be configured so that only the events you will be consuming will be generated. Event Sinks are configured in the `config/config.lua` file.

```
eventLogger=
{
    sinks=
    {
        type="sink1_type",
        -- property1 of sink1
        -- property2 of sink1
    },
    enabledEvents=
    {
        "inStreamCreated",
        "inStreamClosed",
    }
},
```

### Enabling Event Logs

Event Notifications are off by default. To use the Event Notification System, you must modify the EMS configuration file.

1.  Remove comment to the eventLogger section in the configuration `--[[ ]]--`
2.  Select your preferred filename and file format
3.  Configure time-stamp if to be used
4.  Select events that will be enabled under `enabledEvents`


------

## Notes

- Only the events selected will be shown in the logs

------

## Related Links

- [Event Overview](eventoverview.html)
- [Event Sinks](eventsinks.html)
- [Application vs. Server Events](eventappvsserver.html)
- [Events List](eventlist.html)
- [Event Definition](eventdefinition.html)
- [Event Logger](userguide_configlua.html#eventLogger)
- [EvoWebservices Event](evowebservices_event.html)
- [EvoWebservices Event Configuration](evowebservices_eventconfiguration)