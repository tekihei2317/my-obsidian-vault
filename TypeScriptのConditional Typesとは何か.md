# TypeScriptのConditional Typesとは何か

TypeScriptのConditional Typesとは、条件によって分岐する型のことです。Conditional Typesは、型レベルでの三項演算です。

```ts
type If<C extends boolean, T, F> = C extends true ? T : F // CがtrueのときT、falseのときFを返す型

type First<T extends any[]> = T extends [] ? never: T[0]; // 配列の最初の要素の型を求める型
```

Conditional Typesの条件部分には`extends`キーワードを使います。`A extends B`は、AがBのサブタイプである、またはBがAに割り当て可能であることを表します。

[TypeScriptの型エイリアスで使うextendsとは何か](TypeScriptの型エイリアスで使うextendsとは何か.md)

## 参考

- [TypeScript: Documentation - Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html)