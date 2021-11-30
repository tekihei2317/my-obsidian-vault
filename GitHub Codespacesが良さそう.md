#開発環境
# GibHub Codespacesが良さそう

Docker for Macが遅いので、いっそのことLinuxを使おうと考えている。そこでクラウドIDEを調べていると、GitpodとGitHub Codespacesの2つが見つかった。GitHub Codespacesが公式なので良さそうな気がしている。

## 調査

- [GitHub Codespaces が GA しました（概要、課金など色々まとめ） - Qiita](https://qiita.com/uikou/items/1feb83865f9d638807ad#codespacesgithub-%E3%82%82%E4%BD%BF%E3%81%A3%E3%81%A6%E3%82%8B%E3%81%A3%E3%81%A6%E3%82%88)
- [メルカリShops の技術スタックと、その選定理由 | メルカリエンジニアリング](https://engineering.mercari.com/blog/entry/20210810-mercari-shops-tech-stack/)
  - 自前でcode-serverをホスティングして、ブラウザから繋いでいる？

## 機能

- ブラウザで使用する or VSCodeから使用するの2通りの使い方が出来る
- 設定ファイルは`devcontainer.json`
  - これはVSCode Remote Containersと同じ設定で出来るということ?
  - まだ使ったことがない

## 料金

最小プラン（2 Core CPU、4GB RAM）の場合は、月額約4000円くらいになりそう。とりあえずこれで試してみたい。

- Codespace Compute
  - 最小プランの場合は約3500円 / 月（1ドル = 110円、月180時間で計算）
- Codespace Storage
  - 50GB使用するとして、約400円（0.07 × 50 × 110）。


[![Image from Gyazo](https://i.gyazo.com/7a3c287c4a67a075b079d64fb53bd07a.png)](https://gyazo.com/7a3c287c4a67a075b079d64fb53bd07a)