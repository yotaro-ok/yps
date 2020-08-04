## yps1 task#3

#### 前回はこちらです
[#yps1 task#2](https://github.com/yotaro-ok/yps/blob/master/task_2.md)
<br>
<br>

***

## DB接続確認batch作成

[Laravelでbatchを作ろう！](https://twitter.com/yotaro__ok/status/1286722000291942400)
<br>
<br>
[/etc/my.cnf](https://github.com/yotaro-ok/yps/issues/3#issuecomment-663870888)
<br>
[MySQLクライアントに日本語が入力できない理由](https://developer.suzna.com/entry/2018/04/23/103928)
<br>
MySQL CLIで日本語が入力できない件については、ライブラリ変更による影響なのでどうするか考えます。

```
sudo vi /etc/mysql.cnf

// 最終行に以下を追記
[client]
default-character-set=utf8mb4

// 再起動
sudo systemctl restart mysql
```

***

## SQLテーブル作成（復習）

***

```
cd /tmp
sudo yum install wget -y
wget http://tech.pjin.jp/wp-content/uploads/2016/04/worldcup2014.zip
unzip http://worldcup2014.zip
ls -la worldcup2014.sql
```

```
mysql -u root -p

create database worldcup2014db;
use worldcup2014db;

source ./worldcup2014.sql;

show tables; // テーブル名が表示されればOKです

exit
```

## Laravelでバッチ作成（復習）

***

```
cd /var/www/html/yps

php artisan make:model Models/Player
ls -la app/Models/Player.php // ファイルが存在することを確認してください

php artisan make:command TestCommand
ls -la app/Console/Commands/TestCommand.php // ファイルが存在することを確認してください
```

```
// VS Codeで以下のファイルを開く
app/Console/Commands/TestCommand.php
```

[１回全部消して全コピペ](https://github.com/yotaro-ok/yps/issues/3#issuecomment-663672640)


```
php artisan config:clear
php artisan test_command // 選手の名前が表示されればOKです
```

## php.ini設定

***

```
sudo cp /etc/php.ini /etc/php.ini.org
sudo vi /etc/php.ini
```

以下を読んで修正→[CentOSにPHP7をインストールしたらやっておくべき初期設定](https://affiwork.net/php-settings/)
<br>
修正箇所→[colordiff -u /etc/php.ini.org /etc/php.ini](https://github.com/yotaro-ok/yps/issues/5#issuecomment-667203978)
※エラーファイル出力あり

```
sudo touch /var/log/php_errors.log
sudo chown nginx:nginx /var/log/php_errors.log

// サービス再起動
sudo systemctl restart php-fpm
sudo systemctl restart nginx
```

## Git/GitHub設定

***

```
sudo yum install git -y
cd /var/www/html/yps
git init
```

// GitHubでリポジトリ作成

```
cd /var/www/html/yps/
vi .git/config
```

```
[user]
    name = 名前
    email = メールアドレス
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
[remote "origin"]
    url = git@github.com:yotaro-ok/myapp.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```

```
ssh-keygen -t rsa -b 4096 -C "メールアドレス"
// エンターキー押下
// パスワード入力×２
```

```
~/.ssh/id_rsa.pub // 表示された文字列をGitHubに登録
```

***

## GitHubにLaravelソースファイルをアップロード

```
cd /var/www/html/yps/
git add .
git commit -am "initial"
git push origin master
// yes入力
// パスワード入力
```

```
git checkout develop
git branch // 開発用developブランチになっているか確認
```

[Gitを最大限に活用できる「Git flow」で、効率よく開発を進めよう！](https://liginc.co.jp/248864)

***

#### TODO: 資料を纏める

[元ネタツイート](https://twitter.com/yotaro__ok/status/1289185995875745794)
<br>
#### 参考

[よーすけ](https://twitter.com/yosuke_89)さんのブログ→[yps1 task3まとめ](https://yousuke.hatenadiary.com/entry/2020/08/01/000820)
<br>
[miyupaca](https://twitter.com/miyupacaaa)さんのブログ→[2020-07-30 yps学習記録その3](https://paca-gatsby.netlify.app/2020-07-30/)

[Githubの公開鍵を登録する手順](https://qiita.com/tnatsume00/items/e147662368d02e6416d2)
