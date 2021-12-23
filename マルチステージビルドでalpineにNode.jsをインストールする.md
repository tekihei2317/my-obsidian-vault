 # マルチステージビルドでalpineにNode.jsをインストールする
 
 LaravelのコンテナにNode.jsをインストールする必要があり、バージョンを固定したかったので、Laravelにマルチステージビルドでcomposerをインストールする方法を真似して以下のようにやってみた。

```dockerfile
FROM node:16.13.1-alpine3.12 as node

# ここでwarningが出る（tarは相対パスで固めたほうがよい）
RUN tar czf node.tar.gz \
    /usr/local/bin/node \
    /usr/local/bin/npm \
    /usr/local/bin/npx \
    /usr/local/lib/node_modules

FROM php:fpm-alpine3.13

COPY --from=node /node.tar.gz /node.tar.gz
RUN cd / && tar xzf node.tar.gz
 ```

 `tar`で固めているのは、`/usr/local/bin/npm`が`/usr/local/lib/node_modules`配下の実態へのシンボリックリンクになっているため。単純に`COPY`すると、シンボリックが展開された実態がコピーされる。
 
~~このやり方だとインストールはできたが、`npm`コマンド実行時に謎のパーミッションエラーが出た。調べてみると、解決方法で`npm`をインストールし直してくださいと書かれていたので、この方法だと正しくインストール出来ていないような気がする。~~

`npm run`がどの権限で実行されているかが分からないが、とりあえず`777`にすると動いた（やばい）

 ## 参考
 
-  [複数の言語の runtime を持つ Docker image を作る - Qiita](https://qiita.com/izumin5210/items/cf14a1ea58fb82d36bb2)
	  - 一般的なやり方について書かれている
- [Dockerのmulti-stage buildでNodeの実行ファイルをコピーして使う | Simple is Beautiful.](https://blog.kozakana.net/2018/11/node_multistaging_build/)
  - Nodeでの具体的なやり方について書かれている
- [Docker のマルチステージビルド (Multi Stage Build) で Symbolic Link を使う - Qiita](https://qiita.com/qualitia_cdev/items/721d7e27d9ec1e3a4318)
 - [tar: Removing leading `/’ from member names の警告を消す方法 | キュア子の開発ブログ](https://curecode.jp/tech/tar-removing-leading-from-member-names/)
