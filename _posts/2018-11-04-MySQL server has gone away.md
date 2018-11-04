---
layout: post
title: "MySQL server has gone away 错误"
author: "Liang"
header-style: text
tags:
  - Mysql
---



在使用SQL文件初始化数据库时，发生了"***MySQL server has gone away***" 这样一个错误，Mysql服务断开了连接。

经排查，因为执行的SQL中有一条insert语句插入的内容大于**max_allowed_packet**的限制。

查看**max_allowed_packet**的值

```
show variables like 'max_allowed_packet';
```

修改Mysql的**max_allowed_packet为**1G：

### 方法1：

```
set global max_allowed_packet = 1024*1024*1024;
```

通过该方法修改后，需要重新登录Mysql才能看到修改后的值，实际上已经起作用。这个方法修改的值在重启Mysql后失效。

### 方法二：mysqld.cnf 

修改/etc/mysql/mysql.conf.d/mysqld.cnf，在[mysqld]下添加：

```
[mysqld]
max_allowed_packet=1024M
```

重启Mysql后生效。

