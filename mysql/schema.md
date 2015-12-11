## 数据库创建语法

### 创建表以及设置表的约束关系

```
  CREATE TABLE `db_name`.`table_name` (
    `columnd_name` ...,
    PARIMARY KEY(`pk`),
    CONSTRAINT  `fk_1` FOREIGN KEY(`foreign_column`) REFERENCES `table_name`(`column`) ON DELETE CASCADE
  ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
