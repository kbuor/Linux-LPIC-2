```shell
yum install -y samba
```
```shell
mkdir -p /robusta/{giaovien,hocsinh,baithi,software,bangiamhieu}
chmod 777 /robusta/giaovien/
chmod 777 /robusta/hocsinh
chmod 777 /robusta/baithi
```
```shell
vi /etc/samba/smb.conf
```
```shell
[global]
workgroup = MYGROUP
server string = Samba Server
passdb backend = smbpasswd
log file = /var/log/samba/log.%m
max log size = 50
create mask = 0766
directory mask = 0777 
inherit permissions = yes 
access based share enum = yes 
cups options = raw

[homes]
comment = Home Directories
read only = No
browseable = No

[printers]
comment = All Printers
path = /var/spool/samba
printable = Yes
browseable = No
```
> Tạo share hocsinh: mọi user có thể đọc, ghi
```shell
[Hocsinh]
comment = Du lieu dung chung
path = /robusta/hocsinh
read only = No
```
> Tạo share Baithi: nhóm giaovien được đọc, ghi, nhóm hocsinh chỉ có thể đọc
```shell
[Baithi]
comment = Bai thi hoc ky
path = /robusta/baithi
valid users = +hocsinh, +giaovien
write list = +giaovien
```
> Tạo share Giaovien, gv1 tạo, gv2 không thể xem
```shell
[Giaovien]
comment = Du lieu giao vien
path = /robusta/giaovien
valid users = +giaovien
write list = +giaovien
create mask = 0760
directory mask = 0770
veto files = /*.exe/*.mp3/*mp4*/
```
> Tạo share Software mọi user chỉ đọc
```shell
[Software]
comment = Phan mem co ban
path = /robusta/software
```
> Tạo share ẩn bgh chỉ có user ht mới có thể truy cập
```shell
[bgh]
comment = Ban giam hieu
path = /robusta/bangiamhieu
valid users = ht
read only = No
browseable = No
```
> Mount SMB trên Linux Client
```shell
mount -o username=gv1,password=123 //192.168.1.20/gv1 /giaovien
```

> Xem thong tin tài khoản samba:
```shell
pdbedit -L
pdbedit -Lv
pdbedit -Lv hs1
```
```shell
pdbedit -L ; xem danh sách user
pdbedit -x hpho ; xóa user hpho
pdbedit -a hpho ; tạo user hpho password: P@ssword105
```
> Xem policy hiện tại:
```shell
pdbedit -P "min password length"
pdbedit -P "password history" 
```
```shell
pdbedit -P "maximum password age"
pdbedit -P "minimum password age"
pdbedit -P "bad lockout attempt"
pdbedit -P "lockout duration" 
```
> Thiết pập policy theo yêu cầu:
```shell
min password length = 8 characters.
password history = last 4 passwords.
maximum password age = 90 days.
minimum password age = 7 days.
bad lockout attempt = 8 bad logon attempts.
lockout duration = forever, account must be manually reenabled.
```
> Thực hiện các lệnh sau để gán policy:
```shell
pdbedit -P "min password length" -C 8
pdbedit -P "password history" -C 4
pdbedit -P "maximum password age" -C 90
pdbedit -P "minimum password age" -C 7
pdbedit -P "bad lockout attempt" -C 8
pdbedit -P "lockout duration" -C -1
```
> Thêm rule SELINUX (Nếu bật SELINUX)
```shell
chcon -t samba_share_t /home/mydata/
```
