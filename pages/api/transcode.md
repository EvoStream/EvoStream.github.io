---
title: transcode
keywords: api
sidebar: api_sidebar
permalink: transcode.html
folder: api
toc: false
---



This function changes the compression characteristics of an audio and/or video stream. This function allows you to change the resolution of a source stream, change the bitrate of a stream, change a VP8 or MPEG2 stream into H.264 and much more. This function will also allow users to create overlays on the final stream as well as crop streams.

**Transcoding requires SIGNIFICANT computing resources and will severely impact performance. A general guideline is that you can accomplish one transcoding job per CPU core for HD streams.**



## API Parameter Table

|     **Parameter Name**      |  Type   | **Mandatory** |        **Default Value**         | **Description**                          |
| :-------------------------: | :-----: | :-----------: | :------------------------------: | ---------------------------------------- |
|           source            | string  |     true      |              *null*              | Can be a URI or a local stream name from EMS |
|        destinations         | string  |     true      |              *null*              | The target URI(s) or stream name(s) of the transcoded stream. If only a name is given, it will be pushed back to the EMS |
|      targetStreamNames      | string  |     false     |  transcoded_xxxx *(timestamp)*   | The name of the stream(s) at destination(s). If not specified, and a full URI is provided to destinations, name will have a time stamped value |
|          groupName          | string  |     false     | transcoded_group_xxxx *(random)* | The group name assigned to this process. If not specified, `groupName` will have a random value |
|        videoBitrates        | integer |     false     |      input video's bitrate       | Target output video bitrate(s) (in bits/s, append '**k**' to value for kbits/s). Accepts the value '**copy**' to copy the input bitrate. An empty value passed would mean no video |
|         videoSizes          | integer |     false     |        input video's size        | Target output video size(s) in wxh (width x height) format. IE: 240x480 *See Note 3 below* |
| videoAdvancedParamsProfiles | string  |     false     |              *null*              | Name of video profile template that will be used. See the contents of 'evo-avconv-presets' folder for sample file presets. *See Note 3 below* |
|        audioBitrates        | integer |     false     |      input audio's bitrate       | Target output audio bitrate(s) (in bits/s, append '**k**' to value for kbits/s). Accepts the value '**copy**' to copy the input bitrate. An empty value passed would mean no audio |
|     audioChannelsCounts     | integer |     false     |   input audio's channel count    | Target output audio channel(s) count(s). Valid values are **1** (mono), **2** (stereo), and so on. Actual supported channel count is dependent on the number of input audio channels. *See Note 4 below* |
|      audioFrequencies       | string  |     false     |     input audio's frequency      | Target output audio frequency(ies) (in Hz, append '**k**' to value for 'kHz'. *See Note 4 below* |
| audioAdvancedParamsProfiles | string  |     false     |              *null*              | Name of audio profile template that will be used. *See Note 4 below* |
|          overlays           | string  |     false     |              *null*              | Location of the overlay source(s) to be used. These are transparent images (normally in PNG format) that have the same or smaller size than the video. Image is placed at the top-left position of the video |
|          croppings          | string  |     false     |              *null*              | Target video cropping position(s) and size(s) in 'left : top : width : height' format (e.g. 0:0:200:100. Positions are optional (200:100 for a centered cropping of 200 width and 100 height in pixels). Values are limited to the actual size of the video |
|          keepAlive          | integer |     false     |             1 *true*             | If **true**, the server will restart transcoding if it was previously activated |
|        commandFlags         | integer |     false     |              *null*              | Other commands to the transcode process that are not supported by the baseline transcode command |

## API Call Template

``` 
transcode source=<sourceURL> groupName=<groupName> destinations=<destinationStreamName> anyTranscodeParameter=<parameterValue>
```



### Sample API Call

``` 
transcode source=rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 groupName=testGroup destinations=testTranscode groupName=group videoBitrates=200k audioBitrates=copy 
```



### Success Response in JSON

``` 
{
"data":{
    "audioAdvancedParamsProfiles":["na"],
    "audioBitrates":["copy"],
    "audioChannelsCounts":["na"],
    "audioFrequencies":["na"],
    "croppings":["na"],
    "destinations":["stream1"],
    "dstUriPrefix":"-f flv tcp:\/\/localhost:6666\/",
    "emsTargetStreamName":"stream1",
    "fullBinaryPath":"C:\\EvoStream\\emsTranscoder.bat",
    "groupName":"group",
    "keepAlive":true,
    "localStreamName":"",
    "overlays":["na"],
    "source":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4",
    "srcUriPrefix":"rtsp:\/\/localhost:5544\/",
    "targetStreamNames":["testTranscode"],
    "videoAdvancedParamsProfiles":["na"],
    "videoBitrates":["200k"],
    "videoSizes":["na"]
},
"description":"Transcoding successfully started.",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - audioAdvancedParamsProfiles - An array of strings specifying the name of profile presets to be used for audio
  - audioBitrates - An array of integers for target audio output bitrates
  - audioChannelsCounts - An array of values for the target number of audio channels
  - croppings - An array of values for the target cropping positions and size
  - destinations - An array of target URIs or stream names
  - dstUriPrefix - Default destination if destination is a stream name
  - emsTargetStreamName - Target stream name used internally by EMS
  - fullBinaryPath - Actual location of the transcoder binary
  - groupName - Name of the group associated with this transcoding process
  - keepAlive - Transcoding will restart if previously activated
  - localStreamName - Actual EMS stream name of source (if given)
  - overlays - An array of locations for the images to be used as overlays
  - source - The actual stream/file to be used as input for transcoding
  - srcUriPrefix - Default source if given source is a stream name
  - targetStreamNames - An array of the target stream names to be used at the destination
  - videoAdvancedParamsProfiles - An array of strings specifying the name of profile presets to be used for video
  - videoBitrates - An array of values for target video output bitrates
  - videoSizes - An array of values for target video sizes
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- For **any parameter that is pluralized, you may specify one value, or multiple**.

  Multiple values must be separated by only a comma (comma-delimited). Specifying multiple values indicates multiple new streams will be created.

- There must be the **same number of values for all pluralized parameters**.

  **Order is important!** all first values are grouped together to make the first stream, all second parameters are grouped to make the second stream, etc…

- Video related parameters are ignored if the parameter `videoBitrates` is not specified.

- Audio related parameters are ignored if the parameter `audioBitrates` is not specified.


------

## Related Links

- [Transcode a Stream](userguide_transcode.html)

