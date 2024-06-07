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

