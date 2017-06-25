# MySQL 技巧

```
MySQL
http://dev.mysql.com/downloads/mysql/

Windows
http://cdn.mysql.com//Downloads/MySQLInstaller/mysql-installer-community-5.7.16.0.msi
http://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.16-win32.zip
http://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.16-winx64.zip


排除EF错误：IsPrimaryKey...
use YOURDATABASE;
set global optimizer_switch='derived_merge=off';
或者
set @@optimizer_switch='derived_merge=OFF';
select @@optimizer_switch;


C:\> mysql -h localhost -uroot -p

查看数据库
show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| GAN                |
| gogs               |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
6 rows in set (0.00 sec)

查看设置
\s
--------------
mysql.exe  Ver 14.14 Distrib 5.7.12, for Win64 (x86_64)

Connection id:          63
Current database:
Current user:           root@172.17.0.1
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.7.16 MySQL Community Server (GPL)
Protocol version:       10
Connection:             127.0.0.1 via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 1 day 7 hours 3 sec

Threads: 13  Questions: 2934  Slow queries: 0  Opens: 418  Flush tables: 1  Open tables: 329  Queries per second avg: 0.026
--------------

更改字符集
mysql> show variables like 'character%';
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | latin1                     |
| character_set_connection | latin1                     |
| character_set_database   | utf8mb4                    |
| character_set_filesystem | binary                     |
| character_set_results    | latin1                     |
| character_set_server     | latin1                     |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set

更改系统变量
set character_set_client=utf8;
set character_set_connection=utf8;
set character_set_database=utf8;
set character_set_results=utf8;
set character_set_server=utf8;
set character_set_system=utf8;
set collation_connection=utf8;
set collation_database=utf8;
set collation_server=utf8;

更改数据库
alter database mydb character set utf8;
create database mydb character set utf8;

修改opt文件
default-character-set=utf8
default-collation=utf8_general_ci


连接字符串
server=172.24.10.155;user id=root; password=3k5wAq91fbd3WT2AY8kS; database=dpps; pooling=false; charset=utf8

更改密码：
# mysql -u root -p
set password for root@localhost=password('123456');
flush privileges;
或者
use mysql;
select Host,User from user;
update user set password=password('123456') where user='root';
flush privileges;

```