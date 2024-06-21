## THÔNG TIN CHUNG
---
Operating System: `AlmaLinux 9.4 (Seafoam Ocelot) (platform:el9)`

IP Address: `10.10.10.105/24`

Gateway: `10.10.10.10`

Hostname: `proxy.kbuor.io.local`

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
> Cài đặt gói `squid`
```shell
dnf install -y squid
```
```shell
Last metadata expiration check: 0:02:27 ago on Fri Jun 21 23:38:41 2024.
Dependencies resolved.
==========================================================================================================================================================================================================
 Package                                              Architecture                              Version                                                Repository                                    Size
==========================================================================================================================================================================================================
Installing:
 squid                                                x86_64                                    7:5.5-12.el9_4                                         appstream                                    3.4 M
Installing dependencies:
 httpd-filesystem                                     noarch                                    2.4.57-8.el9                                           appstream                                     12 k
 libecap                                              x86_64                                    1.0.1-10.el9                                           appstream                                     25 k
 perl-DBI                                             x86_64                                    1.643-9.el9                                            appstream                                    700 k
 perl-Digest-SHA                                      x86_64                                    1:6.02-461.el9                                         appstream                                     61 k
 perl-English                                         noarch                                    1.11-481.el9                                           appstream                                     12 k
 perl-Math-BigInt                                     noarch                                    1:1.9998.18-460.el9                                    appstream                                    188 k
 perl-Math-Complex                                    noarch                                    1.59-481.el9                                           appstream                                     45 k

Transaction Summary
==========================================================================================================================================================================================================
Install  8 Packages

Total download size: 4.5 M
Installed size: 14 M
Downloading Packages:
(1/8): libecap-1.0.1-10.el9.x86_64.rpm                                                                                                                                    1.5 MB/s |  25 kB     00:00    
(2/8): httpd-filesystem-2.4.57-8.el9.noarch.rpm                                                                                                                           481 kB/s |  12 kB     00:00    
(3/8): perl-Digest-SHA-6.02-461.el9.x86_64.rpm                                                                                                                            2.3 MB/s |  61 kB     00:00    
(4/8): perl-English-1.11-481.el9.noarch.rpm                                                                                                                               410 kB/s |  12 kB     00:00    
(5/8): perl-Math-BigInt-1.9998.18-460.el9.noarch.rpm                                                                                                                      5.7 MB/s | 188 kB     00:00    
(6/8): perl-Math-Complex-1.59-481.el9.noarch.rpm                                                                                                                          1.3 MB/s |  45 kB     00:00    
(7/8): perl-DBI-1.643-9.el9.x86_64.rpm                                                                                                                                    6.4 MB/s | 700 kB     00:00    
(8/8): squid-5.5-12.el9_4.x86_64.rpm                                                                                                                                      9.1 MB/s | 3.4 MB     00:00    
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                     3.4 MB/s | 4.5 MB     00:01     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Running scriptlet: squid-7:5.5-12.el9_4.x86_64                                                                                                                                                      1/1 
  Preparing        :                                                                                                                                                                                  1/1 
  Installing       : perl-Math-Complex-1.59-481.el9.noarch                                                                                                                                            1/8 
  Installing       : perl-Math-BigInt-1:1.9998.18-460.el9.noarch                                                                                                                                      2/8 
  Installing       : perl-DBI-1.643-9.el9.x86_64                                                                                                                                                      3/8 
  Installing       : perl-English-1.11-481.el9.noarch                                                                                                                                                 4/8 
  Installing       : perl-Digest-SHA-1:6.02-461.el9.x86_64                                                                                                                                            5/8 
  Installing       : libecap-1.0.1-10.el9.x86_64                                                                                                                                                      6/8 
  Running scriptlet: httpd-filesystem-2.4.57-8.el9.noarch                                                                                                                                             7/8 
  Installing       : httpd-filesystem-2.4.57-8.el9.noarch                                                                                                                                             7/8 
  Running scriptlet: squid-7:5.5-12.el9_4.x86_64                                                                                                                                                      8/8 
  Installing       : squid-7:5.5-12.el9_4.x86_64                                                                                                                                                      8/8 
  Running scriptlet: squid-7:5.5-12.el9_4.x86_64                                                                                                                                                      8/8 
  Verifying        : httpd-filesystem-2.4.57-8.el9.noarch                                                                                                                                             1/8 
  Verifying        : libecap-1.0.1-10.el9.x86_64                                                                                                                                                      2/8 
  Verifying        : perl-DBI-1.643-9.el9.x86_64                                                                                                                                                      3/8 
  Verifying        : perl-Digest-SHA-1:6.02-461.el9.x86_64                                                                                                                                            4/8 
  Verifying        : perl-English-1.11-481.el9.noarch                                                                                                                                                 5/8 
  Verifying        : perl-Math-BigInt-1:1.9998.18-460.el9.noarch                                                                                                                                      6/8 
  Verifying        : perl-Math-Complex-1.59-481.el9.noarch                                                                                                                                            7/8 
  Verifying        : squid-7:5.5-12.el9_4.x86_64                                                                                                                                                      8/8 

Installed:
  httpd-filesystem-2.4.57-8.el9.noarch            libecap-1.0.1-10.el9.x86_64               perl-DBI-1.643-9.el9.x86_64     perl-Digest-SHA-1:6.02-461.el9.x86_64     perl-English-1.11-481.el9.noarch    
  perl-Math-BigInt-1:1.9998.18-460.el9.noarch     perl-Math-Complex-1.59-481.el9.noarch     squid-7:5.5-12.el9_4.x86_64    

Complete!
```
---
> Cấu hình Proxy Server: `/etc/squid/squid.conf`

