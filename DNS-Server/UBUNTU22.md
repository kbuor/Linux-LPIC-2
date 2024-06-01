## THÔNG TIN CHUNG
---
Operating System: `Ubuntu 22.04.4 LTS (Jammy)`

IP Address: `20.20.20.101/24`

Gateway: `20.20.20.20`

Hostname: `dns.kbuor.io.local`

Domain: `kbuor.io.local`

## CHUẨN BỊ
---
> Update repository
```shell
apt update -y && apt upgrade -y
```

## TRIỂN KHAI
---
> 1. Cài đặt gói `bind9` , `bind9utils` và `bind9-doc`
```shell
sudo apt install bind9 bind9utils bind9-doc
```
```shell
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  bind9-utils dns-root-data
Suggested packages:
  bind-doc resolvconf
The following NEW packages will be installed:
  bind9 bind9-doc bind9-utils bind9utils dns-root-data
0 upgraded, 5 newly installed, 0 to remove and 2 not upgraded.
Need to get 3,629 kB of archives.
After this operation, 9,150 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 bind9-utils amd64 1:9.18.18-0ubuntu0.22.04.2 [161 kB]
Get:2 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 dns-root-data all 2023112702~ubuntu0.22.04.1 [5,136 B]
Get:3 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 bind9 amd64 1:9.18.18-0ubuntu0.22.04.2 [260 kB]
Get:4 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 bind9-doc all 1:9.18.18-0ubuntu0.22.04.2 [3,198 kB]
Get:5 http://vn.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 bind9utils all 1:9.18.18-0ubuntu0.22.04.2 [3,924 B]
Fetched 3,629 kB in 1s (3,283 kB/s)
Selecting previously unselected package bind9-utils.
(Reading database ... 74599 files and directories currently installed.)
Preparing to unpack .../bind9-utils_1%3a9.18.18-0ubuntu0.22.04.2_amd64.deb ...
Unpacking bind9-utils (1:9.18.18-0ubuntu0.22.04.2) ...
Selecting previously unselected package dns-root-data.
Preparing to unpack .../dns-root-data_2023112702~ubuntu0.22.04.1_all.deb ...
Unpacking dns-root-data (2023112702~ubuntu0.22.04.1) ...
Selecting previously unselected package bind9.
Preparing to unpack .../bind9_1%3a9.18.18-0ubuntu0.22.04.2_amd64.deb ...
Unpacking bind9 (1:9.18.18-0ubuntu0.22.04.2) ...
Selecting previously unselected package bind9-doc.
Preparing to unpack .../bind9-doc_1%3a9.18.18-0ubuntu0.22.04.2_all.deb ...
Unpacking bind9-doc (1:9.18.18-0ubuntu0.22.04.2) ...
Selecting previously unselected package bind9utils.
Preparing to unpack .../bind9utils_1%3a9.18.18-0ubuntu0.22.04.2_all.deb ...
Unpacking bind9utils (1:9.18.18-0ubuntu0.22.04.2) ...
Setting up bind9-doc (1:9.18.18-0ubuntu0.22.04.2) ...
Setting up dns-root-data (2023112702~ubuntu0.22.04.1) ...
Setting up bind9-utils (1:9.18.18-0ubuntu0.22.04.2) ...
Setting up bind9 (1:9.18.18-0ubuntu0.22.04.2) ...
Adding group `bind' (GID 119) ...
Done.
Adding system user `bind' (UID 114) ...
Adding new user `bind' (UID 114) with group `bind' ...
Not creating home directory `/var/cache/bind'.
wrote key file "/etc/bind/rndc.key"
named-resolvconf.service is a disabled or a static unit, not starting it.
Created symlink /etc/systemd/system/bind9.service → /lib/systemd/system/named.service.
Created symlink /etc/systemd/system/multi-user.target.wants/named.service → /lib/systemd/system/named.service.
Setting up bind9utils (1:9.18.18-0ubuntu0.22.04.2) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for ufw (0.36.1-4ubuntu0.1) ...
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
> 2. Sửa file `/etc/default/named` cho phép DNS Server hoạt động ở IPv4
```shell
sudo nano /etc/default/named
```
```shell
#
# run resolvconf?
RESOLVCONF=no

# startup options for the server
OPTIONS="-u bind -4"
```
> 3. Restart dịch vụ DNS
```shell
sudo systemctl restart bind9
```
> 4. Sửa file cấu hình DNS Server `/etc/bind/named.conf.options`
```shell
sudo nano /etc/bind/named.conf.options
```
> Thêm block bên dưới vào đầu file, trong đó `kbuor` là tên tùy ý của block, `20.20.20.0/24` là dải mạng được phép query đến DNS Server
```shell
acl "kbuor" {
        20.20.20.0/24; 
};
```
> Thêm nội dung bên dưới vào block `option`
```shell
recursion yes;
allow-recursion { kbuor; };    
listen-on { 20.20.20.101; };   
allow-transfer { none; };      

forwarders {
        8.8.8.8;
        1.1.1.1;
};
```
> File hoàn chỉnh sau khi chỉnh sửa
```shell
acl "kbuor" {
        20.20.20.0/24; 
};

