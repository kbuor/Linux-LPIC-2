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

> Đường dẫn của file userlist: `userlist_file=/etc/vsftpd/user_list`

> Dùng file userlist để cho phép truy cập: `userlist_deny=NO`

> Giới hạn và cho phép truy cập vào thư mục FTP: `chroot_local_user=YES` `allow_writeable_chroot=YES`

> File hoàn chỉnh sau khi chỉnh sửa
```shell
# Example config file /etc/vsftpd/vsftpd.conf
#
# The default compiled in settings are fairly paranoid. This sample file
# loosens things up a bit, to make the ftp daemon more usable.
# Please see vsftpd.conf.5 for all compiled in defaults.
#
# READ THIS: This example file is NOT an exhaustive list of vsftpd options.
# Please read the vsftpd.conf.5 manual page to get a full idea of vsftpd's
# capabilities.
#
# Allow anonymous FTP? (Beware - allowed by default if you comment this out).
anonymous_enable=NO
#
# Uncomment this to allow local users to log in.
local_enable=YES
#
# Uncomment this to enable any form of FTP write command.
write_enable=YES
#
# Default umask for local users is 077. You may wish to change this to 022,
# if your users expect that (022 is used by most other ftpd's)
local_umask=022
#
# Uncomment this to allow the anonymous FTP user to upload files. This only
# has an effect if the above global write enable is activated. Also, you will
# obviously need to create a directory writable by the FTP user.
# When SELinux is enforcing check for SE bool allow_ftpd_anon_write, allow_ftpd_full_access
#anon_upload_enable=YES
#
# Uncomment this if you want the anonymous FTP user to be able to create
# new directories.
#anon_mkdir_write_enable=YES
#
# Activate directory messages - messages given to remote users when they
# go into a certain directory.
dirmessage_enable=YES
#
# Activate logging of uploads/downloads.
xferlog_enable=YES
#
# Make sure PORT transfer connections originate from port 20 (ftp-data).
connect_from_port_20=YES
#
# If you want, you can arrange for uploaded anonymous files to be owned by
# a different user. Note! Using "root" for uploaded files is not
# recommended!
#chown_uploads=YES
#chown_username=whoever
#
# You may override where the log file goes if you like. The default is shown
# below.
xferlog_file=/var/log/xferlog
#
# If you want, you can have your log file in standard ftpd xferlog format.
# Note that the default log file location is /var/log/xferlog in this case.
xferlog_std_format=YES
#
# You may change the default value for timing out an idle session.
#idle_session_timeout=600
#
# You may change the default value for timing out a data connection.
#data_connection_timeout=120
#
# It is recommended that you define on your system a unique user which the
# ftp server can use as a totally isolated and unprivileged user.
#nopriv_user=ftpsecure
#
# Enable this and the server will recognise asynchronous ABOR requests. Not
# recommended for security (the code is non-trivial). Not enabling it,
# however, may confuse older FTP clients.
#async_abor_enable=YES
#
# By default the server will pretend to allow ASCII mode but in fact ignore
# the request. Turn on the below options to have the server actually do ASCII
# mangling on files when in ASCII mode. The vsftpd.conf(5) man page explains
# the behaviour when these options are disabled.
# Beware that on some FTP servers, ASCII support allows a denial of service
# attack (DoS) via the command "SIZE /big/file" in ASCII mode. vsftpd
# predicted this attack and has always been safe, reporting the size of the
# raw file.
# ASCII mangling is a horrible feature of the protocol.
#ascii_upload_enable=YES
#ascii_download_enable=YES
#
# You may fully customise the login banner string:
ftpd_banner=Welcome to KBUOR FTP service.
#
# You may specify a file of disallowed anonymous e-mail addresses. Apparently
# useful for combatting certain DoS attacks.
#deny_email_enable=YES
# (default follows)
#banned_email_file=/etc/vsftpd/banned_emails
#
# You may specify an explicit list of local users to chroot() to their home
# directory. If chroot_local_user is YES, then this list becomes a list of
# users to NOT chroot().
# (Warning! chroot'ing can be very dangerous. If using chroot, make sure that
# the user does not have write access to the top level directory within the
# chroot)
chroot_local_user=YES
allow_writeable_chroot=YES
#chroot_list_enable=YES
# (default follows)
#chroot_list_file=/etc/vsftpd/chroot_list
#
# You may activate the "-R" option to the builtin ls. This is disabled by
# default to avoid remote users being able to cause excessive I/O on large
# sites. However, some broken FTP clients such as "ncftp" and "mirror" assume
# the presence of the "-R" option, so there is a strong case for enabling it.
#ls_recurse_enable=YES
#
# When "listen" directive is enabled, vsftpd runs in standalone mode and
# listens on IPv4 sockets. This directive cannot be used in conjunction
# with the listen_ipv6 directive.
listen=NO
#
# This directive enables listening on IPv6 sockets. By default, listening
# on the IPv6 "any" address (::) will accept connections from both IPv6
# and IPv4 clients. It is not necessary to listen on *both* IPv4 and IPv6
# sockets. If you want that (perhaps because you want to listen on specific
# addresses) then you must run two copies of vsftpd with two configuration
# files.
# Make sure, that one of the listen options is commented !!
listen_ipv6=YES

pam_service_name=vsftpd
userlist_enable=YES
userlist_file=/etc/vsftpd/user_list
userlist_deny=NO
```
> Tạo user cho FTP
```shell
useradd ftp1
passwd ftp1
```
```shell
Changing password for user ftp1.
New password: 
BAD PASSWORD: The password fails the dictionary check - it is based on a dictionary word
Retype new password: 
passwd: all authentication tokens updated successfully.
```
> Thêm user `ftp1` vào userlist
```shell
echo "ftp1" | sudo tee –a /etc/vsftpd/user_list
```
```shell
ftp1
```

