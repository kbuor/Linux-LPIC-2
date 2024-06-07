## THÔNG TIN CHUNG
---
Operating System: `Ubuntu 22.04.4 LTS (Jammy)`

IP Address: `20.20.20.104/24`

Gateway: `20.20.20.20`

Hostname: `nginx.kbuor.io.local`

Domain: `kbuor.io.local`

## CHUẨN BỊ
---
> Update repository
```shell
sudo apt update -y && apt upgrade -y
```

## TRIỂN KHAI
---
> Cài đặt gói nfs-kernel-server
```shell
sudo apt install -y nfs-kernel-server
```
```shell
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  fontconfig-config fonts-dejavu-core libdeflate0 libfontconfig1 libgd3 libjbig0 libjpeg-turbo8 libjpeg8 libtiff5 libwebp7 libxpm4
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  keyutils libnfsidmap1 nfs-common rpcbind
Suggested packages:
  watchdog
The following NEW packages will be installed:
  keyutils libnfsidmap1 nfs-common nfs-kernel-server rpcbind
0 upgraded, 5 newly installed, 0 to remove and 3 not upgraded.
Need to get 521 kB of archives.
After this operation, 1,973 kB of additional disk space will be used.
Get:1 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libnfsidmap1 amd64 1:2.6.1-1ubuntu1.2 [42.9 kB]
Get:2 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 rpcbind amd64 1.2.6-2build1 [46.6 kB]
Get:3 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 keyutils amd64 1.6.1-2ubuntu3 [50.4 kB]
Get:4 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 nfs-common amd64 1:2.6.1-1ubuntu1.2 [241 kB]                                                                                          
Get:5 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 nfs-kernel-server amd64 1:2.6.1-1ubuntu1.2 [140 kB]                                                                                   
Fetched 521 kB in 60s (8,707 B/s)                                                                                                                                                                        
Selecting previously unselected package libnfsidmap1:amd64.
(Reading database ... 75112 files and directories currently installed.)
Preparing to unpack .../libnfsidmap1_1%3a2.6.1-1ubuntu1.2_amd64.deb ...
Unpacking libnfsidmap1:amd64 (1:2.6.1-1ubuntu1.2) ...
Selecting previously unselected package rpcbind.
Preparing to unpack .../rpcbind_1.2.6-2build1_amd64.deb ...
Unpacking rpcbind (1.2.6-2build1) ...
Selecting previously unselected package keyutils.
Preparing to unpack .../keyutils_1.6.1-2ubuntu3_amd64.deb ...
Unpacking keyutils (1.6.1-2ubuntu3) ...
Selecting previously unselected package nfs-common.
Preparing to unpack .../nfs-common_1%3a2.6.1-1ubuntu1.2_amd64.deb ...
Unpacking nfs-common (1:2.6.1-1ubuntu1.2) ...
Selecting previously unselected package nfs-kernel-server.
Preparing to unpack .../nfs-kernel-server_1%3a2.6.1-1ubuntu1.2_amd64.deb ...
Unpacking nfs-kernel-server (1:2.6.1-1ubuntu1.2) ...
Setting up libnfsidmap1:amd64 (1:2.6.1-1ubuntu1.2) ...
Setting up rpcbind (1.2.6-2build1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/rpcbind.service → /lib/systemd/system/rpcbind.service.
Created symlink /etc/systemd/system/sockets.target.wants/rpcbind.socket → /lib/systemd/system/rpcbind.socket.
Setting up keyutils (1.6.1-2ubuntu3) ...
Setting up nfs-common (1:2.6.1-1ubuntu1.2) ...

Creating config file /etc/idmapd.conf with new version

Creating config file /etc/nfs.conf with new version
Adding system user `statd' (UID 115) ...
Adding new user `statd' (UID 115) with group `nogroup' ...
Not creating home directory `/var/lib/nfs'.
Created symlink /etc/systemd/system/multi-user.target.wants/nfs-client.target → /lib/systemd/system/nfs-client.target.
Created symlink /etc/systemd/system/remote-fs.target.wants/nfs-client.target → /lib/systemd/system/nfs-client.target.
auth-rpcgss-module.service is a disabled or a static unit, not starting it.
nfs-idmapd.service is a disabled or a static unit, not starting it.
nfs-utils.service is a disabled or a static unit, not starting it.
proc-fs-nfsd.mount is a disabled or a static unit, not starting it.
rpc-gssd.service is a disabled or a static unit, not starting it.
rpc-statd-notify.service is a disabled or a static unit, not starting it.
rpc-statd.service is a disabled or a static unit, not starting it.
rpc-svcgssd.service is a disabled or a static unit, not starting it.
rpc_pipefs.target is a disabled or a static unit, not starting it.
var-lib-nfs-rpc_pipefs.mount is a disabled or a static unit, not starting it.
Setting up nfs-kernel-server (1:2.6.1-1ubuntu1.2) ...
Created symlink /etc/systemd/system/nfs-client.target.wants/nfs-blkmap.service → /lib/systemd/system/nfs-blkmap.service.
Created symlink /etc/systemd/system/multi-user.target.wants/nfs-server.service → /lib/systemd/system/nfs-server.service.
nfs-mountd.service is a disabled or a static unit, not starting it.
nfsdcld.service is a disabled or a static unit, not starting it.

Creating config file /etc/exports with new version

Creating config file /etc/default/nfs-kernel-server with new version
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.8) ...
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

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
```
> Tạo thư mục để chia sẻ qua NFS
```shell
sudo mkdir -p /srv/nfs/share
```
> Set quyền và sở hữu cho thư mục chia sẻ
```shell
sudo chown -R nobody:nogroup /srv/nfs/share
sudo chmod 755 /srv/nfs/share
```
> Cấu hình file /etc/exports để chia sẻ thư mục qua NFS
```shell
sudo nano /etc/exports
```
> Thêm dòng cấu hình chia sẻ thư mục /srv/nfs/share với mạng 20.20.20.0/24 và các quyền truy cập tương ứng
```shell
/srv/nfs/share 20.20.20.0/24(rw,sync,no_root_squash,no_subtree_check)
```
> Khởi động và enable dịch vụ nfs-kernel-server
```shell
sudo systemctl enable nfs-kernel-server
sudo systemctl start nfs-kernel-server
sudo systemctl status nfs-kernel-server
```
```shell
Synchronizing state of nfs-kernel-server.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable nfs-kernel-server
● nfs-server.service - NFS server and services
     Loaded: loaded (/lib/systemd/system/nfs-server.service; enabled; vendor preset: enabled)
    Drop-In: /run/systemd/generator/nfs-server.service.d
             └─order-with-mounts.conf
     Active: active (exited) since Fri 2024-06-07 02:22:33 UTC; 1min 56s ago
   Main PID: 21366 (code=exited, status=0/SUCCESS)
        CPU: 8ms

Jun 07 02:22:32 nfs.kbuor.io.local systemd[1]: Starting NFS server and services...
Jun 07 02:22:32 nfs.kbuor.io.local exportfs[21365]: exportfs: can't open /etc/exports for reading
Jun 07 02:22:33 nfs.kbuor.io.local systemd[1]: Finished NFS server and services.
```
> Export thư mục chia sẻ
```shell
sudo exportfs -ra
```
> Kiểm tra trạng thái và cấu hình chia sẻ
```shell
sudo exportfs -v
```
```shell
/srv/nfs/share  20.20.20.0/24(sync,wdelay,hide,no_subtree_check,sec=sys,rw,secure,no_root_squash,no_all_squash)
```

