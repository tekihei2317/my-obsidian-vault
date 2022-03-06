# my-obsidian-vault

Obsidianで書いた文書の保管庫です。

## ディレクトリ構成

```text
.
├── anki
├── daily-notes
├── learnings
└── templates
```

- `anki`
  - [Anki](https://apps.ankiweb.net/)に入れたいことを保存するディレクトリです
  - [reuseman/flashcards-obsidian](https://github.com/reuseman/flashcards-obsidian)を使ってAnki化します
- `daily-notes`
  - デイリーノートを保存するディレクトリです
  - Notionに移行したため現在は使っていません
- `learnings`
  - インプットした情報を保存するディレクトリです
  - ブログ、書籍、ポッドキャスト、動画などを解釈するために使います
- `templates`
  - [テンプレート](https://publish.obsidian.md/help-ja/%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3/%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88)を保存するディレクトリです
- ワークスペース直下
  - `Zettelkasten`を構成するノートを入れます

## ワークフロー

### 学習

本・ブログなどの情報を理解するためにまずは手書きをし、理解したことを記録するために`learnings/`に書きます。簡単な場合は直接`learnings/`に書き込みます。

本の文章を書き写しただけで理解できていないことがあるため、`learnings/`に書いた内容を適宜ノートに分割し、豆論文を書くことで理解していることを確認します。

### 整理・理解

[st3v3nmw/obsidian-spaced-repetition](https://github.com/st3v3nmw/obsidian-spaced-repetition)を使って作成したノートを見直し、リファクタリングします。`Zettelkasten`のワークフローはまだ理解・実践できていないことが多いため、今後追記します。
### 記憶

[reuseman/flashcards-obsidian](https://github.com/reuseman/flashcards-obsidian)を使って、記憶したいことをanki化します。ここは、例えば難しい本を読んでいるときに、使われている用語の意味を暗記するために使います。用語の意味を覚えることで内容を理解しやすくなります。

また、まだ試験段階ですが、太字で書いた箇所を穴埋め問題にすることができます。`Spaced Repetition`で見返すときに活用します。

![](https://i.gyazo.com/600da0988ace1f3d76797583d2823264.png)
