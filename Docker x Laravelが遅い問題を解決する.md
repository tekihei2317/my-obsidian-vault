# Docker x Laravelが遅い問題を解決する

遅いなぁとは思いつつも作業していたが、計測してみると、レスポンスが返ってくるまでに3.0s~3.5sくらいかかっていたので、流石に改善しないとと思った。

やってみることは以下。

- node_modulesをコンテナにマウントしない
  - Nodeはホストで動かしたほうが速い（本当？）のでホストで動かしている
- vendorをホストにマウントしない
- データベースのデータをホストにマウントしない

## やってみる

- node_modules（228M）を削除
  - 2.7s ~ 3.0sになった
- db-store（209M）を削除
  - 2.5s ~ 2.75sになった
- vendorをホストにマウントしないように変更
  - named volumesを使うように変更
  - インストールパスを変えて、永続化しないようにするのも良いかも？
- `Generating optimized autoload files`が永遠に終わらなくなった
  - 11:13~終わらなかった
  - 11:32~11:35（docker-cleanしてdocker daemon再起動すると動いた〜、なんじゃこれ）

## 参考

