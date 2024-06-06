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
> Uncommend dòng `DHCPDv4_CONF=/etc/dhcp/dhcpd.conf`
> Thêm interface vào dòng `INTERFACESv4=""`
> File hoàn chỉnh sau khi chỉnh sửa:
```shell
# Defaults for isc-dhcp-server (sourced by /etc/init.d/isc-dhcp-server)

# Path to dhcpd's config file (default: /etc/dhcp/dhcpd.conf).
DHCPDv4_CONF=/etc/dhcp/dhcpd.conf
#DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf

# Path to dhcpd's PID file (default: /var/run/dhcpd.pid).
#DHCPDv4_PID=/var/run/dhcpd.pid
#DHCPDv6_PID=/var/run/dhcpd6.pid

# Additional options to start dhcpd with.
#       Don't use options -cf or -pf here; use DHCPD_CONF/ DHCPD_PID instead
#OPTIONS=""

# On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
#       Separate multiple interfaces with spaces, e.g. "eth0 eth1".
INTERFACESv4="ens33"
INTERFACESv6=""
```
> 3. Chỉnh sửa file cấu hình DHCP Server
```shell
sudo nano /etc/dhcp/dhcpd.conf
```
> Xóa hết nội dung mẫu trong file, thay thế bằng nội dung bên dưới

> Khai báo domain name và thời gian thuê IP từ DHCP Server
```shell
option domain-name "kbuor.io.local";
option domain-name-servers 20.20.20.201;

default-lease-time 600;
max-lease-time 7200;
```
> Khai báo địa chỉ ghi DHCP log

```shell
log-facility local7;
```
> Tạo pool DHCP
```shell
subnet 20.20.20.0 netmask 255.255.255.0 {
  range 20.20.20.103 20.20.20.199;
  option domain-name-servers 20.20.20.101;
  option domain-name "kbuor.io.local";
  option routers 20.20.20.20;
  option broadcast-address 20.20.20.255;
  default-lease-time 600;
}
```
> File cấu hình hoàn chỉnh
```shell
option domain-name "kbuor.io.local";
option domain-name-servers 20.20.20.101;

default-lease-time 600;
max-lease-time 7200;

log-facility local7;

subnet 20.20.20.0 netmask 255.255.255.0 {
  range 20.20.20.103 20.20.20.199;
  option domain-name-servers 20.20.20.101;
  option domain-name "kbuor.io.local";
  option routers 20.20.20.20;
  option broadcast-address 20.20.20.255;
  default-lease-time 600;
}
```
> 4. Start dịch vụ DHCP Server
```shell
systemctl start isc-dhcp-server
systemctl enable isc-dhcp-server
systemctl status isc-dhcp-server
```
```shell
● isc-dhcp-server.service - ISC DHCP IPv4 server
     Loaded: loaded (/lib/systemd/system/isc-dhcp-server.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2024-06-06 03:42:56 UTC; 8s ago
       Docs: man:dhcpd(8)
   Main PID: 22500 (dhcpd)
      Tasks: 4 (limit: 2219)
     Memory: 4.5M
        CPU: 10ms
     CGroup: /system.slice/isc-dhcp-server.service
             └─22500 dhcpd -user dhcpd -group dhcpd -f -4 -pf /run/dhcp-server/dhcpd.pid -cf /etc/dhcp/dhcpd.conf ens33

Jun 06 03:42:56 dhcp dhcpd[22500]: For info, please visit https://www.isc.org/software/dhcp/
Jun 06 03:42:56 dhcp dhcpd[22500]: Wrote 0 leases to leases file.
Jun 06 03:42:56 dhcp sh[22500]: Wrote 0 leases to leases file.
Jun 06 03:42:56 dhcp dhcpd[22500]: Listening on LPF/ens33/00:50:56:01:00:c1/20.20.20.0/24
Jun 06 03:42:56 dhcp sh[22500]: Listening on LPF/ens33/00:50:56:01:00:c1/20.20.20.0/24
Jun 06 03:42:56 dhcp dhcpd[22500]: Sending on   LPF/ens33/00:50:56:01:00:c1/20.20.20.0/24
Jun 06 03:42:56 dhcp sh[22500]: Sending on   LPF/ens33/00:50:56:01:00:c1/20.20.20.0/24
Jun 06 03:42:56 dhcp dhcpd[22500]: Sending on   Socket/fallback/fallback-net
Jun 06 03:42:56 dhcp sh[22500]: Sending on   Socket/fallback/fallback-net
Jun 06 03:42:56 dhcp dhcpd[22500]: Server starting service.
```
## CÁC TÁC VỤ THƯỜNG DÙNG
---
> 1. Assign IP cố định cho một host cụ thể

> Chỉnh sửa file cấu hình DHCP Server
```shell
vi /etc/dhcp/dhcpd.conf
```
> Thêm block `host` vào file
```shell
host dns {
  hardware ethernet 00:50:56:01:00:be;
  fixed-address 20.20.20.101;
}
```
> File sau khi chỉnh sửa

```shell
option domain-name "kbuor.io.local";
option domain-name-servers 20.20.20.101;

default-lease-time 600;
max-lease-time 7200;

log-facility local7;

subnet 20.20.20.0 netmask 255.255.255.0 {
  range 20.20.20.103 20.20.20.199;
  option domain-name-servers 20.20.20.101;
  option domain-name "kbuor.io.local";
  option routers 20.20.20.20;
  option broadcast-address 20.20.20.255;
  default-lease-time 600;
}

host dns {
  hardware ethernet 00:50:56:01:00:be;
  fixed-address 20.20.20.101;
}
```
> Restart dịch vụ DHCP
```shell
systemctl restart dhcpd
```

> 2. Kiểm tra DHCP log
```shell
cat /var/log/boot.log | grep dhcp
```
