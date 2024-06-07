## THÔNG TIN CHUNG
---
Operating System: `AlmaLinux 9.4 (Seafoam Ocelot) (platform:el9)`

IP Address: `10.10.10.104/24`

Gateway: `10.10.10.10`

Hostname: `nfs.kbuor.io.local`

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
> Cài đặt gói nfs-utils từ repository của AlmaLinux 9

```shell
dnf install -y nfs-utils
```
```shell
Last metadata expiration check: 2:22:46 ago on Thu Jun  6 20:31:04 2024.
Dependencies resolved.
==========================================================================================================================================================================================================
 Package                                             Architecture                                Version                                                Repository                                   Size
==========================================================================================================================================================================================================
Installing:
 nfs-utils                                           x86_64                                      1:2.5.4-25.el9                                         baseos                                      429 k
Installing dependencies:
 gssproxy                                            x86_64                                      0.8.4-6.el9                                            baseos                                      108 k
 keyutils                                            x86_64                                      1.6.3-1.el9                                            baseos                                       71 k
 libev                                               x86_64                                      4.33-5.el9                                             baseos                                       52 k
 libnfsidmap                                         x86_64                                      1:2.5.4-25.el9                                         baseos                                       60 k
 libverto-libev                                      x86_64                                      0.3.2-3.el9                                            baseos                                       13 k
 python3-pyyaml                                      x86_64                                      5.4.1-6.el9                                            baseos                                      190 k
 quota                                               x86_64                                      1:4.06-6.el9                                           baseos                                      190 k
 quota-nls                                           noarch                                      1:4.06-6.el9                                           baseos                                       78 k
 rpcbind                                             x86_64                                      1.2.6-7.el9                                            baseos                                       56 k
 sssd-nfs-idmap                                      x86_64                                      2.9.4-6.el9_4                                          baseos                                       43 k

Transaction Summary
==========================================================================================================================================================================================================
Install  11 Packages

Total download size: 1.3 M
Installed size: 3.7 M
Downloading Packages:
(1/11): keyutils-1.6.3-1.el9.x86_64.rpm                                                                                                                                   588 kB/s |  71 kB     00:00    
(2/11): libev-4.33-5.el9.x86_64.rpm                                                                                                                                       418 kB/s |  52 kB     00:00    
(3/11): gssproxy-0.8.4-6.el9.x86_64.rpm                                                                                                                                   844 kB/s | 108 kB     00:00    
(4/11): libverto-libev-0.3.2-3.el9.x86_64.rpm                                                                                                                             1.7 MB/s |  13 kB     00:00    
(5/11): libnfsidmap-2.5.4-25.el9.x86_64.rpm                                                                                                                               3.4 MB/s |  60 kB     00:00    
(6/11): python3-pyyaml-5.4.1-6.el9.x86_64.rpm                                                                                                                             8.8 MB/s | 190 kB     00:00    
(7/11): quota-nls-4.06-6.el9.noarch.rpm                                                                                                                                   6.1 MB/s |  78 kB     00:00    
(8/11): rpcbind-1.2.6-7.el9.x86_64.rpm                                                                                                                                    3.8 MB/s |  56 kB     00:00    
(9/11): nfs-utils-2.5.4-25.el9.x86_64.rpm                                                                                                                                 5.9 MB/s | 429 kB     00:00    
(10/11): sssd-nfs-idmap-2.9.4-6.el9_4.x86_64.rpm                                                                                                                          2.1 MB/s |  43 kB     00:00    
(11/11): quota-4.06-6.el9.x86_64.rpm                                                                                                                                      2.6 MB/s | 190 kB     00:00    
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                     1.2 MB/s | 1.3 MB     00:01     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                  1/1 
  Installing       : libnfsidmap-1:2.5.4-25.el9.x86_64                                                                                                                                               1/11 
  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                      2/11 
  Installing       : rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                      2/11 
  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                      2/11 
Created symlink /etc/systemd/system/multi-user.target.wants/rpcbind.service → /usr/lib/systemd/system/rpcbind.service.
Created symlink /etc/systemd/system/sockets.target.wants/rpcbind.socket → /usr/lib/systemd/system/rpcbind.socket.

  Installing       : quota-nls-1:4.06-6.el9.noarch                                                                                                                                                   3/11 
  Installing       : quota-1:4.06-6.el9.x86_64                                                                                                                                                       4/11 
  Installing       : python3-pyyaml-5.4.1-6.el9.x86_64                                                                                                                                               5/11 
  Installing       : libev-4.33-5.el9.x86_64                                                                                                                                                         6/11 
  Installing       : libverto-libev-0.3.2-3.el9.x86_64                                                                                                                                               7/11 
  Installing       : gssproxy-0.8.4-6.el9.x86_64                                                                                                                                                     8/11 
  Running scriptlet: gssproxy-0.8.4-6.el9.x86_64                                                                                                                                                     8/11 
  Installing       : keyutils-1.6.3-1.el9.x86_64                                                                                                                                                     9/11 
  Running scriptlet: nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                                10/11 
  Installing       : nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                                10/11 
  Running scriptlet: nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                                10/11 
  Installing       : sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                                                                                                                                            11/11 
  Running scriptlet: sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                                                                                                                                            11/11 
  Verifying        : gssproxy-0.8.4-6.el9.x86_64                                                                                                                                                     1/11 
  Verifying        : keyutils-1.6.3-1.el9.x86_64                                                                                                                                                     2/11 
  Verifying        : libev-4.33-5.el9.x86_64                                                                                                                                                         3/11 
  Verifying        : libnfsidmap-1:2.5.4-25.el9.x86_64                                                                                                                                               4/11 
  Verifying        : libverto-libev-0.3.2-3.el9.x86_64                                                                                                                                               5/11 
  Verifying        : nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                                 6/11 
  Verifying        : python3-pyyaml-5.4.1-6.el9.x86_64                                                                                                                                               7/11 
  Verifying        : quota-1:4.06-6.el9.x86_64                                                                                                                                                       8/11 
  Verifying        : quota-nls-1:4.06-6.el9.noarch                                                                                                                                                   9/11 
  Verifying        : rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                     10/11 
  Verifying        : sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                                                                                                                                            11/11 

Installed:
  gssproxy-0.8.4-6.el9.x86_64        keyutils-1.6.3-1.el9.x86_64  libev-4.33-5.el9.x86_64        libnfsidmap-1:2.5.4-25.el9.x86_64  libverto-libev-0.3.2-3.el9.x86_64    nfs-utils-1:2.5.4-25.el9.x86_64 
  python3-pyyaml-5.4.1-6.el9.x86_64  quota-1:4.06-6.el9.x86_64    quota-nls-1:4.06-6.el9.noarch  rpcbind-1.2.6-7.el9.x86_64         sssd-nfs-idmap-2.9.4-6.el9_4.x86_64 

Complete!
```

