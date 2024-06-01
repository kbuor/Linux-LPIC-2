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
