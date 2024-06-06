## THÔNG TIN CHUNG
---
Operating System: `Ubuntu 22.04.4 LTS (Jammy)`

IP Address: `20.20.20.103/24`

Gateway: `20.20.20.20`

Hostname: `nginx.kbuor.io.local`

Domain: `kbuor.io.local`

## CHUẨN BỊ
---
> Update repository
```shell
sudo apt update -y && apt upgrade -y
```

## TRIỂN KHAI
---
> 1. Cài đặt gói `nginx` từ repository của Ubuntu
```shell
sudo apt install nginx
```
```shell
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  fontconfig-config fonts-dejavu-core libdeflate0 libfontconfig1 libgd3 libjbig0 libjpeg-turbo8 libjpeg8 libnginx-mod-http-geoip2 libnginx-mod-http-image-filter libnginx-mod-http-xslt-filter
  libnginx-mod-mail libnginx-mod-stream libnginx-mod-stream-geoip2 libtiff5 libwebp7 libxpm4 nginx-common nginx-core
Suggested packages:
  libgd-tools fcgiwrap nginx-doc ssl-cert
The following NEW packages will be installed:
  fontconfig-config fonts-dejavu-core libdeflate0 libfontconfig1 libgd3 libjbig0 libjpeg-turbo8 libjpeg8 libnginx-mod-http-geoip2 libnginx-mod-http-image-filter libnginx-mod-http-xslt-filter
  libnginx-mod-mail libnginx-mod-stream libnginx-mod-stream-geoip2 libtiff5 libwebp7 libxpm4 nginx nginx-common nginx-core
0 upgraded, 20 newly installed, 0 to remove and 3 not upgraded.
Need to get 2,693 kB of archives.
After this operation, 8,350 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 fonts-dejavu-core all 2.37-2build1 [1,041 kB]
Get:2 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 fontconfig-config all 2.13.1-4.2ubuntu5 [29.1 kB]
Get:3 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 libdeflate0 amd64 1.10-2 [70.9 kB]
Get:4 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 libfontconfig1 amd64 2.13.1-4.2ubuntu5 [131 kB]
Get:5 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 libjpeg-turbo8 amd64 2.1.2-0ubuntu1 [134 kB]
Get:6 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 libjpeg8 amd64 8c-2ubuntu10 [2,264 B]
Get:7 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libjbig0 amd64 2.1-3.1ubuntu0.22.04.1 [29.2 kB]
Get:8 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libwebp7 amd64 1.2.2-2ubuntu0.22.04.2 [206 kB]
Get:9 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libtiff5 amd64 4.3.0-6ubuntu0.8 [185 kB]
Get:10 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libxpm4 amd64 1:3.5.12-1ubuntu0.22.04.2 [36.7 kB]
Get:11 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 libgd3 amd64 2.3.0-2ubuntu2 [129 kB]
Get:12 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 nginx-common all 1.18.0-6ubuntu14.4 [40.0 kB]
Get:13 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libnginx-mod-http-geoip2 amd64 1.18.0-6ubuntu14.4 [11.9 kB]
Get:14 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libnginx-mod-http-image-filter amd64 1.18.0-6ubuntu14.4 [15.4 kB]
Get:15 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libnginx-mod-http-xslt-filter amd64 1.18.0-6ubuntu14.4 [13.7 kB]
Get:16 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libnginx-mod-mail amd64 1.18.0-6ubuntu14.4 [45.7 kB]
Get:17 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libnginx-mod-stream amd64 1.18.0-6ubuntu14.4 [72.9 kB]
Get:18 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libnginx-mod-stream-geoip2 amd64 1.18.0-6ubuntu14.4 [10.1 kB]
Get:19 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 nginx-core amd64 1.18.0-6ubuntu14.4 [484 kB]
Get:20 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 nginx amd64 1.18.0-6ubuntu14.4 [3,872 B]
Fetched 2,693 kB in 1s (3,106 kB/s)
Preconfiguring packages ...
Selecting previously unselected package fonts-dejavu-core.
(Reading database ... 74566 files and directories currently installed.)
Preparing to unpack .../00-fonts-dejavu-core_2.37-2build1_all.deb ...
Unpacking fonts-dejavu-core (2.37-2build1) ...
Selecting previously unselected package fontconfig-config.
Preparing to unpack .../01-fontconfig-config_2.13.1-4.2ubuntu5_all.deb ...
Unpacking fontconfig-config (2.13.1-4.2ubuntu5) ...
Selecting previously unselected package libdeflate0:amd64.
Preparing to unpack .../02-libdeflate0_1.10-2_amd64.deb ...
Unpacking libdeflate0:amd64 (1.10-2) ...
Selecting previously unselected package libfontconfig1:amd64.
Preparing to unpack .../03-libfontconfig1_2.13.1-4.2ubuntu5_amd64.deb ...
Unpacking libfontconfig1:amd64 (2.13.1-4.2ubuntu5) ...
Selecting previously unselected package libjpeg-turbo8:amd64.
Preparing to unpack .../04-libjpeg-turbo8_2.1.2-0ubuntu1_amd64.deb ...
Unpacking libjpeg-turbo8:amd64 (2.1.2-0ubuntu1) ...
Selecting previously unselected package libjpeg8:amd64.
Preparing to unpack .../05-libjpeg8_8c-2ubuntu10_amd64.deb ...
Unpacking libjpeg8:amd64 (8c-2ubuntu10) ...
Selecting previously unselected package libjbig0:amd64.
Preparing to unpack .../06-libjbig0_2.1-3.1ubuntu0.22.04.1_amd64.deb ...
Unpacking libjbig0:amd64 (2.1-3.1ubuntu0.22.04.1) ...
Selecting previously unselected package libwebp7:amd64.
Preparing to unpack .../07-libwebp7_1.2.2-2ubuntu0.22.04.2_amd64.deb ...
Unpacking libwebp7:amd64 (1.2.2-2ubuntu0.22.04.2) ...
Selecting previously unselected package libtiff5:amd64.
Preparing to unpack .../08-libtiff5_4.3.0-6ubuntu0.8_amd64.deb ...
Unpacking libtiff5:amd64 (4.3.0-6ubuntu0.8) ...
Selecting previously unselected package libxpm4:amd64.
Preparing to unpack .../09-libxpm4_1%3a3.5.12-1ubuntu0.22.04.2_amd64.deb ...
Unpacking libxpm4:amd64 (1:3.5.12-1ubuntu0.22.04.2) ...
Selecting previously unselected package libgd3:amd64.
Preparing to unpack .../10-libgd3_2.3.0-2ubuntu2_amd64.deb ...
Unpacking libgd3:amd64 (2.3.0-2ubuntu2) ...
Selecting previously unselected package nginx-common.
Preparing to unpack .../11-nginx-common_1.18.0-6ubuntu14.4_all.deb ...
Unpacking nginx-common (1.18.0-6ubuntu14.4) ...
Selecting previously unselected package libnginx-mod-http-geoip2.
Preparing to unpack .../12-libnginx-mod-http-geoip2_1.18.0-6ubuntu14.4_amd64.deb ...
Unpacking libnginx-mod-http-geoip2 (1.18.0-6ubuntu14.4) ...
Selecting previously unselected package libnginx-mod-http-image-filter.
Preparing to unpack .../13-libnginx-mod-http-image-filter_1.18.0-6ubuntu14.4_amd64.deb ...
Unpacking libnginx-mod-http-image-filter (1.18.0-6ubuntu14.4) ...
Selecting previously unselected package libnginx-mod-http-xslt-filter.
Preparing to unpack .../14-libnginx-mod-http-xslt-filter_1.18.0-6ubuntu14.4_amd64.deb ...
Unpacking libnginx-mod-http-xslt-filter (1.18.0-6ubuntu14.4) ...
Selecting previously unselected package libnginx-mod-mail.
Preparing to unpack .../15-libnginx-mod-mail_1.18.0-6ubuntu14.4_amd64.deb ...
Unpacking libnginx-mod-mail (1.18.0-6ubuntu14.4) ...
Selecting previously unselected package libnginx-mod-stream.
Preparing to unpack .../16-libnginx-mod-stream_1.18.0-6ubuntu14.4_amd64.deb ...
Unpacking libnginx-mod-stream (1.18.0-6ubuntu14.4) ...
Selecting previously unselected package libnginx-mod-stream-geoip2.
Preparing to unpack .../17-libnginx-mod-stream-geoip2_1.18.0-6ubuntu14.4_amd64.deb ...
Unpacking libnginx-mod-stream-geoip2 (1.18.0-6ubuntu14.4) ...
Selecting previously unselected package nginx-core.
Preparing to unpack .../18-nginx-core_1.18.0-6ubuntu14.4_amd64.deb ...
Unpacking nginx-core (1.18.0-6ubuntu14.4) ...
Selecting previously unselected package nginx.
Preparing to unpack .../19-nginx_1.18.0-6ubuntu14.4_amd64.deb ...
Unpacking nginx (1.18.0-6ubuntu14.4) ...
Setting up libxpm4:amd64 (1:3.5.12-1ubuntu0.22.04.2) ...
Setting up libdeflate0:amd64 (1.10-2) ...
Setting up nginx-common (1.18.0-6ubuntu14.4) ...
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /lib/systemd/system/nginx.service.
Setting up libjbig0:amd64 (2.1-3.1ubuntu0.22.04.1) ...
Setting up libnginx-mod-http-xslt-filter (1.18.0-6ubuntu14.4) ...
Setting up fonts-dejavu-core (2.37-2build1) ...
Setting up libjpeg-turbo8:amd64 (2.1.2-0ubuntu1) ...
Setting up libwebp7:amd64 (1.2.2-2ubuntu0.22.04.2) ...
Setting up libnginx-mod-http-geoip2 (1.18.0-6ubuntu14.4) ...
Setting up libjpeg8:amd64 (8c-2ubuntu10) ...
Setting up libnginx-mod-mail (1.18.0-6ubuntu14.4) ...
Setting up fontconfig-config (2.13.1-4.2ubuntu5) ...
Setting up libnginx-mod-stream (1.18.0-6ubuntu14.4) ...
Setting up libtiff5:amd64 (4.3.0-6ubuntu0.8) ...
Setting up libfontconfig1:amd64 (2.13.1-4.2ubuntu5) ...
Setting up libnginx-mod-stream-geoip2 (1.18.0-6ubuntu14.4) ...
Setting up libgd3:amd64 (2.3.0-2ubuntu2) ...
Setting up libnginx-mod-http-image-filter (1.18.0-6ubuntu14.4) ...
Setting up nginx-core (1.18.0-6ubuntu14.4) ...
 * Upgrading binary nginx                                                                                                                                                                          [ OK ] 
Setting up nginx (1.18.0-6ubuntu14.4) ...
Processing triggers for ufw (0.36.1-4ubuntu0.1) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.8) ...
Scanning processes...                                                                                                                                                                                     
Scanning candidates...                                                                                                                                                                                    
Scanning linux images...                                                                                                                                                                                  

Running kernel seems to be up-to-date.

Restarting services...
Service restarts being deferred:
 /etc/needrestart/restart.d/dbus.service
 systemctl restart networkd-dispatcher.service
 systemctl restart systemd-logind.service
 systemctl restart unattended-upgrades.service
 systemctl restart user@1000.service

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
```
> 2. Khởi chạy dịch vụ `nginx`
```shell
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx
```
> (Optional). Khai báo dns record tại nơi quản lý tên miền

