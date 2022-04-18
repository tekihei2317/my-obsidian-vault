# サバイバルTypeScript

リンク: [TypeScript入門『サバイバルTypeScript』〜実務で使うなら最低限ここだけはおさえておきたいこと〜](https://typescriptbook.jp/)

## TypeScriptのあらまし

知らなかったことを以下に書きます。

TypeScriptがコンパイルするJSのバージョンを指定することができます。

ECMAScriptはJavaScriptの使用を定義したもので、毎年更新されています。

ブラウザはJavaScriptエンジン（V8、SpiderMonkey等）とレンダリングエンジン（Blink、Gecko、Webkit）で出来ています。レダリングエンジンはHTMLやCSSを解釈して、文字や画像を配置する位置を計算します。

知らなかったツールには、CLIアプリケーションフレームワークのoclif、IaCツールのPulumiがあります。PulumiはTypeScriptやGoで記述することができ、AWS・Azure・GCPなどに対応しています。

## 作って学ぶTypeScript

### 簡単な関数を作ってみよう

npmでtypescriptパッケージをインストールすると、tscコマンドが使えるようになる。tscコマンドでTypeScriptをJavaScriptにコンパイルすることができる。

## 読んで学ぶTypeScript

### nullとundefinedの違い

nullとundefinedの違いはなにかというと、nullは「代入すべき値がない」undefinedは「代入していないので値がない」という意味です。

意味に応じて使い分けるべきという意見もありますが、**使い分けるメリットはあまりないため、こだわりがなければundefinedに統一することが本書ではおすすめされていました**。実際、TypeScriptの開発チームは「nullは使わずundefinedを使う」というシンプルなコーディングルールを採用しているようです。

### ラッパーオブジェクトへの変換

JavaScriptのプリミティブ型（数値、文字列）にはメソッドがありませんが、メソッドを呼び出すときにラッパーオブジェクトに変換されるためメソッドを呼び出すことができます。このラッパーオブジェクトへの変換をボックス化といいます。

### オブジェクトのプロパティ

JavaScriptのオブジェクトはプロパティの集合です。プロパティには、数値や文字列といったプリミティブ型だけではなく、関数を代入することもできます。これはいわゆるメソッドです。

双変と共変、気になる...。

### readonlyについて

readonlyはプロパティへの代入を制限するものです。一方でconstは、変数への代入を制限するものです。readonlyをすべてのプロパティに付与したい場合は、組み込みの`Readonly<T>`型が便利です。


### 余剰プロパティチェックについて

オブジェクト型にの変数対してオブジェクトリテラルを代入するときのみ、余剰プロパティのチェックが行われます。

```ts
const xy: { x: number; y: number } = { x: 1, y: 2 };
let onlyX: { x: number };
// onlyX = { x: 1, y: 2 }; // コンパイルエラーになる
onlyX = xy;
console.log(onlyX); // { x: 1, y: 2 }
```

noUncheckedIndexedAccessをオンにすると、厳密に定義していない（インデックス型で定義した）プロパティにアクセスしたときの型が、インデックス型で指定した型とundefined型のユニオンになります。