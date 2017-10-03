---
title: Record a Stream
keywords: record
sidebar: userguide_sidebar
permalink: userguide_record.html
folder: userguide
toc: true
---

Records any inbound stream. The record command allows users to record a stream that may not yet exist. When a new stream is brought into the server, it is checked against a list of streams to be recorded.

Streams can be recorded as FLV files, MPEG-TS files or as MP4 files.

**Note:** If you wan't to record the very first frames in your stream, you need to issue the `record` command first before adding the stream to be recorded. This will make sure that there will be no lost frames  



## How To

### Recording MP4 File

This is the default format of the `record` command.

**General Format:**

```
record localstreamname=<localstreamname> pathtofile=../path_to_media/filename type=<fileType>
```

- **For Windows:**

  ```
  record localstreamname=myStream pathtofile=C:\EvoStream\media\myRecord type=mp4
  ```


- **For Linux Package:**

  ```
  record localstreamname=myStream pathtofile=/var/evostreamms/myRecord type=mp4
  ```

- **For Linux Archive:**

  ```
  record localstreamname=myStream pathtofile=/path_to_media/myRecord type=mp4
  ```

To make the call easier, a **relative path** can be used:

```
record localstreamname=myStream pathtofile=../media/myRecord type=mp4
```

The created files will automatically save in the folder declared in `pathtofile`.

```
media:                           --> targetfolder
-testRecord.mp4.info             --> mp4 file on creation                     
-testRecord.mp4.mdat             --> mp4 file on creation               
-testRecord.mp4.track1           --> mp4 file on creation   
-testRecord.mp4.track2           --> mp4 file on creation   
```

If the stream source ended or disconnected, the MP4 files will be compiled as one MP4 file: See [MP4 File Creation](userguide_record.html#mp4-file-creation).

```
media:                           --> targetfolder
-testRecord.mp4                  --> completed mp4 file
```

If `chunkLength` parameter is added:

```
media:                           --> targetfolder
-testRecord_part0000.mp4 	    --> completed mp4 file chunk
-testRecord_part0001.mp4.info    --> mp4 file on creation                    
-testRecord_part0001.mp4.mdat    --> mp4 file on creation          
-testRecord_part0001.mp4.track1  --> mp4 file on creation   
-testRecord_part0001.mp4.track2  --> mp4 file on creation   
```



#### MP4 File Creation

When recording to an MP4 file format the EMS will create three (if video or audio only stream) or four (if sream has audio and video) different files:

- filename.info

- filename.mdat

- filename.track1

- filename.track2 (only if audio and video)

  These files will all exist within the destination folder specified in the Record command issued.

  At the end of recording, or when the recording file is closed by the EMS to start a new chunk, the EMS will automatically combine these files into the final .mp4 file. This is done to ensure optimal MP4 file formatting with the header “atoms” at the beginning of the file.

  The EMS uses the **evo-mp4writer** binary to perform the combination of files into the final MP4 file.

  If for any reason an MP4 file fails to be combined you can manually use the evo-mp4writer binary to create the MP4 file. Typically this failure to combine will only occur if the EMS or the server itself is shutdown mid-record and so the evo-mp4writer is not given a chance to run.

  The syntax for the evo-mp4writer is as follows:

  ```
  evo-mp4writer -path=/path/to/file.mp4
  ```

  The `-path` parameter here should be the same as was used in the record `pathtofile` parameter.

  If the above command fails, you can add a `--recovery` parameter to the end to provide some additional resiliency:

  ```
  evo-mp4writer -path=/path/to/file.mp4 --recovery
  ```

  **Note:**  `--recovery` option is going to be deprecated in the upcoming 1.7.0 revision or in 1.7.1. Previously this option is useful in saving time as it only needs to re write the ftyp and moov atom without changing the mdat. Since both moov and mdat are reordered in our internal codebase, both of them needs to be re-written always in the event that evo-mp4writer is invoked manually.

  ​

### Recording TS File

**General Format:**

```
record localstreamname=<localstreamname> pathtofile=../path_to_media/filename type=<fileType>
```

- **For Windows:**

  ```
  record localstreamname=myStream pathtofile=C:\EvoStream\media\myRecord type=ts
  ```

- **For Linux Package:**

  ```
  record localstreamname=myStream pathtofile=/var/evostreamms/myRecord type=ts
  ```

- **For Linux Archive:**

  ```
  record localstreamname=myStream pathtofile=/path_to_media/myRecord type=ts
  ```

To make the call easier, a **relative path** can be used:

```
record localstreamname=myStream pathtofile=../media/myRecord type=ts
```

The created files will automatically save in the folder declared in `pathtofile`.

```
media:                           --> targetfolder
-testRecord.ts  		       --> ts file         
```

If `chunkLength` parameter is added:

```
media:                           --> targetfolder
-testRecord_part0000.ts          --> ts file chunk                     
-testRecord_part0001.ts          --> ts file chunk          
-testRecord_part0002.ts          --> ts file chunk         
-testRecord_part0003.ts          --> ts file chunk       
...
```

The length of the recorded TS files will depend on the `chunkLength` declared. If the stream source is ended or disconnected, the TS files will remain as it is. 



### Recording FLV File

**General Format:**

```
record localstreamname=<localstreamname> pathtofile=../path_to_media/filename type=<fileType>
```

- **For Windows:**

  ```
  record localstreamname=myStream pathtofile=C:\EvoStream\media\myRecord type=flv
  ```

- **For Linux Package:**

  ```
  record localstreamname=myStream pathtofile=/var/evostreamms/myRecord type=flv
  ```

- **For Linux Archive:**

  ```
  record localstreamname=myStream pathtofile=/path_to_media/myRecord type=flv
  ```

To make the call easier, a **relative path** can be used:

```
record localstreamname=myStream pathtofile=../media/myRecord type=flv
```

The created files will automatically save in the folder declared in `pathtofile`.

```
media:                           --> targetfolder
testRecord.flv                   --> flv file
```

If `chunkLength` parameter is added:

```
media:                            --> targetfolder
-testRecord_part0000.flv          --> flv file chunk                     
-testRecord_part0001.flv          --> flv file chunk          
-testRecord_part0002.flv          --> flv file chunk         
-testRecord_part0003.flv          --> flv file chunk       
...
```

The length of the recorded FLV files will depend on the `chunkLength` declared. If the stream source is ended or disconnected, the FLV files will remain as it is. 



## JSON CLI Response

**API Call:**

```
record localStreamName=testpullstream pathtofile=../media/testRecord type=mp4 overwrite=1
```

**JSON Response:**

```
Command entered successfully!
Recording Stream

    chunkLength: 0
    configId: 5
    localStreamName: testpullstream
    pathToFile: ../media/testRecord
    type: mp4
```



## Stopping a Record

A recorded stream is just like any other stream in the EMS, it is simply directed to a file instead of towards the network. Users may therefore use either of the normal shutdown stream commands to stop a recording. This will cause the recording of this stream to stop, which will close the file that is being written to. All data that had previously been recorded will remain stored in that file. If the stream had not yet been recorded (because a stream with that name was not yet available) then the recording will be canceled.

------

## Related Links

- [record API](api_record.html)
- [Stream Recorder Service](evowebservices_streamrecorder.html)