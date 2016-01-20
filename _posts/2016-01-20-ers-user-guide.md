---
title: ERS User Guide
layout: post
date:   2016-01-01 00:00:00 +0000
categories: jekyll update
permalink: ers_user_guide
---

# Document Definitions

| **TERM** | **DEFINITION** |
| --- | --- |
| EMS | EvoStream Media Server |
| JSON | JavaScript Object Notation |
| NAT | Network Address Translators |
| Room | A logical place where a single EMS joins and waits for incoming clients (web browsers) to connect/join.If there are 10 IP cameras that has a running EMS on each of those cameras, 10 unique rooms will be created by these EMS as they connect to ERS. If an EMS attempts to connect to a room already joined by another EMS instance, the last EMS will not be allowed to join this room.Rooms can be limited by having entries on _allowedrooms_ field of the configuration file (config/default.json) upon ERS start-up. Or they can be added upon run-time through the _ **addRoom** _ admin command. |
| STUN | Session Traversal Utilities for NAT |
| Token | A valid identifier passed by a connecting client (browser) to ERS to indicate that it has the appropriate permission to access the streams available on EMS of a specified room. This token will be available within 10 minutes after it is used by a client and will be removed once the 10 minute mark has expired. Once used, other clients using the same token will not be able to join a room.This prevents unwanted access to the available streams of a running EMS instance. Tokens can be added using the _ **addToken** _ admin command. |
| TURN | Traversal Using Relays around NAT |
| WebRTC | Web Real-Time Communication |

# Purpose

This document provides instructions on how to use the EvoStream Rendezvous Server. It covers installation, configuration and usage

This document is written for users of the EvoStream Rendezvous Server.

# EvoStream Rendezvous Server (ERS)

## What is ERS?

EvoStream Rendezvous Server allows EMS and client browser to be able to meet and communicate with each other without knowing each other's IP addresses. It acts as the signaling server needed to establish connection between these endpoints.

## Key Features

- Acts as signaling server
- Capable of serving static html pages
- Protect streams through tokens

## Pre-requisites

### STUN Server

STUN is a set of methods and network protocols to allow an end host to discover its public IP address even if it's located behind a NAT. This server is used by ERS to allow both EMS and the client end-point (browser) to discover their respective IP addresses. Restund is the recommended open-source STUN/TURN server to be used with ERS.

The default configuration of ERS already points to a public EvoStream STUN server. However, hosting your own STUN/TURN server is also possible as described below.

To install and host restund on Linux, execute the following instructions:

1. Make sure that build-essential and unzip packages are already installed. On a debian-based Linux, these can be done through the following:

        apt-get install build-essential
        apt-get install unzip

1. Download and install the toolkit library to be used by restund:

        wget http://www.creytiv.com/pub/re-0.4.12.tar.gz
        tar -xzf re-0.4.12.tar.gz
        cd re-0.4.12/
        make
        sudo make install

1. Download and install restund itself:

        wget https://github.com/otalk/restund/archive/master.zip
        unzip master.zip
        cd restund-master
        make
        sudo make install
        sudo ldconfig

1. Configure restund (following is a basic sample config file):

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

1. Copy the updated configuration file:

        sudo cp restund.conf /etc/

1. Run restund:

        sudo restund /etc/restund.conf # add -d option for daemon

### Node.JS

Node.js is a server side JavaScript runtime utilized to run ERS.

For Linux/Unix variants, a helper script is available to automate the installation process. See Automatic section.

For windows platforms and/or manual installation:

