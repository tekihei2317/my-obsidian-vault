# vue-apolloでポケモン図鑑を作る（Part 2）

ポケモン一覧画面を作成する。

## ざっくりデザインを考える

英語版の一覧画面をそのまま参考にすることにする。[Pokédex | Pokemon.com](https://www.pokemon.com/us/pokedex/)

## データの取得処理を実装する

vue-apolloのドキュメント（https://apollo.vuejs.org/guide/）をざっくり読みます。

- apollo用の拡張機能がVSCodeにあるみたい（apollo.config.jsというのを書く）

## 画像のアスペクト比問題

サイズの異なる画像を揃えるのにいつも困っている...

ポケモンの画像は縦長のものと横長のものがあるため、揃える必要がある。全体のレイアウトはグリッドレイアウトで作っており、横幅は可変にしている。

縦幅を横幅と同じにして、画像を上下中央に揃えればできると考えた。`tailwind aspect ratio`で調べると[tailwindlabs/tailwindcss-aspect-ratio](https://github.com/tailwindlabs/tailwindcss-aspect-ratio)が見つかったため、これを使用した。

このプラグインを使用して縦横比を1:1にしてみたところ、画像が伸びていた。そのため、`object-fit: contain`を指定して親要素に収まるようにすると、いい感じになった。`object-fit`便利。

前: [[vue-apolloでポケモン図鑑を作る（Part 1）]]
次: [[vue-apolloでポケモン図鑑を作る（Part 3）]]