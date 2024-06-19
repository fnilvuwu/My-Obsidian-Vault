# Node 1

1. Configure the network

`sudo hostnamectl set-hostname node1.network9.example.com`

`sudo nmcli connection add con-name node1 ifname enp1s0 type ethernet ipv4.method manual ipv4.address 172.24.9.10/24 ipv4.gateway 172.24.9.254 ipv4.dns 172.24.9.254 connection.autoconnect yes`

disoal diminta netmask 255.255.255.0 maka prefixnya adalah /24
![[Pasted image 20240602152741.png]]

`nmcli connection up node1`

`nano /etc/ssh/sshd_config`
PermitRootLogin yes
PasswordAuthentication yes

`systemctl restart sshd`

NOTES :
to delete use
`nmcli connection delete {con-name}`
to check all connection
`nmcli con show`

SUGGESTED:
reboot to check if profile is still correct

![[Screenshot_20240529_155235.png]]

2. Create a repository

`sudo dnf config-manager --add-repo=https://mirror.stream.centos.org/9-stream/AppStream/x86_64/os/`
`sudo dnf config-manager --add-repo=https://mirror.stream.centos.org/9-stream/BaseOS/x86_64/os/`

`vim /etc/yum.repos.d/<repo-name>.repo`


[AppStream]
name=AppStream Repository
baseurl=https://mirror.stream.centos.org/9-stream/AppStream/x86_64/os/
enabled=1
gpgcheck=0

[BaseOS]
name=BaseOS Repository
baseurl=https://mirror.stream.centos.org/9-stream/BaseOS/x86_64/os/
enabled=1
gpgcheck=0

NOTE:
to check if it's correct there should be AppStream and BaseOS in :
`sudo dnf update`

3.SElinux
`systemctl status httpd`
`vim /etc/httpd/conf/httpd.conf`
`semanage port -l | grep http`
http_cache_port_t              tcp      8080, 8118, 8123, 10001-10010
http_cache_port_t              udp      3130
http_port_t                    tcp      80, 81, 443, 488, 8008, 8009, 8443, 9000
pegasus_http_port_t            tcp      5988
pegasus_https_port_t           tcp      5989
`semanage port -a -t http_port_t -p tcp 82`
`systemctl enable --now httpd`
`firewall-cmd --add-port=82/tcp --permanent`
`firewall-cmd --reload`

NOTES :
to check
`curl localhost:82`

4. Create the following users, groups and group memberships

`sudo groupadd sysadmin`
`sudo useradd -m -G sysadmin harry`
`sudo useradd -m -G sysadmin natasha`
`sudo useradd -m -s /sbin/nologin sarah`

this is dangerous way, since it might get into the log also other can see it IRL but it works just fine!
`echo 'redhat' | sudo passwd --stdin harry`
`echo 'redhat' | sudo passwd --stdin natasha`
`echo 'redhat' | sudo passwd --stdin sarah`

![[Screenshot_20240530_103358 3.png]]

![[Screenshot_20240530_103824.png]]



5. Create a collaborative directory

Create the directory with group ownership set to sysadmin:
`sudo mkdir -p /common/sysadmin`
`sudo chown -R :sysadmin /common/sysadmin/`
`sudo chown -R {user}:{group} {file_location}`
alternative way :
`chgrp sysadmin /common/sysadmin/`
`chgrp {group} {file_location}`

Set the appropriate permissions to make the directory readable, writable, and accessible only to members of the sysadmin group:
`sudo chmod -R 770 /common/sysadmin/`

Set the setgid bit on the directory so that files created within it inherit the group ownership of the parent directory (sysadmin):
`sudo chmod g+s /common/sysadmin/`
parameter g for group, s for special

NOTE:
kalo mau execute wajib ada read jadi permssionnya 5 begitupun dgn write wajib ada read

![[Screenshot_20240530_105958.png]]

![[Screenshot_20240530_110508.png]]

![[Screenshot_20240530_110836.png]]

![[Screenshot_20240530_111717.png]]

![[Screenshot_20240530_112950.png]]

![[Screenshot_20240530_113036.png]]

