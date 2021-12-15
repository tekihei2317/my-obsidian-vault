# Laravelでテーブルに紐付かない概念モデルを作成する

前にやってみたときは上手くいかなくて、リレーションで誤魔化した（以下の集計と詳細を一緒に返すAPI）。DBから計算した結果に対してロジックが入ってくると有効だと思う。

## 参考

- [Laravelで複雑性と戦うための4つのTips - Qiita](https://qiita.com/pakkun/items/31c5a37c85b415f9d918)
- [Laravel Eloquent で VIEW ライクなモデルをつくる - Qiita](https://qiita.com/nunulk/items/54c2f34b0e4d4069c76c)

[[LaravelでSQLの集計と詳細を一緒に返すAPIを作成する]]