> 3. Tạo file Virtual Host cho domain `kbuor.io.vn`
```shell
sudo nano /etc/nginx/sites-available/kbuor.io.vn.conf
```
> Tạo block `server` với thông tin như bên dưới

```shell
server {
        listen 80;
        server_name kbuor.io.vn;

        root /var/www/kbuor.io.vn;
        index index.html;
}
```
```shell
sudo ln -s /etc/nginx/sites-available/kbuor.io.vn.conf /etc/nginx/sites-enabled/
```
> 4. Tạo thư mục chứa source web
```shell
sudo mkdir -p /var/www/kbuor.io.vn/
```
> Set quyền và sở hữu cho thư mục chứa source
```shell
sudo chown -R www-data:www-data /var/www
```
> 5. Tạo file index demo
```shell
sudo echo "DAY LA WEB SERVER CUA KBUOR TREN UBUNTU" > /var/www/kbuor.io.vn/index.html
```
> 6. Kiểm tra cú pháp của các file configure
```shell
sudo nginx -t
```
```shell
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
> 7. Khởi động lại dịch vụ `nginx`
```shell
sudo systemctl restart nginx
```
> Kết quả


![image](https://github.com/kbuor/Linux-LPIC-2/assets/77895173/08cf4a74-e487-4f12-8786-5db146ebeca1)


## TĂNG BẢO MẬT CHO WEBSERVER BẰNG CÁCH CHẠY VỚI GIAO THỨC HTTPS 
---
> 1. Request Commercial SSL Certificate
> Cài đặt gói `certbot` (Lưu ý, gói `certbot` nằm trong repo Extra Package Enterprise Linux của RHEL. Nếu chưa có, cài đặt gói `epel-release` và update repo)
```shell
sudo apt install certbot
```
```shell
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  python3-acme python3-certbot python3-configargparse python3-icu python3-josepy python3-parsedatetime python3-requests-toolbelt python3-rfc3339 python3-zope.component python3-zope.event
  python3-zope.hookable
