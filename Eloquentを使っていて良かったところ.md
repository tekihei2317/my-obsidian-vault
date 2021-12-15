#laravel #eloquent
# Eloquentを使っていて良かったところ

今のプロジェクトはLaravelの機能を取り入れて、MVC+αのアーキテクチャでやっている。以下の記事とリポジトリを参考にしている。

[5年間 Laravel を使って辿り着いた，全然頑張らない「なんちゃってクリーンアーキテクチャ」という落としどころ](https://zenn.dev/mpyw/articles/ce7d09eb6d8117)
[alexeymezenin/laravel-realworld-example-app: Laravel implementation of the RealWorld app](https://github.com/alexeymezenin/laravel-realworld-example-app/)

Eloquentを使っていて良かったことは、参照系の処理を楽に書けることである。Eloquentを使ってデータを取得し、それをAPIリソースに渡して整形するだけで良い。

Eager Loadingやリレーションも便利。

[[LaravelのEloquentを使いこなす]]
[[Eloquentを使っていてつらかったところ]]
