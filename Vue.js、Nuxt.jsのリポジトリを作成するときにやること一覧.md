# Vue.js、Nuxt.jsのリポジトリを作成するときにやること一覧

- 公式ドキュメントを見ながらプロジェクトを初期化する
	- Vue→`vue create`、Nuxt→`create-nuxt-app`
	- テンプレートリポジトリを作りたい
- Prettierの設定をする
	- あんまりすることはない（`printWidth: 120`、`singleQuote: true`くらい）
- ESLintの設定をする
	- 難しい
- コミット時にLinter、Formatterが実行されるようにする
- コンポーネントライブラリやCSSをどうするか
  - `Element UI` 
  - `Scoped CSS`
  - `Tailwind CSS`

### アーキテクチャ

- とりあえず単一責任原則だけはいつも考えている
- フロントエンドの基本として、通信、状態管理、表示処理を分離する
- API呼び出し周りを整備する
- Composition APIを導入する（Vue2、Nuxt2の場合）
- 適切にコンポーネント分割する
	- 例えばフォームとテーブルの両方を一つのコンポーネントに書いて肥大化したら、分ける
	- 200行のコンポーネントとかは、あんまり読みたくないので
- 参考になりそうな資料
	- [2020年に立ち上げたWebフロントエンド構成の振り返り](https://zenn.dev/yoshiko/articles/32371c83e68cbe)
		- [「3種類」で管理するReactのState戦略](https://zenn.dev/yoshiko/articles/607ec0c9b0408d)
	- [Webフロントエンドの開発効率を高く保つための考え方](https://zenn.dev/adwd/articles/e173f75c512e10)
	- [大規模チームの中でフロントエンドを立ち上げて2ヶ月経ったのでまとめる](https://zenn.dev/erukiti/articles/frontend-team-building)
	- [フロントエンドで長持ちするプロダクトを開発するための心構え](https://zenn.dev/okunokentaro/articles/01fs3mqbcsdr77khmnm7k8crz8)
	- [経年劣化に耐える ReactComponent の書き方](https://zenn.dev/takepepe/articles/howto-withstand-aging-react-component)
	- [テスト優先度をあげたくなる実話 - フロントエンド版 -](https://zenn.dev/takepepe/articles/frontend-testing-motivation)