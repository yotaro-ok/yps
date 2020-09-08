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

#### mysqldumpコマンドでDDL取得

以前利用した worldcup2014db を今回も利用します
テーブル構成を変更するので [DDL](http://e-words.jp/w/DDL.html) をmysqldumpで取得します
vscode起動して　メニューの新しいターミナルを選択してください
```
pwd
/var/www/html/yps // ←このディレクトリにいることを確認してください

mkdir resources/sql // ディレクトリを作成してください

mysqldump -u root -p -d worldcup2014db > resources/sql/worldcup2014db.sql // DDLを取得します　※テーブル定義部分のみでデータは取得しません
```

#### テーブル構成変更

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

## 簡単なWEBアプリケーション作成

#### モデルクラス作成

前に作ったmodelクラスを削除してください
```
cd /var/www/html/yps
rm app/Models/Player.php 
```

modelクラスを作成してください
```
php artisan make:model Models/Country -m
php artisan make:model Models/Goal -m
php artisan make:model Models/Pairing -m
php artisan make:model Models/Player -m
```

テーブル名が複数形でmodelクラス名は単数形にしておけば、自動的にLaravelが紐づけてくれますが
念の為、明示的にテーブル名を指定します
尚、datesも指定します
```
protected $table = "players";
protected $dates = ["expired_at", "deleted_at", "updated_at", "created_at"];
```

Playserクラス以外も同様に$table、$datesを指定してください

***

#### コントローラークラス作成

Controllerクラスを作成してください
```
php artisan make:controller CountryController --resource --model=Models/Country
php artisan make:controller GoalController --resource --model=Models/Goal
php artisan make:controller PairingController --resource --model=Models/Pairing
php artisan make:controller PlayerController --resource --model= Models/Player

php artisan make:controller WelcomeController --resource
```

***

#### ビュー（Blade）作成

ビューを作成してください

resources/views/welcome.blade.php に [これ](https://github.com/yotaro-ok/myapp/blob/develop/resources/views/welcome.blade.php) をコピペしてください

***

#### ルーター作成（変更）

routes/web.php に [これ](https://github.com/yotaro-ok/myapp/blob/develop/routes/web.php) をコピペしてください

最後に以下を実行してください
```
php artisan cache:clear && php artisan config:clear && php artisan route:clear && php artisan view:clear
composer clear-cache && composer dump-autoload --optimize
sudo chown -R centos:nginx /var/www/html/yps
```

ブラウザに [これ](https://twitter.com/yotaro__ok/status/1296939915704332289/photo/1) と同じように表示させてください
※ページネーションは、適当でいいです

ヒントは、  
　1. テーブルビューを１つ追加  
　2. functionを１つ追加  
　3. controllerからviewに変数渡し  
です  

***

#### 答え

1.選手毎の総得点数を分かりやすくするためにテーブルビュー（total_goals）を作成してください
```
CREATE VIEW 
    total_goals AS 
SELECT
    p.id AS id,
    COUNT(g.goal_time) AS goals
FROM
    (players p LEFT JOIN goals g ON((p.id = g.player_id)))
WHERE
    (g.goal_time IS NOT NULL)
GROUP BY
    p.id 
ORDER BY
    goals DESC,
    p.id;
```

2.Playerモデルに関数を作成してください
[getWithCountryBySimplePaginate](https://github.com/yotaro-ok/myapp/blob/6fd6f1ade70d6d42c2829f3a093df9ffb2771278/app/Models/Player.php#L18)です
※この部分をすべてテーブルビューにしても問題ありません

👉[しらたきver](https://github.com/Shirataki7/yps/tree/develop)

WelcomeControllerの[index](https://github.com/yotaro-ok/myapp/blob/6fd6f1ade70d6d42c2829f3a093df9ffb2771278/app/Http/Controllers/WelcomeController.php#L20)ファンクションからgetWithCountryBySimplePaginateファンクションを呼び出してwelcomeブレードに変数を渡します

3.welcomブレードで受け取った変数をループさせて表示させてください
[こんな感じ](https://github.com/yotaro-ok/myapp/blob/6fd6f1ade70d6d42c2829f3a093df9ffb2771278/resources/views/welcome.blade.php#L84)です

[ページネーション](https://github.com/yotaro-ok/myapp/blob/6fd6f1ade70d6d42c2829f3a093df9ffb2771278/resources/views/welcome.blade.php#L120)を付けて完了です

***

<br>
<br>

#### TODO: 資料を纏める

[元ネタツイート](https://twitter.com/yotaro__ok/status/1296798384997535744)
<br>
[元ネタツイート 8/25追加分](https://twitter.com/yotaro__ok/status/1298257156483870721)
#### こっちに書きますね
```
まず、自分をplayersテーブルに追加します
insert into players (country_id, uniform_num, position, name, club, birth, height, weight) values(12, 11, 'MF', 'yotaro', '横浜M', '1990-02-01', 177, 70);

// goalsテーブルにデータを作ります
// これは、やり方いくつかありますが、ロドリゲス（ID=201）のデータを利用しましょう
// ID=201のデータをSELECTしてきてIDのところだけ先程、playersテーブルにINSERTした自分のIDに変えてINSERTします
insert into goals (pairing_id, player_id, goal_time) select pairing_id, 737, goal_time from goals where player_id=201;

// このままだとロドリゲスと得点数が同じになるのでもう１レコード追加します
insert into goals (pairing_id, player_id, goal_time) select pairing_id, 737, goal_time from goals where player_id=201 and pairing_id=5;

// これで完了です
```
<br>

[元ネタツイート 8/26追加分](https://twitter.com/yotaro__ok/status/1298605808813355015)

```
// 酒井選手を検索してそれぞれのIDを確認してください
select * from players where name like '酒井%';

// あとはフルネームでUPDATEするだけです
update players set name='酒井高徳' where id=724;
update players set name='酒井宏樹' where id=723;

// これで完了です
```
<br>

[元ネタツイート 8/27追加分](https://twitter.com/yotaro__ok/status/1298973532647378944)  

はまおさんがハマったやーつｗ
Laravelの[SoftDeletes](https://github.com/yotaro-ok/myapp/blob/6fd6f1ade70d6d42c2829f3a093df9ffb2771278/app/Models/Player.php#L6)を使います
忘れずに[use](https://github.com/yotaro-ok/myapp/blob/6fd6f1ade70d6d42c2829f3a093df9ffb2771278/app/Models/Player.php#L12)してください

```
// playersテーブルの自分以外のdeleted_atに日付を入れるだけです
update players set deleted_at=now() where id != 737;

// 戻すときはnullを入れましょう
update players set deleted_at=null where id != 737;

// これで完了です
```
<br>

[元ネタツイート 8/28追加分](https://twitter.com/yotaro__ok/status/1299007829521477635)

秒で出来ます（僕は時間を止められる👻）

```
// インストールします
sudo yum install --enablerepo=remi,remi-php73 phpMyAdmin

// セキュアにしたいのでディレクトリ名を変更します
// nginx.confでip制限入れると良いです　※vpn使ってたりしてipアドレスがコロコロ変わる場合は、ip制限できないのでphpmyadminは使わないでください
sudo mv /usr/share/phpMyAdmin /usr/share/pma

// シンボリックリンクを張ります
sudo ln -s /usr/share/pma/ /var/www/html/yps/public/pma

// sessionディレクトリのオーナーを変更します
sudo chown nginx:nginx /var/lib/php/session

// 再起動します
sudo systemctl restart php-fpm
sudo systemctl restart nginx

// これで完了です
```

<br>

#### 参考

[miyupaca](https://twitter.com/miyupacaaa)さんのブログ→[2020-08-21 yps学習記録その5](https://paca-gatsby.netlify.app/2020-08-21/)
