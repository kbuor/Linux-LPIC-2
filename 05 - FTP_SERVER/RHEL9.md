## THÔNG TIN CHUNG
---
Operating System: `AlmaLinux 9.4 (Seafoam Ocelot) (platform:el9)`

IP Address: `10.10.10.105/24`

Gateway: `10.10.10.10`

Hostname: `ftp.kbuor.io.local`

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
> Cài đặt gói `vsftpd` từ repository của AlmaLinux 9
```shell
dnf install vsftpd -y
```
```shell
Last metadata expiration check: 2:50:15 ago on Fri Jun  7 10:23:21 2024.
Dependencies resolved.
==========================================================================================================================================================================================================
 Package                                       Architecture                                  Version                                               Repository                                        Size
==========================================================================================================================================================================================================
Installing:
 vsftpd                                        x86_64                                        3.0.5-5.el9                                           appstream                                        157 k

Transaction Summary
==========================================================================================================================================================================================================
Install  1 Package

Total download size: 157 k
Installed size: 347 k
Downloading Packages:
vsftpd-3.0.5-5.el9.x86_64.rpm                                                                                                                                             691 kB/s | 157 kB     00:00    
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                      60 kB/s | 157 kB     00:02     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                  1/1 
  Installing       : vsftpd-3.0.5-5.el9.x86_64                                                                                                                                                        1/1 
  Running scriptlet: vsftpd-3.0.5-5.el9.x86_64                                                                                                                                                        1/1 
  Verifying        : vsftpd-3.0.5-5.el9.x86_64                                                                                                                                                        1/1 

Installed:
  vsftpd-3.0.5-5.el9.x86_64                                                                                                                                                                               

Complete!
```
> Cấu hình FTP Server

> Chỉnh sửa file `/etc/vsftpd/vsftpd.conf`
```shell
vi /etc/vsftpd/vsftpd.conf
```
> Cho phép/Từ chối Anonymous login: `anonymous_enable=YES`

> Cho phép/Từ chối local user login: `local_enable=YES`

> Cho phép/Từ chối quyền ghi của user: `write_enable=YES`

> Cho phép/Từ chối anonymous upload: `anon_upload_enable=YES`

> Cho phép/Từ chối anonymous ghi vào thư mục: `anon_mkdir_write_enable=YES`

> Cho phép ghi log: `xferlog_enable=YES`

> Sử dụng cổng 20 cho FTP-Data: `connect_from_port_20=YES`

> Nơi lưu trữ log: `xferlog_file=/var/log/xferlog`

> Câu chào: `ftpd_banner=Welcome to Kbuor FTP service.`

> Cho phép/Từ chôi sử dụng file userlist để chặn truy cập: `userlist_enable=YES`

# Create user for FTP
useradd ftp1

# Start FTP server
systemctl start vsftpd
systemctl enable vsftpd

# Manage user login ftp
vi /etc/vsftpd/user_list
