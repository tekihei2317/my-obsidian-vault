#aws
# AWSのパブリックサブネットとプライベートサブネットの違い

AWSのパブリックサブネットとプライベートサブネットの違いは、サブネットのルートテーブルに、インターネットゲートウェイへのルーティングがあるかどうかである。

サブネットのルートテーブルとは、サブネットから外に出る通信についてのルールを定めたものである。デフォルトでは、以下のようなルーティングが設定されている。

|送信先|ターゲット|
|-|-|
|10.0.0.24|local|

NOTE: 10.0.0.24ではなく、10.0.0.21かもしれない

`local`とは、サブネット内を意味する。つまり、サブネット内でのみ送信が出来るようになっている。

ルートテーブルにインターネットゲートウェイが設定されている場合は、以下のようになる。

|送信先|ターゲット|
|-|-|
|10.0.0.24|local|
|0.0.0.0|Internet Gateway|

この設定によって、サブネットからインターネットへの送信ができるようになっている。

外から内（インターネット→サブネット）への通信は、セキュリティグループで制御するのだと思う。