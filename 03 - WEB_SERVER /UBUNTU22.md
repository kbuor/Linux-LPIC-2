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
apt update -y && apt upgrade -y
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
systemctl enable nginx
systemctl start nginx
systemctl status nginx
```
> (Optional). Khai báo dns record tại nơi quản lý tên miền

> 3. Tạo file Virtual Host cho domain `kbuor.io.vn`
```shell
/etc/nginx/sites-available/kbuor.io.vn.conf
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
mkdir -p /var/www/kbuor.io.vn/
```
> Set quyền và sở hữu cho thư mục chứa source
```shell
chown -R www-data:www-data /var/www
```
> 5. Tạo file index demo
```shell
echo "DAY LA WEB SERVER CUA KBUOR TREN UBUNTU" > /var/www/kbuor.io.vn/index.html
```
> 6. Kiểm tra cú pháp của các file configure
```shell
nginx -t
```
```shell
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
> 7. Khởi động lại dịch vụ `nginx`
```shell
systemctl restart nginx
```
> Kết quả


![image](https://github.com/kbuor/Linux-LPIC-2/assets/77895173/08cf4a74-e487-4f12-8786-5db146ebeca1)


## TĂNG BẢO MẬT CHO WEBSERVER BẰNG CÁCH CHẠY VỚI GIAO THỨC HTTPS 
---
> 1. Request Commercial SSL Certificate
> Cài đặt gói `certbot` (Lưu ý, gói `certbot` nằm trong repo Extra Package Enterprise Linux của RHEL. Nếu chưa có, cài đặt gói `epel-release` và update repo)
```shell
dnf install certbot
```
```shell
Last metadata expiration check: 0:51:24 ago on Thu Jun  6 20:31:04 2024.
Dependencies resolved.
==========================================================================================================================================================================================================
 Package                                                     Architecture                            Version                                             Repository                                  Size
==========================================================================================================================================================================================================
Installing:
 certbot                                                     noarch                                  2.9.0-1.el9                                         epel                                        49 k
Installing dependencies:
 fontawesome-fonts                                           noarch                                  1:4.7.0-13.el9                                      appstream                                  204 k
 fonts-filesystem                                            noarch                                  1:2.0.5-7.el9.1                                     baseos                                     9.0 k
 python3-acme                                                noarch                                  2.9.0-1.el9                                         epel                                       160 k
 python3-certbot                                             noarch                                  2.9.0-1.el9                                         epel                                       684 k
 python3-cffi                                                x86_64                                  1.14.5-5.el9                                        baseos                                     241 k
 python3-chardet                                             noarch                                  4.0.0-5.el9                                         baseos                                     209 k
 python3-configargparse                                      noarch                                  1.7-1.el9                                           epel                                        45 k
 python3-configobj                                           noarch                                  5.0.6-25.el9                                        appstream                                   62 k
 python3-cryptography                                        x86_64                                  36.0.1-4.el9                                        baseos                                     1.1 M
 python3-distro                                              noarch                                  1.5.0-7.el9                                         appstream                                   36 k
 python3-idna                                                noarch                                  2.10-7.el9                                          baseos                                      92 k
 python3-importlib-metadata                                  noarch                                  4.12.0-2.el9                                        epel                                        43 k
 python3-josepy                                              noarch                                  1.13.0-1.el9                                        epel                                        60 k
 python3-parsedatetime                                       noarch                                  2.6-5.el9                                           epel                                        79 k
 python3-ply                                                 noarch                                  3.11-14.el9                                         baseos                                     103 k
 python3-pyOpenSSL                                           noarch                                  21.0.0-1.el9                                        epel                                        90 k
 python3-pycparser                                           noarch                                  2.20-6.el9                                          baseos                                     124 k
 python3-pyrfc3339                                           noarch                                  1.1-11.el9                                          epel                                        18 k
 python3-pysocks                                             noarch                                  1.7.1-12.el9                                        baseos                                      34 k
 python3-pytz                                                noarch                                  2021.1-5.el9                                        appstream                                   47 k
 python3-requests                                            noarch                                  2.25.1-8.el9                                        baseos                                     113 k
 python3-setuptools                                          noarch                                  53.0.0-12.el9                                       baseos                                     839 k
 python3-urllib3                                             noarch                                  1.26.5-5.el9                                        baseos                                     187 k
 python3-zipp                                                noarch                                  0.5.1-1.el9                                         epel                                        14 k
Installing weak dependencies:
 python-josepy-doc                                           noarch                                  1.13.0-1.el9                                        epel                                        19 k

Transaction Summary
==========================================================================================================================================================================================================
Install  26 Packages

Total download size: 4.6 M
Installed size: 20 M
Is this ok [y/N]: y
Downloading Packages:
(1/26): python3-distro-1.5.0-7.el9.noarch.rpm                                                                                                                              46 kB/s |  36 kB     00:00    
(2/26): python3-pytz-2021.1-5.el9.noarch.rpm                                                                                                                              1.7 MB/s |  47 kB     00:00    
(3/26): python3-configobj-5.0.6-25.el9.noarch.rpm                                                                                                                          77 kB/s |  62 kB     00:00    
(4/26): fontawesome-fonts-4.7.0-13.el9.noarch.rpm                                                                                                                         249 kB/s | 204 kB     00:00    
(5/26): fonts-filesystem-2.0.5-7.el9.1.noarch.rpm                                                                                                                         410 kB/s | 9.0 kB     00:00    
(6/26): python3-cffi-1.14.5-5.el9.x86_64.rpm                                                                                                                              8.7 MB/s | 241 kB     00:00    
(7/26): python3-chardet-4.0.0-5.el9.noarch.rpm                                                                                                                            7.7 MB/s | 209 kB     00:00    
(8/26): python3-ply-3.11-14.el9.noarch.rpm                                                                                                                                4.7 MB/s | 103 kB     00:00    
(9/26): python3-idna-2.10-7.el9.noarch.rpm                                                                                                                                2.4 MB/s |  92 kB     00:00    
(10/26): python3-pycparser-2.20-6.el9.noarch.rpm                                                                                                                          4.7 MB/s | 124 kB     00:00    
(11/26): python3-pysocks-1.7.1-12.el9.noarch.rpm                                                                                                                          1.6 MB/s |  34 kB     00:00    
(12/26): python3-cryptography-36.0.1-4.el9.x86_64.rpm                                                                                                                      13 MB/s | 1.1 MB     00:00    
(13/26): python3-requests-2.25.1-8.el9.noarch.rpm                                                                                                                         4.7 MB/s | 113 kB     00:00    
(14/26): python3-setuptools-53.0.0-12.el9.noarch.rpm                                                                                                                       10 MB/s | 839 kB     00:00    
(15/26): python3-urllib3-1.26.5-5.el9.noarch.rpm                                                                                                                          2.6 MB/s | 187 kB     00:00    
(16/26): python-josepy-doc-1.13.0-1.el9.noarch.rpm                                                                                                                         13 kB/s |  19 kB     00:01    
(17/26): certbot-2.9.0-1.el9.noarch.rpm                                                                                                                                    31 kB/s |  49 kB     00:01    
(18/26): python3-acme-2.9.0-1.el9.noarch.rpm                                                                                                                               93 kB/s | 160 kB     00:01    
(19/26): python3-configargparse-1.7-1.el9.noarch.rpm                                                                                                                      148 kB/s |  45 kB     00:00    
(20/26): python3-certbot-2.9.0-1.el9.noarch.rpm                                                                                                                           1.9 MB/s | 684 kB     00:00    
(21/26): python3-importlib-metadata-4.12.0-2.el9.noarch.rpm                                                                                                               417 kB/s |  43 kB     00:00    
(22/26): python3-josepy-1.13.0-1.el9.noarch.rpm                                                                                                                           681 kB/s |  60 kB     00:00    
(23/26): python3-parsedatetime-2.6-5.el9.noarch.rpm                                                                                                                       932 kB/s |  79 kB     00:00    
(24/26): python3-pyOpenSSL-21.0.0-1.el9.noarch.rpm                                                                                                                        1.0 MB/s |  90 kB     00:00    
(25/26): python3-pyrfc3339-1.1-11.el9.noarch.rpm                                                                                                                          220 kB/s |  18 kB     00:00    
(26/26): python3-zipp-0.5.1-1.el9.noarch.rpm                                                                                                                              169 kB/s |  14 kB     00:00    
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                     538 kB/s | 4.6 MB     00:08     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                  1/1 
  Installing       : python3-setuptools-53.0.0-12.el9.noarch                                                                                                                                         1/26 
  Installing       : python3-pytz-2021.1-5.el9.noarch                                                                                                                                                2/26 
  Installing       : python3-pyrfc3339-1.1-11.el9.noarch                                                                                                                                             3/26 
  Installing       : python3-idna-2.10-7.el9.noarch                                                                                                                                                  4/26 
  Installing       : python3-distro-1.5.0-7.el9.noarch                                                                                                                                               5/26 
  Installing       : python3-zipp-0.5.1-1.el9.noarch                                                                                                                                                 6/26 
  Installing       : python3-importlib-metadata-4.12.0-2.el9.noarch                                                                                                                                  7/26 
  Installing       : python3-parsedatetime-2.6-5.el9.noarch                                                                                                                                          8/26 
  Installing       : python3-configargparse-1.7-1.el9.noarch                                                                                                                                         9/26 
  Installing       : python-josepy-doc-1.13.0-1.el9.noarch                                                                                                                                          10/26 
  Installing       : python3-pysocks-1.7.1-12.el9.noarch                                                                                                                                            11/26 
  Installing       : python3-urllib3-1.26.5-5.el9.noarch                                                                                                                                            12/26 
  Installing       : python3-ply-3.11-14.el9.noarch                                                                                                                                                 13/26 
  Installing       : python3-pycparser-2.20-6.el9.noarch                                                                                                                                            14/26 
  Installing       : python3-cffi-1.14.5-5.el9.x86_64                                                                                                                                               15/26 
  Installing       : python3-cryptography-36.0.1-4.el9.x86_64                                                                                                                                       16/26 
  Installing       : python3-pyOpenSSL-21.0.0-1.el9.noarch                                                                                                                                          17/26 
  Installing       : python3-josepy-1.13.0-1.el9.noarch                                                                                                                                             18/26 
  Installing       : python3-chardet-4.0.0-5.el9.noarch                                                                                                                                             19/26 
  Installing       : python3-requests-2.25.1-8.el9.noarch                                                                                                                                           20/26 
  Installing       : python3-acme-2.9.0-1.el9.noarch                                                                                                                                                21/26 
  Installing       : fonts-filesystem-1:2.0.5-7.el9.1.noarch                                                                                                                                        22/26 
  Installing       : fontawesome-fonts-1:4.7.0-13.el9.noarch                                                                                                                                        23/26 
  Installing       : python3-configobj-5.0.6-25.el9.noarch                                                                                                                                          24/26 
  Installing       : python3-certbot-2.9.0-1.el9.noarch                                                                                                                                             25/26 
  Installing       : certbot-2.9.0-1.el9.noarch                                                                                                                                                     26/26 
  Running scriptlet: certbot-2.9.0-1.el9.noarch                                                                                                                                                     26/26 
Created symlink /etc/systemd/system/timers.target.wants/certbot-renew.timer → /usr/lib/systemd/system/certbot-renew.timer.

Certbot auto renewal timer is not started by default.
Run 'systemctl start certbot-renew.timer' to enable automatic renewals.

  Verifying        : fontawesome-fonts-1:4.7.0-13.el9.noarch                                                                                                                                         1/26 
  Verifying        : python3-configobj-5.0.6-25.el9.noarch                                                                                                                                           2/26 
  Verifying        : python3-distro-1.5.0-7.el9.noarch                                                                                                                                               3/26 
  Verifying        : python3-pytz-2021.1-5.el9.noarch                                                                                                                                                4/26 
  Verifying        : fonts-filesystem-1:2.0.5-7.el9.1.noarch                                                                                                                                         5/26 
  Verifying        : python3-cffi-1.14.5-5.el9.x86_64                                                                                                                                                6/26 
  Verifying        : python3-chardet-4.0.0-5.el9.noarch                                                                                                                                              7/26 
  Verifying        : python3-cryptography-36.0.1-4.el9.x86_64                                                                                                                                        8/26 
  Verifying        : python3-idna-2.10-7.el9.noarch                                                                                                                                                  9/26 
  Verifying        : python3-ply-3.11-14.el9.noarch                                                                                                                                                 10/26 
  Verifying        : python3-pycparser-2.20-6.el9.noarch                                                                                                                                            11/26 
  Verifying        : python3-pysocks-1.7.1-12.el9.noarch                                                                                                                                            12/26 
  Verifying        : python3-requests-2.25.1-8.el9.noarch                                                                                                                                           13/26 
  Verifying        : python3-setuptools-53.0.0-12.el9.noarch                                                                                                                                        14/26 
  Verifying        : python3-urllib3-1.26.5-5.el9.noarch                                                                                                                                            15/26 
  Verifying        : certbot-2.9.0-1.el9.noarch                                                                                                                                                     16/26 
  Verifying        : python-josepy-doc-1.13.0-1.el9.noarch                                                                                                                                          17/26 
  Verifying        : python3-acme-2.9.0-1.el9.noarch                                                                                                                                                18/26 
  Verifying        : python3-certbot-2.9.0-1.el9.noarch                                                                                                                                             19/26 
  Verifying        : python3-configargparse-1.7-1.el9.noarch                                                                                                                                        20/26 
  Verifying        : python3-importlib-metadata-4.12.0-2.el9.noarch                                                                                                                                 21/26 
  Verifying        : python3-josepy-1.13.0-1.el9.noarch                                                                                                                                             22/26 
  Verifying        : python3-parsedatetime-2.6-5.el9.noarch                                                                                                                                         23/26 
  Verifying        : python3-pyOpenSSL-21.0.0-1.el9.noarch                                                                                                                                          24/26 
  Verifying        : python3-pyrfc3339-1.1-11.el9.noarch                                                                                                                                            25/26 
  Verifying        : python3-zipp-0.5.1-1.el9.noarch                                                                                                                                                26/26 

Installed:
  certbot-2.9.0-1.el9.noarch                      fontawesome-fonts-1:4.7.0-13.el9.noarch                fonts-filesystem-1:2.0.5-7.el9.1.noarch          python-josepy-doc-1.13.0-1.el9.noarch          
  python3-acme-2.9.0-1.el9.noarch                 python3-certbot-2.9.0-1.el9.noarch                     python3-cffi-1.14.5-5.el9.x86_64                 python3-chardet-4.0.0-5.el9.noarch             
  python3-configargparse-1.7-1.el9.noarch         python3-configobj-5.0.6-25.el9.noarch                  python3-cryptography-36.0.1-4.el9.x86_64         python3-distro-1.5.0-7.el9.noarch              
  python3-idna-2.10-7.el9.noarch                  python3-importlib-metadata-4.12.0-2.el9.noarch         python3-josepy-1.13.0-1.el9.noarch               python3-parsedatetime-2.6-5.el9.noarch         
  python3-ply-3.11-14.el9.noarch                  python3-pyOpenSSL-21.0.0-1.el9.noarch                  python3-pycparser-2.20-6.el9.noarch              python3-pyrfc3339-1.1-11.el9.noarch            
  python3-pysocks-1.7.1-12.el9.noarch             python3-pytz-2021.1-5.el9.noarch                       python3-requests-2.25.1-8.el9.noarch             python3-setuptools-53.0.0-12.el9.noarch        
  python3-urllib3-1.26.5-5.el9.noarch             python3-zipp-0.5.1-1.el9.noarch                       

Complete!
```
> Request một certificate cho domain `kbuor.io.vn`
```shell
certbot certonly --manual --preferred-challenges dns -d kbuor.io.vn
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
(Y)es/(N)o: yes

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing, once your first certificate is successfully issued, to
share your email address with the Electronic Frontier Foundation, a founding
partner of the Let's Encrypt project and the non-profit organization that
develops Certbot? We'd like to send you email about our work encrypting the web,
EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: yes
Account registered.
Requesting a certificate for kbuor.io.vn

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please deploy a DNS TXT record under the name:

_acme-challenge.kbuor.io.vn.

with the following value:

lDC2PyO_exy_ZnzN-UyXUzhn_tB8fnztIg7R7c1QfuI

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

lDC2PyO_exy_ZnzN-UyXUzhn_tB8fnztIg7R7c1QfuI
```

![image](https://github.com/kbuor/Linux-LPIC-2/assets/77895173/8c007ee0-3582-41f5-9d07-6e233bacc2bf)

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
vi /etc/nginx/conf.d/kbuor.io.vn.conf
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
nginx -t
```
```shell
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
> Khởi động lại dịch vụ `nginx`
```shell
systemctl restart nginx
```
> Kiểm tra kết quả
