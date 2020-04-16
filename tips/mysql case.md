在Linux服务器查看如下：

mysql> show variables like '%case%';
+------------------------+-------+
| Variable_name          | Value |
+------------------------+-------+
| lower_case_file_system | OFF    |
| lower_case_table_names | 0     |
+------------------------+-------+
从上面的结果已经可以看出不同了，然而对这两个参数还没有感觉，不知道具体是什么意思。

在介绍lower_case_table_names的时候，顺便也说一下lower_case_file_system。

lowercasefile_system
此变量描述数据目录所在的文件系统上文件名的区分大小写。 OFF表示文件名区分大小写，ON表示它们不区分大小写。此变量是只读的，因为它反映了文件系统属性并设置它对文件系统没有影响。

lowercasetable_names
该参数为静态，可设置为0、1、2。

0 --大小写敏感。（Unix，Linux默认） 创建的库表将原样保存在磁盘上。如create database TeSt;将会创建一个TeSt的目录，create table AbCCC …将会原样生成AbCCC.frm。 SQL语句也会原样解析。

1 --大小写不敏感。（Windows默认） 创建的库表时，MySQL将所有的库表名转换成小写存储在磁盘上。 SQL语句同样会将库表名转换成小写。 如需要查询以前创建的Testtable（生成Testtable.frm文件），即便执行select * from Testtable，也会被转换成select * from testtable，致使报错表不存在。

2 --大小写不敏感（OS X默认） 创建的库表将原样保存在磁盘上。 但SQL语句将库表名转换成小写。

On Windows the default value is 1. On macOS, the default value is 2. On Linux, a value of 2 is not supported; the server forces the value to 0 instead.

在Windows上，默认值为1。在macOS上，默认值为2。在Linux上不支持值2;服务器强制该值为0。

在CentOS安装的MySQL的配置文件中(/etc/my.cnf)，是没有lower_case_table_names=1这行的。 
在Windows安装的MySQL的配置文件中(my.ini)，是有lower_case_table_names=1这行的。 
lower_case_table_names=1的用途是让MySQL实现不区分大小写。 所以当时出了些毛病，后来才发现是这个的问题。
连忙在my.cnf(/etc/my.cnf)的[mysqld]区段下增加: lower_case_table_names=1
