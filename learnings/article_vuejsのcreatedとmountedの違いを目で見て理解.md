# article_vueのcreatedとmountedの違いを目で見て理解

リンク: [vue.jsのcreatedとmountedの違いを目で見て理解 | アールエフェクト](https://reffect.co.jp/vue/vue-js-created-mounted-diffrence)

以下を実行してみるとなんとなく分かった。CDNでHTMLを読み込んで使用している。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app">
      <h1>Hello, world!</h1>
      <div v-if="isShow">Hello, world!</div>
      <button @click="showEl">show el</button>
      <button @click="updateEl">update el</button>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
    <script src="js/main.js"></script>
  </body>
</html>
```

```js
new Vue({
  el: '#app',
  data: {
    message: 'Hello, world!',
  },
  beforeCreate() {
    console.log('before create');
    console.log(document.querySelector('#app'));
    console.log({ message: this.message });
    console.log('-----');
  },
  created() {
    console.log('created');
    console.log(document.querySelector('#app'));
    console.log({ message: this.message });
    console.log('-----');
  },
  mounted() {
    console.log('mounted');
    console.log(document.querySelector('#app'));
    console.log({ message: this.message });
    console.log('-----');
  },
});

```

![](Pasted%20image%2020220304173759.png)

つまり、以下のことが分かる。

- `beforeCreate`→`created`のタイミングで`data`プロパティが使えるようになっている
- `created`→`mounted`のタイミングで、DOMが構築されている

つまり、`created`は`data`プロパティが使えるようになるタイミングで、`mounted`はDOMの構築が終わった（構築が始まった？）タイミングである。

---

以下はまだ理解できていない現象。

何回か試すと以下のようになることがあった。

![](Pasted%20image%2020220304174328.png)

ここの`Compile el's innerHTML as template`っていうのが終わっている場合と、終わっていない場合によって違いが出ているのだと思う。終わっている場合は空っぽで、終わっていない場合はHTMLに書いたものがそのまま表示される。

> 🐵じゃあなんでbefore createのときはelのinnnerHTMLは空になっているのだろう？

![](Pasted%20image%2020220304174517.png)

以下のようになることもあってますます分からない...。

![](Pasted%20image%2020220304175047.png)