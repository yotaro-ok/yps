## yps2 task#2

#### 前回の続きです
[#yps1 task#1](https://github.com/yotaro-ok/yps/blob/master/task_1.md)
<br>
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

AWS側で　http、https　のポートを開けてください
![スクリーンショット 2020-07-25 09-55-19](https://user-images.githubusercontent.com/63440984/88445366-18b4bd80-ce5d-11ea-8c88-e50b86f57c89.png)

```
sudo systemctl start nginx
```

#### ブラウザに　パブリック DNS (IPv4)　を入力してNginxのWelcome画面が表示されればインストール完了です

Nginxのrootディレクトリを/var/www/htmlに変更してください
```
sudo mkdir /var/www
sudo mkdir /var/www/html
sudo chown -R centos:nginx /var/www

sudo cp /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.org
sudo vi /etc/nginx/conf.d/default.conf

rootのパスを変更してください
#root   /usr/share/nginx/html;
root   /var/www/html;

Nginx構文チェック
nginx -t

Nginxを再起動してください
sudo systemctl restart nginx
```

#### ブラウザでページを更新して 403 エラーになっていればOKです

***

## PHP7.3のインストール、設定

インストール
```
sudo yum install epel-release -y
sudo yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm -y
sudo yum update -y
sudo yum -y install --enablerepo=epel,remi,remi-php73 php php-devel php-mbstring php-pdo php-gd php-xml php-mcrypt php-fpm php-mysql php-mysqlnd zip unzip
php -v
```

php-fpmの設定
```
sudo cp /etc/php-fpm.d/www.conf /etc/php-fpm.d/www.conf.org
sudo vi /etc/php-fpm.d/www.conf

以下に変更
user = nginx
group = nginx
listen = /var/run/php-fpm/php-fpm.sock
listen.owner = nginx
http://listen.group = nginx
listen.mode = 0660
```
Nginxの設定
```
sudo vi /etc/nginx/conf.d/default.conf

以下を変更してください
index  index.php index.html index.htm;
以下を追記してください
try_files $uri $uri/ /index.php?$query_string;

以下を追記してください
location ~ \.php$ {
    fastcgi_pass   unix:/var/run/php-fpm/php-fpm.sock;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    include        fastcgi_params;
}
```

/var/www 以下のパーミッションを変更して
php-fpmを自動起動
Nginx再起動、php-fpm起動
```
sudo chown -R centos:nginx /var/www/
sudo systemctl enable php-fpm
sudo systemctl restart nginx
sudo systemctl start php-fpm
```

php情報を表示
```
ファイルを作成してください
vi /var/www/html/index.php

以下を入力してください
<?php
echo phpinfo();
?>

再起動
sudo systemctl restart nginx
sudo systemctl restart php-fpm
```

#### ブラウザのページを更新してPHP情報が表示されれば完了です

***

## Laravel7のインストール、設定

```
cd /tmp
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer  
sudo chmod +x /usr/local/bin/composer

cd /var/www/html
composer create-project --prefer-dist laravel/laravel yps
php artisan key:generate

cd yps
cp -p .env.example .env

以下を変更してください
APP_URL=ブラウザのURL
DB_PASSWORD="パスワード"


sudo yum install npm node -y

composer install
npm install

sudo chown -R centos:nginx /var/www/
sudo chmod -R 777 storage/ bootstrap/cache/
```

#### とりあえず完了です

***

## Laravel7のWelcome画面表示

```
vi /etc/nginx/conf.d/default.conf

以下の箇所を
/var/www/html;
以下に変更してください
/var/www/html/yps/public;

再起動してください
sudo systemctl restart nginx
sudo systemctl restart php-fpm
```

![スクリーンショット 2020-07-25 10-41-08](https://user-images.githubusercontent.com/63440984/88446279-97acf480-ce63-11ea-8bcb-e3355f9b0a1e.png)

#### ブラウザでページを更新してLaravelのWelcome画面が表示されたら完了です

***

#### TODO: 資料を纏める
[元ネタツイート](https://twitter.com/yotaro__ok/status/1286271610815516672)　　

#### 参考
[miyupaca](https://twitter.com/miyupacaaa)さんのブログ[2020-07-23 yps学習記録その2](https://paca-gatsby.netlify.app/2020-07-23/)
