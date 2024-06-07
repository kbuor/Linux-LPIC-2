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
 flatpak-selinux                                                   noarch                           1.12.8-1.el9                                                appstream                            20 k
 flatpak-session-helper                                            x86_64                           1.12.8-1.el9                                                appstream                            73 k
 fontawesome-fonts                                                 noarch                           1:4.7.0-13.el9                                              appstream                           204 k
 fontconfig                                                        x86_64                           2.14.0-2.el9_1                                              appstream                           274 k
 fonts-filesystem                                                  noarch                           1:2.0.5-7.el9.1                                             baseos                              9.0 k
 freetype                                                          x86_64                           2.10.4-9.el9                                                baseos                              387 k
 fribidi                                                           x86_64                           1.0.10-6.el9.2                                              appstream                            84 k
 fuse                                                              x86_64                           2.9.9-15.el9                                                baseos                               79 k
 gdk-pixbuf2                                                       x86_64                           2.42.6-3.el9                                                appstream                           466 k
 gdk-pixbuf2-modules                                               x86_64                           2.42.6-3.el9                                                appstream                            84 k
 geoclue2                                                          x86_64                           2.6.0-7.el9                                                 appstream                           122 k
 giflib                                                            x86_64                           5.2.1-9.el9                                                 appstream                            47 k
 glib-networking                                                   x86_64                           2.68.3-3.el9                                                baseos                              169 k
 graphene                                                          x86_64                           1.10.6-2.el9                                                appstream                            63 k
 graphite2                                                         x86_64                           1.3.14-9.el9                                                baseos                               94 k
 gsettings-desktop-schemas                                         x86_64                           40.0-6.el9                                                  baseos                              666 k
 gsm                                                               x86_64                           1.0.19-6.el9                                                appstream                            33 k
 gssproxy                                                          x86_64                           0.8.4-6.el9                                                 baseos                              108 k
 gstreamer1                                                        x86_64                           1.22.1-2.el9                                                appstream                           1.4 M
 gstreamer1-plugins-base                                           x86_64                           1.22.1-2.el9                                                appstream                           2.2 M
 gtk-update-icon-cache                                             x86_64                           3.24.31-2.el9                                               appstream                            34 k
 harfbuzz                                                          x86_64                           2.7.4-10.el9                                                baseos                              623 k
 hicolor-icon-theme                                                noarch                           0.17-13.el9                                                 appstream                            65 k
 httpcomponents-client                                             noarch                           4.5.13-3.el9                                                appstream                           657 k
 httpcomponents-core                                               noarch                           4.4.13-7.el9                                                appstream                           633 k
 httpd                                                             x86_64                           2.4.57-8.el9                                                appstream                            45 k
 httpd-core                                                        x86_64                           2.4.57-8.el9                                                appstream                           1.4 M
 httpd-filesystem                                                  noarch                           2.4.57-8.el9                                                appstream                            12 k
 httpd-tools                                                       x86_64                           2.4.57-8.el9                                                appstream                            80 k
 idm-jss                                                           x86_64                           5.5.0-1.el9                                                 appstream                           1.4 M
 idm-jss-tomcat                                                    x86_64                           5.5.0-1.el9                                                 appstream                            39 k
 idm-ldapjdk                                                       noarch                           5.5.0-1.el9                                                 appstream                           467 k
 idm-pki-acme                                                      noarch                           11.5.0-1.el9                                                appstream                           184 k
 idm-pki-base                                                      noarch                           11.5.0-1.el9                                                appstream                           257 k
 idm-pki-ca                                                        noarch                           11.5.0-1.el9                                                appstream                           1.9 M
 idm-pki-java                                                      noarch                           11.5.0-1.el9                                                appstream                           714 k
 idm-pki-kra                                                       noarch                           11.5.0-1.el9                                                appstream                           341 k
 idm-pki-server                                                    noarch                           11.5.0-1.el9                                                appstream                           3.3 M
 idm-pki-tools                                                     x86_64                           11.5.0-1.el9                                                appstream                           969 k
 ipa-client                                                        x86_64                           4.11.0-10.el9_4                                             appstream                           126 k
 ipa-client-common                                                 noarch                           4.11.0-10.el9_4                                             appstream                            41 k
 ipa-common                                                        noarch                           4.11.0-10.el9_4                                             appstream                           652 k
 ipa-healthcheck-core                                              noarch                           0.16-3.el9                                                  appstream                            56 k
 ipa-selinux                                                       noarch                           4.11.0-10.el9_4                                             appstream                            35 k
 ipa-server-common                                                 noarch                           4.11.0-10.el9_4                                             appstream                           443 k
 iso-codes                                                         noarch                           4.6.0-3.el9                                                 appstream                           3.3 M
 jakarta-activation                                                noarch                           1.2.2-5.el9                                                 appstream                            78 k
 jakarta-annotations                                               noarch                           1.3.5-13.el9                                                appstream                            44 k
 java-11-openjdk-headless                                          x86_64                           1:11.0.23.0.9-3.el9                                         appstream                            40 M
 java-17-openjdk                                                   x86_64                           1:17.0.11.0.9-2.el9                                         appstream                           429 k
 java-17-openjdk-devel                                             x86_64                           1:17.0.11.0.9-2.el9                                         appstream                           4.7 M
 java-17-openjdk-headless                                          x86_64                           1:17.0.11.0.9-2.el9                                         appstream                            45 M
 javapackages-filesystem                                           noarch                           6.0.0-4.el9                                                 appstream                            10 k
 javapackages-tools                                                noarch                           6.0.0-4.el9                                                 appstream                            24 k
 jaxb-api                                                          noarch                           2.3.3-5.el9                                                 appstream                           108 k
 jbigkit-libs                                                      x86_64                           2.1-23.el9                                                  appstream                            52 k
 jboss-jaxrs-2.0-api                                               noarch                           1.0.0-16.el9                                                appstream                           111 k
 jboss-logging                                                     noarch                           3.4.1-9.el9                                                 appstream                            57 k
 jboss-logging-tools                                               noarch                           2.2.1-7.el9                                                 appstream                           220 k
 jdeparser                                                         noarch                           2.0.3-12.el9                                                appstream                           216 k
 keyutils                                                          x86_64                           1.6.3-1.el9                                                 baseos                               71 k
 krb5-pkinit                                                       x86_64                           1.21.1-1.el9                                                baseos                               59 k
 krb5-server                                                       x86_64                           1.21.1-1.el9                                                baseos                              293 k
 krb5-workstation                                                  x86_64                           1.21.1-1.el9                                                baseos                              496 k
 langpacks-core-font-en                                            noarch                           3.0-16.el9                                                  appstream                           9.4 k
 lcms2                                                             x86_64                           2.12-3.el9                                                  appstream                           166 k
 libX11                                                            x86_64                           1.7.0-9.el9                                                 appstream                           645 k
 libX11-common                                                     noarch                           1.7.0-9.el9                                                 appstream                           151 k
 libX11-xcb                                                        x86_64                           1.7.0-9.el9                                                 appstream                           9.9 k
 libXau                                                            x86_64                           1.0.9-8.el9                                                 appstream                            30 k
 libXcomposite                                                     x86_64                           0.4.5-7.el9                                                 appstream                            23 k
 libXcursor                                                        x86_64                           1.2.0-7.el9                                                 appstream                            30 k
 libXdamage                                                        x86_64                           1.1.5-7.el9                                                 appstream                            22 k
 libXext                                                           x86_64                           1.3.4-8.el9                                                 appstream                            39 k
 libXfixes                                                         x86_64                           5.0.3-16.el9                                                appstream                            19 k
 libXft                                                            x86_64                           2.3.3-8.el9                                                 appstream                            61 k
 libXi                                                             x86_64                           1.7.10-8.el9                                                appstream                            39 k
 libXinerama                                                       x86_64                           1.1.4-10.el9                                                appstream                            14 k
 libXrandr                                                         x86_64                           1.5.2-8.el9                                                 appstream                            27 k
 libXrender                                                        x86_64                           0.9.10-16.el9                                               appstream                            27 k
 libXtst                                                           x86_64                           1.2.3-16.el9                                                appstream                            20 k
 libXv                                                             x86_64                           1.0.11-16.el9                                               appstream                            18 k
 libXxf86vm                                                        x86_64                           1.1.4-18.el9                                                appstream                            18 k
 libappstream-glib                                                 x86_64                           0.7.18-4.el9                                                appstream                           388 k
 libasyncns                                                        x86_64                           0.8-22.el9                                                  appstream                            29 k
 libatomic                                                         x86_64                           11.4.1-3.el9.alma.1                                         baseos                               30 k
 libcanberra                                                       x86_64                           0.30-27.el9                                                 appstream                            85 k
 libdatrie                                                         x86_64                           0.2.13-4.el9                                                appstream                            32 k
 libdb-utils                                                       x86_64                           5.3.28-53.el9                                               appstream                           131 k
 libepoxy                                                          x86_64                           1.5.5-4.el9                                                 appstream                           242 k
 libev                                                             x86_64                           4.33-5.el9                                                  baseos                               52 k
 libexif                                                           x86_64                           0.6.22-6.el9                                                appstream                           430 k
 libfontenc                                                        x86_64                           1.1.3-17.el9                                                appstream                            30 k
 libgexiv2                                                         x86_64                           0.12.3-1.el9                                                appstream                            82 k
 libglvnd                                                          x86_64                           1:1.3.4-1.el9                                               appstream                           134 k
 libglvnd-egl                                                      x86_64                           1:1.3.4-1.el9                                               appstream                            36 k
 libglvnd-glx                                                      x86_64                           1:1.3.4-1.el9                                               appstream                           144 k
 libgsf                                                            x86_64                           1.14.47-5.el9                                               appstream                           245 k
 libgxps                                                           x86_64                           0.3.2-3.el9                                                 appstream                            78 k
 libicu                                                            x86_64                           67.1-9.el9                                                  baseos                              9.6 M
 libipa_hbac                                                       x86_64                           2.9.4-6.el9_4                                               baseos                               39 k
 libiptcdata                                                       x86_64                           1.0.5-9.el9                                                 appstream                            61 k
 libjose                                                           x86_64                           11-3.el9                                                    appstream                            64 k
 libjpeg-turbo                                                     x86_64                           2.0.90-7.el9                                                appstream                           174 k
 libkadm5                                                          x86_64                           1.21.1-1.el9                                                baseos                               77 k
 libldac                                                           x86_64                           2.0.2.3-10.el9                                              appstream                            40 k
 libnfsidmap                                                       x86_64                           1:2.5.4-25.el9                                              baseos                               60 k
 libnotify                                                         x86_64                           0.7.9-8.el9                                                 appstream                            43 k
 libnsl2                                                           x86_64                           2.0.0-1.el9                                                 appstream                            30 k
 libogg                                                            x86_64                           2:1.3.4-6.el9                                               appstream                            32 k
 libosinfo                                                         x86_64                           1.10.0-1.el9                                                appstream                           312 k
 libpkgconf                                                        x86_64                           1.7.3-10.el9                                                baseos                               35 k
 libpng                                                            x86_64                           2:1.6.37-12.el9                                             baseos                              116 k
 libproxy                                                          x86_64                           0.4.15-35.el9                                               baseos                               73 k
 librsvg2                                                          x86_64                           2.50.7-3.el9                                                appstream                           3.2 M
 libsbc                                                            x86_64                           1.4-9.el9                                                   appstream                            44 k
 libsndfile                                                        x86_64                           1.0.31-8.el9                                                appstream                           205 k
 libsoup                                                           x86_64                           2.72.0-8.el9                                                appstream                           389 k
 libsss_autofs                                                     x86_64                           2.9.4-6.el9_4                                               baseos                               41 k
 libstemmer                                                        x86_64                           0-18.585svn.el9                                             appstream                            82 k
 libthai                                                           x86_64                           0.1.28-8.el9                                                appstream                           208 k
 libtheora                                                         x86_64                           1:1.1.1-31.el9                                              appstream                           163 k
 libtiff                                                           x86_64                           4.4.0-12.el9                                                appstream                           197 k
 libtracker-sparql                                                 x86_64                           3.1.2-3.el9_1                                               appstream                           316 k
 libverto-libev                                                    x86_64                           0.3.2-3.el9                                                 baseos                               13 k
 libvisual                                                         x86_64                           1:0.4.0-34.el9                                              appstream                           142 k
 libvorbis                                                         x86_64                           1:1.3.7-5.el9                                               appstream                           192 k
 libwayland-client                                                 x86_64                           1.21.0-1.el9                                                appstream                            32 k
 libwayland-cursor                                                 x86_64                           1.21.0-1.el9                                                appstream                            18 k
 libwayland-egl                                                    x86_64                           1.21.0-1.el9                                                appstream                            12 k
 libwayland-server                                                 x86_64                           1.21.0-1.el9                                                appstream                            41 k
 libwbclient                                                       x86_64                           4.19.4-104.el9                                              baseos                               43 k
 libwebp                                                           x86_64                           1.2.0-8.el9_3                                               appstream                           276 k
 libxcb                                                            x86_64                           1.13.1-9.el9                                                appstream                           225 k
 libxkbcommon                                                      x86_64                           1.0.3-4.el9                                                 appstream                           132 k
 libxshmfence                                                      x86_64                           1.3-10.el9                                                  appstream                            12 k
 lksctp-tools                                                      x86_64                           1.0.19-3.el9_4                                              baseos                               96 k
 low-memory-monitor                                                x86_64                           2.1-4.el9                                                   appstream                            35 k
 lua                                                               x86_64                           5.4.4-4.el9                                                 appstream                           187 k
 lua-posix                                                         x86_64                           35.0-8.el9                                                  appstream                           131 k
 mailcap                                                           noarch                           2.1.49-5.el9                                                baseos                               32 k
 mesa-libEGL                                                       x86_64                           23.3.3-1.el9                                                appstream                           126 k
 mesa-libGL                                                        x86_64                           23.3.3-1.el9                                                appstream                           168 k
 mesa-libgbm                                                       x86_64                           23.3.3-1.el9                                                appstream                            37 k
 mesa-libglapi                                                     x86_64                           23.3.3-1.el9                                                appstream                            45 k
 mkfontscale                                                       x86_64                           1.2.1-3.el9                                                 appstream                            31 k
 mod_auth_gssapi                                                   x86_64                           1.6.3-7.el9                                                 appstream                            73 k
 mod_lookup_identity                                               x86_64                           1.0.0-15.el9                                                appstream                            27 k
 mod_session                                                       x86_64                           2.4.57-8.el9                                                appstream                            47 k
 mod_ssl                                                           x86_64                           1:2.4.57-8.el9                                              appstream                           109 k
 nfs-utils                                                         x86_64                           1:2.5.4-25.el9                                              baseos                              429 k
 nspr                                                              x86_64                           4.35.0-7.el9_4                                              appstream                           134 k
 nss                                                               x86_64                           3.90.0-7.el9_4                                              appstream                           705 k
 nss-softokn                                                       x86_64                           3.90.0-7.el9_4                                              appstream                           381 k
 nss-softokn-freebl                                                x86_64                           3.90.0-7.el9_4                                              appstream                           305 k
 nss-sysinit                                                       x86_64                           3.90.0-7.el9_4                                              appstream                            19 k
 nss-tools                                                         x86_64                           3.90.0-7.el9_4                                              appstream                           431 k
 nss-util                                                          x86_64                           3.90.0-7.el9_4                                              appstream                            88 k
 oddjob                                                            x86_64                           0.34.7-7.el9                                                appstream                            63 k
 oddjob-mkhomedir                                                  x86_64                           0.34.7-7.el9                                                appstream                            26 k
 open-sans-fonts                                                   noarch                           1.10-16.el9                                                 appstream                           471 k
 openjpeg2                                                         x86_64                           2.4.0-7.el9                                                 appstream                           162 k
 openldap-clients                                                  x86_64                           2.6.6-3.el9                                                 baseos                              173 k
 openssl-perl                                                      x86_64                           1:3.0.7-27.el9                                              appstream                            40 k
 opus                                                              x86_64                           1.3.1-10.el9                                                appstream                           199 k
 orc                                                               x86_64                           0.4.31-6.el9                                                appstream                           183 k
 osinfo-db                                                         noarch                           20231215-1.el9                                              appstream                           283 k
 osinfo-db-tools                                                   x86_64                           1.10.0-1.el9                                                appstream                            68 k
 ostree-libs                                                       x86_64                           2024.4-3.el9_4                                              appstream                           486 k
 pango                                                             x86_64                           1.48.7-3.el9                                                appstream                           297 k
 perl-Algorithm-Diff                                               noarch                           1.2010-4.el9                                                appstream                            47 k
 perl-Archive-Tar                                                  noarch                           2.38-6.el9                                                  appstream                            71 k
 perl-Compress-Raw-Bzip2                                           x86_64                           2.101-5.el9                                                 appstream                            34 k
 perl-Compress-Raw-Lzma                                            x86_64                           2.101-3.el9                                                 appstream                            50 k
 perl-Compress-Raw-Zlib                                            x86_64                           2.101-5.el9                                                 appstream                            60 k
 perl-DB_File                                                      x86_64                           1.855-4.el9                                                 appstream                            81 k
 perl-IO-Compress                                                  noarch                           2.102-4.el9                                                 appstream                           255 k
 perl-IO-Compress-Lzma                                             noarch                           2.101-4.el9                                                 appstream                            74 k
 perl-IO-Zlib                                                      noarch                           1:1.11-4.el9                                                appstream                            19 k
 perl-Term-ReadLine                                                noarch                           1.17-481.el9                                                appstream                            18 k
 perl-Text-Diff                                                    noarch                           1.45-13.el9                                                 appstream                            40 k
 perl-Tie                                                          noarch                           4.6-481.el9                                                 appstream                            30 k
 perl-debugger                                                     noarch                           1.56-481.el9                                                appstream                           132 k
 perl-meta-notation                                                noarch                           5.32.1-481.el9                                              appstream                           8.3 k
 perl-sigtrap                                                      noarch                           1.09-481.el9                                                appstream                            14 k
 perl-threads                                                      x86_64                           1:2.25-460.el9                                              appstream                            57 k
 perl-threads-shared                                               x86_64                           1.61-460.el9                                                appstream                            44 k
 pipewire-jack-audio-connection-kit-libs                           x86_64                           1.0.1-1.el9                                                 appstream                           133 k
 pipewire-libs                                                     x86_64                           1.0.1-1.el9                                                 appstream                           1.8 M
 pixman                                                            x86_64                           0.40.0-6.el9_3                                              appstream                           268 k
 pkgconf                                                           x86_64                           1.7.3-10.el9                                                baseos                               40 k
 pkgconf-m4                                                        noarch                           1.7.3-10.el9                                                baseos                               14 k
 pkgconf-pkg-config                                                x86_64                           1.7.3-10.el9                                                baseos                              9.9 k
 pki-jackson-annotations                                           noarch                           2.14.1-1.el9                                                appstream                            80 k
 pki-jackson-core                                                  noarch                           2.14.1-2.el9                                                appstream                           442 k
 pki-jackson-databind                                              noarch                           2.14.1-2.el9                                                appstream                           1.4 M
 pki-jackson-jaxrs-json-provider                                   noarch                           2.14.1-2.el9                                                appstream                            22 k
 pki-jackson-jaxrs-providers                                       noarch                           2.14.1-2.el9                                                appstream                            43 k
 pki-jackson-module-jaxb-annotations                               noarch                           2.14.1-2.el9                                                appstream                            47 k
 pki-resteasy-client                                               noarch                           3.0.26-19.el9                                               appstream                           160 k
 pki-resteasy-core                                                 noarch                           3.0.26-19.el9                                               appstream                           797 k
 pki-resteasy-jackson2-provider                                    noarch                           3.0.26-19.el9                                               appstream                            27 k
 pki-resteasy-servlet-initializer                                  noarch                           3.0.26-19.el9                                               appstream                            20 k
 policycoreutils-python-utils                                      noarch                           3.6-2.1.el9                                                 appstream                            71 k
 polkit                                                            x86_64                           0.117-11.el9                                                baseos                              145 k
 polkit-pkla-compat                                                x86_64                           0.1-21.el9                                                  baseos                               44 k
 poppler                                                           x86_64                           21.01.0-19.el9                                              appstream                           1.1 M
 poppler-data                                                      noarch                           0.4.9-9.el9                                                 appstream                           1.8 M
 poppler-glib                                                      x86_64                           21.01.0-19.el9                                              appstream                           151 k
 publicsuffix-list                                                 noarch                           20210518-3.el9                                              appstream                            82 k
 pulseaudio-libs                                                   x86_64                           15.0-2.el9                                                  appstream                           666 k
 python3-argcomplete                                               noarch                           1.12.0-5.el9                                                appstream                            61 k
 python3-audit                                                     x86_64                           3.1.2-2.el9                                                 appstream                            82 k
 python3-augeas                                                    noarch                           0.5.0-25.el9                                                appstream                            27 k
 python3-babel                                                     noarch                           2.9.1-2.el9                                                 appstream                           5.8 M
 python3-cffi                                                      x86_64                           1.14.5-5.el9                                                baseos                              241 k
 python3-chardet                                                   noarch                           4.0.0-5.el9                                                 baseos                              209 k
 python3-cryptography                                              x86_64                           36.0.1-4.el9                                                baseos                              1.1 M
 python3-decorator                                                 noarch                           4.4.2-6.el9                                                 baseos                               27 k
 python3-distro                                                    noarch                           1.5.0-7.el9                                                 appstream                            36 k
 python3-dns                                                       noarch                           2.3.0-2.el9                                                 baseos                              372 k
 python3-gssapi                                                    x86_64                           1.6.9-5.el9                                                 appstream                           457 k
 python3-idm-pki                                                   noarch                           11.5.0-1.el9                                                appstream                           154 k
 python3-idna                                                      noarch                           2.10-7.el9                                                  baseos                               92 k
 python3-ipaclient                                                 noarch                           4.11.0-10.el9_4                                             appstream                           494 k
 python3-ipalib                                                    noarch                           4.11.0-10.el9_4                                             appstream                           587 k
 python3-ipaserver                                                 noarch                           4.11.0-10.el9_4                                             appstream                           1.3 M
 python3-jinja2                                                    noarch                           2.11.3-5.el9                                                appstream                           227 k
 python3-jwcrypto                                                  noarch                           0.8-5.el9_4                                                 appstream                            67 k
 python3-kdcproxy                                                  noarch                           1.0.0-7.el9                                                 appstream                            35 k
 python3-ldap                                                      x86_64                           3.4.3-2.el9                                                 appstream                           214 k
 python3-lib389                                                    noarch                           2.4.5-6.el9_4                                               appstream                           896 k
 python3-libipa_hbac                                               x86_64                           2.9.4-6.el9_4                                               baseos                               33 k
 python3-libsemanage                                               x86_64                           3.6-1.el9                                                   appstream                            78 k
 python3-lxml                                                      x86_64                           4.6.5-3.el9                                                 appstream                           1.2 M
 python3-markupsafe                                                x86_64                           1.1.1-12.el9                                                appstream                            32 k
 python3-mod_wsgi                                                  x86_64                           4.7.1-11.el9                                                appstream                           931 k
 python3-netaddr                                                   noarch                           0.8.0-5.el9                                                 appstream                           1.5 M
 python3-netifaces                                                 x86_64                           0.10.6-15.el9                                               appstream                            22 k
 python3-ply                                                       noarch                           3.11-14.el9                                                 baseos                              103 k
 python3-policycoreutils                                           noarch                           3.6-2.1.el9                                                 appstream                           2.0 M
 python3-psutil                                                    x86_64                           5.8.0-12.el9                                                appstream                           205 k
 python3-pyasn1                                                    noarch                           0.4.8-6.el9                                                 appstream                           132 k
 python3-pyasn1-modules                                            noarch                           0.4.8-6.el9                                                 appstream                           210 k
 python3-pycparser                                                 noarch                           2.20-6.el9                                                  baseos                              124 k
 python3-pysocks                                                   noarch                           1.7.1-12.el9                                                baseos                               34 k
 python3-pytz                                                      noarch                           2021.1-5.el9                                                appstream                            47 k
 python3-pyusb                                                     noarch                           1.0.2-13.el9                                                appstream                            83 k
 python3-pyyaml                                                    x86_64                           5.4.1-6.el9                                                 baseos                              190 k
 python3-qrcode-core                                               noarch                           6.1-12.el9                                                  appstream                            49 k
 python3-requests                                                  noarch                           2.25.1-8.el9                                                baseos                              113 k
 python3-setools                                                   x86_64                           4.4.4-1.el9                                                 baseos                              551 k
 python3-setuptools                                                noarch                           53.0.0-12.el9                                               baseos                              839 k
 python3-sss                                                       x86_64                           2.9.4-6.el9_4                                               baseos                               35 k
 python3-sss-murmur                                                x86_64                           2.9.4-6.el9_4                                               baseos                               23 k
 python3-sssdconfig                                                noarch                           2.9.4-6.el9_4                                               baseos                               64 k
 python3-urllib3                                                   noarch                           1.26.5-5.el9                                                baseos                              187 k
 python3-yubico                                                    noarch                           1.3.3-7.el9                                                 appstream                            60 k
 quota                                                             x86_64                           1:4.06-6.el9                                                baseos                              190 k
 quota-nls                                                         noarch                           1:4.06-6.el9                                                baseos                               78 k
 rpcbind                                                           x86_64                           1.2.6-7.el9                                                 baseos                               56 k
 rtkit                                                             x86_64                           0.11-28.el9                                                 appstream                            55 k
 samba-client-libs                                                 x86_64                           4.19.4-104.el9                                              baseos                              5.0 M
 samba-common                                                      noarch                           4.19.4-104.el9                                              baseos                              147 k
 samba-common-libs                                                 x86_64                           4.19.4-104.el9                                              baseos                              100 k
 slapi-nis                                                         x86_64                           0.60.0-5.el9_3                                              appstream                           145 k
 slf4j                                                             noarch                           1.7.30-13.el9                                               appstream                            68 k
 slf4j-jdk14                                                       noarch                           1.7.30-13.el9                                               appstream                            16 k
 softhsm                                                           x86_64                           2.6.1-7.el9.2                                               appstream                           445 k
 sound-theme-freedesktop                                           noarch                           0.8-17.el9                                                  appstream                           377 k
 sscg                                                              x86_64                           3.0.0-7.el9                                                 appstream                            45 k
 sssd-common-pac                                                   x86_64                           2.9.4-6.el9_4                                               baseos                               99 k
 sssd-dbus                                                         x86_64                           2.9.4-6.el9_4                                               baseos                              139 k
 sssd-idp                                                          x86_64                           2.9.4-6.el9_4                                               appstream                            45 k
 sssd-ipa                                                          x86_64                           2.9.4-6.el9_4                                               baseos                              285 k
 sssd-krb5                                                         x86_64                           2.9.4-6.el9_4                                               baseos                               76 k
 sssd-krb5-common                                                  x86_64                           2.9.4-6.el9_4                                               baseos                               97 k
 sssd-nfs-idmap                                                    x86_64                           2.9.4-6.el9_4                                               baseos                               43 k
 sssd-tools                                                        x86_64                           2.9.4-6.el9_4                                               baseos                              167 k
 tomcat                                                            noarch                           1:9.0.87-1.el9_4.1                                          appstream                            91 k
 tomcat-el-3.0-api                                                 noarch                           1:9.0.87-1.el9_4.1                                          appstream                           105 k
 tomcat-jsp-2.3-api                                                noarch                           1:9.0.87-1.el9_4.1                                          appstream                            72 k
 tomcat-lib                                                        noarch                           1:9.0.87-1.el9_4.1                                          appstream                           6.0 M
 tomcat-servlet-4.0-api                                            noarch                           1:9.0.87-1.el9_4.1                                          appstream                           284 k
 totem-pl-parser                                                   x86_64                           3.26.6-2.el9                                                appstream                           130 k
 tracker                                                           x86_64                           3.1.2-3.el9_1                                               appstream                           538 k
 ttmkfdir                                                          x86_64                           3.0.9-65.el9                                                appstream                            52 k
 tzdata-java                                                       noarch                           2024a-1.el9                                                 appstream                           148 k
 upower                                                            x86_64                           0.99.13-2.el9                                               appstream                           165 k
 webkit2gtk3-jsc                                                   x86_64                           2.42.5-1.el9                                                appstream                           3.6 M
 webrtc-audio-processing                                           x86_64                           0.3.1-8.el9                                                 appstream                           304 k
 wireplumber                                                       x86_64                           0.4.14-1.el9                                                appstream                            83 k
 wireplumber-libs                                                  x86_64                           0.4.14-1.el9                                                appstream                           338 k
 words                                                             noarch                           3.0-39.el9                                                  baseos                              1.2 M
 xdg-dbus-proxy                                                    x86_64                           0.1.3-1.el9                                                 appstream                            41 k
 xdg-desktop-portal                                                x86_64                           1.12.6-1.el9                                                appstream                           367 k
 xkeyboard-config                                                  noarch                           2.33-2.el9                                                  appstream                           783 k
 xml-common                                                        noarch                           0.6.3-58.el9                                                appstream                            31 k
 xml-commons-apis                                                  noarch                           1.4.01-36.el9                                               appstream                           230 k
 xml-commons-resolver                                              noarch                           1.2-36.el9                                                  appstream                           109 k
 xorg-x11-fonts-Type1                                              noarch                           7.5-33.el9                                                  appstream                           499 k
