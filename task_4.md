## yps1 task#4

#### 前回はこちらです
[#yps1 task#3](https://github.com/yotaro-ok/yps/blob/master/task_3.md)
<br>
<br>

***

## WordPress5.4.2セットアップ

```
cd /tmp
wget https://ja.wordpress.org/latest-ja.zip
unzip ./latest-ja.zip
```
```
mv wordpress wwpp
mv wwpp /var/www/html/
```
```
mysql -u root -p

// ログインします

create database wwppdb;
grant all on wwppdb.* to wwppuser@localhost identified by '任意のパスワード';
exit;
```
```
cd /var/www/html/wwpp/
cp -p wp-config-sample.php wp-config.php
vi wp-config.php
```
[wp-config.php編集差分](https://github.com/yotaro-ok/yps/issues/12#issuecomment-671045833)
```
cd /var/www/html
sudo chown -R centos:nginx /var/www/html/wwpp/
sudo find /var/www/html/wwpp/ -type f -exec chmod 664 {} \;
sudo find /var/www/html/wwpp/ -type d -exec chmod 775 {} \;
```
```
sudo vi /etc/nginx/conf.d/default.conf

root /var/www/html/yps/public;
// ↓に変更
root   /var/www/html/wwpp;

sudo systemctl restart php-fpm
sudo systemctl restart ngin
```

#### ブラウザからアクセスしてください

![Ee-t22hU4AE1myl](https://user-images.githubusercontent.com/63440984/90323187-b6049c80-df98-11ea-8cce-9329315aef02.png)
<br>
![Ee-uZibU8AUd1iG](https://user-images.githubusercontent.com/63440984/90323207-f82dde00-df98-11ea-997a-87a02143dde7.png)

#### 全項目入力したら WordPressをインスール　ボタンを選択してください
↓これが出てばOKです
<br>
![Ee-t22hU4AE1myl](https://user-images.githubusercontent.com/63440984/90323224-417e2d80-df99-11ea-869e-3def17a5f279.png)

#### ログインしてダッシュボード画面が表示されていることを確認してください

sshポートから出来るようにするプラグインを入れます
<br>
![Ee-vlN7U0AAWcKN](https://user-images.githubusercontent.com/63440984/90323231-683c6400-df99-11ea-8ee7-7b4c98a1e307.png)
<br>

```
cd wp-content/plugins/
wget https://downloads.wordpress.org/plugin/ssh-sftp-updater-support.0.8.2.zip
unzip ./ssh-sftp-updater-support.0.8.2.zip 
rm http://ssh-sftp-updater-support.0.8.2.zip 
sudo chown -R centos:nginx ./ssh-sftp-updater-support/
```
![Ee-xFKYU8AMoWJY](https://user-images.githubusercontent.com/63440984/90323261-ee58aa80-df99-11ea-8b88-4854c516d9b5.jpeg)
<br>
XXX.pemファイル選択してください
<br>
![Ee-xFKYU8AMoWJY](https://user-images.githubusercontent.com/63440984/90323266-0b8d7900-df9a-11ea-95f3-f06a00ab9375.jpeg)

```
cd /var/www/html/wwpp/
sudo chmod 644 ./wp-config.php
```

好きなテーマを選択してインストール、有効化してください
<br>
![Ee-09kJU4AEnSQJ](https://user-images.githubusercontent.com/63440984/90323292-61622100-df9a-11ea-843b-6ec54b97f375.png)

適当にレイアウトやコンテンツ作成して晒してみましょう
<br>
![Ee_CotOUYAE1AMs](https://user-images.githubusercontent.com/63440984/90323306-8bb3de80-df9a-11ea-90f8-823680a4f80a.jpeg)
<br>
<br>
```
Laravelへの戻しです

sudo vi /etc/nginx/conf.d/default.conf

root   /var/www/html/wwpp;
// ↓変更
root    /var/www/html/yps/public;

sudo systemctl restart php-fpm
sudo systemctl restart ngin
```

<br>
<br>

#### TODO: 資料を纏める

[元ネタツイート](https://twitter.com/yotaro__ok/status/1292432592973647872)
<br>
[訂正箇所](https://twitter.com/yotaro__ok/status/1292581686006300674)
<br>
[追加課題](https://twitter.com/yotaro__ok/status/1292586026733428736)
<br>
#### 参考

[miyupaca](https://twitter.com/miyupacaaa)さんのブログ→[2020-08-09 yps学習記録その4](https://paca-gatsby.netlify.app/2020-08-09/)