> Giới hạn host truy cập Internet
```shell
acl robusta-deny-01 src 10.10.10.101-10.10.10.110
...
...
http_access deny robusta-deny-01
```
> Cấm truy cập website
```shell
acl robusta-deny-02 src 10.10.10.111-10.10.10.119
acl deny_web dstdomain "/etc/squid/denyweb"
...
...
http_access deny robusta-deny-02 deny_web
```
> Chỉ cho truy cập 1 số trang web
```shell
acl robusta-deny-03 src 10.10.10.120-10.10.10.129
acl allowweb dstdomain "/etc/squid/allowweb"
...
...
http_access allow robusta-deny-03 allowweb
http_access deny robusta-deny-03
```
> Giới hạn giờ truy cập
```shell
acl sang time MTWHF 8:00-12:00
acl chieu time MTWHF 13:00-17:00
acl dayip4 src 10.10.10.130-10.10.10.139
acl webtronggio dstdomain "/etc/squid/webtronggio"
http_access allow robusta-deny-04 webtronggio sang
http_access allow robusta-deny-04 webtronggio chieu
http_access allow robusta-deny-04 !sang !chieu
http_access deny robusta-deny-04
```
---
> Chứng thực user truy cập

> Cài đặt gói `httpd-tools`
```shell
dnf -y install httpd-tools
```
```shell
Last metadata expiration check: 0:27:37 ago on Fri Jun 21 23:38:41 2024.
Dependencies resolved.
==========================================================================================================================================================================================================
 Package                                              Architecture                               Version                                              Repository                                     Size
==========================================================================================================================================================================================================
Installing:
 httpd-tools                                          x86_64                                     2.4.57-8.el9                                         appstream                                      80 k
Installing dependencies:
 apr                                                  x86_64                                     1.7.0-12.el9_3                                       appstream                                     122 k
 apr-util                                             x86_64                                     1.6.1-23.el9                                         appstream                                      94 k
 apr-util-bdb                                         x86_64                                     1.6.1-23.el9                                         appstream                                      12 k
Installing weak dependencies:
 apr-util-openssl                                     x86_64                                     1.6.1-23.el9                                         appstream                                      14 k

Transaction Summary
==========================================================================================================================================================================================================
Install  5 Packages

Total download size: 322 k
Installed size: 736 k
Downloading Packages:
(1/5): apr-util-bdb-1.6.1-23.el9.x86_64.rpm                                                                                                                               3.3 kB/s |  12 kB     00:03    
(2/5): apr-util-1.6.1-23.el9.x86_64.rpm                                                                                                                                    26 kB/s |  94 kB     00:03    
(3/5): apr-util-openssl-1.6.1-23.el9.x86_64.rpm                                                                                                                           619 kB/s |  14 kB     00:00    
(4/5): apr-1.7.0-12.el9_3.x86_64.rpm                                                                                                                                       33 kB/s | 122 kB     00:03    
(5/5): httpd-tools-2.4.57-8.el9.x86_64.rpm                                                                                                                                2.9 MB/s |  80 kB     00:00    
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                      65 kB/s | 322 kB     00:04     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                  1/1 
  Installing       : apr-1.7.0-12.el9_3.x86_64                                                                                                                                                        1/5 
  Installing       : apr-util-bdb-1.6.1-23.el9.x86_64                                                                                                                                                 2/5 
  Installing       : apr-util-openssl-1.6.1-23.el9.x86_64                                                                                                                                             3/5 
  Installing       : apr-util-1.6.1-23.el9.x86_64                                                                                                                                                     4/5 
  Installing       : httpd-tools-2.4.57-8.el9.x86_64                                                                                                                                                  5/5 
  Running scriptlet: httpd-tools-2.4.57-8.el9.x86_64                                                                                                                                                  5/5 
  Verifying        : apr-1.7.0-12.el9_3.x86_64                                                                                                                                                        1/5 
  Verifying        : apr-util-1.6.1-23.el9.x86_64                                                                                                                                                     2/5 
  Verifying        : apr-util-bdb-1.6.1-23.el9.x86_64                                                                                                                                                 3/5 
  Verifying        : apr-util-openssl-1.6.1-23.el9.x86_64                                                                                                                                             4/5 
  Verifying        : httpd-tools-2.4.57-8.el9.x86_64                                                                                                                                                  5/5 

Installed:
  apr-1.7.0-12.el9_3.x86_64         apr-util-1.6.1-23.el9.x86_64         apr-util-bdb-1.6.1-23.el9.x86_64         apr-util-openssl-1.6.1-23.el9.x86_64         httpd-tools-2.4.57-8.el9.x86_64        

Complete!
```