Installing weak dependencies:
 abattis-cantarell-fonts                                           noarch                           0.301-4.el9                                                 appstream                           364 k
 apr-util-openssl                                                  x86_64                           1.6.1-23.el9                                                appstream                            14 k
 bash-completion                                                   noarch                           1:2.11-5.el9                                                baseos                              291 k
 dconf                                                             x86_64                           0.40.0-6.el9                                                appstream                           108 k
 exiv2                                                             x86_64                           0.27.5-2.el9                                                appstream                           975 k
 flatpak                                                           x86_64                           1.12.8-1.el9                                                appstream                           1.7 M
 gtk3                                                              x86_64                           3.24.31-2.el9                                               appstream                           4.8 M
 libcanberra-gtk3                                                  x86_64                           0.30-27.el9                                                 appstream                            31 k
 libproxy-webkitgtk4                                               x86_64                           0.4.15-35.el9                                               appstream                            20 k
 mod_http2                                                         x86_64                           2.0.26-2.el9_4                                              appstream                           162 k
 mod_lua                                                           x86_64                           2.4.57-8.el9                                                appstream                            59 k
 p11-kit-server                                                    x86_64                           0.25.3-2.el9                                                appstream                           245 k
 perl-Devel-Peek                                                   x86_64                           1.28-481.el9                                                appstream                            31 k
 pipewire                                                          x86_64                           1.0.1-1.el9                                                 appstream                           101 k
 pipewire-alsa                                                     x86_64                           1.0.1-1.el9                                                 appstream                            56 k
 pipewire-jack-audio-connection-kit                                x86_64                           1.0.1-1.el9                                                 appstream                           8.1 k
 pipewire-pulseaudio                                               x86_64                           1.0.1-1.el9                                                 appstream                           185 k
 sssd-passkey                                                      x86_64                           2.9.4-6.el9_4                                               baseos                               51 k
 tomcat-native                                                     x86_64                           1:1.2.36-1.el9                                              epel                                 80 k
 tracker-miners                                                    x86_64                           3.1.2-4.el9_3                                               appstream                           888 k
 xdg-desktop-portal-gtk                                            x86_64                           1.12.0-3.el9                                                appstream                           130 k

Transaction Summary
==========================================================================================================================================================================================================
Install  367 Packages

