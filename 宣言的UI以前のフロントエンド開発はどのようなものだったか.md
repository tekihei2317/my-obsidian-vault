---
tags: review
---

# 宣言的UI以前のフロントエンド開発はどのようなものだったか

GUIプログラミングには状態・ビュー・アクションの3つの要素があります。[GUIを構成する「状態」「ビュー」「アクション」について](GUIを構成する「状態」「ビュー」「アクション」について.md)

宣言的UI以前のフロントエンド開発では、ビューと状態を同じように扱っていたり、状態の変更をビューに伝えてあげる必要がありました。

前者は、DOMを状態として扱っていたということです。例えば、チェックボックスがチェックされているかどうかを、DOMに問い合わせます。

```js
```

後者は例えばキャラクターを動かすゲームを作るときなどです。純粋なJavaScriptやjQueryでは、キャラクターのx座標を変更したからといって、ビュー上でキャラクターは動きません。状態を操作すると同時に、ビューを更新する必要がありました。

```js
player = new Player(x = 0, y = 0);
player.x += 10 // ビューは更新されない！
```