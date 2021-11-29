### 6 .Exclude

- 型の定義で使われるT extends U は、多分T ⊆ U の意味だと思う
- 条件分岐のある型（Conditional Types）にUnionを渡すと、Unionの各要素に対して条件分岐が適用される
- neverとのUnionを取るとneverは消える

```ts
// Unionの各要素に適用される例（分配法則）
type ToArray<Type> = Type extends any ? Type[] : never;
type StrArrOrNumArr = ToArray<string | number>; // string[] | number[]

// Solution
type MyExclude<T, U> = T extends U ? never : T;
type type1 = MyExclude<"a" | "b" | "c", "a">;
type type2 = MyExclude<"a" | "b" | "c", "a" | "b">;
```

### 7. Awaited

- Conditional Typeのextends節の中で、inferキーワードで型を推論させることができる
  - extendsでinferを使って構造を指定して、構造に当てはまった場合は推論した型を当てはめる
- Conditional Typeは入れ子にも出来るし、再帰も使える（すごい）

```ts
// extendsの中での型推論
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
type type4 = ReturnType<(...args: string[]) => number>; // number
type type5 = ReturnType<(...args: string[]) => { field: string }>; // { field: string }
type type6 = ReturnType<number>; // never

// Solution(Promise入れ子の場合は未対応)
type Awaited<T> = T extends Promise<infer U> ? U: never;

// Solution(Promise入れ子の場合に対応)
type Awaited<T extends Promise<any>> = T extends Promise<Promise<infer U>>
  ? Awaited<Promise<U>>
  : T extends Promise<infer U>
  ? U
  : never;
```

### 8. If

- Conditional Typesとextendsの確認
- true | falseは、booleanと全く同じ（多分）なので改善できました

```ts
// Solution
type If<C extends true | false, T, F> = C extends true ? T : F;
// Solution(improved)
type If<C extends boolean, T, F> = C extends true ? T : F;

type type1 = If<true, 'a', 'b'>;
type type2 = If<false, 'a', 'b'>;
```

### 9. Concat

- 型システムでも、タプルに対してスプレッド構文を使うことができる（Variadic Tuple Types）

```ts
// Solution
type Concat<T extends any[], U extends any[]> = [...T, ...U];

type type1 = Concat<[1, 2], ['hello', 'workd']>; // [1, 2, 'hello', 'world']
```

### 10. Includes

- 配列型`T`に対して`T[number]`とすると、配列の要素の型のUnionが取得できる

```ts
const array = [1, 2, 'hello'] as const;
type arrayType = typeof array; // [1, 2, 'hello']
type elementType = arrayType[number]; // 1 | 2 | 'hello'

// Solution(部分点)
type Includes<T extends readonly any[], U> = U extends T[number] ? true: false;
```

- ただし、extendsは以下のような場合にtrueになってしまうため、この解法は間違っている
  - 満点解法はまだ理解していない

```ts
type type4 = true extends boolean ? true : false;　// true
type type5 = { a: 'A' } extends {} ? true : false; // true
```

### 11. Push

- Concatと同じ考えで解ける（Variadic Tuple Types）

```ts
type Push<T extends any[], U> = [...T, U];
```

### 12. Unshift

- これもタプル型のスプレッド演算
- 可変個のタプル型ってあるのかな？（可変個だったら配列？）
  - [string, string, ..., number, number]みたいなもの 

```ts
type Unshift<T extends any[], U> = [U, ...T];
```

### 13. Parameters

- スプレッド構文とinferを組み合わせる
- 以下の例だと、typeof func1を渡したとき、...argsには[arg1, arg2]が入っている（？）
  -  良く分かっていない
- このタプル型の型をinferで推論すると、[arg1: string, arg2: number]となる

```ts
// Solution
type MyParameters<T extends (...args: any[]) => any> = T extends (...args: infer U) => any ? U : never;

const func1 = (arg1: string, arg2: number): void => {};
type type1 = MyParameters<typeof func1>; // [arg1: string, arg2: number]
```
