---
title: Starting EvoStream Media Server
keyword: start ems
sidebar: userguide_sidebar
permalink: userguide_startems.html
folder: userguide
toc: true
---



## Linux Distributions (Linux apt/yum Installer)

Running EMS as a service:

```
# service evostreamms start
```
or
```
# service evostreamms start_console
```

**What's the difference?** If you run EMS using `start_console`, it will show logs on the console where you run the EMS. Starting it with `start`  will not show logs in the console. 

You can also do restart by sending: 

```
# service evostreamms restart
```





## Linux, Mac OSX and BSD Distributions (.tar.gz Distribution)

There are two “run” scripts that can be used to start the EvoStream Media Server, just locate the `./bin` folder of EMS and execute the command:

1. Run EMS with console logs, using `./config/config.lua` as the main server configuration. 

   ```
    $ ./run_console_ems.sh
   ```

2. Run EMS as a background process. The script will attempt to assign the run-process to the user `evostream`.

   ```
    $ ./run_daemon_ems.sh

   ```

**Notes:**

- Either command can be directly executed.
- For `run_daemon_ems.sh`, if the `evostream` user does not exist, an error will be printed to the screen. Despite the error, the EMS will probably have been started. To check if the server is running, user can issue `ps –ef | grep evostream` in terminal.

This command will print differently on different operating systems, but it should let you know that the server is running.

- The **user** used by `run_daemon_ems.sh` can easily be modified by changing the value after the `-u` in the script itself.
- The user running the EvoStream Media Server must have sufficient permission to open and bind to network ports.




## Windows Distribution

The EMS may be started using the **Windows Services** tool in Windows.

### Via Service

**Pre-requisite:**

It is needed to add EMS into your Window's registry to enable the use of service.

1. Open a command prompt

2. Locate the services folder: `C:\EvoStream\services\ems`

3. Send command: `create.bat`

   ```
   C:\EvoStream\services\ems> create.bat
   ```
   **Note:** You can also double click the batch file to run

   ​

4. A confirmation will be asked, click **Yes**

  ![](images/userguide/register.JPG)

  ​

5. EMS keys are now registered! Click **OK**

  ![](images/userguide/register_success.JPG)

  ​

6. Verify the registration by checking in `Control Panel > Administrative  Tools > Services`

  ![](images/userguide/registry_services.jpg)



**Starting the Service**

1. Open a command prompt

2. Locate the services folder: `C:\EvoStream\services\ems`

3. Send command: `start.bat`

   This will start the service if it has not already been started

   ​


**Notes:**

- Call `stop.bat` to stop the running EMS service
- Use the `remove.bat` command if you opt to remove EMS in the registry





### Via Shortcut Icon

User may directly run the EMS using the shortcut icon if added during installation

 ![](images/userguide/emsShortcut.jpg)

This will open a console running EMS.

The shotcut icon calls the `run_console_ems.bat`. You may also run this executable found in the installed EMS. Simply double-clicked to start the server. This script simply runs the Media Server through the command prompt, using `config/config.lua` as the main server configuration. 

```
C:\EvoStream\run_console_ems.bat
```



## Startup Success

For either Windows or Linux/BSD/OSX, when you run the EMS as a console application, you should see the following screen indicating the server is up and running:

![](images/userguide/start1.png)

**Tip!** A successful EMS start will show GO! GO! GO! in console.



## EMS Command Line Definition

The evostreamms executable can be run with a few different options. The command line signature is as follows:

**Format:** evostreamms [OPTIONS][config_file_path]

| Command                          | Function                                 |
| -------------------------------- | ---------------------------------------- |
| `–help`                          | Prints this help and exit.               |
| `–version`                       | Prints the version and exit.             |
| `–use-implicit-console-appender` | Adds extra logging at runtime, but is only effective when the server is started as a console application. This is particularly useful when the server starts and stops immediately for an unknown reason. It will allow you users to see if something is wrong, particularly with the config file. |
| `–daemon`                        | Overrides the daemon setting inside the config file and forces the server to start in daemon mode. |
| `–uid=`                          | Run the process with the specified user id. |
| `–gid=`                          | Run the process with the specified group id. |
| `–pid=<pid_file>`                | Create PID file. Works only if –daemon option is specified. |

------

## Notes

- Starting EMS will also start the following:

  - EMS Web Server
  - EMS Web UI
  - EMS Webservices

- You can configure the startup processes in config.lua

  - [runWebServer](userguide_configlua.html#runwebserver)

  - [runWebUI](userguide_configlua.html#runwebui)

  - [eventLogger](userguide_configlua.html#eventlogger)

    ​