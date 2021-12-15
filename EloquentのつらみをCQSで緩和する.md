# EloquentのつらみをCQSで緩和する

LaravelでMVC+αのコードを書いていて思ったのは、データの取得処理はEloquentとAPIリソースを活用すると楽に書けるが、少し複雑なロジックが入る登録・更新処理でEloquentをEntityとして扱うのはつらいということ。

これを解決するには、取得処理（クエリ）と更新処理（コマンド）で別々のモデルを使う、いわゆるCQSが効果的なのではないかと考えた。

具体的な実装方法はまだ分かっていないが、参考記事のように、更新処理は戦術的DDD、取得処理はFWのモデル（Eloquent）を活用すると良さそう。

## 参考

- [DDD導入に踏み切れない方へ贈る「2層 + CQS アーキテクチャ(Flyweight DDD)」/Flyweight DDD - Speaker Deck](https://speakerdeck.com/hirodragon112/flyweight-ddd?slide=76)

[[Eloquentを使っていて良かったところ]]
[[Eloquentを使っていてつらかったところ]]