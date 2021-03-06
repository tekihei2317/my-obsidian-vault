#TypeScript 

TypeScriptをあまり知らない状態でType Challengesに挑戦してみたところ、2問目から以下のようなコードが出てきてつまづきました。

```ts
// ???
type MyPick<T, K extends keyof T> = {
  [P in K]: T[P]
}

type Todo = {
  title:string
  description: string
  completed: boolean
};
type type1 = MyPick<Todo, 'title' | 'completed'> // { title: string, completed: string }
```

そのため、Type Challengeを解き始める前に、最低限知っておきたかったことについてまとめます。

## 目次

- 基本的な型
- 型エイリアス
- ジェネリック（ジェネリック型エイリアス）

## 基本的な型

TypeScriptには`number`、`string`、`boolean`、`union`、`array`、`tuple`、`object`などの型があります。単純な型については説明不要だと思うので、`array`、`tuple`、`object`、`union`について説明します。

### array

配列は同じ型のデータを並べたものです。`number`の配列、`string`の配列はそれぞれ`number[]`、`string[]`というように書きます。

```ts
const numArray: number[] = [3, 1, 4, 1]
const strArray = ["hello", "world"] // 型はstring[]（明示的に書かなくてもよい）
```

### tuple

`tuple`は配列の一種で、要素数とそれぞれの要素の型が決まっているものです。

```ts
type StringNumberPair = [string, number]
const a: StringNumberPair = ["hello", 100] // OK
const b: StringNumberPair = ["hello", "world"] // NG（型 'string' を型 'number' に割り当てることはできません）
const c: StringNumberPair = ["hello", 100, 200] // NG（型 '[string, number, number]' を型 'StringNumberPair' に割り当てることはできません）
```

### object

object型は、その名の通りオブジェクトを表す型です。例えば以下のように書きます。

```ts
type Person = { name: string, age: number }
const person: Person = { name: 'Taro', age: 30 }
```

オブジェクト型は、プロパティの過不足がある場合はエラーになります。

```ts
const person1: Person = { name: 'Taro' } // error（ageプロパティがない）
const person2: Person = { name: 'Taro', age: 30, email: 'taro@example.com' } // error（emailプロパティは不要）
```

不足していてもよい（省略可能な）プロパティを宣言する場合は、プロパティ名の後ろに`?`をつけます。

```ts
type Person = { name: string, age?: number }
const person: Person = { name: 'Taro' } // ageプロパティは省略可能
```

また、`readonly`修飾子をつけると、プロパティを読み取り専用にすることが出来ます。

```ts
type Person = { name: string, readonly age: number }
const person: Person = { name: 'Taro', age: 30 }
person.name = 'Jiro' // OK
person.age = 31 // error（readonlyがついているため代入できない）
```

### union型

union型は、複数の型のいずれかに当てはまるような型を表すものです。例えば、`string`または`number`をとる型は、以下のように書けます。

```ts
type stringOrNumber = string | number
```

## 型エイリアス

型エイリアスとは、その名の通り型に別名をつけるものです。以下のように`type`キーワードを使って宣言します。

```ts
type Age = number
type Person = {
  age: Age
  name: string
}
const person: Person = { age: 30, name: 'Taro' }
```

通常の変数の宣言と型エイリアスを比較してみると、型エイリアスは、ある型を変数に代入しているとも言えると思います（逆に、通常の変数の宣言は値にエイリアスをつけていると言えると思います）。

```ts
// number型にAgeというエイリアスをつけている
type Age = number
// ageという変数に30を代入している
const age = 30
```

そのため、型エイリアスのことを型変数というと考えていたのですが、型変数という用語は、後述するジェネリック型エイリアスで使用するもののことを指すようです（[型変数 (type variables) | TypeScript入門『サバイバルTypeScript』](https://book.yyts.org/reference/generics/type-variables)）。


## ジェネリック型エイリアス

ジェネリックとは、主に静的型付け言語において、特定の型を指定せずにプログラムを書くための機能のことを言います。ジェネリックを使うことで、色々な型で使用できる、変更に強いプログラムを書くことができます。

単純な例として、渡した引数をそのまま返す関数`identity`を考えます。ジェネリックを使うと、以下のようにある型`T`についての関数が書けます（型`T`は使用時に推論されます）。

```ts
function identity<T>(arg: T) {
  return arg
}
// Tはそれぞれnumber、stringと推論される
const var1: string = identity(3); // Type 'number' is not assignable to type 'string'
const var2: any[] = identity('hello') // Type 'string' is not assignable to type 'any[]'
```

ジェネリックは以下のように、型エイリアスにも使用することが出来ます。

```ts
// 型Tをnullableにするジェネリック型エイリアス
type Nullable<T> = T | null
type strOrNull = Nullable<string> // string | null
type numOrNull = Nullable<number> // number | null

// タプルを2回繰り返すジェネリック型エイリアス
type repeatTuple<T extends any[]> = [...T, ...T]
type myTuple = [number, string]
type myTuple2 =repeatTuple<myTuple> // [number, string, number, string]
```

ジェネリック型エイリアスを使用すると、型から型を作る型エイリアスを作ることができます（これは関数と考えてよいと思います）。Type Challengesは、このジェネリック型エイリアスを作る問題集です。

次回、問題の解説に続きます。

- [[Type ChallengesのEasyを解く(前半)]]
- [[Type ChallengesのEasyを解く(後半)]]

## 参考

- [プログラミングTypeScript-―スケールするJavaScriptアプリケーション開発](https://www.amazon.co.jp/%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0TypeScript-%E2%80%95%E3%82%B9%E3%82%B1%E3%83%BC%E3%83%AB%E3%81%99%E3%82%8BJavaScript%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E9%96%8B%E7%99%BA-Boris-Cherny/dp/4873119049)
- [TypeScriptの型入門 - Qiita](https://qiita.com/uhyo/items/e2fdef2d3236b9bfe74a)
- [TypeScript: Documentation - Object Types](https://www.typescriptlang.org/docs/handbook/2/objects.html)
- [TypeScript: Handbook - Generics](https://www.typescriptlang.org/docs/handbook/generics.html)
- [型変数 (type variables) | TypeScript入門『サバイバルTypeScript』](https://book.yyts.org/reference/generics/type-variables)

