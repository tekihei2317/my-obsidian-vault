# CookieのSameSite属性とはなにか

CookieのSameSite属性は、異なるサイト間でのクッキーを送信を制限するための属性で、主にCSRF対策のためのものです。

[HTTP通信やブラウザにおけるサイトとは何か](HTTP通信やブラウザにおけるサイトとは何か.md)

SameSite属性は`lax`、`strict`、`none`以下の3つの値を取ります。

`strict`は異なるサイト間でのリクエストでのクッキーを送信しません。`lax`は`SameSite`属性を指定しなかった場合のデフォルト値で、サブリクエストではクッキーを送信しません。

`none`はクッキーを送信しますが、`Secure`属性も同時に必要になります。

## 参考

- [SameSite cookies - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite)