Total download size: 234 M
Installed size: 871 M
Is this ok [y/N]: y
Downloading Packages:
(1/367): 389-ds-base-libs-2.4.5-6.el9_4.x86_64.rpm                                                                                                                        2.6 MB/s | 1.4 MB     00:00    
(2/367): adwaita-cursor-theme-40.1.1-3.el9.noarch.rpm                                                                                                                      12 MB/s | 625 kB     00:00    
(3/367): 389-ds-base-2.4.5-6.el9_4.x86_64.rpm                                                                                                                             4.2 MB/s | 2.7 MB     00:00    
(4/367): abattis-cantarell-fonts-0.301-4.el9.noarch.rpm                                                                                                                   554 kB/s | 364 kB     00:00    
(5/367): almalinux-logos-httpd-90.5.1-1.1.el9.noarch.rpm                                                                                                                  1.1 MB/s |  18 kB     00:00    
(6/367): almalinux-logos-ipa-90.5.1-1.1.el9.noarch.rpm                                                                                                                    1.4 MB/s |  20 kB     00:00    
(7/367): apache-commons-cli-1.4-17.el9.noarch.rpm                                                                                                                         3.9 MB/s |  70 kB     00:00    
(8/367): alsa-lib-1.2.10-2.el9.x86_64.rpm                                                                                                                                 8.9 MB/s | 504 kB     00:00    
(9/367): apache-commons-codec-1.15-7.el9.noarch.rpm                                                                                                                       5.2 MB/s | 301 kB     00:00    
(10/367): apache-commons-io-2.8.0-8.el9.noarch.rpm                                                                                                                        6.3 MB/s | 282 kB     00:00    
(11/367): apache-commons-logging-1.2-29.el9.noarch.rpm                                                                                                                    4.0 MB/s |  76 kB     00:00    
(12/367): apache-commons-lang3-3.12.0-6.el9.noarch.rpm                                                                                                                    7.1 MB/s | 559 kB     00:00    
(13/367): apache-commons-net-3.6-14.el9.noarch.rpm                                                                                                                        4.7 MB/s | 289 kB     00:00    
(14/367): apr-1.7.0-12.el9_3.x86_64.rpm                                                                                                                                   4.3 MB/s | 122 kB     00:00    
(15/367): apr-util-bdb-1.6.1-23.el9.x86_64.rpm                                                                                                                            1.2 MB/s |  12 kB     00:00    
(16/367): apr-util-1.6.1-23.el9.x86_64.rpm                                                                                                                                2.2 MB/s |  94 kB     00:00    
(17/367): apr-util-openssl-1.6.1-23.el9.x86_64.rpm                                                                                                                        508 kB/s |  14 kB     00:00    
(18/367): at-spi2-atk-2.38.0-4.el9.x86_64.rpm                                                                                                                             4.2 MB/s |  86 kB     00:00    
(19/367): at-spi2-core-2.40.3-1.el9.x86_64.rpm                                                                                                                            5.3 MB/s | 176 kB     00:00    
(20/367): atk-2.36.0-5.el9.x86_64.rpm                                                                                                                                     6.7 MB/s | 270 kB     00:00    
(21/367): avahi-glib-0.8-20.el9.x86_64.rpm                                                                                                                                1.4 MB/s |  14 kB     00:00    
(22/367): augeas-libs-1.13.0-5.el9.x86_64.rpm                                                                                                                             8.4 MB/s | 405 kB     00:00    
(23/367): cairo-gobject-1.17.4-7.el9.x86_64.rpm                                                                                                                           3.0 MB/s |  18 kB     00:00    
(24/367): certmonger-0.79.17-2.el9.x86_64.rpm                                                                                                                             8.5 MB/s | 591 kB     00:00    
(25/367): checkpolicy-3.6-1.el9.x86_64.rpm                                                                                                                                 10 MB/s | 351 kB     00:00    
(26/367): cairo-1.17.4-7.el9.x86_64.rpm                                                                                                                                   4.2 MB/s | 659 kB     00:00    
(27/367): copy-jdk-configs-4.0-3.el9.noarch.rpm                                                                                                                           2.5 MB/s |  27 kB     00:00    
(28/367): colord-libs-1.4.5-4.el9.x86_64.rpm                                                                                                                              4.8 MB/s | 228 kB     00:00    
(29/367): cyrus-sasl-md5-2.1.27-21.el9.x86_64.rpm                                                                                                                         2.9 MB/s |  42 kB     00:00    
(30/367): dconf-0.40.0-6.el9.x86_64.rpm                                                                                                                                   6.5 MB/s | 108 kB     00:00    
(31/367): exempi-2.6.0-0.2.20211007gite23c213.el9.x86_64.rpm                                                                                                               11 MB/s | 524 kB     00:00    
(32/367): exiv2-0.27.5-2.el9.x86_64.rpm                                                                                                                                   9.4 MB/s | 975 kB     00:00    
(33/367): exiv2-libs-0.27.5-2.el9.x86_64.rpm                                                                                                                               11 MB/s | 779 kB     00:00    
(34/367): fdk-aac-free-2.0.0-8.el9.x86_64.rpm                                                                                                                             8.8 MB/s | 324 kB     00:00    
(35/367): flac-libs-1.3.3-10.el9_2.1.x86_64.rpm                                                                                                                           6.2 MB/s | 217 kB     00:00    
(36/367): ecj-4.20-16.el9.noarch.rpm                                                                                                                                      5.6 MB/s | 1.9 MB     00:00    
(37/367): flatpak-selinux-1.12.8-1.el9.noarch.rpm                                                                                                                         3.0 MB/s |  20 kB     00:00    
(38/367): flatpak-session-helper-1.12.8-1.el9.x86_64.rpm                                                                                                                  5.8 MB/s |  73 kB     00:00    
(39/367): fontawesome-fonts-4.7.0-13.el9.noarch.rpm                                                                                                                       8.5 MB/s | 204 kB     00:00    
(40/367): fontconfig-2.14.0-2.el9_1.x86_64.rpm                                                                                                                            8.8 MB/s | 274 kB     00:00    
(41/367): fribidi-1.0.10-6.el9.2.x86_64.rpm                                                                                                                               5.2 MB/s |  84 kB     00:00    
(42/367): gdk-pixbuf2-2.42.6-3.el9.x86_64.rpm                                                                                                                              12 MB/s | 466 kB     00:00    
(43/367): gdk-pixbuf2-modules-2.42.6-3.el9.x86_64.rpm                                                                                                                     5.7 MB/s |  84 kB     00:00    
(44/367): geoclue2-2.6.0-7.el9.x86_64.rpm                                                                                                                                 7.5 MB/s | 122 kB     00:00    
(45/367): giflib-5.2.1-9.el9.x86_64.rpm                                                                                                                                   4.1 MB/s |  47 kB     00:00    
(46/367): graphene-1.10.6-2.el9.x86_64.rpm                                                                                                                                5.9 MB/s |  63 kB     00:00    
(47/367): gsm-1.0.19-6.el9.x86_64.rpm                                                                                                                                     3.5 MB/s |  33 kB     00:00    
(48/367): adwaita-icon-theme-40.1.1-3.el9.noarch.rpm                                                                                                                      8.0 MB/s |  11 MB     00:01    
(49/367): gstreamer1-1.22.1-2.el9.x86_64.rpm                                                                                                                              4.3 MB/s | 1.4 MB     00:00    
(50/367): gtk-update-icon-cache-3.24.31-2.el9.x86_64.rpm                                                                                                                  2.3 MB/s |  34 kB     00:00    
(51/367): flatpak-1.12.8-1.el9.x86_64.rpm                                                                                                                                 2.8 MB/s | 1.7 MB     00:00    
(52/367): hicolor-icon-theme-0.17-13.el9.noarch.rpm                                                                                                                       6.4 MB/s |  65 kB     00:00    
(53/367): gstreamer1-plugins-base-1.22.1-2.el9.x86_64.rpm                                                                                                                 5.8 MB/s | 2.2 MB     00:00    
(54/367): httpcomponents-client-4.5.13-3.el9.noarch.rpm                                                                                                                   2.3 MB/s | 657 kB     00:00    
(55/367): httpd-2.4.57-8.el9.x86_64.rpm                                                                                                                                   3.4 MB/s |  45 kB     00:00    
(56/367): gtk3-3.24.31-2.el9.x86_64.rpm                                                                                                                                    10 MB/s | 4.8 MB     00:00    
(57/367): httpd-filesystem-2.4.57-8.el9.noarch.rpm                                                                                                                        1.4 MB/s |  12 kB     00:00    
(58/367): httpd-tools-2.4.57-8.el9.x86_64.rpm                                                                                                                             5.7 MB/s |  80 kB     00:00    
(59/367): httpcomponents-core-4.4.13-7.el9.noarch.rpm                                                                                                                     2.6 MB/s | 633 kB     00:00    
(60/367): idm-jss-tomcat-5.5.0-1.el9.x86_64.rpm                                                                                                                           3.4 MB/s |  39 kB     00:00    
(61/367): httpd-core-2.4.57-8.el9.x86_64.rpm                                                                                                                              5.6 MB/s | 1.4 MB     00:00    
(62/367): idm-ldapjdk-5.5.0-1.el9.noarch.rpm                                                                                                                              5.0 MB/s | 467 kB     00:00    
(63/367): idm-pki-acme-11.5.0-1.el9.noarch.rpm                                                                                                                            3.3 MB/s | 184 kB     00:00    
(64/367): idm-pki-base-11.5.0-1.el9.noarch.rpm                                                                                                                            6.5 MB/s | 257 kB     00:00    
(65/367): idm-jss-5.5.0-1.el9.x86_64.rpm                                                                                                                                  7.1 MB/s | 1.4 MB     00:00    
(66/367): idm-pki-kra-11.5.0-1.el9.noarch.rpm                                                                                                                              11 MB/s | 341 kB     00:00    
(67/367): idm-pki-java-11.5.0-1.el9.noarch.rpm                                                                                                                            6.5 MB/s | 714 kB     00:00    
(68/367): idm-pki-tools-11.5.0-1.el9.x86_64.rpm                                                                                                                           5.3 MB/s | 969 kB     00:00    
(69/367): ipa-client-4.11.0-10.el9_4.x86_64.rpm                                                                                                                           5.1 MB/s | 126 kB     00:00    
(70/367): idm-pki-ca-11.5.0-1.el9.noarch.rpm                                                                                                                              5.2 MB/s | 1.9 MB     00:00    
(71/367): ipa-client-common-4.11.0-10.el9_4.noarch.rpm                                                                                                                    1.0 MB/s |  41 kB     00:00    
(72/367): ipa-healthcheck-core-0.16-3.el9.noarch.rpm                                                                                                                      4.8 MB/s |  56 kB     00:00    
(73/367): ipa-selinux-4.11.0-10.el9_4.noarch.rpm                                                                                                                          4.2 MB/s |  35 kB     00:00    
(74/367): ipa-server-4.11.0-10.el9_4.x86_64.rpm                                                                                                                           7.4 MB/s | 393 kB     00:00    
(75/367): ipa-common-4.11.0-10.el9_4.noarch.rpm                                                                                                                           7.0 MB/s | 652 kB     00:00    
(76/367): ipa-server-common-4.11.0-10.el9_4.noarch.rpm                                                                                                                    7.2 MB/s | 443 kB     00:00    
(77/367): jakarta-activation-1.2.2-5.el9.noarch.rpm                                                                                                                       3.9 MB/s |  78 kB     00:00    
(78/367): idm-pki-server-11.5.0-1.el9.noarch.rpm                                                                                                                          6.9 MB/s | 3.3 MB     00:00    
(79/367): jakarta-annotations-1.3.5-13.el9.noarch.rpm                                                                                                                     870 kB/s |  44 kB     00:00    
(80/367): java-17-openjdk-17.0.11.0.9-2.el9.x86_64.rpm                                                                                                                    2.9 MB/s | 429 kB     00:00    
(81/367): iso-codes-4.6.0-3.el9.noarch.rpm                                                                                                                                4.2 MB/s | 3.3 MB     00:00    
(82/367): java-17-openjdk-devel-17.0.11.0.9-2.el9.x86_64.rpm                                                                                                              8.2 MB/s | 4.7 MB     00:00    
(83/367): javapackages-filesystem-6.0.0-4.el9.noarch.rpm                                                                                                                  1.7 MB/s |  10 kB     00:00    
(84/367): javapackages-tools-6.0.0-4.el9.noarch.rpm                                                                                                                       5.0 MB/s |  24 kB     00:00    
(85/367): jaxb-api-2.3.3-5.el9.noarch.rpm                                                                                                                                 8.6 MB/s | 108 kB     00:00    
(86/367): jbigkit-libs-2.1-23.el9.x86_64.rpm                                                                                                                              6.4 MB/s |  52 kB     00:00    
(87/367): jboss-jaxrs-2.0-api-1.0.0-16.el9.noarch.rpm                                                                                                                     7.4 MB/s | 111 kB     00:00    
(88/367): jboss-logging-3.4.1-9.el9.noarch.rpm                                                                                                                            7.3 MB/s |  57 kB     00:00    
(89/367): jboss-logging-tools-2.2.1-7.el9.noarch.rpm                                                                                                                      6.7 MB/s | 220 kB     00:00    
(90/367): jdeparser-2.0.3-12.el9.noarch.rpm                                                                                                                               5.6 MB/s | 216 kB     00:00    
(91/367): langpacks-core-font-en-3.0-16.el9.noarch.rpm                                                                                                                    1.1 MB/s | 9.4 kB     00:00    
(92/367): lcms2-2.12-3.el9.x86_64.rpm                                                                                                                                     6.9 MB/s | 166 kB     00:00    
(93/367): libX11-1.7.0-9.el9.x86_64.rpm                                                                                                                                    12 MB/s | 645 kB     00:00    
(94/367): libX11-common-1.7.0-9.el9.noarch.rpm                                                                                                                            6.5 MB/s | 151 kB     00:00    
(95/367): libX11-xcb-1.7.0-9.el9.x86_64.rpm                                                                                                                               1.9 MB/s | 9.9 kB     00:00    
(96/367): libXau-1.0.9-8.el9.x86_64.rpm                                                                                                                                   4.0 MB/s |  30 kB     00:00    
(97/367): libXcomposite-0.4.5-7.el9.x86_64.rpm                                                                                                                            4.2 MB/s |  23 kB     00:00    
(98/367): libXcursor-1.2.0-7.el9.x86_64.rpm                                                                                                                               3.5 MB/s |  30 kB     00:00    
(99/367): libXdamage-1.1.5-7.el9.x86_64.rpm                                                                                                                               2.1 MB/s |  22 kB     00:00    
(100/367): libXext-1.3.4-8.el9.x86_64.rpm                                                                                                                                 4.7 MB/s |  39 kB     00:00    
(101/367): libXfixes-5.0.3-16.el9.x86_64.rpm                                                                                                                              3.3 MB/s |  19 kB     00:00    
(102/367): libXft-2.3.3-8.el9.x86_64.rpm                                                                                                                                  4.3 MB/s |  61 kB     00:00    
(103/367): libXi-1.7.10-8.el9.x86_64.rpm                                                                                                                                  1.5 MB/s |  39 kB     00:00    
(104/367): libXinerama-1.1.4-10.el9.x86_64.rpm                                                                                                                            2.3 MB/s |  14 kB     00:00    
(105/367): libXrandr-1.5.2-8.el9.x86_64.rpm                                                                                                                               3.9 MB/s |  27 kB     00:00    
(106/367): libXrender-0.9.10-16.el9.x86_64.rpm                                                                                                                            3.8 MB/s |  27 kB     00:00    
(107/367): libXtst-1.2.3-16.el9.x86_64.rpm                                                                                                                                3.0 MB/s |  20 kB     00:00    
(108/367): libXv-1.0.11-16.el9.x86_64.rpm                                                                                                                                 1.2 MB/s |  18 kB     00:00    
(109/367): libXxf86vm-1.1.4-18.el9.x86_64.rpm                                                                                                                             2.3 MB/s |  18 kB     00:00    
(110/367): libappstream-glib-0.7.18-4.el9.x86_64.rpm                                                                                                                      6.6 MB/s | 388 kB     00:00    
(111/367): libasyncns-0.8-22.el9.x86_64.rpm                                                                                                                               4.0 MB/s |  29 kB     00:00    
(112/367): libcanberra-0.30-27.el9.x86_64.rpm                                                                                                                             7.1 MB/s |  85 kB     00:00    
(113/367): libcanberra-gtk3-0.30-27.el9.x86_64.rpm                                                                                                                        4.0 MB/s |  31 kB     00:00    
(114/367): libdatrie-0.2.13-4.el9.x86_64.rpm                                                                                                                              3.6 MB/s |  32 kB     00:00    
(115/367): libdb-utils-5.3.28-53.el9.x86_64.rpm                                                                                                                           4.9 MB/s | 131 kB     00:00    
(116/367): libepoxy-1.5.5-4.el9.x86_64.rpm                                                                                                                                6.9 MB/s | 242 kB     00:00    
(117/367): libexif-0.6.22-6.el9.x86_64.rpm                                                                                                                                9.2 MB/s | 430 kB     00:00    
(118/367): libfontenc-1.1.3-17.el9.x86_64.rpm                                                                                                                             2.7 MB/s |  30 kB     00:00    
(119/367): libgexiv2-0.12.3-1.el9.x86_64.rpm                                                                                                                              4.9 MB/s |  82 kB     00:00    
(120/367): libglvnd-1.3.4-1.el9.x86_64.rpm                                                                                                                                6.4 MB/s | 134 kB     00:00    
(121/367): libglvnd-egl-1.3.4-1.el9.x86_64.rpm                                                                                                                            3.3 MB/s |  36 kB     00:00    
(122/367): libglvnd-glx-1.3.4-1.el9.x86_64.rpm                                                                                                                            8.1 MB/s | 144 kB     00:00    
(123/367): libgsf-1.14.47-5.el9.x86_64.rpm                                                                                                                                5.7 MB/s | 245 kB     00:00    
(124/367): libgxps-0.3.2-3.el9.x86_64.rpm                                                                                                                                 4.6 MB/s |  78 kB     00:00    
(125/367): libiptcdata-1.0.5-9.el9.x86_64.rpm                                                                                                                             4.3 MB/s |  61 kB     00:00    
(126/367): libjose-11-3.el9.x86_64.rpm                                                                                                                                    5.1 MB/s |  64 kB     00:00    
(127/367): libjpeg-turbo-2.0.90-7.el9.x86_64.rpm                                                                                                                          6.7 MB/s | 174 kB     00:00    
(128/367): libldac-2.0.2.3-10.el9.x86_64.rpm                                                                                                                              3.7 MB/s |  40 kB     00:00    
(129/367): libnotify-0.7.9-8.el9.x86_64.rpm                                                                                                                               3.7 MB/s |  43 kB     00:00    
(130/367): libnsl2-2.0.0-1.el9.x86_64.rpm                                                                                                                                 2.9 MB/s |  30 kB     00:00    
(131/367): libogg-1.3.4-6.el9.x86_64.rpm                                                                                                                                  3.6 MB/s |  32 kB     00:00    
(132/367): libosinfo-1.10.0-1.el9.x86_64.rpm                                                                                                                              5.7 MB/s | 312 kB     00:00    
(133/367): libproxy-webkitgtk4-0.4.15-35.el9.x86_64.rpm                                                                                                                   1.8 MB/s |  20 kB     00:00    
(134/367): librsvg2-2.50.7-3.el9.x86_64.rpm                                                                                                                               4.3 MB/s | 3.2 MB     00:00    
(135/367): libsbc-1.4-9.el9.x86_64.rpm                                                                                                                                    3.6 MB/s |  44 kB     00:00    
(136/367): libsndfile-1.0.31-8.el9.x86_64.rpm                                                                                                                             5.7 MB/s | 205 kB     00:00    
(137/367): libsoup-2.72.0-8.el9.x86_64.rpm                                                                                                                                4.3 MB/s | 389 kB     00:00    
(138/367): libstemmer-0-18.585svn.el9.x86_64.rpm                                                                                                                          5.4 MB/s |  82 kB     00:00    
(139/367): libthai-0.1.28-8.el9.x86_64.rpm                                                                                                                                6.4 MB/s | 208 kB     00:00    
(140/367): libtheora-1.1.1-31.el9.x86_64.rpm                                                                                                                              5.0 MB/s | 163 kB     00:00    
(141/367): libtiff-4.4.0-12.el9.x86_64.rpm                                                                                                                                7.2 MB/s | 197 kB     00:00    
(142/367): libtracker-sparql-3.1.2-3.el9_1.x86_64.rpm                                                                                                                     5.8 MB/s | 316 kB     00:00    
(143/367): libvisual-0.4.0-34.el9.x86_64.rpm                                                                                                                              5.4 MB/s | 142 kB     00:00    
(144/367): libvorbis-1.3.7-5.el9.x86_64.rpm                                                                                                                               4.0 MB/s | 192 kB     00:00    
(145/367): libwayland-client-1.21.0-1.el9.x86_64.rpm                                                                                                                      2.4 MB/s |  32 kB     00:00    
(146/367): libwayland-cursor-1.21.0-1.el9.x86_64.rpm                                                                                                                      1.9 MB/s |  18 kB     00:00    
(147/367): libwayland-egl-1.21.0-1.el9.x86_64.rpm                                                                                                                         1.2 MB/s |  12 kB     00:00    
(148/367): libwayland-server-1.21.0-1.el9.x86_64.rpm                                                                                                                      2.9 MB/s |  41 kB     00:00    
(149/367): libwebp-1.2.0-8.el9_3.x86_64.rpm                                                                                                                               3.8 MB/s | 276 kB     00:00    
(150/367): libxcb-1.13.1-9.el9.x86_64.rpm                                                                                                                                 3.7 MB/s | 225 kB     00:00    
(151/367): libxkbcommon-1.0.3-4.el9.x86_64.rpm                                                                                                                            5.5 MB/s | 132 kB     00:00    
(152/367): libxshmfence-1.3-10.el9.x86_64.rpm                                                                                                                             2.3 MB/s |  12 kB     00:00    
(153/367): low-memory-monitor-2.1-4.el9.x86_64.rpm                                                                                                                        3.4 MB/s |  35 kB     00:00    
(154/367): lua-5.4.4-4.el9.x86_64.rpm                                                                                                                                     4.4 MB/s | 187 kB     00:00    
(155/367): lua-posix-35.0-8.el9.x86_64.rpm                                                                                                                                4.7 MB/s | 131 kB     00:00    
(156/367): mesa-libEGL-23.3.3-1.el9.x86_64.rpm                                                                                                                            6.8 MB/s | 126 kB     00:00    
(157/367): mesa-libGL-23.3.3-1.el9.x86_64.rpm                                                                                                                             4.1 MB/s | 168 kB     00:00    
(158/367): mesa-libgbm-23.3.3-1.el9.x86_64.rpm                                                                                                                            2.1 MB/s |  37 kB     00:00    
(159/367): mesa-libglapi-23.3.3-1.el9.x86_64.rpm                                                                                                                          3.5 MB/s |  45 kB     00:00    
(160/367): mkfontscale-1.2.1-3.el9.x86_64.rpm                                                                                                                             1.3 MB/s |  31 kB     00:00    
(161/367): mod_auth_gssapi-1.6.3-7.el9.x86_64.rpm                                                                                                                         3.5 MB/s |  73 kB     00:00    
(162/367): mod_http2-2.0.26-2.el9_4.x86_64.rpm                                                                                                                            3.8 MB/s | 162 kB     00:00    
(163/367): mod_lookup_identity-1.0.0-15.el9.x86_64.rpm                                                                                                                    1.9 MB/s |  27 kB     00:00    
(164/367): mod_lua-2.4.57-8.el9.x86_64.rpm                                                                                                                                3.4 MB/s |  59 kB     00:00    
(165/367): mod_session-2.4.57-8.el9.x86_64.rpm                                                                                                                            3.4 MB/s |  47 kB     00:00    
(166/367): mod_ssl-2.4.57-8.el9.x86_64.rpm                                                                                                                                6.5 MB/s | 109 kB     00:00    
(167/367): nspr-4.35.0-7.el9_4.x86_64.rpm                                                                                                                                 6.1 MB/s | 134 kB     00:00    
(168/367): nss-3.90.0-7.el9_4.x86_64.rpm                                                                                                                                  8.1 MB/s | 705 kB     00:00    
(169/367): nss-softokn-3.90.0-7.el9_4.x86_64.rpm                                                                                                                          9.1 MB/s | 381 kB     00:00    
(170/367): nss-softokn-freebl-3.90.0-7.el9_4.x86_64.rpm                                                                                                                   6.2 MB/s | 305 kB     00:00    
(171/367): nss-sysinit-3.90.0-7.el9_4.x86_64.rpm                                                                                                                          2.2 MB/s |  19 kB     00:00    
(172/367): nss-tools-3.90.0-7.el9_4.x86_64.rpm                                                                                                                            6.3 MB/s | 431 kB     00:00    
(173/367): nss-util-3.90.0-7.el9_4.x86_64.rpm                                                                                                                             4.5 MB/s |  88 kB     00:00    
(174/367): oddjob-0.34.7-7.el9.x86_64.rpm                                                                                                                                 3.1 MB/s |  63 kB     00:00    
(175/367): oddjob-mkhomedir-0.34.7-7.el9.x86_64.rpm                                                                                                                       2.2 MB/s |  26 kB     00:00    
(176/367): open-sans-fonts-1.10-16.el9.noarch.rpm                                                                                                                         5.6 MB/s | 471 kB     00:00    
(177/367): openjpeg2-2.4.0-7.el9.x86_64.rpm                                                                                                                               6.0 MB/s | 162 kB     00:00    
(178/367): openssl-perl-3.0.7-27.el9.x86_64.rpm                                                                                                                           4.3 MB/s |  40 kB     00:00    
(179/367): opus-1.3.1-10.el9.x86_64.rpm                                                                                                                                   4.6 MB/s | 199 kB     00:00    
(180/367): orc-0.4.31-6.el9.x86_64.rpm                                                                                                                                    5.9 MB/s | 183 kB     00:00    
(181/367): osinfo-db-20231215-1.el9.noarch.rpm                                                                                                                            7.3 MB/s | 283 kB     00:00    
(182/367): osinfo-db-tools-1.10.0-1.el9.x86_64.rpm                                                                                                                        5.6 MB/s |  68 kB     00:00    
(183/367): ostree-libs-2024.4-3.el9_4.x86_64.rpm                                                                                                                          894 kB/s | 486 kB     00:00    
(184/367): p11-kit-server-0.25.3-2.el9.x86_64.rpm                                                                                                                         4.1 MB/s | 245 kB     00:00    
(185/367): pango-1.48.7-3.el9.x86_64.rpm                                                                                                                                  6.1 MB/s | 297 kB     00:00    
(186/367): perl-Algorithm-Diff-1.2010-4.el9.noarch.rpm                                                                                                                    2.9 MB/s |  47 kB     00:00    
(187/367): perl-Archive-Tar-2.38-6.el9.noarch.rpm                                                                                                                         3.6 MB/s |  71 kB     00:00    
(188/367): perl-Compress-Raw-Bzip2-2.101-5.el9.x86_64.rpm                                                                                                                 2.5 MB/s |  34 kB     00:00    
(189/367): perl-Compress-Raw-Lzma-2.101-3.el9.x86_64.rpm                                                                                                                  3.7 MB/s |  50 kB     00:00    
(190/367): perl-Compress-Raw-Zlib-2.101-5.el9.x86_64.rpm                                                                                                                  3.8 MB/s |  60 kB     00:00    
(191/367): perl-DB_File-1.855-4.el9.x86_64.rpm                                                                                                                            4.4 MB/s |  81 kB     00:00    
(192/367): java-11-openjdk-headless-11.0.23.0.9-3.el9.x86_64.rpm                                                                                                          8.1 MB/s |  40 MB     00:04    
(193/367): perl-Devel-Peek-1.28-481.el9.x86_64.rpm                                                                                                                         99 kB/s |  31 kB     00:00    
(194/367): perl-IO-Compress-Lzma-2.101-4.el9.noarch.rpm                                                                                                                   4.2 MB/s |  74 kB     00:00    
(195/367): perl-IO-Compress-2.102-4.el9.noarch.rpm                                                                                                                        6.9 MB/s | 255 kB     00:00    
(196/367): perl-IO-Zlib-1.11-4.el9.noarch.rpm                                                                                                                             1.0 MB/s |  19 kB     00:00    
(197/367): perl-Text-Diff-1.45-13.el9.noarch.rpm                                                                                                                          2.3 MB/s |  40 kB     00:00    
(198/367): perl-Tie-4.6-481.el9.noarch.rpm                                                                                                                                3.1 MB/s |  30 kB     00:00    
(199/367): perl-debugger-1.56-481.el9.noarch.rpm                                                                                                                          5.7 MB/s | 132 kB     00:00    
(200/367): perl-meta-notation-5.32.1-481.el9.noarch.rpm                                                                                                                   761 kB/s | 8.3 kB     00:00    
(201/367): perl-sigtrap-1.09-481.el9.noarch.rpm                                                                                                                           1.5 MB/s |  14 kB     00:00    
(202/367): perl-threads-2.25-460.el9.x86_64.rpm                                                                                                                           3.0 MB/s |  57 kB     00:00    
(203/367): perl-threads-shared-1.61-460.el9.x86_64.rpm                                                                                                                    3.3 MB/s |  44 kB     00:00    
(204/367): pipewire-1.0.1-1.el9.x86_64.rpm                                                                                                                                5.8 MB/s | 101 kB     00:00    
(205/367): pipewire-alsa-1.0.1-1.el9.x86_64.rpm                                                                                                                           3.8 MB/s |  56 kB     00:00    
(206/367): pipewire-jack-audio-connection-kit-1.0.1-1.el9.x86_64.rpm                                                                                                      901 kB/s | 8.1 kB     00:00    
(207/367): pipewire-jack-audio-connection-kit-libs-1.0.1-1.el9.x86_64.rpm                                                                                                 7.4 MB/s | 133 kB     00:00    
(208/367): perl-Term-ReadLine-1.17-481.el9.noarch.rpm                                                                                                                      80 kB/s |  18 kB     00:00    
(209/367): pipewire-pulseaudio-1.0.1-1.el9.x86_64.rpm                                                                                                                     8.7 MB/s | 185 kB     00:00    
(210/367): pixman-0.40.0-6.el9_3.x86_64.rpm                                                                                                                               8.7 MB/s | 268 kB     00:00    
(211/367): pki-jackson-annotations-2.14.1-1.el9.noarch.rpm                                                                                                                6.0 MB/s |  80 kB     00:00    
(212/367): pki-jackson-core-2.14.1-2.el9.noarch.rpm                                                                                                                       6.3 MB/s | 442 kB     00:00    
(213/367): pipewire-libs-1.0.1-1.el9.x86_64.rpm                                                                                                                           7.2 MB/s | 1.8 MB     00:00    
(214/367): pki-jackson-jaxrs-json-provider-2.14.1-2.el9.noarch.rpm                                                                                                        2.1 MB/s |  22 kB     00:00    
(215/367): pki-jackson-jaxrs-providers-2.14.1-2.el9.noarch.rpm                                                                                                            2.9 MB/s |  43 kB     00:00    
(216/367): pki-jackson-module-jaxb-annotations-2.14.1-2.el9.noarch.rpm                                                                                                    3.9 MB/s |  47 kB     00:00    
(217/367): pki-resteasy-client-3.0.26-19.el9.noarch.rpm                                                                                                                   8.7 MB/s | 160 kB     00:00    
(218/367): pki-jackson-databind-2.14.1-2.el9.noarch.rpm                                                                                                                   3.3 MB/s | 1.4 MB     00:00    
(219/367): pki-resteasy-core-3.0.26-19.el9.noarch.rpm                                                                                                                     2.5 MB/s | 797 kB     00:00    
(220/367): pki-resteasy-servlet-initializer-3.0.26-19.el9.noarch.rpm                                                                                                      950 kB/s |  20 kB     00:00    
(221/367): pki-resteasy-jackson2-provider-3.0.26-19.el9.noarch.rpm                                                                                                        609 kB/s |  27 kB     00:00    
(222/367): policycoreutils-python-utils-3.6-2.1.el9.noarch.rpm                                                                                                            1.9 MB/s |  71 kB     00:00    
(223/367): poppler-21.01.0-19.el9.x86_64.rpm                                                                                                                               10 MB/s | 1.1 MB     00:00    
(224/367): poppler-glib-21.01.0-19.el9.x86_64.rpm                                                                                                                         6.2 MB/s | 151 kB     00:00    
(225/367): publicsuffix-list-20210518-3.el9.noarch.rpm                                                                                                                    3.6 MB/s |  82 kB     00:00    
(226/367): pulseaudio-libs-15.0-2.el9.x86_64.rpm                                                                                                                          8.1 MB/s | 666 kB     00:00    
(227/367): python3-argcomplete-1.12.0-5.el9.noarch.rpm                                                                                                                    2.9 MB/s |  61 kB     00:00    
(228/367): python3-audit-3.1.2-2.el9.x86_64.rpm                                                                                                                           5.7 MB/s |  82 kB     00:00    
(229/367): python3-augeas-0.5.0-25.el9.noarch.rpm                                                                                                                         2.4 MB/s |  27 kB     00:00    
(230/367): poppler-data-0.4.9-9.el9.noarch.rpm                                                                                                                            4.9 MB/s | 1.8 MB     00:00    
(231/367): python3-distro-1.5.0-7.el9.noarch.rpm                                                                                                                          2.7 MB/s |  36 kB     00:00    
(232/367): python3-gssapi-1.6.9-5.el9.x86_64.rpm                                                                                                                          7.6 MB/s | 457 kB     00:00    
(233/367): python3-idm-pki-11.5.0-1.el9.noarch.rpm                                                                                                                        3.9 MB/s | 154 kB     00:00    
(234/367): python3-ipaclient-4.11.0-10.el9_4.noarch.rpm                                                                                                                   8.6 MB/s | 494 kB     00:00    
(235/367): python3-ipalib-4.11.0-10.el9_4.noarch.rpm                                                                                                                      8.1 MB/s | 587 kB     00:00    
(236/367): python3-babel-2.9.1-2.el9.noarch.rpm                                                                                                                           8.2 MB/s | 5.8 MB     00:00    
(237/367): python3-jinja2-2.11.3-5.el9.noarch.rpm                                                                                                                          11 MB/s | 227 kB     00:00    
(238/367): python3-jwcrypto-0.8-5.el9_4.noarch.rpm                                                                                                                        6.0 MB/s |  67 kB     00:00    
(239/367): python3-kdcproxy-1.0.0-7.el9.noarch.rpm                                                                                                                        4.3 MB/s |  35 kB     00:00    
(240/367): python3-ipaserver-4.11.0-10.el9_4.noarch.rpm                                                                                                                   3.2 MB/s | 1.3 MB     00:00    
(241/367): python3-ldap-3.4.3-2.el9.x86_64.rpm                                                                                                                            4.2 MB/s | 214 kB     00:00    
(242/367): python3-libsemanage-3.6-1.el9.x86_64.rpm                                                                                                                       5.9 MB/s |  78 kB     00:00    
(243/367): python3-lib389-2.4.5-6.el9_4.noarch.rpm                                                                                                                        5.5 MB/s | 896 kB     00:00    
(244/367): python3-markupsafe-1.1.1-12.el9.x86_64.rpm                                                                                                                     2.0 MB/s |  32 kB     00:00    
(245/367): python3-lxml-4.6.5-3.el9.x86_64.rpm                                                                                                                            6.5 MB/s | 1.2 MB     00:00    
(246/367): java-17-openjdk-headless-17.0.11.0.9-2.el9.x86_64.rpm                                                                                                          6.4 MB/s |  45 MB     00:07    
(247/367): python3-mod_wsgi-4.7.1-11.el9.x86_64.rpm                                                                                                                       1.3 MB/s | 931 kB     00:00    
(248/367): python3-netifaces-0.10.6-15.el9.x86_64.rpm                                                                                                                     680 kB/s |  22 kB     00:00    
(249/367): python3-psutil-5.8.0-12.el9.x86_64.rpm                                                                                                                         6.7 MB/s | 205 kB     00:00    
(250/367): python3-pyasn1-0.4.8-6.el9.noarch.rpm                                                                                                                          4.5 MB/s | 132 kB     00:00    
(251/367): python3-netaddr-0.8.0-5.el9.noarch.rpm                                                                                                                         2.0 MB/s | 1.5 MB     00:00    
(252/367): python3-pytz-2021.1-5.el9.noarch.rpm                                                                                                                           3.7 MB/s |  47 kB     00:00    
(253/367): python3-pyasn1-modules-0.4.8-6.el9.noarch.rpm                                                                                                                  3.5 MB/s | 210 kB     00:00    
(254/367): python3-pyusb-1.0.2-13.el9.noarch.rpm                                                                                                                          3.4 MB/s |  83 kB     00:00    
(255/367): python3-qrcode-core-6.1-12.el9.noarch.rpm                                                                                                                      2.2 MB/s |  49 kB     00:00    
(256/367): python3-yubico-1.3.3-7.el9.noarch.rpm                                                                                                                          2.3 MB/s |  60 kB     00:00    
(257/367): rtkit-0.11-28.el9.x86_64.rpm                                                                                                                                   2.1 MB/s |  55 kB     00:00    
(258/367): slapi-nis-0.60.0-5.el9_3.x86_64.rpm                                                                                                                            4.0 MB/s | 145 kB     00:00    
(259/367): slf4j-1.7.30-13.el9.noarch.rpm                                                                                                                                 2.1 MB/s |  68 kB     00:00    
(260/367): slf4j-jdk14-1.7.30-13.el9.noarch.rpm                                                                                                                           928 kB/s |  16 kB     00:00    
(261/367): python3-policycoreutils-3.6-2.1.el9.noarch.rpm                                                                                                                 7.0 MB/s | 2.0 MB     00:00    
(262/367): sscg-3.0.0-7.el9.x86_64.rpm                                                                                                                                    2.1 MB/s |  45 kB     00:00    
(263/367): softhsm-2.6.1-7.el9.2.x86_64.rpm                                                                                                                               3.9 MB/s | 445 kB     00:00    
(264/367): sound-theme-freedesktop-0.8-17.el9.noarch.rpm                                                                                                                  3.1 MB/s | 377 kB     00:00    
(265/367): sssd-idp-2.9.4-6.el9_4.x86_64.rpm                                                                                                                              1.1 MB/s |  45 kB     00:00    
(266/367): tomcat-9.0.87-1.el9_4.1.noarch.rpm                                                                                                                             2.1 MB/s |  91 kB     00:00    
(267/367): tomcat-jsp-2.3-api-9.0.87-1.el9_4.1.noarch.rpm                                                                                                                 2.7 MB/s |  72 kB     00:00    
(268/367): tomcat-el-3.0-api-9.0.87-1.el9_4.1.noarch.rpm                                                                                                                  2.6 MB/s | 105 kB     00:00    
(269/367): totem-pl-parser-3.26.6-2.el9.x86_64.rpm                                                                                                                        5.0 MB/s | 130 kB     00:00    
(270/367): tomcat-servlet-4.0-api-9.0.87-1.el9_4.1.noarch.rpm                                                                                                             5.4 MB/s | 284 kB     00:00    
(271/367): tracker-3.1.2-3.el9_1.x86_64.rpm                                                                                                                               5.5 MB/s | 538 kB     00:00    
(272/367): ttmkfdir-3.0.9-65.el9.x86_64.rpm                                                                                                                               4.1 MB/s |  52 kB     00:00    
(273/367): tzdata-java-2024a-1.el9.noarch.rpm                                                                                                                             9.2 MB/s | 148 kB     00:00    
(274/367): upower-0.99.13-2.el9.x86_64.rpm                                                                                                                                4.5 MB/s | 165 kB     00:00    
(275/367): tracker-miners-3.1.2-4.el9_3.x86_64.rpm                                                                                                                        5.3 MB/s | 888 kB     00:00    
(276/367): webrtc-audio-processing-0.3.1-8.el9.x86_64.rpm                                                                                                                 4.5 MB/s | 304 kB     00:00    
(277/367): wireplumber-0.4.14-1.el9.x86_64.rpm                                                                                                                            3.1 MB/s |  83 kB     00:00    
(278/367): wireplumber-libs-0.4.14-1.el9.x86_64.rpm                                                                                                                       7.6 MB/s | 338 kB     00:00    
(279/367): xdg-dbus-proxy-0.1.3-1.el9.x86_64.rpm                                                                                                                          3.5 MB/s |  41 kB     00:00    
(280/367): xdg-desktop-portal-1.12.6-1.el9.x86_64.rpm                                                                                                                     7.4 MB/s | 367 kB     00:00    
(281/367): xdg-desktop-portal-gtk-1.12.0-3.el9.x86_64.rpm                                                                                                                 5.2 MB/s | 130 kB     00:00    
(282/367): webkit2gtk3-jsc-2.42.5-1.el9.x86_64.rpm                                                                                                                        7.3 MB/s | 3.6 MB     00:00    
(283/367): tomcat-lib-9.0.87-1.el9_4.1.noarch.rpm                                                                                                                         7.4 MB/s | 6.0 MB     00:00    
(284/367): xml-common-0.6.3-58.el9.noarch.rpm                                                                                                                             305 kB/s |  31 kB     00:00    
(285/367): xml-commons-resolver-1.2-36.el9.noarch.rpm                                                                                                                     4.2 MB/s | 109 kB     00:00    
(286/367): xml-commons-apis-1.4.01-36.el9.noarch.rpm                                                                                                                      5.3 MB/s | 230 kB     00:00    
(287/367): xkeyboard-config-2.33-2.el9.noarch.rpm                                                                                                                         1.9 MB/s | 783 kB     00:00    
(288/367): ModemManager-glib-1.20.2-1.el9.x86_64.rpm                                                                                                                      4.8 MB/s | 337 kB     00:00    
(289/367): xorg-x11-fonts-Type1-7.5-33.el9.noarch.rpm                                                                                                                     4.8 MB/s | 499 kB     00:00    
(290/367): avahi-libs-0.8-20.el9.x86_64.rpm                                                                                                                               1.8 MB/s |  67 kB     00:00    
(291/367): adobe-source-code-pro-fonts-2.030.1.050-12.el9.1.noarch.rpm                                                                                                    6.1 MB/s | 831 kB     00:00    
(292/367): autofs-5.1.7-58.el9.x86_64.rpm                                                                                                                                 3.6 MB/s | 369 kB     00:00    
(293/367): bluez-libs-5.64-2.el9.x86_64.rpm                                                                                                                               2.9 MB/s |  83 kB     00:00    
(294/367): bubblewrap-0.4.1-6.el9.x86_64.rpm                                                                                                                              2.7 MB/s |  49 kB     00:00    
(295/367): cyrus-sasl-gssapi-2.1.27-21.el9.x86_64.rpm                                                                                                                     2.1 MB/s |  26 kB     00:00    
(296/367): bash-completion-2.11-5.el9.noarch.rpm                                                                                                                          3.4 MB/s | 291 kB     00:00    
(297/367): cyrus-sasl-plain-2.1.27-21.el9.x86_64.rpm                                                                                                                      1.2 MB/s |  23 kB     00:00    
(298/367): dbus-tools-1.12.20-8.el9.x86_64.rpm                                                                                                                            3.2 MB/s |  50 kB     00:00    
(299/367): fonts-filesystem-2.0.5-7.el9.1.noarch.rpm                                                                                                                      946 kB/s | 9.0 kB     00:00    
(300/367): cups-libs-2.3.3op2-24.el9.x86_64.rpm                                                                                                                           3.2 MB/s | 261 kB     00:00    
(301/367): fuse-2.9.9-15.el9.x86_64.rpm                                                                                                                                   2.9 MB/s |  79 kB     00:00    
(302/367): glib-networking-2.68.3-3.el9.x86_64.rpm                                                                                                                        6.6 MB/s | 169 kB     00:00    
(303/367): freetype-2.10.4-9.el9.x86_64.rpm                                                                                                                               4.4 MB/s | 387 kB     00:00    
(304/367): graphite2-1.3.14-9.el9.x86_64.rpm                                                                                                                              3.2 MB/s |  94 kB     00:00    
(305/367): gssproxy-0.8.4-6.el9.x86_64.rpm                                                                                                                                4.2 MB/s | 108 kB     00:00    
(306/367): gsettings-desktop-schemas-40.0-6.el9.x86_64.rpm                                                                                                                6.0 MB/s | 666 kB     00:00    
(307/367): dejavu-sans-fonts-2.37-18.el9.noarch.rpm                                                                                                                       5.3 MB/s | 1.3 MB     00:00    
(308/367): harfbuzz-2.7.4-10.el9.x86_64.rpm                                                                                                                               5.5 MB/s | 623 kB     00:00    
(309/367): krb5-pkinit-1.21.1-1.el9.x86_64.rpm                                                                                                                            3.5 MB/s |  59 kB     00:00    
(310/367): keyutils-1.6.3-1.el9.x86_64.rpm                                                                                                                                1.2 MB/s |  71 kB     00:00    
(311/367): libatomic-11.4.1-3.el9.alma.1.x86_64.rpm                                                                                                                       2.6 MB/s |  30 kB     00:00    
(312/367): krb5-server-1.21.1-1.el9.x86_64.rpm                                                                                                                            7.2 MB/s | 293 kB     00:00    
(313/367): libev-4.33-5.el9.x86_64.rpm                                                                                                                                    1.4 MB/s |  52 kB     00:00    
(314/367): libipa_hbac-2.9.4-6.el9_4.x86_64.rpm                                                                                                                           2.7 MB/s |  39 kB     00:00    
(315/367): krb5-workstation-1.21.1-1.el9.x86_64.rpm                                                                                                                       5.1 MB/s | 496 kB     00:00    
(316/367): libnfsidmap-2.5.4-25.el9.x86_64.rpm                                                                                                                            2.9 MB/s |  60 kB     00:00    
(317/367): libkadm5-1.21.1-1.el9.x86_64.rpm                                                                                                                               1.5 MB/s |  77 kB     00:00    
(318/367): libpkgconf-1.7.3-10.el9.x86_64.rpm                                                                                                                             1.9 MB/s |  35 kB     00:00    
(319/367): libpng-1.6.37-12.el9.x86_64.rpm                                                                                                                                3.8 MB/s | 116 kB     00:00    
(320/367): libsss_autofs-2.9.4-6.el9_4.x86_64.rpm                                                                                                                         3.2 MB/s |  41 kB     00:00    
(321/367): libproxy-0.4.15-35.el9.x86_64.rpm                                                                                                                              1.7 MB/s |  73 kB     00:00    
(322/367): libverto-libev-0.3.2-3.el9.x86_64.rpm                                                                                                                          849 kB/s |  13 kB     00:00    
(323/367): libwbclient-4.19.4-104.el9.x86_64.rpm                                                                                                                          1.4 MB/s |  43 kB     00:00    
(324/367): lksctp-tools-1.0.19-3.el9_4.x86_64.rpm                                                                                                                         2.0 MB/s |  96 kB     00:00    
(325/367): mailcap-2.1.49-5.el9.noarch.rpm                                                                                                                                1.0 MB/s |  32 kB     00:00    
(326/367): openldap-clients-2.6.6-3.el9.x86_64.rpm                                                                                                                        8.5 MB/s | 173 kB     00:00    
(327/367): pkgconf-1.7.3-10.el9.x86_64.rpm                                                                                                                                2.5 MB/s |  40 kB     00:00    
(328/367): pkgconf-m4-1.7.3-10.el9.noarch.rpm                                                                                                                             1.4 MB/s |  14 kB     00:00    
(329/367): pkgconf-pkg-config-1.7.3-10.el9.x86_64.rpm                                                                                                                     995 kB/s | 9.9 kB     00:00    
(330/367): nfs-utils-2.5.4-25.el9.x86_64.rpm                                                                                                                              4.7 MB/s | 429 kB     00:00    
(331/367): polkit-0.117-11.el9.x86_64.rpm                                                                                                                                 4.0 MB/s | 145 kB     00:00    
(332/367): polkit-pkla-compat-0.1-21.el9.x86_64.rpm                                                                                                                       1.4 MB/s |  44 kB     00:00    
(333/367): python3-cffi-1.14.5-5.el9.x86_64.rpm                                                                                                                           6.1 MB/s | 241 kB     00:00    
(334/367): python3-chardet-4.0.0-5.el9.noarch.rpm                                                                                                                         5.3 MB/s | 209 kB     00:00    
(335/367): python3-decorator-4.4.2-6.el9.noarch.rpm                                                                                                                       2.4 MB/s |  27 kB     00:00    
(336/367): python3-dns-2.3.0-2.el9.noarch.rpm                                                                                                                             5.3 MB/s | 372 kB     00:00    
(337/367): python3-idna-2.10-7.el9.noarch.rpm                                                                                                                             4.1 MB/s |  92 kB     00:00    
(338/367): python3-libipa_hbac-2.9.4-6.el9_4.x86_64.rpm                                                                                                                   2.2 MB/s |  33 kB     00:00    
(339/367): python3-cryptography-36.0.1-4.el9.x86_64.rpm                                                                                                                   7.0 MB/s | 1.1 MB     00:00    
(340/367): python3-ply-3.11-14.el9.noarch.rpm                                                                                                                             2.6 MB/s | 103 kB     00:00    
(341/367): python3-pysocks-1.7.1-12.el9.noarch.rpm                                                                                                                        3.9 MB/s |  34 kB     00:00    
(342/367): python3-pycparser-2.20-6.el9.noarch.rpm                                                                                                                        4.1 MB/s | 124 kB     00:00    
(343/367): python3-requests-2.25.1-8.el9.noarch.rpm                                                                                                                       5.9 MB/s | 113 kB     00:00    
(344/367): python3-pyyaml-5.4.1-6.el9.x86_64.rpm                                                                                                                          4.1 MB/s | 190 kB     00:00    
(345/367): python3-setools-4.4.4-1.el9.x86_64.rpm                                                                                                                         6.3 MB/s | 551 kB     00:00    
(346/367): python3-sss-2.9.4-6.el9_4.x86_64.rpm                                                                                                                           2.8 MB/s |  35 kB     00:00    
(347/367): python3-sss-murmur-2.9.4-6.el9_4.x86_64.rpm                                                                                                                    1.4 MB/s |  23 kB     00:00    
(348/367): python3-sssdconfig-2.9.4-6.el9_4.noarch.rpm                                                                                                                    4.5 MB/s |  64 kB     00:00    
(349/367): python3-setuptools-53.0.0-12.el9.noarch.rpm                                                                                                                    5.9 MB/s | 839 kB     00:00    
(350/367): python3-urllib3-1.26.5-5.el9.noarch.rpm                                                                                                                        4.8 MB/s | 187 kB     00:00    
(351/367): quota-nls-4.06-6.el9.noarch.rpm                                                                                                                                5.1 MB/s |  78 kB     00:00    
(352/367): quota-4.06-6.el9.x86_64.rpm                                                                                                                                    4.0 MB/s | 190 kB     00:00    
(353/367): rpcbind-1.2.6-7.el9.x86_64.rpm                                                                                                                                 1.8 MB/s |  56 kB     00:00    
(354/367): samba-common-4.19.4-104.el9.noarch.rpm                                                                                                                         8.9 MB/s | 147 kB     00:00    
(355/367): samba-common-libs-4.19.4-104.el9.x86_64.rpm                                                                                                                    7.2 MB/s | 100 kB     00:00    
(356/367): sssd-common-pac-2.9.4-6.el9_4.x86_64.rpm                                                                                                                       8.7 MB/s |  99 kB     00:00    
(357/367): sssd-dbus-2.9.4-6.el9_4.x86_64.rpm                                                                                                                             9.4 MB/s | 139 kB     00:00    
(358/367): sssd-ipa-2.9.4-6.el9_4.x86_64.rpm                                                                                                                              6.9 MB/s | 285 kB     00:00    
(359/367): sssd-krb5-2.9.4-6.el9_4.x86_64.rpm                                                                                                                             4.5 MB/s |  76 kB     00:00    
(360/367): sssd-krb5-common-2.9.4-6.el9_4.x86_64.rpm                                                                                                                      3.9 MB/s |  97 kB     00:00    
(361/367): sssd-nfs-idmap-2.9.4-6.el9_4.x86_64.rpm                                                                                                                        3.1 MB/s |  43 kB     00:00    
(362/367): sssd-passkey-2.9.4-6.el9_4.x86_64.rpm                                                                                                                          2.4 MB/s |  51 kB     00:00    
(363/367): sssd-tools-2.9.4-6.el9_4.x86_64.rpm                                                                                                                            7.4 MB/s | 167 kB     00:00    
(364/367): words-3.0-39.el9.noarch.rpm                                                                                                                                    7.6 MB/s | 1.2 MB     00:00    
(365/367): samba-client-libs-4.19.4-104.el9.x86_64.rpm                                                                                                                    8.4 MB/s | 5.0 MB     00:00    
(366/367): libicu-67.1-9.el9.x86_64.rpm                                                                                                                                   6.2 MB/s | 9.6 MB     00:01    
(367/367): tomcat-native-1.2.36-1.el9.x86_64.rpm                                                                                                                           22 kB/s |  80 kB     00:03    
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                      11 MB/s | 234 MB     00:20     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Running scriptlet: copy-jdk-configs-4.0-3.el9.noarch                                                                                                                                                1/1 
  Running scriptlet: java-11-openjdk-headless-1:11.0.23.0.9-3.el9.x86_64                                                                                                                              1/1 
  Running scriptlet: java-17-openjdk-headless-1:17.0.11.0.9-2.el9.x86_64                                                                                                                              1/1 
  Preparing        :                                                                                                                                                                                  1/1 
  Installing       : javapackages-filesystem-6.0.0-4.el9.noarch                                                                                                                                     1/367 
  Installing       : nspr-4.35.0-7.el9_4.x86_64                                                                                                                                                     2/367 
  Installing       : python3-setuptools-53.0.0-12.el9.noarch                                                                                                                                        3/367 
  Installing       : nss-util-3.90.0-7.el9_4.x86_64                                                                                                                                                 4/367 
  Installing       : libpng-2:1.6.37-12.el9.x86_64                                                                                                                                                  5/367 
  Installing       : libicu-67.1-9.el9.x86_64                                                                                                                                                       6/367 
  Installing       : fonts-filesystem-1:2.0.5-7.el9.1.noarch                                                                                                                                        7/367 
  Installing       : avahi-libs-0.8-20.el9.x86_64                                                                                                                                                   8/367 
  Installing       : python3-pyasn1-0.4.8-6.el9.noarch                                                                                                                                              9/367 
  Installing       : libjpeg-turbo-2.0.90-7.el9.x86_64                                                                                                                                             10/367 
  Installing       : gdk-pixbuf2-2.42.6-3.el9.x86_64                                                                                                                                               11/367 
  Installing       : alsa-lib-1.2.10-2.el9.x86_64                                                                                                                                                  12/367 
  Installing       : libogg-2:1.3.4-6.el9.x86_64                                                                                                                                                   13/367 
  Installing       : libvorbis-1:1.3.7-5.el9.x86_64                                                                                                                                                14/367 
  Installing       : python3-dns-2.3.0-2.el9.noarch                                                                                                                                                15/367 
  Installing       : openldap-clients-2.6.6-3.el9.x86_64                                                                                                                                           16/367 
  Installing       : cyrus-sasl-gssapi-2.1.27-21.el9.x86_64                                                                                                                                        17/367 
  Installing       : libwayland-client-1.21.0-1.el9.x86_64                                                                                                                                         18/367 
  Installing       : apr-1.7.0-12.el9_3.x86_64                                                                                                                                                     19/367 
  Installing       : apr-util-bdb-1.6.1-23.el9.x86_64                                                                                                                                              20/367 
  Installing       : apr-util-openssl-1.6.1-23.el9.x86_64                                                                                                                                          21/367 
  Installing       : apr-util-1.6.1-23.el9.x86_64                                                                                                                                                  22/367 
  Installing       : python3-pyasn1-modules-0.4.8-6.el9.noarch                                                                                                                                     23/367 
  Installing       : python3-ldap-3.4.3-2.el9.x86_64                                                                                                                                               24/367 
  Installing       : cups-libs-1:2.3.3op2-24.el9.x86_64                                                                                                                                            25/367 
  Installing       : sssd-dbus-2.9.4-6.el9_4.x86_64                                                                                                                                                26/367 
  Running scriptlet: sssd-dbus-2.9.4-6.el9_4.x86_64                                                                                                                                                26/367 
  Installing       : python3-sssdconfig-2.9.4-6.el9_4.noarch                                                                                                                                       27/367 
  Installing       : libnfsidmap-1:2.5.4-25.el9.x86_64                                                                                                                                             28/367 
  Installing       : krb5-pkinit-1.21.1-1.el9.x86_64                                                                                                                                               29/367 
  Installing       : keyutils-1.6.3-1.el9.x86_64                                                                                                                                                   30/367 
  Installing       : python3-lxml-4.6.5-3.el9.x86_64                                                                                                                                               31/367 
  Installing       : opus-1.3.1-10.el9.x86_64                                                                                                                                                      32/367 
  Installing       : libstemmer-0-18.585svn.el9.x86_64                                                                                                                                             33/367 
  Installing       : libX11-xcb-1.7.0-9.el9.x86_64                                                                                                                                                 34/367 
  Installing       : lcms2-2.12-3.el9.x86_64                                                                                                                                                       35/367 
  Installing       : ipa-client-common-4.11.0-10.el9_4.noarch                                                                                                                                      36/367 
  Installing       : gstreamer1-1.22.1-2.el9.x86_64                                                                                                                                                37/367 
  Installing       : augeas-libs-1.13.0-5.el9.x86_64                                                                                                                                               38/367 
  Installing       : atk-2.36.0-5.el9.x86_64                                                                                                                                                       39/367 
  Installing       : python3-augeas-0.5.0-25.el9.noarch                                                                                                                                            40/367 
  Installing       : libwayland-cursor-1.21.0-1.el9.x86_64                                                                                                                                         41/367 
  Installing       : sssd-krb5-common-2.9.4-6.el9_4.x86_64                                                                                                                                         42/367 
  Installing       : dejavu-sans-fonts-2.37-18.el9.noarch                                                                                                                                          43/367 
  Installing       : python3-distro-1.5.0-7.el9.noarch                                                                                                                                             44/367 
  Installing       : python3-netaddr-0.8.0-5.el9.noarch                                                                                                                                            45/367 
  Installing       : python3-qrcode-core-6.1-12.el9.noarch                                                                                                                                         46/367 
  Running scriptlet: polkit-0.117-11.el9.x86_64                                                                                                                                                    47/367 
  Installing       : polkit-0.117-11.el9.x86_64                                                                                                                                                    47/367 
  Running scriptlet: polkit-0.117-11.el9.x86_64                                                                                                                                                    47/367 
  Installing       : polkit-pkla-compat-0.1-21.el9.x86_64                                                                                                                                          48/367 
  Running scriptlet: samba-common-4.19.4-104.el9.noarch                                                                                                                                            49/367 
  Installing       : samba-common-4.19.4-104.el9.noarch                                                                                                                                            49/367 
  Running scriptlet: samba-common-4.19.4-104.el9.noarch                                                                                                                                            49/367 
  Running scriptlet: libwbclient-4.19.4-104.el9.x86_64                                                                                                                                             50/367 
  Installing       : libwbclient-4.19.4-104.el9.x86_64                                                                                                                                             50/367 
  Installing       : samba-common-libs-4.19.4-104.el9.x86_64                                                                                                                                       51/367 
  Installing       : samba-client-libs-4.19.4-104.el9.x86_64                                                                                                                                       52/367 
  Installing       : python3-idna-2.10-7.el9.noarch                                                                                                                                                53/367 
  Installing       : lksctp-tools-1.0.19-3.el9_4.x86_64                                                                                                                                            54/367 
  Installing       : libproxy-0.4.15-35.el9.x86_64                                                                                                                                                 55/367 
  Installing       : libkadm5-1.21.1-1.el9.x86_64                                                                                                                                                  56/367 
  Installing       : libipa_hbac-2.9.4-6.el9_4.x86_64                                                                                                                                              57/367 
  Installing       : dbus-tools-1:1.12.20-8.el9.x86_64                                                                                                                                             58/367 
  Running scriptlet: xml-common-0.6.3-58.el9.noarch                                                                                                                                                59/367 
  Installing       : xml-common-0.6.3-58.el9.noarch                                                                                                                                                59/367 
  Installing       : tzdata-java-2024a-1.el9.noarch                                                                                                                                                60/367 
  Installing       : python3-pyusb-1.0.2-13.el9.noarch                                                                                                                                             61/367 
  Installing       : python3-libsemanage-3.6-1.el9.x86_64                                                                                                                                          62/367 
  Installing       : pixman-0.40.0-6.el9_3.x86_64                                                                                                                                                  63/367 
  Installing       : perl-threads-1:2.25-460.el9.x86_64                                                                                                                                            64/367 
  Installing       : perl-meta-notation-5.32.1-481.el9.noarch                                                                                                                                      65/367 
  Installing       : perl-Compress-Raw-Zlib-2.101-5.el9.x86_64                                                                                                                                     66/367 
  Installing       : oddjob-0.34.7-7.el9.x86_64                                                                                                                                                    67/367 
  Running scriptlet: oddjob-0.34.7-7.el9.x86_64                                                                                                                                                    67/367 
  Installing       : mesa-libglapi-23.3.3-1.el9.x86_64                                                                                                                                             68/367 
  Installing       : libxshmfence-1.3-10.el9.x86_64                                                                                                                                                69/367 
  Installing       : libwayland-server-1.21.0-1.el9.x86_64                                                                                                                                         70/367 
  Installing       : libwayland-egl-1.21.0-1.el9.x86_64                                                                                                                                            71/367 
  Installing       : libglvnd-1:1.3.4-1.el9.x86_64                                                                                                                                                 72/367 
  Installing       : libXau-1.0.9-8.el9.x86_64                                                                                                                                                     73/367 
  Installing       : libxcb-1.13.1-9.el9.x86_64                                                                                                                                                    74/367 
  Installing       : mesa-libgbm-23.3.3-1.el9.x86_64                                                                                                                                               75/367 
  Running scriptlet: httpd-filesystem-2.4.57-8.el9.noarch                                                                                                                                          76/367 
  Installing       : httpd-filesystem-2.4.57-8.el9.noarch                                                                                                                                          76/367 
  Installing       : fribidi-1.0.10-6.el9.2.x86_64                                                                                                                                                 77/367 
  Installing       : dconf-0.40.0-6.el9.x86_64                                                                                                                                                     78/367 
  Running scriptlet: dconf-0.40.0-6.el9.x86_64                                                                                                                                                     78/367 
  Installing       : libglvnd-egl-1:1.3.4-1.el9.x86_64                                                                                                                                             79/367 
  Installing       : mesa-libEGL-23.3.3-1.el9.x86_64                                                                                                                                               80/367 
  Installing       : oddjob-mkhomedir-0.34.7-7.el9.x86_64                                                                                                                                          81/367 
  Running scriptlet: oddjob-mkhomedir-0.34.7-7.el9.x86_64                                                                                                                                          81/367 
  Installing       : perl-sigtrap-1.09-481.el9.noarch                                                                                                                                              82/367 
  Installing       : perl-threads-shared-1.61-460.el9.x86_64                                                                                                                                       83/367 
  Installing       : python3-yubico-1.3.3-7.el9.noarch                                                                                                                                             84/367 
  Installing       : iso-codes-4.6.0-3.el9.noarch                                                                                                                                                  85/367 
  Installing       : python3-libipa_hbac-2.9.4-6.el9_4.x86_64                                                                                                                                      86/367 
  Installing       : krb5-workstation-1.21.1-1.el9.x86_64                                                                                                                                          87/367 
  Installing       : sssd-common-pac-2.9.4-6.el9_4.x86_64                                                                                                                                          88/367 
  Installing       : sssd-ipa-2.9.4-6.el9_4.x86_64                                                                                                                                                 89/367 
  Running scriptlet: rtkit-0.11-28.el9.x86_64                                                                                                                                                      90/367 
  Installing       : rtkit-0.11-28.el9.x86_64                                                                                                                                                      90/367 
  Running scriptlet: rtkit-0.11-28.el9.x86_64                                                                                                                                                      90/367 