## KẾT NỐI TỪ MÁY CLIENT
---
> Cài đặt gói nfs-common trên máy client
```shell
sudo apt update
sudo apt install -y nfs-common
```
```shell
Hit:1 http://vn.archive.ubuntu.com/ubuntu jammy InRelease
Get:2 http://vn.archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]
Get:3 http://vn.archive.ubuntu.com/ubuntu jammy-backports InRelease [127 kB] 
Get:4 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [1,712 kB]
Get:5 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main Translation-en [316 kB]
Get:6 http://vn.archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [1,966 kB]
Get:7 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]   
Get:8 http://vn.archive.ubuntu.com/ubuntu jammy-updates/restricted Translation-en [335 kB]
Get:9 http://vn.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages [1,085 kB]    
Get:10 http://vn.archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 Packages [43.0 kB]  
Get:11 http://vn.archive.ubuntu.com/ubuntu jammy-backports/universe amd64 Packages [27.2 kB]
Get:12 http://vn.archive.ubuntu.com/ubuntu jammy-backports/universe Translation-en [16.3 kB]
Get:13 http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages [1,497 kB]
Get:14 http://security.ubuntu.com/ubuntu jammy-security/main Translation-en [257 kB]
Get:15 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [1,910 kB]
Get:16 http://security.ubuntu.com/ubuntu jammy-security/restricted Translation-en [324 kB]
Get:17 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages [856 kB]
Fetched 10.7 MB in 6s (1,670 kB/s)                                                                                                                                                                       
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
7 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  keyutils libnfsidmap1 rpcbind
Suggested packages:
  watchdog
The following NEW packages will be installed:
  keyutils libnfsidmap1 nfs-common rpcbind
0 upgraded, 4 newly installed, 0 to remove and 7 not upgraded.
Need to get 381 kB of archives.
After this operation, 1,447 kB of additional disk space will be used.
Get:1 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libnfsidmap1 amd64 1:2.6.1-1ubuntu1.2 [42.9 kB]
Get:2 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 rpcbind amd64 1.2.6-2build1 [46.6 kB]
Get:3 http://vn.archive.ubuntu.com/ubuntu jammy/main amd64 keyutils amd64 1.6.1-2ubuntu3 [50.4 kB]
Get:4 http://vn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 nfs-common amd64 1:2.6.1-1ubuntu1.2 [241 kB]
Fetched 381 kB in 1s (411 kB/s) 
Selecting previously unselected package libnfsidmap1:amd64.
(Reading database ... 74610 files and directories currently installed.)
Preparing to unpack .../libnfsidmap1_1%3a2.6.1-1ubuntu1.2_amd64.deb ...
Unpacking libnfsidmap1:amd64 (1:2.6.1-1ubuntu1.2) ...
Selecting previously unselected package rpcbind.
Preparing to unpack .../rpcbind_1.2.6-2build1_amd64.deb ...
Unpacking rpcbind (1.2.6-2build1) ...
Selecting previously unselected package keyutils.
Preparing to unpack .../keyutils_1.6.1-2ubuntu3_amd64.deb ...
Unpacking keyutils (1.6.1-2ubuntu3) ...
Selecting previously unselected package nfs-common.
Preparing to unpack .../nfs-common_1%3a2.6.1-1ubuntu1.2_amd64.deb ...
Unpacking nfs-common (1:2.6.1-1ubuntu1.2) ...
Setting up libnfsidmap1:amd64 (1:2.6.1-1ubuntu1.2) ...
Setting up rpcbind (1.2.6-2build1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/rpcbind.service → /lib/systemd/system/rpcbind.service.
Created symlink /etc/systemd/system/sockets.target.wants/rpcbind.socket → /lib/systemd/system/rpcbind.socket.
Setting up keyutils (1.6.1-2ubuntu3) ...
Setting up nfs-common (1:2.6.1-1ubuntu1.2) ...

Creating config file /etc/idmapd.conf with new version

Creating config file /etc/nfs.conf with new version
Adding system user `statd' (UID 116) ...
Adding new user `statd' (UID 116) with group `nogroup' ...
Not creating home directory `/var/lib/nfs'.
Created symlink /etc/systemd/system/multi-user.target.wants/nfs-client.target → /lib/systemd/system/nfs-client.target.
Created symlink /etc/systemd/system/remote-fs.target.wants/nfs-client.target → /lib/systemd/system/nfs-client.target.
auth-rpcgss-module.service is a disabled or a static unit, not starting it.
nfs-idmapd.service is a disabled or a static unit, not starting it.
nfs-utils.service is a disabled or a static unit, not starting it.
proc-fs-nfsd.mount is a disabled or a static unit, not starting it.
rpc-gssd.service is a disabled or a static unit, not starting it.
rpc-statd-notify.service is a disabled or a static unit, not starting it.
rpc-statd.service is a disabled or a static unit, not starting it.
rpc-svcgssd.service is a disabled or a static unit, not starting it.
rpc_pipefs.target is a disabled or a static unit, not starting it.
var-lib-nfs-rpc_pipefs.mount is a disabled or a static unit, not starting it.
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.8) ...
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
> Tạo thư mục mount point trên máy client
```shell
sudo mkdir -p /mnt/nfsshare
```
> Mount thư mục chia sẻ từ server NFS
```shell
sudo mount -t nfs 20.20.20.104:/srv/nfs/share /mnt/nfsshare
```
> Kiểm tra kết quả
```shell
df -h /mnt/nfsshare
```
```shell
Filesystem                   Size  Used Avail Use% Mounted on
20.20.20.104:/srv/nfs/share   17G  5.2G   11G  33% /mnt/nfsshare
```
Tạo một file test để kiểm tra quyền ghi
```shell
touch /mnt/nfsshare/testfile
```