6. Automount the remote user home directory

Install autofs (use appropriate package manager)
sometimes lab is not started correctly so check it first :
`ping utility.network9.example.com`

`sudo dnf install autofs`    # For CentOS/RHEL

check if mounting point is available 
`mount -t nfs utility.network9.example.com:/netdir/remoteuser9 /mnt`

verify if mounting point is mounted
[root@node1 ~]# `df -h`
Filesystem                                        Size  Used Avail Use% Mounted on
devtmpfs                                          4.0M     0  4.0M   0% /dev
tmpfs                                             227M     0  227M   0% /dev/shm
tmpfs                                              91M  4.0M   87M   5% /run
/dev/mapper/rhel-root                              17G  1.8G   16G  11% /
/dev/vda1                                        1014M  244M  771M  24% /boot
tmpfs                                              46M     0   46M   0% /run/user/0
utility.network9.example.com:/netdir/remoteuser9   17G  1.8G   16G  11% /mnt

to unmount use
`umount /mnt`

Configure autofs master file
`sudo nano /etc/auto.master.d/remoteuser9.autofs`
/- /etc/auto.remoteuser9

Configure auto.netdir file
`sudo nano /etc/auto.remoteuser9`

Add the following line:
/netdir/remoteuser9 -rw,sync,fstype=nfs4 utility.network9.example.com:/netdir/remoteuser9

`systemctl restart autofs`

`su - remoteuser9`
[remoteuser9@node1 ~]$ `df -h`
Filesystem                                        Size  Used Avail Use% Mounted on
devtmpfs                                          4.0M     0  4.0M   0% /dev
tmpfs                                             227M     0  227M   0% /dev/shm
tmpfs                                              91M  4.0M   87M   5% /run
/dev/mapper/rhel-root                              17G  1.8G   16G  11% /
/dev/vda1                                        1014M  244M  771M  24% /boot
tmpfs                                              46M     0   46M   0% /run/user/0
utility.network9.example.com:/netdir/remoteuser9   17G  1.8G   16G  11% /netdir/remoteuser9

7. Configure Crontab
`crontab -e -u natasha`

30 12 * * * /bin/echo "hello"

8. Configure your system as NTP client
`dnf install chrony`
`sudo nano /etc/chrony.conf`
server time.cloudflare.com iburst
`systemctl restart chronyd`
`chronyc sources -v`

9. Locate all the files owned by sarah and make a copy of them in the given path
/root/find.user
make the directory first
`mkdir /root/find.user`
`find / -type f -user`
`find / -type f -user sarah -exec cp -a {} /root/find.user \;`

10. Find the string
`grep "home" /etc/passwd > /root/search.txt`
`grep home /etc/passwd`
![[Pasted image 20240530153252.png]]
`grep home /etc/passwd > /root/search.txt`

so basically the task had to be done in order
![[Pasted image 20240530153521.png]]

11. Create a user account
`sudo useradd -u 1326 alies`
`echo 'redhat' | sudo passwd --stdin alies`

12. Create a archive files
`sudo tar -zcvf /root/archive.tgz /var/tmp`
`sudo tar -czf /root/archive.tgz /var/tmp`

confirm using
`file /root/archive.tgz`

13. Build a container image as user neith

using root to install the package
[root@node1 ~]# `dnf install container-tools`

`ssh neith@node1`
pass = redhat
`wget https://raw.githubusercontent.com/omidiyanto/RHCSA9/main/Containerfile`

`podman build -t monitor .`

verify with
`podman images`

![[Pasted image 20240530160712.png]]

14. Configure the container as a system start-up service and mount volumes
persistently.

