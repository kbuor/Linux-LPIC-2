## THÔNG TIN CHUNG
---
Operating System: `AlmaLinux 9.4 (Seafoam Ocelot) (platform:el9)`

IP Address: `10.10.10.106/24`

Gateway: `10.10.10.10`

Hostname: `ipa.kbuor.io.local`

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
> Cài đặt gói `ipa-server` (nếu sử dụng dns tích hợp thì cài đặt thêm gói `ipa-server-dns`)
```shell
dnf install ipa-server
```
```shell
Last metadata expiration check: 19:59:14 ago on Fri Jun  7 09:58:27 2024.
Dependencies resolved.
==========================================================================================================================================================================================================
 Package                                                           Architecture                     Version                                                     Repository                           Size
==========================================================================================================================================================================================================
Installing:
 ipa-server                                                        x86_64                           4.11.0-10.el9_4                                             appstream                           393 k
Installing dependencies:
 389-ds-base                                                       x86_64                           2.4.5-6.el9_4                                               appstream                           2.7 M
 389-ds-base-libs                                                  x86_64                           2.4.5-6.el9_4                                               appstream                           1.4 M
 ModemManager-glib                                                 x86_64                           1.20.2-1.el9                                                baseos                              337 k
 adobe-source-code-pro-fonts                                       noarch                           2.030.1.050-12.el9.1                                        baseos                              831 k
 adwaita-cursor-theme                                              noarch                           40.1.1-3.el9                                                appstream                           625 k
 adwaita-icon-theme                                                noarch                           40.1.1-3.el9                                                appstream                            11 M
 almalinux-logos-httpd                                             noarch                           90.5.1-1.1.el9                                              appstream                            18 k
 almalinux-logos-ipa                                               noarch                           90.5.1-1.1.el9                                              appstream                            20 k
 alsa-lib                                                          x86_64                           1.2.10-2.el9                                                appstream                           504 k
 apache-commons-cli                                                noarch                           1.4-17.el9                                                  appstream                            70 k
 apache-commons-codec                                              noarch                           1.15-7.el9                                                  appstream                           301 k
 apache-commons-io                                                 noarch                           1:2.8.0-8.el9                                               appstream                           282 k
 apache-commons-lang3                                              noarch                           3.12.0-6.el9                                                appstream                           559 k
 apache-commons-logging                                            noarch                           1.2-29.el9                                                  appstream                            76 k
 apache-commons-net                                                noarch                           3.6-14.el9                                                  appstream                           289 k
 apr                                                               x86_64                           1.7.0-12.el9_3                                              appstream                           122 k
 apr-util                                                          x86_64                           1.6.1-23.el9                                                appstream                            94 k
 apr-util-bdb                                                      x86_64                           1.6.1-23.el9                                                appstream                            12 k
 at-spi2-atk                                                       x86_64                           2.38.0-4.el9                                                appstream                            86 k
 at-spi2-core                                                      x86_64                           2.40.3-1.el9                                                appstream                           176 k
 atk                                                               x86_64                           2.36.0-5.el9                                                appstream                           270 k
 augeas-libs                                                       x86_64                           1.13.0-5.el9                                                appstream                           405 k
 autofs                                                            x86_64                           1:5.1.7-58.el9                                              baseos                              369 k
 avahi-glib                                                        x86_64                           0.8-20.el9                                                  appstream                            14 k
 avahi-libs                                                        x86_64                           0.8-20.el9                                                  baseos                               67 k
 bluez-libs                                                        x86_64                           5.64-2.el9                                                  baseos                               83 k
 bubblewrap                                                        x86_64                           0.4.1-6.el9                                                 baseos                               49 k
 cairo                                                             x86_64                           1.17.4-7.el9                                                appstream                           659 k
 cairo-gobject                                                     x86_64                           1.17.4-7.el9                                                appstream                            18 k
 certmonger                                                        x86_64                           0.79.17-2.el9                                               appstream                           591 k
 checkpolicy                                                       x86_64                           3.6-1.el9                                                   appstream                           351 k
 colord-libs                                                       x86_64                           1.4.5-4.el9                                                 appstream                           228 k
 copy-jdk-configs                                                  noarch                           4.0-3.el9                                                   appstream                            27 k
 cups-libs                                                         x86_64                           1:2.3.3op2-24.el9                                           baseos                              261 k
 cyrus-sasl-gssapi                                                 x86_64                           2.1.27-21.el9                                               baseos                               26 k
 cyrus-sasl-md5                                                    x86_64                           2.1.27-21.el9                                               appstream                            42 k
 cyrus-sasl-plain                                                  x86_64                           2.1.27-21.el9                                               baseos                               23 k
 dbus-tools                                                        x86_64                           1:1.12.20-8.el9                                             baseos                               50 k
 dejavu-sans-fonts                                                 noarch                           2.37-18.el9                                                 baseos                              1.3 M
 ecj                                                               noarch                           1:4.20-16.el9                                               appstream                           1.9 M
 exempi                                                            x86_64                           2.6.0-0.2.20211007gite23c213.el9                            appstream                           524 k
 exiv2-libs                                                        x86_64                           0.27.5-2.el9                                                appstream                           779 k
 fdk-aac-free                                                      x86_64                           2.0.0-8.el9                                                 appstream                           324 k
 flac-libs                                                         x86_64                           1.3.3-10.el9_2.1                                            appstream                           217 k
...
...
...
...
...                                                                                                                                      315/367 
  Verifying        : libipa_hbac-2.9.4-6.el9_4.x86_64                                                                                                                                             316/367 
  Verifying        : libkadm5-1.21.1-1.el9.x86_64                                                                                                                                                 317/367 
  Verifying        : libnfsidmap-1:2.5.4-25.el9.x86_64                                                                                                                                            318/367 
  Verifying        : libpkgconf-1.7.3-10.el9.x86_64                                                                                                                                               319/367 
  Verifying        : libpng-2:1.6.37-12.el9.x86_64                                                                                                                                                320/367 
  Verifying        : libproxy-0.4.15-35.el9.x86_64                                                                                                                                                321/367 
  Verifying        : libsss_autofs-2.9.4-6.el9_4.x86_64                                                                                                                                           322/367 
  Verifying        : libverto-libev-0.3.2-3.el9.x86_64                                                                                                                                            323/367 
  Verifying        : libwbclient-4.19.4-104.el9.x86_64                                                                                                                                            324/367 
  Verifying        : lksctp-tools-1.0.19-3.el9_4.x86_64                                                                                                                                           325/367 
  Verifying        : mailcap-2.1.49-5.el9.noarch                                                                                                                                                  326/367 
  Verifying        : nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                              327/367 
  Verifying        : openldap-clients-2.6.6-3.el9.x86_64                                                                                                                                          328/367 
  Verifying        : pkgconf-1.7.3-10.el9.x86_64                                                                                                                                                  329/367 
  Verifying        : pkgconf-m4-1.7.3-10.el9.noarch                                                                                                                                               330/367 
  Verifying        : pkgconf-pkg-config-1.7.3-10.el9.x86_64                                                                                                                                       331/367 
  Verifying        : polkit-0.117-11.el9.x86_64                                                                                                                                                   332/367 
  Verifying        : polkit-pkla-compat-0.1-21.el9.x86_64                                                                                                                                         333/367 
  Verifying        : python3-cffi-1.14.5-5.el9.x86_64                                                                                                                                             334/367 
  Verifying        : python3-chardet-4.0.0-5.el9.noarch                                                                                                                                           335/367 
  Verifying        : python3-cryptography-36.0.1-4.el9.x86_64                                                                                                                                     336/367 
  Verifying        : python3-decorator-4.4.2-6.el9.noarch                                                                                                                                         337/367 
  Verifying        : python3-dns-2.3.0-2.el9.noarch                                                                                                                                               338/367 
  Verifying        : python3-idna-2.10-7.el9.noarch                                                                                                                                               339/367 
  Verifying        : python3-libipa_hbac-2.9.4-6.el9_4.x86_64                                                                                                                                     340/367 
  Verifying        : python3-ply-3.11-14.el9.noarch                                                                                                                                               341/367 
  Verifying        : python3-pycparser-2.20-6.el9.noarch                                                                                                                                          342/367 
  Verifying        : python3-pysocks-1.7.1-12.el9.noarch                                                                                                                                          343/367 
  Verifying        : python3-pyyaml-5.4.1-6.el9.x86_64                                                                                                                                            344/367 
  Verifying        : python3-requests-2.25.1-8.el9.noarch                                                                                                                                         345/367 
  Verifying        : python3-setools-4.4.4-1.el9.x86_64                                                                                                                                           346/367 
  Verifying        : python3-setuptools-53.0.0-12.el9.noarch                                                                                                                                      347/367 
  Verifying        : python3-sss-2.9.4-6.el9_4.x86_64                                                                                                                                             348/367 
  Verifying        : python3-sss-murmur-2.9.4-6.el9_4.x86_64                                                                                                                                      349/367 
  Verifying        : python3-sssdconfig-2.9.4-6.el9_4.noarch                                                                                                                                      350/367 
  Verifying        : python3-urllib3-1.26.5-5.el9.noarch                                                                                                                                          351/367 
  Verifying        : quota-1:4.06-6.el9.x86_64                                                                                                                                                    352/367 
  Verifying        : quota-nls-1:4.06-6.el9.noarch                                                                                                                                                353/367 
  Verifying        : rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                   354/367 
  Verifying        : samba-client-libs-4.19.4-104.el9.x86_64                                                                                                                                      355/367 
  Verifying        : samba-common-4.19.4-104.el9.noarch                                                                                                                                           356/367 
  Verifying        : samba-common-libs-4.19.4-104.el9.x86_64                                                                                                                                      357/367 
  Verifying        : sssd-common-pac-2.9.4-6.el9_4.x86_64                                                                                                                                         358/367 
  Verifying        : sssd-dbus-2.9.4-6.el9_4.x86_64                                                                                                                                               359/367 
  Verifying        : sssd-ipa-2.9.4-6.el9_4.x86_64                                                                                                                                                360/367 
  Verifying        : sssd-krb5-2.9.4-6.el9_4.x86_64                                                                                                                                               361/367 
  Verifying        : sssd-krb5-common-2.9.4-6.el9_4.x86_64                                                                                                                                        362/367 
  Verifying        : sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                                                                                                                                          363/367 
  Verifying        : sssd-passkey-2.9.4-6.el9_4.x86_64                                                                                                                                            364/367 
  Verifying        : sssd-tools-2.9.4-6.el9_4.x86_64                                                                                                                                              365/367 
  Verifying        : words-3.0-39.el9.noarch                                                                                                                                                      366/367 
  Verifying        : tomcat-native-1:1.2.36-1.el9.x86_64                                                                                                                                          367/367 

Installed:
  389-ds-base-2.4.5-6.el9_4.x86_64                                389-ds-base-libs-2.4.5-6.el9_4.x86_64                             ModemManager-glib-1.20.2-1.el9.x86_64                               
  abattis-cantarell-fonts-0.301-4.el9.noarch                      adobe-source-code-pro-fonts-2.030.1.050-12.el9.1.noarch           adwaita-cursor-theme-40.1.1-3.el9.noarch                            
  adwaita-icon-theme-40.1.1-3.el9.noarch                          almalinux-logos-httpd-90.5.1-1.1.el9.noarch                       almalinux-logos-ipa-90.5.1-1.1.el9.noarch                           
  alsa-lib-1.2.10-2.el9.x86_64                                    apache-commons-cli-1.4-17.el9.noarch                              apache-commons-codec-1.15-7.el9.noarch                              
  apache-commons-io-1:2.8.0-8.el9.noarch                          apache-commons-lang3-3.12.0-6.el9.noarch                          apache-commons-logging-1.2-29.el9.noarch                            
  apache-commons-net-3.6-14.el9.noarch                            apr-1.7.0-12.el9_3.x86_64                                         apr-util-1.6.1-23.el9.x86_64                                        
  apr-util-bdb-1.6.1-23.el9.x86_64                                apr-util-openssl-1.6.1-23.el9.x86_64                              at-spi2-atk-2.38.0-4.el9.x86_64                                     
  at-spi2-core-2.40.3-1.el9.x86_64                                atk-2.36.0-5.el9.x86_64                                           augeas-libs-1.13.0-5.el9.x86_64                                     
  autofs-1:5.1.7-58.el9.x86_64                                    avahi-glib-0.8-20.el9.x86_64                                      avahi-libs-0.8-20.el9.x86_64                                        
  bash-completion-1:2.11-5.el9.noarch                             bluez-libs-5.64-2.el9.x86_64                                      bubblewrap-0.4.1-6.el9.x86_64                                       
  cairo-1.17.4-7.el9.x86_64                                       cairo-gobject-1.17.4-7.el9.x86_64                                 certmonger-0.79.17-2.el9.x86_64                                     
  checkpolicy-3.6-1.el9.x86_64                                    colord-libs-1.4.5-4.el9.x86_64                                    copy-jdk-configs-4.0-3.el9.noarch                                   
  cups-libs-1:2.3.3op2-24.el9.x86_64                              cyrus-sasl-gssapi-2.1.27-21.el9.x86_64                            cyrus-sasl-md5-2.1.27-21.el9.x86_64                                 
  cyrus-sasl-plain-2.1.27-21.el9.x86_64                           dbus-tools-1:1.12.20-8.el9.x86_64                                 dconf-0.40.0-6.el9.x86_64                                           
  dejavu-sans-fonts-2.37-18.el9.noarch                            ecj-1:4.20-16.el9.noarch                                          exempi-2.6.0-0.2.20211007gite23c213.el9.x86_64                      
  exiv2-0.27.5-2.el9.x86_64                                       exiv2-libs-0.27.5-2.el9.x86_64                                    fdk-aac-free-2.0.0-8.el9.x86_64                                     
  flac-libs-1.3.3-10.el9_2.1.x86_64                               flatpak-1.12.8-1.el9.x86_64                                       flatpak-selinux-1.12.8-1.el9.noarch                                 
  flatpak-session-helper-1.12.8-1.el9.x86_64                      fontawesome-fonts-1:4.7.0-13.el9.noarch                           fontconfig-2.14.0-2.el9_1.x86_64                                    
  fonts-filesystem-1:2.0.5-7.el9.1.noarch                         freetype-2.10.4-9.el9.x86_64                                      fribidi-1.0.10-6.el9.2.x86_64                                       
  fuse-2.9.9-15.el9.x86_64                                        gdk-pixbuf2-2.42.6-3.el9.x86_64                                   gdk-pixbuf2-modules-2.42.6-3.el9.x86_64                             
  geoclue2-2.6.0-7.el9.x86_64                                     giflib-5.2.1-9.el9.x86_64                                         glib-networking-2.68.3-3.el9.x86_64                                 
  graphene-1.10.6-2.el9.x86_64                                    graphite2-1.3.14-9.el9.x86_64                                     gsettings-desktop-schemas-40.0-6.el9.x86_64                         
  gsm-1.0.19-6.el9.x86_64                                         gssproxy-0.8.4-6.el9.x86_64                                       gstreamer1-1.22.1-2.el9.x86_64                                      
  gstreamer1-plugins-base-1.22.1-2.el9.x86_64                     gtk-update-icon-cache-3.24.31-2.el9.x86_64                        gtk3-3.24.31-2.el9.x86_64                                           
  harfbuzz-2.7.4-10.el9.x86_64                                    hicolor-icon-theme-0.17-13.el9.noarch                             httpcomponents-client-4.5.13-3.el9.noarch                           
  httpcomponents-core-4.4.13-7.el9.noarch                         httpd-2.4.57-8.el9.x86_64                                         httpd-core-2.4.57-8.el9.x86_64                                      
  httpd-filesystem-2.4.57-8.el9.noarch                            httpd-tools-2.4.57-8.el9.x86_64                                   idm-jss-5.5.0-1.el9.x86_64                                          
  idm-jss-tomcat-5.5.0-1.el9.x86_64                               idm-ldapjdk-5.5.0-1.el9.noarch                                    idm-pki-acme-11.5.0-1.el9.noarch                                    
  idm-pki-base-11.5.0-1.el9.noarch                                idm-pki-ca-11.5.0-1.el9.noarch                                    idm-pki-java-11.5.0-1.el9.noarch                                    
  idm-pki-kra-11.5.0-1.el9.noarch                                 idm-pki-server-11.5.0-1.el9.noarch                                idm-pki-tools-11.5.0-1.el9.x86_64                                   
  ipa-client-4.11.0-10.el9_4.x86_64                               ipa-client-common-4.11.0-10.el9_4.noarch                          ipa-common-4.11.0-10.el9_4.noarch                                   
  ipa-healthcheck-core-0.16-3.el9.noarch                          ipa-selinux-4.11.0-10.el9_4.noarch                                ipa-server-4.11.0-10.el9_4.x86_64                                   
  ipa-server-common-4.11.0-10.el9_4.noarch                        iso-codes-4.6.0-3.el9.noarch                                      jakarta-activation-1.2.2-5.el9.noarch                               
  jakarta-annotations-1.3.5-13.el9.noarch                         java-11-openjdk-headless-1:11.0.23.0.9-3.el9.x86_64               java-17-openjdk-1:17.0.11.0.9-2.el9.x86_64                          
  java-17-openjdk-devel-1:17.0.11.0.9-2.el9.x86_64                java-17-openjdk-headless-1:17.0.11.0.9-2.el9.x86_64               javapackages-filesystem-6.0.0-4.el9.noarch                          
  javapackages-tools-6.0.0-4.el9.noarch                           jaxb-api-2.3.3-5.el9.noarch                                       jbigkit-libs-2.1-23.el9.x86_64                                      
  jboss-jaxrs-2.0-api-1.0.0-16.el9.noarch                         jboss-logging-3.4.1-9.el9.noarch                                  jboss-logging-tools-2.2.1-7.el9.noarch                              
  jdeparser-2.0.3-12.el9.noarch                                   keyutils-1.6.3-1.el9.x86_64                                       krb5-pkinit-1.21.1-1.el9.x86_64                                     
  krb5-server-1.21.1-1.el9.x86_64                                 krb5-workstation-1.21.1-1.el9.x86_64                              langpacks-core-font-en-3.0-16.el9.noarch                            
  lcms2-2.12-3.el9.x86_64                                         libX11-1.7.0-9.el9.x86_64                                         libX11-common-1.7.0-9.el9.noarch                                    
  libX11-xcb-1.7.0-9.el9.x86_64                                   libXau-1.0.9-8.el9.x86_64                                         libXcomposite-0.4.5-7.el9.x86_64                                    
  libXcursor-1.2.0-7.el9.x86_64                                   libXdamage-1.1.5-7.el9.x86_64                                     libXext-1.3.4-8.el9.x86_64                                          
  libXfixes-5.0.3-16.el9.x86_64                                   libXft-2.3.3-8.el9.x86_64                                         libXi-1.7.10-8.el9.x86_64                                           
  libXinerama-1.1.4-10.el9.x86_64                                 libXrandr-1.5.2-8.el9.x86_64                                      libXrender-0.9.10-16.el9.x86_64                                     
  libXtst-1.2.3-16.el9.x86_64                                     libXv-1.0.11-16.el9.x86_64                                        libXxf86vm-1.1.4-18.el9.x86_64                                      
  libappstream-glib-0.7.18-4.el9.x86_64                           libasyncns-0.8-22.el9.x86_64                                      libatomic-11.4.1-3.el9.alma.1.x86_64                                
  libcanberra-0.30-27.el9.x86_64                                  libcanberra-gtk3-0.30-27.el9.x86_64                               libdatrie-0.2.13-4.el9.x86_64                                       
  libdb-utils-5.3.28-53.el9.x86_64                                libepoxy-1.5.5-4.el9.x86_64                                       libev-4.33-5.el9.x86_64                                             
  libexif-0.6.22-6.el9.x86_64                                     libfontenc-1.1.3-17.el9.x86_64                                    libgexiv2-0.12.3-1.el9.x86_64                                       
  libglvnd-1:1.3.4-1.el9.x86_64                                   libglvnd-egl-1:1.3.4-1.el9.x86_64                                 libglvnd-glx-1:1.3.4-1.el9.x86_64                                   
  libgsf-1.14.47-5.el9.x86_64                                     libgxps-0.3.2-3.el9.x86_64                                        libicu-67.1-9.el9.x86_64                                            
  libipa_hbac-2.9.4-6.el9_4.x86_64                                libiptcdata-1.0.5-9.el9.x86_64                                    libjose-11-3.el9.x86_64                                             
  libjpeg-turbo-2.0.90-7.el9.x86_64                               libkadm5-1.21.1-1.el9.x86_64                                      libldac-2.0.2.3-10.el9.x86_64                                       
  libnfsidmap-1:2.5.4-25.el9.x86_64                               libnotify-0.7.9-8.el9.x86_64                                      libnsl2-2.0.0-1.el9.x86_64                                          
  libogg-2:1.3.4-6.el9.x86_64                                     libosinfo-1.10.0-1.el9.x86_64                                     libpkgconf-1.7.3-10.el9.x86_64                                      
  libpng-2:1.6.37-12.el9.x86_64                                   libproxy-0.4.15-35.el9.x86_64                                     libproxy-webkitgtk4-0.4.15-35.el9.x86_64                            
  librsvg2-2.50.7-3.el9.x86_64                                    libsbc-1.4-9.el9.x86_64                                           libsndfile-1.0.31-8.el9.x86_64                                      
  libsoup-2.72.0-8.el9.x86_64                                     libsss_autofs-2.9.4-6.el9_4.x86_64                                libstemmer-0-18.585svn.el9.x86_64                                   
  libthai-0.1.28-8.el9.x86_64                                     libtheora-1:1.1.1-31.el9.x86_64                                   libtiff-4.4.0-12.el9.x86_64                                         
  libtracker-sparql-3.1.2-3.el9_1.x86_64                          libverto-libev-0.3.2-3.el9.x86_64                                 libvisual-1:0.4.0-34.el9.x86_64                                     
  libvorbis-1:1.3.7-5.el9.x86_64                                  libwayland-client-1.21.0-1.el9.x86_64                             libwayland-cursor-1.21.0-1.el9.x86_64                               
  libwayland-egl-1.21.0-1.el9.x86_64                              libwayland-server-1.21.0-1.el9.x86_64                             libwbclient-4.19.4-104.el9.x86_64                                   
  libwebp-1.2.0-8.el9_3.x86_64                                    libxcb-1.13.1-9.el9.x86_64                                        libxkbcommon-1.0.3-4.el9.x86_64                                     
  libxshmfence-1.3-10.el9.x86_64                                  lksctp-tools-1.0.19-3.el9_4.x86_64                                low-memory-monitor-2.1-4.el9.x86_64                                 
  lua-5.4.4-4.el9.x86_64                                          lua-posix-35.0-8.el9.x86_64                                       mailcap-2.1.49-5.el9.noarch                                         
  mesa-libEGL-23.3.3-1.el9.x86_64                                 mesa-libGL-23.3.3-1.el9.x86_64                                    mesa-libgbm-23.3.3-1.el9.x86_64                                     
  mesa-libglapi-23.3.3-1.el9.x86_64                               mkfontscale-1.2.1-3.el9.x86_64                                    mod_auth_gssapi-1.6.3-7.el9.x86_64                                  
  mod_http2-2.0.26-2.el9_4.x86_64                                 mod_lookup_identity-1.0.0-15.el9.x86_64                           mod_lua-2.4.57-8.el9.x86_64                                         
  mod_session-2.4.57-8.el9.x86_64                                 mod_ssl-1:2.4.57-8.el9.x86_64                                     nfs-utils-1:2.5.4-25.el9.x86_64                                     
  nspr-4.35.0-7.el9_4.x86_64                                      nss-3.90.0-7.el9_4.x86_64                                         nss-softokn-3.90.0-7.el9_4.x86_64                                   
  nss-softokn-freebl-3.90.0-7.el9_4.x86_64                        nss-sysinit-3.90.0-7.el9_4.x86_64                                 nss-tools-3.90.0-7.el9_4.x86_64                                     
  nss-util-3.90.0-7.el9_4.x86_64                                  oddjob-0.34.7-7.el9.x86_64                                        oddjob-mkhomedir-0.34.7-7.el9.x86_64                                
  open-sans-fonts-1.10-16.el9.noarch                              openjpeg2-2.4.0-7.el9.x86_64                                      openldap-clients-2.6.6-3.el9.x86_64                                 
  openssl-perl-1:3.0.7-27.el9.x86_64                              opus-1.3.1-10.el9.x86_64                                          orc-0.4.31-6.el9.x86_64                                             
  osinfo-db-20231215-1.el9.noarch                                 osinfo-db-tools-1.10.0-1.el9.x86_64                               ostree-libs-2024.4-3.el9_4.x86_64                                   
  p11-kit-server-0.25.3-2.el9.x86_64                              pango-1.48.7-3.el9.x86_64                                         perl-Algorithm-Diff-1.2010-4.el9.noarch                             
  perl-Archive-Tar-2.38-6.el9.noarch                              perl-Compress-Raw-Bzip2-2.101-5.el9.x86_64                        perl-Compress-Raw-Lzma-2.101-3.el9.x86_64                           
  perl-Compress-Raw-Zlib-2.101-5.el9.x86_64                       perl-DB_File-1.855-4.el9.x86_64                                   perl-Devel-Peek-1.28-481.el9.x86_64                                 
  perl-IO-Compress-2.102-4.el9.noarch                             perl-IO-Compress-Lzma-2.101-4.el9.noarch                          perl-IO-Zlib-1:1.11-4.el9.noarch                                    
  perl-Term-ReadLine-1.17-481.el9.noarch                          perl-Text-Diff-1.45-13.el9.noarch                                 perl-Tie-4.6-481.el9.noarch                                         
  perl-debugger-1.56-481.el9.noarch                               perl-meta-notation-5.32.1-481.el9.noarch                          perl-sigtrap-1.09-481.el9.noarch                                    
  perl-threads-1:2.25-460.el9.x86_64                              perl-threads-shared-1.61-460.el9.x86_64                           pipewire-1.0.1-1.el9.x86_64                                         
  pipewire-alsa-1.0.1-1.el9.x86_64                                pipewire-jack-audio-connection-kit-1.0.1-1.el9.x86_64             pipewire-jack-audio-connection-kit-libs-1.0.1-1.el9.x86_64          
  pipewire-libs-1.0.1-1.el9.x86_64                                pipewire-pulseaudio-1.0.1-1.el9.x86_64                            pixman-0.40.0-6.el9_3.x86_64                                        
  pkgconf-1.7.3-10.el9.x86_64                                     pkgconf-m4-1.7.3-10.el9.noarch                                    pkgconf-pkg-config-1.7.3-10.el9.x86_64                              
  pki-jackson-annotations-2.14.1-1.el9.noarch                     pki-jackson-core-2.14.1-2.el9.noarch                              pki-jackson-databind-2.14.1-2.el9.noarch                            
  pki-jackson-jaxrs-json-provider-2.14.1-2.el9.noarch             pki-jackson-jaxrs-providers-2.14.1-2.el9.noarch                   pki-jackson-module-jaxb-annotations-2.14.1-2.el9.noarch             
  pki-resteasy-client-3.0.26-19.el9.noarch                        pki-resteasy-core-3.0.26-19.el9.noarch                            pki-resteasy-jackson2-provider-3.0.26-19.el9.noarch                 
  pki-resteasy-servlet-initializer-3.0.26-19.el9.noarch           policycoreutils-python-utils-3.6-2.1.el9.noarch                   polkit-0.117-11.el9.x86_64                                          
  polkit-pkla-compat-0.1-21.el9.x86_64                            poppler-21.01.0-19.el9.x86_64                                     poppler-data-0.4.9-9.el9.noarch                                     
  poppler-glib-21.01.0-19.el9.x86_64                              publicsuffix-list-20210518-3.el9.noarch                           pulseaudio-libs-15.0-2.el9.x86_64                                   
  python3-argcomplete-1.12.0-5.el9.noarch                         python3-audit-3.1.2-2.el9.x86_64                                  python3-augeas-0.5.0-25.el9.noarch                                  
  python3-babel-2.9.1-2.el9.noarch                                python3-cffi-1.14.5-5.el9.x86_64                                  python3-chardet-4.0.0-5.el9.noarch                                  
  python3-cryptography-36.0.1-4.el9.x86_64                        python3-decorator-4.4.2-6.el9.noarch                              python3-distro-1.5.0-7.el9.noarch                                   
  python3-dns-2.3.0-2.el9.noarch                                  python3-gssapi-1.6.9-5.el9.x86_64                                 python3-idm-pki-11.5.0-1.el9.noarch                                 
  python3-idna-2.10-7.el9.noarch                                  python3-ipaclient-4.11.0-10.el9_4.noarch                          python3-ipalib-4.11.0-10.el9_4.noarch                               
  python3-ipaserver-4.11.0-10.el9_4.noarch                        python3-jinja2-2.11.3-5.el9.noarch                                python3-jwcrypto-0.8-5.el9_4.noarch                                 
  python3-kdcproxy-1.0.0-7.el9.noarch                             python3-ldap-3.4.3-2.el9.x86_64                                   python3-lib389-2.4.5-6.el9_4.noarch                                 
  python3-libipa_hbac-2.9.4-6.el9_4.x86_64                        python3-libsemanage-3.6-1.el9.x86_64                              python3-lxml-4.6.5-3.el9.x86_64                                     
  python3-markupsafe-1.1.1-12.el9.x86_64                          python3-mod_wsgi-4.7.1-11.el9.x86_64                              python3-netaddr-0.8.0-5.el9.noarch                                  
  python3-netifaces-0.10.6-15.el9.x86_64                          python3-ply-3.11-14.el9.noarch                                    python3-policycoreutils-3.6-2.1.el9.noarch                          
  python3-psutil-5.8.0-12.el9.x86_64                              python3-pyasn1-0.4.8-6.el9.noarch                                 python3-pyasn1-modules-0.4.8-6.el9.noarch                           
  python3-pycparser-2.20-6.el9.noarch                             python3-pysocks-1.7.1-12.el9.noarch                               python3-pytz-2021.1-5.el9.noarch                                    
  python3-pyusb-1.0.2-13.el9.noarch                               python3-pyyaml-5.4.1-6.el9.x86_64                                 python3-qrcode-core-6.1-12.el9.noarch                               
  python3-requests-2.25.1-8.el9.noarch                            python3-setools-4.4.4-1.el9.x86_64                                python3-setuptools-53.0.0-12.el9.noarch                             
  python3-sss-2.9.4-6.el9_4.x86_64                                python3-sss-murmur-2.9.4-6.el9_4.x86_64                           python3-sssdconfig-2.9.4-6.el9_4.noarch                             
  python3-urllib3-1.26.5-5.el9.noarch                             python3-yubico-1.3.3-7.el9.noarch                                 quota-1:4.06-6.el9.x86_64                                           
  quota-nls-1:4.06-6.el9.noarch                                   rpcbind-1.2.6-7.el9.x86_64                                        rtkit-0.11-28.el9.x86_64                                            
  samba-client-libs-4.19.4-104.el9.x86_64                         samba-common-4.19.4-104.el9.noarch                                samba-common-libs-4.19.4-104.el9.x86_64                             
  slapi-nis-0.60.0-5.el9_3.x86_64                                 slf4j-1.7.30-13.el9.noarch                                        slf4j-jdk14-1.7.30-13.el9.noarch                                    
  softhsm-2.6.1-7.el9.2.x86_64                                    sound-theme-freedesktop-0.8-17.el9.noarch                         sscg-3.0.0-7.el9.x86_64                                             
  sssd-common-pac-2.9.4-6.el9_4.x86_64                            sssd-dbus-2.9.4-6.el9_4.x86_64                                    sssd-idp-2.9.4-6.el9_4.x86_64                                       
  sssd-ipa-2.9.4-6.el9_4.x86_64                                   sssd-krb5-2.9.4-6.el9_4.x86_64                                    sssd-krb5-common-2.9.4-6.el9_4.x86_64                               
  sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                             sssd-passkey-2.9.4-6.el9_4.x86_64                                 sssd-tools-2.9.4-6.el9_4.x86_64                                     
  tomcat-1:9.0.87-1.el9_4.1.noarch                                tomcat-el-3.0-api-1:9.0.87-1.el9_4.1.noarch                       tomcat-jsp-2.3-api-1:9.0.87-1.el9_4.1.noarch                        
  tomcat-lib-1:9.0.87-1.el9_4.1.noarch                            tomcat-native-1:1.2.36-1.el9.x86_64                               tomcat-servlet-4.0-api-1:9.0.87-1.el9_4.1.noarch                    
  totem-pl-parser-3.26.6-2.el9.x86_64                             tracker-3.1.2-3.el9_1.x86_64                                      tracker-miners-3.1.2-4.el9_3.x86_64                                 
  ttmkfdir-3.0.9-65.el9.x86_64                                    tzdata-java-2024a-1.el9.noarch                                    upower-0.99.13-2.el9.x86_64                                         
  webkit2gtk3-jsc-2.42.5-1.el9.x86_64                             webrtc-audio-processing-0.3.1-8.el9.x86_64                        wireplumber-0.4.14-1.el9.x86_64                                     
  wireplumber-libs-0.4.14-1.el9.x86_64                            words-3.0-39.el9.noarch                                           xdg-dbus-proxy-0.1.3-1.el9.x86_64                                   
  xdg-desktop-portal-1.12.6-1.el9.x86_64                          xdg-desktop-portal-gtk-1.12.0-3.el9.x86_64                        xkeyboard-config-2.33-2.el9.noarch                                  
  xml-common-0.6.3-58.el9.noarch                                  xml-commons-apis-1.4.01-36.el9.noarch                             xml-commons-resolver-1.2-36.el9.noarch                              
  xorg-x11-fonts-Type1-7.5-33.el9.noarch                         

Complete!
```
> Bootstrap IPA Server
```shell
ipa-server-install
```
> Lựa chọn sử dụng DNS tích hợp hoặc DNS bên ngoài
```shell
The log file for this installation can be found in /var/log/ipaserver-install.log
==============================================================================
This program will set up the IPA Server.
Version 4.11.0

This includes:
  * Configure a stand-alone CA (dogtag) for certificate management
  * Configure the NTP client (chronyd)
  * Create and configure an instance of Directory Server
  * Create and configure a Kerberos Key Distribution Center (KDC)
  * Configure Apache (httpd)
  * Configure SID generation
  * Configure the KDC to enable PKINIT

To accept the default shown in brackets, press the Enter key.

Do you want to configure integrated DNS (BIND)? [no]:
```
> Set hostname cho IPA server
```shell
Do you want to configure integrated DNS (BIND)? [no]: no

Enter the fully qualified domain name of the computer
on which you're setting up server software. Using the form
<hostname>.<domainname>
Example: master.example.com


Server host name [ipa.kbuor.io.local]:
```
> Xác nhận domain name sẽ sử dụng
```shell
Server host name [ipa.kbuor.io.local]: ipa.kbuor.io.local

The domain name has been determined based on the host name.

Please confirm the domain name [kbuor.io.local]:
```
> Đặt `REALM NAME` sẽ sử dụng, thông thường `REALM NAME` sẽ là domain name viết hoa.
```shell
Please confirm the domain name [kbuor.io.local]: kbuor.io.local

The kerberos protocol requires a Realm name to be defined.
This is typically the domain name converted to uppercase.

Please provide a realm name [KBUOR.IO.LOCAL]:
```
> Đặt password cho Directory Manager (quản lý user)
```shell
Please provide a realm name [KBUOR.IO.LOCAL]: KBUOR.IO.LOCAL
Certain directory server operations require an administrative user.
This user is referred to as the Directory Manager and has full access
to the Directory for system management tasks and will be added to the
instance of directory server created for IPA.
The password must be at least 8 characters long.

Directory Manager password: 
```
> Đặt password cho user admin của IPA
```shell
Directory Manager password: 
Password (confirm): 

The IPA server requires an administrative user, named 'admin'.
This user is a regular system account used for IPA server administration.

IPA admin password:
```
> Đặt NetBIOS name cho domain (tên ngắn gọn của domain)
```shell
IPA admin password: 
Password (confirm): 

Trust is configured but no NetBIOS domain name found, setting it now.
Enter the NetBIOS name for the IPA domain.
Only up to 15 uppercase ASCII letters, digits and dashes are allowed.
Example: EXAMPLE.


NetBIOS domain name [KBUOR]:
```
> Cấu hình NTP Server
```shell
NetBIOS domain name [KBUOR]: KBUOR

Do you want to configure chrony with NTP server or pool address? [no]: yes
Enter NTP source server addresses separated by comma, or press Enter to skip: 0.asia.pool.ntp.org
Enter a NTP source pool address, or press Enter to skip:
```
> Kiểm tra thông tin và xác nhận
```shell
The IPA Master Server will be configured with:
Hostname:       ipa.kbuor.io.local
IP address(es): 10.10.10.105
Domain name:    kbuor.io.local
Realm name:     KBUOR.IO.LOCAL

The CA will be configured with:
Subject DN:   CN=Certificate Authority,O=KBUOR.IO.LOCAL
Subject base: O=KBUOR.IO.LOCAL
Chaining:     self-signed

NTP server:     0.asia.pool.ntp.org
Continue to configure the system with these values? [no]:
```
> Quá trình cài đặt diễn ra và hoàn tất
```shell
...
...
...
  [4/8]: updating Kerberos config
'dns_lookup_kdc' already set to 'true', nothing to do.
  [5/8]: activating sidgen task
  [6/8]: restarting Directory Server to take MS PAC and LDAP plugins changes into account
  [7/8]: adding fallback group
  [8/8]: adding SIDs to existing users and groups
This step may take considerable amount of time, please wait..
Done.
Configuring client side components
This program will set up IPA client.
Version 4.11.0

Using existing certificate '/etc/ipa/ca.crt'.
Client hostname: ipa.kbuor.io.local
Realm: KBUOR.IO.LOCAL
DNS Domain: kbuor.io.local
IPA Server: ipa.kbuor.io.local
BaseDN: dc=kbuor,dc=io,dc=local

Configured /etc/sssd/sssd.conf
Systemwide CA database updated.
Adding SSH public key from /etc/ssh/ssh_host_ed25519_key.pub
Adding SSH public key from /etc/ssh/ssh_host_ecdsa_key.pub
Adding SSH public key from /etc/ssh/ssh_host_rsa_key.pub
Could not update DNS SSHFP records.
SSSD enabled
Configured /etc/openldap/ldap.conf
Configured /etc/ssh/ssh_config
Configured /etc/ssh/sshd_config.d/04-ipa.conf
Configuring kbuor.io.local as NIS domain.
Client configuration complete.
The ipa-client-install command was successful

Please add records in this file to your DNS system: /tmp/ipa.system.records.3l9i8elg.db
==============================================================================
Setup complete

Next steps:
        1. You must make sure these network ports are open:
                TCP Ports:
                  * 80, 443: HTTP/HTTPS
                  * 389, 636: LDAP/LDAPS
                  * 88, 464: kerberos
                UDP Ports:
                  * 88, 464: kerberos
                  * 123: ntp

        2. You can now obtain a kerberos ticket using the command: 'kinit admin'
           This ticket will allow you to use the IPA tools (e.g., ipa user-add)
           and the web user interface.

Be sure to back up the CA certificates stored in /root/cacert.p12
These files are required to create replicas. The password for these
files is the Directory Manager password
The ipa-server-install command was successful
```
> Cập nhập các dns record được liệt kê trong file `Please add records in this file to your DNS system: /tmp/ipa.system.records.3l9i8elg.db` vào DNS Server
```shell
cat /tmp/ipa.system.records.3l9i8elg.db
```
```shell
_kerberos-master._tcp.kbuor.io.local. 3600 IN SRV 0 100 88 ipa.kbuor.io.local.
_kerberos-master._udp.kbuor.io.local. 3600 IN SRV 0 100 88 ipa.kbuor.io.local.
_kerberos._tcp.kbuor.io.local. 3600 IN SRV 0 100 88 ipa.kbuor.io.local.
_kerberos._udp.kbuor.io.local. 3600 IN SRV 0 100 88 ipa.kbuor.io.local.
_kerberos.kbuor.io.local. 3600 IN TXT "KBUOR.IO.LOCAL"
_kerberos.kbuor.io.local. 3600 IN URI 0 100 "krb5srv:m:tcp:ipa.kbuor.io.local."
_kerberos.kbuor.io.local. 3600 IN URI 0 100 "krb5srv:m:udp:ipa.kbuor.io.local."
_kpasswd._tcp.kbuor.io.local. 3600 IN SRV 0 100 464 ipa.kbuor.io.local.
_kpasswd._udp.kbuor.io.local. 3600 IN SRV 0 100 464 ipa.kbuor.io.local.
_kpasswd.kbuor.io.local. 3600 IN URI 0 100 "krb5srv:m:tcp:ipa.kbuor.io.local."
_kpasswd.kbuor.io.local. 3600 IN URI 0 100 "krb5srv:m:udp:ipa.kbuor.io.local."
_ldap._tcp.kbuor.io.local. 3600 IN SRV 0 100 389 ipa.kbuor.io.local.
ipa-ca.kbuor.io.local. 3600 IN A 10.10.10.105
```
> Hoàn tất quá trình cài đặt