Created symlink /etc/systemd/system/graphical.target.wants/rtkit-daemon.service → /usr/lib/systemd/system/rtkit-daemon.service.

  Installing       : langpacks-core-font-en-3.0-16.el9.noarch                                                                                                                                      91/367 
  Installing       : sssd-krb5-2.9.4-6.el9_4.x86_64                                                                                                                                                92/367 
  Installing       : colord-libs-1.4.5-4.el9.x86_64                                                                                                                                                93/367 
  Installing       : httpd-tools-2.4.57-8.el9.x86_64                                                                                                                                               94/367 
  Installing       : tomcat-native-1:1.2.36-1.el9.x86_64                                                                                                                                           95/367 
  Running scriptlet: tomcat-native-1:1.2.36-1.el9.x86_64                                                                                                                                           95/367 
  Installing       : python3-kdcproxy-1.0.0-7.el9.noarch                                                                                                                                           96/367 
  Installing       : flac-libs-1.3.3-10.el9_2.1.x86_64                                                                                                                                             97/367 
  Installing       : libtheora-1:1.1.1-31.el9.x86_64                                                                                                                                               98/367 
  Installing       : gtk-update-icon-cache-3.24.31-2.el9.x86_64                                                                                                                                    99/367 
  Installing       : libgsf-1.14.47-5.el9.x86_64                                                                                                                                                  100/367 
  Installing       : libnotify-0.7.9-8.el9.x86_64                                                                                                                                                 101/367 
  Installing       : avahi-glib-0.8-20.el9.x86_64                                                                                                                                                 102/367 
  Installing       : abattis-cantarell-fonts-0.301-4.el9.noarch                                                                                                                                   103/367 
  Installing       : fontawesome-fonts-1:4.7.0-13.el9.noarch                                                                                                                                      104/367 
  Installing       : open-sans-fonts-1.10-16.el9.noarch                                                                                                                                           105/367 
  Installing       : adobe-source-code-pro-fonts-2.030.1.050-12.el9.1.noarch                                                                                                                      106/367 
  Installing       : gsettings-desktop-schemas-40.0-6.el9.x86_64                                                                                                                                  107/367 
  Installing       : nss-softokn-freebl-3.90.0-7.el9_4.x86_64                                                                                                                                     108/367 
  Installing       : nss-softokn-3.90.0-7.el9_4.x86_64                                                                                                                                            109/367 
  Installing       : nss-3.90.0-7.el9_4.x86_64                                                                                                                                                    110/367 
  Running scriptlet: nss-3.90.0-7.el9_4.x86_64                                                                                                                                                    110/367 
  Installing       : nss-sysinit-3.90.0-7.el9_4.x86_64                                                                                                                                            111/367 
  Installing       : nss-tools-3.90.0-7.el9_4.x86_64                                                                                                                                              112/367 
  Installing       : certmonger-0.79.17-2.el9.x86_64                                                                                                                                              113/367 
  Running scriptlet: certmonger-0.79.17-2.el9.x86_64                                                                                                                                              113/367 
  Installing       : 389-ds-base-libs-2.4.5-6.el9_4.x86_64                                                                                                                                        114/367 
  Installing       : python3-setools-4.4.4-1.el9.x86_64                                                                                                                                           115/367 
  Installing       : exiv2-libs-0.27.5-2.el9.x86_64                                                                                                                                               116/367 
  Installing       : exiv2-0.27.5-2.el9.x86_64                                                                                                                                                    117/367 
  Installing       : libgexiv2-0.12.3-1.el9.x86_64                                                                                                                                                118/367 
  Installing       : words-3.0-39.el9.noarch                                                                                                                                                      119/367 
  Installing       : sssd-passkey-2.9.4-6.el9_4.x86_64                                                                                                                                            120/367 
  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                   121/367 
  Installing       : rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                   121/367 
  Running scriptlet: rpcbind-1.2.6-7.el9.x86_64                                                                                                                                                   121/367 
