# CentOS Install MySQL 

## 1 查看已安装MySQL

``` 
rpm -aq | grep -i mysql
```

## 2 卸载
```
yum remove mysql mysql-server mysql-libs compat-mysql51
rpm -aq | grep -i mysql
rpm -e mysql-community-common-5.6.40-2.el7.x86_64
rpm -e mysql-community-release-el7-5.noarch
whereis mysql
rm -rf /usr/lib/mysql
```

## 3 安装

查找最新的下载安装包
https://dev.mysql.com/downloads/repo/yum/

```
wget https://repo.mysql.com//mysql80-community-release-el7-1.noarch.rpm
rpm -ivh mysql80-community-release-el7-1.noarch.rpm
yum -y install mysql mysql-server mysql-devel
```

## 4 启动
```
service mysqld start
```

## 5 测试
由于新版本MySQL更改了安全策略, 即在安装过程中,创建root账户的同时,随机生成了一个密码,并且是标记为已过期. 登陆之后需重新设置密码.默认密码可在日志文件中查看.
```
cat /var/log/mysqld.log |grep -i password
mysql -u root -p
alter user 'root'@'localhost' identified by 'Password1!';
show databases;
```

> 密码强度设置
```
SHOW VARIABLES LIKE 'validate_password%'
```

- validate_password.policy

Policy|描述
------|--------
LOW(0)|Length
MEDIUM(1)|Length;numeric,lowercase/uppercase,and special charaters; 
STRONG(2)|Lenght;numeric,lowercase/uppercase,and special charaters; dictionary file

```
set global validate_password.policy=0;
set global validate_password.length=6;  
alter user 'root'@'localhost' identified by '123456';
```