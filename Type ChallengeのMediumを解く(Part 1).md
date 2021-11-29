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