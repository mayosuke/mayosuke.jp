+++
date = "2017-04-16T00:46:29+09:00"
draft = false
title = "Jupyter で学ぶ「ゼロから作る Deep Learning」（その１）"

+++
ディープラーニングのことを手を動かしながら学べると評判の良い[ゼロから作る Deep Learning](https://www.amazon.co.jp/dp/4873117585)の学習を開始した。
せっかくなので、 [Jupyter](http://jupyter.org/) 上で写経してみる。

Jupyter は、 anaconda をインストールすると含まれている。

```
$ pyenv install anaconda3-4.3.1
$ pyenv local anaconda3-4.3.1
```

jupyter は以下のコマンドを実行すると起動してブラウザ上にUIが表示される。

`$ jupyter notebook`

今回は２章のパーセブトロンのところまで進めた。
１段のパーセブトロンでAND・OR・NANDの論理回路が実現できること、２段のパーセブトロンでXORが実現できることを Jupyter 上で手を動かしながら確かめた。
確認に使った jupyter ノートブックは、 [ここ](https://github.com/mayosuke/deep-learning-from-scratch) に公開した。
GitHub は jupyter ノートブックをレンダリングしてくれるので、[こんな感じ](https://github.com/mayosuke/deep-learning-from-scratch/blob/master/deep-learning-from-scratch-c2.ipynb)でコードとその実行結果を簡単に見ることができてとても便利。

 
