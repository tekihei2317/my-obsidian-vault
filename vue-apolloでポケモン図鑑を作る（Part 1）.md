 # vue-apolloでポケモン図鑑を作る（Part 1）

vue-apolloの試運転。8時間くらいで作りたいなぁ。ポケモンのGraphQL APIは[ここ](https://graphql-pokemon2.vercel.app/)から試すことが出来る。

## 作成するページと情報

- ポケモン一覧（トップページ）
  - 図鑑番号
  - 画像
  - ポケモン名
  - タイプ
- ポケモン詳細
  - 分類
  - 高さ、重さ
  - 特性
  - 進化（他のポケモンへのリンクにする）
  - 説明（あれば）

## とりあえずクエリを作ってみる

```graphql
fragment PokemonBasicInfo on Pokemon{
  id
  number
  name
  types
  image
}

query fetchPokemons {
  pokemons(first: 10) {
    ...PokemonBasicInfo
  }
}

query fetchPokemon {
  pokemon(id: "UG9rZW1vbjowMDE=") {
    ...PokemonBasicInfo
    classification
    height {
      minimum
      maximum
    }
    weight {
      minimum
      maximum
    }
    evolutions {
      ...PokemonBasicInfo
    }
  }
}
```

特性と説明以外は取得することが出来た。

 ## デザインの参考
 
 - [メガフシギバナ｜ポケモンずかん](https://zukan.pokemon.co.jp/detail/003-1)
 - [Pokédex | Pokemon.com](https://www.pokemon.com/us/pokedex/)

## 参考

- [GraphQL Pokémon を使って楽しく学ぶ GraphQL クエリ - kakakakakku blog](https://kakakakakku.hatenablog.com/entry/2019/12/30/135420)

[[vue-apolloでポケモン図鑑を作る（Part 2）]]に続く。