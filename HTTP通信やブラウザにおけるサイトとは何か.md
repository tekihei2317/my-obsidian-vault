# HTTP通信やブラウザにおけるサイトとは何か

サイト（Site）とはざっくり説明すると、同じドメインにあるWebページの集まりのことで、同じ組織によって運営されます。

サイトをより厳密にいうと、登録可能なドメインのことです。つまり、ドメインの公開接尾辞（`com`、`org`、`co.uk`など）とその1つ前のドメインを合わせたもののことをいいます。

以下の2つのURLは、登録可能なドメイン`mozilla.org`が同じため同一サイトです。

- `https://developer.mozilla.org/en-US/docs/`
- `https://support.mozilla.org/en-US/`


以下の2つのURLは、登録可能なドメインが異なるため同一サイトではありません。

- `https://developer.mozilla.org/en-US/docs/`
- `https://example.com`

## 参考

- [Site - MDN Web Docs Glossary: Definitions of Web-related terms | MDN](https://developer.mozilla.org/en-US/docs/Glossary/Site)
	- 日本語だと省略されていて良く分かりませんでした
- [same-site/cross-site, same-origin/cross-originをちゃんと理解する](https://zenn.dev/agektmr/articles/f8dcd345a88c97)
