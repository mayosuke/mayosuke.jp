---
title: "\"Detroit: Become Human\"プレイ中に頻発したフリーズを解決した時の手順"
date: 2021-01-24T21:00:00+09:00
draft: false
---

昨年末Steamのセールで安くなってた時に買った
[Detroit: Become Human](https://www.quanticdream.com/en/detroit-become-human)を開始。面白い！でもなんか頻繁にフリーズが発生する。。ゲームの途中で、突然映像が止まり操作不能になり、音声だけが流れ続ける、という現象が、最初の章？を終えた後の章から頻発するようになり、ゲームが全然進められなくなってしまった。マシンスペックはこんな感じで、性能不足では無いはず。

- CPU: i5-10400F
- RAM: 32GB
- GPU: RTX2060 Super

「detroit become human freeze」で軽くググると、同じようなエラーに遭遇して、NVIDIAのドライバを特定のバージョンに落とすと解決した、という内容の書き込みがSteamのDetroit: Become Humanのフォーラムにあった。

[Stop game's crash , HOW TO: :: Detroit: Become Human General Discussions](https://steamcommunity.com/app/1222140/discussions/0/2569815696856072388/)

なんとなくドライバのバージョンを落とすのが嫌だなと思い、なんとかそうせずに解決したかった。そこで、まずはその時点で適用していなかったWindows10のバージョン20H2アップデートを適用してPCを再起動してからゲームを起動してみた。するとNVIDIAのドライバーが古いと警告された。NVIDIAのドライバはその時点の最新版をインストールしていたつもりだったけど、実際にインストールされていたバージョンは432.00で、最新は461.09だった。とりあえず461.09にアップデートして、ゲームを起動してみたが、フリーズはすぐ再現してしまった。

今度は、先述したリンク先に書いてある、"Remove all the shaders in steamapps\common\Detroit Become Human\ShaderCache"をやってからゲームを再起動してみたが、これもダメ。またすぐフリーズが発生してしまった。

ここまでいろいろあがいてみて、どうにも解決しそうになかったので、観念して素直にリンク先に書いてあった以下の手順をなぞってみることにした。すると、フリーズして全然ゲームが進められなかった章はすんなり最後まで進めることができて、次の章も問題なく進められた。どうやらフリーズ解消されたっぽい！

1. Download 446.14 from nvidia
2. Restart your PC
3. Remove all the shaders in steamapps\common\Detroit Become Human\ShaderCache
4. Start the game

これで、安心してゲームが進められそう。ただ、NVIDIAのドライバのバージョンをずっと446.14に固定するのはなんか気持ちわるいので、ドライバ側のアップデートで解消されるとありがたいなあ。

余談だが、英語の学習を兼ねてゲームは英語音声・英語字幕でプレイしている。テキストを読むタイミングで、よくわからない英語が出てきたら通常はブラウザのGoogle翻訳に英文・単語を手打ちで入れて翻訳してもらっている。Google翻訳にはスマホアプリもあるので、試しにゲーム画面をカメラで撮影させて翻訳させてみた。わりとくっきりしたテキストを撮影したつもりだったので、手打ちでテキストを入力した時と同等な結果になるのを期待していたが、残念ながら、クオリティはいまいちな感じだった。

![](/images/2021-01-24-how-to-solve-freezing-problem-when-playing-detroit-become-human/dbh-text-translated.png)

## References

- [Detroit: Become Human | Official Site | Quantic Dream](https://www.quanticdream.com/en/detroit-become-human)
- [Stop game's crash , HOW TO: :: Detroit: Become Human General Discussions](https://steamcommunity.com/app/1222140/discussions/0/2569815696856072388/)
- [Yosuke MIYAJIMA on Twitter: "昨年末Steamのセールで安くなってた時に買った Detroit: Become Humanを開始。面白い！でもなんか頻繁にフリーズしちゃう。" / Twitter](https://twitter.com/mayosuke/status/1353180671276060673?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1353180671276060673%7Ctwgr%5E%7Ctwcon%5Es1_&ref_url=https%3A%2F%2Froamresearch.com%2F%2Fapp%2Fmayosuke)
