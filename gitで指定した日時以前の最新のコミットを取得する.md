---
sr-due: 2021-12-27
sr-interval: 8
sr-ease: 130
---

#review

# gitで指定した日時以前の最新のコミットを取得する

`git log`の`--pretty`オプションと`--before`（`--until`）オプションを使えば良い。

```bash
git log --before "2021-12-05 00:00:00 +09:00" --pretty="format:%H" | head -n 1
```

この例では、2021年12月5日以前（12月5日は含まない）の最新のコミットハッシュが取得出来る。

## 注意点

`--before`オプションで日時とタイムゾーンを指定している理由は、日付のみを指定した場合だと標準時で計算されていそうだったため。

例えば`--before=2021-12-05`と指定したとき、`2021-12-05 01:00:56(+9)`のコミットは含まれたが、`2021-12-05 20:49:18(+9)`のコミットは含まれなかった。

## タイムゾーンについて検証

`--before`は指定した日付を含まない（older than）と`git log --help`に書いてあった。そのため、おそらく標準時で計算していると推測。適当に日時とタイムゾーンを指定すると想定した挙動になった。

TODO: 信頼できる情報源を見つける→見つからなさそうなので検証してみよう
TODO: 境界値で`---before`で日時を指定したとき、指定した日時も含んでいた（20:49:18とすると20:49:18のコミットが含まれたが、20:49:17とすると含まれなかった）。実は閉区間である可能性と、日時を指定した場合はそれを含む可能性の2つある。

## 参考

```text
$ git log
commit f97f9e7e948c8fc6c32f6286efee303c73028f7b (HEAD -> main)
Author:     tekihei2317 <tekihei2317@gmail.com>
AuthorDate: Sat Jan 1 09:00:01 2022 +0900
Commit:     tekihei2317 <tekihei2317@gmail.com>
CommitDate: Thu Dec 9 17:43:33 2021 +0900

    commit 3

commit 2c7abe4d47bedacdb015f22a06a23427248f445e
Author:     tekihei2317 <tekihei2317@gmail.com>
AuthorDate: Sat Jan 1 09:00:00 2022 +0900
Commit:     tekihei2317 <tekihei2317@gmail.com>
CommitDate: Thu Dec 9 17:43:09 2021 +0900

    commit 2

commit 31c53de6633360649a289b4a3dea95a4cf7e4e27
Author:     tekihei2317 <tekihei2317@gmail.com>
AuthorDate: Sat Jan 1 08:59:59 2022 +0900
Commit:     tekihei2317 <tekihei2317@gmail.com>
CommitDate: Thu Dec 9 17:42:29 2021 +0900

    commit 1

$ git rebase -i @~3 --committer-date-is-author-date
$ git log
commit ba91a02af688e57c662403f168167ffbcae3d011 (HEAD -> main)
Author:     tekihei2317 <tekihei2317@gmail.com>
AuthorDate: Sat Jan 1 09:00:01 2022 +0900
Commit:     tekihei2317 <tekihei2317@gmail.com>
CommitDate: Sat Jan 1 09:00:01 2022 +0900

    commit 3

commit 0ec674947142561c3e54aa246cc7d3356826295e
Author:     tekihei2317 <tekihei2317@gmail.com>
AuthorDate: Sat Jan 1 09:00:00 2022 +0900
Commit:     tekihei2317 <tekihei2317@gmail.com>
CommitDate: Sat Jan 1 09:00:00 2022 +0900

    commit 2

commit 5aac641a161351ec7489a02496f2cff9b849253f
Author:     tekihei2317 <tekihei2317@gmail.com>
AuthorDate: Sat Jan 1 08:59:59 2022 +0900
Commit:     tekihei2317 <tekihei2317@gmail.com>
CommitDate: Sat Jan 1 08:59:59 2022 +0900

    commit 1

```

- 日付だけ指定した場合は標準時で計算している気がする
  - 違う気がする
  - 01:00→含まれる
  - 09:00→含まれる
  - 21:00→含まれない
- タイムゾーンを指定していない場合は現在のタイムゾーンで計算している
- 範囲は閉区間（境界を含む）

- [Git - コミット履歴の閲覧](https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E5%9F%BA%E6%9C%AC-%E3%82%B3%E3%83%9F%E3%83%83%E3%83%88%E5%B1%A5%E6%AD%B4%E3%81%AE%E9%96%B2%E8%A6%A7)
- [Gitのコミット日時を上書きする２つの方法 - Qiita](https://qiita.com/yoichi22/items/b25d223b639621b834cb)