Suggested packages:
  python-certbot-doc python3-certbot-apache python3-certbot-nginx python-acme-doc
The following NEW packages will be installed:
  certbot python3-acme python3-certbot python3-configargparse python3-icu python3-josepy python3-parsedatetime python3-requests-toolbelt python3-rfc3339 python3-zope.component python3-zope.event
  python3-zope.hookable
0 upgraded, 12 newly installed, 0 to remove and 3 not upgraded.
Need to get 958 kB of archives.
After this operation, 4,915 kB of additional disk space will be used.
Get:1 http://vn.archive.ubuntu.com/ubuntu jammy/universe amd64 python3-josepy all 1.10.0-1 [22.0 kB]
Get:2 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 python3-requests-toolbelt all 0.9.1-1 [38.0 kB]
Get:3 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 python3-rfc3339 all 1.1-3 [7,110 B]
Get:4 http://vn.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 python3-acme all 1.21.0-1ubuntu0.1 [36.4 kB]
Get:5 http://vn.archive.ubuntu.com/ubuntu jammy/universe amd64 python3-configargparse all 1.5.3-1 [26.9 kB]
Get:6 http://vn.archive.ubuntu.com/ubuntu jammy/universe amd64 python3-parsedatetime all 2.6-2 [32.9 kB]
Get:7 http://vn.archive.ubuntu.com/ubuntu jammy/universe amd64 python3-zope.hookable amd64 5.1.0-1build1 [11.6 kB]
Get:8 http://vn.archive.ubuntu.com/ubuntu jammy/universe amd64 python3-zope.event all 4.4-3 [8,180 B]
Get:9 http://vn.archive.ubuntu.com/ubuntu jammy/universe amd64 python3-zope.component all 4.3.0-3 [38.3 kB]
Get:10 http://vn.archive.ubuntu.com/ubuntu jammy/universe amd64 python3-certbot all 1.21.0-1build1 [175 kB]
Get:11 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 python3-icu amd64 2.8.1-0ubuntu2 [540 kB]
Get:12 http://vn.archive.ubuntu.com/ubuntu jammy/universe amd64 certbot all 1.21.0-1build1 [21.3 kB]
Fetched 958 kB in 1s (934 kB/s)
Preconfiguring packages ...
Selecting previously unselected package python3-josepy.
(Reading database ... 74808 files and directories currently installed.)
Preparing to unpack .../00-python3-josepy_1.10.0-1_all.deb ...
Unpacking python3-josepy (1.10.0-1) ...
Selecting previously unselected package python3-requests-toolbelt.
Preparing to unpack .../01-python3-requests-toolbelt_0.9.1-1_all.deb ...
Unpacking python3-requests-toolbelt (0.9.1-1) ...
Selecting previously unselected package python3-rfc3339.
Preparing to unpack .../02-python3-rfc3339_1.1-3_all.deb ...
Unpacking python3-rfc3339 (1.1-3) ...
Selecting previously unselected package python3-acme.
Preparing to unpack .../03-python3-acme_1.21.0-1ubuntu0.1_all.deb ...
Unpacking python3-acme (1.21.0-1ubuntu0.1) ...
Selecting previously unselected package python3-configargparse.
Preparing to unpack .../04-python3-configargparse_1.5.3-1_all.deb ...
Unpacking python3-configargparse (1.5.3-1) ...
Selecting previously unselected package python3-parsedatetime.
Preparing to unpack .../05-python3-parsedatetime_2.6-2_all.deb ...
Unpacking python3-parsedatetime (2.6-2) ...
Selecting previously unselected package python3-zope.hookable.
Preparing to unpack .../06-python3-zope.hookable_5.1.0-1build1_amd64.deb ...
Unpacking python3-zope.hookable (5.1.0-1build1) ...
Selecting previously unselected package python3-zope.event.
Preparing to unpack .../07-python3-zope.event_4.4-3_all.deb ...
Unpacking python3-zope.event (4.4-3) ...
Selecting previously unselected package python3-zope.component.
Preparing to unpack .../08-python3-zope.component_4.3.0-3_all.deb ...
Unpacking python3-zope.component (4.3.0-3) ...
Selecting previously unselected package python3-certbot.
Preparing to unpack .../09-python3-certbot_1.21.0-1build1_all.deb ...
Unpacking python3-certbot (1.21.0-1build1) ...
Selecting previously unselected package python3-icu.
Preparing to unpack .../10-python3-icu_2.8.1-0ubuntu2_amd64.deb ...
Unpacking python3-icu (2.8.1-0ubuntu2) ...
Selecting previously unselected package certbot.
Preparing to unpack .../11-certbot_1.21.0-1build1_all.deb ...
Unpacking certbot (1.21.0-1build1) ...
Setting up python3-configargparse (1.5.3-1) ...
Setting up python3-requests-toolbelt (0.9.1-1) ...
Setting up python3-parsedatetime (2.6-2) ...
Setting up python3-icu (2.8.1-0ubuntu2) ...
Setting up python3-zope.event (4.4-3) ...
Setting up python3-zope.hookable (5.1.0-1build1) ...
Setting up python3-josepy (1.10.0-1) ...
Setting up python3-rfc3339 (1.1-3) ...
Setting up python3-zope.component (4.3.0-3) ...
Setting up python3-acme (1.21.0-1ubuntu0.1) ...
Setting up python3-certbot (1.21.0-1build1) ...
Setting up certbot (1.21.0-1build1) ...
Created symlink /etc/systemd/system/timers.target.wants/certbot.timer → /lib/systemd/system/certbot.timer.
Processing triggers for man-db (2.10.2-1) ...
Scanning processes...                                                                                                                                                                                     
Scanning candidates...                                                                                                                                                                                    
Scanning linux images...                                                                                                                                                                                  

