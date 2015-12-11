## 数据库创建语法

### Mysql 创建数据库用户
对于应用程序来说,应该为每个数据库创建一个用户,在程序中使用该用户来连接数据库,而不应该使用root

#### 创建用户

```
  CREATE DATABASE `cloud`;
  CREATE USER cloud identified by 'cloud';
```

#### 对用户进行授权

```
GRANT ALL ON cloud.* to cloud@`localhost` identified by 'cloud';
GRANT ALL ON cloud.* to cloud@`%` identified by 'cloud';
```
cloud@`%` 允许cloud 用户远程访问数据库 cloud
### 创建表以及设置表的约束关系

```
  CREATE TABLE `db_name`.`table_name` (
    `columnd_name` ...,
    PARIMARY KEY(`pk`),
    CONSTRAINT  `fk_1` FOREIGN KEY(`foreign_column`) REFERENCES `table_name`(`column`) ON DELETE CASCADE
  ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
