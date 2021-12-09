---
sr-due: 2021-12-11
sr-interval: 3
sr-ease: 250
---

#review

# Laravelで入力値をフォームリクエストで加工する

LaravelのAPIリソースが非常に便利だった。APIリソースは、データをレスポンスとして返すときに整形処理をするものである。APIリソースには、返却する値（またはAPIの仕様）を明確にするというメリットがある。

データを返すときに整形処理をするものが有用なのであれば、データを受け取ったときに整形処理をするものも有用なはずである。そのため、Laravelでどうすれば良いかを調査した。

## 調査

`Laravel リクエスト 加工`などで調べると、`prepareForValidation`と`merge`メソッドを使って、リクエストにプロパティを追加するものが出てきた。ただ今回は、受け取ったものをそのまま置き換えたかったので少し違った。

```php
```

## ソースコードを読む

Laravelの`Request`クラス（`Illuminate\Http\Request`）のインスタンスは、入力ソースというものを持っている。以下が入力ソースを取得するメソッドで、HTTPメソッドに応じて返却するものを変えている。

```php
// Illuminate\Http\Request
protected function getInputSource()
{
    if ($this->isJson()) {
        return $this->json();
    }

	// $queryプロパティと$requestプロパティは、それぞれクエリストリングとリクエストボディを表すインスタンス
    return in_array($this->getRealMethod(), ['GET', 'HEAD']) ? $this->query : $this->request;
}
```

この`getInputSource()`メソッドは、リクエストインスタンスから値を取得するときに使う、`all`メソッドや`input`メソッドで使われている。

```php
// Illuminate\Http\Concerns\InteractsWithInput（Requestクラスにmixinされているトレイト）

// allメソッドはinputメソッドを使用している
public function all($keys = null)
{
    $input = array_replace_recursive($this->input(), $this->allFiles());

    // 省略
}

// inputメソッドは、getInputSourceメソッドを使用している
public function input($key = null, $default = null)
{
    return data_get(
        $this->getInputSource()->all() + $this->query->all(), $key, $default
    );
}
```

そのため、この入力ソースを丸ごと置き換えてあげれば良いと考えた。`Request`クラスには`replace`メソッドが用意されていたのでそれを使った。ソースコードを少し追ってみると、入力ソースの内容をまるごと指定した配列で置き換えていることが分かった。

```php
// Illuminate\Http\Request
public function replace(array $input)
{
    $this->getInputSource()->replace($input);

    return $this;
}
```

フォームリクエスト側は以下のように書く（これ最初に持っていったほうがいいな...）。

```php
```

これでデータを受け取ったときの整形処理を実装することができた。しかし、フォームリクエストにレスポンスの整形とバリデーションという2つのことをしているので、そこは改善の余地があると考える。

## 参考

- [バリデーション 8.x Laravel](https://readouble.com/laravel/8.x/ja/validation.html)
  - 入力値の加工に、`prepareForValidation`と`merge`メソッドを使っている
- [フォームリクエストでバリデーション前後にデータを加工する - Qiita](https://qiita.com/zdjjs/items/cd1c92f82f39a2475104)
  - ここに大体書いてあることに気がついた。