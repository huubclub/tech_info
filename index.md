# Huub技術情報

最終更新日:2020/06/07

## 全体計画

イベントの様子をTwitchで放送します。
DJは専用のサーバを経由して、VJにストリームを送信します。
VJはDJが送信したストリームにリアルタイムに映像を付けて、専用のサーバに送信します。

放送サーバのOBSでストリームを束ねます。
OBSで入力元のストリームを切り替えながらTwitchにストリームをおこないます。

もし、DJが専属のVJを付けて映像付きで参加する場合は、事前に専用のサーバを用意しますので、事前にお知らせください。

![HuubDiagram](https://huubclub.github.io/tech_info/HuubDiagram.png)

Discordでストリームの調整を行います。
招待はTakayuki Tominagaが行っておりますので、イベント参加者はDiscordに参加をお願いします。

## DJ用ストリーム設定

### 解像度

1280x820 @ 30Hz(720p30) を基本設定とします。
もし720p30でのストリーミングがPCの処理負荷によって難しい場合は854x480(480p30)としてください。

> :warning: 720pで放送しますので、1080pでのストリーミングは避けてください。
リソースの浪費になり、帯域幅の問題が発生しやすくなります。

### ビデオ設定

h.264 @ 2500-5000 Kbpsとしてください。
5000Kbpsを基本設定としますが、もし通信が不安定な場合はビットレートを落としてください。

### オーディオ設定

320kbps AAC Stereo 48kHzに設定してください。(44.1kHzでも大丈夫です)

## OBS設定

> :warning: windowsユーザの方はこれ(64bit)もしくはこれ(32bit)をインストールして、OBSで高音質オーディオエンコーディングを有効にしてください。OBSデフォルトのAACコーデックは品質が悪いです。

> :warning: ストリームの送信ソフトにはOBS StudioとStreamLabs OBSがありますが、StreamLabs OBSではなくOBS Studioを使用してください。StreamLabs OBSはCoreAudioがサポートされておらず品質が良くありません。

### Stream

![fig1](https://huubclub.github.io/tech_info/fig1.png)

* Service
  * Custom
* Server
  * 以下の表を参照してください
* Stream Key
 * 以下の表を参照してください

| 出演者名 | Server | Stream Key |
| --- | --- | --- |
| DJ Sharpnel | rtmp://~~~~~~~~ | ~~~~~~~ |
| JAKAZiD | rtmp://~~~~~~~~ | ~~~~~~~ |
| goreshit | rtmp://~~~~~~~~ | ~~~~~~~ |
| Othermoon | rtmp://~~~~~~~~ | ~~~~~~~ |
| DJ BrainShit | rtmp://~~~~~~~~ | ~~~~~~~ |
| Lolistyle Gabbers | rtmp://~~~~~~~~ | ~~~~~~~ |
| 栄免建設 | rtmp://~~~~~~~~ | ~~~~~~~ |
| DENPA-SAMPLER | rtmp://~~~~~~~~ | ~~~~~~~ |
| Takayuki Tomianaga | rtmp://~~~~~~~~ | ~~~~~~~ |
| zukutya | rtmp://~~~~~~~~ | ~~~~~~~ |

### Output

![fig2](https://huubclub.github.io/tech_info/fig2.png)

* Output Mode
  * Simple
* Video Bitrate
  * (音源だけを送信して映像を付けない場合)2500Kbps
  * (映像付きで送信する場合)5000Kbps
* Encoder
  * Software(x264)
    * もしOBSを起動しているPCにグラフィックボードが搭載されている場合、ハードウェアエンコーダが使えます。ハードウェアエンコードが使える場合は使ってください。
    * もしMacOSを使っている場合はOutput ModeをAdvanceに変更することで、"Apple VT H264 Hardware Encoder"が使えます。  
    ![fig3](https://huubclub.github.io/tech_info/fig3.png)  
    ![fig4](https://huubclub.github.io/tech_info/fig4.png)
* Audio Bitrate
  * 320Kbps

### Audio

![fig5](https://huubclub.github.io/tech_info/fig5.png)

* Sample Rate
  * 48 KHz もしくは 44.1 KHz
* Channels
  * Stereo

### Video

![fig6](https://huubclub.github.io/tech_info/fig6.png)

* Base (Canvas) Resolution
  * 1280x720
* Output (Scaled) Resolution
  * 1280x720
* Downscale Filter
  * Lanczos (もしCPU負荷が気になるのであればBicubicかBilinearでも大丈夫)
* Common FPS Values
  * 30


## Special Thanks
marcan & AnimeltUp!Crew