Created symlink /etc/systemd/system/multi-user.target.wants/rpcbind.service → /usr/lib/systemd/system/rpcbind.service.
Created symlink /etc/systemd/system/sockets.target.wants/rpcbind.socket → /usr/lib/systemd/system/rpcbind.socket.

  Installing       : quota-nls-1:4.06-6.el9.noarch                                                                                                                                                122/367 
  Installing       : quota-1:4.06-6.el9.x86_64                                                                                                                                                    123/367 
  Installing       : python3-sss-murmur-2.9.4-6.el9_4.x86_64                                                                                                                                      124/367 
  Installing       : python3-sss-2.9.4-6.el9_4.x86_64                                                                                                                                             125/367 
  Installing       : sssd-tools-2.9.4-6.el9_4.x86_64                                                                                                                                              126/367 
  Installing       : python3-pyyaml-5.4.1-6.el9.x86_64                                                                                                                                            127/367 
  Installing       : python3-pysocks-1.7.1-12.el9.noarch                                                                                                                                          128/367 
  Installing       : python3-urllib3-1.26.5-5.el9.noarch                                                                                                                                          129/367 
  Installing       : python3-ply-3.11-14.el9.noarch                                                                                                                                               130/367 
  Installing       : python3-pycparser-2.20-6.el9.noarch                                                                                                                                          131/367 
  Installing       : python3-cffi-1.14.5-5.el9.x86_64                                                                                                                                             132/367 
  Installing       : python3-cryptography-36.0.1-4.el9.x86_64                                                                                                                                     133/367 
  Installing       : python3-jwcrypto-0.8-5.el9_4.noarch                                                                                                                                          134/367 
  Installing       : python3-decorator-4.4.2-6.el9.noarch                                                                                                                                         135/367 
  Installing       : python3-gssapi-1.6.9-5.el9.x86_64                                                                                                                                            136/367 
  Installing       : python3-chardet-4.0.0-5.el9.noarch                                                                                                                                           137/367 
  Installing       : python3-requests-2.25.1-8.el9.noarch                                                                                                                                         138/367 
  Installing       : python3-idm-pki-11.5.0-1.el9.noarch                                                                                                                                          139/367 
  Installing       : idm-pki-base-11.5.0-1.el9.noarch                                                                                                                                             140/367 
  Running scriptlet: idm-pki-base-11.5.0-1.el9.noarch                                                                                                                                             140/367 
  Installing       : pkgconf-m4-1.7.3-10.el9.noarch                                                                                                                                               141/367 
  Installing       : mailcap-2.1.49-5.el9.noarch                                                                                                                                                  142/367 
  Installing       : httpd-core-2.4.57-8.el9.x86_64                                                                                                                                               143/367 
  Installing       : mod_auth_gssapi-1.6.3-7.el9.x86_64                                                                                                                                           144/367 
  Installing       : mod_lookup_identity-1.0.0-15.el9.x86_64                                                                                                                                      145/367 
  Installing       : mod_lua-2.4.57-8.el9.x86_64                                                                                                                                                  146/367 
  Installing       : mod_session-2.4.57-8.el9.x86_64                                                                                                                                              147/367 
  Installing       : python3-mod_wsgi-4.7.1-11.el9.x86_64                                                                                                                                         148/367 
  Installing       : libsss_autofs-2.9.4-6.el9_4.x86_64                                                                                                                                           149/367 
  Installing       : libpkgconf-1.7.3-10.el9.x86_64                                                                                                                                               150/367 
  Installing       : pkgconf-1.7.3-10.el9.x86_64                                                                                                                                                  151/367 
  Installing       : pkgconf-pkg-config-1.7.3-10.el9.x86_64                                                                                                                                       152/367 
  Installing       : bash-completion-1:2.11-5.el9.noarch                                                                                                                                          153/367 
  Installing       : libev-4.33-5.el9.x86_64                                                                                                                                                      154/367 
  Installing       : libverto-libev-0.3.2-3.el9.x86_64                                                                                                                                            155/367 
  Installing       : gssproxy-0.8.4-6.el9.x86_64                                                                                                                                                  156/367 
  Running scriptlet: gssproxy-0.8.4-6.el9.x86_64                                                                                                                                                  156/367 
  Running scriptlet: nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                              157/367 
  Installing       : nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                              157/367 
  Running scriptlet: nfs-utils-1:2.5.4-25.el9.x86_64                                                                                                                                              157/367 
  Installing       : krb5-server-1.21.1-1.el9.x86_64                                                                                                                                              158/367 
  Running scriptlet: krb5-server-1.21.1-1.el9.x86_64                                                                                                                                              158/367 
  Installing       : libatomic-11.4.1-3.el9.alma.1.x86_64                                                                                                                                         159/367 
  Installing       : webkit2gtk3-jsc-2.42.5-1.el9.x86_64                                                                                                                                          160/367 
  Installing       : libproxy-webkitgtk4-0.4.15-35.el9.x86_64                                                                                                                                     161/367 
  Installing       : glib-networking-2.68.3-3.el9.x86_64                                                                                                                                          162/367 
  Installing       : libsoup-2.72.0-8.el9.x86_64                                                                                                                                                  163/367 
  Installing       : libappstream-glib-0.7.18-4.el9.x86_64                                                                                                                                        164/367 
  Installing       : osinfo-db-tools-1.10.0-1.el9.x86_64                                                                                                                                          165/367 
  Installing       : graphite2-1.3.14-9.el9.x86_64                                                                                                                                                166/367 
  Installing       : harfbuzz-2.7.4-10.el9.x86_64                                                                                                                                                 167/367 
  Installing       : freetype-2.10.4-9.el9.x86_64                                                                                                                                                 168/367 
  Installing       : fontconfig-2.14.0-2.el9_1.x86_64                                                                                                                                             169/367 
  Running scriptlet: fontconfig-2.14.0-2.el9_1.x86_64                                                                                                                                             169/367 
  Installing       : ttmkfdir-3.0.9-65.el9.x86_64                                                                                                                                                 170/367 
  Installing       : fuse-2.9.9-15.el9.x86_64                                                                                                                                                     171/367 
  Installing       : cyrus-sasl-plain-2.1.27-21.el9.x86_64                                                                                                                                        172/367 
  Installing       : bubblewrap-0.4.1-6.el9.x86_64                                                                                                                                                173/367 
  Installing       : bluez-libs-5.64-2.el9.x86_64                                                                                                                                                 174/367 
  Installing       : autofs-1:5.1.7-58.el9.x86_64                                                                                                                                                 175/367 
  Running scriptlet: autofs-1:5.1.7-58.el9.x86_64                                                                                                                                                 175/367 
  Installing       : ModemManager-glib-1.20.2-1.el9.x86_64                                                                                                                                        176/367 
  Running scriptlet: geoclue2-2.6.0-7.el9.x86_64                                                                                                                                                  177/367 
  Installing       : geoclue2-2.6.0-7.el9.x86_64                                                                                                                                                  177/367 
  Running scriptlet: geoclue2-2.6.0-7.el9.x86_64                                                                                                                                                  177/367 
  Installing       : xkeyboard-config-2.33-2.el9.noarch                                                                                                                                           178/367 
  Installing       : libxkbcommon-1.0.3-4.el9.x86_64                                                                                                                                              179/367 
  Installing       : xdg-dbus-proxy-0.1.3-1.el9.x86_64                                                                                                                                            180/367 
  Installing       : webrtc-audio-processing-0.3.1-8.el9.x86_64                                                                                                                                   181/367 
  Installing       : upower-0.99.13-2.el9.x86_64                                                                                                                                                  182/367 
  Running scriptlet: upower-0.99.13-2.el9.x86_64                                                                                                                                                  182/367 
