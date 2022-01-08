# Firestoreでサブコレクションを追加する

- `users/user_id/profiles/profile_id`のようなものを作る
- addDocで親ドキュメントを作成
	- IDは自動で割り振られるようにする
- 追加したドキュメントのリファレンスからIDを取得し、addDocでドキュメントを追加する

```js
const userData = {
  name: `test ${new Date().toLocaleString()}`,
  email: 'test@example.com',
};

const userProfileData = {
  age: 18,
  prefecture: 'Hyogo',
};

const user = await addDoc(collection(db, 'users'), userData);
const userProfile = await addDoc(collection(db, 'users', user.id, 'profiles'), userProfileData);
```

`profile`サブコレクションを追加することが出来た。中身は`userProfileData`が入っている。

![](https://i.gyazo.com/6e7d9035d7421ea7a28186414f867f94.png)

## 参考

- [Firestore v9: サブコレクションにデータを追加＆取得する](https://zenn.dev/hiro__dev/scraps/bfe3ca1757ffae)
