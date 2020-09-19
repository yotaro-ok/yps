## yps1 task#6

#### 前回はこちらです
[#yps1 task#5](https://github.com/yotaro-ok/yps/blob/master/task_5.md)
<br>
<br>

***

#### お手軽簡単WEBアプリケーション

Laravelでメール認証月のToDoアプリを作ります

初学者がある程度、学習してくると次に何をやればいいのか？と悩むことがあるそうです
<br>
そーゆーときはブログ記事などを参考にしてみましょう
<br>
でも、それだけだとコピペで済んでしまうので複数記事をドッキングしたりリミックスして
<br>
カスタマイズすると面白いですyo!

***

#### 課題の題材

２つのブログ記事を利用します

[Laravel 6.x laravel/uiを利用してbootstrap 4を適用する](https://blog.hrendoh.com/laravel-6-setup-bootstrap4-with-laravel-ui/)
<br>
[【Laravel】ユーザ登録時にメール認証する(v5.7以上)](https://qiita.com/nekyo/items/03e50b4d0dd6f09287d6)

#### プロジェクトの作成

```
// まず新規プロジェクトを作ります

cd /var/www/html
composer create-project --prefer-dist laravel/laravel myapp2 "7.25.0" // 👈ここ注意してね
```
```
// 途中で何か聞かれたら全部　Yes　でOKです
cd myapp2
composer require laravel/ui
npm install
php artisan ui bootstrap --auth
npm install cross-env
npm run dev
```
```
// npm run dev　でエラーが出たらこれ👇やってください

rm ./package-lock.json
rm -rf ./node_modules/
npm install
```
```
// Nginxの設定をいじります
sudo vi /etc/nginx/conf.d/default.conf

/var/www/html/yps/public;

// 👇ypsをmyapp2に全部置換してください

/var/www/html/myapp2/public;

// で、再起動
sudo systemctl restart nginx && sudo systemctl restart php-fpm
```
```
// 前回入れた phpmyadmin も使えるようにしておきましょう

cd ../yps/public/
unlink pma
cd -
sudo ln -s /usr/share/pma/ /var/www/html/myapp2/public/pma

// pmaがphpmyadminとかの人はディレクトリ名変えてね
```
```
// キャッシュクリア
php artisan cache:clear &&php artisan config:clear && php artisan route:clear &&php artisan view:clear

composer clear-cache && composer dump-autoload --optimize

// オーナーとディレクトリ権限変更
sudo chown -R centos:nginx /var/www/
sudo chmod -R 777 storage/ bootstrap/cache/
```

右上にlogin、registerがあることを確認してください

![EhE0aGzU8AAOap0](https://user-images.githubusercontent.com/63440984/93662154-d2fd2580-fa98-11ea-9077-95cfe39b0018.jpeg)


#### タスクアプリを作成

```
php artisan make:model Task -m

// で表示されたファイルを開いてブログのとおりコピペしてください

ls -la database/migrations/

// で作成されたファイルが見つかるはずです
```
```
// データベースを作成します

mysql -u root -p

create database myapp2db;

exit
```
```
// .envを編集します
vi .env

DB_DATABASE=myapp2db                                                                                
DB_USERNAME=root
DB_PASSWORD="パスワード"
```
```
// マイグレートします
php artisan migrate

// テーブルが作成されているか確認します
mysql -u root -p -D myapp2db
show tables;

// で👇と同じならOKです

+--------------------+
| Tables_in_myapp2db |
+--------------------+
| failed_jobs        |
| migrations         |
| password_resets    |
| tasks              |
| users              |
+--------------------+
```

#### Gmailでのメール認証


#### まとめ

あとは、余裕ですよね？

ブログに書いてある

ロジックを実装

から　模写　してください

出来た人は、ここにいいねして　#yps1 #tsk6　のハッシュタグ付けてスクショ晒してください 

👇ここ多分、ハマると思うー　がんばえー

ちゃんとログインしてメール認証もしてね
TOP画面は何でもいいですyo!

#### TODO: 資料を纏める

[元ネタツイート](https://twitter.com/yotaro__ok/status/1301869326383812608)
<br>
<br>
#### 参考
