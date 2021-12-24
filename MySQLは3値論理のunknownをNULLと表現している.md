# MySQLは3値論理のunknownをNULLと表現している

達人に学ぶSQL徹底指南書に、3値論理では`true`、`false`以外に第3の論理値として`unknown`があるという記述があった。

`unknown`は、例えば`NULL`に比較演算子を使った結果として現れる。

```text
1 = NULL → unknown
2 > NULL → unknown
NULL = NULL → unknown
```


`unknown`が真偽値であるならば、以下の`unknown` = `unknown`を表す式は`true`になるのではないかと考えたが、実際には`NULL`になった。

```sql
select (NULL = 1) = (NULL > 2); -- NULL
```

これはSQLにおいては、`unknown`という値の代わりに`NULL`を使っているからだと考えられる。つまり、以下のように評価されている。

```sql
select (NULL = 1) = (NULL > 2);
select NULL = NULL; -- unknownの代わりにNULLが使われる
select NULL; -- NULL = NULLはunknownだが、代わりにNULLが使われる
```

## 参考

- [MySQL - NULL と UNKNOWN は等価？｜teratail](https://teratail.com/questions/29384)