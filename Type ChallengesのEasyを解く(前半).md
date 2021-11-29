#TypeScript #型パズル
interfaceやtypeが何かまだ分かっていないのですが、ノリでやります。
型を表す変数のことを型変数という？（ここらへんの基本的な概念を知りたい）

前半のキーポイントは、`Mapped Types`、`Indexed Access Types`の2つです（`Conditional Types`も少し）。
後半のキーポイントは、`Conditional Types`（`infer`を使う少し複雑なもの）、`Variadic Tuple Types`の2つです。

### 1. Pick

- オブジェクト型へのマッピング（Mapped Types）
  - Union型を反復処理してオブジェクト型を作ります
- keyof
  - オブジェクト型のプロパティを、Union型で取得します

```ts
// オブジェクト型へのマッピング
type type1 = 'prop1' | 'prop2'
type type2 = {
  [key in type1]: string
} // { prop1: string, props2: string }

// keyof
type todoProps = keyof {
  title: string
  description: string
  completed: boolean
}; // { 'title' | 'description' | 'completed' }

// 解答例
type MyPick<T, K extends keyof T> = {
  [P in K]: T[P]
}
```

### 2. Readonly

- オブジェクト型へのマッピング（Mapped Types）では、プロパティに`readonly`と`?`を追加（または削除）することができます。

```ts
// 解答例
type MyReadonly<T> = {
  readonly [K in keyof T]: T[K]
};

// 削除する場合は-をつける
type CreateMutable<Type> = {
  -readonly [Property in keyof Type]: Type[Property];
};
 
type LockedAccount = {
  readonly id: string;
  readonly name: string;
};
type UnlockedAccount = CreateMutable<LockedAccount>; // { id: string, name: string }
```

### 3. Tuple to Object
- Tがタプル型である（Union型ではない）ため、直接オブジェクト型へマッピングすることは出来ません
- `T[number]`で配列の要素がとりうる型を、Union型で取得できます
- そのため、前の問題と同様に、`Mapped Types`を使うことが出来ます

```ts
// T[number]の例
type type1 = [1, 2, 'hello', 'world']
type type2 = type5[number] // 1 | 2 | "hello" | "world"

const arr = [1, 2, 'hello', 'world']
type type3 = typeof arr; // (string | number)[]
type type4 = type7[number] // string | number

// 解答例
type TupleToObject<T extends readonly string[]> = {
  [K in T[number]]: K
}
```

### 4. First of Array

- `T[0]`で、配列型`T`の0番目の要素の型を取得できます
- ただし、`T`が空の配列の場合は`T[0]`は、`undefined`になってしまいます
- 条件分岐には`Conditional Types`を使います。`T`が空の配列であるかどうかは、`T extends []`で判定できます

```ts
type First<T extends any[]> = T extends [] ? never : T[0];
```

- 分かっていないところ
  - `extends`の意味。雰囲気から察するに、`A extends B`は集合でいうと`A ⊆ B`の意味なのかなぁと思っています。

### 5. Length of Tuple

- 他のオブジェクトのプロパティの型を、添字で取得することができます（`Indexed Access Types`）
- 配列型の型変数には、（配列型の変数と同じように）`length`プロパティがあるようです

```ts
// Indexed Access Typesの例
type Person = { age: number, name: string }
type Age = Person['age'] // number
type AgeOrName = Person['age' | 'name'] // string | number(添字にUnionを指定することもできます)

type type1  = ['1', '2', '3'];
type type2 = type1['length']; // 3

// 解法
type Length<T extends readonly any[]> = T['length'];
```

### 6. Exclude

- `Conditional Types`の`T extends U`の`T`がユニオン型である場合の挙動は、少し特殊です
  - 具体的には、`T`の各要素に対して条件が適用されます（分配法則）
  - `Conditional Types`を使用する型変数を`f(T, U)`とすると、`f(type1 | type2, U) = f(type1, U) | f(type2, U)`となります
- `never`型とユニオンを取ると、`never`型は消えます


```ts
// 解答例
type MyExclude<T, U> = T extends U ? never : T;

// Conditional Typesにユニオン型を渡したときの、分配法則について
type type1 = MyExclude<'a' | 'b' | 'c', 'a'> // "b" | "c"

// → ('a' | 'b' | 'c') extends 'a' ? never : T
// → ('a' extends 'a' ? never : 'a') | ('b' extends 'a' ? never : 'b') | ('c' extends 'a' ? never : 'c')
// → never | 'b' | 'c'
// 'b' | 'c'
```

[[Type ChallengesのEasyを解く(後半)]]に続きます。