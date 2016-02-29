## Mysql 存储过程

### 查看存储过程
```
 1. SHOW PROCEDURE STATUS
  
 2. SELECT name from mysql.proc where db='your_db_name' and type = 'PROCEDURE'
```

### 查看创建存储过程语句
```
  SHOW CREATE PROCEDURE proc_name
  SHOW CREATE FUNCTION func_name
```

### 创建存储过程语法
```
  CREATE PROCEDURE proc_name( IN param1 TYPE, IN param2 TYPE[, ...])
    RETURNS TYPE
    
  BEGIN
    DECLARE var1 type;
    DECLARE var2 type;
    
    RETURN var?
  EDN
```
