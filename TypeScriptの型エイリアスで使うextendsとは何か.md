---
tags: review
---

# TypeScriptの型エイリアスで使うextendsとは何か

ジェネリック型エイリアスを作るときに、ジェネリック型に制約をつけたり、Conditional Typesで条件分岐をするために`extends`を使います。

TypeScriptのConditional Typesのドキュメントには、割り当て可能と書いてあります。

> When the type on the left of the extends is assignable to the one on the right, then you’ll get the type in the first branch (the “true” branch); otherwise you’ll get the type in the latter branch (the “false” branch).

`T extends U`というのは、TがUの部分集合である（？）ことや、TがUのサブタイプである（？）ということを表しているっぽいです。

- [TypeScript: Documentation - Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html)