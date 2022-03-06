# 実践Terraform　AWSにおけるシステム設計とベストプラクティス

## メタデータ

著者: 野村 友規
メモ作成日: 2021-12-23
書籍リンク: [実践Terraform　AWSにおけるシステム設計とベストプラクティス](https://www.amazon.co.jp/%E5%AE%9F%E8%B7%B5Terraform-AWS%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E8%A8%AD%E8%A8%88%E3%81%A8%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-%E6%8A%80%E8%A1%93%E3%81%AE%E6%B3%89%E3%82%B7%E3%83%AA%E3%83%BC%E3%82%BA%EF%BC%88NextPublishing%EF%BC%89-%E9%87%8E%E6%9D%91-%E5%8F%8B%E8%A6%8F-ebook/dp/B07XT7LJLC)

## 要約・考えたこと

- 本に印をつけながら全部読む
- 終わったあとに、印をつけたところを読み返しながら、重要だと思った箇所を抜き出す

2章

- EC2インスタンスの場合、user_data（起動時のコマンド）を指定するとインスタンスを再作成する必要があった
- 変数、ローカル変数と出力方法
- terraformはaws cliをバックエンドで利用している？

3章

- TypeScriptみたいな補完とLintがほしい
  - そこにどういうプロパティを書けるのかが知りたい
- `リソース種別.リソース名`で他のリソースを参照できる
- モジュールの作成
  - モジュールのインターフェイスは、入力→`variable`、出力→`output`で定義する
- `terraform console`コマンドでREPLを起動できる
  - あれこれ競技プログラミングできるのでは？

5章 IAM

- IAMのロールとポリシーが良くわかっていない

7章 ネットワーク

- セキュリティグループのアウトバウンドルールって必要なのだろうか
  - ネットワークに繋がっていないのでyumで失敗していた、必要ですね
  - 外からアクセスするには不要

8章 ロードバランサとDNS

- ロードバランサとは何か
  - [１台のEC2でもELBを使うメリットについてまとめてみました | DevelopersIO](https://dev.classmethod.jp/articles/benefit_elb_with_one_ec2/)
  - 負荷分散以外にも、死活監視、インスタンスの差し替え、SSLの設定などのメリットがある

9章 コンテナオーケストレーション

- 検証レベルでECSを使っていいものなのかが分からない
 - [迷える子羊に捧げるコンテナ環境徹底比較　〜ECS、Fargate、EKSは何が得意で不得意か〜 - Speaker Deck](https://speakerdeck.com/hamadakoji/mi-eruzi-yang-nipeng-gerukontenahuan-jing-che-di-bi-jiao-ecs-fargate-ekshahe-gade-yi-debu-de-yi-ka?slide=109)
 - とりあえず迷ったらECS on Fargateとある