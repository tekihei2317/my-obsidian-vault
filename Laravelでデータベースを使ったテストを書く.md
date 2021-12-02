# Laravelでデータベースを使ったテストを書く

## Model Factoryの使い方

RailsでFactory Botを使ったことがあるので、それと大体同じものだと思う。やりたいことは、

- 明示的に指定しない場合は初期値が使われる
- 初期値を上書きすることができる
- 関連するモデルを同時に作成することができる

など。

```php
// モデルのインスタンス化
// makeメソッドを使う

// 永続化
// createメソッドを使う

// 値の上書き
// 1. メソッドを定義して、内部でstate関数を呼ぶ）
// 2. makeメソッド、createメソッドに上書きする値を渡す

// 関連するモデルの作成
```

## 参考

- [データベーステスト 8.x Laravel](https://readouble.com/laravel/8.x/ja/database-testing.html)
- [Eloquent Model Factory を使ってテストデータを整備する - Qiita](https://qiita.com/nunulk/items/06370af1594a10faa749)
