##### 一、create database Statement

###### 1.语法

```
CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name [create_option] ...

create_option: [DEFAULT] {
  CHARACTER SET [=] charset_name
 | COLLATE [=] collation_name
}
```

\#CREATE SCHEMA是CREATE DATABASE的同义词，create schema等同于create database

\#记不住字符集和排序规则的时候，分别使用 SHOW CHARACTER SET and SHOW COLLATION语句查看可用的字符集和排序规则，

 

###### 2.示例

```
mysql> create database testdb01 default character set utf8mb4 collate utf8mb4_general_ci;
```

 

###### 3.其它事项

a.如果您在数据目录下手动创建一个目录（例如，使用mkdir），则服务器将其视为数据库目录并显示在 show databases.

```
[root@mydb01 data]# mkdir testdb
[root@mydb01 data]# chown mysql:mysql testdb
[root@mydb01 data]# mysql -uroot -p

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| database           |
| mysql              |
| performance_schema |
| sys                |
| testdb             |
| testdb01           |
+--------------------+

mysql> show create database testdb;
+----------+--------------------------------------------------------------------+
| Database | Create Database                                                    |
+----------+--------------------------------------------------------------------+
| testdb   | CREATE DATABASE `testdb` /*!40100 DEFAULT CHARACTER SET utf8mb4 */ |
+----------+--------------------------------------------------------------------+
1 row in set (0.00 sec)
```

b.创建数据库时，让服务器管理目录和其中的文件。直接操作数据库目录和文件可能会导致不一致和意外结果。

c.MySQL 对数据库的数量没有限制。底层文件系统可能对目录的数量有限制。

d.还可以使用mysqladmin来创建数据库，示例：

```
[root@mydb01 ~]# mysqladmin -uroot -proot create test123
[root@mydb01 ~]# mysqladmin -uroot -proot drop test123
```

