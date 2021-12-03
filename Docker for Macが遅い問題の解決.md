## Dockerのボリュームが分からない

Dockerのボリュームの仕様がわからない...（bind mountしているディレクトリの中を、named volumeを使って共有しないようにしている）

- ディレクトリを削除すると共有されるようになった
- コンテナを起動し直すと、共有されなくなった
  - 起動したときにホストに空のディレクトリができた
  - コンテナ内には昔のデータがはいっていた（？）

## どうやっているかOSSを調査

- [Disclude a subdir from a bind mount - General Discussions - Docker Community Forums](https://forums.docker.com/t/disclude-a-subdir-from-a-bind-mount/76238)
  - 共有していないディレクトリにインストールする方法がおすすめされている
  - コンテナ内にインストールする場合はアリかな...？
- [Unifiedtransform/docker-compose.yml at master · changeweb/Unifiedtransform](https://github.com/changeweb/Unifiedtransform/blob/master/docker-compose.yml)
  - 特にボリュームで工夫しているところはなさそうだった
- [austintoddj/canvas: A Laravel publishing platform](https://github.com/austintoddj/canvas)
  - GitPodっていうのを使って、開発環境をDockerで構築しているみたい
  - docker-composeは使っていない（何使っているんだろう？）
- [forem/forem: For empowering community 🌱](https://github.com/forem/forem#contributing)
  - これもGitPodがある、使ってみようかな
  - delegatedつけているだけっぽい、とりあえずこれでいいかな...

## 参考

- [Docker の Volume がよくわからないから調べた - Qiita](https://qiita.com/aki_55p/items/63c47214cab7bcb027e0)
  - 匿名ボリューム、名前付きボリューム、バンドマウントが何か理解できる
- [docker-compose の bind mount を1行で書くな](https://zenn.dev/sarisia/articles/0c1db052d09921)

[[GitHub Codespacesが良さそう]]