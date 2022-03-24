---
tags: review
---

# Composition APIの基礎

Composition APIを使うことによって、Options APIでthisに依存していたことによってコンポーネントに書かざるを得なかった処理を、別の場所に分離することが出来る。

また、Options APIのルール（リアクティブなデータを`data`に書く、メソッドは`methods`に書く、...）に縛られずに、純粋なJavaScriptのコードを書くことができる。

余談だが、thisに依存する処理をVueのミックスイン機能を使って分離することもできる。しかし、これはミックスインとコンポーネントの依存関係をコントロールできないためアンチパターンである。

[コンポーネントをまたぐ関心事の共通化の歴史](コンポーネントをまたぐ関心事の共通化の歴史.md)

## 参考

- [コンポーネントを小さく・きれいに設計しよう。Vue Composition APIを活用したコンポーネント分割術 - ICS MEDIA](https://ics.media/entry/210929/)
- [Vue3とComposition APIの概要を一気に解説 - YouTube](https://www.youtube.com/watch?v=XIpQLdcqawc)
- [Vue 2.xのOptions APIからVue 3.0のComposition APIへの移行で知っておくと便利なTips - ZOZO TECH BLOG](https://techblog.zozo.com/entry/vue-options-api-to-composition-api)
