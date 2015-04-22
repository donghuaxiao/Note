<style type="text/css">
code {
	color: blue;
	font-size: 14px;
}
</style>
## Java

### 1. Tomcat 删除自带的应用
首先删除webapps目录的的应用目录， 然后在conf/Catalina/localhost目录下的应用配置文件 如： manager.xml



## JSP

### 1. EL 表达式 ！= null 和 not empty 的区别
${ test != null } : 用来判断 test 是否为null

${ not empty test } : 用来判断 test 是否为null 和 是否为空字符串


在request 中设置 request.setAttribute(test,  "     ");

	${ test != null ? "aaa" : "test is null"}  ===> "aaa"

	${ not empty test ? "bbb" : "test is empty"}  ====> "bbb"

To evluate empty A

* If A is null, return true
* Otherwise,if A is the empty string, then return true
* Otherwise, if A is an empty array, then return true
* Otherwise, if A is an empty Map, return true
* Otherwise, if A is an empty Collection, return true
* Otherwise, return false


${ str + str2 } : 在 EL表达式中， +  是算术运算符， 只能用来数字相加， 不能用来进行字符串连接。

如果 str 或 str2 位非数字， 会抛出 <font style="color:red">NumberFormatException</font>


### 2. jsp:include 指令
jsp:include 指令是把编译后的结果包含进来
#### 没有参数
	<jsp:include page="page-path"></jsp:include> 
要注意，没有参数的形式， 开始和结束标签要在同一行， 否则会报期望参数的异常

#### 带有参数
	<jsp:include page="">
		<jsp:param name="" value=""></jsp：param>
	</jsp:include>

### 3. jsp include 指令 <%@ include file="filt-path" %> 
jsp include 指令是包静态页面包含的本页当中



## Tomcat

### 1. Tomcat 环境变量设置

#### CATALINA_OPTS 设置

CATALINA_OPTS allows specification of additional options options for the java command that starts Tomcat.

设置调试信息

设置Tomcat 的内存

#### JAVA_OPTS 设置

设置启动和关闭 Tomcat 的 java 命令选项

注意：
	
	不要使用 JAVA_OPTS　来设置 Tomcat运行的内存， 因为 JAVA_OPTS 设置 启动和关闭 Tomcat 的 Java 命令的参数， 明显关闭 Tomcat 只需要很少的内存，应该使用 CATALINA_OPTS来设置 Tomcat 运行的内心

