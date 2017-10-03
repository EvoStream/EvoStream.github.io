---
title: Configuring the EMS Web Service Plugins
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_pluginconfiguration.html
folder: evowebservices
toc: false
---



Every EMS Web Service is contained within a “**plugin**”. Each plugin can be enabled or disabled, effectively turning on and off each web service. The EMS Web Service system allows many Web Service Plugins to be active at one time, allowing users to create an entire suite of features.



## A. Configuration file (config.ini/plugins.json)

The EMS Web Services has a primary configuration file for the plugins.

**For php:** evowebservices > config > config.ini

**For node:** evowebservices > config > plugins.json

Turn on a plugin by changing the **disabled** to **enabled**. By default all plugins are disabled.

Plugin Configuration:

```
StreamLoadBalancer = disabled 
StreamAutoRouter = disabled
StreamRecorder = disabled
AmazonHDSUpload = disabled
AmazonHLSUpload = disabled 

```

See [EMS Web Service Plugins](http://docs.evostream.com/ems_web_services_user_guide/ems_web_services_plugins) for the detailed information of plugins.



## B. Logging (logging.json)

Available only on node. This is the configuration for the evowebservices log files and the log console. Go to **evowebservices > config > logging.json** for configuration.

Configuration options for logging:

```
{
  "options": {
    "level": "silly",    
    "handleExceptions": true,
    "json": false,
    "maxsize": 5242880
  }

```

- level - the logging level for logs

  There are 6 default levels in winston:

  ```
  level 0 = silly (lowest)
  level 1 = debug
  level 2 = verbose
  level 3 = info
  level 4 = warn
  level 5 = error (highest)

  ```

- handleExceptions - Handling Uncaught Exceptions with winston

- json - log files are in json format otherwise log files are saved as string format

- maxsize - maximum size of the log file in KB