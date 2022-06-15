# CORSとは何か

CORSとは、異なるオリジン間でのデータの取得を制限するブラウザのルールのことです。

あくまで取得に関するルールなので、リクエスト自体は成功します。つまり、CSRFに対する対策とはなりません。

またブラウザでのルールなので、モバイルアプリやCLIなどのアプリには関係がありません。

TODO: 以下の項目について必要になったときに調べて書く

- 関連するリクエストヘッダについて
	- `Access-Control-Allow-Origin`
	- `Access-Control-Allow-Credentials`
- Preflight Requestについて