> Tạo thư mục để chia sẻ qua NFS
```shell
mkdir -p /var/nfsshare
```
> Set quyền và sở hữu cho thư mục chia sẻ
```shell
chown -R nfsnobody:nfsnobody /var/nfsshare
chmod 755 /var/nfsshare
```
> Cấu hình file /etc/exports để chia sẻ thư mục qua NFS
```shell
vi /etc/exports
```
> Thêm dòng cấu hình chia sẻ thư mục /var/nfsshare với mạng 10.10.10.0/24 và các quyền truy cập tương ứng
```shell
/var/nfsshare 10.10.10.0/24(rw,sync,no_root_squash,no_subtree_check)
```
> Khởi động và enable dịch vụ nfs-server
```shell
systemctl enable nfs-server
systemctl start nfs-server
systemctl status nfs-server
```
```shell
● nfs-server.service - NFS server and services
     Loaded: loaded (/usr/lib/systemd/system/nfs-server.service; enabled; preset: disabled)
    Drop-In: /run/systemd/generator/nfs-server.service.d
             └─order-with-mounts.conf
     Active: active (exited) since Thu 2024-06-06 22:56:56 +07; 14ms ago
       Docs: man:rpc.nfsd(8)
             man:exportfs(8)
    Process: 6436 ExecStartPre=/usr/sbin/exportfs -r (code=exited, status=0/SUCCESS)
    Process: 6437 ExecStart=/usr/sbin/rpc.nfsd (code=exited, status=0/SUCCESS)
    Process: 6456 ExecStart=/bin/sh -c if systemctl -q is-active gssproxy; then systemctl reload gssproxy ; fi (code=exited, status=0/SUCCESS)
   Main PID: 6456 (code=exited, status=0/SUCCESS)
        CPU: 17ms

Jun 06 22:56:56 nfs.kbuor.io.local systemd[1]: Starting NFS server and services...
Jun 06 22:56:56 nfs.kbuor.io.local systemd[1]: Finished NFS server and services.
```
> Export thư mục chia sẻ
```shell
exportfs -r
```
> Kiểm tra trạng thái và cấu hình chia sẻ
```shell
exportfs -v
```
```shell
/var/nfsshare   10.10.10.0/24(sync,wdelay,hide,no_subtree_check,sec=sys,rw,secure,no_root_squash,no_all_squash)
```

