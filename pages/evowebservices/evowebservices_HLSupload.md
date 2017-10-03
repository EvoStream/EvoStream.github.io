---
title: Amazon S3 HLS Upload
keywords: webservices
sidebar: evowebservices_sidebar
permalink: evowebservices_HLSupload.html
folder: evowebservices
toc: false
---



This web service automatically uploads an HLS stream to an Amazon S3 storage instance.

As the EMS writes HLS chunks to disk, this web service uploads those file chunks to your Amazon S3 instance.

Your Amazon S3 access and secret key must be set in the config.ini file.

1. **aws_access_key**. The amazon aws s3 access key

2. **aws_secret_key**. The amazon aws s3 secret key

3. **default_bucket**. The bucket in amazon aws s3 where files will be uploaded

   ```
       "AmazonHLSUpload": {
           "plugin_switch": "enabled",
           "parameters": {
               "aws_access_key": "1234567890",
               "aws_secret_key": "ABCDEFGHIJ1234567890",
               "default_bucket": "HLS_files",
           }
       },

   ```

In this configuration, all the HLS files to be created will automatically be uploaded on the Amazon S3 bucket inside *HLS_files*.

**Note:** All files created when the service is not running will not be included in upload​
