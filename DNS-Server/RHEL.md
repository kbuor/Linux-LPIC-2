> 1. Cài đặt gói `bind` và `bind-utils`
```shell
yum install bind bind-utils -y
```

```shell
Last metadata expiration check: 0:26:26 ago on Sat Jun  1 08:42:37 2024.
Package bind-utils-32:9.16.23-18.el9_4.1.x86_64 is already installed.
Dependencies resolved.
===========================================================================================================
 Package                              Architecture   Version                       Repository         Size
===========================================================================================================
Installing:
 bind                                 x86_64         32:9.16.23-18.el9_4.1         appstream         488 k
Installing dependencies:
 bind-dnssec-doc                      noarch         32:9.16.23-18.el9_4.1         appstream          45 k
 checkpolicy                          x86_64         3.6-1.el9                     appstream         351 k
 policycoreutils-python-utils         noarch         3.6-2.1.el9                   appstream          71 k
 python3-audit                        x86_64         3.1.2-2.el9                   appstream          82 k
 python3-bind                         noarch         32:9.16.23-18.el9_4.1         appstream          60 k
 python3-distro                       noarch         1.5.0-7.el9                   appstream          36 k
 python3-libsemanage                  x86_64         3.6-1.el9                     appstream          78 k
 python3-ply                          noarch         3.11-14.el9                   baseos            103 k
 python3-policycoreutils              noarch         3.6-2.1.el9                   appstream         2.0 M
 python3-setools                      x86_64         4.4.4-1.el9                   baseos            551 k
 python3-setuptools                   noarch         53.0.0-12.el9                 baseos            839 k
Installing weak dependencies:
 bind-dnssec-utils                    x86_64         32:9.16.23-18.el9_4.1         appstream         114 k

Transaction Summary
===========================================================================================================
Install  13 Packages

Total download size: 4.8 M
Installed size: 17 M
Downloading Packages:
(1/13): bind-dnssec-doc-9.16.23-18.el9_4.1.noarch.rpm                      1.0 MB/s |  45 kB     00:00    
(2/13): bind-dnssec-utils-9.16.23-18.el9_4.1.x86_64.rpm                    2.2 MB/s | 114 kB     00:00    
(3/13): checkpolicy-3.6-1.el9.x86_64.rpm                                    13 MB/s | 351 kB     00:00    
(4/13): policycoreutils-python-utils-3.6-2.1.el9.noarch.rpm                2.7 MB/s |  71 kB     00:00    
(5/13): python3-audit-3.1.2-2.el9.x86_64.rpm                               6.0 MB/s |  82 kB     00:00    
(6/13): python3-bind-9.16.23-18.el9_4.1.noarch.rpm                         4.4 MB/s |  60 kB     00:00    
(7/13): python3-distro-1.5.0-7.el9.noarch.rpm                              4.4 MB/s |  36 kB     00:00    
(8/13): bind-9.16.23-18.el9_4.1.x86_64.rpm                                 4.6 MB/s | 488 kB     00:00    
(9/13): python3-libsemanage-3.6-1.el9.x86_64.rpm                           4.1 MB/s |  78 kB     00:00    
(10/13): python3-ply-3.11-14.el9.noarch.rpm                                8.8 MB/s | 103 kB     00:00    
(11/13): python3-setuptools-53.0.0-12.el9.noarch.rpm                        12 MB/s | 839 kB     00:00    
(12/13): python3-setools-4.4.4-1.el9.x86_64.rpm                            4.6 MB/s | 551 kB     00:00    
(13/13): python3-policycoreutils-3.6-2.1.el9.noarch.rpm                    9.9 MB/s | 2.0 MB     00:00    
-----------------------------------------------------------------------------------------------------------
Total                                                                      2.3 MB/s | 4.8 MB     00:02     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                   1/1 
  Installing       : python3-setuptools-53.0.0-12.el9.noarch                                          1/13 
  Installing       : python3-distro-1.5.0-7.el9.noarch                                                2/13 
  Installing       : python3-setools-4.4.4-1.el9.x86_64                                               3/13 
  Installing       : python3-ply-3.11-14.el9.noarch                                                   4/13 
  Installing       : python3-bind-32:9.16.23-18.el9_4.1.noarch                                        5/13 
  Installing       : python3-libsemanage-3.6-1.el9.x86_64                                             6/13 
  Installing       : python3-audit-3.1.2-2.el9.x86_64                                                 7/13 
  Installing       : checkpolicy-3.6-1.el9.x86_64                                                     8/13 
  Installing       : python3-policycoreutils-3.6-2.1.el9.noarch                                       9/13 
  Installing       : policycoreutils-python-utils-3.6-2.1.el9.noarch                                 10/13 
  Installing       : bind-dnssec-doc-32:9.16.23-18.el9_4.1.noarch                                    11/13 
  Installing       : bind-dnssec-utils-32:9.16.23-18.el9_4.1.x86_64                                  12/13 
  Running scriptlet: bind-32:9.16.23-18.el9_4.1.x86_64                                               13/13 
  Installing       : bind-32:9.16.23-18.el9_4.1.x86_64                                               13/13 
  Running scriptlet: bind-32:9.16.23-18.el9_4.1.x86_64                                               13/13 
  Verifying        : bind-32:9.16.23-18.el9_4.1.x86_64                                                1/13 
  Verifying        : bind-dnssec-doc-32:9.16.23-18.el9_4.1.noarch                                     2/13 
  Verifying        : bind-dnssec-utils-32:9.16.23-18.el9_4.1.x86_64                                   3/13 
  Verifying        : checkpolicy-3.6-1.el9.x86_64                                                     4/13 
  Verifying        : policycoreutils-python-utils-3.6-2.1.el9.noarch                                  5/13 
  Verifying        : python3-audit-3.1.2-2.el9.x86_64                                                 6/13 
  Verifying        : python3-bind-32:9.16.23-18.el9_4.1.noarch                                        7/13 
  Verifying        : python3-distro-1.5.0-7.el9.noarch                                                8/13 
  Verifying        : python3-libsemanage-3.6-1.el9.x86_64                                             9/13 
  Verifying        : python3-policycoreutils-3.6-2.1.el9.noarch                                      10/13 
  Verifying        : python3-ply-3.11-14.el9.noarch                                                  11/13 
  Verifying        : python3-setools-4.4.4-1.el9.x86_64                                              12/13 
  Verifying        : python3-setuptools-53.0.0-12.el9.noarch                                         13/13 

Installed:
  bind-32:9.16.23-18.el9_4.1.x86_64                     bind-dnssec-doc-32:9.16.23-18.el9_4.1.noarch      
  bind-dnssec-utils-32:9.16.23-18.el9_4.1.x86_64        checkpolicy-3.6-1.el9.x86_64                      
  policycoreutils-python-utils-3.6-2.1.el9.noarch       python3-audit-3.1.2-2.el9.x86_64                  
  python3-bind-32:9.16.23-18.el9_4.1.noarch             python3-distro-1.5.0-7.el9.noarch                 
  python3-libsemanage-3.6-1.el9.x86_64                  python3-ply-3.11-14.el9.noarch                    
  python3-policycoreutils-3.6-2.1.el9.noarch            python3-setools-4.4.4-1.el9.x86_64                
  python3-setuptools-53.0.0-12.el9.noarch              

Complete!
```

