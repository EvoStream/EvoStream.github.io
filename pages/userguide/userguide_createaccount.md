---
title: Create Local Account
keyword: create account
sidebar: userguide_sidebar
permalink: userguide_createaccount.html
folder: userguide
toc: false
---

To access the EMS Web UI, a user should have a local account, or a Facebook account, or a Google+ account. You have the option to create a local account using your **email address** or, just log in via **Facebook** account or **Google+** account. 

To proceed with creating an account, go in this URL: `<EMSIPaddress>:4100`

![](images/userguide/signup.JPG)



## Create Local Account

To add a local account using an email address:

1. Enter the **email address** and **password** to be used

   ![](images/userguide/email.JPG)

2. Click **Create Account**

   ![](images/userguide/accountcreationsuccess.JPG)



**Notes:** 

- Only one local account can be created. 
- If you want to change the email registered, you need to delete the **user.json** file in `node_modules\ems_web_ui\data`. This will remove the registered email and linked social media accounts in use.