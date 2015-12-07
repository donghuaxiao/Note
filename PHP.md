## PHP

### 1. 编译安装PHP
  PHP5.3 以上的版本已经自动打包了php-cgi , 安装完php后， 就可以直接运行 php-cgi.
  
  php-cgi : PHP的连接器， 当部署PHP 和 Nginx 时， Nginx 接受到php后缀的请求， 会把请求转发给 php-cgi, 由php 处理完成之后， 把结果转发的Nginx ,由 Nginx 返回的客户端。
