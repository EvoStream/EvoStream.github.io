---
title: launchProcess
keywords: api
sidebar: api_sidebar
permalink: launchProcess.html
folder: api
toc: false
---

Allows the user to launch an external process on the local machine. This can be used to do transcoding when paired with applications such as LibAVConv and FFMPEG.



## API Parameter Table



|  Parameter Name  |  Type   | Mandatory |              Default Value               | Description                              |
| :--------------: | :-----: | :-------: | :--------------------------------------: | ---------------------------------------- |
|  fullBinaryPath  | string  |   true    |                  *null*                  | The path to the executable               |
|    keepAlive     | boolean |   false   |                 1 *true*                 | If the process dies for any reason, the EMS will restart the external application when `keepAlive` is 1 |
|    arguments     | string  |   false   |           *zero-length string*           | Complete list of arguments that need to be passed to the process, delimited by ESCAPED SPACES (“\ “) |
|    groupName     | string  |   false   | *if not assigned, will create a random value process_group_xxx* | The group name assigned to the process   |
|  $[ENV]=[VALUE]  | string  |   false   |           *zero-length string*           | Any number of environment variables that need to be set just before launching the process |
| processKillTimer | integer |   false   |                    0                     | Will manually kill the process if it is still running after processKillTimer seconds of process execution |



## API Call Template

``` 
launchProcess parameterA=<value> parameterB=<value> ...
```



### Sample API Call

``` 
launchProcess fullBinaryPath=/home/ems/ffmpeg_preset.sh arguments=10fps\ Stream1\ Stream1_10fps keepAlive=1 $SAMPLE_E_VAR=MyVal
```

This sample command launches a script, named ffmpeg_prest.sh, which presumably contains a shell-script that will run FFMPEG with a specific set of parameters.

The arguments field passes the three values (“10fps”, “Stream1”, “Stream1_10fps”) to the ffmpeg_preset.sh script. In this example, these parameters might tell this hypothetical script to transcode Stream1 to be only 10 frames-per-second, and then name the resultant stream “Stream1_10fps”.

The final parameter is an example for setting an environment variable (SAMPLE_E_VAR set to MyVal) on the command line prior to script/binary execution.



### Success Response in JSON

``` 
{
   "data":{
      "$SAMPLE_E_VAR":"MyVal",   
      "arguments":"10fps\ Stream1\ Stream1_10fps",
      "configId":1,
      "fullBinaryPath":"/home/ems/ffmpeg_preset.sh",
      "groupName":"process_group_UHBqMT6C",
      "keepAlive":true,
      "operationType":6
      "processKillTimer":0
   },
   "description":"Process enqueued for start",
   "status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse.
  - $[ENV]=[VALUE] – Any number of environment variables that need to be set just before launching the process
  - arguments – Complete list of arguments that need to be passed to the process
  - configID – The configuration ID for this command
  - fullBinaryPath – Full path to the binary that needs to be launched
  - groupName - The group name assigned to the process
  - keepAlive – If `keepAlive` is set to 1, the server will restart the process if it exits
  - operationType – The type of operation
  - processKillTimer – Will manually kill the process if it is still running after processKillTimer seconds of process execution
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- If process has processKillTimer and keepAlive of true, the process will be called again after it was killed by the processKillTimer because of the keepAlive mechanism