`ssh root@node1`
`loginctl enable-linger neith`
`loginctl show-user neith`
![[Pasted image 20240530162104.png]]
`mkdir /opt/files
`mkdir /opt/processed`
`chmod 777 /opt/files/`
`chmod 777 /opt/processed/`
`chown neith: /opt/files/`
`chown neith: /opt/processed/`
![[Pasted image 20240530162359.png]]

exit from root and ssh from workstation
`ssh neith@node1`

`podman images`

`podman run -d --name ascii2pdf -v /opt/files:/opt/incoming:Z -v /opt/processed:/opt/outgoing:Z localhost/monitor:latest`

`podman ps -a`

![[Pasted image 20240530163303.png]]

Turning it into service
`mkdir -p /home/neith/.config/systemd/user`
`cd /home/neith/.config/systemd/user`
`podman generate systemd --name ascii2pdf --files --new `

`systemctl --user daemon-reload`

`systemctl --user enable --now container-ascii2pdf.service`
![[Pasted image 20240530163944.png]]

confirm if service running
`systemctl --user status container-ascii2pdf.service`

and confirm if service working

`touch /opt/files/coba
`file /opt/processed/coba
![[Pasted image 20240530164233.png]]
NOTE
to remove if build failed
`podman rm ascii2pdf`
to stop if it's running
`podman stop ascii2pdf`

make sure to if container cant be removed 
`systemctl --user disable container-ascii2pdf`
`systemctl --user stop container-ascii2pdf`

in case crun error, run using root
`dnf update crun`

seems the filename also matter when testing, it only work for "coba"
![[Pasted image 20240530172118.png]]

![[Pasted image 20240530172159.png]]

15. Configure default permissions

`vim /home/natasha/.bashrc`
or
`vim /home/natasha/.bash_profile`

add to the very bottom :
umask 0277

![[Pasted image 20240530145512.png]]

![[Pasted image 20240530145410.png]]

![[Screenshot_20240530_111717.png]]

![[Screenshot_20240530_111717 1.png]]
disoal kita diminta mengatur izin direktori menjadi d r-x------ a karena direktori itu defaultnya 777 untuk mengubahnya menjadi read dan execute maka kita perlu permission 500 5 itu dari 4 + 1, r + x karena di soal diminta untuk user saja maka kita hanya mengubah digit pertama 500. Lalu cara kerja dari umask kita tidak perlu mempertimbangkan izin dari file, izin file akan mengikuti izin dari direktori
maka didapatlah nilai umask 
777-500=277
https://phoenixnap.com/kb/what-is-umask


16. Set the Password expire date
`sudo nano /etc/login.defs`
PASS_MAX_DAYS   60

17. Configure sudoers
`sudo visudo`
%sysadmin ALL=(ALL) NOPASSWD: ALL

18. Configure the application
`su - alies`
`nano ~/.bashrc`
export RHCSA="Welcome to RHCSA Timedrills"
echo $RHCSA

19. Create the shell script (IDK) (WRONG script stilll wrong)
`sudo nano /usr/local/bin/mysearch`

Find files in /usr directory with size between 30k and 50k and special user ID permissions
`find /usr -type f -size +30k -size -50k -perm -u=s > /root/myfiles`

#!/bin/bash
find /usr -type f -size +30k -size -50k -perm -u=s > /root/myfiles

`sudo chmod a+x /usr/local/bin/mysearch`

`mysearch`

`cat /root/myfiles`
# Node 2


20. Assign root user password as redhat
press on keyboard or via vm monitor `ctrl+alt+delete`
`rd.break`
![[Pasted image 20240531104345.png]]

sh-5.1# `mount -o remount,rw /sysroot`
sh-5.1# `chroot /sysroot`
sh-5.1# `passwd root`
enter `redhat`
sh-5.1# `touch /.autorelabel`

![[Pasted image 20240531105600.png]]

reboot first by `exit`

`nano /etc/ssh/sshd_config`
PermitRootLogin yes
PasswordAuthentication yes

`systemctl restart sshd`

how to reset password : https://www.geeksforgeeks.org/how-to-reset-the-root-password-of-redhat-centos-linux/

21. Configure repo

`sudo dnf config-manager --add-repo=https://mirror.stream.centos.org/9-stream/AppStream/x86_64/os/`
`sudo dnf config-manager --add-repo=https://mirror.stream.centos.org/9-stream/BaseOS/x86_64/os/`

`vim /etc/yum.repos.d/<repo-name>.repo`

