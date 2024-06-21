## THÔNG TIN CHUNG
---
Operating System: `Centos 7 (platform:el7)`

IP Address: `10.10.10.105/24`

Gateway: `10.10.10.10`

Hostname: `mail.kbuor.io.local`

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
> Install common package
```shell
yum install -y open-vm-tools epel-release wget zip bind-utils net-tools
yum update -y
```

> Check your hostname correctly
```shell
hostnamectl set-hostname mail.kbuor.io.local
hostnamectl
```

> Add to end of your host file your IP address and Hostname
```shell
echo '103.89.85.24 mail.kbuor.io.local mail' >> /etc/hosts
reboot
```

> Remove Postfix
```shell
yum remove postfix -y
```

> Install dependence package
```shell
yum -y install unzip net-tools sysstat openssh-clients perl-core libaio nmap-ncat libstdc++.so.6
```

> Download Zimbra
```shell
cd /tmp
wget https://files.zimbra.com/downloads/8.8.15_GA/zcs-8.8.15_GA_3869.RHEL7_64.20190918004220.tgz
```

> Extract downloaded file
```shell
tar -xzvf zcs-8*
cd zcs-8*
chmod +x install.sh
```

> Check DNS record
```shell
dig A mail.kbuor.io.local
```
```shell
            ; <<>> DiG 9.11.4-P2-RedHat-9.11.4-26.P2.el7_9.10 <<>> A mail.kbuor.io.local
            ;; global options: +cmd
            ;; Got answer:
            ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 21229
            ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

            ;; OPT PSEUDOSECTION:
            ; EDNS: version: 0, flags:; udp: 512
            ;; QUESTION SECTION:
            ;mail.kbuor.io.local.            IN      A

            ;; ANSWER SECTION:
            mail.kbuor.io.local.     300     IN      A       103.89.85.24

            ;; Query time: 50 msec
            ;; SERVER: 8.8.8.8#53(8.8.8.8)
            ;; WHEN: Sat Oct 29 10:01:54 +07 2022
            ;; MSG SIZE  rcvd: 63
```
```shell
dig MX kbuor.io.local
```
```shell
            ; <<>> DiG 9.11.4-P2-RedHat-9.11.4-26.P2.el7_9.10 <<>> MX kbuor.io.local
            ;; global options: +cmd
            ;; Got answer:
            ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 5960
            ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

            ;; OPT PSEUDOSECTION:
            ; EDNS: version: 0, flags:; udp: 512
            ;; QUESTION SECTION:
            ;kbuor.io.local.                 IN      MX

            ;; ANSWER SECTION:
            kbuor.io.local.          300     IN      MX      10 mail.kbuor.io.local.

            ;; Query time: 51 msec
            ;; SERVER: 8.8.8.8#53(8.8.8.8)
            ;; WHEN: Sat Oct 29 10:02:17 +07 2022
            ;; MSG SIZE  rcvd: 63
```
> Recommend run script via tmux
```shell
cd /tmp/zcs-8*
./install.sh
```
```shell

                        Operations logged to /tmp/install.log.bnyHvXPW
                        Checking for existing installation...
                            zimbra-drive...NOT FOUND
                            zimbra-imapd...NOT FOUND
                            zimbra-modern-ui...NOT FOUND
                            zimbra-modern-zimlets...NOT FOUND
                            zimbra-patch...NOT FOUND
                            zimbra-mta-patch...NOT FOUND
                            zimbra-proxy-patch...NOT FOUND
                            zimbra-license-tools...NOT FOUND
                            zimbra-license-extension...NOT FOUND
                            zimbra-network-store...NOT FOUND
                            zimbra-network-modules-ng...NOT FOUND
                            zimbra-chat...NOT FOUND
                            zimbra-connect...NOT FOUND
                            zimbra-talk...NOT FOUND
                            zimbra-ldap...NOT FOUND
                            zimbra-logger...NOT FOUND
                            zimbra-mta...NOT FOUND
                            zimbra-dnscache...NOT FOUND
                            zimbra-snmp...NOT FOUND
                            zimbra-store...NOT FOUND
                            zimbra-apache...NOT FOUND
                            zimbra-spell...NOT FOUND
                            zimbra-convertd...NOT FOUND
                            zimbra-memcached...NOT FOUND
                            zimbra-proxy...NOT FOUND
                            zimbra-archiving...NOT FOUND
                            zimbra-core...NOT FOUND

                        Do you agree with the terms of the software license agreement? [N] y
                        Use Zimbra's package repository [Y] y
                        Found zimbra-core (local)
                        Found zimbra-ldap (local)
                        Found zimbra-logger (local)
                        Found zimbra-mta (local)
                        Found zimbra-dnscache (local)
                        Found zimbra-snmp (local)
                        Found zimbra-store (local)
                        Found zimbra-apache (local)
                        Found zimbra-spell (local)
                        Found zimbra-memcached (repo)
                        Found zimbra-proxy (local)
                        Found zimbra-drive (repo)
                        Found zimbra-imapd (local)
                        Found zimbra-patch (repo)
                        Found zimbra-mta-patch (repo)
                        Found zimbra-proxy-patch (repo)
                        ...
                        Select the packages to install
                        Install zimbra-ldap [Y] y
                        Install zimbra-logger [Y] y
                        Install zimbra-mta [Y] y
                        Install zimbra-dnscache [Y] n
                        Install zimbra-snmp [Y] y
                        Install zimbra-store [Y] y
                        Install zimbra-apache [Y] y
                        Install zimbra-spell [Y] y
                        Install zimbra-memcached [Y] y
                        Install zimbra-proxy [Y] y
                        Install zimbra-drive [Y] y
                        Install zimbra-imapd (BETA - for evaluation only) [N] n
                        Install zimbra-chat [Y] y
                        Checking required space for zimbra-core
                        Checking space for zimbra-store
                        Checking required packages for zimbra-store
                        zimbra-store package check complete.
                        Installing:
                        ...
                            zimbra-core
                            ...
                            zimbra-chat
                        ...
                        The system will be modified.  Continue? [N] y
                        Beginning Installation - see /tmp/install.log.PtZTEKqZ for details...
                                                  zimbra-core-components will be downloaded and installed.
                                                    zimbra-timezone-data will be installed.
                                                  zimbra-common-core-jar will be installed.
                                                 zimbra-common-mbox-conf will be installed.
                                           zimbra-common-mbox-conf-attrs will be installed.
                                            zimbra-common-mbox-conf-msgs will be installed.
                                          zimbra-common-mbox-conf-rights will be installed.
                                                   zimbra-common-mbox-db will be installed.
                                                 zimbra-common-mbox-docs will be installed.
                                           zimbra-common-mbox-native-lib will be installed.
                                                 zimbra-common-core-libs will be installed.
                                                             zimbra-core will be installed.
                                                  zimbra-ldap-components will be downloaded and installed.
                                                             zimbra-ldap will be installed.
                                                           zimbra-logger will be installed.
                                                   zimbra-mta-components will be downloaded and installed.
                                                              zimbra-mta will be installed.
                                              zimbra-dnscache-components will be downloaded and installed.
                                                         zimbra-dnscache will be installed.
                                                  zimbra-snmp-components will be downloaded and installed.
                                                             zimbra-snmp will be installed.
                                                 zimbra-store-components will be downloaded and installed.
                                               zimbra-jetty-distribution will be downloaded and installed.
                                                        zimbra-mbox-conf will be installed.
                                                         zimbra-mbox-war will be installed.
                                                     zimbra-mbox-service will be installed.
                                               zimbra-mbox-webclient-war will be installed.
                                           zimbra-mbox-admin-console-war will be installed.
                                                  zimbra-mbox-store-libs will be installed.
                                                            zimbra-store will be installed.
                                                zimbra-apache-components will be downloaded and installed.
                                                           zimbra-apache will be installed.
                                                 zimbra-spell-components will be downloaded and installed.
                                                            zimbra-spell will be installed.
                                                        zimbra-memcached will be downloaded and installed.
                                                 zimbra-proxy-components will be downloaded and installed.
                                                            zimbra-proxy will be installed.
                                                            zimbra-drive will be downloaded and installed (later).
                                                            zimbra-imapd will be installed.
                                                            zimbra-patch will be downloaded and installed (later).
                                                        zimbra-mta-patch will be downloaded and installed (later).
                                                      zimbra-proxy-patch will be downloaded and installed (later).
                                                             zimbra-chat will be downloaded and installed (later).
                        Downloading packages (11):
                        ...
                           zimbra-core-components
                           ...
                           zimbra-proxy-components
                              ...done
                        ...
                        Removing /opt/zimbra
                        Removing zimbra crontab entry...done.
                        Cleaning up zimbra init scripts...done.
                        Cleaning up /etc/security/limits.conf...done.
                        Finished removing Zimbra Collaboration Server.
                        Installing repo packages (11):
                        ...
                           zimbra-core-components
                           ...
                           zimbra-proxy-components
                              ...done
                        ...
                        Installing local packages (27):
                        ...
                           zimbra-timezone-data
                           ...
                           zimbra-imapd
                              ...done
                        ...
                        Installing extra packages (5):
                        ...
                           zimbra-drive
                           ...
                           zimbra-chat
                              ...done
                        ...
                        Running Post Installation Configuration:
                        Operations logged to /tmp/zmsetup.20220411-024200.log
                        Installing LDAP configuration database...done.
                        Setting defaults...
                        DNS ERROR resolving MX for mail.kbuor.io.local
                        It is suggested that the domain name have an MX record configured in DNS
                        Change domain name? [Yes] yes
                        Create domain: [mail.kbuor.io.local] kbuor.io.local  #Replace by your domain
                                    MX: mail.kbuor.io.local (103.89.85.24)
                                    Interface: 127.0.0.1
                                    Interface: ::1
                                    Interface: 103.89.85.24
                        done.
                        Checking for port conflicts
                        Main menu
                           1) Common Configuration:
                           2) zimbra-ldap:                             Enabled
                           3) zimbra-logger:                           Enabled
                           4) zimbra-mta:                              Enabled
                           5) zimbra-snmp:                             Enabled
                           6) zimbra-store:                            Enabled
                                +Create Admin User:                    yes
                                +Admin user to create:                 admin@azdigi.online
                        ******* +Admin Password                        UNSET  #chưa set Password
                                +Anti-virus quarantine user:           virus-quarantine.oz1ioypute@azdigi.online
                                +Enable automated spam training:       yes
                                +Spam training user:                   spam.wnlas9fe1o@azdigi.online
                                +Non-spam(Ham) training user:          ham.97krutc9vl@azdigi.online
                                +SMTP host:                            webmail.azdigi.online
                                +Web server HTTP port:                 8080
                                +Web server HTTPS port:                8443
                                +Web server mode:                      https
                                +IMAP server port:                     7143
                                +IMAP server SSL port:                 7993
                                +POP server port:                      7110
                                +POP server SSL port:                  7995
                                +Use spell check server:               yes
                                +Spell server URL:                     http://webmail.azdigi.online:7780/aspell.php
                                +Enable version update checks:         TRUE
                                +Enable version update notifications:  TRUE
                                +Version update notification email:    admin@azdigi.online
                                +Version update source email:          admin@azdigi.online
                                +Install mailstore (service webapp):   yes
                                +Install UI (zimbra,zimbraAdmin webapps): yes
                           7) zimbra-spell:                            Enabled
                           8) zimbra-proxy:                            Enabled
                           9) zimbra-imapd:                            Enabled
                          10) Default Class of Service Configuration:
                           s) Save config to file
                           x) Expand menu
                           q) Quit
                        Address unconfigured (**) items  (? - help) 6
                        Store configuration
                           1) Status:                                  Enabled
                           2) Create Admin User:                       yes
                           3) Admin user to create:                    admin@azdigi.online
                        ** 4) Admin Password                           UNSET
                           5) Anti-virus quarantine user:              virus-quarantine.oz1ioypute@azdigi.online
                           6) Enable automated spam training:          yes
                           7) Spam training user:                      spam.wnlas9fe1o@azdigi.online
                           8) Non-spam(Ham) training user:             ham.97krutc9vl@azdigi.online
                           9) SMTP host:                               webmail.azdigi.online
                          10) Web server HTTP port:                    8080
                          11) Web server HTTPS port:                   8443
                          12) Web server mode:                         https
                          13) IMAP server port:                        7143
                          14) IMAP server SSL port:                    7993
                          15) POP server port:                         7110
                          16) POP server SSL port:                     7995
                          17) Use spell check server:                  yes
                          18) Spell server URL:                        http://webmail.azdigi.online:7780/aspell.php
                          19) Enable version update checks:            TRUE
                          20) Enable version update notifications:     TRUE
                          21) Version update notification email:       admin@azdigi.online
                          22) Version update source email:             admin@azdigi.online
                          23) Install mailstore (service webapp):      yes
                          24) Install UI (zimbra,zimbraAdmin webapps): yes
                        Select, or 'r' for previous menu [r] 4
                        Password for admin@azdigi.online (min 6 characters): [JqA8eqasM] #Your password
                        Store configuration
                           1) Status:                                  Enabled
                           2) Create Admin User:                       yes
                           3) Admin user to create:                    admin@azdigi.online
                           4) Admin Password                           set #Đã set Password
                           5) Anti-virus quarantine user:              virus-quarantine.oz1ioypute@azdigi.online
                           6) Enable automated spam training:          yes
                           7) Spam training user:                      spam.wnlas9fe1o@azdigi.online
                           8) Non-spam(Ham) training user:             ham.97krutc9vl@azdigi.online
                           9) SMTP host:                               webmail.azdigi.online
                          10) Web server HTTP port:                    8080
                          11) Web server HTTPS port:                   8443
                          12) Web server mode:                         https
                          13) IMAP server port:                        7143
                          14) IMAP server SSL port:                    7993
                          15) POP server port:                         7110
                          16) POP server SSL port:                     7995
                          17) Use spell check server:                  yes
                          18) Spell server URL:                        http://webmail.azdigi.online:7780/aspell.php
                          19) Enable version update checks:            TRUE
                          20) Enable version update notifications:     TRUE
                          21) Version update notification email:       admin@azdigi.online
                          22) Version update source email:             admin@azdigi.online
                          23) Install mailstore (service webapp):      yes
                          24) Install UI (zimbra,zimbraAdmin webapps): yes
                        Select, or 'r' for previous menu [r] r
                        Main menu
                           1) Common Configuration:
                           2) zimbra-ldap:                             Enabled
                           3) zimbra-logger:                           Enabled
                           4) zimbra-mta:                              Enabled
                           5) zimbra-dnscache:                         Enabled
                           6) zimbra-snmp:                             Enabled
                           7) zimbra-store:                            Enabled
                           8) zimbra-spell:                            Enabled
                           9) zimbra-proxy:                            Enabled
                          10) zimbra-imapd:                            Enabled
                          11) Default Class of Service Configuration:
                           s) Save config to file
                           x) Expand menu
                           q) Quit
                        *** CONFIGURATION COMPLETE - press 'a' to apply
                        Select from menu, or press 'a' to apply config (? - help) a
                        Save configuration data to a file? [Yes] yes
                        Save config in file: [/opt/zimbra/config.15635] /opt/zimbra/config.15635
                        Saving config in /opt/zimbra/config.15635...done.
                        The system will be modified - continue? [No] yes
                        ...
                           Operations logged to /tmp/zmsetup.20220411-024200.log
                           ...
                           Finished installing common zimlets.
                        Restarting mailboxd...done.
                        ...
                        Creating galsync account for default domain...done.
                        You have the option of notifying Zimbra of your installation.
                        This helps us to track the uptake of the Zimbra Collaboration Server.
                        The only information that will be transmitted is:
                                    The VERSION of zcs installed (8.8.15_GA_3869_RHEL7_64)
                                    The ADMIN EMAIL ADDRESS created (admin@azdigi.online)
                        Notify Zimbra of your installation? [Yes] n
                        Checking if the NG started running...done.
                        Setting up zimbra crontab...done.
                        Moving /tmp/zmsetup.20220411-024200.log to /opt/zimbra/log

                        Configuration complete - press return to exit
                        
```
> Update SSH Key for zimbra user
```shell
sudo -u zimbra -i
zmupdateauthkeys
exit
```

