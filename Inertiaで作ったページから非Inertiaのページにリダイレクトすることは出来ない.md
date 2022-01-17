#laravel #inertiajs
# Inertiaで作ったページから非Inertiaのページにリダイレクトすることは出来ない

Inertiaで作ったページから普通のBladeのページにリダイレクトしようとすると、以下のようにモーダルで表示される。修正方法が分からなかったため、BladeのページをInertia（Vue）で作り直した。

![](https://i.gyazo.com/acac10379f385c6dc16cd3829c8e3e94.png)

ページ遷移でも同様のことが起きた。Inertiaのページから`inertia-link`コンポーネントを使って非Inertiaのページに遷移しようとすると、上と同じようにモーダルが出現する。この問題は、`inertia-link`の代わりに`aタグ`を使うことで解決できた。
