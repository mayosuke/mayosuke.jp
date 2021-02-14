---
title: "HugoのテーマをHugo ZenからM10cに移行"
date: 2021-02-14T21:54:04+09:00
draft: false
---

[mayosuke.jp](https://mayosuke.jp)に新規投稿作成しようと、`hugo server`したら、サイトのトップがこんな感じになって、記事一覧が表示されなくなってしまった。

![](/images/2021-02-14-migrate-hugo-theme-from-hugo-zen-to-m10c/hugo-zen-top-page-corrupted.png)

`hugo server`実行時に、こういうWARNが出ていた。

```shell
❯ hugo server --theme=hugo-zen --buildDrafts --watch --disableFastRender
Start building sites … 
WARN 2021/02/14 17:42:46 Page.Hugo is deprecated and will be removed in a future release. Use the global hugo function.
```

hugoのバージョンは[v0.80.0](https://github.com/gohugoio/hugo/releases/tag/v0.80.0)で、2021年2月14日現在で最新。
3年前に設定したテーマなので、hugo本体の更新にテーマが追いつけていないことを疑った。テーマ自体を変えたいと思っていたところだったので、せっかくなので新しいテーマに変えてみた。

今回から、テーマはちゃんとconfig.tomlに記載するようにしてみる。フォークしたリポジトリをクローンして、一応自分がいじるようのブランチを切ってプッシュしておく。

```shell
❯❯❯ git clone https://github.com/mayosuke/hugo-theme-m10c.git m10c
Cloning into 'm10c'...
❯❯❯ cd m10c/
❯❯❯ git checkout -b mayosuke.jp
Switched to a new branch 'mayosuke.jp'
❯❯❯ git push origin mayosuke.jp
```

config.tomlにthemeを指定。

```shell
❯❯❯ git diff
... 
+theme = "m10c"
...
```

というわけで、本日からmayosuke.jpのテーマは[m10c](https://github.com/vaga/hugo-theme-m10c)になりました。

## ToDos

- アバター画像を囲う丸い枠が楕円になってしまっててかっこわるいので、ちゃんと円にしたい
- フッターあたりにコピーライト表示を復活させる
- ファビコンをちゃんとする
- テーマのカラースキームを、もうちょっと見やすくする

## References

新しく設定したテーマ。
- [vaga/hugo-theme-m10c: A minimalistic (m10c) blog theme for Hugo](https://github.com/vaga/hugo-theme-m10c)

今まで使っていたテーマ。3年以上お世話になりました。ありがとうございました！
- [rakuishi/hugo-zen: Hugo Zen is a minimal hugo theme.](https://github.com/rakuishi/hugo-zen)

