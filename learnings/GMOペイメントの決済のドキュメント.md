# GMOペイメントの決済のドキュメント

リンク: [クレジットカード決済利用マニュアル](file:///Users/gib0017/Downloads/%E3%82%AF%E3%83%AC%E3%82%B7%E3%82%99%E3%83%83%E3%83%88%E3%82%AB%E3%83%BC%E3%83%88%E3%82%99%E6%B1%BA%E6%B8%88_1_21.pdf)

↑クラウドストレージに上げて参照できるようにしたい

リンクタイプと違って、こちらはAPIを叩いて利用する方式のような気がする。クレジットカードの情報とかもパラメータで送るのだろうか？

- オーダーIDは、APIの使用者が取引を識別するために設定する、P7
	- 一度使用した値を再度使用することはできない
- 仮売上と即時売上の2つの方法がある、P10
- 未決済について書かれていますね、P12
	- > 未決済 UNPROCESSED 決済が完了していない状態（お客様がご注文途中に離脱が主な原因）
- カード番号入力型で決済する場合のシーケンス図、P25
	- 取引の登録、決済の実行をアプリ側から行うような気がする→そうですね
	- 取引登録（EntryTran）→取引実行（ExecTran）
		- 取引実行で、クレジットカード番号やカードの有効期限、名義人を送信する
- 取引状態の紹介API（SearchTrade）では、取引を登録する際に指定した値を使用する、P86
