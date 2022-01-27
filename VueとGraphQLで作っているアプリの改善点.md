---
tags: vue,graphql
---

# VueとGraphQLで作っているアプリの改善点

- NuxtにComposition APIを導入する
	- [Nuxt Composition API](https://composition-api.nuxtjs.org/)
- vue-apolloをComposition APIで使う
	- 多分v4に上げればよい
	- [Vue Apolloを@vue/apollo-composableに書き換える - Qiita](https://qiita.com/toshi1973814/items/1a33d536a685e67980b6?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items)
	- Nuxtで使っているのでアップデートできるか分からない
		- これで出来そう
		- [Nuxt.js と @nuxtjs/apollo 構成で @vue/apollo-composable を使えるようにする | ラッコWeb](https://don-bu-rakko.com/nuxt-js-%E3%81%A8-nuxtjs-apollo-%E6%A7%8B%E6%88%90%E3%81%A7-vue-apollo-composable-%E3%82%92%E4%BD%BF%E3%81%88%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%99%E3%82%8B/)
- TypeScriptを使う
	- VueファイルでTypeScriptを使うとどこが変わるんだろう？
	- あんまりイメージが沸かない
- graphql-codegenを使う
	- GraphQLのスキーマからTypeScriptの型定義を作るやつ？
- エラーハンドリングを書く
	- 500が出ると普通に死ぬと思う
	- apolloの設定が必要
- [GraphQLクライアントを使ってNuxtアプリケーションの実装をする](https://zenn.dev/sterashima78/articles/e6f1281f4ea8e3)
	- 拡張機能を入れれば、graphqlファイルを書くときに補完が効くみたい

順番的には、Composition API→TypeScript→graphql-codegenかな？