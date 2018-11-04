---
layout: post
title: "Docker安装Mysql大小写敏感"
author: "Liang"
header-style: text
tags:
  - Docker
  - Mysql
---

进入Mysql容器的交互页面：

```
docker exec -it 容器ID/名称 /bin/bash
```

查看当前大小写敏感配置：

```
show global variables like '%lower_case%';
```

```
+------------------------+-------+
| Variable_name          | Value |
+------------------------+-------+
| lower_case_file_system | OFF   |
| lower_case_table_names | 0     |
+------------------------+-------+
```

lower_case_file_system 当前系统文件是否大小写敏感，只读参数，不能修改，ON  大小写敏感，OFF 大小写不敏感。

lower_case_table_names 表名是否敏感 0敏感，1敏感。



修改 lower_case_table_names  参数：

进入Docker的Mysql容器，编辑 /etc/mysql/mysql.conf.d/mysqld.cnf 文件，在[mysqld]下添加：

```
[mysqld] 
lower_case_table_names=1
```

保存退出，重启容器

```
docker restart 容器ID/名称
```