> 2. Đặt hostname

```shell
hostnamectl set-hostname dns.kbuor.io.local
```

> 3. Sửa file `/etc/named.conf`

```shell
vi /etc/named.conf
```
> Sửa các dòng sau:

```shell
listen-on port 53 { 127.0.0.1; 10.10.10.101; };
```
```shell
allow-query     { localhost; 10.10.10.0/24; };
```

> Thêm vào file để khai báo các DNS Zone:

```shell
zone "kbuor.io.local" IN {
        type master;
        file "forward.kbuor.io.local";
        allow-update { none; };
};

zone "10.10.10.in-addr.arpa" IN {
        type master;
        file "reverse.kbuor.io.local";
        allow-update { none; };
};
```

> Nội dung hoàn chỉnh

```shell
//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//

options {
        listen-on port 53 { 127.0.0.1; 10.10.10.101; };
        listen-on-v6 port 53 { ::1; };
        directory       "/var/named";
        dump-file       "/var/named/data/cache_dump.db";
        statistics-file "/var/named/data/named_stats.txt";
        memstatistics-file "/var/named/data/named_mem_stats.txt";
        secroots-file   "/var/named/data/named.secroots";
        recursing-file  "/var/named/data/named.recursing";
        allow-query     { localhost; 10.10.10.0/24; };

        /* 
         - If you are building an AUTHORITATIVE DNS server, do NOT enable recursion.
         - If you are building a RECURSIVE (caching) DNS server, you need to enable 
           recursion. 
         - If your recursive DNS server has a public IP address, you MUST enable access 
           control to limit queries to your legitimate users. Failing to do so will
           cause your server to become part of large scale DNS amplification 
           attacks. Implementing BCP38 within your network would greatly
           reduce such attack surface 
        */
        recursion yes;

        dnssec-validation yes;

        managed-keys-directory "/var/named/dynamic";
        geoip-directory "/usr/share/GeoIP";

        pid-file "/run/named/named.pid";
        session-keyfile "/run/named/session.key";

        /* https://fedoraproject.org/wiki/Changes/CryptoPolicy */
        include "/etc/crypto-policies/back-ends/bind.config";
};

logging {
        channel default_debug {
                file "data/named.run";
                severity dynamic;
        };
};

zone "." IN {
        type hint;
        file "named.ca";
};


zone "kbuor.io.local" IN {
        type master;
        file "forward.kbuor.io.local";
        allow-update { none; };
};

zone "10.10.10.in-addr.arpa" IN {
        type master;
        file "reverse.kbuor.io.local";
        allow-update { none; };
};

include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";
```