Running kernel seems to be up-to-date.

Restarting services...
Service restarts being deferred:
 /etc/needrestart/restart.d/dbus.service
 systemctl restart networkd-dispatcher.service
 systemctl restart systemd-logind.service
 systemctl restart unattended-upgrades.service
 systemctl restart user@1000.service

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
```
> Request một certificate cho domain `kbuor.io.vn`
```shell
sudo certbot certonly --manual --preferred-challenges dns -d kbuor.io.vn
```
```shell
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Enter email address (used for urgent renewal and security notices)
 (Enter 'c' to cancel): admin@kbuor.io.vn

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.4-April-3-2024.pdf. You must agree in
order to register with the ACME server. Do you agree?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: y

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing, once your first certificate is successfully issued, to
share your email address with the Electronic Frontier Foundation, a founding
partner of the Let's Encrypt project and the non-profit organization that
develops Certbot? We'd like to send you email about our work encrypting the web,
EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: y
Account registered.
Requesting a certificate for kbuor.io.vn

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please deploy a DNS TXT record under the name:

_acme-challenge.kbuor.io.vn.

with the following value:

ESUm2D54JXrJ7MEnCcfFaefRIPUUcyDagdao7y3lY0c

Before continuing, verify the TXT record has been deployed. Depending on the DNS
provider, this may take some time, from a few seconds to multiple minutes. You can
check if it has finished deploying with aid of online tools, such as the Google
Admin Toolbox: https://toolbox.googleapps.com/apps/dig/#TXT/_acme-challenge.kbuor.io.vn.
Look for one or more bolded line(s) below the line ';ANSWER'. It should show the
value(s) you've just added.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Press Enter to Continue
```
> Tạo DNS record tại nơi quản trị tên miền với thông tin được hiển thị
```shell
_acme-challenge.kbuor.io.vn.

