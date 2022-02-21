---
tags: review
---

# ORMについて調べた雑なメモ

## Prisma（TypeScriptのORM）について

Prismaがデータベース操作の完成形だと思っている。あんまり使っていないけれど、以下の点が優れていると感じた。

- SQLに近い構文でDBに問い合わせができること
	- ORMを使っていても発行するSQLを確認するので、エンジニアはSQLを書きたいのだ
- クエリが強力に型付けされていること
- クラスにマッピングされないこと？（Active Recordパターンではないこと）

Laravelを使っているとEloquentを使うことになるが、これはActive Recordパターンである。Eloquentのモデルは使いづらいが、クエリビルダはそこまで悪くはない。

## 調べたメモ

- [Java ORマッパー選定のポイント #jsug](https://www.slideshare.net/masatoshitada7/java-or-jsug)
	- ORMをタイプで分類しており、クエリビルダ型が推奨されている
- [DDD x CQRS 更新系と参照系で異なるORMを併用して上手くいった話](https://www.slideshare.net/koichiromatsuoka/ddd-x-cqrs-orm)
	- 書き込みはHibernate（Active Record）、読み込みはjOOQ（クエリビルダ）を使用している
	- 松岡さんがTwitterで今は両方jOOQを使っていると言っていた気がする
- [PHP用ORM Emonkak\Ormの概要 - emonkak's Blog](https://emonkak.hatenablog.com/entry/2017/10/06/170737)
	- コードリーディングに良さそう

## 感想

Eloquentを使っていてつらいと思ったところは以下。Active Recordパターンの問題は、また別のところにあると思う。

- Entityとして利用するには型が貧弱
	- nullかどうかが分からないのは、ちょっと複雑なコードを書くとなるとつらい
		- これは静的型付け言語の問題なのかな...
- リレーションの表現方法が分からない
	- プロパティに勝手にEloquentのモデルのコレクションを突っ込めばいいのか？
	- そもそも勝手にプロパティを生やしていいのか？


