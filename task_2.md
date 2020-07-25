## 暇な人は↓これでもやっといてください

[シェルスクリプトプログラミング](https://manual.atmark-techno.com/armadillo-guide/armadillo-guide-2_ja-2.2.0/ch05.html)
<br>
[C言語による実践プログラミング](https://manual.atmark-techno.com/armadillo-guide/armadillo-guide-2_ja-2.2.0/ch06.html)
<br>

## MySQL5.7のインストール、設定

```
sudo yum localinstall http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm
sudo yum install -y mysql-community-server -y
```
```
mysqld --version
sudo systemctl enable mysqld
sudo systemctl start mysqld
sudo systemctl status mysqld
sudo systemctl stop mysqld
```
```
sudo cat /var/log/mysqld.log | grep -i root
root@localhost: パスワード
sudo systemctl start mysqld
mysql -u root -p
パスワードを入力
MySQLのプロンプトが表示されたらOK
exit　で抜ける
```

***

## Nginx1.8のインストール、設定

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