with the following value:

ESUm2D54JXrJ7MEnCcfFaefRIPUUcyDagdao7y3lY0c
```

![image](https://github.com/kbuor/Linux-LPIC-2/assets/77895173/b1237e0c-8068-4cf1-ad21-1ff82e13719d)

> Sao khi tạo xong `enter` để tiếp tục

> Kết quả trả về request thành công, certificate, private key, CA được lưu tại `/etc/letsencrypt/live/kbuor.io.vn/`
```shell
Press Enter to Continue

Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/kbuor.io.vn/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/kbuor.io.vn/privkey.pem
This certificate expires on 2024-09-04.
These files will be updated when the certificate renews.

NEXT STEPS:
- This certificate will not be renewed automatically. Autorenewal of --manual certificates requires the use of an authentication hook script (--manual-auth-hook) but one was not provided. To renew this certificate, repeat this same certbot command before the certificate's expiry date.
We were unable to subscribe you the EFF mailing list because your e-mail address appears to be invalid. You can try again later by visiting https://act.eff.org.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
If you like Certbot, please consider supporting our work by:
 * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
 * Donating to EFF:                    https://eff.org/donate-le
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```
> Sửa file `/etc/nginx/conf.d/kbuor.io.vn.conf` cho phép nginx chạy ở `443` với `ssl` và `https`
```shell
sudo nano /etc/nginx/sites-available/kbuor.io.vn.conf
```
> Thêm block server 443

```shell
server {
        listen 443 ssl;
        server_name kbuor.io.vn;
        ssl_certificate         /etc/letsencrypt/live/kbuor.io.vn/fullchain.pem;
        ssl_certificate_key     /etc/letsencrypt/live/kbuor.io.vn/privkey.pem;

        root /var/www/kbuor.io.vn;
        index index.html;
}
```

> Điều chỉnh block server http 80 để tự động redirect về https 443
```shell
server {
        listen 80;
        server_name kbuor.io.vn;

        return 301 https://kbuor.io.vn$request_uri;

}
```
> File config hoàn hình sau khi chỉnh sửa
```shell
server {
        listen 80;
        server_name kbuor.io.vn;

        return 301 https://kbuor.io.vn$request_uri;

}
server {
        listen 443 ssl;
        server_name kbuor.io.vn;
        ssl_certificate         /etc/letsencrypt/live/kbuor.io.vn/fullchain.pem;
        ssl_certificate_key     /etc/letsencrypt/live/kbuor.io.vn/privkey.pem;

        root /var/www/kbuor.io.vn;
        index index.html;
}
```
> Kiểm tra cấu hình `nginx`
```shell
sudo nginx -t
```
```shell
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
> Khởi động lại dịch vụ `nginx`
```shell
sudo systemctl restart nginx
```
> Kiểm tra kết quả

![image](https://github.com/kbuor/Linux-LPIC-2/assets/77895173/c927be66-fa3f-4314-b23b-619f6566c05b)
