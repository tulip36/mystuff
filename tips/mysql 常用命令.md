### 1. 在Mysql中显示所有用户**

#### 1).登录数据库

首先，你需要使用如下[命令](https://www.linuxcool.com/)登录到数据库，注意，必须是root用户哦~

```
## mysql -u root -p
```

#### 2).查询用户表

在Mysql中其实有一个内置且名为**mysql**的数据库，这个数据库中存储的是Mysql的一些数据，比如用户、权限信息、存储过程等，所以呢，我们可以通过如下**简单的查询语句**来显示所有的用户呢。

```
SELECT User, Host, Password FROM mysql.user;
```

**你将会看到如下这样的信息：**

```
+------------------+--------------+--------------+
| user             | host         | password     |
+------------------+--------------+--------------+
| root             | localhost    | 37as%#8123fs |
| debian-test-user | localhost    | HmBEqPjC5Y   |
| johnsm           | localhost    |              |
| brian            | localhost    |              |
| root             | 111.111.111.1|              |
| guest            | %            |              |
| linuxprobe       | 10.11.12.13  | RFsgY6aiVg   |
+------------------+--------------+--------------+
7 rows in set (0.01 sec)
```

如果你想增加或减少一些列的显示，那么你只需要编辑这条sql语句即可，比如你只需要显示用户的用户名，那么你就可以这样使用**SELECT User FROM mysql.user;**，就是这样了，很简单嘛，就用这种方法就可以获得所有用户了呢，快去试试吧。

#### 3).显示所有的用户（不重复）

熟悉Mysql的朋友们都知道**DISTINCT**这个修饰的作用吧，对了，就是去除重复的数据，所以我们可以使用如下命令显示所有你的Mysql的用户而忽略那些仅仅是主机名不同的用户。

```
SELECT DISTINCT User FROM mysql.user;
```

这条命令的输出就像下面显示的这样：

```
+------------------+
| user             | 
+------------------+
| root             | 
| debian-test-user | 
| johnsm           | 
| brian            | 
| guest            | 
| linuxprobe       | 
+------------------+
6 rows in set (0.01 sec)
```



### 2. . 改变用户密码

Mysql change user password using the following method:

1. Open the bash shell and connect to the server as root user

2. **mysql -u root -h localhost -p**

3. Run command:

4. **ALTER USER 'userName'@'localhost' IDENTIFIED BY 'New-Password-Here';**

### 3. 显示数据库列表。 
   show databases; 

### 4. 显示库中的数据表： 
   use mysql;
   show tables; 

### 5. 显示数据表的结构： 
   describe 表名; 
### 6. 建库： 
   create database 库名; 
### 7. 建表： 
   use 库名； 
   create table 表名 (字段设定列表)； 
### 8. 删库和删表: 
   drop database 库名; 
   drop table 表名； 
### 9. 将表中记录清空： 
   delete from 表名; 
### 10. 显示表中的记录： 
   select * from 表名