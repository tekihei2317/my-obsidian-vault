---
sr-due: 2021-12-16
sr-interval: 9
sr-ease: 250
---

#review
# LaravelでSQLの集計と詳細を一緒に返すAPIを作成する

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
    "total_price": 650,
    "details": [
      { "name": "りんご", "price": 200 },
      { "name": "みかん", "price": 300 },
      { "name": "ばなな", "price": 150 },
    ],
  },
  {
    "shop_id": 2,
    "total_price": 700,
    "details": [
      { "name": "りんご", "price": 300 },
      { "name": "ぶどう", "price": 400 },
    ],
  },
]
```

## 考察

LaravelのAPIリソースを使用してレスポンスの整形を行いたいため、結果をモデルのコレクションで取得する必要があります。APIリソースの実装は、以下のようなものを想定しています。

```php
// 店ごとの商品の価格の合計を、商品と一緒に返す
class TotalPriceByShopResource extends JsonResource
{
	public function toArray($request)
    {
       	return [
            'shop_id' => $this->shop_id,
            'total_price' => $this->total_price,
            'details' => ProductResource::collection($this->products)
        ];
    }
}
```

問題は、詳細データをリレーションで取得できるようにするところです（上の実装の`$this->products`の部分）。集計結果はDBにテーブルとして存在するわけではないため、DBにレコードとして存在しないデータをモデルライクに扱えるようにする必要があります。

この問題を解決するために、[Laravel Eloquent で VIEW ライクなモデルをつくる - Qiita](https://qiita.com/nunulk/items/54c2f34b0e4d4069c76c#%E3%81%AA%E3%81%AB%E3%81%8C%E3%81%86%E3%82%8C%E3%81%97%E3%81%84%E3%81%AE%E3%81%8B)を参考に、モデルのグローバルスコープを利用して、SELECT文をモデルにマッピングすることにしました。

## 実装

### 準備

マイグレーション、シーダー、モデル、コントローラー、ルーティング、リソースを作成します。

```bash
$ php artisan make:model Product -cm　# コントローラーとマイグレーションを一緒に作成
$ php artisan make:resource TotalPriceByShopResource # 店舗ごとの価格の合計を表すAPIリソース
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

// ルーティング
Route::get('/products', [ProductController::class, 'index']);

// コントローラー
public function index()
{
    $totalPriceByShop = [];
    return TotalPriceByShopResource::collection($totalPriceByShop);
}

// モデルとリソースはそのまま
```

シーダーを実行してから`/products`にアクセスすると、空の配列が表示されます。

## 実装

### 1. 集計結果の計算

まずは、SELECT文をモデルにマッピングする用のクラスの基底クラスを作ります。ファイルパスは`app/Models/Views/View.php`にしました。

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

この状態で`/products`にアクセスすると、集計結果を確認することが出来ます。

![](https://i.gyazo.com/1079794efa576123cffb9c951a4b11f2.png)

### 2. 詳細を一緒に返すようにする

作成したモデルにリレーションを定義し、詳細を一緒に返すようにします。

モデル

```php
<?php

namespace App\Models\Views;

use App\Models\Product;
use Illuminate\Support\Facades\DB;
use Illuminate\Database\Eloquent\Builder;

class TotalPriceByShop extends View
{
	// 追加
    public function products()
    {
        return $this->hasMany(Product::class, 'shop_id', 'shop_id');
    }
}
```

リソース（価格合計、商品）

```php

<?php

namespace App\Http\Resources;

use Illuminate\Http\Resources\Json\JsonResource;

// 価格合計リソース
class TotalPriceByShopResource extends JsonResource
{
    public function toArray($request)
    {
        $result = [
            'shop_id' => $this->shop_id,
            'total_price' => $this->total_price,
			// 追加
            'details' => ProductResource::collection($this->products)
        ];

        return $result;
    }
}
```

```php
<?php

namespace App\Http\Resources;

use Illuminate\Http\Resources\Json\JsonResource;

// 商品リソース
class ProductResource extends JsonResource
{
    public function toArray($request)
    {
        return [
            'name' => $this->name,
            'price' => $this->price,
        ];
    }
}
```

これで詳細データも一緒に取得できるようになりました！

![](https://i.gyazo.com/600c329596b345d1dd60080719fbb5d4.png)

## 感想

集計と詳細データを別々に取得して、リソースでマージするほうが考えること少なくて分かりやすい気がしてきた...
↑window関数で集計を計算すれば、コレクションが1つだけで済む...？

## 参考

- [Laravel Eloquent で VIEW ライクなモデルをつくる - Qiita](https://qiita.com/nunulk/items/54c2f34b0e4d4069c76c#%E3%81%AA%E3%81%AB%E3%81%8C%E3%81%86%E3%82%8C%E3%81%97%E3%81%84%E3%81%AE%E3%81%8B)
