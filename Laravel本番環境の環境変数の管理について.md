#laravel
# Laravelの本番環境の環境変数の管理について

DBのパスワードなどの秘匿情報をgitの管理に含めるのはよろしくないので、どうすればよいか調査した。

## 環境変数の優先順位について

プロセスに設定されている値 >  docker-compose.ymlで設定した値 > Laravelの`.env.${APP_ENV}` > Laravelの`.env`

docker-composeについて

環境変数が設定済みの場合はそちらが使用される。環境変数が存在しない場合は、`environment`や`env_file`の値が設定される。

laravelのenvについて

環境変数が設定済みの場合はそちらが使用される（要出典）。環境変数が存在しない場合は、ファイルの値が設定される（要出典）。使用されるファイルは、`.env.${APP_ENV}`が存在する場合はそれで、存在しない場合は`.env`が使われる。

## どうすればよいか

秘匿情報（DBのパスワードやAPIキーなど）はプロセスに設定しておき、それ以外はLaravelの`.env.{$APP_ENV}`に設定すればよい。秘匿情報をプロセスに設定する方法がまだ分かっていない。

`docker-compose`でデプロイする場合は、`KEY=VALUE docker-compose up`のようにすると、その値が優先して使用される。こういうことをCDサービスで設定すればよい？

`ECS`でデプロイする場合は、`S3`から読み込んだり、`AWS Systems Manager Parameter Store`を使ったりするらしい。

## 参考

- [[Laravelの環境変数について]]
- [ECSコンテナに環境変数を設定する3つの方法 - DENET 技術ブログ](https://blog.denet.co.jp/cloudformation-ecs-setenv/#1_%E3%83%99%E3%82%BF%E6%9B%B8%E3%81%8D)
- [[アップデート]ECS on EC2で環境変数の設定がS3から参照できるようになりました | DevelopersIO](https://dev.classmethod.jp/articles/ecs_ec2_env_s3/)
  - 割と最近のアップデートで出来るようになったんですね