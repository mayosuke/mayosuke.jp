---
title: "Amazon Cloudfrontのキャッシュ無効化(Invalidation)を AWS CLIから行う方法"
date: 2021-02-03T10:26:20+09:00
draft: false
---

## Introduction

[個人サイト](https://mayosuke.jp)(このサイトのことです)のコンテンツをS3にアップロードしたあと、Amazon CloudFrontに更新を即時反映するためにinvalidateを行うのに毎回マネコンを触っている。現在のワークフローでは、サイト更新の際この作業以外ではマネコンを触る必要がないので、この作業もマネコン触らずにできるようにしたい。

## Invalidate Amazon CloudFront from AWS CLI

invalidate関係のCLIコマンドは以下のとおり。

- [create-invalidation — AWS CLI 1.18.223 Command Reference](https://docs.aws.amazon.com/cli/latest/reference/cloudfront/create-invalidation.html)
- [get-invalidation — AWS CLI 1.18.223 Command Reference](https://docs.aws.amazon.com/cli/latest/reference/cloudfront/get-invalidation.html)
- [list-invalidations — AWS CLI 1.18.223 Command Reference](https://docs.aws.amazon.com/cli/latest/reference/cloudfront/list-invalidations.html)

コマンドを実際に試してみる。試した時の環境は以下のとおり。
```
❯❯❯ aws --version
aws-cli/1.18.166 Python/2.7.16 Darwin/19.6.0 botocore/1.19.6
❯❯❯ python --version
Python 2.7.16
```

やってみた結果。
```
❯❯❯ aws cloudfront create-invalidation --distribution-id XXXXXXXX --paths "/*"
{
    "Invalidation": {
        "Status": "InProgress", 
        "InvalidationBatch": {
            "Paths": {
                "Items": [
                    "/*"
                ], 
                "Quantity": 1
            }, 
            "CallerReference": "XXXXXXXX"
        }, 
        "Id": "XXXXXXXX", 
        "CreateTime": "2021-02-03T01:21:55.655Z"
    }, 
    "Location": "https://cloudfront.amazonaws.com/2020-05-31/distribution/XXXXXXXX/invalidation/XXXXXXXX"
}
❯❯❯ aws cloudfront list-invalidations --distribution-id XXXXXXXX
{
    "InvalidationList": {
        "Items": [
            {
                "Status": "InProgress", 
                "Id": "XXXXXXXX", 
                "CreateTime": "2021-02-03T01:21:55.655Z"
            }
        ]
    }
}
❯❯❯ aws cloudfront get-invalidation --distribution-id XXXXXXXX --id XXXXXXXX
{
    "Invalidation": {
        "Status": "Completed", 
        "InvalidationBatch": {
            "Paths": {
                "Items": [
                    "/*"
                ], 
                "Quantity": 1
            }, 
            "CallerReference": "XXXXXXXX"
        }, 
        "Id": "XXXXXXXX", 
        "CreateTime": "2021-02-03T01:21:55.655Z"
    }
}
```

無事できた！

## Conclusion

Pythonからbotoでやるのは次にやってみたい。頻繁にinvalidateするのはよくなさそうなので、更新を反映するためにinvalidateするんじゃなくて、キャッシュのTTLを短くするのがいいみたい。このへんの仕組みちゃんと理解していきたい。

[CloudFrontのキャッシュをPythonから無効化(Invalidate)する | Developers.IO](https://dev.classmethod.jp/articles/invalidate-cloudfront-cache-from-python/)

> 無効機能は、予想できない状況でのみ使用できます。前もって頻繁にファイルをキャッシュから削除する必要がある場合は、ファイルのバージョニングシステムの実行または失効期間の短縮 (あるいは両方) を行います。 https://aws.amazon.com/cloudfront/faqs/

- [5分でできるS3とCloudFrontを利用したセキュアな静的Webサイトの作り方 | Developers.IO](https://dev.classmethod.jp/articles/cfn-s3-webhosting-cloudfront/)

> オリジンとして利用するS3、低コストで高い配信性能が期待できる事からキャッシュのTTLは長くせず(一律300秒)、コンテンツ更新後のキャッシュ消去(Invalidation)は極力実施しない設定とします。

## References
- [cloudfront — AWS CLI 1.18.223 Command Reference](https://docs.aws.amazon.com/cli/latest/reference/cloudfront/index.html#cli-aws-cloudfront)
- [CloudFrontのキャッシュをPythonから無効化(Invalidate)する | Developers.IO](https://dev.classmethod.jp/articles/invalidate-cloudfront-cache-from-python/)
- [5分でできるS3とCloudFrontを利用したセキュアな静的Webサイトの作り方 | Developers.IO](https://dev.classmethod.jp/articles/cfn-s3-webhosting-cloudfront/)
- [Cloudfront経由で公開しているS3にホストしたWebサイトに手動で最新のコンテンツを反映させる - mayosuke.jp](https://mayosuke.jp/post/2018-03-04-cloundfront-invalidation/)
