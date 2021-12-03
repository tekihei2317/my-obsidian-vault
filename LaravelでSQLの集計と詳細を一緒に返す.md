# LaravelでSQLの集計と詳細を一緒に返す

商品を表す以下のようなテーブルがあるとします。

|ID|店舗ID|商品名|価格|
|-|-|-|-|
|1|1|りんご|200|
|2|1|みかん|300|
|3|1|ばなな|150|
|4|2|りんご|300|
|5|2|ぶどう|400|

以下のように、店舗ごとの商品の価格の合計と、その詳細を一緒に返すAPIを実装したいです。

```json
[
  {
    "shop_id": 1,
    "price_total": 650,
    "details": [
      { "name": "りんご", "price": 200 },
      { "name": "みかん", "price": 300 },
      { "name": "ばなな", "price": 150 },
    ],
  },
  {
    "shop_id": 2,
    "price_total": 700,
    "details": [
      { "name": "りんご", "price": 300 },
      { "name": "ぶどう", "price": 400 },
    ],
  },
]
```

## 考察

LaravelのAPIリソースを使用してレスポンスの整形をするため、結果をモデルのコレクションで取得する必要があります。APIリソースの実装は、以下のような感じです。

```php
```

問題は、詳細データをリレーションで取得できるようにするところです。集計結果はDBにテーブルとして存在するわけではないため、そのようなデータをモデルライクに扱えるようにする必要があります。

結論としては、[Laravel Eloquent で VIEW ライクなモデルをつくる - Qiita](https://qiita.com/nunulk/items/54c2f34b0e4d4069c76c#%E3%81%AA%E3%81%AB%E3%81%8C%E3%81%86%E3%82%8C%E3%81%97%E3%81%84%E3%81%AE%E3%81%8B)を参考に、モデルのグローバルスコープを利用して、SELECT文をモデルにマッピングすることにしました。

## 実装

ブラウザでサクッとLaravelを実装できる環境を起動できるようにしたい...今日のタスクが終わったらやってみようと思います。

### 準備

マイグレーション、シーダー、モデル、コントローラー、ルーティング、リソースを作成します。

```bash
$ php artisan make:model Product -cm
$ php artisan make:resource TotalPriceByShopResource
```

```php
// マイグレーション
Schema::create('products', function (Blueprint $table) {
    $table->id();
    $table->unsignedInteger('shop_id')->comment('店舗ID');
    $table->string('name')->comment('商品名');
    $table->unsignedInteger('price')->comment('価格');
    $table->timestamps();
});

// ルーティング
Route::get('/products', [ProductController::class, 'index']);

// コントローラー
public function index()
{
    $totalPriceByShop = [];
    return TotalPriceByShopResource::collection($totalPriceByShop);
}

// モデルとリソースはそのまま

// シーダー
public function run()
{
    $products = [
        ['shop_id' => 1, 'name' => 'りんご', 'price' => 200],
        ['shop_id' => 1, 'name' => 'みかん', 'price' => 300],
        ['shop_id' => 1, 'name' => 'ばなな', 'price' => 150],
        ['shop_id' => 2, 'name' => 'りんご', 'price' => 300],
        ['shop_id' => 2, 'name' => 'ぶどう', 'price' => 400],
    ];

    foreach ($products as $product) {
        Product::create($products);
    }
}
```

シーダーを実行してから`/products`にアクセスすると、空の配列が表示されると思います。

## 実装

### 1. 集計結果の計算

まずは、SELECT文をモデルにマッピングする用のクラスの基底クラス（以降Viewクラス）を作ります。ファイルパスは`app/Models/Views/View.php`にしました。

```bash
touch app/Models/Views/View.php
```

```php
<?php

namespace App\Models\Views;

use Illuminate\Database\Eloquent\Model;

abstract class View extends Model
{
    protected $fillable = [];

    final public function __set($key, $value)
    {
        throw new \RuntimeException('this class is just readable.');
    }
}
```

次に、このクラスを拡張して、集計結果を保持するモデルを作ります。グローバルスコープで集計のクエリを実行しています。

```bash
touch app/Models/Views/TotalPriceByShop.php
```

```php
<?php

namespace App\Models\Views;

use Illuminate\Support\Facades\DB;
use Illuminate\Database\Eloquent\Builder;

class TotalPriceByShop extends View
{
    protected $table = 'products';

    protected static function boot()
    {
        parent::boot();

        static::addGlobalScope('core', function (Builder $builder) {
            $builder
                ->groupBy('shop_id')
                ->select('shop_id', DB::raw('SUM(price) as total_price'));
        });
    }
}
```

この状態で`/products`にアクセスすると、集計結果を確認することが出来ました。

![](https://i.gyazo.com/1079794efa576123cffb9c951a4b11f2.png)

### 2. 詳細を一緒に返すようにする

作成したモデルにリレーションを定義し、詳細を一緒に返すようにします。

```php

```

## 参考

- [Laravel Eloquent で VIEW ライクなモデルをつくる - Qiita](https://qiita.com/nunulk/items/54c2f34b0e4d4069c76c#%E3%81%AA%E3%81%AB%E3%81%8C%E3%81%86%E3%82%8C%E3%81%97%E3%81%84%E3%81%AE%E3%81%8B)

