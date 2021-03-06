# git MOC

- [[gitを使い始めたときに知りたかった5つのこと]]
- [gitで指定した日時以前の最新のコミットを取得する](gitで指定した日時以前の最新のコミットを取得する.md)
- gitを全く知らない状態からプルリクエストを送れるようになるまで
	- 🐵大体以下の知識があれば大丈夫だと思います
	- そもそもなぜgitを使うのか
	- gitのインデックスとワーキングツリーを理解する（基本）
		- addコマンド
		- diffコマンド
	- gitのコミットとブランチについて理解する
	- gitのリモート追跡ブランチについて理解する
	- gitのマージについて理解する
		- マージには早送りマージとマージコミットを作るマージの2種類がある
	- gitのフェッチについて理解する
		- マージと組み合わせるとプルになる
	- gitのリベースについて理解する
		- よくある問題
			- コミットを間違える→amend、rebase -i + edit
	- gitのインデックスとワーキングツリーを理解する（応用）
		- resetコマンド
	- gitのコンフリクトの解消方法について理解する
	- その他、知ってると便利なこと
		- スタッシュコマンド
		- ブランチモデル
		- gitのコンフィグについて（グローバル、ローカル）
		- コミットをvimやVSCodeで開く
			- コミットメッセージを修正しやすいので便利（複数行書くこともできる）
- VSCodeのGit Graphを使いながら説明するのはそれなりに需要がありそう
	- git問題集とかがあるとなお良い
- FAQ（よくあるパターン集）を作って、関連箇所への解説にリンクを貼る
	- addを取り消したい→git reset→ワーキングツリー、インデックス、HEADの解説