> Install Syslog for Administration Dashboard
```shell
/opt/zimbra/libexec/zmsyslogsetup
```

> Enable ClamAV Antivirus
```shell
su - zimbra
zmprov mcf zimbraAttachmentsScanURL clam://localhost:3310/
zmprov mcf zimbraAttachmentsScanEnabled TRUE
```
> Generate DKIM record
```shell
/opt/zimbra/libexec/zmdkimkeyutil -a -d kbuor.io.local
```

> Add DNS record in DNS Server

> DKIM: 

> DMARC:
_DMARC IN v=DMARC1; p=reject; pct=100; rua=mailto:admin@kbuor.io.local

> SPF:
@ IN v=spf1 ip4:103.89.85.24 include:kbuor.io.local mx -all

---
> Secure Zimbra with Let's Encrypt
(Login as root)
> Install Certbot package
```shell
yum install -y certbot
```
> Obtaining an SSL Certificate
```shell
certbot certonly -d mail.kbuor.io.local
```
> Configure SSL Certificate for Zimbra
```shell
su - zimbra
zmcontrol stop
```
> Copy certificate file to correct location
```shell
mkdir /opt/zimbra/ssl/letsencrypt
cp /etc/letsencrypt/live/mail.kbuor.io.local/* /opt/zimbra/ssl/letsencrypt/
cd /opt/zimbra/ssl/letsencrypt/
echo > chain.pem
```
> Paste content below to chain.pem file
```shell
-----BEGIN CERTIFICATE-----
MIIFMTCCBBmgAwIBAgISA7KAKK5msndhydn4BNZP5TWiMA0GCSqGSIb3DQEBCwUA
MDIxCzAJBgNVBAYTAlVTMRYwFAYDVQQKEw1MZXQncyBFbmNyeXB0MQswCQYDVQQD
EwJSMzAeFw0yMjAzMjMwNTI5MThaFw0yMjA2MjEwNTI5MTdaMCAxHjAcBgNVBAMT
FW1haWwuZG90cnVuZ3F1YW4uc2l0ZTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
AQoCggEBAKyO0W6G9PDG2E3k7E6fGvInutJ0+ICGm3rZkmVQtiihxDCvbeLbbGgQ
ozz2IXdd57Rs2tn0daXAnHhhYBp9LzuuktLIn6fZK6+m1lOQr7/D8P6Z2x8eqYVr
sppuQm3NgCe68ZNqbBrCZ9BLFAhSr/s3T9tsmwAJ2zGjC9W3jLklJFl527pHzhu3
IUsLorVUuYC0FVEQKPSJjoTy8x4EMkggp17ec7vZh7t8s8PoICi3wGtDz72L+9FC
43tJTQ3Z6OD/5oU/zBw4wttiRSdi0J3xlvYEjp1kVbQuKDAEZEgG+ed9nqeZ+wHB
sCl5p+4J0X0gIi/xwlSn5L3k9clsljcCAwEAAaOCAlEwggJNMA4GA1UdDwEB/wQE
AwIFoDAdBgNVHSUEFjAUBggrBgEFBQcDAQYIKwYBBQUHAwIwDAYDVR0TAQH/BAIw
ADAdBgNVHQ4EFgQUYvcEWd6L1cE4BYjbKheQecSjMWMwHwYDVR0jBBgwFoAUFC6z
F7dYVsuuUAlA5h+vnYsUwsYwVQYIKwYBBQUHAQEESTBHMCEGCCsGAQUFBzABhhVo
dHRwOi8vcjMuby5sZW5jci5vcmcwIgYIKwYBBQUHMAKGFmh0dHA6Ly9yMy5pLmxl
bmNyLm9yZy8wIAYDVR0RBBkwF4IVbWFpbC5kb3RydW5ncXVhbi5zaXRlMEwGA1Ud
IARFMEMwCAYGZ4EMAQIBMDcGCysGAQQBgt8TAQEBMCgwJgYIKwYBBQUHAgEWGmh0
dHA6Ly9jcHMubGV0c2VuY3J5cHQub3JnMIIBBQYKKwYBBAHWeQIEAgSB9gSB8wDx
AHcA36Veq2iCTx9sre64X04+WurNohKkal6OOxLAIERcKnMAAAF/tXckiQAABAMA
SDBGAiEA8vwBUawi1GSn4Ly0rRKdyEUYSilMpzn3jrphPUCBGfsCIQCqRozDbEZ3
JfQMnoFcrAhKONru79n4AvRF9GDpGxN3JwB2AEalVet1+pEgMLWiiWn0830RLEF0
vv1JuIWr8vxw/m1HAAABf7V3JLIAAAQDAEcwRQIgeVMJ5zV+OXAgpyALWopypgyO
p8FiyU6ZOn2hJS1FUCwCIQCdZYH4ooMucAdCc+Mru7iO7Tc+Czx48MyDfmBzauRO
KzANBgkqhkiG9w0BAQsFAAOCAQEATaHH+j9fdvo/yD++NYzHBVu9ka03xNpSAr1i
EjPtk+xYc7qy84nAxAQ6HOCLdMGUSRyv3os8Aa+l+CoV+5FiShphuHza0y6byZzK
FZyzpinijZvx1Lz/GEZLDG245RzagO5vLXFv8Hv5w14z9/PQcAd/eEy2f0iY060b
bDYZxZcENhA9dgu+M4xVCMEFUtCAqLAmY+A42bJPIQJ0nJnMBmNUG9vW9PfI4Ga7
X5/C+3bysuR59B1IpJdaL2NE3vP5eV9XDEwWu2jVi84lTycrjReLJVWiCj3Tf1VS
Bd7zmPxYBSLJvHXh7uVmJ/8a2i+0mazzZv7fN1n1uspQ/xoh0g==
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIFFjCCAv6gAwIBAgIRAJErCErPDBinU/bWLiWnX1owDQYJKoZIhvcNAQELBQAw
TzELMAkGA1UEBhMCVVMxKTAnBgNVBAoTIEludGVybmV0IFNlY3VyaXR5IFJlc2Vh
cmNoIEdyb3VwMRUwEwYDVQQDEwxJU1JHIFJvb3QgWDEwHhcNMjAwOTA0MDAwMDAw
WhcNMjUwOTE1MTYwMDAwWjAyMQswCQYDVQQGEwJVUzEWMBQGA1UEChMNTGV0J3Mg
RW5jcnlwdDELMAkGA1UEAxMCUjMwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEK
AoIBAQC7AhUozPaglNMPEuyNVZLD+ILxmaZ6QoinXSaqtSu5xUyxr45r+XXIo9cP
R5QUVTVXjJ6oojkZ9YI8QqlObvU7wy7bjcCwXPNZOOftz2nwWgsbvsCUJCWH+jdx
sxPnHKzhm+/b5DtFUkWWqcFTzjTIUu61ru2P3mBw4qVUq7ZtDpelQDRrK9O8Zutm
NHz6a4uPVymZ+DAXXbpyb/uBxa3Shlg9F8fnCbvxK/eG3MHacV3URuPMrSXBiLxg
Z3Vms/EY96Jc5lP/Ooi2R6X/ExjqmAl3P51T+c8B5fWmcBcUr2Ok/5mzk53cU6cG
/kiFHaFpriV1uxPMUgP17VGhi9sVAgMBAAGjggEIMIIBBDAOBgNVHQ8BAf8EBAMC
AYYwHQYDVR0lBBYwFAYIKwYBBQUHAwIGCCsGAQUFBwMBMBIGA1UdEwEB/wQIMAYB
Af8CAQAwHQYDVR0OBBYEFBQusxe3WFbLrlAJQOYfr52LFMLGMB8GA1UdIwQYMBaA
FHm0WeZ7tuXkAXOACIjIGlj26ZtuMDIGCCsGAQUFBwEBBCYwJDAiBggrBgEFBQcw
AoYWaHR0cDovL3gxLmkubGVuY3Iub3JnLzAnBgNVHR8EIDAeMBygGqAYhhZodHRw
Oi8veDEuYy5sZW5jci5vcmcvMCIGA1UdIAQbMBkwCAYGZ4EMAQIBMA0GCysGAQQB
gt8TAQEBMA0GCSqGSIb3DQEBCwUAA4ICAQCFyk5HPqP3hUSFvNVneLKYY611TR6W
PTNlclQtgaDqw+34IL9fzLdwALduO/ZelN7kIJ+m74uyA+eitRY8kc607TkC53wl
ikfmZW4/RvTZ8M6UK+5UzhK8jCdLuMGYL6KvzXGRSgi3yLgjewQtCPkIVz6D2QQz
CkcheAmCJ8MqyJu5zlzyZMjAvnnAT45tRAxekrsu94sQ4egdRCnbWSDtY7kh+BIm
lJNXoB1lBMEKIq4QDUOXoRgffuDghje1WrG9ML+Hbisq/yFOGwXD9RiX8F6sw6W4
avAuvDszue5L3sz85K+EC4Y/wFVDNvZo4TYXao6Z0f+lQKc0t8DQYzk1OXVu8rp2
yJMC6alLbBfODALZvYH7n7do1AZls4I9d1P4jnkDrQoxB3UqQ9hVl3LEKQ73xF1O
yK5GhDDX8oVfGKF5u+decIsH4YaTw7mP3GFxJSqv3+0lUFJoi5Lc5da149p90Ids
hCExroL1+7mryIkXPeFM5TgO9r0rvZaBFOvV2z0gp35Z0+L4WPlbuEjN/lxPFin+
HlUjr8gRsI3qfJOQFy/9rKIJR0Y/8Omwt/8oTWgy1mdeHmmjk7j1nYsvC9JSQ6Zv
MldlTTKB3zhThV1+XWYp6rjd5JW1zbVWEkLNxE7GJThEUG3szgBVGP7pSWTUTsqX
nLRbwHOoq7hHwg==
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIFazCCA1OgAwIBAgIRAIIQz7DSQONZRGPgu2OCiwAwDQYJKoZIhvcNAQELBQAw
TzELMAkGA1UEBhMCVVMxKTAnBgNVBAoTIEludGVybmV0IFNlY3VyaXR5IFJlc2Vh
cmNoIEdyb3VwMRUwEwYDVQQDEwxJU1JHIFJvb3QgWDEwHhcNMTUwNjA0MTEwNDM4
WhcNMzUwNjA0MTEwNDM4WjBPMQswCQYDVQQGEwJVUzEpMCcGA1UEChMgSW50ZXJu
ZXQgU2VjdXJpdHkgUmVzZWFyY2ggR3JvdXAxFTATBgNVBAMTDElTUkcgUm9vdCBY
MTCCAiIwDQYJKoZIhvcNAQEBBQADggIPADCCAgoCggIBAK3oJHP0FDfzm54rVygc
h77ct984kIxuPOZXoHj3dcKi/vVqbvYATyjb3miGbESTtrFj/RQSa78f0uoxmyF+
0TM8ukj13Xnfs7j/EvEhmkvBioZxaUpmZmyPfjxwv60pIgbz5MDmgK7iS4+3mX6U
A5/TR5d8mUgjU+g4rk8Kb4Mu0UlXjIB0ttov0DiNewNwIRt18jA8+o+u3dpjq+sW
T8KOEUt+zwvo/7V3LvSye0rgTBIlDHCNAymg4VMk7BPZ7hm/ELNKjD+Jo2FR3qyH
B5T0Y3HsLuJvW5iB4YlcNHlsdu87kGJ55tukmi8mxdAQ4Q7e2RCOFvu396j3x+UC
B5iPNgiV5+I3lg02dZ77DnKxHZu8A/lJBdiB3QW0KtZB6awBdpUKD9jf1b0SHzUv
KBds0pjBqAlkd25HN7rOrFleaJ1/ctaJxQZBKT5ZPt0m9STJEadao0xAH0ahmbWn
OlFuhjuefXKnEgV4We0+UXgVCwOPjdAvBbI+e0ocS3MFEvzG6uBQE3xDk3SzynTn
jh8BCNAw1FtxNrQHusEwMFxIt4I7mKZ9YIqioymCzLq9gwQbooMDQaHWBfEbwrbw
qHyGO0aoSCqI3Haadr8faqU9GY/rOPNk3sgrDQoo//fb4hVC1CLQJ13hef4Y53CI
rU7m2Ys6xt0nUW7/vGT1M0NPAgMBAAGjQjBAMA4GA1UdDwEB/wQEAwIBBjAPBgNV
HRMBAf8EBTADAQH/MB0GA1UdDgQWBBR5tFnme7bl5AFzgAiIyBpY9umbbjANBgkq
hkiG9w0BAQsFAAOCAgEAVR9YqbyyqFDQDLHYGmkgJykIrGF1XIpu+ILlaS/V9lZL
ubhzEFnTIZd+50xx+7LSYK05qAvqFyFWhfFQDlnrzuBZ6brJFe+GnY+EgPbk6ZGQ
3BebYhtF8GaV0nxvwuo77x/Py9auJ/GpsMiu/X1+mvoiBOv/2X/qkSsisRcOj/KK
NFtY2PwByVS5uCbMiogziUwthDyC3+6WVwW6LLv3xLfHTjuCvjHIInNzktHCgKQ5
ORAzI4JMPJ+GslWYHb4phowim57iaztXOoJwTdwJx4nLCgdNbOhdjsnvzqvHu7Ur
TkXWStAmzOVyyghqpZXjFaH3pO3JLF+l+/+sKAIuvtd7u+Nxe5AW0wdeRlN8NwdC
jNPElpzVmbUq4JUagEiuTDkHzsxHpFKVK7q4+63SM1N95R1NbdWhscdCb+ZAJzVc
oyi3B43njTOQ5yOf+1CceWxG1bQVs5ZufpsMljq4Ui0/1lvh+wjChP4kqKOJ2qxq
4RgqsahDYVvTH9w7jXbyLeiNdd8XM2w9U/t7y0Ff/9yi0GE44Za4rF2LN9d11TPA
mRGunUHBcnWEvgJBQl9nJEiU0Zsnvgc/ubhPgXRR4Xq37Z0j4r7g1SgEEzwxA57d
emyPxgcYxn/eR44/KJ4EBs+lVDR3veyJm+kXQ99b21/+jh5Xos1AnX5iItreGCc=
-----END CERTIFICATE-----
```
```shell
chown zimbra:zimbra /opt/zimbra/ssl/letsencrypt/*
```
> Verify SSL certificate
```shell
cd /opt/zimbra/ssl/letsencrypt
/opt/zimbra/bin/zmcertmgr verifycrt comm privkey.pem cert.pem chain.pem
```
> Deploy SSL certificate
```shell
cp /opt/zimbra/ssl/letsencrypt/privkey.pem /opt/zimbra/ssl/zimbra/commercial/commercial.key
chown zimbra:zimbra /opt/zimbra/ssl/zimbra/commercial/commercial.key
cd /opt/zimbra/ssl/letsencrypt
/opt/zimbra/bin/zmcertmgr deploycrt comm cert.pem chain.pem
```
> Start zimbra service
```shell
zmcontrol restart
```
