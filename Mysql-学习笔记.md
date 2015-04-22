<style type="text/css">
code {
	font-size: 14px;
	color: blue;
}
</style>
## Mysql 学习笔记


### 1.Mysql5.5 安装

####安装mysql5.5 源 
	rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
	rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
	yum --enablerepo=remi,remi-test install mysql mysql-server

### 2. Mysql 表名大小写敏感问题

在 /etc/my.cnf 中的[mysqld] 设置 lower_case_table_names 来控制表名的大小写敏感问题：

	lower_case_table_names = 1 不区分大小写
	lower_case_table_names = 0 区分大小写

### 3. 在Shell 脚本中执行Mysql 命令
#### 1)、使用 -e 选项传递命令，适合简单命令 

mysql -uusername -ppasswd -e "mysql cmd"
例子：

	mysql -uroot -pcloud -e "delete from cloud_front.sys_asynchrouns"

#### 2)、 使用here Document，适合复杂命令 
mysql -uusername -ppasswd << EOF

mysql cmd;

mysql cmd;
...

EOF

例子：

	mysql -uroot -pcloud <<EOF
	use cloud;
	CREATE TABLE user (
		username char(30) not null,
		age int,
		sex char(1)
	);
	
	EOF
	
#### 3)、使用< 重定向脚本 
	mysql -uusername -ppasswd < test.sql

