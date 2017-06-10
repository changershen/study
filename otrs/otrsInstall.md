### 服务器配置

#### 环境配置

1.[Ubuntu系统安装](http://www.zrway.com/news/8390.html)

2.[Ubuntu安装mysql](https://jingyan.baidu.com/article/425e69e6bbc6c7be14fc1640.html)

```bash
# sudo apt-get update
# sudo apt-get install mysql-server mysql-client
# sudo service mysql restart
# sudo service mysql stop
```

3.安装perl

```bash
# sudo apt-get install perl
# perl -v
```

4.[安装Apache](http://www.linuxidc.com/Linux/2013-06/85827.htm)

```bash
# sudo apt-get install apache2
# sudo /etc/init.d/apache2 restart/stop/start
```

我的安装完之后一直有报错，按照教程解决了以后也是一样，然后我试着打开网址，网址上出现it work!所以还是先看看能不能打开网址。

5.[安装游览器](http://www.cnblogs.com/alala666888/archive/2012/05/24/2516518.html)(没有桌面的建议安装)

```bash
# sudo apt-get install w3m
# w3m www.baidu.com  --打开网址 q 退出
```

6.安装lxde桌面(可以不安装)：

```bash
sudo apt-get install lxde --安装后没有测试到是否成功了
```

7.安装vnc服务(可以不安装远程桌面)： 

```ssh
# sudo apt-get install vnc4server --安装vnc服务
# vncpasswd --.修改VNC密码
# vncserver --启动VNC server：
# adduser vnc --添加用户
# apt-get install sudo --if installed sudo you can scape it
# gpasswd -a vnc sudo
# su - vnc --chang to vnc user
$ vncserver --开启关闭服务
$ vncserver -kill :1
```

8.安装程序

```bash
下载安装
# wget ftp.otrs.org.cn/pub/otrs/otrs-5.0.18.tar.gz
# tar xzf /tmp/otrs-x.x.x.tar.gz
# mv otrs-x.x.x /opt/otrs
# perl /opt/otrs/bin/otrs.CheckModules.pl --解决未安装的模块
# apt-cache search Digest::MD5
# apt-get install libdigest-md5-perl
# perl -MCPAN -e shell 
添加用户
useradd -d /opt/otrs -c 'OTRS user' otrs
usermod -G www-data otrs
激活配置
shell> cd /opt/otrs/
shell> cp Kernel/Config.pm.dist Kernel/Config.pm
检查模块
shell> perl -cw /opt/otrs/bin/cgi-bin/index.pl
/opt/otrs/bin/cgi-bin/index.pl syntax OK
shell> perl -cw /opt/otrs/bin/cgi-bin/customer.pl
/opt/otrs/bin/cgi-bin/customer.pl syntax OK
shell> perl -cw /opt/otrs/bin/otrs.Console.pl
/opt/otrs/bin/otrs.Console.pl syntax OK
配置Apache web服务器
shell> apt-get install apache2 libapache2-mod-perl2  出错，
root@vultr:/opt/otrs# apt-get install apache2 libache2-mod-perl2
Reading package lists... Done
Building dependency tree
Reading state information... Done
E: Unable to locate package libache2-mod-perl2
设置权限
/opt/otrs/var# chmod 777 tmp
 cp /opt/otrs/scripts/apache2-httpd.include.conf /etc/apache2/conf-available/otrs.conf 创建连接
ubuntu-shell> a2enconf otrs.conf
ubuntu-shell> service apache2 restart

shell> a2enmod perl
shell> a2enmod version 这里报错后面就没有处理不影响
shell> a2enmod deflate
shell> a2enmod filter
shell> a2enmod headers

开启守护进程
/opt/otrs/var/cron/otrs_daemon检查文件是否存在
/opt/otrs/bin/Cron.sh start开启cron文件
sudo -u otrs ./otrs.Daemon.pl start 用otrs账号开启Daemon文件
bin/otrs.Daemon.pl status状态检查
```

### 总结

1.安装的过程就是按照步骤来进行没有问题，设置的时候一定要把权限打开。

2.安装完之后就可以登陆了，但一定要记录下那个root自动生成的密码，不然会很惨。

3.linux命令安装的时候记得看好，有的命令好长。

参考文献：[vnc](https://www.digitalocean.com/community/tutorials/how-to-set-up-vnc-server-on-debian-8)