## KẾT NỐI TỪ MÁY CLIENT
---
> Cài đặt gói nfs-utils trên máy client
```shell
dnf install -y nfs-utils
```
```shell
Last metadata expiration check: 3:23:15 ago on Fri Jun  7 05:44:38 2024.
Dependencies resolved.
==========================================================================================================================================================================================================
 Package                                             Architecture                                Version                                                Repository                                   Size
==========================================================================================================================================================================================================
Installing:
 nfs-utils                                           x86_64                                      1:2.5.4-25.el9                                         baseos                                      429 k
Installing dependencies:
 gssproxy                                            x86_64                                      0.8.4-6.el9                                            baseos                                      108 k
 keyutils                                            x86_64                                      1.6.3-1.el9                                            baseos                                       71 k
 libev                                               x86_64                                      4.33-5.el9                                             baseos                                       52 k
 libnfsidmap                                         x86_64                                      1:2.5.4-25.el9                                         baseos                                       60 k
 libverto-libev                                      x86_64                                      0.3.2-3.el9                                            baseos                                       13 k
 python3-pyyaml                                      x86_64                                      5.4.1-6.el9                                            baseos                                      190 k
 quota                                               x86_64                                      1:4.06-6.el9                                           baseos                                      190 k
 quota-nls                                           noarch                                      1:4.06-6.el9                                           baseos                                       78 k
 rpcbind                                             x86_64                                      1.2.6-7.el9                                            baseos                                       56 k
 sssd-nfs-idmap                                      x86_64                                      2.9.4-6.el9_4                                          baseos                                       43 k

Transaction Summary
==========================================================================================================================================================================================================
Install  11 Packages

Total download size: 1.3 M
Installed size: 3.7 M
Downloading Packages:
(1/11): keyutils-1.6.3-1.el9.x86_64.rpm                                                                                                                                    86 kB/s |  71 kB     00:00    
(2/11): gssproxy-0.8.4-6.el9.x86_64.rpm                                                                                                                                   127 kB/s | 108 kB     00:00    
(3/11): libev-4.33-5.el9.x86_64.rpm                                                                                                                                        61 kB/s |  52 kB     00:00    
(4/11): libnfsidmap-2.5.4-25.el9.x86_64.rpm                                                                                                                               2.0 MB/s |  60 kB     00:00    
(5/11): libverto-libev-0.3.2-3.el9.x86_64.rpm                                                                                                                             707 kB/s |  13 kB     00:00    
(6/11): python3-pyyaml-5.4.1-6.el9.x86_64.rpm                                                                                                                             4.2 MB/s | 190 kB     00:00    
(7/11): nfs-utils-2.5.4-25.el9.x86_64.rpm                                                                                                                                 7.4 MB/s | 429 kB     00:00    
(8/11): quota-4.06-6.el9.x86_64.rpm                                                                                                                                       2.6 MB/s | 190 kB     00:00    
(9/11): rpcbind-1.2.6-7.el9.x86_64.rpm                                                                                                                                    942 kB/s |  56 kB     00:00    
(10/11): quota-nls-4.06-6.el9.noarch.rpm                                                                                                                                  1.0 MB/s |  78 kB     00:00    
(11/11): sssd-nfs-idmap-2.9.4-6.el9_4.x86_64.rpm                                                                                                                          1.0 MB/s |  43 kB     00:00    
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                     486 kB/s | 1.3 MB     00:02     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                  1/1 
  Installing       : libnfsidmap-1:2.5.4-25.el9.x86_64                                                                                                                                               1/11 
  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                      2/11 
  Installing       : rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                      2/11 
  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                      2/11 
Created symlink /etc/systemd/system/multi-user.target.wants/rpcbind.service → /usr/lib/systemd/system/rpcbind.service.
Created symlink /etc/systemd/system/sockets.target.wants/rpcbind.socket → /usr/lib/systemd/system/rpcbind.socket.

  Installing       : quota-nls-1:4.06-6.el9.noarch                                                                                                                                                   3/11 
  Installing       : quota-1:4.06-6.el9.x86_64                                                                                                                                                       4/11 
  Installing       : python3-pyyaml-5.4.1-6.el9.x86_64                                                                                                                                               5/11 
  Installing       : libev-4.33-5.el9.x86_64                                                                                                                                                         6/11 
  Installing       : libverto-libev-0.3.2-3.el9.x86_64                                                                                                                                               7/11 
  Installing       : gssproxy-0.8.4-6.el9.x86_64                                                                                                                                                     8/11 
  Running scriptlet: gssproxy-0.8.4-6.el9.x86_64                                                                                                                                                     8/11 
  Installing       : keyutils-1.6.3-1.el9.x86_64                                                                                                                                                     9/11 
  Running scriptlet: nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                                10/11 
  Installing       : nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                                10/11 
  Running scriptlet: nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                                10/11 
  Installing       : sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                                                                                                                                            11/11 
  Running scriptlet: sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                                                                                                                                            11/11 
  Verifying        : gssproxy-0.8.4-6.el9.x86_64                                                                                                                                                     1/11 
  Verifying        : keyutils-1.6.3-1.el9.x86_64                                                                                                                                                     2/11 
  Verifying        : libev-4.33-5.el9.x86_64                                                                                                                                                         3/11 
  Verifying        : libnfsidmap-1:2.5.4-25.el9.x86_64                                                                                                                                               4/11 
  Verifying        : libverto-libev-0.3.2-3.el9.x86_64                                                                                                                                               5/11 
  Verifying        : nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                                 6/11 
  Verifying        : python3-pyyaml-5.4.1-6.el9.x86_64                                                                                                                                               7/11 
  Verifying        : quota-1:4.06-6.el9.x86_64                                                                                                                                                       8/11 
  Verifying        : quota-nls-1:4.06-6.el9.noarch                                                                                                                                                   9/11 
  Verifying        : rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                     10/11 
  Verifying        : sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                                                                                                                                            11/11 

Installed:
  gssproxy-0.8.4-6.el9.x86_64        keyutils-1.6.3-1.el9.x86_64  libev-4.33-5.el9.x86_64        libnfsidmap-1:2.5.4-25.el9.x86_64  libverto-libev-0.3.2-3.el9.x86_64    nfs-utils-1:2.5.4-25.el9.x86_64 
  python3-pyyaml-5.4.1-6.el9.x86_64  quota-1:4.06-6.el9.x86_64    quota-nls-1:4.06-6.el9.noarch  rpcbind-1.2.6-7.el9.x86_64         sssd-nfs-idmap-2.9.4-6.el9_4.x86_64 

Complete!
```
> Tạo thư mục mount point trên máy client
```shell
mkdir -p /mnt/nfsshare
```
> Mount thư mục chia sẻ từ server NFS
```shell
mount -t nfs 10.10.10.104:/var/nfsshare /mnt/nfsshare
```
> Kiểm tra kết quả
```shell
df -h /mnt/nfsshare
```
```shell
Filesystem                  Size  Used Avail Use% Mounted on
10.10.10.104:/var/nfsshare  7.4G  1.6G  5.8G  22% /mnt/nfsshare
```
> Tạo một file test để kiểm tra quyền ghi
```shell
touch /mnt/nfsshare/testfile
```
