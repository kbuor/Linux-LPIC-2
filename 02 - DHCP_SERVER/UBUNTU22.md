## THÔNG TIN CHUNG
---
Operating System: `Ubuntu 22.04.4 LTS (Jammy)`

IP Address: `20.20.20.102/24`

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
> 1. Cài đặt gói `isc-dhcp-server`
```shell
sudo apt install isc-dhcp-server
```
```shell
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libirs-export161 libisccfg-export163
Suggested packages:
  isc-dhcp-server-ldap policycoreutils
The following NEW packages will be installed:
  isc-dhcp-server libirs-export161 libisccfg-export163
0 upgraded, 3 newly installed, 0 to remove and 4 not upgraded.
Need to get 529 kB of archives.
After this operation, 1,546 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 libisccfg-export163 amd64 1:9.11.19+dfsg-2.1ubuntu3 [53.0 kB]
Get:2 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 libirs-export161 amd64 1:9.11.19+dfsg-2.1ubuntu3 [20.0 kB]
Get:3 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 isc-dhcp-server amd64 4.4.1-2.3ubuntu2.4 [456 kB]
Fetched 529 kB in 0s (9,022 kB/s)    
Preconfiguring packages ...
Selecting previously unselected package libisccfg-export163.
(Reading database ... 74574 files and directories currently installed.)
Preparing to unpack .../libisccfg-export163_1%3a9.11.19+dfsg-2.1ubuntu3_amd64.deb ...
Unpacking libisccfg-export163 (1:9.11.19+dfsg-2.1ubuntu3) ...
Selecting previously unselected package libirs-export161.
Preparing to unpack .../libirs-export161_1%3a9.11.19+dfsg-2.1ubuntu3_amd64.deb ...
Unpacking libirs-export161 (1:9.11.19+dfsg-2.1ubuntu3) ...
Selecting previously unselected package isc-dhcp-server.
Preparing to unpack .../isc-dhcp-server_4.4.1-2.3ubuntu2.4_amd64.deb ...
Unpacking isc-dhcp-server (4.4.1-2.3ubuntu2.4) ...
Setting up libisccfg-export163 (1:9.11.19+dfsg-2.1ubuntu3) ...
Setting up libirs-export161 (1:9.11.19+dfsg-2.1ubuntu3) ...
Setting up isc-dhcp-server (4.4.1-2.3ubuntu2.4) ...
Generating /etc/default/isc-dhcp-server...
Created symlink /etc/systemd/system/multi-user.target.wants/isc-dhcp-server.service → /lib/systemd/system/isc-dhcp-server.service.
Created symlink /etc/systemd/system/multi-user.target.wants/isc-dhcp-server6.service → /lib/systemd/system/isc-dhcp-server6.service.
Processing triggers for libc-bin (2.35-0ubuntu3.8) ...
Processing triggers for man-db (2.10.2-1) ...
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
> 2. Sửa file `/etc/default/isc-dhcp-server` để xác định configure IPv4 và Interface sẽ sử dụng
```shell
sudo nano /etc/default/isc-dhcp-server
```
