#laravel #eloquent
# Eloquentを使っていてつらかったところ

Eloquentは更新系には向いていないと考えている。

単純な登録・更新処理であれば、フォームリクエストでバリデーションした値を`validated`で取得し、それをEloquentモデルで保存すればよい。しかし、そこにロジックが入ってくると辛くなる。

具体的には、プロパティが`null`を取りうるのかが分からなかったり、永続化していないデータのリレーションをどのように扱えば良いのかが分からなかったのが辛かった。

アプリケーションの登場人物として扱う場合は、Eloquentのモデルより、POPOのEntityのほうが向いている。Eloquentの複雑な実装について考えなくて良いので、扱いやすい。

[[Eloquentを使っていて良かったところ]]