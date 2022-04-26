# 読んで学ぶTypeScript Part 2

文: [文 | TypeScript入門『サバイバルTypeScript』](https://typescriptbook.jp/reference/statements)
関数: [関数 | TypeScript入門『サバイバルTypeScript』](https://typescriptbook.jp/reference/functions)

## 文

JavaScriptにはグローバルオブジェクトという変数がたった一つ存在し、グローバルオブジェクトのプロパティとグローバル変数は同じである。ブラウザの場合のグローバルオブジェクトは`window`で、Node.jsの場合は`global`である。

for-of文で配列のインデックスを取得したい場合は`Array.prototype.entries`メソッドを使う。この関数はイテレーターを返す。

TypeScriptでは、catchしたエラーは`any`型になる。なぜかというと、JavaScriptでは任意の型の値をスローできるからである。コンパイラーオプションの`useUnknownInCatchVariables`をオンにすると、catchしたエラーを`unknown`型にすることができる。

TypeScriptでは、Union型の変数について型を条件分岐で判定することで型を絞り込むことができる。`typeof month === string`などのように、型を条件判定に使うことを型ガードと呼ぶ。型ガードでは特定クラスのインスタンスであることを判定する`instance of`、プロパティを持っているか判定する`in`演算子なども使える。

unknown型はちょっと安全なany型である。どちらもどんな型の変数も代入できるが、any型はどんな変数にも代入できる一方、unknown型は特定の型には代入できない。また、unknown型のプロパティにアクセスするとエラーになる。unknown型は主に、「まだ型が分かっていないけれどこれから絞り込むとき」に使用する。

## 関数

TypeScriptの関数は、戻り値の型は推論されるが、引数の型は推論されずany型になる。noImplicitAnyをオンにしている場合はエラーになるため、基本的に引数には型注釈を書くことになる。

TypeScriptの関数の型宣言には、型エイリアス（type）を使用する。アロー関数や関数式には型注釈を書くことができるが、関数宣言は代入しないため型注釈を書くことができない。また、既存の関数に`typeof`演算子を使うことで関数の型を取得することができる。

`void型`は、基本的には戻り値のない関数の型注釈にのみ使用する。関数の戻り値の型注釈に使用する場合は、`undefined型`と同じになるが、`undefined型`を指定した場合は`return undefined;`と書く必要がある（あまり使わない気がする）。


