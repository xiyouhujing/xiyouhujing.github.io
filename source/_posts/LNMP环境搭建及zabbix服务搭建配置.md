---
title: LNMP环境搭建及zabbix服务搭建配置
date: 2019-10-18 16:03:22
tags:
- zabbix
copyright: true
categories: Linux
mathjax: true
---

**前言**

> 在linux环境中安装nginx、mysql、php，搭建LNMP环境。搭建zabbix服务端，在客户机上安装zabbix客户端，基于zabbix客户端，编写一个脚本程序，检测linux客户端上特定软件包（本次指定openssl）的版本，上报到服务端

<!-- more -->

### LNMP环境搭建

#### 环境说明：

OS：   centos7.7_x64

nginx： nginx-1.8.0

php：   php-5.6.28

mysql： mysql-5.7.28

zabbix：zabbix-3.4.3

#### 安装前准备

##### 关闭防火墙和selinux

\# systemctl status firewalld  //查看防火墙状态

\# systemctl stop firewalld   //停止防火墙

\# systemctl disable firewalld.service  //禁止开机启用防火墙

\# vi /etc/selinux/config    //进入配置文件  设置：SELINUX=disabled（重启才生效）

##### 准备yum源

\# wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

\# yum -y install epel-release

##### 安装依赖关系

\# yum install pcre*   //为了支持rewrite功能

\# yum install openssl  openssl-devel

\#yum install gcc make gd-devel libjpeg-devel libpng-devel libxml2-devel bzip2-devel libcurl-devel -y  //编译需要的依赖包

#### nginx安装

##### 下载安装包

\# wget http://nginx.org/download/nginx-1.8.0.tar.gz

##### 编译安装

\# tar –zxvf nginx-1.8.0.tar.gz -C /usr/local     //解压nginx到/usr/local路径下

\# cd /usr/local/nginx-1.8.0/

\#./configure --user=nobody --group=nobody --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_gzip_static_module --with-http_realip_module --with-http_sub_module --with-http_ssl_module

\# make && make install

##### 启动nginx服务

\# /usr/local/nginx/sbin/nginx

打开浏览器访问此机器的 IP，如果浏览器出现 Welcome to nginx! 则表示 Nginx 已经安装并运行成功。

##### 编辑nginx主配置文件

\# vi /usr/local/nginx/conf/nginx.conf

主要对server项做如下的改动：

​       server {

​        listen       80;

​        server_name  localhost;

 

​        location / {

​            root   /usr/local/nginx-1.8.0/html/;

​            index  index.html index.htm index.php;

​            autoindex on;

​        }        

autoindex on;

​        autoindex_exact_size on;

autoindex_localtime on;

 

​        location ~ \.php$ {

​            root           /usr/loca/nginx-1.8.0/html;

​            fastcgi_pass   127.0.0.1:9000;

​            fastcgi_index  index.php;

​            fastcgi_param  SCRIPT_FILENAME  /usr/local/nginx-1.8.0/html$fastcgi_script_name;

​            \# fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;

​            include        fastcgi_params;

​        }

}

##### 重启nginx

\# /usr/local/nginx/sbin/nginx –s reload

#### 安装mysql

##### 下载和安装mysql5.7

\# wget http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm

\# yum localinstall mysql57-community-release-el7-7.noarch.rpm

\# yum repolist enabled | grep "mysql.*-community.*"

\# yum install mysql-community-server

\# systemctl start mysqld.service

\# grep 'temporary password' /var/log/mysqld.log  //记录随机密码

\# mysql_secure_installation  //初始化

\# mysql -u root –p  //用随机密码登陆

##### 新建以及初始化数据库zabbix

\> create database zabbix character set utf8;;

\> use zabbix;

\> source /root/zabbix-3.4.3/database/mysql/schema.sql;  // 在安装完zabbix后的操作

\> source /root/zabbix-3.4.3/database/mysql/data.sql;     // 在安装完zabbix后的操作

\> source /root/zabbix-3.4.3/database/mysql/images.sql;   // 在安装完zabbix后的操作

#### 安装php

##### 安装依赖扩展包

\# yum -y install libmcrypt libmcrypt-devel

