
# 前言
> 目的：安装mysql数据库、记录遇到的问题
> 环境: Windows10、centOs7

# Windows
## 下载mysql
地址可能会有改变、所以就不贴了，手动搜索官方下载，以下附网盘地址。
1、上官网 https://www.mysql.com/
[mysql官网](https://www.mysql.com/)

2、菜单栏找到并进入`DOWNLOADS`

3、点击`MySQL Community (GPL) Downloads »`下载选择

4、选择对应的系统版本
如Windows 进入 MySQL Installer for Windows

5、进入页面后只看得到最新的mysql版本，目前我看到的是8.0.22，但是我想要5.7的怎么办呢？ 看右边有个 `Looking for previous GA versions?`, 点击之后就可以选择以往的版本了，如果没有你要的，可以点击菜单栏的`Archives`, 我选择了5.7.32，下面点击下载（487.5M）；

## 安装
1、点击安装程序
可以选择默认安装、也可以自定义安装 next即可
2、管理员账户默认为root， password为你的密码 继续Execute next finish
## 配环境变量
如果是未选择安装路径默认是`C:\Program Files\MySQL\MySQL Server 5.7\bin`
配入环境变量path

## 启动/暂停mysql
1、`Windows+r`进入cmd
2、键入`services.msc`确定
3、找到mysql启动/暂停 （右键）

## 链接msyql
``` sh
$ mysql -u roo t -p
```




# centOs7

## 卸载
如果系统里有其他版本低的mysql，或者卸载未卸载干净，先处理残留
``` sh
[root@localhost ~]# rpm -qa|grep mariadb  // 查询出来已安装的mariadb
[root@localhost ~]# rpm -e --nodeps 文件名  // 卸载mariadb，文件名为上述命令查询出来的文件
```
如果未卸载干净，找到与`mysql`相关的文件夹并手动删除

## 阿里云Linux上安装配置mysql
1、安装MySQL官方的yum repository
``` sh
[root@localhost ~]# wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
```
2、下载rpm包
``` sh
[root@localhost ~]# yum -y install mysql57-community-release-el7-10.noarch.rpm
```
3、安装MySQL服务
```sh
[root@localhost ~]# yum -y install mysql-community-server
```
4、启动MySQL服务
``` sh
[root@localhost ~]# systemctl start  mysqld.service
```

## mysql几个常见的命令
``` js
重启：systemctl restart mysqld.service

停止：systemctl stop mysqld.service

查看状态：systemctl status mysqld.service
```
## 配置MySQL的开机启动：
``` sh
[root@woitumi-128 ~]# systemctl enable mysqld

[root@woitumi-128 ~]# systemctl daemon-reload   刚刚配置的服务需要让systemctl能识别，就必须刷新配置
```

## 登录MySQL
1、链接msyql
``` js
[root@localhost ~]# mysql -u root -p
```
2、密码查看
第一次登录的时候有零时密码，是mysql安装的时候自动生成的，这个时候我们需要用默认密码登录去修改密码。
``` sh
grep "password" /var/log/mysqld.log   # 查看密码
```

3、使用密码登录会提示错误，这时候我们要跳过密码验证
停止服务：
`systemctl stop mysqld.service`
修改mMySQL的配置文件：
`vi /etc/my.cnf`
在最后加上配置：
`skip-grant-tables`
然后再启动服务：
`systemctl start mysqld.service`

4 执行1、登录就行了

5、修改密码  
这里我们进入mysql的表，在执行sql语句，去更新 进入mysql的表
` update mysql.user set authentication_string=password('你的密码') where user='root' ;`

## 远程登录的问题




参考：
[阿里云cenos安装mysql](https://www.cnblogs.com/zydeboke/p/11467095.html)