> 4. Thêm vào nội dung file `forward zone`
```shell
touch /var/named/forward.kbuor.io.local
vi /var/named/forward.kbuor.io.local
```
```shell
$TTL 86400

@       IN      SOA     kbuor.io.local. root.kbuor.io.local. (
                        2024060101      ; Serial
                        3600            ; Refresh
                        1800            ; Retry
                        604800          ; Expire
                        86400           ; Minimun TTL
                        )

@       IN      NS      dns.kbuor.io.local.

dns     IN      A       10.10.10.101
```
> 5. Thêm vào nội dung file `reverse zone`
```shell
touch /var/named/reverse.kbuor.io.local
vi /var/named/reverse.kbuor.io.local
```
```shell
$TTL 86400

@       IN      SOA     kbuor.io.local. root.kbuor.io.local. (
                        2024060101      ; Serial
                        3600            ; Refresh
                        1800            ; Retry
                        604800          ; Expire
                        86400           ; Minimun TTL
                        )

@       IN      NS      dns.kbuor.io.local.

101     IN      PTR     dns.kbuor.io.local.
```
> 6. Chuyển quyền cho các file configure
```shell
chgrp named -R /var/named
chown -v root:named /etc/named.conf
```
```shell
ownership of '/etc/named.conf' retained as root:named
```
> 7. Cấu hình SELINUX (nếu có bật SELINUX)
```shell
restorecon -rv /var/named
restorecon /etc/named.conf
```
> 8. Khởi động dịch vụ
```shell
systemctl start named
systemctl enable named
```
```shell
● named.service - Berkeley Internet Name Domain (DNS)
     Loaded: loaded (/usr/lib/systemd/system/named.service; disabled; preset: disabled)
     Active: active (running) since Sat 2024-06-01 09:52:59 EDT; 3s ago
    Process: 5216 ExecStartPre=/bin/bash -c if [ ! "$DISABLE_ZONE_CHECKING" == "yes" ]; then /usr/sb>
    Process: 5218 ExecStart=/usr/sbin/named -u named -c ${NAMEDCONF} $OPTIONS (code=exited, status=0>
   Main PID: 5219 (named)
      Tasks: 5 (limit: 11108)
     Memory: 17.8M
        CPU: 63ms
     CGroup: /system.slice/named.service
             └─5219 /usr/sbin/named -u named -c /etc/named.conf

Jun 01 09:52:59 dns.kbuor.io.local named[5219]: zone kbuor.io.local/IN: loaded serial 2024060101
Jun 01 09:52:59 dns.kbuor.io.local named[5219]: zone localhost/IN: loaded serial 0
Jun 01 09:52:59 dns.kbuor.io.local named[5219]: all zones loaded
Jun 01 09:52:59 dns.kbuor.io.local systemd[1]: Started Berkeley Internet Name Domain (DNS).
Jun 01 09:52:59 dns.kbuor.io.local named[5219]: running
Jun 01 09:52:59 dns.kbuor.io.local named[5219]: zone kbuor.io.local/IN: sending notifies (serial 202>
Jun 01 09:53:00 dns.kbuor.io.local named[5219]: network unreachable resolving './DNSKEY/IN': 2001:7f>
Jun 01 09:53:00 dns.kbuor.io.local named[5219]: network unreachable resolving './DNSKEY/IN': 2001:50>
Jun 01 09:53:00 dns.kbuor.io.local named[5219]: managed-keys-zone: Initializing automatic trust anch>
Jun 01 09:53:00 dns.kbuor.io.local named[5219]: resolver priming query complete
```
