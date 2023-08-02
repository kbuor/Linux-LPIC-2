# Prepare Linux (Centos 7)
```shell
yum install -y open-vm-tools git wget unzip zip epel-release
yum update -y
systemctl stop firewalld
systemctl disable firewalld
sed -i "s/=enforcing/=disabled/" /etc/sysconfig/selinux
reboot
```

# Start deloyment
```shell
yum install -y bind bind-utils
hostnamectl set-hostname dns.kbuor.local
```

# Edit DNS Server config file
```shell
sed -i s/"listen-on port 53 { 127.0.0.1; };"/"listen-on port 53 { 127.0.0.1; 10.19.0.11; };"/ /etc/named.conf
sed -i s/"allow-query     { localhost; };"/"allow-query     { localhost; 10.19.0.0/24; };"/ /etc/named.conf
```

# Add forward zone
```shell
sed -i "59 i zone \"kbuor.local\" IN {" /etc/named.conf
sed -i "60 i type master;" /etc/named.conf
sed -i "61 i file \"forward.kbuor.local\";" /etc/named.conf
sed -i "62 i allow-update { none; };" /etc/named.conf
sed -i "63 i };" /etc/named.conf
```

# Add reverse zone
```shell
sed -i "64 i zone \"0.19.10.in-addr.arpa\" IN {" /etc/named.conf
sed -i "65 i type master;" /etc/named.conf
sed -i "66 i file \"reverse.kbuor.local\";" /etc/named.conf
sed -i "67 i allow-update { none; };" /etc/named.conf
sed -i "68 i };" /etc/named.conf
```

# Create forward file
```shell
touch /var/named/forward.kbuor.local
cat << EOF > /var/named/forward.$var_domain
\$TTL 86400
@ IN SOA kbuor.local. admin.kbuor.local. (
2023061401 ;Serial
3600 ;Refresh
1800 ;Retry
604800 ;Expire
86400 ;Minimun TTL
)
@ IN NS dns.kbuor.local.
dns IN A 10.19.0.11
EOF
```

# Create reverse file
```shell
touch /var/named/reverse.kbuor.local
cat << EOF > /var/named/reverse.$var_domain
\$TTL 86400
@ IN SOA kbuor.local. admin.kbuor.local. (
2023061401 ;Serial
3600 ;Refresh
1800 ;Retry
604800 ;Expire
86400 ;Minimun TTL
)
@ IN NS dns.kbuor.local.
11 IN PTR dns.kbuor.local.
EOF
```

# Start DNS Service
```shell
systemctl start named
systemctl enable --now named
chgrp named -R /var/named
chown -v root:named /etc/named.conf
restorecon -rv /var/named
restorecon /etc/named.conf
```