mhash mhash-devel mcrypt libxml2-devel bzip2-devel libcurl-devel libjpeg-devel libpng
libpng-devel freetype freetype-devel libmcrypt libmcrypt-devel

##### 下载php

\# wget http://php.net/get/php-5.6.28.tar.gz/from/this/mirror -O php-5.6.28.tar.gz

##### 编译安装php

\# tar –zxvf php-5.6.28.tar.gz

\# cd php-5.6.28

\# ./configure -prefix=/usr/local/php -with-config-file-path=/usr/local/php/etc -with-bz2 -with-curl -enable-ftp -enable-sockets -disable-ipv6 -with-gd -with-jpeg-dir=/usr/local -with-png-dir=/usr/local -with-freetype-dir=/usr/local -enable-gd-native-ttf -with-iconv-dir=/usr/local -enable-mbstring -enable-calendar -with-gettext -with-libxml-dir=/usr/local -with-zlib -with-pdo-mysql=mysqlnd -with-mysqli=mysqlnd -with-mysql=mysqlnd -with-ldap -enable-dom -enable-xml -enable-fpm -with-libdir=lib64 -enable-bcmath

\# make && make install

##### 准备php和php-fpm的配置文件

编辑php-5.6.28解压文件下的php.ini-production

\# vi /php-5.6.28/ php.ini-production

修改如下参数：

max_execution_time = 300

memory_limit = 128M

​      post_max_size = 16M

​      upload_max_filesize = 2M

​      max_input_time = 300

​      date.timezone = PRC

\# cp /php-5.6.28php.ini-production /usr/local/php/etc/php.ini

\# cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf

##### 编辑php-fpm的配置文件

\# /usr/local/php/etc/php-fpm.conf

取消pid的注释：

……

[global]

 

pid = run/php-fpm.pid

……

##### 启动php-fpm，占用端口9000

\# /usr/local/php/sbin/php-fpm

##### 测试php

在/usr/local/nginx-1.8.0/html/目录下新建test.php：

vi /usr/local/nginx-1.8.0/html/test.php

内容如下：

​    <?php

​    phpinfo();

​    ?>

重启nginx：

\# /usr/local/nginx/sbin/nginx -s reload

在浏览器中输入：http://192.168.112.101/test.php ，出现以下画面则说明配置php成功

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/php%E6%B5%8B%E8%AF%95%E9%A1%B5%E9%9D%A2.png)

### zabbix server安装与配置

#### 安装zabbix

##### 安装依赖包

\# yum install mysql-devel –y

如果编译遇到mysql文件冲突，则可能是版本冲突，使用rpm下载：

\# wget ftp://ftp.pbone.net/mirror/dev.mysql.com/pub/Downloads/MySQL-5.7/mysql-community-devel-5.7.25-1.el7.x86_64.rpm

\# yum localinstall mysql-community-devel-5.7.25-1.el7.x86_64.rpm

\# yum install net-snmp-devel –y

\# yum install libevent-devel –y

##### 下载zabbix

\# wget https://nchc.dl.sourceforge.net/project/zabbix/ZABBIX%20Latest%20Stable/3.4.3/zabbix-3.4.3.tar.gz

#### 编译安装zabbix

\# tar –zxvf zabbix-3.4.3

\# cd zabbix-3.4.3

\#./configure --prefix=/usr/local/zabbix --with-mysql --with-net-snmp --with-libcurl --enable-server --enable-agent --enable-proxy

\# make && make install

安装完成后记得回到数据库安装步骤，导入数据库

#### 配置server和agentd

##### 编辑zabbix_server.conf

vi /usr/local/zabbix/etc/zabbix_server.conf

做如下的改动：

​    DBName=zabbix

​    DBUser=root         // 如果给zabbix数据库创建了用户，则改为zabbix数据库用户

​    DBPassword=123456  // zabbix数据库的密码

​    DBPort=3306

##### 编辑zabbix_agentd.conf

vi /usr/local/zabbix/etc/zabbix_agentd.conf

做如下改动：

​    Server=127.0.0.1

​    ServerActive=127.0.0.1

​	Hostname=Zabbix server

##### 配置nginx zabbix

拷贝zabbix前端文件到nginx的html文件夹中：

\# cp -r /root/zabbix-3.4.3/frontends/php/*   /usr/local/nginx-1.8.0/html/zabbix

