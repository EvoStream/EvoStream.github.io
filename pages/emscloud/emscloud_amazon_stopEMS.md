---
title: Stopping/Terminating EMS
keywords: amazon
sidebar: emscloud_sidebar
permalink: emscloud_amazon_stopEMS.html
folder: emscloud
toc: false
---

According to Amazon, *"You can stop and restart your instance if it has an Amazon EBS volume as its root device."*

If you are not using the EMS anymore, it is highly recommended to STOP or TERMINATE the instance to avoid unnecessary charges. When you terminate an instance, you'll lose all changes or files that you have on the server. If you have anything that you don't want to lose, be sure to save it to Amazon Simple Storage Service (Amazon S3) before terminating the instance or you'll lose your data. 

After you've saved your data, do the following to stop or terminate an instance:

1. **Log in** to your AWS account.

2. In the Navigation pane, under Instances, click **Instances**.

3. Select the running instance(s) that you want to terminate.

4. Click the **Actions** button, and then click on **Stop** or **Terminate**. Confirm the termination. The Instance State column for the selected instance(s) will show if the instance is shut down or terminated.

   ![](images/emscloud/stopter.jpg)



- **EMS Stopped Instance**

  ![](images/emscloud/stop.jpg)


- **EMS Terminated Instance**

  ![](images/emscloud/terminate.jpg)

**Note:** Amazon recommends that you confirm the machine reaches the terminated state before signing out. Charges will continue to accrue for instances that fail to shut down. See Amazon documentation on stopping and terminating [here](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Stop_Start.html).