# Huub技術情報

最終更新日:2020/06/28

## 全体計画

イベントの様子をTwitchで放送します。
DJは専用のサーバを経由して、VJにストリームを送信します。
VJはDJが送信したストリームにリアルタイムに映像を付けて、専用のサーバに送信します。

放送サーバのOBSでストリームを束ねます。
OBSで入力元のストリームを切り替えながらTwitchにストリームをおこないます。

もし、DJが専属のVJを付けて映像付きで参加する場合は、事前に専用のサーバを用意しますので、事前にお知らせください。

![HuubDiagram](https://github.com/huubclub/tech_info/raw/master/HuubDiagram.png)

Discordでストリームの調整を行います。
招待はTakayuki Tominagaが行っておりますので、イベント参加者はDiscordに参加をお願いします。

## DJ用ストリーム設定

### 解像度

1280x720 @ 30Hz(720p30) を基本設定とします。
もし720p30でのストリーミングがPCの処理負荷によって難しい場合は854x480(480p30)としてください。

> :warning: 720pで放送しますので、1080pでのストリーミングは避けてください。
リソースの浪費になり、帯域幅の問題が発生しやすくなります。

### ビデオ設定

h.264 @ 2500-5000 Kbpsとしてください。
5000Kbpsを基本設定としますが、もし通信が不安定な場合はビットレートを落としてください。

### オーディオ設定

320kbps AAC Stereo 48kHzに設定してください。(44.1kHzでも大丈夫です)

## OBS設定

> :warning: windowsユーザの方は[これ(64bit)](https://drive.google.com/file/d/1G8aankChNmFSEukzqDKYlc1RGrLafvLl/view?usp=sharing)もしくは[これ(32bit)](https://drive.google.com/file/d/11_Gtge_nFwZTCap_qB85ey_8VDaXmeMI/view?usp=sharing)をインストールして、OBSで高音質オーディオエンコーディングを有効にしてください。OBSデフォルトのAACコーデックは品質が悪いです。設定は後述します。

> :warning: ストリームの送信ソフトにはOBS StudioとStreamLabs OBSがありますが、StreamLabs OBSではなくOBS Studioを使用してください。StreamLabs OBSはCoreAudioがサポートされておらず品質が良くありません。

### Stream

![fig1](https://github.com/huubclub/tech_info/raw/master/fig1.png)

* Service
  * Custom
* Server
  * 以下の表を参照してください
* Stream Key
  * 以下の表を参照してください

| 出演者名 | Server | Stream Key |
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
  * (音源だけを送信して映像を付けない場合)2500Kbps
  * (映像付きで送信する場合)5000Kbps
* Encoder
  * Software(x264)
    * もしOBSを起動しているPCにグラフィックボードが搭載されている場合、ハードウェアエンコーダが使えます。ハードウェアエンコードが使える場合は使ってください。
    * **もしMacOSを使っている場合** Output ModeをAdvanceに変更することで、"Apple VT H264 Hardware Encoder"が使えます。  
    ![fig3](https://github.com/huubclub/tech_info/raw/master/fig3.png)  
    ![fig4](https://github.com/huubclub/tech_info/raw/master/fig4.png)
* Audio Bitrate
  * 320Kbps

> :warning: 基本的にはSimple Modeを推奨しますが、もしAdvance Modeを使用する場合、Keyframe Intervalの値を1〜2に設定してください。

### Audio

![fig5](https://github.com/huubclub/tech_info/raw/master/fig5.png)

* Sample Rate
  * 48 KHz もしくは 44.1 KHz
* Channels
  * Stereo

### Video

![fig6](https://github.com/huubclub/tech_info/raw/master/fig6.png)

* Base (Canvas) Resolution
  * 1280x720
* Output (Scaled) Resolution
  * 1280x720
* Downscale Filter
  * Lanczos (もしCPU負荷が気になるのであればBicubicかBilinearでも大丈夫)
* Common FPS Values
  * 30

## Windows向けオーディオコーデック設定

OBSがデフォルトで使用しているffmpegのオーディオコーデックの品質はあまりよくありません。
Windowsユーザは以下のパッケージをインストールしてください。

* [AppleApplicationSupport.msi(64bit)](https://drive.google.com/file/d/1G8aankChNmFSEukzqDKYlc1RGrLafvLl/view?usp=sharing)
* [AppleApplicationSupport.msi(32bit)](https://drive.google.com/file/d/11_Gtge_nFwZTCap_qB85ey_8VDaXmeMI/view?usp=sharing)

インストールした後、テストストリームを実行して、OBSのログファイル(OBSのメニューより Help > Log Files > View Current Log から参照できます)を見ると以下のようなログが確認できれば大丈夫です。

```
15:23:14.514: [CoreAudio AAC: 'avc_aac_stream']: settings:
15:23:14.514:     mode:          AAC
15:23:14.514:     bitrate:       320
15:23:14.514:     sample rate:   48000
15:23:14.514:     cbr:           on
15:23:14.514:     output buffer: 1536
```

もし、上記のようなログが出力されず、代わりに'acc' (ffmpeg_aac) というようなログが出力されている場合は、何か設定に誤りがありますので確認してみてください。

## Server

DJ/VJの方は以下のいずれかのRTMPサーバに対してストリーミングします。rtmpサーバは東日本、イギリス、ドイツ、韓国に設置しますので、自宅から近いサーバを選んでストリーミングします。

| サーバ名 | RTMPサーバアドレス | 用途 |
| --- | --- | --- |
| JP#1 | rtmp://huub-rtmp-1.japaneast.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp-1.japaneast.cloudapp.azure.com) | DJ -> VJ Relay |
| JP#2 | rtmp://huub-rtmp-2.japaneast.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp-2.japaneast.cloudapp.azure.com) | DJ -> VJ Relay |
| JP#3 | rtmp://huub-rtmp-3.japaneast.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp-3.japaneast.cloudapp.azure.com) | VJ -> BroadcastServer Relay |
| JP#4 | rtmp://huub-rtmp-4.japaneast.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp-4.japaneast.cloudapp.azure.com) | VJ -> BroadcastServer Relay |
| UK | rtmp://huub-rtmp.uksouth.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp.uksouth.cloudapp.azure.com) | DJ -> VJ Relay |
| DE | rtmp://huub-rtmp.germanywestcentral.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp.germanywestcentral.cloudapp.azure.com) | DJ -> VJ Relay |
| KR | rtmp://huub-rtmp.koreacentral.cloudapp.azure.com [(SpeedTest)](http://huub-rtmp.koreacentral.cloudapp.azure.com) | DJ -> VJ Relay |

DJの方は"DJ -> VJ Relay"のサーバに対してStreamを送信し、VJの方は"VJ -> BroadcastServer Relay"のサーバに対してStreamを送信します。

各サーバにはSpeedTestを実装してありますので、あらかじめ、配信環境からSpeedTestを実行し、最低でも20mbps以上の安定した速度が出ることを確認してください。

OBSを利用してストリームを送信する場合は以下のように設定します。

* Server
  * rtmp://{RTMPサーバのアドレス}/live
* Stream Key
  * 任意の文字列

RTMPサーバからストリームを受信する場合は以下のアドレスから取得できます。

* rtmp://{RTMPサーバのアドレス}/live/{送信時に設定したStream Keyの値}

## Serverの利用ルール

* イベントの前まで土日はサーバを立ち上げっぱなしにしますので、自由にストリーミングをテストすることができます。
  * もしサーバに繋がらない場合はサーバが停止している可能性が高いので、Discordで@touka_ttまで連絡ください。すぐに起動できます。土日以外に確認したい場合も連絡ください。
* イベント期間中でも時々ストリームをテストすることができますが、自分の枠でない場合は前に何時間もストリームを流しっぱなしにしないようにしてください。
* 最終的なストリームは、自分より前のDJのパフォーマンス開始と同時に開始することができます。
  * 例えばDJ Sharpnelのライブが14:00-14:45、goreshitのライブが14:45-15:30、Othermoonのライブが15:30-16:15というタイムテーブルの場合、goreshitは14:45からの本番に備えて14:00よりストリーミングを開始し、14:45のライブ開始までストリーミングを続けることができます（コンテンツ/テストは何でも構いません）。  
  同様にOthermoonも15:30からのライブストリームに備えて14:45からストリームの送信が可能になります。
* 最終チェックのため可能であれば予定時間の15分前までにストリーミングを開始してください。

## Streamのテスト

割り当てられたサーバとストリームキーを使用して、イベントの前の土日はいつでもサーバへのストリーム配信を可能にします。
送信したストリームは各種メディアプレイヤーを使用すると自分のストリームを受信できます。

* RTMPストリームを再生できるメディアプレイヤー
  * VLC (Windows or Linux or MacOS)
  * IINA (MacOS)

例えばrtmp://huub-rtmp-1.japaneast.cloudapp.azure.com/liveに対して"sample-streamkey"というStreamKeyを設定してストリーム送信した場合、VLCであれば`ファイル > ネットワークを開く`からURLを以下のように設定すると、自分が送信したストリームを確認できます。

![fig7](https://github.com/huubclub/tech_info/raw/master/fig7.png)

IINAの場合も`ファイル > URLから開く`から同様に設定することで、自分が送信したストリームを確認出来ます。

![fig8](https://github.com/huubclub/tech_info/raw/master/fig8.png)

## Content

DJは最低限Liveパフォーマンスの音源だけ送っていただければ大丈夫です。（つまり画面は黒一色でOK）
もし、Webカメラ等でDJパフォーマンスの様子を撮影できるのであればベターですが、
これは必須ではありません。
もしパフォーマンスの様子を一緒に送る場合は、Discordで事前に連携してください。
視聴者に最も優先して届くべきものは音楽で、演出は二の次だと言うことを忘れないでください。

## DJの交代

DJの交代の間に簡単なDJ交代用のスプラッシュスクリーンを出して交代します。
DJの交代は@touka_ttと@zktyがDiscordで指示します。
イベント期間中は常にDiscordの連絡を見ることが出来る状態にしておいてください。

> :warning: Twitchの配信にはラグがあります。くれぐれもTwitchのストリームを見てタイミングを合わせようとしないでください。

1. 前のDJのパフォーマンスが終了すると同時にフェードアウト。
1. スプラッシュスクリーンをフェードイン。
1. VJがDJに対して音源の送信を指示し、DJがパフォーマンスを開始
1. DJのパフォーマンスを受けてVJがパフォーマンスを開始
1. VJのストリームの受信をもって、スプラッシュスクリーンをフェードアウト

DJ -> VJ間、そしてVJ -> Broadcast Server間に通信ラグがある関係で、
どうしてもイントロに派手なビジュアルを送信したり、重要なMCを入れたりすることは難しいです。この点は予め認識しておいてください。

## DJ出力の取り込み（おまけ）

DJの音をどのように取り込むかは各々の環境によるので一概に言えないのですが、一例として仮想オーディオデバイスを使用する方法を挙げます。
Macの場合はSoundFlowerを使用します。Windowsの場合はVB-CABLEのようなソフトを使います。

以下はMacのSoundFlowerとRekordboxを使用した例です。

> :warning: この方法はPC内部で再生されている音をOBSに取り込む方法ですが、実物のオーディオインタフェースを使用する方法も基本的には同じです。
手順1，2を飛ばして、手順3で新規Audio Input Captureを作成するところで使用するオーディオインタフェースを選択するとOBSに音が取り込めます。  
DJコントローラーによってはオーディオインタフェースを内蔵している機種もあるので、そのようなコントローラを使用している場合は、OBSのキャプチャデバイスとしてコントローラー内蔵のインタフェースを指定すると良いでしょう。

1. Soundflowerをダウンロードし、インストールする。リンク先のドキュメントにあるとおり、セキュリティ警告がでて一回目のインストールは必ず失敗するので、気にしないこと。詳しくはリンク先を読んでください。  
[https://github.com/mattingalls/Soundflower/releases/tag/2.0b2](https://github.com/mattingalls/Soundflower/releases/tag/2.0b2)
1. Rekordboxのオーディオ出力をSoundflower(2ch)に変更する。  
![fig9](https://github.com/huubclub/tech_info/raw/master/fig9.png)
1. OBSのSourceより新規AudioInputCaptureを作成。名前はSoundflowerを設定。デバイスはSoundflower(2ch)を選択。  
![fig10](https://github.com/huubclub/tech_info/raw/master/fig10.png)  
![fig11](https://github.com/huubclub/tech_info/raw/master/fig11.png)  
![fig12](https://github.com/huubclub/tech_info/raw/master/fig12.png)  
1. DJしたら音がOBSに取り込まれているようになる
![fig13](https://github.com/huubclub/tech_info/raw/master/fig13.png)  

## Special Thanks
marcan & AnimeltUp!Crew
