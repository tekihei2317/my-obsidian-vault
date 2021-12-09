---
sr-due: 2021-12-11
sr-interval: 3
sr-ease: 250
---

#review

# Vueでチェックボックスのコンポーネントを実装する

[Vue.jsでFormの各要素をComponent化する際の覚え書き - Qiita](https://qiita.com/ryo2132/items/2e3fcedaffeff9fc3967#checkbox)のやり方を参考に実装したが、`v-model`で渡す変数に初期状態があった場合チェックされないという改善点がある。

Vueのドキュメントを見てみると、以下のようにチェックボックスの各要素に`v-model`を使用して値を渡していた。

```html
<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
<label for="jack">Jack</label>
<input type="checkbox" id="john" value="John" v-model="checkedNames">
<label for="john">John</label>
<input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
<label for="mike">Mike</label>
```

`v-model`はどのコンポーネントに使用するかによって、何の省略形かが変化する。チェックボックスの場合は、`checked`プロパティと`change`イベントを使用するとドキュメントにある。

そこで`checked`プロパティに配列を渡してみると、すべてのチェックボックスが選択された（JavaScriptで配列は`truthy`なため）。

```html
```

そのため、以下のように、各チェックボックスに対して、選択状態かどうかを判定する必要がある。`find`を使うと計算量が少し気になる（問題にはならないレベルだが）ので、`Map`を使うと良いかもしれない。

```html
```

チェックボックスでの`v-model`が何の省略系かどうかが気になる。

## 参考

- [Vue.jsでFormの各要素をComponent化する際の覚え書き - Qiita](https://qiita.com/ryo2132/items/2e3fcedaffeff9fc3967#checkbox)
- [フォーム入力バインディング — Vue.js](https://jp.vuejs.org/v2/guide/forms.html)
- [チェックボックス（input type="checkbox"）の使い方 - HTMLリファレンス](https://code-kitchen.dev/html/input-checkbox/)