---
tags: review
---

# Vuexの基礎

Vuex（というよりストア全般）はコンポーネントの「状態」「アクション」の2つをコンポーネントから分離するためにある。分離したそれらを、複数のコンポーネントで共有することによって、状態のバケツリレーを防ぐ。

## 「状態」「アクション」はVuexのどれに対応するか

- 状態
	- state
- アクション
	- action
- 「アクション」→「状態」
	- mutation
		- 状態を変更するための唯一の方法

## APIについて

- commit
	- mutationを実行する
- dispatch
	- actionを実行する

## 参考

- みんなのVue.js
- [Vue.js 状態管理の選択肢 - そのVuex本当に必要ですか - / Vue.js State Management Options - Speaker Deck](https://speakerdeck.com/kawamataryo/vue-dot-js-state-management-options)