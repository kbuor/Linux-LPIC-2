## THÔNG TIN CHUNG
---
Operating System: `AlmaLinux 9.4 (Seafoam Ocelot) (platform:el9)`

IP Address: `10.10.10.103/24`

Gateway: `10.10.10.10`

Hostname: `nginx.kbuor.io.local`

Domain: `kbuor.io.local`

## CHUẨN BỊ
---
> Tải các gói cần thiết cho RHEL, tắt firewall trong quá trình cài đặt, tắt SELINUX.
```shell
dnf install -y open-vm-tools git wget unzip zip epel-release vim net-tools vim
dnf update -y
systemctl stop firewalld
systemctl disable firewalld
setenforce 0
sed -i "s/=enforcing/=disabled/" /etc/sysconfig/selinux
reboot
```

## TRIỂN KHAI
---
> 1. Cài đặt gói `nginx` từ repository của Alma Linux 9
```shell
dnf install instal
```
```shell
Last metadata expiration check: 0:13:20 ago on Thu Jun  6 20:31:04 2024.
Dependencies resolved.
=================================================================================================================================================================
 Package                                     Architecture                 Version                                          Repository                       Size
=================================================================================================================================================================
Installing:
 nginx                                       x86_64                       1:1.20.1-14.el9_2.1.alma.1                       appstream                        36 k
Installing dependencies:
 almalinux-logos-httpd                       noarch                       90.5.1-1.1.el9                                   appstream                        18 k
 nginx-core                                  x86_64                       1:1.20.1-14.el9_2.1.alma.1                       appstream                       565 k
 nginx-filesystem                            noarch                       1:1.20.1-14.el9_2.1.alma.1                       appstream                       8.4 k

Transaction Summary
=================================================================================================================================================================
Install  4 Packages

Total download size: 627 k
Installed size: 1.8 M
Is this ok [y/N]: y
Downloading Packages:
(1/4): nginx-1.20.1-14.el9_2.1.alma.1.x86_64.rpm                                                                                 321 kB/s |  36 kB     00:00    
(2/4): almalinux-logos-httpd-90.5.1-1.1.el9.noarch.rpm                                                                           155 kB/s |  18 kB     00:00    
(3/4): nginx-filesystem-1.20.1-14.el9_2.1.alma.1.noarch.rpm                                                                      348 kB/s | 8.4 kB     00:00    
(4/4): nginx-core-1.20.1-14.el9_2.1.alma.1.x86_64.rpm                                                                            3.7 MB/s | 565 kB     00:00    
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                            540 kB/s | 627 kB     00:01     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                         1/1 
  Running scriptlet: nginx-filesystem-1:1.20.1-14.el9_2.1.alma.1.noarch                                                                                      1/4 
  Installing       : nginx-filesystem-1:1.20.1-14.el9_2.1.alma.1.noarch                                                                                      1/4 
  Installing       : nginx-core-1:1.20.1-14.el9_2.1.alma.1.x86_64                                                                                            2/4 
  Installing       : almalinux-logos-httpd-90.5.1-1.1.el9.noarch                                                                                             3/4 
  Installing       : nginx-1:1.20.1-14.el9_2.1.alma.1.x86_64                                                                                                 4/4 
  Running scriptlet: nginx-1:1.20.1-14.el9_2.1.alma.1.x86_64                                                                                                 4/4 
  Verifying        : almalinux-logos-httpd-90.5.1-1.1.el9.noarch                                                                                             1/4 
  Verifying        : nginx-1:1.20.1-14.el9_2.1.alma.1.x86_64                                                                                                 2/4 
  Verifying        : nginx-core-1:1.20.1-14.el9_2.1.alma.1.x86_64                                                                                            3/4 
  Verifying        : nginx-filesystem-1:1.20.1-14.el9_2.1.alma.1.noarch                                                                                      4/4 

Installed:
  almalinux-logos-httpd-90.5.1-1.1.el9.noarch                nginx-1:1.20.1-14.el9_2.1.alma.1.x86_64         nginx-core-1:1.20.1-14.el9_2.1.alma.1.x86_64        
  nginx-filesystem-1:1.20.1-14.el9_2.1.alma.1.noarch        

Complete!
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
vi /etc/nginx/conf.d/kbuor.io.vn.conf
```
> Tạo block `server` với thông tin như bên dưới

```shell
server {
        listen 80;
        server_name kbuor.io.vn;

        root /var/www/kbuor.io.vn/index.html;
        index index.html;
}
```
> 4. Tạo thư mục chứa source web
```shell
mkdir -p /var/www/kbuor.io.vn/
```
> Set quyền và sở hữu cho thư mục chứa source
```shell
chown -R nginx:nginx /var/www
```
> 5. Tạo file index demo
```shell
echo "DAY LA WEB SERVER CUA KBUOR" > /var/www/kbuor.io.vn/index.html
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


![image](https://github.com/kbuor/Linux-LPIC-2/assets/77895173/5eca2b7b-c25c-4a6b-8230-b221cd3515e3)

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

