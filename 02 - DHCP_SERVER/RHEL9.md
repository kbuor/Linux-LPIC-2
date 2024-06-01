## THÔNG TIN CHUNG
---
Operating System: `AlmaLinux 9.4 (Seafoam Ocelot) (platform:el9)`

IP Address: `10.10.10.102/24`

Gateway: `10.10.10.10`

Hostname: `dhcp.kbuor.io.local`

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
> 1. Cài đặt gói `dhcp-server`
```shell
dnf install dhcp-server
```
```shell
Last metadata expiration check: 0:00:33 ago on Sun Jun  2 02:37:02 2024.
Dependencies resolved.
======================================================================================
 Package             Architecture   Version                      Repository      Size
======================================================================================
Installing:
 dhcp-server         x86_64         12:4.4.2-19.b1.el9           baseos         1.2 M
Installing dependencies:
 dhcp-common         noarch         12:4.4.2-19.b1.el9           baseos         128 k

Transaction Summary
======================================================================================
Install  2 Packages

Total download size: 1.3 M
Installed size: 4.2 M
Is this ok [y/N]: y
Downloading Packages:
(1/2): dhcp-common-4.4.2-19.b1.el9.noarch.rpm         1.2 MB/s | 128 kB     00:00    
(2/2): dhcp-server-4.4.2-19.b1.el9.x86_64.rpm         7.9 MB/s | 1.2 MB     00:00    
--------------------------------------------------------------------------------------
Total                                                 1.2 MB/s | 1.3 MB     00:01     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                              1/1 
  Installing       : dhcp-common-12:4.4.2-19.b1.el9.noarch                        1/2 
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64                        2/2 
  Installing       : dhcp-server-12:4.4.2-19.b1.el9.x86_64                        2/2 
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64                        2/2 
  Verifying        : dhcp-common-12:4.4.2-19.b1.el9.noarch                        1/2 
  Verifying        : dhcp-server-12:4.4.2-19.b1.el9.x86_64                        2/2 

Installed:
  dhcp-common-12:4.4.2-19.b1.el9.noarch     dhcp-server-12:4.4.2-19.b1.el9.x86_64    

Complete!
```
> 2. Chỉnh sửa file cấu hình DHCP Server
```shell
cp /usr/share/doc/dhcp*/dhcpd.conf.example /etc/dhcp/dhcpd.conf
vi /etc/dhcp/dhcpd.conf
```
