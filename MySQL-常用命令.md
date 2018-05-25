# MySQL 常用操作
## 数据库连接
```
mysql -h host -P3306 -u user -p;
```

## 数据库管理

操作|命令|备注
---|---|---
显示所有数据库|show databases;
创建数据库|create database dbname;|可设置字符集 charset utf8; 
删除数据库|drop database dbname;
选择数据库|use dbname;
显示当前数据库|select database();
显示当前版本|select version();
显示当前时间|select current_date;
查询数据库参数|show variables like 'max_%';

## 表管理
操作|命令|备注
---|---|---
显示所有表|show tables;
显示表结构|desc students;
创建表|create table students(id int, name varchar(20));
删除表|drop table students;
增加字段|alter table students add(age int);
删除字段|alter table students drop age;
设置自增和主键|alter table students modify id int auto_increment primary key;
修改字段类型|alter table students modify age char(10);
设置默认值|alter table students alter column age set default 0;
重命名字段|alter tbale students change age age2 char(20);

## 索引操作
操作|命令|备注
---|---|---
查看索引|show index from students;
唯一索引|alter table students add unique(name);|允许有控制
索引|alter table students add index(age);
删除索引|drop index indexname on students;


## 数据操作
操作|命令|备注
---|---|---
查询数据|select * from students;
更新数据|update students set name='Rob';
插入数据|insert students(id,name) values(1,'Lee');
插入多条数据|insert students(id,name) values(1,'Lee'),(2,'Jay');
删除数据|delete from students;
清空数据|truncate table students;

## 用户管理
操作|命令|备注
---|---|---
当前用户|select user();
创建用户|create user uv identified by '123456';
更改普通用户密码|set password for name=PASSWORD('123456');
查看权限|show grants for uv;
