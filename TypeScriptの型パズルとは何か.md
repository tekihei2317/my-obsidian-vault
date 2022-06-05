# TypeScriptの型パズルとは何か

TypeScriptの型パズルとは、**ある型から目的の型を得られるような、ジェネリック型エイリアスを作ること**です。ジェネリック型エイリアスとは、簡単に言うと「型から型を作る関数」です。

例えば、組み込み型の`Pick<T, K>`は、レコード型`T`とユニオン型`K`を引数にとって、`T`から`K`に含まれるプロパティだけを残した型を作る関数（ジェネリック型エイリアス）です。

```ts
type Todo = {
  title: string
  description: string
  completed: boolean
}

type TodoPreview = Pick<Todo, 'title' | 'completed'> // { title: string, completed: boolean }
```

`Pick<T, K>`は以下のように自作することができます。

```ts
type MyPick<T, K extends keyof T> = {
  [k in K]: T[k]
}
```

このように、TypeScriptの型の演算の機能を使って、目的の型が得られるような型を作ることが型パズルです。
