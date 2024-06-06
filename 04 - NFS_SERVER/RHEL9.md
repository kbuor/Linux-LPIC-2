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
> Export thư mục chia sẻ
```shell
exportfs -r
```
> Kiểm tra trạng thái và cấu hình chia sẻ
```shell
exportfs -v
```

## KẾT NỐI TỪ MÁY CLIENT
---
Cài đặt gói nfs-utils trên máy client
shell
Sao chép mã
dnf install -y nfs-utils
Tạo thư mục mount point trên máy client
shell
Sao chép mã
mkdir -p /mnt/nfsshare
Mount thư mục chia sẻ từ server NFS
shell
Sao chép mã
mount -t nfs 10.10.10.103:/var/nfsshare /mnt/nfsshare
Kiểm tra kết quả
shell
Sao chép mã
df -h /mnt/nfsshare
Tạo một file test để kiểm tra quyền ghi

shell
Sao chép mã
touch /mnt/nfsshare/testfile
