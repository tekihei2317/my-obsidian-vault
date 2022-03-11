# Laravelでオブジェクト指向設計をするときの方針と参考資料

まず、Eloquent Modelをドメインオブジェクトにするかどうかの選択肢があります。Eloquent Modelをドメインオブジェクトにする場合は以下の記事が参考になります。

- [5年間 Laravel を使って辿り着いた，全然頑張らない「なんちゃってクリーンアーキテクチャ」という落としどころ](https://zenn.dev/mpyw/articles/ce7d09eb6d8117)

ドメインオブジェクトをPOPOにする場合は、DDDの資料が参考になります。

- [Laravel におけるリポジトリ実装のポイント - Shin x Blog](https://blog.shin1x1.com/entry/laravel-repository)
	- リポジトリは、オブジェクトの再構築と永続化を担当する（テーブルのCRUDではない）
- [Laravel - 『ドメイン駆動設計入門』してみて Clean な世界を垣間見た話し - Qiita](https://qiita.com/anfangd/items/dc824c9768a3731045e1)
	- DDD関連の資料がまとまっている

## 参考リポジトリ

実装の参考になるリポジトリを以下に書きます。

- [shin1x1/laravel-ddd-sample](https://github.com/shin1x1/laravel-ddd-sample)