\# chmod –R 777 /usr/local/nginx-1.8.0/html

##### 启动zabbix server和zabbix agent

\# /usr/local/zabbix/sbin/zabbix_server

\# /usr/local/zabbix/sbin/zabbix_agentd

#### 界面配置zabbix

##### 使用浏览器访问

http://192.168.112.101/zabbix/setup.php

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E8%AE%BF%E9%97%AEzabbix%E9%85%8D%E7%BD%AE%E9%A1%B5%E9%9D%A2.png)

在检测信息时，可查看具体的报错信息对/usr/local/php/etc/php.ini文件进行编辑解决

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E4%BF%A1%E6%81%AF%E6%A3%80%E6%B5%8B%E9%A1%B5%E9%9D%A2.png)

对应/usr/local/zabbix/etc/zabbix_server.conf文件填写数据库名称、用户和密码：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE%E5%BA%93.png)

host与port不需要修改，name自定义

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/zabbix%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%AF%A6%E7%BB%86%E4%BF%A1%E6%81%AF.png)

确认信息,正确点击下一步

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E5%AE%89%E8%A3%85%E5%89%8D%E6%B1%87%E6%80%BB.png)

根据以下页面的提示下载配置文件，并将配置文件保存到/usr/local/nginx-1.8.0/html/zabbix/conf/zabbix.conf.php，点击“完成”

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/zabbix%E9%85%8D%E7%BD%AE%E5%AE%8C%E6%88%90.png)

配置完成后进入登陆页面，默认登陆名为：admin，密码为：zabbix

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/zabbix%E7%99%BB%E9%99%86%E7%95%8C%E9%9D%A2.png)

在跳转的页面中点击右上角的小人头像可以设置web页面的语言：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/zabbix%E9%A1%B5%E9%9D%A2%E8%AF%AD%E8%A8%80%E8%AE%BE%E7%BD%AE.png)

##### 添加监控信息

修改监控管理机zabbix server：配置>>主机>>Zabbix server

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E4%BF%AE%E6%94%B9%E7%9B%91%E6%8E%A7%E7%AE%A1%E7%90%86%E6%9C%BA.png)

主机名称： 要与主机名相同，这是zabbix server程序用的

可见名称： 显示在zabbix网页上的，给我们看的

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E9%85%8D%E7%BD%AE%E7%9B%91%E6%8E%A7%E7%AE%A1%E7%90%86%E6%9C%BA.png)

修改后，要将下面的已启用要勾上。添加完成就有了管理机的监控主机，注意ZBX要显示为绿色

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E7%9B%91%E6%8E%A7%E4%B8%BB%E6%9C%BA%E9%85%8D%E7%BD%AE%E5%AE%8C%E6%88%90.png)

### 监控客户机的openssl版本

#### 客户机安装zabbix agent

##### 安装依赖

\# yum -y install net-snmp-devel

libxml2-devellibcurl-deve libevent libevent-devel

##### 安装zabbix agent

\# yum install zabbix-agent –y

##### 编辑配置文件

\# vi /etc/zabbix/zabbix_agentd.conf

修改server、hostname、serveractive信息：

Server=192.168.112.101   //zabbix server的ip

ServerActive=192.168.112.101   //和server相同

Hostname=centos6   //记住hostname，在zabbix server中添加主机时用到

##### 启动zabbix agent

\# /usr/sbin/zabbix_agentd

#### zabbix server添加监控主机

##### 创建主机

配置>>主机，主机名称与zabbix_agentd.conf中的一致，IP地址填写客户机的IP地址

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E5%88%9B%E5%BB%BA%E4%B8%BB%E6%9C%BA.png)

##### 客户端自定义监控项

本次监控的是客户机上的openssl版本。

（1）查看客户端openssl版本：

\# yum info openssl

可以看到两组信息，一个是已安装的openssl软件包的信息，还有一组是可安装的openssl软件包的信息，其中，客户端已安装版本是1.0.1e，可安装版本是1.0.2k，我们需要让zabbix server自动监控客户端的openssl版本，并在版本较低时发出告警。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E5%B7%B2%E5%AE%89%E8%A3%85%E7%9A%84openssl%E4%BF%A1%E6%81%AF.png)

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E5%8F%AF%E5%AE%89%E8%A3%85%E7%9A%84openssl%E4%BF%A1%E6%81%AF.png)

