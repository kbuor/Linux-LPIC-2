## TRIỂN KHAI
---
> Cài đặt gói nfs-kernel-server
```shell
sudo apt install -y nfs-kernel-server
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
sudo vi /etc/exports
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
Tạo một file test để kiểm tra quyền ghi
```shell
touch /mnt/nfsshare/testfile
```
