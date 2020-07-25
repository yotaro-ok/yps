## 暇な人は↓これでもやっといてください

[シェルスクリプトプログラミング](https://manual.atmark-techno.com/armadillo-guide/armadillo-guide-2_ja-2.2.0/ch05.html)
<br>
[C言語による実践プログラミング](https://manual.atmark-techno.com/armadillo-guide/armadillo-guide-2_ja-2.2.0/ch06.html)
<br>

## MySQL5.7のインストール、設定

インストール
```
sudo yum localinstall http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm
sudo yum install -y mysql-community-server -y
```

自動起動、動作確認
```
mysqld --version
sudo systemctl enable mysqld
sudo systemctl start mysqld
sudo systemctl status mysqld
sudo systemctl stop mysqld
```

MySQLログイン
```
sudo cat /var/log/mysqld.log | grep -i root
root@localhost: パスワード
sudo systemctl start mysqld
mysql -u root -p
パスワードを入力
MySQLのプロンプトが表示されたらOK

パスワード変更　※8文字以上で英大文字・小文字・数字・記号を混ぜる
SET PASSWORD = PASSWORD('パスワード');

変更できたら
exit　で抜ける
```

文字コード設定
```
sudo vi /etc/my.cnf

最終行に以下を追記
character-set-server=utf8mb4

[client]
default-character-set=utf8mb4
```

```
sudo systemctl restart mysqld
mysql -u root -p

mysql> show variables like "chara%";
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8mb4                    |
| character_set_connection | utf8mb4                    |
| character_set_database   | utf8mb4                    |
| character_set_filesystem | binary                     |
| character_set_results    | utf8mb4                    |
| character_set_server     | utf8mb4                    |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set (0.00 sec)
```

##### MySQLのインストール、設定は完了です

***

## Nginx1.8のインストール、設定

インストール
```
sudo vi /etc/yum.repos.d/nginx.repo

以下を入力
[nginx]
name=nginx repo
baseurl=https://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1

sudo yum install nginx -y
nginx -v

sudo systemctl enable nginx
```

***

## PHP7.3のインストール、設定

***

## Laravel7のインストール、設定

***

## Laravel7のWelcome画面表示

***

#### TODO: 資料を纏める
[元ネタツイート](https://twitter.com/yotaro__ok/status/1286271610815516672)　　

#### 参考
[miyupaca](https://twitter.com/miyupacaaa)さんのブログ[2020-07-23 yps学習記録その2](https://paca-gatsby.netlify.app/2020-07-23/)
