---
title: Connecting to Web UI
sidebar: userguide_sidebar
permalink: userguide_connectui.html
folder: userguide
toc: true
---

Once EMS is started, you can now connect to its UI. There are several ways to start the UI:

## Starting EMS Web UI

### Via Console

Starting the Web UI using `run_console_webui` will open a separate console for the Web UI. This is very helpful if you want to see solely logs from the Web UI. 

1. Run `run_console_webui.sh` in Linux,  `run_console_webui.bat` in Windows

   ![](images/userguide/startui_console.jpg)

   ​

   **Note:**

   - You may configure the logging level of UI in `../node-webui/config/logging.json`



### Via Daemon

For Linux environment only, running Web UI via Daemon mode is also available. This will not show a console showing the logs of the activities of the Web UI.  

1. Run `run_daemon_webui.sh`

   **Note:**

   - Run ***ps -ef|grep node*** to see if Web UI is running, you should see `./evo-node node-webui/bin/webui_activate` in the result
   - You may check the Web UI logs in `../node-webui/logs/`
   - The configuration of the log level is the same with console logs and file logs



### Via Service

Same with EMS, you may add a Web UI service in Windows Registry. Running Web UI via service is like running the Web UI in Daemon mode on Linux environment.

1. Create the service first

   a. Open a command prompt

   b. Locate the services folder: `C:\EvoStream\services\webui`

   c. Send command: `create.bat`

   ```
   C:\EvoStream\services\webui> create_webui_service.bat
   ```

   or run as Administrator the `create_webui_service.bat` in the location

   d. A confirmation will be asked, click **Yes**

   ![](images/userguide/register.JPG)

   e. EMS keys are now registered! Click **OK**

   ![](images/userguide/register_success.JPG)

   f. Verify the registration by checking in `Control Panel > Administrative  Tools > Services`

   ![](images/userguide/service_ui_.jpg)




## Stopping Web UI

The EMS Web UI process will not be killed when EMS is stopped. You may still access the Web UI but will not be able to do show the EMS functionalities.



### Stopping Console UI

If you run the UI using the `run_console_webui.bat` or `run_console_webui.sh` or `run_daemon_ems.sh`:

1. Run run_stop_webui.bat in Windows or run_stop_webui.sh in Linux

   ```
   $ ./run_stop_webui.sh 
   webui will now be stopped
   ```

This will end the process of the WebUI running in Console.



### Stopping Web UI Service

If you Start the Web UI as a service (for Windows only):

1. Go to Services, click on the EMS Web UI service entry

2. Click **Stop**

   or go to the services folder of EMS Web UI, double click on `stop_webui_service.bat`