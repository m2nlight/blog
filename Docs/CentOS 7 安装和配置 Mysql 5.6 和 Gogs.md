# CentOS 7 安装和配置 Mysql 5.6 和 Gogs

```
sudo
$ su
# vim /etc/sudoers
在 root  ALL=(ALL) ALL后面添加相同一行，新行的root改成当前用户，然后w!写入，退出vim
# exit
$ 
就可以了。



mysql 5.6
$ su
# rpm -qa|grep -i mariadb
# rpm -e --nodeps mariadb-devel mariadb-libs
# groupadd -r mysql
# useradd -g mysql mysql -d /home/mysql -s /sbin/nologin
# rpm -ivh ./MySQL-client-5.6.34-1.el7.x86_64.rpm
# rpm -ivh ./MySQL-server-5.6.34-1.el7.x86_64.rpm
(如果安装失败，可能是需要rpm安装autoconf，看提示。)
# systemctl start mysql.service
# cat /root/.mysql_secret 
The random password set for the root user at Tue Feb 21 13:55:26 2017 (local time): vZQwDJLbxm_zHno_
# mysql_secure_installation
# mysql -u root -p
mysql> grant all privileges on *.* to 'root'@'%' identified by '123456';
mysql> flush privileges;
mysql> exit
# firewall-cmd --zone=public --add-port=3306/tcp --permanent
# firewall-cmd --reload
# exit
# vim /etc/my.cnf
[mysqld]
skin-name-resolve
max_connections=1000

# systemctl restart mysql.service



gogs
$ su
# groupadd -r git
# useradd -g git git -d /home/git
# mv gogs /home/git/
# chown git:git /home/git/gogs
# cp /home/git/gogs/scripts/gogs.service /etc/systemd/system
# cat /etc/systemd/system
(或者系统systemd路径：/lib/systemd/system/gogs.service)
[Unit]
Description=Gogs
After=syslog.target
After=network.target
After=mariadb.service mysqld.service postgresql.service memcached.service redis.service

[Service]
# Modify these two values and uncomment them if you have
# repos with lots of files and get an HTTP error 500 because
# of that
###
#LimitMEMLOCK=infinity
#LimitNOFILE=65535
Type=simple
User=git
Group=git
WorkingDirectory=/home/git/gogs
ExecStart=/home/git/gogs/gogs web
Restart=always
Environment=USER=git HOME=/home/git

[Install]
WantedBy=multi-user.target

# systemctl enable gogs.service
# systemctl start gogs.service

# vim /etc/sysconfig/selinux
将SELINUX=enforce改为disabled

# firewall-cmd --zone=public --add-port=3000/tcp --permanent
# firewall-cmd --reload

# mysql -uroot -p123456 < /home/git/gogs/scripts/mysql.sql
或者
# mysql -uroot -p123456 -e "source /home/git/gogs/scripts/mysql.sql"
或者
# mysql -u root -p
mysql> source /home/git/gogs/scripts/mysql.sql
mysql> exit
# exit
$
然后在浏览器打开
http://localhost:3000

升级gogs
$ sudo systemctl stop gogs.service
$ sudo su - git
$ cd ~
$ pwd
/home/git
$ ls
gogs gogs-repositories
$ mv gogs gogs_old

$ wget https://dl.gogs.io/gogs_v$VERSION_$OS_$ARCH.tar.gz
$ tar -zxvf gogs_v$VERSION_$OS_$ARCH.tar.gz
$ ls
gogs gogs_old gogs-repositories gogs_v$VERSION_$OS_$ARCH.tar.gz

$ cp -R gogs_old/custom gogs
$ cp -R gogs_old/data gogs
$ cp -R gogs_old/log gogs

$ sudo systemctl start gogs.service

```