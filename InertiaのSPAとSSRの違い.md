# InertiaのSPAとSSRの違い

## InertiaのSPAモード

### 初回のアクセス

初回の描画では、ページオブジェクト（Vueコンポーネントに渡すデータで、propsなどが入っている）が埋め込まれた状態のHTMLが返却されます。具体的には以下のような感じです。

Bladeファイル:

```html
<body class="font-sans antialiased">
    <div class="min-h-screen">
        <!-- Page Content -->
        @inertia
    </div>
</body>
```

レスポンス:

```html
<body class="font-sans antialiased">
    <div class="min-h-screen">
        <!-- Page Content -->
		<div id="app" data-page="JSON形式のページオブジェクト"></div>
    </div>
</body>
```

Inertiaは、ページオブジェクトをVueコンポーネントに渡し、データを受け取ったVueがDOMを構築します。データがHTMLに埋め込まれている以外は、普通のVueで作るSPAと同じです。

### リンクを使ってページ遷移したとき

`Inertia`では、`a`タグの代わりに`inertia-link`コンポーネントを使ってページ遷移を行います。`inertia-link`を使ってページ遷移すると、XHRリクエストが送られ、ページオブジェクトがJSONで返却されます。そのデータはInertiaによって、Vueコンポーネントに渡されます。

[Inertia.jsでシンプルにSPAを構築する　Inertia入門#１ | SOHO MIND](https://blog.shipweb.jp/archives/398)

## InertiaのSSRモード

Inertiaは、2022年1月にリリースでSSRに対応しました（Vue2・Vue3・Reactに対応。Svelteは現状では未対応）。

InertiaのSSRモードは、Nuxt等のSSRと全く同じです。つまりI、初回のアクセスで完全なHTMLが返却され、ページ遷移による2回目以降のアクセスは、SPAの挙動をします。

[Inertia.js SSR vs Oldschool Multiple Page for SEO](https://laracasts.com/discuss/channels/laravel/inertiajs-ssr-vs-oldschool-multiple-page-for-seo)

SSRは以下のように実現されていると思います。

1. サーバー側のアプリケーション（Ruby/PHP製）が、ページオブジェクトをHTMLに埋め込む代わりに、Node.jsのプロセスに渡す
2. Node.jsのプロセスが、ページオブジェクトをもとにHTMLを生成して、サーバー側のアプリに返す
3. サーバー側のアプリが、HTMLをレスポンスとして返す

## 参考

- [Server-side rendering (SSR) - Inertia.js](https://inertiajs.com/server-side-rendering)
- [Server-side Rendering for Inertia.js | Laravel News](https://laravel-news.com/inertia-server-side-rendering)
- [Inertia.js SSR vs Oldschool Multiple Page for SEO](https://laracasts.com/discuss/channels/laravel/inertiajs-ssr-vs-oldschool-multiple-page-for-seo)
