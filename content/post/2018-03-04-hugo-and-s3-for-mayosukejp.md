---
title: "mayosuke.jpを編集・公開するための手順"
date: 2018-03-04T12:02:31+09:00
draft: false
---

2018年3月現在、mayosuke.jpはhugoで生成したファイルをS3上でホストしている。

# 使うツール
- git
- hugo
- aws cli

macの場合はhugoをbrewでインストールする。
```
brew install hugo
```

# githubリポジトリの取得

```
git clone git@github.com:mayosuke/mayosuke.jp.git
cd mayosuke.jp
git clone git@github.com:mayosuke/hugo-zen.git themes/hugo-zen
```

# 新しい投稿の作成

```
hugo new post/2018-03-04-hugo-and-s3-for-mayosukejp
```

Newして生成される投稿のfrontmatterのデフォルトがYAML形式になっていた。

`hugo new`した投稿が`hugo server`で反映されなくてちょっとハマったが、
`hugo new`で指定する投稿のファイルの拡張子を指定していないからだった。。
```
hugo new post/2018-03-04-test2.md
```

# レンダリング結果の確認

```
hugo server --theme=hugo-zen --buildDrafts --watch --disableFastRender
```

深い理由は無いが、テーマの指定はオプションで行っている。
`.md`無しで`hugo new`していたファイルに`.md`をつけて`hugo server`したら以下のようなエラーになってしまった。。

```
hugo server --theme=hugo-zen --buildDrafts --watch --disableFastRender
Building sites … ERROR 2018/03/04 11:53:40 failed to parse page metadata for "post/2018-03-04-hugo-and-s3-for-mayosukejp.md": Near line 0 (last key parsed ''): bare keys cannot contain ':'
Total in 17 ms
Error: Error building site: failed to parse page metadata for "post/2018-03-04-hugo-and-s3-for-mayosukejp.md": Near line 0 (last key parsed ''): bare keys cannot contain ':'
```

新しい投稿のfrontmatterのフォーマット指定だけ手編集でYAMLの`---`からTOMLの`+++`に変えただけで、中身のフォーマットはYAMLのままにしていたからだった。中身のフォーマットをTOMLに直したらエラーは解消されたが、デフォルトをTOMLにするやり方を調べたくなかったので、今後は手編集せずに(YAML)デフォルトのままで作業することにする。

# サイトの生成とS3へのアップロード

## fishシェルの場合
```
hugo --theme=hugo-zen; and aws s3 sync --delete ./public s3://mayosuke.jp
```

