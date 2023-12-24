# CloudFormation-Beginners-Handson
CloudFormation入門者用のハンズオンを改良したテンプレートファイルです。
![サムネイル](./img.jpg)

## 概要
CloudFormationの入門ハンズオンを改良したものです。
参考にした記事は下に記載をしています。
プラスアルファでいくつか設定を変更しています。

## 参考にした記事
CloudFormation入門者にはとてもわかりやすい記事でした。

【AWS入門】CloudFormation【ハンズオン】
https://devlog.neton.co.jp/middleware/cloudformation/

## この記事を実践する前に気をつけること
- 作業するリージョンの確認：
  (私の場合は東京リージョン用に変更して作業をしました)
- ami-idを変更する。
  記事のままのami-idを指定しても動かないので調べて変更する。
- pemファイルをダウンロードしたらパーミッションを変更する。

## プラスアルファで加えた変更
- 東京リージョンに作成するように変更
- VPCのCidrBlockを10.0.0.0/16に変更
- セキュリティグループを2つに分割して各インスタンスに異なるセキュリティグループを設定
- パブリックサブネットのEC2インスタンスにElasticIPを割り当てるように変更
- カスタムネットワークACLを設定

## 動作確認に使用するコマンド
最終的に、プライベートサブネット内のEC2インスタンスにSSH接続するために使用するコマンドです。

```

# ホストマシンからリモートマシンにpemファイルを転送する
scp -i testkeypair.pem -r testkeypair.pem ec2-user@<Elastic IP Address>:/tmp

パブリックサブネットにssh接続する
ssh -i testkeypair.pem ec2-user@<Elastic IP Address>

プライベートサブネットにssh接続する
ssh -i /tmp/testkeypair.pem ec2-user@<Private IP Address>

```

