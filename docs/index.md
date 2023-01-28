# Introduction à Linux

## Say koi linuks

Au début on avait "Unix" : [Unix — Wikipédia](https://fr.wikipedia.org/wiki/Unix)

Après on a eu "Linux": [Linux — Wikipédia](https://fr.wikipedia.org/wiki/Linux)

Linux est un dérivé d'Unix qui est développé à la base par un des guru fondateur du libre et de linux : Linux Torvalds.

Exemple d'unix : Solaris et HP-UX

Exemple de linux : Ubuntu, Debian.

Une page pour aller plus loin dans la différence : [Unix Vs Linux: Quelle est la différence entre UNIX et Linux - Autre](https://fre.myservername.com/unix-vs-linux-what-is-difference-between-unix#:~:text=Linux%20fait%20r%C3%A9f%C3%A9rence%20au%20noyau,de%20syst%C3%A8mes%20d'exploitation%20d%C3%A9riv%C3%A9s.)

## Différentes distributions

Source : Wikipedia

### Historique

* Debian
  
  * Non Commercial
  
  * Très répandu.
  
  * pkg / apt
  
  * debian-installer

* Red Hat
  
  * Commercial
  
  * Très répandu dans le monde pro, et principalement serveurs.
  
  * rpm / Dnf (ex yum)
  
  * Fedora, Centos, Rocky.
  
  * Anaconda

* Suse
  
  * La plus ancienne distribution commercial.
  
  * YaST (Yet Another Setup Tool)

* Arch Linux
  
  * Minimaliste
  
  * Pacman
  
  * Aimée par les barbus

### Enormément d'enfants

Fedora, Ubuntu, Mint, Kali, ...

![periodic-table-distro](/images/periodic-table-of-distro.png)

[DistroWatch.com: Put the fun back into computing. Use Linux, BSD.](https://distrowatch.com/dwres.php?resource=family-tree)

## Les bases

### Dossiers d'arborescence

Par défaut, chaque répertoire à son utilisation/rôle. Les principaux à retenir :

* / : C'est la racine, le point de départ. Attention à ne pas la surcharger et y faire n'importe quoi.

* /etc (Editing Text Config) : C'est l'emplacement dans lequel on va retrouver la plupart des fichiers de configuration

* /tmp : Pour Temporaire, c'est la dedans qu'on va coller toutes les informations temporaires servant aux différents programmes.

* /home : Porte bien son nom là aussi. C'est le dossier par défaut qui va héberger les $HOME des utilisateurs (/home/toto/)

* /mnt : Mnt pour MouNT. C'est ici que font être monter automatiquement les périphériques (cdrom, usb, etc) 

* /root  : C'est la $HOME de l'utilisateur "root". Là ausssi, attention, on a vite fait de la surcharger.

* /var : Dossier dit "variable", mais c'est un peu un faux amis. Il héberge des fichiers qui varient, pas les variables (logs, run, spool, etc)

* /proc, /sys, /dev, /run ... : Tous ces dossiers sont liés au système lui même. Ils hébergent les fichiers liés aux processus, aux fichiers spéciaux, etc ...

Pour aller plus loin dans le détail : [Arborescence du système Linux - Wiki - Wiki](https://www.linuxtricks.fr/wiki/arborescence-du-systeme-linux)

### Systèmes de fichiers

<img src="https://static.javatpoint.com/linux/images/linux-file-system2.png" title="" alt="Linux File System" width="608">

Un système de fichier défini la manière d'organiser le stockage d'information sur un disque dur. Il en existe des dizaines (centaines ?). Chaque FS (FileSystem) a ses avantages et inconvénients. Ils sont caractérisé par la taille maximum des fichiers gérés, la taille des partitions possible, la journalisation et la gestion de snapshot. 

Par exemple, ext3 ne pouvait pas gérer des fichiers plus gros que 2TB. ext4 permet de monter à 16TB.

Sous linux, le plus répandu est probablement "ext4" qui est la 4eme version de "Extended File System"

La relève devrait être assurée par BtrFS (pour BetterFS) 

Les plus répandus et connus sont les suivants.

* ext2, 3 et 4

* jfs

* ReiserFS

* XFS

* Btrfs

### Les shells

Un "shell" permet le lien entre l'utilisateur et le noyau : 

![](https://web.maths.unsw.edu.au/~lafaye/CCM/unix/images/shell.png)

* Bash : Bourne Again Shell : Celui de base aujourd'hui

* Csh, tcsh, ksh : Des ancêtres

* zsh : censé être le futur unique qui les gouvernera tous.

Chaque utilisateur d'un système linux possède un shell par défaut : /bin/bash, /bin/csh, etc ...

Pareil pour les scripts, le "shebang" en début de chaque script permet d'indiquer au système le langage utilisé (#!/bin/bash)

## Commandes de bases

### Must have

* MAN ! : RTFM : Commande a connaitre par coeur. Permet d'avoir l'aide de n'importe quelle commande (y compris elle même)

* vi, vim, nano, emacs : Différents éditeurs, choose your poison. 

* ls : Permet de lister le contenu d'un dossier.

* tail, head : Permettent d'afficher respectivement la fin et le début de fichier. Tail permet de garde le stdin ouvert : tail -f

* dmesg : Permet d'afficher des logs kernel

* cat : Permet d'afficher le contenu d'un fichier

* cp, rm, mv : Manipulation de fichier (copie, remove, move)

* chmod, chown : Modifications des droits.

* df : Disk File. Permet de lister les filesystem et leur utilisation.

* ps : Instantané des processus

* free : Permet de voir rapidement l'utilisation de mémoire

* top : Permet de voir rapidement les conso de cpu/mémoire sous forme de graph

### Des commandes qui lancent des commandes:

* lsscsi : Liste les périphériques dit "SCSI". Ca concerne le bus lui même, donc les disques durs aussi, pas seulement les vieilles cartes des années 50

* nmcli: Permet la configuration raison. On en parlera plus tard.

* systemctl : "system control". On en parle un peu après aussi. Permet de "piloter" le système.

* uname: Récupère des infos sur l'OS, son kernel, son archi.

* lscpu : Récupère des infos sur le CPU. On peut aussi les avoir avec un `cat /proc/cpuinfo`

### Et des commandes qui permettent de gérer les soft

* dnf, apt, yast, pacam, pip, etc ... :

* make, cmake, configure, etc ... 

## Les commandes "système"

### DNF

Nouveau nom de Yum. Equivalent à apt/aptitude sous debian.

Permet l'installation de paquet à condition qu'ils soient dans les dépôt. Un paquet .rpm contient les instruction d'installation, les binaires, fichiers de conf, etc ... d'un logiciel.

* dnf search / install / provide / info

```shell
# dnf search httpd
Dernière vérification de l’expiration des métadonnées effectuée il y a 12 days, 21:31:24 le mer. 11 janv. 2023 16:03:11 EST.
====================================================================================== Nom correspond exactement à : httpd ======================================================================================
httpd.x86_64 : Apache HTTP Server
======================================================================================= Nom & Résumé correspond à : httpd =======================================================================================
almalinux-logos-httpd.noarch : AlmaLinux-related icons and pictures used by httpd
keycloak-httpd-client-install.noarch : Tools to configure Apache HTTPD as Keycloak client
python3-keycloak-httpd-client-install.noarch : Tools to configure Apache HTTPD as Keycloak client
=========================================================================================== Nom correspond à : httpd ============================================================================================
httpd-devel.x86_64 : Development interfaces for the Apache HTTP server
httpd-filesystem.noarch : The basic directory layout for the Apache HTTP server
httpd-manual.noarch : Documentation for the Apache HTTP server
httpd-tools.x86_64 : Tools for use with the Apache HTTP Server
libmicrohttpd.i686 : Lightweight library for embedding a webserver in applications
libmicrohttpd.x86_64 : Lightweight library for embedding a webserver in applications
========================================================================================== Résumé correspond à : httpd ==========================================================================================
mod_auth_mellon.x86_64 : A SAML 2.0 authentication module for the Apache Httpd Server
mod_dav_svn.x86_64 : Apache httpd module for Subversion server
```

```shell
# dnf info httpd
AlmaLinux 8 - BaseOS                                                                                                                                                             5.3 kB/s | 3.8 kB     00:00
AlmaLinux 8 - BaseOS                                                                                                                                                             385 kB/s | 4.0 MB     00:10
AlmaLinux 8 - AppStream                                                                                                                                                          6.9 kB/s | 4.1 kB     00:00
AlmaLinux 8 - AppStream                                                                                                                                                          547 kB/s |  11 MB     00:19
AlmaLinux 8 - Extras                                                                                                                                                             8.2 kB/s | 3.8 kB     00:00
AlmaLinux 8 - Extras                                                                                                                                                              33 kB/s |  18 kB     00:00
Paquets disponibles
Nom          : httpd
Version      : 2.4.37
Publication  : 51.module_el8.7.0+3281+01e58653
Architecture : x86_64
Taille       : 1.4 M
Source       : httpd-2.4.37-51.module_el8.7.0+3281+01e58653.src.rpm
Dépôt        : appstream
Résumé       : Apache HTTP Server
URL          : https://httpd.apache.org/
Licence      : ASL 2.0
Description  : The Apache HTTP Server is a powerful, efficient, and extensible
             : web server.
```

* Configuration des dépôts

```shell
# cat /etc/yum.repos.d/almalinux.repo
# almalinux.repo

[baseos]
name=AlmaLinux $releasever - BaseOS
mirrorlist=https://mirrors.almalinux.org/mirrorlist/$releasever/baseos
# baseurl=https://repo.almalinux.org/almalinux/$releasever/BaseOS/$basearch/os/
enabled=1
gpgcheck=1
countme=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-AlmaLinux

[appstream]
name=AlmaLinux $releasever - AppStream
mirrorlist=https://mirrors.almalinux.org/mirrorlist/$releasever/appstream
# baseurl=https://repo.almalinux.org/almalinux/$releasever/AppStream/$basearch/os/
enabled=1
gpgcheck=1
countme=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-AlmaLinux
```

Il existe des dépôts tiers maintenus par Pierre, Paul ou Jaques.

Exemple avec "Fusion" ou encore "Remi ([Dépôt remi — Wiki Fedora-Fr](https://doc.fedora-fr.org/wiki/D%C3%A9p%C3%B4t_remi) et [Dépôt RPM Fusion — Wiki Fedora-Fr](https://doc.fedora-fr.org/wiki/D%C3%A9p%C3%B4t_RPM_Fusion))

Les dépôts EPEL font partis des plus connu et classique [Extra Packages for Enterprise Linux (EPEL) :: Fedora Docs](https://docs.fedoraproject.org/en-US/epel/)

**Ajouter un dépôt (pour les nuls)**

```shell
dnf install epel-release
```

**Ajouter un dépôt (pour les nuls qui se la pètent)**

```shell
# vim /etc/yum.repos.d/epel.repo
[epel]
name=Extra Packages for Enterprise Linux $releasever - $basearch
#baseurl=https://download.fedoraproject.org/pub/epel/$releasever/Everything/$basearch
metalink=https://mirrors.fedoraproject.org/metalink?repo=epel-$releasever&arch=$basearch&infra=$infra&content=$contentdir
enabled=1
gpgcheck=1
countme=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-8

[epel-debuginfo]
name=Extra Packages for Enterprise Linux $releasever - $basearch - Debug
#baseurl=https://download.fedoraproject.org/pub/epel/$releasever/Everything/$basearch/debug
metalink=https://mirrors.fedoraproject.org/metalink?repo=epel-debug-$releasever&arch=$basearch&infra=$infra&content=$contentdir
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-8
gpgcheck=1

[epel-source]
name=Extra Packages for Enterprise Linux $releasever - $basearch - Source
#baseurl=https://download.fedoraproject.org/pub/epel/$releasever/Everything/SRPMS
metalink=https://mirrors.fedoraproject.org/metalink?repo=epel-source-$releasever&arch=$basearch&infra=$infra&content=$contentdir
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-8
gpgcheck=1
```

### Systemd

Nouveau gestionnaire de service de linux. Remplace init.d. C'est un environnement couteau suisse qui permet de faire plein de choses. Wikipedia parle de "suite logicielle"

* systemctl status/restart/start/stop/enable/list-units

```shell
# systemctl status sshd
● sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2023-01-24 13:22:04 EST; 11min ago
     Docs: man:sshd(8)
           man:sshd_config(5)
 Main PID: 926 (sshd)
    Tasks: 1 (limit: 11347)
   Memory: 6.2M
   CGroup: /system.slice/sshd.service
           └─926 /usr/sbin/sshd -D -oCiphers=aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-ctr,aes256-cbc,aes128-gcm@openssh.com,aes128-ctr,aes128-cbc -oMACs=hmac-sha2-256-etm@openssh.com,hmac-s>

janv. 24 13:22:04 localhost.localdomain systemd[1]: Starting OpenSSH server daemon...
janv. 24 13:22:04 localhost.localdomain sshd[926]: Server listening on 0.0.0.0 port 22.
janv. 24 13:22:04 localhost.localdomain sshd[926]: Server listening on :: port 22.
janv. 24 13:22:04 localhost.localdomain systemd[1]: Started OpenSSH server daemon.
janv. 24 13:20:27 localhost.localdomain sshd[1588]: Accepted password for root from 192.168.50.200 port 51302 ssh2
janv. 24 13:20:27 localhost.localdomain sshd[1588]: pam_unix(sshd:session): session opened for user root by (uid=0)
```

* journactl 

```shell
# journactl -u sshd
-- Logs begin at Tue 2023-01-24 13:20:14 EST, end at Tue 2023-01-24 13:29:01 EST. --
janv. 24 13:22:04 localhost.localdomain systemd[1]: Starting OpenSSH server daemon...
janv. 24 13:22:04 localhost.localdomain sshd[926]: Server listening on 0.0.0.0 port 22.
janv. 24 13:22:04 localhost.localdomain sshd[926]: Server listening on :: port 22.
janv. 24 13:22:04 localhost.localdomain systemd[1]: Started OpenSSH server daemon.
janv. 24 13:20:27 localhost.localdomain sshd[1588]: Accepted password for root from 192.168.50.200 port 51302 ssh2
janv. 24 13:20:27 localhost.localdomain sshd[1588]: pam_unix(sshd:session): session opened for user root by (uid=0)
```

* fichiers .service. 

Ces fichiers décrivent comment doivent fonctionner les services. L'ordre de démarrage, la/les commandes à lancer, avec quels paramètres, etc ...

Exemple avec sshd:

> /usr/lib/systemd/system/sshd.service

```shell
[Unit]
Description=OpenSSH server daemon
Documentation=man:sshd(8) man:sshd_config(5)
After=network.target sshd-keygen.target
Wants=sshd-keygen.target

[Service]
Type=notify
EnvironmentFile=-/etc/crypto-policies/back-ends/opensshserver.config
EnvironmentFile=-/etc/sysconfig/sshd
ExecStart=/usr/sbin/sshd -D $OPTIONS $CRYPTO_POLICY
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure
RestartSec=42s

[Install]
WantedBy=multi-user.target
```

### Nmcli - Network Manager

C'est l'outil de configuration réseau. 3 manière de faire:

- Clic bouton

- Modifier les fichiers de conf (/etc/sysconfig/networks-scripts/xxx)

```shell
# cat /etc/sysconfig/network-scripts/ifcfg-enp0s8
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=none
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=default
NAME=enp0s8
UUID=b37aa47a-eed1-4564-a3d2-11d98d31a63d
DEVICE=enp0s8
ONBOOT=yes
IPADDR=192.168.50.1
PREFIX=24
```

- En ligne de commande avec nmcli:
  
  - nmcli con mod (connexion modify), show, edit
  
  - nmcli device status

```shell
# nmcli con show
NAME    UUID                                  TYPE      DEVICE
enp0s3  abb310de-e47c-4490-9468-03d26709f14a  ethernet  enp0s3
enp0s8  b37aa47a-eed1-4564-a3d2-11d98d31a63d  ethernet  enp0s8
# nmcli device status
DEVICE  TYPE      STATE     CONNECTION
enp0s3  ethernet  connecté  enp0s3
enp0s8  ethernet  connecté  enp0s8
lo      loopback  non-géré  --
```

### LVM -Logical Volume Manager

Permet la création de volume logique. Il ne remplace par la notion de raid et ne gère pas les backup. Il est utilisé par défaut sous linux.

Il fonctionne avec 3 "couches"

* PV : Physical Volume

En gros, c'est une partition utilisable:

```shell
# pvs
  PV         VG        Fmt  Attr PSize  PFree
  /dev/sda2  almalinux lvm2 a--  <7,00g    0

# pvdisplay /dev/sda2
  --- Physical volume ---
  PV Name               /dev/sda2
  VG Name               almalinux
  PV Size               <7,00 GiB / not usable 3,00 MiB
  Allocatable           yes (but full)
  PE Size               4,00 MiB
  Total PE              1791
  Free PE               0
  Allocated PE          1791
  PV UUID               xrRTpi-8cVH-To8h-2GI0-7DLa-zJow-F9AHy2
```

Ici, on est bien sur une partition : sda**2**. Le disque est /dev/sda:

```shell
# fdisk -l
Disque /dev/sda : 8 GiB, 8589934592 octets, 16777216 secteurs
Unités : secteur de 1 × 512 = 512 octets
Taille de secteur (logique / physique) : 512 octets / 512 octets
taille d'E/S (minimale / optimale) : 512 octets / 512 octets
Type d'étiquette de disque : dos
Identifiant de disque : 0xccaf9352

Périphérique Amorçage   Début      Fin Secteurs Taille Id Type
/dev/sda1    *           2048  2099199  2097152     1G 83 Linux
/dev/sda2             2099200 16777215 14678016     7G 8e LVM Linux




Disque /dev/mapper/almalinux-root : 6,2 GiB, 6652166144 octets, 12992512 secteurs
Unités : secteur de 1 × 512 = 512 octets
Taille de secteur (logique / physique) : 512 octets / 512 octets
taille d'E/S (minimale / optimale) : 512 octets / 512 octets


Disque /dev/mapper/almalinux-swap : 820 MiB, 859832320 octets, 1679360 secteurs
Unités : secteur de 1 × 512 = 512 octets
Taille de secteur (logique / physique) : 512 octets / 512 octets
taille d'E/S (minimale / optimale) : 512 octets / 512 octets
```

Ici mon /dev/sda1 est utilisé par ma partition de boot. Mon /dev/sda2 est utilisé par mon lvm.

On peut le voir avec mount et df  :

```shell
# df -h /boot
Sys. de fichiers Taille Utilisé Dispo Uti% Monté sur
/dev/sda1         1014M    221M  794M  22% /boot
```

```shell
# mount -l | grep boot
/dev/sda1 on /boot type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
```

* VG : Volume Group.

Comme son nom l'indique, c'est un groupe de volume. Il englobe les différents PV et les LV (cf après) s'y rattachent

Ici on a qu'un seul PV dans un seul VG, on verra dans un TD pour en rajouter:

```shell
# vgs
  VG        #PV #LV #SN Attr   VSize  VFree
  almalinux   1   2   0 wz--n- <7,00g    0
# vgdisplay almalinux
  --- Volume group ---
  VG Name               almalinux
  System ID
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  3
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               2
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <7,00 GiB
  PE Size               4,00 MiB
  Total PE              1791
  Alloc PE / Size       1791 / <7,00 GiB
  Free  PE / Size       0 / 0
  VG UUID               Tj7vzn-nubi-CvHp-yQbR-DIIS-g2yY-oyciPz
```

* LV : Logical Volume

Dernier maillon de la chaine, c'est celui dans lequel on va déposer nos données.

Généralement on leur donne le nom du dossier qui va y monter:

```shell
# lvs
  LV   VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root almalinux -wi-ao----  <6,20g
  swap almalinux -wi-ao---- 820,00m

# lvdisplay /dev/almalinux/root
  --- Logical volume ---
  LV Path                /dev/almalinux/root
  LV Name                root
  VG Name                almalinux
  LV UUID                SlMZf8-bAKE-sOWp-QkVJ-XSxd-Lm73-ZHkYIm
  LV Write Access        read/write
  LV Creation host, time localhost.localdomain, 2023-01-11 14:41:39 -0500
  LV Status              available
  # open                 1
  LV Size                <6,20 GiB
  Current LE             1586
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:0
```

Ici, notre LV "root" est monté sur /

```shell
# mount | grep root
/dev/mapper/almalinux-root on / type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
```

## Pare-feu

Sous Linux (en tout cas Debian et RHEL), le parefeu est géré par Netfilter.

A l'instar de init.d et des network-scripts, sa gestion/configuration est en train d'évoluer.

Anciennement on utilise iptables. Soit en modifiant directement le fichier `/etc/sysconfig/iptables` soit a l'aide de la commande du même nom `iptables`

De plus en plus, on utilise *firewalld* sous RHEL, *ufw* sous Debian.

### Avec Iptables

Exemple en créant une règle pour autoriser le ssh : 

```shell
# iptables -A INPUT -p tcp --dport ssh -j ACCEPT

# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:ssh

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

Pour changer la règle par défaut (attention à ne pas se couper la branche):

```shell
# iptables -P INPUT DROP
Chain INPUT (policy DROP)
target     prot opt source               destination
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:ssh

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

### Avec firewalld

(source: [Comment configurer un pare-feu en utilisant firewalld sur CentOS 8 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-8-fr) )

Firewalld fonctionne avec un système de zone.

```shell
# firewall-cmd --get-zones
block dmz drop external home internal nm-shared public trusted work
```

Ces zones sont préconfigurés suivant le niveau de confiance octroyé: 

- **drop** : le niveau de confiance le plus bas. Toutes les connexions entrantes sont interrompues sans réponse et seules les connexions sortantes sont possibles.
- **block** : similaire à ce qui précède, mais au lieu de simplement interrompre les connexions, les demandes entrantes sont rejetées avec un message `icmp-host-prohibited` ou `icmp6-adm-prohibited`.
- **public** : représente les réseaux publics, non fiables. Vous ne faites pas confiance aux autres ordinateurs, mais vous pouvez autoriser certaines connexions entrantes au cas par cas.
- **external** : les réseaux externes dans l’éventualité où vous utilisez le pare-feu comme passerelle. Il est configuré pour le masquage NAT de sorte que votre réseau interne reste privé mais accessible.
- **interne** : l’autre côté de la zone externe, utilisé pour la partie interne d’une passerelle. Les ordinateurs sont assez fiables et certains services supplémentaires sont disponibles.
- **dmz** : utilisé pour les ordinateurs situés dans un DMZ (ordinateurs isolés qui n’auront pas accès au reste de votre réseau). Seules certaines connexions entrantes sont autorisées.
- **work** : utilisé pour les machines de travail. Fait confiance à la plupart des ordinateurs du réseau. Quelques services supplémentaires pourraient être autorisés.
- **home** : un environnement domestique. Cela implique généralement que vous faites confiance à la plupart des autres ordinateurs et que quelques services supplémentaires seront acceptés.
- **trusted** : fais confiance à toutes les machines du réseau. La plus ouverte des options disponibles et doit être utilisée avec parcimonie.

Ensuite, on a les services, qui correspondent aux protocol et port qu'on veut ouvrir

Par défaut, il en existe pas mal qui sont déjà "nommé"

```shell
# firewall-cmd --get-services
RH-Satellite-6 RH-Satellite-6-capsule amanda-client amanda-k5-client amqp amqps apcupsd audit bacula bacula-client bb bgp bitcoin bitcoin-rpc bitcoin-testnet bitcoin-testnet-rpc bittorrent-lsd ceph ceph-mon cfengine cockpit collectd condor-collector ctdb dhcp dhcpv6 dhcpv6-client distcc dns dns-over-tls docker-registry docker-swarm dropbox-lansync elasticsearch etcd-client etcd-server finger foreman foreman-proxy freeipa-4 freeipa-ldap freeipa-ldaps freeipa-replication freeipa-trust ftp galera ganglia-client ganglia-master git grafana gre high-availability http https imap imaps ipp ipp-client ipsec irc ircs iscsi-target isns jenkins kadmin kdeconnect kerberos kibana klogin kpasswd kprop kshell kube-apiserver ldap ldaps libvirt libvirt-tls lightning-network llmnr managesieve matrix mdns memcache minidlna mongodb mosh mountd mqtt mqtt-tls ms-wbt mssql murmur mysql nbd nfs nfs3 nmea-0183 nrpe ntp nut openvpn ovirt-imageio ovirt-storageconsole ovirt-vmconsole plex pmcd pmproxy pmwebapi pmwebapis pop3 pop3s postgresql privoxy prometheus proxy-dhcp ptp pulseaudio puppetmaster quassel radius rdp redis redis-sentinel rpc-bind rquotad rsh rsyncd rtsp salt-master samba samba-client samba-dc sane sip sips slp smtp smtp-submission smtps snmp snmptrap spideroak-lansync spotify-sync squid ssdp ssh steam-streaming svdrp svn syncthing syncthing-gui synergy syslog syslog-tls telnet tentacle tftp tftp-client tile38 tinc tor-socks transmission-client upnp-client vdsm vnc-server wbem-http wbem-https wsman wsmans xdmcp xmpp-bosh xmpp-client xmpp-local xmpp-server zabbix-agent zabbix-server
```

On retrouve http (80) et https (443) par exemple.

Le principe de fonctionnement, de base, simplifié est le suivant : 

1) On choisis une zone pour notre interface

```shell
# firewall-cmd --zone=work --change-interface=enp0s8
```

2. On ouvre les ports/services qu'on veut

```shell
# firewall-cmd --zone=work --add-service=http --permanent
```

## Les fichiers !

### Les logs

- `/var/log/messages`

- `/var/log/secure`

En gros, si il y a 2 fichiers à retenir, c'est ceux là. Ils contiennent 90% des logs système.

Les appli iront loguer soit dans messages, soit dans leurs fichiers à elles (ie `/var/log/httpd/access.log`)

###  Compte, groupe et mdp

* passwd, shadow et groups 

Les 3 fichiers permettant de stocker les informations concernant les utilisateurs, groupes et mdp.

### Et du coup, les permissions ? 777 ?

`-rw-r--r--` : 644. on compte en binaire

Premier octet:

```-
- : fichier classique
d : répertoire
l : lien symbolique
c : périphérique de type caractère
b : périphérique de type bloc
p : pipe (FIFO) "tube" ou "tuyau" en anglais ou pipeline aussi en français
s : socket
```

Pour les 9 autres octets, ils se prennent par bloc de 3 et correspond au "Propriétaire, Groupe, Other"

R = Read (Lecture)

W = Write (Ecriture)

X = eXecute (Exécuter ...)

<u>Exemple</u>: 

`-rw-r--r--. 1 root root 0 25 janv. 12:55 /home/toto`

Le fichier appartient à root, groupe root.

C'est un fichier classique (-)

Le propriétaire à les droit de lecture (r) et d'écriture (w). Le groupe "root" peut lire, et other peut lire.

Les commandes `chmod`et `chown`permettent de modifier les droits.

### La FSTAB

Le fichier `/etc/fstab`est celui qui permet de connaitre au système comment sont monter les différents filesystem.

# Pré-requis aux TP
## Environnement Client - Serveurs

Pour les quelques TP qui seront présentés ci dessous, on partira sur une infrastructure relativement simple basée sur Virtual Box.
2 VMs seront principalement utilisées. Une VM serveur et une VM linux. Les 2 seront basées sur la distribution AlmaLinux.

L'iso de déploiement utilisée dans les 2 cas est la version minimaliste disponible ici :  [Alma - x86](http://mirror.crexio.com/almalinux/8.7/isos/x86_64/)

### VM Serveurs
#### Premier Déploiement
Sous Virtual Box:

* Nouvelle VM
  * Nouvelle VM
  * Nom: Alma-Serveur
  * Dossier local
  * Type: RHEL8
  * Stockage : 20Go
  * 2 cartes réseaux : 1) NAT 2) Host-Only Network
* Configuration
  * RAM : 2048
  * Activer l'EFI
* Configuration Réseau Virtual Box
  * Gestionnaire de réseau -> Host-Only Networks -> Désactiver DHCP

* Premier Boot / Installation
  * Réseau : Activer les 2 cartes Réseau --> Définir l'ip 192.168
  * Installation Destination : Configurer son partionnement. (On peut se faire aider par l'installeur).
```
Personnalisé (On attends ... trop longtps !)
> LVM : Oui
> / : 5 Gio
> /home : 5 Gio
> /boot/efi : 600 Mio
> /boot : 1024 Mio
> swap : 2 Gio
```
  * Mirroir et sources : Installation Minimal / Serveur

#### Post Configuration
Se connecter en ssh depuis "l'hyperviseur" : `ssh root@192.168.56.10`
```shell
# useradd admin
# passwd admin
Changement de mot de passe pour l'utilisateur admin.
Nouveau mot de passe :
Retapez le nouveau mot de passe :
passwd : mise à jour réussie de tous les jetons d'authentification.
```
Pour être propre et efficace, on va maintenant générer une clef privé/publique pour se connecter à notre serveur

Depuis l'hôte hyperviseur, avec votre compte
```shell
# ssh-keygen # On répond aux questions
# cat ~.ssh/id_rsa.pub | ssh admin@192.168.56.10 "cat >> .ssh/authorized_keys"
# ssh admin@192.168.56.10
```

Normalement, la dernière connexion ssh ne doit pas demander de mot de pass.
On peut vérifier l'échange de clef en augmentant la verbosité de ssh : `ssh -vvv admin@192.168.56.10`

Et enfin, on va modifier la conf ssh pour ne plus autoriser root à se connecter par ce biais:
`# vim /etc/sshd_config`. 
On modifie la ligne "PermitRootLogin"
```shell
#LoginGraceTime 2m
#PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
```
```shell
# systemctl restart sshd
# systemctl status sshd
```

On peut maintenant se connecter au serveur depuis notre hôte en utilisant le compte admin.
Pour récupérer les droit root, on "Switch User" :
```shell
$ su - 
```

# Installation DHCPD
## Prérequis

En prérequis on part du principe qu'on à déjà a disposition:
* Une VM "Serveur" sous Almalinux avec 2 cartes réseaux. Une "NATée", l'autre sur un sous réseau hôte, privé.
* Cette VM serveur aura l'ip 192.168.56.10/24 sur le réseau privé.
* Elle fera office de serveur DHCP + DNS
* On se connecte à cette VM depuis l'hyperviseur en tant qu'utilisateur et on y fait une élévation de droit avec un `su -` (Pas de connexion root@ mais pas de sudo non plus ...)

Le sous réseau hôte sera une simulation de réseau d'entreprise avec les différentes services de bases.

## Côté Serveur

```shell
# dnf install dhcpd-server
# vim /etc/dhcpd/dhcpd.conf
```
```shell
default-lease-time 86400; #24h bail
authoritative;

# On déclare le réseau

subnet 192.168.50.0 netmask 255.255.255.0 {
        range 192.168.50.100 192.168.50.150; # de 100 a 150
        option domain-name-servers 192.168.50.10; # Sera diffusé aux client
        option routers 192.168.50.1; # A voir si on garde.
}
```
On a plus qu'à activer et lancer le service.
On peut lancer la commande `dhcpd -t` pour vérifier que notre configuration est OK. Très pratique pour éviter de casser la prod.

```shell
# systemctl enable dhcpd && systemctl start dhcpd
```

## Côté Client

```shell
# nmcli con show
NAME    UUID                                  TYPE      DEVICE
enp0s3  2b1cbf16-82b7-4cb4-a326-bf9680fb256a  ethernet  enp0s3
virbr0  aa91c9db-037f-4c4a-97c7-53ecf7d9237d  bridge    virbr0

# nmcli con mod enp0s3 ipv4.method auto
# systemctl restart NetworkManager
```
Ici on à 1) Forcer le mode dhcp sur la carte réseau. 2) Relancer les services réseaux pour prendre en compte la conf.

## Vérifications
### Côté Serveur

On peut vérifier le bon fonctionnement du DHCP en regardant plusieurs fichiers:
```shell
# cat /var/log/messages | grep DHCP
Jan 28 03:20:04 localhost dhcpd[1220]: DHCPREQUEST for 192.168.56.101 from 08:00:27:52:b9:c1 via enp0s8: wrong network.
Jan 28 03:20:04 localhost dhcpd[1220]: DHCPNAK on 192.168.56.101 to 08:00:27:52:b9:c1 via enp0s8
Jan 28 03:20:04 localhost dhcpd[1220]: DHCPDISCOVER from 08:00:27:52:b9:c1 via enp0s8
Jan 28 03:20:04 localhost dhcpd[1220]: DHCPOFFER on 192.168.50.100 to 08:00:27:52:b9:c1 via enp0s8
Jan 28 03:20:04 localhost dhcpd[1220]: DHCPREQUEST for 192.168.50.100 (192.168.50.1) from 08:00:27:52:b9:c1 via enp0s8
Jan 28 03:20:04 localhost dhcpd[1220]: DHCPACK on 192.168.50.100 to 08:00:27:52:b9:c1 via enp0s8
```
Ici on peut voir l'échange entre le client et le serveur (on peut voir d'ailleur que le client a requété une mauvaise adresse IP)
Les commandes `systemctl status dhcpd` et `journalctl -u dhcpd` renverrons grosso-modo les mêmes informations.

On peut également voir le bail lui même : 
```shell
# cat /var/lib/dhcpd/dhcpd.leases
# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.3.6

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

lease 192.168.50.100 {
  starts 6 2023/01/28 08:20:04;
  ends 0 2023/01/29 08:20:04;
  tstp 0 2023/01/29 08:20:04;
  cltt 6 2023/01/28 08:20:04;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:52:b9:c1;
  uid "\001\010\000'R\271\301";
}
server-duid "\000\001\000\001+Q\344T\010\000'1\001\240";
```






# Installation DNS

