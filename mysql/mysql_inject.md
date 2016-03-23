##Sql inject

1. 什么是SQL 注入？
首先我们来看一条sql 语句：
 ```
  MariaDB [test]> select * from users where name='' or 1;
+----+---------+--------------+-------------+
| id | name    | fullname     | password    |
+----+---------+--------------+-------------+
|  1 | donghua | donghua Xiao | xdhua860923 |
|  2 | jack    | Jack test    | 123456      |
|  3 | donghua | donghuaXiao  | 123123      |
|  4 | jackson | jackson Jue  | 234523      |
|  5 | test1   | cloud test1  | 2wsx3edc    |
+----+---------+--------------+-------------+
 ```
 有where 从句的 sql 语句执行过程：把每一条记录中的字段代入 where 从句中 进行计算， 如果值为真， 就返回该条记录，
 
 现在条件为： name='' or 1 ， 始终为真， 所以返回所有记录。
 
 SQL 注入： 在 表单或 querystring 中字段值后面加上条件语句，使得条件始终为真，以通过认证，获取数据库数据，或在后面加上 破坏性的
 sql 语句， 当执行该sql 语句时， 执行一些更新或删除操作，破坏数据库。
 
 例子：
 . select * from user where name='' or 1
 . select * from user where nanme=''; delete * from user where 1 or name=''
 
2. 怎样避免SQL 注入？
  1. 对所以sql 的赋值 进行检测， 避免拼接sql 语句
  2. 使用预先编译的语句， java 中使用 PreparedStatement, php PDO 中使用 prepare 
  3. 预先编译的sql 语句也不是觉得安全，还要避免以下几点：
    1. 不能使用站位符 ？ 替代一组值， 比如：  in( ? )
    2. 不能使用 ？ 替代 表名，列名 比如： order by ?
    3. 不要使用 ? 替代 sql 语句, 可能传入破坏性的sql 语句。
  4. 关闭错误输出， 把错误输入的日志文件中，避免攻击者从错误中获取平台相关的信息。
  5. 为数据库访问创建单独的用户， 控制用户的权限， 在程序中不要用 root 用户连接数据库。