## CÁC TÁC VỤ THƯỜNG DÙNG VỚI IPA SERVER
---
> Khởi tạo Kerberos Ticket
```shell
kinit admin
```
```shell
Password for admin@KBUOR.IO.LOCAL:
```
> Kiểm tra các Kerberos Ticket hiện có
```shell
klist
```
```shell
Ticket cache: KCM:0
Default principal: admin@KBUOR.IO.LOCAL

Valid starting     Expires            Service principal
06/08/24 06:37:29  06/09/24 06:18:08  krbtgt/KBUOR.IO.LOCAL@KBUOR.IO.LOCAL
```
> Hủy ticket
```shell
kdestroy
```
> Thay đổi shell mặc định cho các IPA user sử dụng /bin/bash
```shell
ipa config-mod --defaultshell=/bin/bash
```
```shell
Maximum username length: 32
Maximum hostname length: 64
Home directory base: /home
Default shell: /bin/bash
Default users group: ipausers
Default e-mail domain: kbuor.io.local
Search time limit: 2
Search size limit: 100
User search fields: uid,givenname,sn,telephonenumber,ou,title
Group search fields: cn,description
Enable migration mode: False
Certificate Subject base: O=KBUOR.IO.LOCAL
Password Expiration Notification (days): 4
Password plugin features: AllowNThash, KDC:Disable Last Success
SELinux user map order: guest_u:s0$xguest_u:s0$user_u:s0$staff_u:s0-s0:c0.c1023$sysadm_u:s0-s0:c0.c1023$unconfined_u:s0-s0:c0.c1023
Default SELinux user: unconfined_u:s0-s0:c0.c1023
Default PAC types: MS-PAC, nfs:NONE
IPA masters: ipa.kbuor.io.local
IPA master capable of PKINIT: ipa.kbuor.io.local
IPA CA servers: ipa.kbuor.io.local
IPA CA renewal master: ipa.kbuor.io.local
```
> Kiểm tra configure của ipa
```shell
ipa config-show
```
```shell
Maximum username length: 32
Maximum hostname length: 64
Home directory base: /home
Default shell: /bin/bash
Default users group: ipausers
Default e-mail domain: kbuor.io.local
Search time limit: 2
Search size limit: 100
User search fields: uid,givenname,sn,telephonenumber,ou,title
Group search fields: cn,description
Enable migration mode: False
Certificate Subject base: O=KBUOR.IO.LOCAL
Password Expiration Notification (days): 4
Password plugin features: AllowNThash, KDC:Disable Last Success
SELinux user map order: guest_u:s0$xguest_u:s0$user_u:s0$staff_u:s0-s0:c0.c1023$sysadm_u:s0-s0:c0.c1023$unconfined_u:s0-s0:c0.c1023
Default SELinux user: unconfined_u:s0-s0:c0.c1023
Default PAC types: MS-PAC, nfs:NONE
IPA masters: ipa.kbuor.io.local
IPA master capable of PKINIT: ipa.kbuor.io.local
IPA CA servers: ipa.kbuor.io.local
IPA CA renewal master: ipa.kbuor.io.local
```
> Add a FreeIPA user account
```shell
ipa user-add robusta --first=Robusta --last=HCM --password
```

