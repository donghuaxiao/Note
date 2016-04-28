## CloudStack ##

### 1. CloudStack 模板 ###

#### CloudStack 模板下载路径 ####
http://cloudstack.apt-get.eu/， 该URL  包含了CloudStack 4.0开始的所有版本的rpm,deb安装包， 和各个版本的系统模板

* rpm安装包目录： rhel
* 系统模板目录：systemvm
* ubuntu安装包目录： ubuntu

### 2. CloudStack Debug
* debug management
  Add the following line in the file  /etc/cloudstack/management/tomcat6.conf

 	    CATALINA_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,address=8787,server=y,suspend=n"
    
* debug kvm-agent
    
	Edit /etc/init.d/cloudstack-agent file

    	DEBUG="-Xdebug -Xrunjdwp:transport=dt_socket,address=8787,server=y,suspend=n"
		JSVS -c "$CLASSPATH" 
		JSVC "${DEBUG}" -c "$CLASSPATH" 

* debug ssvm and cpvm Agent
