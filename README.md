# b2rMonitoring

#!/bin/bash

echo -n "#Architecture: "; uname -a

echo -n "#CPU physical : "; grep -c processor /proc/cpuinfo

echo -n "#vCPU : "; cat /proc/cpuinfo | grep processor | wc -l

echo -n "#Memory Usage: "; free -m | awk 'NR == 2{printf "%s/%sMB (%.2f%%)\n", $3, $2, ($3 / $2) * 100}'

echo -n "#Disk Usage: "; df -h | awk '$NF=="/"{printf "%d/%.1fGB (%s)\n", $3, $4, $5}'

echo -n "#CPU load: "; top -bn1 | grep 'load' | awk '{printf "%.2f%%\n", $(NF - 2)}'

echo -n "#Last boot: "; who | grep 'pts/0' | awk '{printf "%s %s\n", $3, $4}'

echo -n "#LVM use: "; if cat /etc/fstab | grep -q "/dev/mapper/"; then echo "yes"; else echo "no"; fi

echo -n "#Connexions TCP : "; cat /proc/net/tcp | wc -l | awk '{printf "%d", $1-1}'; echo " ESTABLISHED"

echo -n "#User log: "; w | wc -l | awk '{printf "%d\n", $1-2}'

echo -n "#Network: "; echo -n "IP "; ip route list | grep 'link' | awk '{printf "%s", $9}'
ip link show | grep 'link/ether' | awk '{printf " (%s)", $2}'; echo ""

echo -n "#Sudo : "; cat /var/log/sudo.log | grep 'COMMAND' | wc -l | tr '\n' ' '; echo "cmd"


__________________________________


Show Partitions:
lsblk

Go to root:
su -

edit hostname:
sudo hostnamectl set-hostname NAME

Add user to group:
usermod -aG GROUP USER_NAME
Check users in group:
getent group GROUP

Add group:
sudo addgroup GROUP_NAME

Create user:
sudo adduser USER_NAME

Remove user:
sudo userdel USER_NAME

sudo config:
sudo vi /etc/sudoers.d/config

sudo logs:
/var/log/sudo.log

is service installed:
dpkg -l | grep SERVICE

check ssh status:
sudo service ssh status

ssh config:
sudo vi /etc/ssh/sshd_config

UFW add port
sudo ufw allow PORT

check UFW status:
sudo ufw status

passwords age settings:
sudo vi /etc/login.defs (160)
password strength settings:
sudo vi /etc/pam.d/common-password

Setup Cron job:
sudo vi /etc/crontab

MariaDB:
mariadb -u dhubleur -p
SHOW DATABSES;

Config Wordpress:
sudo vi /var/www/html/wp-config.php

Config FTP:
sudo vi /etc/vsftpd.conf
sudo vi /etc/vsftpd.userlist 