> Tạo và phân quyền thư mục cho FTP User
```shell
mkdir -p /home/ftp1/ftp/upload
chmod 550 /home/ftp1/ftp
chmod 750 /home/ftp1/ftp/upload
chown -R ftp1: /home/ftp1/ftp
```

> Start dịch vụ FTP Server
```shell
systemctl start vsftpd
systemctl enable vsftpd
systemctl status vsftpd
```
```shell
● vsftpd.service - Vsftpd ftp daemon
     Loaded: loaded (/usr/lib/systemd/system/vsftpd.service; enabled; preset: disabled)
     Active: active (running) since Fri 2024-06-07 16:48:59 +07; 8min ago
    Process: 2466 ExecStart=/usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf (code=exited, status=0/SUCCESS)
   Main PID: 2468 (vsftpd)
      Tasks: 1 (limit: 23165)
     Memory: 752.0K
        CPU: 44ms
     CGroup: /system.slice/vsftpd.service
             └─2468 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf

Jun 07 16:48:59 ftp.kbuor.io.local systemd[1]: Starting Vsftpd ftp daemon...
Jun 07 16:48:59 ftp.kbuor.io.local systemd[1]: Started Vsftpd ftp daemon.
```
> Kiểm tra dịch vụ
```shell
ftp ftp.kbuor.io.local
```
```shell
Connected to ftp.kbuor.io.local (10.10.10.105).
220 Welcome to KBUOR FTP service.
Name (ftp.kbuor.io.local:root): ftp1
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
```
> Setup SSL
```shell
vi /etc/vsftpd/vsftpd.conf
```
```shell
rsa_cert_file=/etc/ssl/private/vsftpd.pem
rsa_private_key_file=/etc/ssl/private/vsftpd.pem

ssl_enable=YES

allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
ssl_tlsv1=YES
ssl_sslv2=NO
ssl_sslv3=NO
require_ssl_reuse=NO
ssl_ciphers=HIGH
```
> Restart service `vsftpd`
```shell
systemctl restart vsftpd
```
