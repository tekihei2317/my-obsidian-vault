# Cloud Functions for Firebaseでステータスコード200以外を返す

ドキュメントに書いてある。[アプリから関数を呼び出す  |  Firebase Documentation](https://firebase.google.com/docs/functions/callable#handle_errors)

以下のように、`functions.https.HttpsError`例外を投げればよい。

```javascript
// ドキュメントより引用
if (!(typeof text === 'string') || text.length === 0) {
  // Throwing an HttpsError so that the client gets the error details.
  throw new functions.https.HttpsError('invalid-argument', 'The function must be called with ' +
      'one arguments "text" containing the message text to add.');
}
```

`functions.https.HttpsError`の第一引数に渡したキーに応じて、ステータスコードが変化する。例えば上記のように`invalid-argument`を渡した場合は、`400 Bad Request`になる。

また、`functions.https.HttpsError`以外の例外が発生した場合は、ステータスコードとメッセージ（？）は`internal`にマスクされる。

> 関数から HttpsError 以外のエラーがスローされると、クライアントでは代わりにメッセージ INTERNAL とコード internal が含まれるエラーを受け取ります。

## 余談: 適切なレスポンスを返すことの重要性

既存の実装を見てみると、`{ status: 500 }`みたいなレスポンスを返していて、それは無視されていた。アプリの実行を継続できない状態のまま実行されることのマズさを実感できた。いわゆる、車が壊れているのに走り続けている状態。

例えば登録処理で登録ができていないのに`CREATED`のレスポンスが返されるのは問題がある。ちゃんと動いていないなら、ちゃんと動いていないことを表すデータを返してほしい。