Created symlink /etc/systemd/system/graphical.target.wants/upower.service → /usr/lib/systemd/system/upower.service.

  Installing       : totem-pl-parser-3.26.6-2.el9.x86_64                                                                                                                                          183/367 
  Installing       : sscg-3.0.0-7.el9.x86_64                                                                                                                                                      184/367 
  Installing       : mod_ssl-1:2.4.57-8.el9.x86_64                                                                                                                                                185/367 
  Installing       : sound-theme-freedesktop-0.8-17.el9.noarch                                                                                                                                    186/367 
  Running scriptlet: sound-theme-freedesktop-0.8-17.el9.noarch                                                                                                                                    186/367 
  Running scriptlet: softhsm-2.6.1-7.el9.2.x86_64                                                                                                                                                 187/367 
  Installing       : softhsm-2.6.1-7.el9.2.x86_64                                                                                                                                                 187/367 
  Running scriptlet: softhsm-2.6.1-7.el9.2.x86_64                                                                                                                                                 187/367 
  Installing       : python3-pytz-2021.1-5.el9.noarch                                                                                                                                             188/367 
  Installing       : python3-babel-2.9.1-2.el9.noarch                                                                                                                                             189/367 
  Installing       : python3-psutil-5.8.0-12.el9.x86_64                                                                                                                                           190/367 
  Installing       : python3-netifaces-0.10.6-15.el9.x86_64                                                                                                                                       191/367 
  Installing       : python3-markupsafe-1.1.1-12.el9.x86_64                                                                                                                                       192/367 
  Installing       : python3-jinja2-2.11.3-5.el9.noarch                                                                                                                                           193/367 
  Installing       : python3-audit-3.1.2-2.el9.x86_64                                                                                                                                             194/367 
  Installing       : python3-argcomplete-1.12.0-5.el9.noarch                                                                                                                                      195/367 
  Installing       : publicsuffix-list-20210518-3.el9.noarch                                                                                                                                      196/367 
  Installing       : poppler-data-0.4.9-9.el9.noarch                                                                                                                                              197/367 
  Installing       : perl-Tie-4.6-481.el9.noarch                                                                                                                                                  198/367 
  Installing       : perl-Term-ReadLine-1.17-481.el9.noarch                                                                                                                                       199/367 
  Installing       : perl-Devel-Peek-1.28-481.el9.x86_64                                                                                                                                          200/367 
  Installing       : perl-debugger-1.56-481.el9.noarch                                                                                                                                            201/367 
  Installing       : perl-DB_File-1.855-4.el9.x86_64                                                                                                                                              202/367 
  Installing       : perl-Compress-Raw-Lzma-2.101-3.el9.x86_64                                                                                                                                    203/367 
  Installing       : perl-Compress-Raw-Bzip2-2.101-5.el9.x86_64                                                                                                                                   204/367 
  Installing       : perl-IO-Compress-2.102-4.el9.noarch                                                                                                                                          205/367 
  Installing       : perl-IO-Compress-Lzma-2.101-4.el9.noarch                                                                                                                                     206/367 
  Installing       : perl-IO-Zlib-1:1.11-4.el9.noarch                                                                                                                                             207/367 
  Installing       : perl-Algorithm-Diff-1.2010-4.el9.noarch                                                                                                                                      208/367 
  Installing       : perl-Text-Diff-1.45-13.el9.noarch                                                                                                                                            209/367 
  Installing       : perl-Archive-Tar-2.38-6.el9.noarch                                                                                                                                           210/367 
  Installing       : p11-kit-server-0.25.3-2.el9.x86_64                                                                                                                                           211/367 
  Installing       : ostree-libs-2024.4-3.el9_4.x86_64                                                                                                                                            212/367 
  Installing       : osinfo-db-20231215-1.el9.noarch                                                                                                                                              213/367 
  Installing       : libosinfo-1.10.0-1.el9.x86_64                                                                                                                                                214/367 
  Installing       : orc-0.4.31-6.el9.x86_64                                                                                                                                                      215/367 
  Installing       : openssl-perl-1:3.0.7-27.el9.x86_64                                                                                                                                           216/367 
  Installing       : openjpeg2-2.4.0-7.el9.x86_64                                                                                                                                                 217/367 
  Installing       : lua-posix-35.0-8.el9.x86_64                                                                                                                                                  218/367 
  Installing       : lua-5.4.4-4.el9.x86_64                                                                                                                                                       219/367 
  Installing       : copy-jdk-configs-4.0-3.el9.noarch                                                                                                                                            220/367 
  Installing       : java-11-openjdk-headless-1:11.0.23.0.9-3.el9.x86_64                                                                                                                          221/367 
  Running scriptlet: java-11-openjdk-headless-1:11.0.23.0.9-3.el9.x86_64                                                                                                                          221/367 
  Installing       : java-17-openjdk-headless-1:17.0.11.0.9-2.el9.x86_64                                                                                                                          222/367 
  Running scriptlet: java-17-openjdk-headless-1:17.0.11.0.9-2.el9.x86_64                                                                                                                          222/367 
  Installing       : pki-jackson-core-2.14.1-2.el9.noarch                                                                                                                                         223/367 
  Installing       : slf4j-1.7.30-13.el9.noarch                                                                                                                                                   224/367 
  Installing       : jaxb-api-2.3.3-5.el9.noarch                                                                                                                                                  225/367 
  Installing       : jboss-logging-3.4.1-9.el9.noarch                                                                                                                                             226/367 
  Installing       : pki-jackson-annotations-2.14.1-1.el9.noarch                                                                                                                                  227/367 
  Installing       : pki-jackson-databind-2.14.1-2.el9.noarch                                                                                                                                     228/367 
  Installing       : jboss-jaxrs-2.0-api-1.0.0-16.el9.noarch                                                                                                                                      229/367 
  Installing       : slf4j-jdk14-1.7.30-13.el9.noarch                                                                                                                                             230/367 
  Installing       : pki-jackson-jaxrs-providers-2.14.1-2.el9.noarch                                                                                                                              231/367 
  Installing       : apache-commons-codec-1.15-7.el9.noarch                                                                                                                                       232/367 
  Installing       : apache-commons-io-1:2.8.0-8.el9.noarch                                                                                                                                       233/367 
  Installing       : apache-commons-lang3-3.12.0-6.el9.noarch                                                                                                                                     234/367 
  Installing       : httpcomponents-core-4.4.13-7.el9.noarch                                                                                                                                      235/367 
  Installing       : httpcomponents-client-4.5.13-3.el9.noarch                                                                                                                                    236/367 
  Installing       : apache-commons-cli-1.4-17.el9.noarch                                                                                                                                         237/367 
  Installing       : tomcat-servlet-4.0-api-1:9.0.87-1.el9_4.1.noarch                                                                                                                             238/367 
  Running scriptlet: tomcat-servlet-4.0-api-1:9.0.87-1.el9_4.1.noarch                                                                                                                             238/367 
  Installing       : apache-commons-logging-1.2-29.el9.noarch                                                                                                                                     239/367 
  Installing       : apache-commons-net-3.6-14.el9.noarch                                                                                                                                         240/367 
  Installing       : xml-commons-apis-1.4.01-36.el9.noarch                                                                                                                                        241/367 
  Installing       : idm-jss-5.5.0-1.el9.x86_64                                                                                                                                                   242/367 
  Installing       : javapackages-tools-6.0.0-4.el9.noarch                                                                                                                                        243/367 
  Installing       : xml-commons-resolver-1.2-36.el9.noarch                                                                                                                                       244/367 
  Installing       : tomcat-el-3.0-api-1:9.0.87-1.el9_4.1.noarch                                                                                                                                  245/367 
  Running scriptlet: tomcat-el-3.0-api-1:9.0.87-1.el9_4.1.noarch                                                                                                                                  245/367 
  Installing       : jakarta-activation-1.2.2-5.el9.noarch                                                                                                                                        246/367 
  Installing       : pki-jackson-module-jaxb-annotations-2.14.1-2.el9.noarch                                                                                                                      247/367 
  Installing       : pki-jackson-jaxrs-json-provider-2.14.1-2.el9.noarch                                                                                                                          248/367 
  Installing       : pki-resteasy-jackson2-provider-3.0.26-19.el9.noarch                                                                                                                          249/367 
  Installing       : tomcat-jsp-2.3-api-1:9.0.87-1.el9_4.1.noarch                                                                                                                                 250/367 
  Running scriptlet: tomcat-jsp-2.3-api-1:9.0.87-1.el9_4.1.noarch                                                                                                                                 250/367 
  Installing       : ecj-1:4.20-16.el9.noarch                                                                                                                                                     251/367 
  Installing       : tomcat-lib-1:9.0.87-1.el9_4.1.noarch                                                                                                                                         252/367 
  Installing       : idm-jss-tomcat-5.5.0-1.el9.x86_64                                                                                                                                            253/367 
  Running scriptlet: tomcat-1:9.0.87-1.el9_4.1.noarch                                                                                                                                             254/367 
  Installing       : tomcat-1:9.0.87-1.el9_4.1.noarch                                                                                                                                             254/367 
  Running scriptlet: tomcat-1:9.0.87-1.el9_4.1.noarch                                                                                                                                             254/367 
  Installing       : idm-ldapjdk-5.5.0-1.el9.noarch                                                                                                                                               255/367 
  Installing       : jakarta-annotations-1.3.5-13.el9.noarch                                                                                                                                      256/367 
  Installing       : jdeparser-2.0.3-12.el9.noarch                                                                                                                                                257/367 
  Installing       : jboss-logging-tools-2.2.1-7.el9.noarch                                                                                                                                       258/367 
  Installing       : pki-resteasy-core-3.0.26-19.el9.noarch                                                                                                                                       259/367 
  Installing       : pki-resteasy-client-3.0.26-19.el9.noarch                                                                                                                                     260/367 
  Installing       : pki-resteasy-servlet-initializer-3.0.26-19.el9.noarch                                                                                                                        261/367 
  Installing       : idm-pki-java-11.5.0-1.el9.noarch                                                                                                                                             262/367 
  Installing       : idm-pki-tools-11.5.0-1.el9.x86_64                                                                                                                                            263/367 
  Installing       : low-memory-monitor-2.1-4.el9.x86_64                                                                                                                                          264/367 
  Running scriptlet: low-memory-monitor-2.1-4.el9.x86_64                                                                                                                                          264/367 
Created symlink /etc/systemd/system/basic.target.wants/low-memory-monitor.service → /usr/lib/systemd/system/low-memory-monitor.service.

  Installing       : libwebp-1.2.0-8.el9_3.x86_64                                                                                                                                                 265/367 
  Installing       : libvisual-1:0.4.0-34.el9.x86_64                                                                                                                                              266/367 
  Installing       : libsbc-1.4-9.el9.x86_64                                                                                                                                                      267/367 
  Installing       : libnsl2-2.0.0-1.el9.x86_64                                                                                                                                                   268/367 
  Installing       : libldac-2.0.2.3-10.el9.x86_64                                                                                                                                                269/367 
  Installing       : libjose-11-3.el9.x86_64                                                                                                                                                      270/367 
  Installing       : sssd-idp-2.9.4-6.el9_4.x86_64                                                                                                                                                271/367 
  Installing       : libiptcdata-1.0.5-9.el9.x86_64                                                                                                                                               272/367 
  Installing       : libfontenc-1.1.3-17.el9.x86_64                                                                                                                                               273/367 
  Installing       : mkfontscale-1.2.1-3.el9.x86_64                                                                                                                                               274/367 
  Installing       : xorg-x11-fonts-Type1-7.5-33.el9.noarch                                                                                                                                       275/367 
  Running scriptlet: xorg-x11-fonts-Type1-7.5-33.el9.noarch                                                                                                                                       275/367 
  Installing       : libexif-0.6.22-6.el9.x86_64                                                                                                                                                  276/367 
  Installing       : libepoxy-1.5.5-4.el9.x86_64                                                                                                                                                  277/367 
  Installing       : libdb-utils-5.3.28-53.el9.x86_64                                                                                                                                             278/367 
  Installing       : libdatrie-0.2.13-4.el9.x86_64                                                                                                                                                279/367 
  Installing       : libthai-0.1.28-8.el9.x86_64                                                                                                                                                  280/367 
  Installing       : libasyncns-0.8-22.el9.x86_64                                                                                                                                                 281/367 
  Installing       : libX11-common-1.7.0-9.el9.noarch                                                                                                                                             282/367 
  Installing       : libX11-1.7.0-9.el9.x86_64                                                                                                                                                    283/367 
  Installing       : libXext-1.3.4-8.el9.x86_64                                                                                                                                                   284/367 
  Installing       : libXrender-0.9.10-16.el9.x86_64                                                                                                                                              285/367 
  Installing       : cairo-1.17.4-7.el9.x86_64                                                                                                                                                    286/367 
  Installing       : libXi-1.7.10-8.el9.x86_64                                                                                                                                                    287/367 
  Installing       : libXfixes-5.0.3-16.el9.x86_64                                                                                                                                                288/367 
  Installing       : cairo-gobject-1.17.4-7.el9.x86_64                                                                                                                                            289/367 
  Installing       : libXtst-1.2.3-16.el9.x86_64                                                                                                                                                  290/367 
  Installing       : libXcomposite-0.4.5-7.el9.x86_64                                                                                                                                             291/367 
  Installing       : at-spi2-core-2.40.3-1.el9.x86_64                                                                                                                                             292/367 
  Installing       : at-spi2-atk-2.38.0-4.el9.x86_64                                                                                                                                              293/367 
  Installing       : libXcursor-1.2.0-7.el9.x86_64                                                                                                                                                294/367 
  Installing       : libXdamage-1.1.5-7.el9.x86_64                                                                                                                                                295/367 
  Installing       : libXft-2.3.3-8.el9.x86_64                                                                                                                                                    296/367 
  Installing       : pango-1.48.7-3.el9.x86_64                                                                                                                                                    297/367 
  Installing       : librsvg2-2.50.7-3.el9.x86_64                                                                                                                                                 298/367 
  Installing       : libXrandr-1.5.2-8.el9.x86_64                                                                                                                                                 299/367 
  Installing       : libXinerama-1.1.4-10.el9.x86_64                                                                                                                                              300/367 
  Installing       : libXv-1.0.11-16.el9.x86_64                                                                                                                                                   301/367 
  Installing       : libXxf86vm-1.1.4-18.el9.x86_64                                                                                                                                               302/367 
  Installing       : libglvnd-glx-1:1.3.4-1.el9.x86_64                                                                                                                                            303/367 
  Installing       : mesa-libGL-23.3.3-1.el9.x86_64                                                                                                                                               304/367 
  Installing       : jbigkit-libs-2.1-23.el9.x86_64                                                                                                                                               305/367 
  Installing       : libtiff-4.4.0-12.el9.x86_64                                                                                                                                                  306/367 
  Installing       : gdk-pixbuf2-modules-2.42.6-3.el9.x86_64                                                                                                                                      307/367 
  Installing       : libgxps-0.3.2-3.el9.x86_64                                                                                                                                                   308/367 
  Installing       : poppler-21.01.0-19.el9.x86_64                                                                                                                                                309/367 
  Installing       : poppler-glib-21.01.0-19.el9.x86_64                                                                                                                                           310/367 
  Installing       : ipa-healthcheck-core-0.16-3.el9.noarch                                                                                                                                       311/367 
  Installing       : hicolor-icon-theme-0.17-13.el9.noarch                                                                                                                                        312/367 
  Installing       : gsm-1.0.19-6.el9.x86_64                                                                                                                                                      313/367 
  Installing       : libsndfile-1.0.31-8.el9.x86_64                                                                                                                                               314/367 
  Installing       : pulseaudio-libs-15.0-2.el9.x86_64                                                                                                                                            315/367 
  Installing       : libcanberra-0.30-27.el9.x86_64                                                                                                                                               316/367 
  Running scriptlet: libcanberra-0.30-27.el9.x86_64                                                                                                                                               316/367 
  Installing       : graphene-1.10.6-2.el9.x86_64                                                                                                                                                 317/367 
  Installing       : gstreamer1-plugins-base-1.22.1-2.el9.x86_64                                                                                                                                  318/367 
  Installing       : giflib-5.2.1-9.el9.x86_64                                                                                                                                                    319/367 
  Installing       : flatpak-session-helper-1.12.8-1.el9.x86_64                                                                                                                                   320/367 
  Installing       : fdk-aac-free-2.0.0-8.el9.x86_64                                                                                                                                              321/367 
  Running scriptlet: pipewire-1.0.1-1.el9.x86_64                                                                                                                                                  322/367 
  Installing       : pipewire-1.0.1-1.el9.x86_64                                                                                                                                                  322/367 
  Running scriptlet: pipewire-1.0.1-1.el9.x86_64                                                                                                                                                  322/367 
