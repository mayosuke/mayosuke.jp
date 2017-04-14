+++
date = "2017-04-15T05:30:39+09:00"
draft = false
title = "curl でリファラー指定が必要なサイトからファイルをダウンロードする"

+++
運営のサポートをしている妻のワードプレスサイトに、カスタムフォントをインストールすることになった。
妻が選んだのはこれ。

[はんなり明朝](http://typingart.net/?p=44)

ワードプレスを動かしているサーバ上で

`curl http://typingart.net/fontdata/hannari.zip -O`

して unzip したら、

```
Archive:  hannari.zip
End-of-central-directory signature not found.  Either this file is not
a zipfile, or it constitutes one disk of a multi-part archive.  In the
latter case the central directory and zipfile comment will be found on
the last disk(s) of this archive.
unzip:  cannot find zipfile directory in one of hannari.zip or
hannari.zip.zip, and cannot find hannari.zip.ZIP, period.
```

と怒られた。
ブラウザ上で当該フォントのダウンロードリンクをクリックするとちゃんとダウンロードできる。

-I オプションをつけてもう一度試したら、 403 エラーが返ってきていた。
ブラウザのアドレスバーにダウンロード先のURLを直接入力しても、同じ結果だった。

```
$ curl -I http://typingart.net/fontdata/hannari.zip                                                                             
HTTP/1.1 403 Forbidden
Server: nginx
Date: Fri, 14 Apr 2017 19:18:17 GMT
Content-Type: text/html
Content-Length: 1422
Connection: keep-alive
Last-Modified: Wed, 08 Mar 2017 06:10:43 GMT
Accept-Ranges: bytes
```

ヘッダーにリファラーをつけたら成功した。

 `$ curl -H "Referer: http://typingart.net/?p=44" http://typingart.net/fontdata/hannari.zip -O`

