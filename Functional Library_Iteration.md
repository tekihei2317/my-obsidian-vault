# Functional Library_Iteration

リンク: [Functional Library: Iteration](https://igor.io/2014/01/06/functional-library-iter.html)

イテレーターを使うと、必要なときにデータを取得することができる。こうすることで、メモリに展開されるデータの量を減らすことができる。

PHPの場合、イテレーターに`foreach`を使うと、遅延性がなくなってしまう。

## 感想

`use function`でインポートしたら、Intelephenseの補完が効かなくてちょっとつらかったです。

コレクション操作のライブラリを2つ使ってみました（`akanehara/ginq`、`nikic/iter`）。イテレーターを使う場所は分かってないです。

Laravelのコレクションは多機能なので、Laravelでコレクションを使いたい場合はLaravelのコレクションクラス（`Illuminate\Support\Collection`）をラップして使えばいいかなと思います

---

mapとfilterとreduceがあれば80%はカバーできて、contains（includes）、some（any）、all、first（find）もあれば配列操作の95%くらいはカバーできると思います（主観）。