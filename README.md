# Web-Notebook
## Ubuntu + Apache + PHP + MySQL (LAMP)
### Install Apache

透過apt-get指令安裝apache server
```cmd
sudo apt-get update
sudo apt-get install apache2
```
在組態檔中新增伺服器IP或是網域名稱（Domain Name)
```cmd
sudo vim /etc/apache2/apache2.conf
```
在`apache2.conf`裡面新增`Server Name`並輸入IP或網域名稱(Domain Name)
```
SeverName ip or domain name
```
重新啟動Apache伺服器
```cmd
sudo systemctl restart apache2
```
在瀏覽器中輸入`127.0.0.1`或`localhost`瀏覽預設頁面
成功看到預設頁面表示Apache伺服器已經成功架設好了

```cmd
sudo mv /var/www/html /var/www/html.bkp
mkdir ~/public_html
sudo ln -s ~/public_html /var/www/html
```
### Install MySQL

透過apt-get指令安裝MySQL Server
```cmd
sudo apt-get update
sudo apt-get instll mysql-server
```
MySQL安全設定
透過下面指令設定root密碼，移除用不到的資料庫和資料表
```cmd
sudo mysql_secure_installation
```
安裝完成可以透過下面指令登入MySQL
```cmd
mysql -u root -p
```
### Install PHP

安裝PHP和其他模組
```cmd
sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql
```
## Install phpMyAdmin

使用apt-get安裝phpMyAdmin
```cmd
sudo apt-get update
sudo apt-get install phpmyadmin php-mbstring php-gettext
```
```cmd
sudo phpenmod mcrypt
sudo phpenmod mbstring
```
重新啟動Apache伺服器
```cmd
sudo systemctl restart apache2
```
在瀏覽器中輸入`https://localhost/phpmyadmin`進入phpMyAdmin管理頁面
## Drupal(CMS)
### Install Drush

透過apt-get安裝Drush
```cmd
sudo apt-get update
sudo apt-get install drush
```
### Install Drupal

進入`/var/www/html`使用Drush下載Drupal
```cmd
drush dl drupal
```
將檔案名稱改為drupal
```cmd
rm /var/www/html/drupal-7.50 /var/www/html/drupal
```
複製`sites/default/default.settings.php`為`sites/default/settings.php`
```cmd
cp sites/default/default.settings.php sites/default/settings.php
```
修改權限
```cmd
sudo chown --recursive username:www-data ~/public_html
sudo chmod --recursive g+w ~/public_html
```
為Drupal在MySQL建立一個資料庫
```cmd
mysql -u root -p
```
MySQL指令
```mysql
create database drupal;
flush privileges;
exit
```
開啟網頁`http://localhost`安裝Drupal
