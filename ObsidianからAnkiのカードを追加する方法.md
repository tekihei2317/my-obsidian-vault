---
tags: review
---

# ObsidianからAnkiのカードを追加する方法

[reuseman/flashcards-obsidian: 🎴 An Anki plugin for Obsidian.md](https://github.com/reuseman/flashcards-obsidian)を使って、ObsidianからAnkiのカードを作成します。

- 普通のノートに使うと汚れるので、Anki用のObsidianのノートを作成する
- カードを追加するための文法
	- 方法1
		- h2、h3タグなどの後ろに`#card`タグを付ける
	- 方法2
		- `問題::答え`の形式で文章を書く
		- 単純な問題の場合はこれでいいと思います
- 穴埋め問題を作るための方法
	- `{}`で穴埋めしたい箇所を囲む
		- 1つの文の中で複数使うこともできます
		- リスト（箇条書き）の中で使うこともできます
	- `{1:___}`、`{2:___}`のようと、個別に穴埋め問題を作成することができる
		- あんまり用途は分かりませんが
		- 複数作って個別に穴を開けられるようにしたい
