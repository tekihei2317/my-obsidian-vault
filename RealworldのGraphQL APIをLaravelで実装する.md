# RealworldのGraphQL APIをLaravelで実装する

[[GraphQLの参考資料まとめ]]

RealworldのLaravelのGraphQL APIの実装が多分ないので、勉強も兼ねて自分で作ってみようと思う。Realworldは`REST API`向けに作られているため、`GraphQL API`の公式の仕様書はおそらくない（`GraphQL API`のNode.js実装とRails実装のスキーマをパッと見たところ、同じではなかった）。

`dostu`さん（RailsとReactのGraphQL実装を作ってる方）が、GraphQLのAPIの仕様書を作成してくれているので、それを参考に作ってみようと思う。
[rails-graphql-realworld-example-app/GRAPHQL_API_SPEC.md at master · dostu/rails-graphql-realworld-example-app](https://github.com/dostu/rails-graphql-realworld-example-app/blob/master/GRAPHQL_API_SPEC.md)

話はそれるがRealworld以外のGraphQL APIの実装例はここから色々見れる（Repoからリポジトリが見れる）。
[APIs-guru/graphql-apis: 📜 A collective list of public GraphQL APIs](https://github.com/APIs-guru/graphql-apis)

## 参考実装

### バックエンド

- Hapi（Node.jsのフレームワーク？）
	- [realworld-graphql/src at master · thebergamo/realworld-graphql](https://github.com/thebergamo/realworld-graphql)
- NestJS + MongoDB + GraphQL
	- [ramzitannous/medium-graphql-nestjs: A medium like graphql server using nestjs + graphql](https://github.com/ramzitannous/medium-graphql-nestjs)
- なんか色々
	- [jsBlackBelt/microservices-realworld-app: A realworld app implementation using nx, nest.js & graphql using a micro-services approach](https://github.com/jsBlackBelt/microservices-realworld-app)
- Rails
  - [dostu/rails-graphql-realworld-example-app: Exemplary real world backend GraphQL API built with Ruby on Rails https://realworld.io](https://github.com/dostu/rails-graphql-realworld-example-app)

### フロントエンド

- React + Apollo
  - [dostu/rails-graphql-realworld-example-app: Exemplary real world backend GraphQL API built with Ruby on Rails https://realworld.io](https://github.com/dostu/rails-graphql-realworld-example-app)

### フルスタック

- Elm + Hasura
	- [andrewMacmurray/realworld-hasura: Realworld inspired blogging platform (Remake of Conduit) using Hasura + Purescript + Elm](https://github.com/andrewMacmurray/realworld-hasura)

