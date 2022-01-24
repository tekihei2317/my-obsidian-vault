# 既存のGraphQL APIからスキーマを取得する方法

イントロスペクションという機能があることは知っていたが、具体的にどうやってスキーマを取得するかを知らなかった。

[prisma-labs/get-graphql-schema](https://github.com/prisma-labs/get-graphql-schema)を使うと、CLIでGraphQL APIからスキーマを取得できる。

現在、LaravelのLighthouseというライブラリを使ってAPIを開発している。Lighthouseでは独自のディレクティブを定義しているため、これを直接スキーマとして解釈することはできない。そのため、APIから直接スキーマを取得して、それをモックサーバーなどで使用する。

参考: [既存のGraphQLサービスからSchemaを取得する](https://zenn.dev/nekoshita/articles/7c454e8e552c0d)

上記の記事にはcurlで取得する方法も書かれている。