Download and install or extract node.js from their website: [https://nodejs.org/en/download/](https://nodejs.org/en/download/)

If extracted, add the Node.JS location to the environment path so that the corresponding binaries can be found even if packages are installed on different folder location.

### NPM

The Node Package Manager allows easy installation of a Node.JS package and its dependencies. NPM will be used to install ERS. NPM is already part of the Node.JS application.

### PM2

Although not necessarily a prerequisite, a Node.JS application/process manager can be installed, as well. This will manage the ERS process and restart it in case of failures and/or machine restart if configured. Currently PM2 is the recommended package for this task.

This package is already automatically installed through the Linux/Unix helper script as described on Automatic section.

To manually install pm2 package:

    npm install -g pm2

# Installation

## Manual

Select a location where ERS will be installed and then change directory to that folder. Install ERS through the following command:

    npm install http://tarballs.evostream.com/ers/ers-<version>.tgz


For example:

    npm install http://tarballs.evostream.com/ers/ers-1.0.0.tgz

## Automatic

For Linux/Unix platforms, an easy to use script is provided to install Node.JS, PM2 and ERS automatically, and then start ERS using the PM2 node.js application manager.

This script can be download from `http://tarballs.evostream.com/ers/ers-<version>-<OS>-<arch>.sh` (e.g. `http://tarballs.evostream.com/ers/ers-1.0.0-linux-x64.sh`).

Once downloaded, select the target installation directory, change to that folder, and run the script:

    sudo ./ers-<version>-<OS>-<arch>.sh

# Configuration

## Default

A default configuration file, `default.json` is included in the `config` folder where ERS was installed (e.g. INSTALL_DIRECTORY/node_modules/ers/config/default.json). This file can be modified to customize the settings of ERS.

Following is the content of the `default.json` config file:

    {
      "server": {
        "port": 3535,
        "secure": false,
        "key": null,
        "cert": null,
        "password": null,
        "tokensEnabled": false,
        "webServerEnabled": true,
        "adminAccessEnabled": true,
        "adminIP": "127.0.0.1",
        "adminPort": 3030
      },
      "allowedrooms": [
      ],
      "stunservers": [
        {
        "url": "stun:162.209.96.37:55555"
        }
      ],
      "turnservers": [
      ]
    }

## Field Description

| **Name** | **Default Value** | **Description** |
| --- | --- | --- |
| server |  | Top level field containing all server related settings. |
| port | 3535 | Port number where ERS will listen to. |
| secure | false | Indicates if ERS will use HTTPS instead of regular HTTP. |
| key | null | Private Key file to be used for HTTPS. |
| cert | null | Certificate file to be used for HTTPS. |
| password | null | Password of the certificate file. |
| tokensEnabled | false | Indicates if tokens (a security mechanism) is enabled. This limits viewers who can access available streams of EMS. |
| webServerEnabled | true | Indicates if a web server will be instantiated that enables ERS to serve static files such as html pages containing the video player. |
| adminAccessEnabled | true | Indicates if admin access used to manage ERS is enabled. |
| adminIP | 127.0.0.1 | Allowed IP address that can connect to ERS as an admin. This needs to be adjusted to match the actual IP address of the machine used to access the admin APIs of ERS. |
| adminPort | 3030 | Port number where ERS admin access listens to. |
| allowedrooms |  | List of room names as strings that will only allowed to be created by ERS. Leave this empty to allow any rooms to be created. Or create one room for each running ems instance so that only intended rooms get created which also serves as an additional layer of security. |
| stunservers |  | List of STUN servers that ERS can use. |
| turnservers |  | List of TURN servers that ERS can use. |

# Start-up

## Using Node

On the installation folder on ERS, change directory to the _node_modules/ers_folder and execute the following command:

    node ers.js

ERS will then launch with the following message:

    info: ERS running on port 3535...
    info: Webserver port: 3535
    info: Admin access port: 3030


To stop ERS, simply hit **CTRL-C**.

## Using PM2

On the installation folder on ERS, change directory to the _node_modules/ers_folder and execute the following command:

    pm2 start ers.js

To stop ERS:

    pm2 stop ers

# API

A set of APIs are available to manage ERS and allow the actual generation and deletion of tokens and rooms. These APIs are accessible through an HTTP GET request with the following format:

    http(s)://<ERS IP>:<ERS adminPort>/?c=<commandName>&i=<Id>

Where:

| **Field** | **Description** |
| --- | --- |
| ERS IP | IP address of the machine hosting ERS |
| ERS adminPort | Port number where admin APIs can be accessed |
| commandName | Name of the actual command |
| Id | Value of the parameter, either token ID or room ID |

For example, an ERS running on the same machine where the request is being generated from (default setup) can use the following:

    http://127.0.0.1:3030/?c=addToken&i=thisIsASampleToken

This HTTP GET request can be sent through any scripting language desired.

An example admin interface which uses Javascript to send out this request can be accessed through:

    http://127.0.0.1:3030/ersadmin.html

## Get Version

Returns the current version of ERS.

| **Field** | **Value** |
| --- | --- |
| Command Name | version |
| Parameter Id | (ignored) |

Example:

    http://127.0.0.1:3030/?c=version

## Add Token

Adds a token that can be used later by a client trying to connect with EMS.

| **Field** | **Value** |
| --- | --- |
| Command Name | addToken |
| Parameter Id | `<token Id>` |

Example:

    http://127.0.0.1:3030/?c=addToken&i=tokenId

## Delete Token

Deletes an existing token.

| **Field** | **Value** |
| --- | --- |
| Command Name | delToken |
| Parameter Id | `<token Id>` |

Example:

    http://127.0.0.1:3030/?c=delToken&i=tokenId

## List Tokens

Displays all created tokens currently active.

| **Field** | **Value** |
| --- | --- |
| Command Name | listTokens |
| Parameter Id | (ignored) |

Example:

    http://127.0.0.1:3030/?c=listTokens

## Add Room

Adds an allowed room to the list during runtime. This command also effectively prevents creation of rooms not included on the list.

| **Field** | **Value** |
| --- | --- |
| Command Name | addRoom |
| Parameter Id | `<room ID>` |

Example:

    http://127.0.0.1:3030/?c=addRoom&i=roomId

## Delete Room

Deletes a room added from the list.

| **Field** | **Value** |
| --- | --- |
| Command Name | delRoom |
| Parameter Id | `<room ID>` |

Example:

    http://127.0.0.1:3030/?c=delRoom&i=roomId

## List Rooms

Displays all rooms with their corresponding descriptions and status.

| **Field** | **Value** |
| --- | --- |
| Command Name | listRooms |
| Parameter Id | (ignored) |

Example:

    http://127.0.0.1:3030/?c=listRooms
