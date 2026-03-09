# Setup SSL cho Apache web server
> [!CAUTION]
> Bạn cần chuẩn bị trước các certificate để thực hiện hướng dẫn này/

## 1. Bật ssl trên apache
Bạn cần bật ssl mod trên apache
````
$ sudo a2enmod ssl
$ sudo systemctl restart apache2
````

## 2. Tạo 1 site mới
Tạo 1 site mới tại `sudo nano /etc/apache2/sites-avaliable/`
````
<VirtualHost *:443>
  ServerName <tên server>
  DocumentRoot /var/www/html
  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
  SSLEngine on
  SSLCertificateFile <certificate>
  SSLCertificateKeyFile <certificate key>
</VirtualHost>
````
Bật site
````
$ sudo a2ensite <tên site>
````

## 3. Redirect HTTP -> HTTPS
Tại page mặc định thay đổi như sau
````
<VirtualHost *:80>
    ServerName www.example.com
    Redirect permanent / https://www.example.com/
</VirtualHost>
````
