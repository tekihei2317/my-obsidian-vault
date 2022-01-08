# WebアプリをAlfredでデスクトップアプリと同様に起動する

- とりあえずChromeのショートカットを作成する
	- `~/Applications/Chrome\ Apps.localized/`配下にあるのでそこを検索結果に追加する
	- 反映されない
- そもそもAlfredはアプリケーションをどうやって検索しているのだろう？
- `~/hoge/`を検索対象に含めるには？
	- `~/hoge`を検索対象に追加して、アプリケーション検索のキャッシュを削除するとできた
	- ディレクトリを直接追加しないと反映されなかった（嘘だろ...）
- `~/Applications/Chrome\ Apps.localized/<APP_NAME>`は検索対象に追加できなかった
	- Finder上フォルダではなくアプリだとみなされているからかな
- `Flotate`というアプリがある
	- 検索がブラウザ標準じゃなかったりするので不安
- `~/Applications/Chrome\ Apps.localized/<APP_NAME>`を`/Applications/<APP_NAME>`に移動することにした
	- うーん微妙

## 参考

- [2019年に使い始めた便利Tools まとめ - まっせぎ blog](https://masegi.hatenablog.com/entry/useful_tools_2019#Flotate---%EF%B8%8FDeprecated)