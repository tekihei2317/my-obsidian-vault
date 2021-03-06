---
tags: article
---
# 5年間 Laravel を使って辿り着いた，全然頑張らない「なんちゃってクリーンアーキテクチャ」という落としどころ

リンク: [5年間 Laravel を使って辿り着いた，全然頑張らない「なんちゃってクリーンアーキテクチャ」という落としどころ](https://zenn.dev/mpyw/articles/ce7d09eb6d8117)

- モデルにロジックを含むCRUD処理を含むと、モデルが肥大化する
	- トレイトを作ったとしても、トレイトが増えてくると大変になる
		- トレイト同士が依存をもったり、トレイトとクラスにあるものに依存が生まれる可能性があるため
	- 関数名が衝突したりしてしんどい
	- →サービスクラス（ユースケース）を作ろう
- サービスクラスに複数メソッドを書くと結局肥大化するので、シングルアクションにする
	- これはクリーンアーキテクチャにおけるユースケースに相当する
- ここでクリーンアーキテクチャを厳密に適用した場合を考える
	- ファイル数が増える
	- ユースケースからEloquentモデルを使うことが出来ないのが大変
		- ユースケース層はインフラ層に依存してはいけないため
- どうやって妥協するか？→ユースケースだけを取り入れる
- 疑問点
	- DBに依存しないEntityっぽいクラスを書きたくなったらどうする？
		- テーブルに対応しないエンティティが出てきたらどうするの？のところに回答がある
		- モデルをラップしたクラスを作って、ユースケースと同じ階層に置くことがオススメされている
			- `app/UseCases`の直下のディレクトリがパッケージみたいな感覚かな
		- > （意訳）本来、ドメインはユースケースにある抽象的な処理をまとめるためにある
			- MVCからの進化の流れを説明している気がする
	- 結局ドメインロジックはモデルや、モデルをラップしたクラスに書くということになる？
		- おそらくそうですね

## 感想

- > Q7. テーブル正規化されまくってて，超複雑かつ多機能なプロジェクトなんだけど？この案件でこの考え方使っても本当に大丈夫？
無理です。潔く Eloquent Model を今すぐ完全に捨てて，本気で DDD やる構えを見せなさい。いくらなんでも適材適所ってものがあるよ！
  - これを読んでなるほど〜となった。紹介されている構成は小〜中規模のアプリケーション向けの構成なのかなぁと思う（業務アプリというよりは、クライアント向けアプリ？向き？）
  - MVCからの正統な派生系なのかなぁと思う。そもそもActive RecordパターンがDDDやクリーンアーキテクチャと相性が悪いことが問題なのかな。
- コマンド（POST）とクエリ（GET）を分割して、クエリはEloquent依存、Commandは戦略的DDDにするのはどうだろう
  - クエリはEloquentやクエリビルダを使うと楽だが、コマンドがEloquentだとつらい経験がある
  - 日本でFlyweight DDDと呼ばれているやつ
  - 僕はこれが結構いいのではないかと思っている
	  - クエリにドメインロジックがあんまり入らないことが前提
	  - 正直ドメインロジックが何なのか、どれくらいあるのかがまだあまり想像できない