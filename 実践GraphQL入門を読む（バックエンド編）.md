## 感想

- 型定義をするときの`Lighthouse`のディレクティブに補完が効かないのがつらい（特にMutation）
  - 補完用のファイルを生成するコマンドがあるらしい
  - [LaravelにLighthouseを導入してGraphQLサーバーを作る - Fusic Tech Blog](https://tech.fusic.co.jp/posts/2019-12-08-laravel-lighthouse-graphql-server/)
  - 使っているバージョンにはまだ追加されていないっぽかった
- コードをかなりたくさん書いてから動作確認することになるので、もう少し細かい単位に分けられていたら嬉しい
- `Follows`テーブルと`Followers`テーブルの両方はいらない（中間テーブルが2つある状態）
  - 1が2をフォローしたとき`(accout_id, follow_id) = (1, 2)`を`Follows`テーブル、`(account_id, follower_id) = (2, 1)`を`Followers`テーブルに入れている

[[実践GraphQL入門を読む（フロントエンド編）]]