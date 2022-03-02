# article_作りながら学ぶDIコンテナ

リンク: [作りながら学ぶDIコンテナ](https://zenn.dev/y_ahiru/articles/learn-a-di-container)

かんたんなDIコンテナはすぐ作れる。

- defineメソッド
	- キーとクラス名の対応を保存する配列
- getメソッド
	- 定義したクラスをインスタンス化して取得する
	- PHPではインスタンス化するときのクラス名に変数を使える
		- `new Hoge`と`new Hoge()`は同じ？

```php
$className = 'Hoge';
new $className(); // new Hoge()と同じ
```


```php
<?php

class Container
{
    /** @var array<string, string> */
    private array $definitions = [];

    public function define(string $id, string $className)
    {
        $this->definitions[$id] = $className;
    }

    public function get(string $id)
    {
        if (!isset($this->definitions[$id])) {
            return null;
        }

        $className = $this->definitions[$id];

        return new $className;
    }
}

class Hoge
{
}

$container = new Container;
$container->define('hoge', Hoge::class);

$instance = $container->get('hoge');
var_dump($instance);
```

## 依存しているクラスを自動でインスタンス化する

この実装だと、例えばHogeクラスがFugaクラスに依存している場合にエラーが起きる。

```php
class Hoge
{
    private Fuga $fuga;

    public function __construct(Fuga $fuga)
    {
        $this->fuga = $fuga;
    }
}

class Fuga
{
}
```

そのため、コンストラクタの引数にクラスのインスタンスがある場合は、そのクラスをインスタンス化することにする。PHPではリフレクションのAPIがあるため、それを使ってコンストラクタの引数を解析してインスタンス化する。

リフレクションは、プログラムの実行中にプログラム自身の情報を読み取ったり書き換えたりすること。メタプログラミングと呼ばれたりする。

`get`メソッドを以下のように書き換える。以下の2点に注意する。

1. 再帰的にインスタンス化している
2. 識別子とクラス名が同じ場合は、定義しなくてもインスタンス化できるように変更している

```php
public function get(string $id)
{
    $className = $this->definitions[$id] ?? $id; // 注意点2
    $ref = new ReflectionClass($className);
    $constructor = $ref->getConstructor();

    if ($constructor === null) {
        return new $className;
    }

    // コンストラクタの依存先をインスタンス化する
    $args = [];
    foreach ($constructor->getParameters() as $parameter) {
        $type = $parameter->getType()->getName();
        $args[] = $this->get($type); // 注意点1
    }

    return new $className(...$args);
}
```

## 感想

とても分かりやすかった。アルゴリズムの問題を解いているみたいで楽しかった。
