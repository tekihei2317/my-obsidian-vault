# Firestoreのサブコレクションとは何か

- サブコレクションは、ドキュメントの中にあるコレクションのこと
- Firestoreでは、ドキュメントやコレクションの位置はパスで表現できる
	- `users` → ユーザーのコレクション
	- `users/sato` → IDが`sato`のユーザーのドキュメント
- `collection/document/subcollection/document`のようにネストさせられる
	- コレクションとドキュメントが交互になるようにしか作れない
	- コレクション内のコレクションや、ドキュメント内のドキュメントは作れない
- Firesotreのリファレンスとは
	- ドキュメント・コレクションの位置を指すオブジェクト

## 参考

- [Cloud Firestore データモデル  |  Firebase Documentation](https://firebase.google.com/docs/firestore/data-model?hl=ja#web-version-9_1)
