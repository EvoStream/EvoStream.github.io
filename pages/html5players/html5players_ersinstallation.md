---
title: ERS Installation
keywords: html5
sidebar: html5players_sidebar
permalink: html5players_ersinstallation.html
folder: html5players
toc: true
---



## Pre-requisites

### STUN Server

STUN is a set of methods and network protocols to allow an end host to discover its public IP address even if it’s located behind a NAT. This server is used by ERS to allow both EMS and the client end-point (browser) to discover their respective IP addresses. Restund is the recommended open-source STUN/TURN server to be used with ERS.

The default configuration of ERS already points to a public EvoStream STUN server. However, hosting your own STUN/TURN server is also possible as described below.

To install and host restund on Linux, execute the following instructions:

1. Make sure that build-essential and unzip packages are already installed. On a debian-based Linux, these can be done through the following:

   ```
   apt-get install build-essential
   apt-get install unzip
   ```

2. Download and install the toolkit library to be used by restund:

   ```
   wget http://www.creytiv.com/pub/re-0.4.12.tar.gz
   tar -xzf re-0.4.12.tar.gz
   cd re-0.4.12/
   make
   sudo make install
   ```

3. Download and install restund itself:

   ```
   wget https://github.com/otalk/restund/archive/master.zip
   unzip master.zip
   cd restund-master
   make
   sudo make install
   sudo ldconfig
   ```

4. Configure restund (following is a basic sample config file):

   ```
   #
   # restund.conf
   #
   # core
   #
   daemon no
   debug yes
   realm TestRealmThatCanBeChanged
   syncinterval 600
   udp_listen <ip>:<port>
   udp_sockbuf_size 524288
   tcp_listen <ip>:<port>
   #
   # modules (STUN messages are processed in module loading order)
   #
   module_path /usr/local/lib/restund/modules
   module stat.so
   module binding.so
   module syslog.so
   module status.so
   #
   # syslog
   #
   syslog_facility 24
   ```

5. Copy the updated configuration file:

   ```
   sudo cp restund.conf /etc/
   ```

6. Run restund:

   ```
   sudo restund /etc/restund.conf # add -d option for daemon
   ```


- **Node.JS**

  Node.js is a server side JavaScript runtime utilized to run ERS.

  For Linux/Unix variants, a helper script is available to automate the installation process. See Automatic section.

  For windows platforms and/or manual installation:

  Download and install or extract node.js from their [website](https://nodejs.org/en/download/).

  If extracted, add the Node.JS location to the environment path so that the corresponding binaries can be found even if packages are installed on different folder location.



- **NPM**

  The Node Package Manager allows easy installation of a Node.JS package and its dependencies. NPM will be used to install ERS. NPM is already part of the Node.JS application.



- **PM2**

  Although not necessarily a prerequisite, a Node.JS application/process manager can be installed, as well. This will manage the ERS process and restart it in case of failures and/or machine restart if configured. Currently PM2 is the recommended package for this task.

  This package is already automatically installed through the Linux/Unix helper script as described on Automatic section.

  To manually install PM2 package:

  ```
  npm install -g pm2
  ```






## Installation Procedure

### Manual Installation

Select a location where ERS will be installed and then change directory to that folder. Install ERS through the following command:

```
npm install http://tarballs.evostream.com/ers/ers-<version>.tgz
```

**Example:**

```
npm install http://tarballs.evostream.com/ers/ers-1.0.0.tgz
```


### Automatic Installation

For Linux/Unix platforms, an easy to use script is provided to install Node.JS, PM2 and ERS automatically, and then start ERS using the PM2 node.js application manager.

This script can be download from:

```
http://tarballs.evostream.com/ers/ers-<version>-<OS>-<arch>.sh
```

**Example:**

```
http://tarballs.evostream.com/ers/ers-2.0.0-linux-x64.sh
```

Once downloaded, select the target installation directory, change to that folder, and run the script:

```
sudo ./ers-<version>-<OS>-<arch>.sh
```



## ERS Configuration

A **default** configuration file, `default.json` is included in the `config` folder where ERS was installed (e.g. `INSTALL_DIRECTORY/node_modules/ers/config/default.json`). This file can be modified to customize the settings of ERS.

Following is the content of the `default.json` config file:

```
{
  "server": {
    "port": 4545,
    "secure": false,
    "key": server.key,
    "cert": server.cert,
    "password": null,
    "tokensEnabled": false,
    "webServerEnabled": true,
    "adminAccessEnabled": true,
    "adminIP": "127.0.0.1",
    "adminPort": 3030
  },
  "allowedrooms": [
  ],
  "emsTokens": [
  ],
  "stunservers": [
    {
    "url": "stun:162.209.96.37:55555"
    }
  ],
  "turnservers": [
  ]
}
```



**Field Description**

|      **Name**      |    **Default Value**     | **Description**                          |
| :----------------: | :----------------------: | ---------------------------------------- |
|       server       |            -             | Top level field containing all server related settings |
|        port        |           4545           | Port number where ERS will listen to     |
|       secure       |          false           | Indicates if ERS will use HTTPS instead of regular HTTP |
|        key         |           null           | Private Key file to be used for HTTPS    |
|        cert        |           null           | Certificate file to be used for HTTPS    |
|      password      |           null           | Password of the certificate file         |
|   tokensEnabled    |          false           | Indicates if tokens (a security mechanism) is enabled. This limits viewers who can access available streams of EMS |
|  webServerEnabled  |           true           | Indicates if a web server will be instantiated that enables ERS to serve static files such as html pages containing the video player |
| adminAccessEnabled |           true           | Indicates if admin access used to manage ERS is enabled |
|      adminIP       |        127.0.0.1         | Allowed IP address that can connect to ERS as an admin. This needs to be adjusted to match the actual IP address of the machine used to access the admin APIs of ERS |
|     adminPort      |           3030           | Port number where ERS admin access listens to |
|    allowedrooms    |            -             | List of room names as strings that will only allowed to be created by ERS. Leave this empty to allow any rooms to be created. Or create one room for each running ems instance so that only intended rooms get created which also serves as an additional layer of security |
|     emsTokens      |            -             | Security token of ERS                    |
|    stunservers     | stun:162.209.96.37:55555 | List of STUN servers that ERS can use    |
|    turnservers     |            -             | List of TURN servers that ERS can use    |





## Starting ERS

### Using Node

On the installation folder on ERS, change directory to the `node_modules/ers` folder and execute the following command:

```
node ers.js
```

ERS will then launch with the following message:

```
info: ERS running on port 4545...
info: Webserver port: 4545
info: Admin access port: 3030
```

To stop ERS, simply hit **CTRL-C**.



### Using PM2

On the installation folder on ERS, change directory to the `node_modules/ers` folder and execute the following command:

```
pm2 start ers.js
```

To stop ERS:

```
pm2 stop ers
```