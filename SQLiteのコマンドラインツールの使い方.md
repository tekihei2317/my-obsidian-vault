# SQLiteのコマンドラインツールの使い方

`sqlite3`コマンドを使用する。Macではデフォルトでインストールされている。

```bash
# データベースに入る
$ sqlite3 database/database.sqlite

# テーブル一覧
sqlite> .tables
failed_jobs             password_resets         users
migrations              personal_access_tokens

# SQLの実行
sqlite> select * from migrations;
1|2014_10_12_000000_create_users_table|1
2|2014_10_12_100000_create_password_resets_table|1
3|2019_08_19_000000_create_failed_jobs_table|1
4|2019_12_14_000001_create_personal_access_tokens_table|1

# ヘッダ行を表示させる
sqlite> .headers on

# 再度SELECT文の実行
sqlite> select * from migrations;
id|migration|batch
1|2014_10_12_000000_create_users_table|1
2|2014_10_12_100000_create_password_resets_table|1
3|2019_08_19_000000_create_failed_jobs_table|1
4|2019_12_14_000001_create_personal_access_tokens_table|1

```

## 参考

- [SQLite | SELECT文の結果を表示する時にカラム名をヘッダーとして表示(.headersコマンド)](https://www.dbonline.jp/sqlite/sqlite_command/index5.html)
- [Macで使うSQLite3入門編 - TASK NOTES](https://www.task-notes.com/entry/20140720/1405845794)