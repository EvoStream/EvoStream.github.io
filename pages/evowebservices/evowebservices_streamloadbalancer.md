---
title: Stream Load Balancer
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_streamloadbalancer.html
folder: evowebservices
toc: false
---



The Load Balancer web service ensures that a group of EMS instances maintain the same collection of inbound (source) streams.

When a new stream is created on one EMS, this web service will tell all the other EMS instances to also to and get that stream.

The list of EMS instances the Load Balancer will maintain is defined in the config.ini file:

1. **destination_uri**. The array of ip address where the inbound streams would be replicated to

   ```
       "StreamLoadBalancer": {
           "plugin_switch": "enabled", 
           "parameters": {
               "destination_uri": [
                   "192.168.2.3",
                   "192.168.2.4",
                   "192.168.2.5"
               ]
           }

   ```

In this configuration, all the server IPs listed *(192.168.2.3, 192.168.2.4, 192.168.2.5)* will have the same pulled streams as the host EMS.

To verify, do `listconfig` in all destination IPs. All pulled streams from the host EMS should also be pulled by the destination servers.



