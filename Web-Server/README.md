# Install LEMP Stack
> L = Linux

> E = Nginx

> M = MySQL

> P = PHP

## Prepare Linux (Centos 7)
```shell
yum install -y open-vm-tools git wget unzip zip epel-release
yum update -y
systemctl stop firewalld
systemctl disable firewalld
vi /etc/sysconfig/selinux
```
> Edit line 7: SELINUX=disabled
```shell
reboot
```

## Install Nginx
```shell
yum install nginx -y
systemctl start nginx
systemctl enable nginx
```

## Secure Nginx with Let's Encrypt
```shell
yum install certbot -y
openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
sudo mkdir -p /var/lib/letsencrypt/.well-known
sudo chgrp nginx /var/lib/letsencrypt
sudo chmod g+s /var/lib/letsencrypt
sudo mkdir /etc/nginx/snippets
```
> Edit file `/etc/nginx/snippets/letsencrypt.conf`
```shell
vi /etc/nginx/snippets/letsencrypt.conf
```
> Add the content bellow:
```shell
location ^~ /.well-known/acme-challenge/ {
    allow all;
    root /var/lib/letsencrypt/;
    default_type "text/plain";
    try_files $uri =404;
}
```
> Edit file `/etc/nginx/snippets/ssl.conf`
```shell        
vi /etc/nginx/snippets/ssl.conf
```
> Add the content bellow:
```shell
ssl_dhparam /etc/ssl/certs/dhparam.pem;

ssl_session_timeout 1d;
ssl_session_cache shared:SSL:50m;
ssl_session_tickets off;

ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
ssl_ciphers 'ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS';
ssl_prefer_server_ciphers on;

ssl_stapling on;
ssl_stapling_verify on;
resolver 8.8.8.8 8.8.4.4 valid=300s;
resolver_timeout 30s;

add_header Strict-Transport-Security "max-age=15768000; includeSubdomains; preload";
add_header X-Frame-Options SAMEORIGIN;
add_header X-Content-Type-Options nosniff;
```

```shell
vi /etc/nginx/conf.d/kbuor.website.conf 
```
> (replace kbuor.website by your domain)

> Add the content bellow: (replace kbuor.website by your domain)
```shell
server {
    listen 80;
    server_name kbuor.website www.kbuor.website;

    include snippets/letsencrypt.conf;
}
 ```

 ```shell
 sudo systemctl reload nginx
 sudo certbot certonly --agree-tos --email admin@kbuor.website --webroot -w /var/lib/letsencrypt/ -d kbuor.website -d www.kbuor.website
 ```

 > (replace kbuor.website by your domain)
 
 ```shell
 vi /etc/nginx/conf.d/kbuor.website.conf
 
```

> Add the content bellow: (replace kbuor.website by your domain)

```shell
server {
    listen 80;
    server_name www.kbuor.website kbuor.website;

    include snippets/letsencrypt.conf;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    server_name www.kbuor.website;

    ssl_certificate /etc/letsencrypt/live/kbuor.website/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/kbuor.website/privkey.pem;
    ssl_trusted_certificate /etc/letsencrypt/live/kbuor.website/chain.pem;
    include snippets/ssl.conf;
    include snippets/letsencrypt.conf;

    return 301 https://kbuor.website$request_uri;
}

server {
    listen 443 ssl http2;
    server_name kbuor.website;

    ssl_certificate /etc/letsencrypt/live/kbuor.website/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/kbuor.website/privkey.pem;
    ssl_trusted_certificate /etc/letsencrypt/live/kbuor.website/chain.pem;
    include snippets/ssl.conf;
    include snippets/letsencrypt.conf;
}
 ```

 ```shell
 sudo systemctl reload nginx
 crontab -e
 
        0 */12 * * * root test -x /usr/bin/certbot -a \! -d /run/systemd/system && perl -e 'sleep int(rand(3600))' && certbot -q renew --renew-hook "systemctl reload nginx"
 ```

 ## Install MySQL 8.0 on CentOS 7
 ```shell
 yum localinstall https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm -y
 rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
 yum install mysql-community-server -y
 systemctl enable mysqld
 systemctl start mysqld
 
 sudo grep 'temporary password' /var/log/mysqld.log
 mysql_secure_installation
 .
 .
 .
 
 mysql -u root -p
 > CREATE DATABASE wordpress CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
 > CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'P@ssw0rd';
 > GRANT ALL ON wordpress.* TO 'wpuser'@'localhost';
 > FLUSH PRIVILEGES;
 > EXIT;
 ```

 ## Install PHP 7.4
 ```shell
 yum install epel-release yum-utils
 yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
 yum-config-manager --enable remi-php74
 yum install php-cli php-fpm php-mysql php-json php-opcache php-mbstring php-xml php-gd php-curl
 ```

 ```shell
 vi /etc/php-fpm.d/www.conf
 ```
 
 > Edit line 24: user = nginx
 
 > Edit line 26: group = nginx
 
 > Edit line 38: listen = /run/php-fpm/www.sock
 
 > Edit line 48: listen.owner = nginx
 
 > Edit line 49: listen.group = nginx
 
 ```shell
 chown -R root:nginx /var/lib/php
 systemctl enable php-fpm
 systemctl start php-fpm
 ```

 ## Download Wordpress
 
 ```shell
 sudo mkdir -p /var/www/html/kbuor.website (replace kbuor.website by your domain)
 cd /tmp
 wget https://wordpress.org/latest.tar.gz
 tar xf latest.tar.gz
 mv /tmp/wordpress/* /var/www/html/kbuor.website/ (replace kbuor.website by your domain)
 chown -R nginx: /var/www/html/kbuor.website (replace kbuor.website by your domain)
 ```
 
 ```shell
 vi /etc/nginx/conf.d/kbuor.website.conf
 ```

 ```shell
# Add the content bellow: (replace kbuor.website by your domain)
# Redirect HTTP -> HTTPS
server {
    listen 80;
    server_name www.kbuor.website kbuor.website;

    include snippets/letsencrypt.conf;
    return 301 https://kbuor.website$request_uri;
}

# Redirect WWW -> NON WWW
server {
    listen 443 ssl http2;
    server_name www.kbuor.website;

    ssl_certificate /etc/letsencrypt/live/kbuor.website/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/kbuor.website/privkey.pem;
    ssl_trusted_certificate /etc/letsencrypt/live/kbuor.website/chain.pem;
    include snippets/ssl.conf;

    return 301 https://kbuor.website$request_uri;
}

server {
    listen 443 ssl http2;
    server_name kbuor.website;

    root /var/www/html/kbuor.website;
    index index.php;

    # SSL parameters
    ssl_certificate /etc/letsencrypt/live/kbuor.website/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/kbuor.website/privkey.pem;
    ssl_trusted_certificate /etc/letsencrypt/live/kbuor.website/chain.pem;
    include snippets/ssl.conf;
    include snippets/letsencrypt.conf;

    # log files
    access_log /var/log/nginx/kbuor.website.access.log;
    error_log /var/log/nginx/kbuor.website.error.log;

    location = /favicon.ico {
        log_not_found off;
        access_log off;
    }

    location = /robots.txt {
        allow all;
        log_not_found off;
        access_log off;
    }

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_pass unix:/run/php-fpm/www.sock;
        fastcgi_index   index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
        expires max;
        log_not_found off;
    }

}
 ```

 ```shell
 nginx -t
 systemctl restart nginx
```