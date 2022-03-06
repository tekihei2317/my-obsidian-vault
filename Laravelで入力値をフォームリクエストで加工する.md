---
tags: review
sr-due: 2022-10-22
sr-interval: 230
sr-ease: 230
---

# Laravelで入力値をフォームリクエストで加工する

LaravelのAPIリソースがとても便利だったので、その逆をフォームリクエストでやりたくなった。LaravelのAPIリソースは、Eloquentのモデル（コレクション）をレスポンス用に整形するもので、返却する値（APIの仕様）を明確にすることが出来る。

その逆というと、リクエストを受け取ってコントローラーに渡す前にデータを加工することである。用途でいうと、キャメルケースをスネークケースに変換したり、...等があると思う。

## 結論

xxxクラスの`replace`メソッドまたは`merge`メソッドを使用する。名前の通り、`replace`メソッドはフォームリクエストが保持している入力値を置き換え、`merge`メソッドは入力値に値を追加する。

```php
```

## ソースコードを読んでみる

Laravelの`Request`クラス（`Illuminate\Http\Request`）のインスタンスは、入力ソースというものを持っている。入力ソースはリクエストで送られたデータを表すものである。以下が入力ソースを取得するメソッドで、HTTPメソッドに応じて返却するものを変えていることが分かる。

```php
// Illuminate\Http\Request
protected function getInputSource()
{
    if ($this->isJson()) {
        return $this->json();
    }

	// $queryプロパティと$requestプロパティは、それぞれクエリストリングとリクエストボディを表すインスタンス(Symfonyのクラス)
    return in_array($this->getRealMethod(), ['GET', 'HEAD']) ? $this->query : $this->request;
}
```

この`getInputSource()`メソッドは、リクエストインスタンスから値を取得するときに使われている。例えば、`all`メソッドや`input`メソッドで使われている。

```php
// Illuminate\Http\Concerns\InteractsWithInput（Requestクラスにmixinされているトレイト）

public function all($keys = null)
{
	// allメソッドはinputメソッドを使用している
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

そのため、この入力ソースを変更してあげればよい。`Request`クラスには`replace`メソッドと`merge`メソッドがあるので、それを使用すればよい（処理を追っていくと、入力ソースに変更を加えていることが分かった）。

```php
// Illuminate\Http\Request
public function replace(array $input)
{
    $this->getInputSource()->replace($input);

    return $this;
}

// TODO: mergeメソッド
```

## まとめ

以上の方法で、リクエストの整形処理を実装することができた。フォームリクエストがリクエストの整形とバリデーションという2つのことをしているので、改善の余地があると思う。

## 参考

- [バリデーション 8.x Laravel](https://readouble.com/laravel/8.x/ja/validation.html)
  - 入力値の加工に、`prepareForValidation`と`merge`メソッドを使っている
- [フォームリクエストでバリデーション前後にデータを加工する - Qiita](https://qiita.com/zdjjs/items/cd1c92f82f39a2475104)