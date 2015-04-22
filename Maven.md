<style type="text/css">
code {
	color:blue;
	font-size: 14px;
}
</style>


## Maven

### 1. 设置Maven 仓库的URL地址

#### 国内OSChina 提供的镜像
	<mirror>
      <id>CN</id>
      <name>OSChina Central</name>                                                                                                                       
      <url>http://maven.oschina.net/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>
    </mirror>

通过在 maven 主配置文件 settings.xml 中， mirros 节点下 配置上述的xml 片段， 就可以从OSChina的镜像上下载 jar 包， 而不会去从Maven　中央仓库去下载。

	<mirrors>
		<mirror>
	      <id>CN</id>
	      <name>OSChina Central</name>                                                                                                                       
	      <url>http://maven.oschina.net/content/groups/public/</url>
		  <mirrorOf>central</mirrorOf>
	    </mirror>
	</mirrors>

