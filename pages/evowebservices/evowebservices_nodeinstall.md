---
title: Installation Using Node.js
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_nodeinstall.html
folder: evowebservices
toc: false
---



## Pre-requisites:

- Node.js
- npm
- EMS (events enabled)




## Getting evowebservices

### A. Windows

1. **Download** the evowebservices Windows batch file installer from our Github

   Link: [https://github.com/EvoStream/evowebservices-archives/tree/master/installers](https://github.com/EvoStream/evowebservices-archives/tree/master/installers)

2. Double click on the .bat file to **install** evowebservices

   ```
   evowebservices-0.0.1-win-x64.bat
   ```

3. If the installation is successful, evowebservices will start automatically

   ```
   starting evowebservices using npm....
      
   > evowebservices@0.0.0 start C:\node_evowebservices\node_modules\evowebservices
   > node ./bin/www
      
   STARTED: evowebservices:server Listening on port 4000
   info: STARTED: evowebservices:server Listening on port 4000
   info: Get enabled Plugins
   ```

   ​

###  B. Linux Installation

1.  **Download** the evowebservices Bash Script file installer from our Github.

   Link: [https://github.com/EvoStream/evowebservices-archives/tree/master/installers](https://github.com/EvoStream/evowebservices-archives/tree/master/installers)

2. Locate the installer file, **install** the script by typing this in terminal:

   ```
   ./evowebservices-0.0.1-linux-x64.sh
   ```

3. If the installation is successful, evowebservices will start automatically

   ```
   Starting EVOWEBSERVICES...
      
   > evowebservices@0.0.0 start /home/user/Desktop/node_modules/evowebservices
   > node ./bin/www
      
   STARTED: evowebservices:server Listening on port 4000 
   info: STARTED: evowebservices:server Listening on port 4000 
   info: Get enabled Plugins
   ```

   ​

## Starting evowebservices:

1. Run the evowebservices before starting EMS. Make sure the plugins in evowebservices is configured as well as the event notification system in the config.lua of the EMS.

2. Open your node command prompt and go to your evowebservices directory. Start the evowebservices by executing command:

   ```
   npm start
   ```

**Note:** You may check the node console terminal and evowebservice log for errors. The evowebservices log is located on the evowebservices/logs directory
