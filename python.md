<style type="text/css">
code {
	color: blue;
	font-size: 16px;
}
</style>
## Python ##

### 1. Python 环境变量设置

在PATH 中添加 python的安装目录， 和安装目录下的Scripts目录(pip)， 

### 2.使用国内的pypi镜像 ###

Linux 在~/.pip/pip.conf 文件中
Windows 在%HOME%\pip\pip.ini 文件中， 添加一下内容：

	[global]
	index-url=http://pypi.douban.com/simple/

在命令行中指定镜像：
	
	pip install package-name -i url

### 3. windows 下 MySQL-Python　安装
在http://www.codegood.com/download 网站上下载 MySQL-python-1.2.3.win-amd64-py2.7.exe
安装即可


## Python Mysql

### 1. 连接数据库
	
connect( *args, **kwargs), 返回一个Connection对象

#### connect( *args, **kwargs )函数参数详解：
* host： name of host to connect to . Default: use the local host via a UNIX socket
* user: user to authenticate as
* passwd: password to authenticate with
* db: database to use
* poart: TCP port of MySQL server
* init_command:
* connect_timout: 连接超时
* charset: 字符集
* ssl: 

例子：
	conn = MySQLdb.connect( host=host, user=user, passwd=password, db=db, port=3306)

如果没有在 connect 中指定数据库， 可以使用
	conn.select_db(dbname)
选择数据库

### 2. 获取游标
	cur = conn.cursor(cursorType)

#### Cursor 的类型
Curosr 在 MySQLdb.cursors包下

* BaseCursor: The base class for Cursor objects
* CursorStoreResultMixIn: 使用 mysql_store_result()函数查询结果， 整个结果集保存在客户端
* CursorUseResultMixIn： 使用 mysql_use_result()函数查询结果，结果集保存在服务端， 使用fetch 操作获取数据
* CursorTupleRowsMixIn：把结果的列值作为一个Tuple(元组)返回
* CursorDictRowsMixIn： 把结果作为Dict(字典), 表的column 名作为 key， 列值作为value
* Cursor： conn.cursor()的函数默认值， This class is composed of CursorWarningMixIn, ursorStoreResultMixIn, CursorTupleRowsMixIn, and BaseCursor, i.e. it raises Warning, uses mysql_store_result(), and returns rows as tuples.
* DictCursor: Like Cursor except it returns rows as dictionaries
* SSCursor: A "server-side" cursor. Like Cursor but uses CursorUseResultMixIn. Use only if you are dealing with potentially large result sets
* SSDictCursor: Like SSCursor except it returns rows as dictionaries.
### 3. 执行Sql 语句
	
#### 执行单条sql语句
	cur.execute( sql )
	conn.commit()
例子：

	c.execute("""SELECT spam, eggs, sausage FROM breakfast
          WHERE price < %s""", (max_price,))
#### 批处理
	cur.executemany( sql , [])
	conn.commit()
例子：

	c.executemany(
      """INSERT INTO breakfast (name, spam, eggs, sausage, price)
      VALUES (%s, %s, %s, %s, %s)""",
      [
      ("Spam and Sausage Lover's Plate", 5, 1, 8, 7.95 ),
      ("Not So Much Spam Plate", 3, 2, 0, 3.95 ),
      ("Don't Wany ANY SPAM! Plate", 0, 4, 3, 5.95 )
      ] )

### 4. 获取结果
#### 获取单个结果
#### 获取多个结果
#### 获取所有结果

	cur.fetchone()
	cur.fetchall()
	cur.fetchmany(count)

### 5. 关闭连接
	cur.close()
	conn.close()