Created symlink /etc/systemd/user/sockets.target.wants/pipewire.socket → /usr/lib/systemd/user/pipewire.socket.

  Installing       : pipewire-libs-1.0.1-1.el9.x86_64                                                                                                                                             323/367 
  Installing       : wireplumber-0.4.14-1.el9.x86_64                                                                                                                                              324/367 
  Installing       : wireplumber-libs-0.4.14-1.el9.x86_64                                                                                                                                         325/367 
  Installing       : pipewire-jack-audio-connection-kit-libs-1.0.1-1.el9.x86_64                                                                                                                   326/367 
  Installing       : exempi-2.6.0-0.2.20211007gite23c213.el9.x86_64                                                                                                                               327/367 
  Installing       : libtracker-sparql-3.1.2-3.el9_1.x86_64                                                                                                                                       328/367 
  Installing       : tracker-3.1.2-3.el9_1.x86_64                                                                                                                                                 329/367 
  Running scriptlet: tracker-3.1.2-3.el9_1.x86_64                                                                                                                                                 329/367 
  Installing       : tracker-miners-3.1.2-4.el9_3.x86_64                                                                                                                                          330/367 
  Running scriptlet: tracker-miners-3.1.2-4.el9_3.x86_64                                                                                                                                          330/367 
  Installing       : cyrus-sasl-md5-2.1.27-21.el9.x86_64                                                                                                                                          331/367 
  Installing       : checkpolicy-3.6-1.el9.x86_64                                                                                                                                                 332/367 
  Installing       : python3-policycoreutils-3.6-2.1.el9.noarch                                                                                                                                   333/367 
  Installing       : policycoreutils-python-utils-3.6-2.1.el9.noarch                                                                                                                              334/367 
  Installing       : python3-lib389-2.4.5-6.el9_4.noarch                                                                                                                                          335/367 
  Installing       : 389-ds-base-2.4.5-6.el9_4.x86_64                                                                                                                                             336/367 
  Running scriptlet: 389-ds-base-2.4.5-6.el9_4.x86_64                                                                                                                                             336/367 
  Installing       : slapi-nis-0.60.0-5.el9_3.x86_64                                                                                                                                              337/367 
  Installing       : flatpak-selinux-1.12.8-1.el9.noarch                                                                                                                                          338/367 
  Running scriptlet: flatpak-selinux-1.12.8-1.el9.noarch                                                                                                                                          338/367 
  Installing       : xdg-desktop-portal-1.12.6-1.el9.x86_64                                                                                                                                       339/367 
  Running scriptlet: xdg-desktop-portal-1.12.6-1.el9.x86_64                                                                                                                                       339/367 
  Running scriptlet: flatpak-1.12.8-1.el9.x86_64                                                                                                                                                  340/367 
  Installing       : flatpak-1.12.8-1.el9.x86_64                                                                                                                                                  340/367 
  Running scriptlet: ipa-selinux-4.11.0-10.el9_4.noarch                                                                                                                                           341/367 
  Installing       : ipa-selinux-4.11.0-10.el9_4.noarch                                                                                                                                           341/367 
  Running scriptlet: ipa-selinux-4.11.0-10.el9_4.noarch                                                                                                                                           341/367 
  Installing       : ipa-common-4.11.0-10.el9_4.noarch                                                                                                                                            342/367 
  Installing       : python3-ipalib-4.11.0-10.el9_4.noarch                                                                                                                                        343/367 
  Installing       : python3-ipaclient-4.11.0-10.el9_4.noarch                                                                                                                                     344/367 
  Installing       : ipa-client-4.11.0-10.el9_4.x86_64                                                                                                                                            345/367 
  Running scriptlet: ipa-client-4.11.0-10.el9_4.x86_64                                                                                                                                            345/367 
  Installing       : almalinux-logos-ipa-90.5.1-1.1.el9.noarch                                                                                                                                    346/367 
  Installing       : almalinux-logos-httpd-90.5.1-1.1.el9.noarch                                                                                                                                  347/367 
  Installing       : mod_http2-2.0.26-2.el9_4.x86_64                                                                                                                                              348/367 
  Installing       : httpd-2.4.57-8.el9.x86_64                                                                                                                                                    349/367 
  Running scriptlet: httpd-2.4.57-8.el9.x86_64                                                                                                                                                    349/367 
  Running scriptlet: ipa-server-common-4.11.0-10.el9_4.noarch                                                                                                                                     350/367 
  Installing       : ipa-server-common-4.11.0-10.el9_4.noarch                                                                                                                                     350/367 
  Installing       : python3-ipaserver-4.11.0-10.el9_4.noarch                                                                                                                                     351/367 
  Installing       : adwaita-cursor-theme-40.1.1-3.el9.noarch                                                                                                                                     352/367 
  Installing       : adwaita-icon-theme-40.1.1-3.el9.noarch                                                                                                                                       353/367 
  Installing       : libcanberra-gtk3-0.30-27.el9.x86_64                                                                                                                                          354/367 
  Installing       : xdg-desktop-portal-gtk-1.12.0-3.el9.x86_64                                                                                                                                   355/367 
  Running scriptlet: xdg-desktop-portal-gtk-1.12.0-3.el9.x86_64                                                                                                                                   355/367 
  Installing       : gtk3-3.24.31-2.el9.x86_64                                                                                                                                                    356/367 
  Installing       : java-17-openjdk-1:17.0.11.0.9-2.el9.x86_64                                                                                                                                   357/367 
  Running scriptlet: java-17-openjdk-1:17.0.11.0.9-2.el9.x86_64                                                                                                                                   357/367 
  Installing       : java-17-openjdk-devel-1:17.0.11.0.9-2.el9.x86_64                                                                                                                             358/367 
  Running scriptlet: java-17-openjdk-devel-1:17.0.11.0.9-2.el9.x86_64                                                                                                                             358/367 
  Running scriptlet: idm-pki-server-11.5.0-1.el9.noarch                                                                                                                                           359/367 
  Installing       : idm-pki-server-11.5.0-1.el9.noarch                                                                                                                                           359/367 
  Running scriptlet: idm-pki-server-11.5.0-1.el9.noarch                                                                                                                                           359/367 
  Installing       : idm-pki-acme-11.5.0-1.el9.noarch                                                                                                                                             360/367 
  Installing       : idm-pki-ca-11.5.0-1.el9.noarch                                                                                                                                               361/367 
  Installing       : idm-pki-kra-11.5.0-1.el9.noarch                                                                                                                                              362/367 
  Running scriptlet: ipa-server-4.11.0-10.el9_4.x86_64                                                                                                                                            363/367 
  Installing       : ipa-server-4.11.0-10.el9_4.x86_64                                                                                                                                            363/367 
  Running scriptlet: ipa-server-4.11.0-10.el9_4.x86_64                                                                                                                                            363/367 
  Installing       : pipewire-jack-audio-connection-kit-1.0.1-1.el9.x86_64                                                                                                                        364/367 
  Installing       : pipewire-alsa-1.0.1-1.el9.x86_64                                                                                                                                             365/367 
  Installing       : pipewire-pulseaudio-1.0.1-1.el9.x86_64                                                                                                                                       366/367 
  Running scriptlet: pipewire-pulseaudio-1.0.1-1.el9.x86_64                                                                                                                                       366/367 
Created symlink /etc/systemd/user/sockets.target.wants/pipewire-pulse.socket → /usr/lib/systemd/user/pipewire-pulse.socket.

  Installing       : sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                                                                                                                                          367/367 
  Running scriptlet: dconf-0.40.0-6.el9.x86_64                                                                                                                                                    367/367 
  Running scriptlet: nss-3.90.0-7.el9_4.x86_64                                                                                                                                                    367/367 
  Running scriptlet: fontconfig-2.14.0-2.el9_1.x86_64                                                                                                                                             367/367 
  Running scriptlet: copy-jdk-configs-4.0-3.el9.noarch                                                                                                                                            367/367 
  Running scriptlet: java-11-openjdk-headless-1:11.0.23.0.9-3.el9.x86_64                                                                                                                          367/367 
  Running scriptlet: java-17-openjdk-headless-1:17.0.11.0.9-2.el9.x86_64                                                                                                                          367/367 
  Running scriptlet: wireplumber-0.4.14-1.el9.x86_64                                                                                                                                              367/367 
