# shin1x1/laravel-ddd-sample

リンク: [shin1x1/laravel-ddd-sample](https://github.com/shin1x1/laravel-ddd-sample)

具体的な実装方法について調べる。

```text
packages/Acme/Shop
├── Application
│   ├── Controllers
│   ├── Requests
│   └── UseCases
├── Domain
│   ├── Exceptions
│   └── Models
│       ├── Cart
│       │   └── Test
│       ├── Item
│       └── Test
└── Infrastructure
    ├── Eloquents
    └── Repositories
        ├── Application
        │   └── HttpSession
        └── Domain
            ├── Array
            └── Eloquent
```

- ディレクトリ構成
	- `Application`
		- コントローラーとリクエストはいったんLaravelのデフォルトのままにする
	- `Domain`
		- `Models`配下が結構特徴があるので、あとで再調査する
- リポジトリ
- ユースケース
	-  ドメインオブジェクトを使ってロジックを組み立てる
	- ユースケースのインターフェイスはプリミティブにしているっぽい（ドメインオブジェクトではない）
- エンティティ
	- DBを使う実装はなかった（配列の場合のみ）

## Models配下を見る

- `Domainable.php`
	- `toDomain`メソッドのインターフェイス（Eloquentなどで使う）
	- Eloquentモデルがドメインオブジェクトと1:1対応している場合に使う？
- `Identifier.php`
	- IDを値オブジェクトにするとき用の抽象クラス
- `None.php`
	- 空のインターフェイス（どこかで使っている？）
- `PositiveNumber.php`
	- 正の整数を値オブジェクトにするとき用の抽象クラス
- `Cart.php`
	- 一番ビジネスロジックが書かれているクラス

## 気になっていること

- 保存前のドメインオブジェクトのIDには何を入れればいいのか
