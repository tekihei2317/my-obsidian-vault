# FirestoreのCRUD処理を整理する

追加

- `setDoc`と`addDoc`がある
	- `setDoc`はIDを指定し、`addDoc`は指定しない
	- `setDoc`で同じIDのものが存在する場合は、置き換えられる
		- オプションでマージするように指定することも可能

取得