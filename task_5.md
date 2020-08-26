## yps1 task#5

#### 前回はこちらです
[#yps1 task#4](https://github.com/yotaro-ok/yps/blob/master/task_4.md)
<br>
<br>

***

#### 事前準備その１

nodejs、npmをバージョンアップします
```
sudo yum remove node npm -y
curl -sL https://rpm.nodesource.com/setup_12.x | sudo bash -
sudo yum install nodejs -y

// バージョンナンバーが微妙に異なる場合があります
$ node -v
v12.18.3
$ npm -v
6.14.6

cd /var/www/html/yps
rm -rf ./node_modules
npm install && npm run dev // エラーが表示されなければOKです
```

LaravelのuiにBootstrapを指定してください
```
composer require laravel/ui
php artisan ui bootstrap

npm install && npm run dev // エラーが表示されなければOKです
```

***

#### 事前準備その２

以前利用した worldcup2014db を今回も利用します
テーブル構成を変更するのでDDLをmysqldumpで取得します
vscode起動して　メニューの新しいターミナルを選択してください
```
pwd
/var/www/html/yps // ←このディレクトリにいることを確認してください

mkdir resources/sql // ディレクトリを作成してください

mysqldump -u root -p -d worldcup2014db > resources/sql/worldcup2014db.sql // データ構造のみのdumpを取ります
```

以下のテーブルがあるか確認してください
```
grep -i 'create table' resources/sql/worldcup2014db.sql
CREATE TABLE `countries` (
CREATE TABLE `goals` (
CREATE TABLE `goals_tmp` (
CREATE TABLE `pairings` (
CREATE TABLE `pairings_tmp` (
CREATE TABLE `players` (
CREATE TABLE `players_tmp` (
```

以下のテーブルにフィールドを追加します
```
countries
goals
pairings
players
```

エディタを使って以下のフィールドを各テーブルに追加します
```
`expired_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
`deleted_at` timestamp NULL DEFAULT NULL,
`updated_at` timestamp NULL DEFAULT NULL,
`created_at` timestamp NULL DEFAULT NULL,
```

[こんな感じです](https://github.com/yotaro-ok/yps/issues/14#issuecomment-678294088)

mysql cliにログインしてください
```
mysql -u root -p 

drop database worldcup2014db; // DBを削除します
create database worldcup2014db; // DBを再作成します

use worldcup2014db;
source resources/sql/worldcup2014db.sql; // 先程、テーブル構成を変更したdumpのSQLファイルを流し込みます

show tables; // テーブルが作成されているか確認してください

exit;
```

[#yps1 task#4](https://github.com/yotaro-ok/yps/blob/master/task_4.md) と同じことをします
```
cd /tmp
sudo yum install wget unzip -y
wget http://tech.pjin.jp/wp-content/uploads/2016/04/worldcup2014.zip
unzip http://worldcup2014.zip
ls -la worldcup2014.sql
```

以下のテーブルを作成している箇所を全部削除してください
```
grep -i 'create table' /tmp/worldcup2014.sql
CREATE TABLE `countries` (
CREATE TABLE `goals` (
CREATE TABLE `goals_tmp` (
CREATE TABLE `pairings` (
CREATE TABLE `pairings_tmp` (
CREATE TABLE `players` (
CREATE TABLE `players_tmp` (
```

データを流し込みます
```
mysql -u root -p -D worldcup2014db

source /tmp/worldcup2014.sql; // warningはデータバグなので無視してください
```

各テーブルのデータ件数を確認してください
```
mysql> select count(*) from countries;
+----------+
| count(*) |
+----------+
|       32 |
+----------+

mysql> select count(*) from goals;
+----------+
| count(*) |
+----------+
|      188 |
+----------+

mysql> select count(*) from pairings;
+----------+
| count(*) |
+----------+
|      144 |
+----------+

mysql> select count(*) from players;
+----------+
| count(*) |
+----------+
|      736 |
+----------+
```

これでデータが出来上がりました

mysql cli から exit　してください

****

#### 簡単なWEBアプリケーション作成

***

#### mysqldump

***

#### テーブル定義変更

***

#### モデルクラス作成

***

#### コントローラークラス作成

***

#### ビュー（Blade）作成

***

#### Bootstrapの利用

***

#### その２へ

***
<br>
<br>

#### TODO: 資料を纏める

[元ネタツイート](https://twitter.com/yotaro__ok/status/1296798384997535744)
<br>
[元ネタツイート 8/25追加分](https://twitter.com/yotaro__ok/status/1298257156483870721)
<br>
[元ネタツイート 8/26追加分](https://twitter.com/yotaro__ok/status/1298605808813355015)
<br>
#### 参考

[miyupaca](https://twitter.com/miyupacaaa)さんのブログ→[2020-08-21 yps学習記録その5](https://paca-gatsby.netlify.app/2020-08-21/)
