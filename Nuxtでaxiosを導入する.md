# Nuxtでaxiosを導入する

- 設定ファイルをどう書くか
- TypeScriptでの、薄めのいい感じのラッパーがあるか
	- コンポーネントにcatchとかが入るのを避けたいので

[Introduction - Axios Module](https://axios.nuxtjs.org/)

SSRなので、ちょっとわからないところがある（asyncDataの中でどうやって使うか？）

参考実装を見つける

- [tadashi-aikawa/togowl: Togowl for next generation owls](https://github.com/tadashi-aikawa/togowl)
- [potato4d/pokemon63: 「みんなの63 - スクリーンショットから自動解析できるポケモンの選出投稿サイト」のソースコード](https://github.com/potato4d/pokemon63)

`this.$axios`とか、`asyncData`の中で`$axios`で受け取るのは避けたい。クラスでラップして使いたいので。ファイルからnewすると、`config`で設定した値が使えない。

つまり、Nuxtが初期化するaxiosのインスタンスを取得する必要がある。

## 色々な例を見てみる

- [Nuxt.js×Axios×RepositoryFactoryのオレオレベストプラクティス - Qiita](https://qiita.com/lucaspoppy/items/a081beb8fdd7746a8c05)
	- axiosのインスタンスを受け取って、オブジェクトを返すクラスを作っている
	- オブジェクトには`store`、`get`みたいなメソッドがあって、それでリクエストを送る
	- asyncDataから使うのは大丈夫だけど、それ以外だと`this.$repositories`みたいにthis経由でアクセスする必要があるのがちょっと嫌
		- これはComposition APIを使わないと解決できない問題？
		- Composition APIを使えば`useContext`で解決できそう
- 普通にimportしたいのだけれど、それだとあんまり良くないのかな？
- [【Vue.js】Web API通信のデザインパターン (個人的ベストプラクティス) - Qiita](https://qiita.com/07JP27/items/0923cbe3b6435c19d761)
	- これが元ネタかな
	- 関数でリポジトリ取得するのではなく、普通にプロパティ生やせばいいのでは、と思っている（それ以外は賛成）
- [Vue 3 + TypeScript ではじめるリポジトリパターン - Qiita](https://qiita.com/blasg5884/items/394184cbf2f3ea760d4a)
	- TypeScriptのaxiosの実装が参考になる
- [Vue Composition API + TypeScriptで DI(依存性の注入）, DIP（依存性逆転の原則） を実装してみる - Qiita](https://qiita.com/ryo2132/items/03380df2df5b4b2933d7#api%E5%B7%AE%E3%81%97%E6%9B%BF%E3%81%88%E3%81%A7%E3%81%AE%E6%B4%BB%E7%94%A8)
	- provide / inject使うといいのかもしれない、Nuxtでもできるのかな？