Created symlink /etc/systemd/user/pipewire-session-manager.service → /usr/lib/systemd/user/wireplumber.service.
Created symlink /etc/systemd/user/pipewire.service.wants/wireplumber.service → /usr/lib/systemd/user/wireplumber.service.

  Running scriptlet: ipa-selinux-4.11.0-10.el9_4.noarch                                                                                                                                           367/367 
  Running scriptlet: httpd-2.4.57-8.el9.x86_64                                                                                                                                                    367/367 
  Running scriptlet: java-17-openjdk-1:17.0.11.0.9-2.el9.x86_64                                                                                                                                   367/367 
  Running scriptlet: java-17-openjdk-devel-1:17.0.11.0.9-2.el9.x86_64                                                                                                                             367/367 
  Running scriptlet: ipa-server-4.11.0-10.el9_4.x86_64                                                                                                                                            367/367 
  Running scriptlet: sssd-nfs-idmap-2.9.4-6.el9_4.x86_64                                                                                                                                          367/367 
  Verifying        : 389-ds-base-2.4.5-6.el9_4.x86_64                                                                                                                                               1/367 
  Verifying        : 389-ds-base-libs-2.4.5-6.el9_4.x86_64                                                                                                                                          2/367 
  Verifying        : abattis-cantarell-fonts-0.301-4.el9.noarch                                                                                                                                     3/367 
  Verifying        : adwaita-cursor-theme-40.1.1-3.el9.noarch                                                                                                                                       4/367 
  Verifying        : adwaita-icon-theme-40.1.1-3.el9.noarch                                                                                                                                         5/367 
  Verifying        : almalinux-logos-httpd-90.5.1-1.1.el9.noarch                                                                                                                                    6/367 
  Verifying        : almalinux-logos-ipa-90.5.1-1.1.el9.noarch                                                                                                                                      7/367 
  Verifying        : alsa-lib-1.2.10-2.el9.x86_64                                                                                                                                                   8/367 
  Verifying        : apache-commons-cli-1.4-17.el9.noarch                                                                                                                                           9/367 
  Verifying        : apache-commons-codec-1.15-7.el9.noarch                                                                                                                                        10/367 
  Verifying        : apache-commons-io-1:2.8.0-8.el9.noarch                                                                                                                                        11/367 
  Verifying        : apache-commons-lang3-3.12.0-6.el9.noarch                                                                                                                                      12/367 
  Verifying        : apache-commons-logging-1.2-29.el9.noarch                                                                                                                                      13/367 
  Verifying        : apache-commons-net-3.6-14.el9.noarch                                                                                                                                          14/367 
  Verifying        : apr-1.7.0-12.el9_3.x86_64                                                                                                                                                     15/367 
  Verifying        : apr-util-1.6.1-23.el9.x86_64                                                                                                                                                  16/367 
  Verifying        : apr-util-bdb-1.6.1-23.el9.x86_64                                                                                                                                              17/367 
  Verifying        : apr-util-openssl-1.6.1-23.el9.x86_64                                                                                                                                          18/367 
  Verifying        : at-spi2-atk-2.38.0-4.el9.x86_64                                                                                                                                               19/367 
  Verifying        : at-spi2-core-2.40.3-1.el9.x86_64                                                                                                                                              20/367 
  Verifying        : atk-2.36.0-5.el9.x86_64                                                                                                                                                       21/367 
  Verifying        : augeas-libs-1.13.0-5.el9.x86_64                                                                                                                                               22/367 
  Verifying        : avahi-glib-0.8-20.el9.x86_64                                                                                                                                                  23/367 
  Verifying        : cairo-1.17.4-7.el9.x86_64                                                                                                                                                     24/367 
  Verifying        : cairo-gobject-1.17.4-7.el9.x86_64                                                                                                                                             25/367 
  Verifying        : certmonger-0.79.17-2.el9.x86_64                                                                                                                                               26/367 
  Verifying        : checkpolicy-3.6-1.el9.x86_64                                                                                                                                                  27/367 
  Verifying        : colord-libs-1.4.5-4.el9.x86_64                                                                                                                                                28/367 
  Verifying        : copy-jdk-configs-4.0-3.el9.noarch                                                                                                                                             29/367 
  Verifying        : cyrus-sasl-md5-2.1.27-21.el9.x86_64                                                                                                                                           30/367 
  Verifying        : dconf-0.40.0-6.el9.x86_64                                                                                                                                                     31/367 
  Verifying        : ecj-1:4.20-16.el9.noarch                                                                                                                                                      32/367 
  Verifying        : exempi-2.6.0-0.2.20211007gite23c213.el9.x86_64                                                                                                                                33/367 
  Verifying        : exiv2-0.27.5-2.el9.x86_64                                                                                                                                                     34/367 
  Verifying        : exiv2-libs-0.27.5-2.el9.x86_64                                                                                                                                                35/367 
  Verifying        : fdk-aac-free-2.0.0-8.el9.x86_64                                                                                                                                               36/367 
  Verifying        : flac-libs-1.3.3-10.el9_2.1.x86_64                                                                                                                                             37/367 
  Verifying        : flatpak-1.12.8-1.el9.x86_64                                                                                                                                                   38/367 
  Verifying        : flatpak-selinux-1.12.8-1.el9.noarch                                                                                                                                           39/367 
  Verifying        : flatpak-session-helper-1.12.8-1.el9.x86_64                                                                                                                                    40/367 
  Verifying        : fontawesome-fonts-1:4.7.0-13.el9.noarch                                                                                                                                       41/367 
  Verifying        : fontconfig-2.14.0-2.el9_1.x86_64                                                                                                                                              42/367 
  Verifying        : fribidi-1.0.10-6.el9.2.x86_64                                                                                                                                                 43/367 
  Verifying        : gdk-pixbuf2-2.42.6-3.el9.x86_64                                                                                                                                               44/367 
  Verifying        : gdk-pixbuf2-modules-2.42.6-3.el9.x86_64                                                                                                                                       45/367 
  Verifying        : geoclue2-2.6.0-7.el9.x86_64                                                                                                                                                   46/367 
  Verifying        : giflib-5.2.1-9.el9.x86_64                                                                                                                                                     47/367 
  Verifying        : graphene-1.10.6-2.el9.x86_64                                                                                                                                                  48/367 
  Verifying        : gsm-1.0.19-6.el9.x86_64                                                                                                                                                       49/367 
  Verifying        : gstreamer1-1.22.1-2.el9.x86_64                                                                                                                                                50/367 
  Verifying        : gstreamer1-plugins-base-1.22.1-2.el9.x86_64                                                                                                                                   51/367 
  Verifying        : gtk-update-icon-cache-3.24.31-2.el9.x86_64                                                                                                                                    52/367 
  Verifying        : gtk3-3.24.31-2.el9.x86_64                                                                                                                                                     53/367 
  Verifying        : hicolor-icon-theme-0.17-13.el9.noarch                                                                                                                                         54/367 
  Verifying        : httpcomponents-client-4.5.13-3.el9.noarch                                                                                                                                     55/367 
  Verifying        : httpcomponents-core-4.4.13-7.el9.noarch                                                                                                                                       56/367 
  Verifying        : httpd-2.4.57-8.el9.x86_64                                                                                                                                                     57/367 
  Verifying        : httpd-core-2.4.57-8.el9.x86_64                                                                                                                                                58/367 
  Verifying        : httpd-filesystem-2.4.57-8.el9.noarch                                                                                                                                          59/367 
  Verifying        : httpd-tools-2.4.57-8.el9.x86_64                                                                                                                                               60/367 
  Verifying        : idm-jss-5.5.0-1.el9.x86_64                                                                                                                                                    61/367 
  Verifying        : idm-jss-tomcat-5.5.0-1.el9.x86_64                                                                                                                                             62/367 
  Verifying        : idm-ldapjdk-5.5.0-1.el9.noarch                                                                                                                                                63/367 
  Verifying        : idm-pki-acme-11.5.0-1.el9.noarch                                                                                                                                              64/367 
  Verifying        : idm-pki-base-11.5.0-1.el9.noarch                                                                                                                                              65/367 
  Verifying        : idm-pki-ca-11.5.0-1.el9.noarch                                                                                                                                                66/367 
  Verifying        : idm-pki-java-11.5.0-1.el9.noarch                                                                                                                                              67/367 
  Verifying        : idm-pki-kra-11.5.0-1.el9.noarch                                                                                                                                               68/367 
  Verifying        : idm-pki-server-11.5.0-1.el9.noarch                                                                                                                                            69/367 
  Verifying        : idm-pki-tools-11.5.0-1.el9.x86_64                                                                                                                                             70/367 
  Verifying        : ipa-client-4.11.0-10.el9_4.x86_64                                                                                                                                             71/367 
  Verifying        : ipa-client-common-4.11.0-10.el9_4.noarch                                                                                                                                      72/367 
  Verifying        : ipa-common-4.11.0-10.el9_4.noarch                                                                                                                                             73/367 
  Verifying        : ipa-healthcheck-core-0.16-3.el9.noarch                                                                                                                                        74/367 
  Verifying        : ipa-selinux-4.11.0-10.el9_4.noarch                                                                                                                                            75/367 
  Verifying        : ipa-server-4.11.0-10.el9_4.x86_64                                                                                                                                             76/367 
  Verifying        : ipa-server-common-4.11.0-10.el9_4.noarch                                                                                                                                      77/367 
  Verifying        : iso-codes-4.6.0-3.el9.noarch                                                                                                                                                  78/367 
  Verifying        : jakarta-activation-1.2.2-5.el9.noarch                                                                                                                                         79/367 
  Verifying        : jakarta-annotations-1.3.5-13.el9.noarch                                                                                                                                       80/367 
  Verifying        : java-11-openjdk-headless-1:11.0.23.0.9-3.el9.x86_64                                                                                                                           81/367 
  Verifying        : java-17-openjdk-1:17.0.11.0.9-2.el9.x86_64                                                                                                                                    82/367 
  Verifying        : java-17-openjdk-devel-1:17.0.11.0.9-2.el9.x86_64                                                                                                                              83/367 
  Verifying        : java-17-openjdk-headless-1:17.0.11.0.9-2.el9.x86_64                                                                                                                           84/367 
  Verifying        : javapackages-filesystem-6.0.0-4.el9.noarch                                                                                                                                    85/367 
  Verifying        : javapackages-tools-6.0.0-4.el9.noarch                                                                                                                                         86/367 
  Verifying        : jaxb-api-2.3.3-5.el9.noarch                                                                                                                                                   87/367 
  Verifying        : jbigkit-libs-2.1-23.el9.x86_64                                                                                                                                                88/367 
  Verifying        : jboss-jaxrs-2.0-api-1.0.0-16.el9.noarch                                                                                                                                       89/367 
  Verifying        : jboss-logging-3.4.1-9.el9.noarch                                                                                                                                              90/367 
  Verifying        : jboss-logging-tools-2.2.1-7.el9.noarch                                                                                                                                        91/367 
  Verifying        : jdeparser-2.0.3-12.el9.noarch                                                                                                                                                 92/367 
  Verifying        : langpacks-core-font-en-3.0-16.el9.noarch                                                                                                                                      93/367 
  Verifying        : lcms2-2.12-3.el9.x86_64                                                                                                                                                       94/367 
  Verifying        : libX11-1.7.0-9.el9.x86_64                                                                                                                                                     95/367 
  Verifying        : libX11-common-1.7.0-9.el9.noarch                                                                                                                                              96/367 
  Verifying        : libX11-xcb-1.7.0-9.el9.x86_64                                                                                                                                                 97/367 
  Verifying        : libXau-1.0.9-8.el9.x86_64                                                                                                                                                     98/367 
  Verifying        : libXcomposite-0.4.5-7.el9.x86_64                                                                                                                                              99/367 
  Verifying        : libXcursor-1.2.0-7.el9.x86_64                                                                                                                                                100/367 
  Verifying        : libXdamage-1.1.5-7.el9.x86_64                                                                                                                                                101/367 
  Verifying        : libXext-1.3.4-8.el9.x86_64                                                                                                                                                   102/367 
  Verifying        : libXfixes-5.0.3-16.el9.x86_64                                                                                                                                                103/367 
  Verifying        : libXft-2.3.3-8.el9.x86_64                                                                                                                                                    104/367 
  Verifying        : libXi-1.7.10-8.el9.x86_64                                                                                                                                                    105/367 
  Verifying        : libXinerama-1.1.4-10.el9.x86_64                                                                                                                                              106/367 
  Verifying        : libXrandr-1.5.2-8.el9.x86_64                                                                                                                                                 107/367 
  Verifying        : libXrender-0.9.10-16.el9.x86_64                                                                                                                                              108/367 
  Verifying        : libXtst-1.2.3-16.el9.x86_64                                                                                                                                                  109/367 
  Verifying        : libXv-1.0.11-16.el9.x86_64                                                                                                                                                   110/367 
  Verifying        : libXxf86vm-1.1.4-18.el9.x86_64                                                                                                                                               111/367 
  Verifying        : libappstream-glib-0.7.18-4.el9.x86_64                                                                                                                                        112/367 
  Verifying        : libasyncns-0.8-22.el9.x86_64                                                                                                                                                 113/367 
  Verifying        : libcanberra-0.30-27.el9.x86_64                                                                                                                                               114/367 
  Verifying        : libcanberra-gtk3-0.30-27.el9.x86_64                                                                                                                                          115/367 
  Verifying        : libdatrie-0.2.13-4.el9.x86_64                                                                                                                                                116/367 
  Verifying        : libdb-utils-5.3.28-53.el9.x86_64                                                                                                                                             117/367 
  Verifying        : libepoxy-1.5.5-4.el9.x86_64                                                                                                                                                  118/367 
  Verifying        : libexif-0.6.22-6.el9.x86_64                                                                                                                                                  119/367 
  Verifying        : libfontenc-1.1.3-17.el9.x86_64                                                                                                                                               120/367 
  Verifying        : libgexiv2-0.12.3-1.el9.x86_64                                                                                                                                                121/367 
  Verifying        : libglvnd-1:1.3.4-1.el9.x86_64                                                                                                                                                122/367 
  Verifying        : libglvnd-egl-1:1.3.4-1.el9.x86_64                                                                                                                                            123/367 
  Verifying        : libglvnd-glx-1:1.3.4-1.el9.x86_64                                                                                                                                            124/367 
  Verifying        : libgsf-1.14.47-5.el9.x86_64                                                                                                                                                  125/367 
  Verifying        : libgxps-0.3.2-3.el9.x86_64                                                                                                                                                   126/367 
  Verifying        : libiptcdata-1.0.5-9.el9.x86_64                                                                                                                                               127/367 
  Verifying        : libjose-11-3.el9.x86_64                                                                                                                                                      128/367 
  Verifying        : libjpeg-turbo-2.0.90-7.el9.x86_64                                                                                                                                            129/367 
  Verifying        : libldac-2.0.2.3-10.el9.x86_64                                                                                                                                                130/367 
  Verifying        : libnotify-0.7.9-8.el9.x86_64                                                                                                                                                 131/367 
  Verifying        : libnsl2-2.0.0-1.el9.x86_64                                                                                                                                                   132/367 
  Verifying        : libogg-2:1.3.4-6.el9.x86_64                                                                                                                                                  133/367 
  Verifying        : libosinfo-1.10.0-1.el9.x86_64                                                                                                                                                134/367 
  Verifying        : libproxy-webkitgtk4-0.4.15-35.el9.x86_64                                                                                                                                     135/367 
  Verifying        : librsvg2-2.50.7-3.el9.x86_64                                                                                                                                                 136/367 
  Verifying        : libsbc-1.4-9.el9.x86_64                                                                                                                                                      137/367 
  Verifying        : libsndfile-1.0.31-8.el9.x86_64                                                                                                                                               138/367 
  Verifying        : libsoup-2.72.0-8.el9.x86_64                                                                                                                                                  139/367 
  Verifying        : libstemmer-0-18.585svn.el9.x86_64                                                                                                                                            140/367 
  Verifying        : libthai-0.1.28-8.el9.x86_64                                                                                                                                                  141/367 
  Verifying        : libtheora-1:1.1.1-31.el9.x86_64                                                                                                                                              142/367 
  Verifying        : libtiff-4.4.0-12.el9.x86_64                                                                                                                                                  143/367 
  Verifying        : libtracker-sparql-3.1.2-3.el9_1.x86_64                                                                                                                                       144/367 
  Verifying        : libvisual-1:0.4.0-34.el9.x86_64                                                                                                                                              145/367 
  Verifying        : libvorbis-1:1.3.7-5.el9.x86_64                                                                                                                                               146/367 
  Verifying        : libwayland-client-1.21.0-1.el9.x86_64                                                                                                                                        147/367 
  Verifying        : libwayland-cursor-1.21.0-1.el9.x86_64                                                                                                                                        148/367 
  Verifying        : libwayland-egl-1.21.0-1.el9.x86_64                                                                                                                                           149/367 
  Verifying        : libwayland-server-1.21.0-1.el9.x86_64                                                                                                                                        150/367 
  Verifying        : libwebp-1.2.0-8.el9_3.x86_64                                                                                                                                                 151/367 
  Verifying        : libxcb-1.13.1-9.el9.x86_64                                                                                                                                                   152/367 
  Verifying        : libxkbcommon-1.0.3-4.el9.x86_64                                                                                                                                              153/367 
  Verifying        : libxshmfence-1.3-10.el9.x86_64                                                                                                                                               154/367 
  Verifying        : low-memory-monitor-2.1-4.el9.x86_64                                                                                                                                          155/367 
  Verifying        : lua-5.4.4-4.el9.x86_64                                                                                                                                                       156/367 
  Verifying        : lua-posix-35.0-8.el9.x86_64                                                                                                                                                  157/367 
  Verifying        : mesa-libEGL-23.3.3-1.el9.x86_64                                                                                                                                              158/367 
  Verifying        : mesa-libGL-23.3.3-1.el9.x86_64                                                                                                                                               159/367 
  Verifying        : mesa-libgbm-23.3.3-1.el9.x86_64                                                                                                                                              160/367 
  Verifying        : mesa-libglapi-23.3.3-1.el9.x86_64                                                                                                                                            161/367 
  Verifying        : mkfontscale-1.2.1-3.el9.x86_64                                                                                                                                               162/367 
  Verifying        : mod_auth_gssapi-1.6.3-7.el9.x86_64                                                                                                                                           163/367 
  Verifying        : mod_http2-2.0.26-2.el9_4.x86_64                                                                                                                                              164/367 
  Verifying        : mod_lookup_identity-1.0.0-15.el9.x86_64                                                                                                                                      165/367 
  Verifying        : mod_lua-2.4.57-8.el9.x86_64                                                                                                                                                  166/367 
  Verifying        : mod_session-2.4.57-8.el9.x86_64                                                                                                                                              167/367 
  Verifying        : mod_ssl-1:2.4.57-8.el9.x86_64                                                                                                                                                168/367 
  Verifying        : nspr-4.35.0-7.el9_4.x86_64                                                                                                                                                   169/367 
  Verifying        : nss-3.90.0-7.el9_4.x86_64                                                                                                                                                    170/367 
  Verifying        : nss-softokn-3.90.0-7.el9_4.x86_64                                                                                                                                            171/367 
  Verifying        : nss-softokn-freebl-3.90.0-7.el9_4.x86_64                                                                                                                                     172/367 
  Verifying        : nss-sysinit-3.90.0-7.el9_4.x86_64                                                                                                                                            173/367 
  Verifying        : nss-tools-3.90.0-7.el9_4.x86_64                                                                                                                                              174/367 
  Verifying        : nss-util-3.90.0-7.el9_4.x86_64                                                                                                                                               175/367 
  Verifying        : oddjob-0.34.7-7.el9.x86_64                                                                                                                                                   176/367 
  Verifying        : oddjob-mkhomedir-0.34.7-7.el9.x86_64                                                                                                                                         177/367 
  Verifying        : open-sans-fonts-1.10-16.el9.noarch                                                                                                                                           178/367 
  Verifying        : openjpeg2-2.4.0-7.el9.x86_64                                                                                                                                                 179/367 
  Verifying        : openssl-perl-1:3.0.7-27.el9.x86_64                                                                                                                                           180/367 
  Verifying        : opus-1.3.1-10.el9.x86_64                                                                                                                                                     181/367 
  Verifying        : orc-0.4.31-6.el9.x86_64                                                                                                                                                      182/367 
  Verifying        : osinfo-db-20231215-1.el9.noarch                                                                                                                                              183/367 
  Verifying        : osinfo-db-tools-1.10.0-1.el9.x86_64                                                                                                                                          184/367 
  Verifying        : ostree-libs-2024.4-3.el9_4.x86_64                                                                                                                                            185/367 
  Verifying        : p11-kit-server-0.25.3-2.el9.x86_64                                                                                                                                           186/367 
  Verifying        : pango-1.48.7-3.el9.x86_64                                                                                                                                                    187/367 
  Verifying        : perl-Algorithm-Diff-1.2010-4.el9.noarch                                                                                                                                      188/367 
  Verifying        : perl-Archive-Tar-2.38-6.el9.noarch                                                                                                                                           189/367 
  Verifying        : perl-Compress-Raw-Bzip2-2.101-5.el9.x86_64                                                                                                                                   190/367 
  Verifying        : perl-Compress-Raw-Lzma-2.101-3.el9.x86_64                                                                                                                                    191/367 
  Verifying        : perl-Compress-Raw-Zlib-2.101-5.el9.x86_64                                                                                                                                    192/367 
  Verifying        : perl-DB_File-1.855-4.el9.x86_64                                                                                                                                              193/367 
  Verifying        : perl-Devel-Peek-1.28-481.el9.x86_64                                                                                                                                          194/367 
  Verifying        : perl-IO-Compress-2.102-4.el9.noarch                                                                                                                                          195/367 
  Verifying        : perl-IO-Compress-Lzma-2.101-4.el9.noarch                                                                                                                                     196/367 
  Verifying        : perl-IO-Zlib-1:1.11-4.el9.noarch                                                                                                                                             197/367 
  Verifying        : perl-Term-ReadLine-1.17-481.el9.noarch                                                                                                                                       198/367 
  Verifying        : perl-Text-Diff-1.45-13.el9.noarch                                                                                                                                            199/367 
  Verifying        : perl-Tie-4.6-481.el9.noarch                                                                                                                                                  200/367 
  Verifying        : perl-debugger-1.56-481.el9.noarch                                                                                                                                            201/367 
  Verifying        : perl-meta-notation-5.32.1-481.el9.noarch                                                                                                                                     202/367 
  Verifying        : perl-sigtrap-1.09-481.el9.noarch                                                                                                                                             203/367 
  Verifying        : perl-threads-1:2.25-460.el9.x86_64                                                                                                                                           204/367 
  Verifying        : perl-threads-shared-1.61-460.el9.x86_64                                                                                                                                      205/367 
  Verifying        : pipewire-1.0.1-1.el9.x86_64                                                                                                                                                  206/367 
  Verifying        : pipewire-alsa-1.0.1-1.el9.x86_64                                                                                                                                             207/367 
  Verifying        : pipewire-jack-audio-connection-kit-1.0.1-1.el9.x86_64                                                                                                                        208/367 
  Verifying        : pipewire-jack-audio-connection-kit-libs-1.0.1-1.el9.x86_64                                                                                                                   209/367 
  Verifying        : pipewire-libs-1.0.1-1.el9.x86_64                                                                                                                                             210/367 
  Verifying        : pipewire-pulseaudio-1.0.1-1.el9.x86_64                                                                                                                                       211/367 
  Verifying        : pixman-0.40.0-6.el9_3.x86_64                                                                                                                                                 212/367 
  Verifying        : pki-jackson-annotations-2.14.1-1.el9.noarch                                                                                                                                  213/367 
  Verifying        : pki-jackson-core-2.14.1-2.el9.noarch                                                                                                                                         214/367 
  Verifying        : pki-jackson-databind-2.14.1-2.el9.noarch                                                                                                                                     215/367 
  Verifying        : pki-jackson-jaxrs-json-provider-2.14.1-2.el9.noarch                                                                                                                          216/367 
  Verifying        : pki-jackson-jaxrs-providers-2.14.1-2.el9.noarch                                                                                                                              217/367 
  Verifying        : pki-jackson-module-jaxb-annotations-2.14.1-2.el9.noarch                                                                                                                      218/367 
  Verifying        : pki-resteasy-client-3.0.26-19.el9.noarch                                                                                                                                     219/367 
  Verifying        : pki-resteasy-core-3.0.26-19.el9.noarch                                                                                                                                       220/367 
  Verifying        : pki-resteasy-jackson2-provider-3.0.26-19.el9.noarch                                                                                                                          221/367 
  Verifying        : pki-resteasy-servlet-initializer-3.0.26-19.el9.noarch                                                                                                                        222/367 
  Verifying        : policycoreutils-python-utils-3.6-2.1.el9.noarch                                                                                                                              223/367 
  Verifying        : poppler-21.01.0-19.el9.x86_64                                                                                                                                                224/367 
  Verifying        : poppler-data-0.4.9-9.el9.noarch                                                                                                                                              225/367 
  Verifying        : poppler-glib-21.01.0-19.el9.x86_64                                                                                                                                           226/367 
  Verifying        : publicsuffix-list-20210518-3.el9.noarch                                                                                                                                      227/367 
  Verifying        : pulseaudio-libs-15.0-2.el9.x86_64                                                                                                                                            228/367 
  Verifying        : python3-argcomplete-1.12.0-5.el9.noarch                                                                                                                                      229/367 
  Verifying        : python3-audit-3.1.2-2.el9.x86_64                                                                                                                                             230/367 
  Verifying        : python3-augeas-0.5.0-25.el9.noarch                                                                                                                                           231/367 
  Verifying        : python3-babel-2.9.1-2.el9.noarch                                                                                                                                             232/367 
  Verifying        : python3-distro-1.5.0-7.el9.noarch                                                                                                                                            233/367 
  Verifying        : python3-gssapi-1.6.9-5.el9.x86_64                                                                                                                                            234/367 
  Verifying        : python3-idm-pki-11.5.0-1.el9.noarch                                                                                                                                          235/367 
  Verifying        : python3-ipaclient-4.11.0-10.el9_4.noarch                                                                                                                                     236/367 
  Verifying        : python3-ipalib-4.11.0-10.el9_4.noarch                                                                                                                                        237/367 
  Verifying        : python3-ipaserver-4.11.0-10.el9_4.noarch                                                                                                                                     238/367 
  Verifying        : python3-jinja2-2.11.3-5.el9.noarch                                                                                                                                           239/367 
  Verifying        : python3-jwcrypto-0.8-5.el9_4.noarch                                                                                                                                          240/367 
  Verifying        : python3-kdcproxy-1.0.0-7.el9.noarch                                                                                                                                          241/367 
  Verifying        : python3-ldap-3.4.3-2.el9.x86_64                                                                                                                                              242/367 
  Verifying        : python3-lib389-2.4.5-6.el9_4.noarch                                                                                                                                          243/367 
  Verifying        : python3-libsemanage-3.6-1.el9.x86_64                                                                                                                                         244/367 
  Verifying        : python3-lxml-4.6.5-3.el9.x86_64                                                                                                                                              245/367 
  Verifying        : python3-markupsafe-1.1.1-12.el9.x86_64                                                                                                                                       246/367 
  Verifying        : python3-mod_wsgi-4.7.1-11.el9.x86_64                                                                                                                                         247/367 
  Verifying        : python3-netaddr-0.8.0-5.el9.noarch                                                                                                                                           248/367 
  Verifying        : python3-netifaces-0.10.6-15.el9.x86_64                                                                                                                                       249/367 
  Verifying        : python3-policycoreutils-3.6-2.1.el9.noarch                                                                                                                                   250/367 
  Verifying        : python3-psutil-5.8.0-12.el9.x86_64                                                                                                                                           251/367 
  Verifying        : python3-pyasn1-0.4.8-6.el9.noarch                                                                                                                                            252/367 
  Verifying        : python3-pyasn1-modules-0.4.8-6.el9.noarch                                                                                                                                    253/367 
  Verifying        : python3-pytz-2021.1-5.el9.noarch                                                                                                                                             254/367 
  Verifying        : python3-pyusb-1.0.2-13.el9.noarch                                                                                                                                            255/367 
  Verifying        : python3-qrcode-core-6.1-12.el9.noarch                                                                                                                                        256/367 
  Verifying        : python3-yubico-1.3.3-7.el9.noarch                                                                                                                                            257/367 
  Verifying        : rtkit-0.11-28.el9.x86_64                                                                                                                                                     258/367 
  Verifying        : slapi-nis-0.60.0-5.el9_3.x86_64                                                                                                                                              259/367 
  Verifying        : slf4j-1.7.30-13.el9.noarch                                                                                                                                                   260/367 
  Verifying        : slf4j-jdk14-1.7.30-13.el9.noarch                                                                                                                                             261/367 
  Verifying        : softhsm-2.6.1-7.el9.2.x86_64                                                                                                                                                 262/367 
  Verifying        : sound-theme-freedesktop-0.8-17.el9.noarch                                                                                                                                    263/367 
  Verifying        : sscg-3.0.0-7.el9.x86_64                                                                                                                                                      264/367 
  Verifying        : sssd-idp-2.9.4-6.el9_4.x86_64                                                                                                                                                265/367 
  Verifying        : tomcat-1:9.0.87-1.el9_4.1.noarch                                                                                                                                             266/367 
  Verifying        : tomcat-el-3.0-api-1:9.0.87-1.el9_4.1.noarch                                                                                                                                  267/367 
  Verifying        : tomcat-jsp-2.3-api-1:9.0.87-1.el9_4.1.noarch                                                                                                                                 268/367 
  Verifying        : tomcat-lib-1:9.0.87-1.el9_4.1.noarch                                                                                                                                         269/367 
  Verifying        : tomcat-servlet-4.0-api-1:9.0.87-1.el9_4.1.noarch                                                                                                                             270/367 
  Verifying        : totem-pl-parser-3.26.6-2.el9.x86_64                                                                                                                                          271/367 
  Verifying        : tracker-3.1.2-3.el9_1.x86_64                                                                                                                                                 272/367 
  Verifying        : tracker-miners-3.1.2-4.el9_3.x86_64                                                                                                                                          273/367 
  Verifying        : ttmkfdir-3.0.9-65.el9.x86_64                                                                                                                                                 274/367 
  Verifying        : tzdata-java-2024a-1.el9.noarch                                                                                                                                               275/367 
  Verifying        : upower-0.99.13-2.el9.x86_64                                                                                                                                                  276/367 
  Verifying        : webkit2gtk3-jsc-2.42.5-1.el9.x86_64                                                                                                                                          277/367 
  Verifying        : webrtc-audio-processing-0.3.1-8.el9.x86_64                                                                                                                                   278/367 
  Verifying        : wireplumber-0.4.14-1.el9.x86_64                                                                                                                                              279/367 
  Verifying        : wireplumber-libs-0.4.14-1.el9.x86_64                                                                                                                                         280/367 
  Verifying        : xdg-dbus-proxy-0.1.3-1.el9.x86_64                                                                                                                                            281/367 
  Verifying        : xdg-desktop-portal-1.12.6-1.el9.x86_64                                                                                                                                       282/367 
  Verifying        : xdg-desktop-portal-gtk-1.12.0-3.el9.x86_64                                                                                                                                   283/367 
  Verifying        : xkeyboard-config-2.33-2.el9.noarch                                                                                                                                           284/367 
  Verifying        : xml-common-0.6.3-58.el9.noarch                                                                                                                                               285/367 
  Verifying        : xml-commons-apis-1.4.01-36.el9.noarch                                                                                                                                        286/367 
  Verifying        : xml-commons-resolver-1.2-36.el9.noarch                                                                                                                                       287/367 
  Verifying        : xorg-x11-fonts-Type1-7.5-33.el9.noarch                                                                                                                                       288/367 
  Verifying        : ModemManager-glib-1.20.2-1.el9.x86_64                                                                                                                                        289/367 
  Verifying        : adobe-source-code-pro-fonts-2.030.1.050-12.el9.1.noarch                                                                                                                      290/367 
  Verifying        : autofs-1:5.1.7-58.el9.x86_64                                                                                                                                                 291/367 
  Verifying        : avahi-libs-0.8-20.el9.x86_64                                                                                                                                                 292/367 
  Verifying        : bash-completion-1:2.11-5.el9.noarch                                                                                                                                          293/367 
  Verifying        : bluez-libs-5.64-2.el9.x86_64                                                                                                                                                 294/367 
  Verifying        : bubblewrap-0.4.1-6.el9.x86_64                                                                                                                                                295/367 
  Verifying        : cups-libs-1:2.3.3op2-24.el9.x86_64                                                                                                                                           296/367 
  Verifying        : cyrus-sasl-gssapi-2.1.27-21.el9.x86_64                                                                                                                                       297/367 
  Verifying        : cyrus-sasl-plain-2.1.27-21.el9.x86_64                                                                                                                                        298/367 
  Verifying        : dbus-tools-1:1.12.20-8.el9.x86_64                                                                                                                                            299/367 
  Verifying        : dejavu-sans-fonts-2.37-18.el9.noarch                                                                                                                                         300/367 
  Verifying        : fonts-filesystem-1:2.0.5-7.el9.1.noarch                                                                                                                                      301/367 
  Verifying        : freetype-2.10.4-9.el9.x86_64                                                                                                                                                 302/367 
  Verifying        : fuse-2.9.9-15.el9.x86_64                                                                                                                                                     303/367 
  Verifying        : glib-networking-2.68.3-3.el9.x86_64                                                                                                                                          304/367 
  Verifying        : graphite2-1.3.14-9.el9.x86_64                                                                                                                                                305/367 
  Verifying        : gsettings-desktop-schemas-40.0-6.el9.x86_64                                                                                                                                  306/367 
  Verifying        : gssproxy-0.8.4-6.el9.x86_64                                                                                                                                                  307/367 
  Verifying        : harfbuzz-2.7.4-10.el9.x86_64                                                                                                                                                 308/367 
  Verifying        : keyutils-1.6.3-1.el9.x86_64                                                                                                                                                  309/367 
  Verifying        : krb5-pkinit-1.21.1-1.el9.x86_64                                                                                                                                              310/367 
  Verifying        : krb5-server-1.21.1-1.el9.x86_64                                                                                                                                              311/367 
  Verifying        : krb5-workstation-1.21.1-1.el9.x86_64                                                                                                                                         312/367 
  Verifying        : libatomic-11.4.1-3.el9.alma.1.x86_64                                                                                                                                         313/367 
  Verifying        : libev-4.33-5.el9.x86_64                                                                                                                                                      314/367 
  Verifying        : libicu-67.1-9.el9.x86_64                                                                                                                                                     315/367 
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
ipa-server-install --setup-dns

kinit admin
klist
ipa config-mod --defaultshell=/bin/bash