[AppStream]
name=AppStream Repository
baseurl=https://mirror.stream.centos.org/9-stream/AppStream/x86_64/os/
enabled=1
gpgcheck=0

[BaseOS]
name=BaseOS Repository
baseurl=https://mirror.stream.centos.org/9-stream/BaseOS/x86_64/os/
enabled=1
gpgcheck=0

22. Create swap partitons with size of 512MiB

Create a new partition, type '82' for Linux swap size is +512M
`sudo fdisk /dev/vdb`
n
p
1
enter
+512M
w

![[Pasted image 20240531111412.png]]
`udevadm settle`
`partprobe`
confirm with
`lsblk`
![[Pasted image 20240530154118.png]]

Write changes and exit
`sudo mkswap /dev/vdb1`
![[Pasted image 20240531111702.png]]

copy UUID and add to /etc/fstab so it'll load on reboot
`nano /etc/fstab`
UUID={swap_uid} swap swap defaults 0 0
![[Pasted image 20240531111615.png]]

mount the partition set on /etc/fstab
`mount -a`

`sudo swapon /dev/vdb1`
confirm with
`lsblk`
![[Pasted image 20240530154448.png]]

NOTE :
to exit from fdisk use : 
wq

23. Create one logical volume named ‘database’ and it should be on ‘datastore’ volume (WRONG)
each extend is 8MiB so 50x8 = 400MiB
![[Pasted image 20240531112930.png]]

Logical Volume Manager (LVM) in Linux consist of : physical volume, volume group, logical volume

`sudo fdisk /dev/vdb`

Create a new partition, with size more than 408M since we need 8M volume group
![[Pasted image 20240531112455.png]]

Write changes and exit

![[Pasted image 20240531112523.png]]

`pvcreate /dev/vdb2`
`vgcreate -s 8M datastore /dev/vdb2`

to confirm `vgdisplay datastore`
![[Pasted image 20240531113022.png]]

`lvcreate -n database -l 50 datastore
![[Pasted image 20240531113141.png]]

![[Screenshot_20240531_113358.png]]

`mkfs.ext3 /dev/datastore/database`
![[Pasted image 20240531113504.png]]

`vim /etc/fstab`
UUID={id_lv} /mnt/infinite ext3 defaults 0 0
![[Pasted image 20240531113606.png]]

mount the partition set on /etc/fstab
`mount -a`

confirm with `lsblk`

![[Pasted image 20240531113651.png]]

NOTE :
to check uid use
`lsblk --output=UUID {path_to_partition}`
![[Pasted image 20240531114340.png]]

24. Resize the logical volume size of 800M on /mnt/infinite directory. (WRONG)
 
![[Pasted image 20240531114434.png]]
Create a new partition, with size 900M
`sudo fdisk /dev/vdb`
n
p
+1G
wq

`udevadm settle; partprobe`
![[Pasted image 20240531114715.png]]

![[Pasted image 20240531114742.png]]

`pvcreate /dev/vdb3`
`vgextend datastore /dev/vdb3`

`lvextend -r -L 800M /dev/datastore/database`
![[Pasted image 20240531115246.png]]

[root@node2 ~]# `lvs`
  LV       VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  database datastore -wi-a----- 800.00m
  root     rhel      -wi-ao---- <17.00g
  swap     rhel      -wi-ao----   2.00g

25. Set the recommend tuned profile for your system
find the recommended profile name
`tuned-adm recommend`
set it based on the output
`tuned-adm profile virtual-guest`
`tuned-adm profile {profile_name}

confirm if profile is active using
`tuned-adm active`
![[Pasted image 20240531115619.png]]

TIPS for future self :
always try to spam `tab` to check If you're correct or forgot something

pastikan reboot terlebih dahulu sebelum digrading, soal yang harus persistent saat reboot untuk soal :
- jaringan
- autofs
- docker dan container
- partition dan lvm
repo bisa jadi 

Saran untuk IL :
jika ingin clear terminal harap dikabari dlu menteenya agar mentee dapat mengambil screenshot terlebih dahulu, atau mentor melakukan ss sebelum melakukan clear terminal lalu dishare ke mentee