---
title: Amazon S3 HDS Upload
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_HDSupload.html
folder: evowebservices
toc: false
---



This web service automatically uploads an HDS stream to an Amazon S3 storage instance.

As the EMS writes HDS chunks to disk, this web service uploads those file chunks to your Amazon S3 instance.

Your Amazon S3 access and secret key must be set in the config.ini file.

1. **aws_access_key**. The amazon aws s3 access key

2. **aws_secret_key**. The amazon aws s3 secret key

3. **default_bucket**. The bucket in amazon aws s3 where files will be uploaded

4. **bootstrap**. The bootstrap file included with the fragments

   **Note:** Bootstrap is the bootstrap file which should be included with the HDS chunks. If you are unsure what this should be, it should be left as ‘**bootstrap**’.

   ```
       "AmazonHDSUpload": {
           "plugin_switch": "enabled",
           "parameters": {
               "aws_access_key": "1234567890",
               "aws_secret_key": "ABCDEFGHIJ1234567890",
               "default_bucket": "HDS_files",
               "bootstrap": "bootstrap"
           }
       },

   ```

In this configuration, all the HDS files to be created will automatically be uploaded on the Amazon S3 bucket inside *HDS_files*.

**Note:** All files created when the service is not running will not be included in upload