options {
        directory "/var/cache/bind";

        recursion yes;                 
        allow-recursion { kbuor; };  
        listen-on { 20.20.20.101; };   
        allow-transfer { none; };      

        forwarders {
                8.8.8.8;
                1.1.1.1;
        };

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable 
        // nameservers, you probably want to use them as forwarders.  
        // Uncomment the following block, and insert the addresses replacing 
        // the all-0's placeholder.

        // forwarders {
        //      0.0.0.0;
        // };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        dnssec-validation auto;

        listen-on-v6 { any; };
};
```
> 5. Sửa file `/etc/bind/named.conf.local` để khai báo các zone DNS
```shell
sudo nano /etc/bind/named.conf.local
```
> Thêm forward zone cho domain `kbuor.io.local`
```shell
zone "kbuor.io.local" {
    type primary;
    file "/etc/bind/zones/db.kbuor.io.local";
};
```
> Thêm reverse zone cho subnet `20.20.20.0/24`
```shell
zone "20.20.20.in-addr.arpa" {
    type primary;
    file "/etc/bind/zones/db.20.20.20";
};
```
> File hoàn chỉnh sau khi chỉnh sửa
```shell
//
// Do any local configuration here
//

// Consider adding the 1918 zones here, if they are not used in your
// organization
//include "/etc/bind/zones.rfc1918";

zone "kbuor.io.local" {
    type primary;
    file "/etc/bind/zones/db.kbuor.io.local";
};

zone "20.20.20.in-addr.arpa" {
    type primary;
    file "/etc/bind/zones/db.20.20.20";
};
```
> 6. Tạo và thêm nội dung vào file forward zone
```shell
sudo mkdir /etc/bind/zones
sudo cp /etc/bind/db.local /etc/bind/zones/db.kbuor.io.local
sudo nano /etc/bind/zones/db.kbuor.io.local
```
> Sửa thông tin cho record `SOA`
```shell
@       IN      SOA     kbuor.io.local. root.kbuor.io.local. (
```
> Sửa thông tin cho record `NS`
```shell
@       IN      NS      dns.kbuor.io.local.
```
> Sửa thông tin cho record `A`
```shell
dns     IN      A       20.20.20.101
```
> File hoàn chỉnh sau khi chỉnh sửa
```shell
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     kbuor.oi.local. root.kbuor.io.local. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      dns.kbuor.io.local.
dns     IN      A       20.20.20.101
```
> 7. Tạo và thêm nội dung vào file reverse zone
```shell
sudo cp /etc/bind/db.127 /etc/bind/zones/db.20.20.20
sudo nano /etc/bind/zones/db.20.20.20
```
> Sửa thông tin cho record `SOA`
```shell
@       IN      SOA     kbuor.io.local. root.kbuor.io.local. (
```
> Sửa thông tin cho record `NS`
```shell
@       IN      NS      dns.kbuor.io.local.
```
> Sửa thông tin cho record `PTR`
```shell
101     IN      PTR       dns.kbuor.io.local.
```
> File hoàn chỉnh sau khi chỉnh sửa
```shell
;
; BIND reverse data file for local loopback interface
;
$TTL    604800
@       IN      SOA     kbuor.io.local. root.kbuor.io.local. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      dns.kbuor.io.local.
101     IN      PTR     dns.kbuor.io.local.
```
> 8. Kiểm tra cú pháp của các file configure
```shell
sudo named-checkconf
```
> 9. Restart dịch vụ DNS
```shell
sudo systemctl restart bind9
```
> 10. Trỏ DNS Server về `20.20.20.101`
```shell
sudo nano /etc/netplan/00-installer-config.yaml
```
```shell
# This is the network config written by 'subiquity'
network:
  ethernets:
    ens33:
      addresses:
      - 20.20.20.101/24
      nameservers:
        addresses:
        - 20.20.20.101
        search:
        - kbuor.io.local
      routes:
      - to: default
        via: 20.20.20.20
  version: 2
```
```shell
sudo nano /etc/resolv.conf
```
```shell
# This is /run/systemd/resolve/stub-resolv.conf managed by man:systemd-resolved(8).
# Do not edit.
#
# This file might be symlinked as /etc/resolv.conf. If you're looking at
# /etc/resolv.conf and seeing this text, you have followed the symlink.
#
# This is a dynamic resolv.conf file for connecting local clients to the
# internal DNS stub resolver of systemd-resolved. This file lists all
# configured search domains.
#
# Run "resolvectl status" to see details about the uplink DNS servers
# currently in use.
#
# Third party programs should typically not access this file directly, but only
# through the symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a
# different way, replace this symlink by a static file or a different symlink.
#
# See man:systemd-resolved.service(8) for details about the supported modes of
# operation for /etc/resolv.conf.

nameserver 20.20.20.101
options edns0 trust-ad
search kbuor.io.local
```

> 11. Kiểm tra dịch vụ DNS
```shell
nslookup dns.kbuor.io.local
```
```shell
Server:         20.20.20.101
Address:        20.20.20.101#53

Name:   dns.kbuor.io.local
Address: 20.20.20.101
```
```shell
nslookup 20.20.20.101
```
```shell
101.20.20.20.in-addr.arpa       name = dns.kbuor.io.local.
```
