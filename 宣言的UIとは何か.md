---
tags: review
---

# 宣言的UIとは何か

宣言的UIとは、「画面は状態の関数」であるという考え方です。つまり、状態が決まればUIが決まるということです。

仮想DOMなど技術を使って、クライアント側で持っている状態が変わったときに、DOMを更新することで実現します。

宣言的UIによって、jQueryなどのDOMを直接操作する技術は過去のものになりました。

[[フロントエンドの状態管理とは何か]]
[[宣言的UI以前のフロントエンド開発はどのようなものだったか]]

## 参考

- [宣言的UI - Speaker Deck](https://speakerdeck.com/sonatard/xuan-yan-de-ui)
	- 確かこのスライドで宣言的UIってのが重要なんだなぁと思った記憶がある
	- 「クラスコンポーネントのライフサイクルフックは時間的凝集を強いる」、なるほど
		- 凝集度については最近見たCAの講義資料にも書かれていた
- [宣言的UIって何なん？ 〜日本昔ばなし「やめ太郎」〜 - Qiita](https://qiita.com/Yametaro/items/3c27305072464e1d6230)
	- シンプルで分かりやすい
- [なぜ仮想DOMという概念が俺達の魂を震えさせるのか - Qiita](https://qiita.com/mizchi/items/4d25bc26def1719d52e6)
	- 原典
- [宣言的UIはReact Hooksで完成に至り、現代的設計論が必須の時代になる - Qiita](https://qiita.com/erukiti/items/fb7bcbd9d79696579d06)

