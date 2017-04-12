+++
date = "2017-04-12T23:56:39+09:00"
draft = false
title = "Watson Speech to Text でセミナー録音データのテキストおこしを試してみたがダメだった"

+++

最初は、Google ドキュメントの音声入力機能もかなりいけてるという情報を見つけたので試してみたが、
自分の環境ではあまりうまく認識できなかったので、すぐあきらめた。

その後、以前見つけて気になっていた以下の記事を参考にして、 Watson の Speech to Text でテキストおこしに挑戦してみることにした。

[人工知能Watsonにテープ起こしさせてみた:WebClip - ウェブ制作、UXD／IA、アクセシビリティ - CNET Japan](https://japan.cnet.com/blog/webclip/2016/12/19/entry_30022839/)

手元にあるセミナー録音データは AudioNote ファイルなので、まず AudioNote アプリ上で音声をエクスポートした。
エクスポートの形式はMP3しか選べなかった。

Watson の Speech to Text は MP3 を入力として受け付けないので、別形式に変換する必要があった。
Flac などもサポートされているが、 Flac に馴染みが無かったので Wav にすることにした。
MP3 から WAV への変換は、ググって最初に見つけた FFMPEG でコマンドラインから簡単に変換にすることができた。

`$ ./ffmpeg -i "input.mp3" -vn -ac 2 -ar 44100 -acodec pcm_s16le -f wav "output.wav"`

2時間半以上あるセミナーの講義音声は、 MP3 の時点で 200MB オーバー、 WAV にしたら 1.5GB オーバーで、 Speech to Text が一度に受けつける入力音声の容量が最大 100MB までなので、 WAV を分割する必要があった。
分割するツールをちょっとググったら sox というのが見つかったので、以下のQiitaを参考にこれを試してみたところ、

[今更聞けない目的別soxの使い方 - Qiita](http://qiita.com/mountcedar/items/a04ebc4f8c27c226bbff)

`$ sox output.wav output-0.wav 0 600 # 0秒目から、600秒分を切り出す指定`

みたいなコマンドで簡単に分割できた。目見当で10分刻みの分割にしたら 100MB をちょっと超えてしまったので、9 分刻みにしたところ 95MB 程度で収まった。
sox の使い心地が良い感じで、 MP3 から WAV への変換も可能だったので、試したらこれもすぐできた。

`$ sox input.mp3 output.wav`

FFMPEG でも分割できそうだし、いろいろ高機能で使いこなせたら便利そうだけど、現時点の用途としては sox のほうが早そうなので sox メインでいくことにした。

分割作業は、以下のような簡単なrubyスクリプトを書いて行った。

```ruby
S = 540 # 9 min x 60 sec = 540 sec
16.times do |i| # output.wavの録音時間を9分で割ってきりが良くなる値
  `sox output.wav output-#{i}.wav trim #{i * S} #{S}`
  end
```

  入力音声の準備ができた後は、 Bluemix の利用開始手続きを行った。
  これが初めての Bluemix 利用なので、30 日間は無料で遊べる。これを機にいろいろ試してみよう。

  CNET の記事を参考にしながら、アカウント登録など進めてた。
  なぜかログイン直後の言語設定がドイツ語か何かになっていて一瞬びっくりした。

  資格情報をもとに、curl で API をたたいてみた。

```
$ curl -X POST -u username:password
  --header "Content-Type: audio/wav"
  --header "Transfer-Encoding: chunked"
  --data-binary @output-0.wav
  "https://stream.watsonplatform.net/speech-to-text/api/v1/models/ja-JP_BroadbandModel/recognize?continuous=true"
```

  レスポンスが返ってくるまでに 6 分ほどかかった。ほとんどの時間がアップロードで、アップロードが終わったらすぐにレスポンスが返ったので、 Watson 側で受信した端から順番に解析をしているのかな？

  返ってきた結果は、ほとんど意味不明だった。
  元データの音声の録音条件があまり良くなかったので、まあ想定はしていたけど残念だ。。

