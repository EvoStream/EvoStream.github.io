---
title: Configuring EMS Event Notifications
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_eventconfiguration.html
folder: evowebservices
toc: false
---



EMS Event Notifications must be configured to communicate with the EMS Web Services. The EMS configuration file must be modified as follows. Please view the [EMS User’s Guide](http://docs.evostream.com/ems_user_guide/table_of_contents) for more detailed information on configuring Event Notifications.

**config.lua:**

```
eventLogger= 
{
  sinks=
  { 
    {
      type="RPC", 
      url="http://192.168.2.39/evowebservices/evowebservices.php",    -- for php
      url="http://localhost:4000/evowebservices/",                    -- for node       
      serializerType="JSON",
      -- serializerType="XML" 
      -- serializerType="XMLRPC"
      enabledEvents= 
      { 
		"inStreamCreated",
		"inStreamClosed",
		"outStreamCreated",
		"timerCreated",
		"timerTriggered",
		"timerClosed",						
		"hlsMasterPlaylistUpdated",
		"hlsChildPlaylistUpdated",
		"hlsChunkClosed",
		"hdsMasterPlaylistUpdated",
		"hdsChildPlaylistUpdated",
		"hdsChunkClosed",
		"dashChunkClosed",
		"dashPlaylistUpdated"	
      }, 
    }, 
  }, 

```

The **enabledEvents** parameter is optional and allows you to specify only the events which you wish to receive. **If the enabledEvents section is not specified, all events will be generated.** The list of all possible events can be found above, and more detail on each event can be found in the EMS API Definition document.

The evowebservices rely on EMS Events being generated as follows:

- **RPC – Remote Procedure Calls**

  Event details are transmitted to a remote host via HTTP POST. The EMS will ignore any response from the remote host.

  RPC sink configuration:

  ```
  type="RPC",
  url="http://localhost/evowebservices/evowebservices.php",       -- for php
  url="http://localhost:4000/evowebservices/",                    -- for node     
  serializerType="JSON" 
  ```

  The url field specifies the destination which will be accepting the HTTP POST event notifications. In this example, the web services are installed on the same computer that the EMS is running on (“localhost”). This value can be changed to the IP address of the computer running the web services.



- **serializerType**

  Format for the event logs. The serializerType can in the format of JSON, XML or XMLRPC.

  Sample format of JSON:

  ```
  {"payload":{"creationTimestamp":1349335053486.4370,"name":"","queryTimestamp":1349335053487.4370,"type":"NR","uniqueId":1,"upTime":1.0000},"type":"streamCreated"}
  ```


------

## Related Links

- [EvoWebservices Event](evowebservices_event.html)
- [Event Overview](eventoverview.html)
- [Configuring Event Notifications](eventnotification.html)
- [Event Sinks](eventsinks.html)
- [Application vs. Server Events](eventappvsserver.html)
- [Events List](eventlist.html)
- [Event Definition](eventdefinition.html)
- [Event Logger](userguide_configlua.html#eventLogger)