---
sr-due: 2021-12-25
sr-interval: 18
sr-ease: 270
---

#review

# Laravel x VueでRealwoldのGraphQL実装を作る（Part 1）

## Laravelをインストールする

- `composer create-project`

## lighthouseのインストール & 最初のクエリの作成

- lighthouseのドキュメントの通りにやる
- ide-helperがどこで機能するのかが分からない
- Apollo Studioからリクエストを送るので、corsの設定をする
- `hello`タイプをスキーマに追加してから、`lighthouse:query`コマンドでリゾルバを作成
  - `world`を返すように実装
- エンドポイントは`lodalhost:8000/graphql`なので、そこに投げる
  - できた 

```json
{
  "data": {
    "hello": "world"
  }
}
```

## usersクエリを作成する

- データベースはひとまずsqliteを使うことにした

[[RealworldのGraphQL APIをLaravelで実装する]]


