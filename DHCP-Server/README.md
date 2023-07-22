## Prepare Linux (Centos 7)
```shell
yum install -y open-vm-tools git wget unzip epel-release
yum update -y
systemctl stop firewalld
systemctl disable firewalld
sed -i "s/=enforcing/=disabled/g" /etc/sysconfig/selinux
reboot
```

## Install DHCP Server package
```shell
yum install -y dhcp
```
## Configure DHCP Server
```shell
cp /usr/share/doc/dhcp*/dhcpd.conf.example /etc/dhcp/dhcpd.conf
vi /etc/dhcp/dhcpd.conf
```
> Edit line 7: option domain-name "kbuor.local";

> Edit line 8: option domain-name-servers 8.8.8.8, 1.1.1.1;

> Edit line 10: default-lease-time 600; # Thời gian mặc định cấp IP cho một client

> Edit line 11: max-lease-time 7200; # Thời gian tối đa cấp IP cho một client, nếu client có yêu cầu về thời gian

> Edit line 22: log-facility local7; # Log DHCP, mặc định lưu vào /var/log/boot.log

> Edit line 47: subnet 10.19.0.0 netmask 255.255.255.0 { # Network dùng để cấp phát DHCP

> Edit line 48: range 10.19.0.230 10.19.0.239; # Range IP dùng để cấp phát DHCP

> Edit line 49: option domain-name-servers 8.8.8.8; # DNS Server dùng để cấp phát DHCP

> Edit line 50: option domain-name "kbuor.local"; # Domain name dùng để cấp phát DHCP

> Edit line 51: option routers 10.19.0.254; # Default Gateway dùng để cấp phát DHCP

> Edit line 52: option broadcast-address 10.19.0.255;

> Edit line 53: default-lease-time 600; # Thời gian mặc định cấp IP cho một client

> Edit line 54: max-lease-time 7200; # Thời gian tối đa cấp IP cho một client, nếu client có yêu cầu về thời gian

## Start DHCP Service
```shell
systemctl start dhcpd
systemctl enable dhcpd
```

## Monitor DHCP leasing
```shell
cat /var/lib/dhcpd/dhcpd.leases
```

## Monitor DHCP log
```shell
cat /var/log/boot.log | grep dhcp
```

## Assign IP to specify client
```shell
vi /etc/dhcp/dhcpd.conf
```

> Edit line 75: host lasuno {

> Edit line 76: hardware ethernet 08:00:07:26:c0:a5;

> Edit line 77: fixed-address 10.19.0.236;

```shell
systemctl restart dhcpd
```
