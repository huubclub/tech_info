# Huub tech info

Last update: 2020/06/20

# Abstract

The event will be broadcast on Twitch.
The DJ sends the stream to the VJ via a dedicated server.
The VJ attaches video to the stream sent by the DJ in real time and sends it to a dedicated server.

The stream is bundled together on the broadcast server's OBS.
The OBS will be used to stream to Twitch, switching between the source streams.

If you want to have a DJ with a dedicated VJ and video, you'll need to set up a dedicated server in advance. so please let us know in advance.

![HuubDiagram](https://github.com/huubclub/tech_info/raw/master/HuubDiagram.png)

We will coordinate the stream in Discord.
Invited by Takayuki Tominaga, event attendees are invited to attend Please join Discord.

## Stream settings for DJs

### Resolution

1280x720 @ 30Hz(720p30) is the default setting.
If streaming at 720p30 is difficult due to your PC's processing load, set it to 854x480 (480p30).

> :warning: We broadcast in 720p, so please do not stream in 1080p.
This is a waste of resources and is more likely to cause bandwidth issues.

### Video Settings

Use h.264 @ 2500-5000 Kbps.
If the communication is not stable, reduce the bit rate and set the rate to 5000 Kbps.

### Audio Settings

Set it to 320kbps AAC Stereo 48kHz. (44.1 kHz is fine.)

## OBS settings

> :warning: If you are a windows user, install [this(64bit)](https://drive.google.com/file/d/1G8aankChNmFSEukzqDKYlc1RGrLafvLl/view?usp=sharing) or [this(32bit)](https://drive.google.com/file/d/11_Gtge_nFwZTCap_qB85ey_8VDaXmeMI/view?usp=sharing), and try OBS for high quality sound! Audio encoding is enabled; the OBS default AAC codec is The quality is poor. Settings are described below.

> :warning: OBS Studio and StreamLabs OBS are two examples of stream transmission software, but Please use OBS Studio and not StreamLabs OBS StreamLabs OBS does not support CoreAudio and the quality is not good.

### Stream

![fig1](https://github.com/huubclub/tech_info/raw/master/fig1.png)

* Service
  * Custom
* Server.
  * Please refer to the following table
* Stream Key
  * Please refer to the following table

  | Artist name | Server | Stream Key |
  | --- | --- | --- |
  | DJ Sharpnel | rtmp://huub-rtmp-1.japaneast.cloudapp.azure.com/sharpnel | shrpnl |
  | JAKAZiD | rtmp://huub-rtmp.uksouth.cloudapp.azure.com/jakazid | jkzd |
  | goreshit | rtmp://huub-rtmp.uksouth.cloudapp.azure.com/goreshit | grsht |
  | Othermoon | rtmp://huub-rtmp-2.japaneast.cloudapp.azure.com/othermoon | othrmn |
  | DJ BrainShit | rtmp://huub-rtmp.germanywestcentral.cloudapp.azure.com/brainshit | brnsht |
  | Lolistyle Gabbers | rtmp://huub-rtmp-2.japaneast.cloudapp.azure.com/loligabber | llgbbr |
  | 栄免建設 | rtmp://huub-rtmp-1.japaneast.cloudapp.azure.com/amenkensetsu | amen |
  | DENPA-SAMPLER | rtmp://huub-rtmp.koreacentral.cloudapp.azure.com/denpa | dnp |
  | Takayuki Tomianaga | rtmp://huub-rtmp-3.japaneast.cloudapp.azure.com/tominaga | touka |
  | zukutya | rtmp://huub-rtmp-4.japaneast.cloudapp.azure.com/zukutya | zkty |

### Output

![fig2](https://github.com/huubclub/tech_info/raw/master/fig2.png)

* Output Mode
  * Simple
* Video Bitrate
  * (when only the sound source is transmitted and no video is attached) 2500Kbps
  * (with video) 5000Kbps
* Encoder.
  * Software(x264)
    * If your PC is equipped with a graphics board, you can use the hardware You can use the encoder. If you can use hardware encoding, use it.
    * **If you're using MacOS** If you can use hardware encoding, use it. You can use "Apple VT H264 Hardware Encoder".  
    ![fig3](https://github.com/huubclub/tech_info/raw/master/fig3.png)  
    ![fig4](https://github.com/huubclub/tech_info/raw/master/fig4.png)
* Audio Bitrate
  * 320Kbps

> :warning: Simple Mode is recommended, but if you want to use Advance Mode, you can use Set the value of Keyframe Interval to 1 or 2.

### Audio

![fig5](https://github.com/huubclub/tech_info/raw/master/fig5.png)

* Sample Rate
  * 48 KHz or 44.1 KHz
* Channels.
  * Stereo

### Video

![fig6](https://github.com/huubclub/tech_info/raw/master/fig6.png)

* Base (Canvas) Resolution
  * 1280x720
* Output (Scaled) Resolution
  * 1280x720
* Downscale Filter
  * Lanczos (if you're worried about CPU load, Bicubic or Bilinear will work too)
* Common FPS Values
  * 30

## Audio Codec Settings for Windows.

The quality of the ffmpeg audio codec used by OBS by default is not very good.
Windows users need to install the following packages

* [AppleApplicationSupport.msi(64bit)](https://drive.google.com/file/d/1G8aankChNmFSEukzqDKYlc1RGrLafvLl/view?usp=sharing)
* [AppleApplicationSupport.msi(32bit)](https://drive.google.com/file/d/11_Gtge_nFwZTCap_qB85ey_8VDaXmeMI/view?usp=sharing)

After installation, if you run the test stream and look at the OBS log file (you can refer to it from the OBS menu under Help > Log Files > View Current Log), you should be fine if you can see the following logs.

```
15:23:14.514: [CoreAudio AAC: 'avc_aac_stream']: settings:
15:23:14.514:     mode:          AAC
15:23:14.514:     bitrate:       320
15:23:14.514:     sample rate:   48000
15:23:14.514:     cbr:           on
15:23:14.514:     output buffer: 1536
```

If you don't see the above log, but instead see a log like 'acc' (ffmpeg_aac), there is something wrong with your settings.

## Server

DJs/VJs can stream to one of the following RTMP servers: rtmp The servers will be located in eastern Japan, the United Kingdom, Germany, and South Korea, so you can choose a server close to your home. Streaming.

| Server Name | RTMP Server Address | purpose |
| --- | --- | --- |
| JP#1 | rtmp://huub-rtmp-1.japaneast.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp-1.japaneast.cloudapp.azure.com) | DJ -> VJ Relay |
| JP#2 | rtmp://huub-rtmp-2.japaneast.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp-2.japaneast.cloudapp.azure.com) | DJ -> VJ Relay |
| JP#3 | rtmp://huub-rtmp-3.japaneast.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp-3.japaneast.cloudapp.azure.com) | VJ -> BroadcastServer Relay |
| JP#4 | rtmp://huub-rtmp-4.japaneast.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp-4.japaneast.cloudapp.azure.com) | VJ -> BroadcastServer Relay |
| UK | rtmp://huub-rtmp.uksouth.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp.uksouth.cloudapp.azure.com) | DJ -> VJ Relay |
| DE | rtmp://huub-rtmp.germanywestcentral.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp.germanywestcentral.cloudapp.azure.com) | DJ -> VJ Relay |
| KR | rtmp://huub-rtmp.koreacentral.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp.koreacentral.cloudapp.azure.com) | DJ -> VJ Relay |

The DJ sends a Stream to the "DJ -> VJ Relay" server and the VJ sends a Stream to the " Send a Stream to the "VJ -> BroadcastServer Relay" server, and The speed test is implemented on each server.

Each server has SpeedTest implemented, so run SpeedTest from the distribution environment and make sure that the speed is stable at least 20mbps.

To send a stream using OBS, configure as follows.

* Server.
  * rtmp://{RTMP server address}/live
* Stream Key
  * Any string

If you want to receive a stream from the RTMP server, you can get it from the following address.

* rtmp://{address of the RTMP server}/live/{Stream set at the time of sending Key value}

## Server Usage Rules

* We will keep the server up on Saturdays and Sundays until before the event so you can test the streaming at your leisure.
  * If you can't connect to the server, it's likely the server is down and you can use Discord to @ Please contact touka_tt. We'll get you up and running in no time. If you want to check outside of Saturday and Sunday, please contact me as well.
* You can test streams from time to time during the event, but please don't leave the stream running for hours before if it's not your slot.
* The final stream can start at the same time as the DJ before you starts performing.
  * For example, if DJ Sharpnel is live from 14:00-14:45, goreshit's live is from 14:45 to 15:30 and Othermoon's live performance is from 15:30 to 16:15. In the case of the timetable, goreshit starts at 14:00 in preparation for the show at 14:45 You can start streaming and continue streaming until 2:45 p.m. when it goes live! (Any content/testing is fine).  
  Similarly, Othermoon will start at 14:45 in preparation for the live stream at 15:30. You will be able to send your stream.
* Please start streaming at least 15 minutes before the scheduled time if possible for a final check.

## Stream Testing.

Using the assigned server and stream key, the server can be sent to the server at any time on the Saturday or Sunday before the event. Enables stream distribution.
You can receive your own stream when you send it using various media players.

* Media players that can play RTMP streams.
  * VLC (Windows or Linux or MacOS)
  * IINA (MacOS)

For example, you can use "sample-streamkey" for rtmp://huub-rtmp-1.japaneast.cloudapp. For example, if you set "sample-streamkey" for azure.com/live If you set up a StreamKey and streamed, you can use the `File > Open Network` as follows, you can check the stream you sent You can.

![fig7](https://github.com/huubclub/tech_info/raw/master/fig7.png)

In the case of IINA, you can do the same thing by going to `File > Open from URL` and setting up your own You can check the stream.

![fig8](https://github.com/huubclub/tech_info/raw/master/fig8.png)

## Content

At the very least, the DJ should only send us the soundtrack of the live performance. (In other words, the screen can be all black.)
If you can use a webcam or other means to capture the DJ performance, it's better.
This is not required.
If you want to send your performance along, please collaborate with us in advance on Discord.
Remember, the music should be the highest priority to reach your audience, and the production is secondary to the music!

## Switching DJs

In between DJ changes, we'll put out a simple DJ change splash screen to take over.
DJ changes will be directed by @touka_tt and @zkty in Discord.
Be sure to keep your Discord contact visible at all times during the event.

> :warning: There is a lag in the Twitch stream. Please don't try to time the Twitch stream.

1. fade out as soon as the previous DJ's performance ends.
1. fade in the splash screen.
1. the VJ instructs the DJ to transmit the sound source and the DJ starts performing.
1. the VJ starts performing after the DJ's performance
1. fade out the splash screen with the receipt of the VJ stream

Due to the communication lag between DJ -> VJ and between VJ -> Broadcast Server, there is a
Inevitably, it's hard to send a flashy visual to the intro or include an important MC Please be aware of this point in advance. Please be aware of this point in advance.

## Special Thanks

marcan & AnimeltUp!Crew
