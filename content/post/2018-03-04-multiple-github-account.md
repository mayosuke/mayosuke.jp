---
title: "普段使っているgithubアカウントと異なるアカウントでgithubにgit pushする"
date: 2018-03-04T13:23:46+09:00
draft: false
---

普段使っているgithubアカウントと異なるアカウントでgithubに`git push`しようとした時、permission deniedというエラーになった。

以下のURLを参考にしてしてエラーは解決できたけど、別アカウントを使う時にリポジトリ毎にいちいち`git remote`で`origin`を削除して設定し直すのはめんどくさい。

- [GitHub リポジトリに git push したら Permission が denied - Qiita](https://qiita.com/tanishilove/items/3164ecf3f16585fa3bf2)
[githubの複数アカウントの扱い方 - Qiita](https://qiita.com/okappy/items/8fb3dacf176b45db85eb)
- [同一端末で異なるgithubアカウントにpushするときの手順 - Qiita](https://qiita.com/uni-3/items/9f303bae952da74f25e3#_reference-d99e6cda362604b4d477)

結局、`origin`を使わずに`git push`することにした。リポジトリの指定の面倒くささはシェルのコマンド履歴に頼ることで回避することにした。

`git push git@github-mayosuke:mayosuke/mayosuke.jp.git master`

このやり方は以下を参考にした。

- [Git における SSH オプション指定方法あれこれ - Qiita](https://qiita.com/kyanny/items/c397370862095c305cbe)

