---
title: "Cloudfront経由で公開しているS3にホストしたWebサイトに手動で最新のコンテンツを反映させる"
date: 2018-03-04T15:07:37+09:00
draft: false
---

1. AWSマネージメントコンソールにログインし、[ClourFront](https://console.aws.amazon.com/cloudfront/home)のダッシュボードを開く

2. キャッシュを更新したいWebサイトのDistributionを選択する

3. Invalidationタブを開いて、「Create Invalidation」ボタンをクリックする

4. ポップアップウィンドウの「Object Paths」に「/*」と入力して、「Invalidate」をクリックする

