# クローンするときにディレクトリの権限がないときにPermission denied（publickey）になる

セッションマネージャでEC2にログインして`git clone`すると、`Permission denied（public key）`がでた。鍵の設定を間違っているのかと思ったが、間違えて`~/.ssh/`でクローンしたときはエラーが出なかったので、ディレクトリの権限の問題みたい。

```text
sh-4.2$ cd /var/www/html/
sh-4.2$ git clone git@github.com:GIBJapan/alien.git
fatal: could not create work tree dir 'alien': Permission denied
sh-4.2$ sudo git clone git@github.com:GIBJapan/alien.git
Cloning into 'alien'...
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
sh-4.2$ cd -
/home/ssm-user/.ssh
sh-4.2$ git@github.com:GIBJapan/alien.git
sh: git@github.com:GIBJapan/alien.git: No such file or directory
sh-4.2$ git clone git@github.com:GIBJapan/alien.git
Cloning into 'alien'...
remote: Enumerating objects: 662, done.
remote: Counting objects: 100% (662/662), done.
remote: Compressing objects: 100% (431/431), done.
remote: Total 662 (delta 311), reused 530 (delta 184), pack-reused 0
Receiving objects: 100% (662/662), 545.68 KiB | 1.14 MiB/s, done.
Resolving deltas: 100% (311/311), done.
```

あれこれは`~/.ssh`でクローンした成功したのか。`~/.ssh/config`を見てみる。いや、sudoつけたときに`~`がルートユーザーのホームディレクトリになっているからか。

```text
# 修正前
Host github.com
  HostName github.com
  IdentityFile ~/.ssh/id_ed25519
  User git

# 修正後
Host github.com
  HostName github.com
  IdentityFile /home/ssm-user/.ssh/id_ed25519
  User git
```

ルートユーザーで実行したときに、このSSHの設定ファイルが読み込まれていないのでエラーが出ていた。