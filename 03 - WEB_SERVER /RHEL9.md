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