2）修改客户端配置文件zabbix_agentd.conf

\# vi /etc/zabbix/zabbix_agentd.conf

搜索 ‘UnsafeUserParameters’取消注释#号，将‘0’改为‘1’

Include=/etc/zabbix/zabbix_agentd.d/*.conf

\# cd cd /etc/zabbix/zabbix_agentd.d/

自定义监控项的key值，格式为UserParameter=<key>,<shell command>，key值不能与现有的重复。

\# vi userparameter_openssl.conf   // 新建自定义监控项的配置文件，内容如下

UserParameter=openssl_version,yum info openssl|awk -F: '/^Version/{print $2;exit;}'

其中openssl_version为key值，yum info openssl|awk -F: '/^Version/{print $2;exit;}'为获取openssl版本号的命令。

##### 在server端配置

（1）在zabbix服务端使用zabbix-get

\# yum install zabbix-get –y

\# zabbix_get -s 192.168.112.101 -p 10050 -k "openssl_version"

结果为：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/server%E7%AB%AF%E4%BD%BF%E7%94%A8zabbix_get.png)

其中-s参数指定客户端地址，-p指定端口，-k指定key值，这里获取到客户端的openssl版本号为1.0.1e。

（2）在zabbix的web界面添加自定义监控项

点击：配置>>主机>>监控项

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E6%B7%BB%E5%8A%A0%E8%87%AA%E5%AE%9A%E4%B9%89%E7%9B%91%E6%8E%A7%E9%A1%B9.png)

在跳转的页面中点击“创建监控项”，跳转到如下界面，并添加监控项信息，其中的键值要去自定义的key值对应，即openssl_version，因为获取的是字符串，所以数据类型选择“字符”，更新时间间隔，历史数据保留时长等根据所添加的监控项合理设置，这里为了尽快看到数据，将更新时间设置为30秒。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E9%85%8D%E7%BD%AE%E8%87%AA%E5%AE%9A%E4%B9%89%E7%9B%91%E6%8E%A7%E9%A1%B9.png)

在页面最后勾选“已启用”，点击“添加”。

点击：监测中>>最新数据>>监控项的历史记录，就可以看到监控的结果

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E8%87%AA%E5%AE%9A%E4%B9%89openssl%E7%9B%91%E6%8E%A7%E7%9A%84%E7%9B%91%E6%8E%A7%E7%BB%93%E6%9E%9C.png)

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E6%98%BE%E7%A4%BA%E5%AE%A2%E6%88%B7%E6%9C%BA%E7%9A%84openssl%E7%89%88%E6%9C%AC.png)

（3）设置触发器

点击：配置>>主机>>触发器

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E5%88%9B%E5%BB%BA%E8%A7%A6%E5%8F%91%E5%99%A8.png)

在跳转的页面中点击右上角的“创建触发器”，在名称中填写告警的提示信息，严重性可以自己选择，这里选择的是“警告”，即如果监控到的客户机openssl版本与指定的版本不一致，将会出现名为“The openssl needs
to be updated”的警告信息。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E9%85%8D%E7%BD%AE%E8%A7%A6%E5%8F%91%E5%99%A8.png)

在表达式中填写规则，点击右侧的“添加”，在弹出的窗口中填入规则信息，监控项选择我们我们创建的监控项openssl，功能选择“查找字符串V的最近值……”，V则填写我们指定的openssl版本号，最后点击插入。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E8%AE%BE%E7%BD%AE%E8%A7%A6%E5%8F%91%E6%9D%A1%E4%BB%B6.png)

勾选页面下面的“已启用”，最后点击“添加”。

##### 监控结果

点击：检测中>>仪表盘，可以显示问题信息，由于我们客户机的openssl版本是1.0.1e，而我们指定的版本是1.0.2k，所以触发了“The openssl needs to be updated”的警告信息

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/LNMP%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8Azabbix%E6%9C%8D%E5%8A%A1%E6%90%AD%E5%BB%BA%E9%85%8D%E7%BD%AE/%E8%A7%A6%E5%8F%91%E8%AD%A6%E5%91%8A%E4%BF%A1%E6%81%AF.png)

