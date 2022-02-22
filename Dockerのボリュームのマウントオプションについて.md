# Dockerのボリュームのマウントオプションについて

`delegated`、`cached`、`consistent`の3つのオプションがある。

- `delegated`
	- コンテナ側の書き込みがホスト側に反映されるまでに遅延がありうる
- `cached`
	- ホスト側の反映がコンテナに書き込まれるまでに遅延がありうる
- `consistent`
	- デフォルト

ホスト側でエディタで編集しているため、ホスト側の書き込みがコンテナに反映されればよいと思い、`delegated`にした。しかし、なぜか書き込みが反映されないのが頻繁に起こる。

[[Dockerのボリュームマウントでホストまたはコンテナだけにファイルを置く方法]]

## 参考

- [Docker for Macでマウントしたvolumeの遅さに対処する · Lupus](https://www.to-mega-therion.net/docker/docker-mounted-volume-slow)
- [Docker for Mac が遅い(怒) - 箱のプログラミング日記。](https://www.y-hakopro.com/entry/2021/07/11/175236)
