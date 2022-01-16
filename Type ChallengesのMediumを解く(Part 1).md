### 1. Get Return Type

- inferで推論する
- 任意の関数を表す型は、(...args: any) => any
- EasyのParametersと同じだった

```ts
type MyReturnType<T extends (...args: any) => any> = T extends (...args: any) => infer U ? U : never;
```

### 2. Omit

- keyof Tは、オブジェクト型TのキーをUnion型で取得する
- mapped typesは、Union型を反復して、オブジェクト型を生成する
- mapped typesのas句でneverを返すと、そのキーは除外される

```ts
// mapped typesのas句でキーを除外する例
type RemoveHogeField<T> = {
  [K in keyof T as K extends 'hoge' ? never : K]: T[K]
  // [K in keyof T as Exclude<K, 'hoge'>]: T[K] でもOK
}

interface Hoge {
  hoge: string,
  fuga: string,
  piyo: number
}
type type1 = RemoveHogeField<Hoge>; // { fuga: string, piyo: number}

// Solution
type MyOmit<T, K extends keyof T> = {
  [P in keyof T as P extends K ? never : P]: T[P]
}
```

### 3. Readonly 2

- 交差型
  - `T & U`は`T`であり、かつ`U`であるような型
- 交差型は両方の条件を満たす必要があるので、同じプロパティ`prop`についての条件がある場合は、両方の条件を満たす必要があります
  - つまり、`prop`が片方で`readonly`で、もう一方で`readonly`でない場合は、`readonly`になります（指定なし⊃`readonly`のため？←本当？）
- そのため、指定されたプロパティ`K`を`readonly`にしたオブジェクト型と、元のオブジェクト型`T`の交差型をとればよいです

```ts
// readonlyなプロパティとそうでないプロパティの交差型
type Type1 = { aaa: string } & { readonly aaa: string }
type Type2 = { readonly aaa: string } & { aaa: string }

const obj1: Type1 = { aaa: "aaa" }
obj1.aaa = "bbb" // error（読み取り専用プロパティであるため、'aaa' に代入することはできません。）

const obj2: Type2 = { aaa: "aaa" }
obj2.aaa = "bbb" // error（読み取り専用プロパティであるため、'aaa' に代入することはできません。）

// 解答例（TS Playground上ではreadonlyになっていなかった）
type MyReadonly2<T, K extends keyof T = keyof T> = T & {
  readonly [P in K]: T[P]
}

// 解答例（TS PlaygroundでOKだったもの）
type MyReadonly2<T, K extends keyof T = keyof T> = Omit<T, K> & {
  readonly [P in K]: T[P]
}
```


### 4. Deep Readonly

- Conditional Typesには再帰が使えるのでそれを使う
- 問題はオブジェクトかどうかの判定で、`T extends {}`や`T extends Object`だとうまくできない
  - `function`を渡した場合も`true`になる
- オブジェクトかどうかの判定は、`T extends Record<string, unknown>`で出来るらしい
  - `unknown` => `any`にすると駄目だった（`extends`も含め、よく分かっていない）

```ts
type DeepReadonly<T> = {
  readonly [K in keyof T]: T[K] extends Record<string, unknown> ? DeepReadonly<T[K]> : T[K]
}
```

## 参考

すごそうなのを見つけた。http://typescript.ninja/typescript-in-definitelyland/index.html