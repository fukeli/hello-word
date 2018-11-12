Centos7 安装 MySql8 二进制安装包
===

1、自行下载二进制安装包 
---
>我下载的是 mysql-8.0.13-linux-glibc2.12-x86_64.tar.xz  地址:[https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)
![image](https://github.com/fukeli/hello-word/blob/master/images/mysql%E4%B8%8B%E8%BD%BD1.png)
![image](https://github.com/fukeli/hello-word/blob/master/images/mysql%E4%B8%8B%E8%BD%BD2.png)
>自己挑选下载的版本即可

2、先卸载当前系统中已安装的mariadb
---
>列出当前系统中已安装的mariadb: rpm -qa | grep mariadb 和已安装的数据库 ： rpm -qa | grep mysql
```
[root@localhost mysql8]# rpm -qa | grep mariadb
mariadb-5.5.52-1.el7.x86_64
mariadb-server-5.5.52-1.el7.x86_64
mariadb-devel-5.5.52-1.el7.x86_64
mariadb-libs-5.5.52-1.el7.x86_64
......
```
>删除
```
[root@localhost local]# rpm -e mysql* 和  mariadb*   
如果遇到问题  用  rpm -e --nodeps mysql*  和  mariadb*
```

3、MySql安装
----
>将 mysql-8.0.13-linux-glibc2.12-x86_64.tar.xz 上传到服务器 /usr/local/ 目录下 ，然后：
```
#进入 /usr/local 目录
cd /usr/local/ 
#解压文件
tar -xvf mysql-8.0.13-linux-glibc2.12-x86_64.tar.xz     
#创建mysql文件目录
mkdir mysql8
#将解压后的文件挪动到指定目录
cp -r mysql-8.0.13-linux-glibc2.12-x86_64/* mysql8/
#进入mysql8 目录
cd mysql8/
#创建数据库文件目录 和 日志目录
mkdir data 
mkdir log
#创建mysql组和用户
groupadd mysql8
useradd -r -g mysql8 -s /bin/false mysql8
chown  -R  mysql8:mysql8 /usr/local/mysql8
```
>#在 /etc 下，创建 my.cnf文件 , 文件内容如下：
```
[mysqld]
port=3306
datadir=/usr/local/mysql8/data
log-error=/usr/local/mysql8/log/mysql-err.log
user=mysql8
#default_authentication_plugin=mysql_native_password   #此项是为了兼容当前的远程连接工具可以连接
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
#default-storage-engine=INNODB
# 默认使用“mysql_native_password”插件认证
default_authentication_plugin=mysql_native_password
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8

[client]
socket=/tmp/mysql.sock
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8
```
>配置环境变量
```
echo "export PATH=$PATH:/usr/local/mysql8/bin"  >>  /etc/profile
source /etc/profile
```
>制作启动文件
```
cp  /usr/local/mysql8/support-files/mysql.server  /etc/init.d/mysqld
vi /etc/init.d/mysqld     #将basedir =  改为 basedir = /usr/local/mysql8 ,将datadir = 改为 datadir = /usr/local/mysql8/data

#给予/etc/init.d/mysqld运行权限
chmod  755 /etc/init.d/mysqld
```
>初始化和启动 ： 这里需要特别注意，mysql初始化后，默认密码会在日志里记录，查看 more log/mysql-err.log ,其中有一行
```
A temporary password is generated for root@localhost: aQujM!tBb2Re . 结尾的 aQujM!tBb2Re ，即为密码，记住后面用。
```
```
#初始化mysql 
/etc/init.d/mysqld --initialize --user=mysql8  --basedir=/usr/local/mysql8  --datadir=/usr/local/mysql8/data
#启动和关闭
/etc/init.d/mysqld start
/etc/init.d/mysqld stop
```
4、用户配置
----
>启动mysql服务，查看库
```
#进入mysql  ， 密码是初始化数据库时，随机生成的密码，在日志里，我的是 aQujM!tBb2Re
mysql -uroot -p 
#查看库
 show databases; 
 +--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+

#创建自己库  -- 将下面 'dataset' 替换成自己的库名
CREATE DATABASE IF NOT EXISTS dataset default charset utf8 COLLATE utf8_general_ci;   

#创建用户名
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
   --> 说明：
          username：你将创建的用户名
          host：指定该用户在哪个主机上可以登陆，如果是本地用户可用localhost，如果想让该用户可以从任意远程主机登陆，可以使用通配符%
          password：该用户的登陆密码，密码可以为空，如果为空则该用户可以不需要密码登陆服务器
          如: CREATE USER 'dataset'@'%' IDENTIFIED BY '1233456';
  
#给用户授权
GRANT privileges ON databasename.tablename TO 'username'@'host'
   -->说明：
        privileges：用户的操作权限，如SELECT，INSERT，UPDATE等，如果要授予所的权限则使用ALL
        databasename：数据库名
        tablename：表名，如果要授予该用户对所有数据库和表的相应操作权限则可用*表示，如*.*
        如：GRANT ALL ON dataset.* TO 'dataset'@'%';
        
```
参考网址：<br>
[https://www.cnblogs.com/sos-blue/p/6852945.html](https://www.cnblogs.com/sos-blue/p/6852945.html)

欢迎进入我的github，[提出建议](https://github.com/fukeli)<br>
---
