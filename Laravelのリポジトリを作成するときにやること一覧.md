# Laravelのリポジトリを作成するときにやること一覧

- [ucan-lab/docker-laravel: 🐳 Build a simple laravel development environment with docker-compose.](https://github.com/ucan-lab/docker-laravel)を使わせていただく
	- 自分でテンプレートを作ってみたい

## アーキテクチャについて

- とりあえず単一責任原則はいつも考えている
	- > 型から入る（クリーンアーキテクチャを体現する）のではなく解決したい事象である「保守のしやすさ」の実現だけを考えておけばよくて、手段を目的化してはならない。
		- [フロントエンドで長持ちするプロダクトを開発するための心構え](https://zenn.dev/okunokentaro/articles/01fs3mqbcsdr77khmnm7k8crz8)
		- 分かる。僕は逆で、なんでDDDをやるんだろう？ということが分からなくて、ずっとMVC+αしてて成長していない。
- mpywさんのなんちゃってクリーンアーキテクチャがいいのではないかと思う
	- [5年間 Laravel を使って辿り着いた，全然頑張らない「なんちゃってクリーンアーキテクチャ」という落としどころ](https://zenn.dev/mpyw/articles/ce7d09eb6d8117#%E3%83%86%E3%82%B9%E3%83%88%E3%81%A9%E3%81%86%E3%81%99%E3%82%8B%E3%81%AE%EF%BC%9F)
- 前引き継いでから一人で担当したプロジェクトは、MVC+αでゴリ押してしまった
	- 「なんちゃってクリーンアーキテクチャ」のもうちょっとゆるい感じ
	- 感想としては、取得処理はモデルのリレーションとAPIリソースを活用してきれいにかけたが、更新処理がところどころ辛かった
		- ロジックが複雑でプロパティがnullだと困るところがあったので、そこだけEntityを使ったりした
- 今趣味で作っているプロジェクトは、CommandだけDDDっぽくしようとしている
	- [DDD導入に踏み切れない方へ贈る「2層 + CQS アーキテクチャ(Flyweight DDD)」/Flyweight DDD - Speaker Deck](https://speakerdeck.com/hirodragon112/flyweight-ddd?slide=73)
	- `lighthouse-php`でGraphQLサーバーを作っている