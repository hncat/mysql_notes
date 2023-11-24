# 1 使用mysql
## 0.1 连接
```sql
mysql -uroot -hlocalhost -p
```
## 0.2 选择数据库
use database; => database为需要使用的数据库名称
```sql
mysql> use far_demo;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```
## 0.3 了解数据库和表
但我们不知道使用那个数据库时可以查看可用的数据库列表和列
### 显示所有数据库列表: show databases;
```sql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| far_demo           |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)
```
### 显示数据的表的列表: show tables;
```sql
use far_demo;
mysql> show tables;
+--------------------+
| Tables_in_far_demo |
+--------------------+
| customers          |
| orderitems         |
| orders             |
| productnotes       |
| products           |
| vendors            |
+--------------------+
6 rows in set (0.00 sec)
```
### 使用show显示表的列信息: show columns from (table_name);
```sql
mysql> show columns from customers;
+--------------+-----------+------+-----+---------+----------------+
| Field        | Type      | Null | Key | Default | Extra          |
+--------------+-----------+------+-----+---------+----------------+
| cust_id      | int       | NO   | PRI | NULL    | auto_increment |
| cust_name    | char(50)  | NO   |     | NULL    |                |
| cust_address | char(50)  | YES  |     | NULL    |                |
| cust_city    | char(50)  | YES  |     | NULL    |                |
| cust_state   | char(5)   | YES  |     | NULL    |                |
| cust_zip     | char(10)  | YES  |     | NULL    |                |
| cust_country | char(50)  | YES  |     | NULL    |                |
| cust_contact | char(50)  | YES  |     | NULL    |                |
| cust_email   | char(255) | YES  |     | NULL    |                |
+--------------+-----------+------+-----+---------+----------------+
9 rows in set (0.00 sec)
```
### 其它的show语句
```
 SHOW STATUS，用于显示广泛的服务器状态信息；
 SHOW CREATE DATABASE和SHOW CREATE TABLE，分别用来显示创
建特定数据库或表的MySQL语句；
 SHOW GRANTS，用来显示授予用户（所有用户或特定用户）的安
全权限；
 SHOW ERRORS和SHOW WARNINGS，用来显示服务器错误或警告消息。
```