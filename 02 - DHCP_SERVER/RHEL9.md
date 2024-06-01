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
vi /etc/dhcp/dhcpd.conf
```
> Xóa hết nội dung mẫu trong file, thay thế bằng nội dung bên dưới

> Khai báo domain name và thời gian thuê IP từ DHCP Server
```shell
option domain-name "kbuor.io.local";
option domain-name-servers 10.10.10.101;

default-lease-time 600;
max-lease-time 7200;
```
> Khai báo địa chỉ ghi DHCP log

```shell
log-facility local7;
```
> Tạo pool DHCP
```shell
subnet 10.10.10.0 netmask 255.255.255.0 {
  range 10.10.10.103 10.10.10.199;
  option domain-name-servers 10.10.10.101;
  option domain-name "kbuor.io.local";
  option routers 10.10.10.10;
  option broadcast-address 10.10.10.255;
  default-lease-time 600;
}
```
> File cấu hình hoàn chỉnh
```shell
option domain-name "kbuor.io.local";
option domain-name-servers 10.10.10.101;

default-lease-time 600;
max-lease-time 7200;

log-facility local7;

subnet 10.10.10.0 netmask 255.255.255.0 {
  range 10.10.10.103 10.10.10.199;
  option domain-name-servers 10.10.10.101;
  option domain-name "kbuor.io.local";
  option routers 10.10.10.10;
  option broadcast-address 10.10.10.255;
  default-lease-time 600;
}
```
> 3. Start dịch vụ DHCP Server
```shell
systemctl start dhcpd
systemctl enable dhcpd
systemctl status dhcpd
```
```shell
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: active (running) since Sun 2024-06-02 02:53:38 +07; 5s ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 4509 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 11108)
     Memory: 5.2M
        CPU: 11ms
     CGroup: /system.slice/dhcpd.service
             └─4509 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dh>

Jun 02 02:53:38 dhcp.kbuor.io.local dhcpd[4509]: Copyright 2004-2019 Internet Systems>
Jun 02 02:53:38 dhcp.kbuor.io.local dhcpd[4509]: All rights reserved.
Jun 02 02:53:38 dhcp.kbuor.io.local dhcpd[4509]: For info, please visit https://www.i>
Jun 02 02:53:38 dhcp.kbuor.io.local dhcpd[4509]: Source compiled to use binary-leases
Jun 02 02:53:38 dhcp.kbuor.io.local dhcpd[4509]: Wrote 0 leases to leases file.
Jun 02 02:53:38 dhcp.kbuor.io.local dhcpd[4509]: Listening on LPF/ens33/00:50:56:01:0>
Jun 02 02:53:38 dhcp.kbuor.io.local dhcpd[4509]: Sending on   LPF/ens33/00:50:56:01:0>
Jun 02 02:53:38 dhcp.kbuor.io.local dhcpd[4509]: Sending on   Socket/fallback/fallbac>
Jun 02 02:53:38 dhcp.kbuor.io.local dhcpd[4509]: Server starting service.
Jun 02 02:53:38 dhcp.kbuor.io.local systemd[1]: Started DHCPv4 Server Daemon.
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
  fixed-address 10.10.10.101;
}
```
> File sau khi chỉnh sửa

```shell
option domain-name "kbuor.io.local";
option domain-name-servers 10.10.10.101;

default-lease-time 600;
max-lease-time 7200;

log-facility local7;

subnet 10.10.10.0 netmask 255.255.255.0 {
  range 10.10.10.103 10.10.10.199;
  option domain-name-servers 10.10.10.101;
  option domain-name "kbuor.io.local";
  option routers 10.10.10.10;
  option broadcast-address 10.10.10.255;
  default-lease-time 600;
}

host dns {
  hardware ethernet 00:50:56:01:00:be;
  fixed-address 10.10.10.101;
}
```
> Restart dịch vụ DHCP
```shell
systemctl restart dhcpd
```

> Kiểm tra DHCP log
```shell
cat /var/log/boot.log | grep dhcp
```
```shell
Jun  2 02:53:38 dhcp dhcpd[4509]: Internet Systems Consortium DHCP Server 4.4.2b1
Jun  2 02:53:38 dhcp dhcpd[4509]: Copyright 2004-2019 Internet Systems Consortium.
Jun  2 02:53:38 dhcp dhcpd[4509]: All rights reserved.
Jun  2 02:53:38 dhcp dhcpd[4509]: For info, please visit https://www.isc.org/software/dhcp/
Jun  2 02:53:38 dhcp dhcpd[4509]: Source compiled to use binary-leases
Jun  2 02:53:38 dhcp dhcpd[4509]: Wrote 0 leases to leases file.
Jun  2 02:53:38 dhcp dhcpd[4509]: Listening on LPF/ens33/00:50:56:01:00:c0/10.10.10.0/24
Jun  2 02:53:38 dhcp dhcpd[4509]: Sending on   LPF/ens33/00:50:56:01:00:c0/10.10.10.0/24
Jun  2 02:53:38 dhcp dhcpd[4509]: Sending on   Socket/fallback/fallback-net
Jun  2 02:53:38 dhcp dhcpd[4509]: Server starting service.
```
