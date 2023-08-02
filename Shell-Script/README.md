# Practice 01
```shell
#!/bin/bash
clear
read -p 'Nhap vao o cung muon kiem tra: ' disk
fdisk -l $disk > /dev/null 2> /dev/null
if [ $? -eq 0 ]
then
    echo -e "\n========== THONG TIN DIA CUNG $disk ==========\n"
    echo -e "Kiem tra ngay $(date +%d" thang "%m" nam "%Y)\n"
    disk_info=$(fdisk -l $disk | sed -n '2p' | cut -d ' ' -f 3-)
    echo -e "O cung $disk co dung luong: ${disk_info}\n"
    disk_part=$(fdisk -l $disk | grep $disk | tail -n +2 | cut -d ' ' -f 1)
    echo 'Cac phan vung:'
    echo -e "${disk_part}\n"
    blkid -s TYPE | grep $disk | awk -F ' ' '{print "Phan vung " $1,"co kieu du lieu la " $2}'
    echo ''
else
    echo "O cung $disk khong ton tai trong he thong."
fi
```
-------------
# Practice 02

```shell
#!/bin/bash
if [ $1 = create ]
then
    if [ $USER = root ]
    then
        id $2 > /dev/null 2> /dev/null
        if [ $? -ne 0 ]
        then
            echo "Kiem tra tai khoan $2 : Tai khoan chua ton tai"
            useradd $2
            echo "Da tao tai khoan $2 thanh cong."
            read -p "Dat mat khau cho user $2. Chon 1 de dong y, ngoai ra khong dong y. Ban chon: " select
            if [ $select -eq 1 ]
            then
                passwd $2
                echo "Dat mat khau cho user $2 thanh cong"
            else
                echo "Ban khong dat mat khau cho user $2"
            fi
        else
            echo "Kiem tra tai khoan $2: Tai khoan $2 da ton tai trong he thong. Ket thuc!"
        fi
    else
        echo 'Ban khong phai la root user. Vui long chay script nay bang root user.'
    fi
elif [ $1 = delete ]
then
    if [ $USER = root ]
    then
        id $2 > /dev/null 2> /dev/null
        if [ $? -eq 0 ]
        then
            userdel -rf $2
            echo "Kiem tra tai khoan $2 : Tai khoan $2 co ton tai tren he thong. Da xoa tai khoan $2"
        else
            echo "Kiem tra tai khoan $2: Tai khoan $2 khong ton tai trong he thong. Ket thuc!"
        fi
    else
        echo 'Ban khong phai la root user. Vui long chay script nay bang root user.'
    fi
else
    echo 'Khong dung cu phap. Su dung mkaccount create/delete username de tao/xoa username'
fi
```