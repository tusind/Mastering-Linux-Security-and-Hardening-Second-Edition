# [sudo](https://www.sudo.ws/)

edit sudo file with visudo

sudoers example:

``` bash
##FName: sudoers
## Read drop-in files from /etc/sudoers.d (the # here does not mean a comment)
#includedir /etc/sudoers.d

## EDITOR
Defaults editor=/usr/bin/vim, !env_editor

## HOST ALIAS
# Host_Alias centos = centos8, centos7

## USER ALIAS
# User_Alias ADMINS = jsmith, mikem
## OR USE %groupname

## CMND ALIAS
## Networking
Cmnd_Alias NETWORK = /sbin/route, /sbin/ifconfig, /bin/ping, /sbin/dhclient, \
				/usr/bin/net, /sbin/iptables, /usr/bin/rfcomm, /usr/bin/wvdial, \
				/sbin/iwconfig, /sbin/mii-too, /usr/bin/netctl \

Cmnd_Alias  SSHD = /usr/bin/systemctl status sshd.service, /usr/bin/systemctl start sshd.service, \
		   /usr/bin/systemctl stop sshd.service, /usr/bin/systemctl restart sshd.service, \
		   sudoedit /etc/ssh/sshd_config

## PACKAGE MANAGERS
Cmnd_Alias RHEL_SOFTWARE = /bin/rpm, /usr/bin/up2date, /usr/bin/yum, /usr/bin/dnf
Cmnd_Alias ARCH_SOFTWARE = /usr/bin/pacman, sudoedit /etc/pacman.d/mirrorlist

Cmnd_Alias MNT =/usr/sbin/cryptsetup, /usr/bin/umount, /usr/bin/mount
Cmnd_Alias OVPN =/usr/sbin/openvpn
Cmnd_Alias POWER = /usr/bin/shutdown -h now, /usr/bin/halt, /usr/bin/poweroff, /usr/bin/reboot. \
				   /usr/sbin/poweroff

## CREATE GROUPS
## # for i in  power network pkg ; do groupadd -r $i ; done
## ADD USER TO GROUPS
## # for i in power network pkg ; do gpasswd -a userName $i ; done

%power   ALL = (root)  NOPASSWD: POWER
%network ALL = (root)  NETWORK, SSHD, OVPN, MNT
%pkg     ALL = (root)  RHEL_SOFTWARE, ARCH_SOFTWARE

# Refuse to run if unable to disable echo on the tty.
Defaults   !visiblepw

Defaults    env_reset
Defaults    env_keep =  "COLORS DISPLAY HOSTNAME HISTSIZE KDEDIR LS_COLORS"
Defaults    env_keep += "MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE"
Defaults    env_keep += "LC_COLLATE LC_IDENTIFICATION LC_MEASUREMENT LC_MESSAGES"
Defaults    env_keep += "LC_MONETARY LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE"
Defaults    env_keep += "LC_TIME LC_ALL LANGUAGE LINGUAS _XKB_CHARSET XAUTHORITY"

Defaults    secure_path = /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

## Allow root to run any commands anywhere
root ALL=(ALL)  ALL
```
