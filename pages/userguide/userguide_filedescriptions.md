---
title: File Descriptions
sidebar: userguide_sidebar
permalink: userguide_filedescriptions.html
folder: userguide
toc: true
---

## Command Files

| File                | Description                              |
| ------------------- | ---------------------------------------- |
| evostreamms(.exe)   | The EvoStream binary itself              |
| evo-webserver(.exe) | The EvoStream Web Server (EWS) binary. This handles the serving of all files over HTTP |
| evo-mp4writer(.exe) | This binary application combines the various pieces of each MP4 recording once the file is ready to be finalized |
| evo-avconv(.exe)    | The EvoStream Transcoder binary. This gets called in reaction to the `transcode` API command |
| run_daemon_ems.sh   | Shell script used on **Linux/Unix** environments to start the EMS as a background application. Use this for production deployments. It requires that the user “evostream” exists, the script will not work without it. Please feel free to modify this script to use a different user. When using the daemon script, to validate that the server is running, you can issue the command `ps –ef` |
| run_console_ems.bat | Batch file/script on **Windows** which runs the EMS as a console application. This is useful for new users as it provides instant feedback on the console when commands are entered and shows errors if they occur in new streams. |
| create.bat          | Script to create a **Windows** service for the EMS. This will also start the EMS as a background process. This must be run with Administrative privileges as it writes to the Windows Registry. *This only needs to be run once.* |
| remove.bat          | Script to remove the **Windows** service for the EMS and remove the relevant Windows Registry entries. This must be run with Administrative privileges. |
| start.bat           | Script to start the EMS **Windows** service. This script will not work if create.bat has not been run first. |
| stop.bat            | Script to stop the EMS **Windows** Service. |
| srvany.exe          | This is a binary provided by Microsoft and is used to create the Windows Service. |



## Configuration Files

| File                | Description                              |
| ------------------- | ---------------------------------------- |
| config.lua          | The main configuration file used by the EMS. The contents of this file are detailed later in this document. |
| webconfig.lua       | The EvoStream Web Server (EWS) configuration file. The contents of this file are detailed later in this document. |
| users.lua           | Defines the valid authentication the server will require when streams are pushed into the EMS. |
| pushPullSetup.xml   | This file is used by the EMS to store stream action commands that are made through the Runtime API. This file may not be modified. At startup, if the EMS detects that the file has been modified it will rename the file and start with a blank/fresh copy. |
| connlimits.xml      | Defines the maximum number of concurrent connections you want the EMS to accept |
| bandwidthlimits.xml | Defines the maximum amount of bandwidth you want the server to be able to use (set the instantaneous bandwidth cap). |



## Documentation

| File                               | Description                              |
| ---------------------------------- | ---------------------------------------- |
| EvoStream Media Server EULA v2.pdf | The End User License Agreement for the EMS |



## Miscellaneous

| File                            | Description                              |
| ------------------------------- | ---------------------------------------- |
| demo/emsdemo.htmldemo/base64.js | The emsdemo.html file can be opened directly in a web browser and provides some example commands which can be sent to the EMS. |
| media/                          | The media directory is the default location for video-on-demand files. This is where the EMS will look when VOD requests are made. This default location can be changed in the EMS main configuration file, which is typically `config/config.lua` |
| logs/                           | This is the directory that EMS will write its logs to. This default location can be changed in the EMS main configuration file, which is typically `config/config.lua` |
| License.lic                     | This is the license file required to run the EMS. It can be placed in the `config/` , `bin/` , or `/etc/evostreamms/` folders, or in whatever folder the evostreamms binary resides. |
| evowebservices.log              | This is an auto-generated file which contains the logs for the evowebservices. The file will be placed in `../evo-webroot/evowebservices`. |

