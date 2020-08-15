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