> Lock or unlock a FreeIPA user
```shell
ipa user-disable robusta
ipa user-enable robusta
```

> Serch a FreeIPA user
```shell
ipa user-find robusta
ipa user-show --raw robusta
```

> Delete a FreeIPA user
```shell
ipa user-del robusta
```

> Add a FreeIPA group
```shell
ipa group-add --desc='Robusta Group' robusgroup
```

> Add members in a FreeIPA group
```shell
ipa group-add-member --users=robusta,kbuor robusgroup
```

> Add a group in a FreeIPA group
```shell
ipa group-add-member --groups=robustahcm robusgroup
```

> Search a FreeIPA group
```shell
ipa group-find robusgroup
```

> Delete a FreeIPA group
```shell
ipa group-del robusgroup
```
## JOIN CLIENT TO IPA SERVER
---
Operating System: `AlmaLinux 9.4 (Seafoam Ocelot) (platform:el9)`

IP Address: `10.10.10.107/24`

Gateway: `10.10.10.10`

Hostname: `client01.kbuor.io.local`

Domain: `kbuor.io.local`

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
> LƯU Ý: Tạo DNS record (A và PTR) cho client trước khi tiếp tục

> Configure FreeIPA Client
```shell
yum install -y ipa-client
ipa-client-install --force-ntpd
```
```shell
        Discovery was successful!
        Client hostname: client01.kbuor.io.local
        Realm: KBUOR.IO.LOCAL
        DNS Domain: kbuor.io.local
        IPA Server: ipa.kbuor.io.local
        BaseDN: dc=kbuor,dc=io,dc=local

        # confirm settings and proceed with [yes]
        Continue to configure the system with these values? [no]: yes

        Synchronizing time with KDC...
        Attempting to sync time using ntpd.  Will timeout after 15 seconds
        # answer with admin
        User authorized to enroll computers: admin
        Password for admin@KBUOR.IO.LOCAL:
        Successfully retrieved CA cert
            Subject:     CN=Certificate Authority,O=KBUOR.IO.LOCAL
            Issuer:      CN=Certificate Authority,O=KBUOR.IO.LOCAL
            Valid From:  2024-06-07 10:44:32
            Valid Until: 2030-10-07 10:44:32

        Enrolled in IPA realm KBUOR.IO.LOCAL
        Created /etc/ipa/default.conf
        New SSSD config will be created
        Configured sudoers in /etc/nsswitch.conf
        Configured /etc/sssd/sssd.conf
        Configured /etc/krb5.conf for IPA realm KBUOR.IO.LOCAL
        trying https://ipa.kbuor.io.local/ipa/json
        [try 1]: Forwarding 'schema' to json server 'https://ipa.kbuor.io.local/ipa/json'
        trying https://ipa.kbuor.io.local/ipa/session/json
        [try 1]: Forwarding 'ping' to json server 'https://ipa.kbuor.io.local/ipa/session/json'
        [try 1]: Forwarding 'ca_is_enabled' to json server 'https://ipa.kbuor.io.local/ipa/session/json'
        Systemwide CA database updated.
        Adding SSH public key from /etc/ssh/ssh_host_rsa_key.pub
        Adding SSH public key from /etc/ssh/ssh_host_ecdsa_key.pub
        Adding SSH public key from /etc/ssh/ssh_host_ed25519_key.pub
        [try 1]: Forwarding 'host_mod' to json server 'https://ipa.kbuor.io.local/ipa/session/json'
        Could not update DNS SSHFP records.
        SSSD enabled
        Configured /etc/openldap/ldap.conf
        NTP enabled
        Configured /etc/ssh/ssh_config
        Configured /etc/ssh/sshd_config
        Configuring kbuor.local as NIS domain.
        Client configuration complete.
        The ipa-client-install command was successful
```
> Enable home directory cho IPA user
```shell
authselect enable-feature with-mkhomedir
systemctl enable --now oddjobd
```
---
> Set quyền Sudo cho IPA user

### Thực hiện trên IPA server

> Khởi tạo vé chứng thực:
```shell
kinit admin
```
> Thêm người dùng mới (nếu cần):
```shell
ipa user-add kbuor --first=New --last=User --password
```
> Tạo Sudo Rule và gán quyền:
```shell
ipa sudorule-add sudo_for_newuser --cmdcat=all --hostcat=all
ipa sudorule-add-user --users=kbuor sudo_for_newuser
```

### Thực hiện trên máy Client

> Cấu hình sssd và sudo trên các máy trạm

> Sửa file `/etc/sssd/sssd.conf`
```shell
[domain/yourdomain]
...
sudo_provider = ipa
```
> Sửa file `/etc/nsswitch.conf`
```shell
sudoers: files sss
```
> Khởi động lại dịch vụ sssd:
```shell
sudo systemctl restart sssd
```
