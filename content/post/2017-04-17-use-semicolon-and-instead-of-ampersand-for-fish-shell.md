+++
date = "2017-04-17T02:17:43+09:00"
draft = false
title = "fish シェルでコマンドをつなげる時は && でなくて ; and を使う"

+++
Hugo の記事を作成してローカルで表示確認した後、S3 にアップロードする前にサイトをビルドする作業をいつも忘れてしまう。
ビルドしてアップロード、をまとめて行おうと、&& でコマンドをつなげたら fish シェルではサポートされていないと怒られた。

```
⋊> --theme=THEME_NAME && aws s3 sync --delete ./public s3://BUCKET_NAME
Unsupported use of '&&'. In fish, please use 'COMMAND; and COMMAND'.
fish: hugo --theme=hugo-zen && aws s3 sync --delete ./public s3://BUCKET_NAME
                             ^
```

`&&`を`; and`に置換して無事実行できた。
`⋊> hugo --theme=THEME_NAME; and aws s3 sync --delete ./public s3://BUCKET_NAME`
