---
title: Adding Streams
sidebar: userguide_sidebar
permalink: userguide_add.html
folder: userguide
toc: true
---

This is where you can add a stream to your EMS. You can add simple streams and HTTP streams in this page.



## Adding Inbound Live Streams

This is similar to the `pullStream` command. If you wan't to add a RTSP or RTMP stream, simply do the following:

1. Choose  **Inbound Live Stream** under Choose the Stream Type to Add

2. Enter the **URI Stream Source**

3. Enter the **Local Stream Name**

4. Click **Add Stream**

   ![](images/userguide/addstream.JPG)

   ​

**Notes:**

- ![](images/userguide/clear.JPG)  - will clear inputs in fields

- ![](images/userguide/viewstream.JPG)   - redirects to Active to view the stream in list

See [pullStream](api_pullStream.html) API for more information.



## Adding HTTP Streams

Adding HTTP streams has made easy in this page. You can now create your HLS, DASH, HDS and MSS here.

1. Choose the  **HTTP Stream Type** (HLS, DASH, HDS, MSS)

2. Choose the **Stream Source**

   **Note:** List of Active streams will be shown under the Stream Source field. You can select more than one

3. Enter **Target Folder**

   **Note:** Should use absolute path 

4. Enter **Group Name**

5. Enter **Chunk Length**

6. Enter **Bitrate** (optional)

7. Click **Add Stream**

![](images/userguide/addhttpstream.JPG)



**Notes:**

- ![](images/userguide/clear.JPG)   - will clear inputs in fields
- ![](images/userguide/viewstream.JPG)   - redirects to Active to view the stream in list


