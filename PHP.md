## PHP

### 1. 编译安装PHP
  PHP5.3 以上的版本已经自动打包了php-cgi , 安装完php后， 就可以直接运行 php-cgi.
  
  php-cgi : PHP的连接器， 当部署PHP 和 Nginx 时， Nginx 接受到php后缀的请求， 会把请求转发给 php-cgi, 由php 处理完成之后， 把结果转发的Nginx ,由 Nginx 返回的客户端。

### 1. 安装依赖包：
yum install zlib zlib-devel  openssl openssl-devel libxml2 libxml2-devel libpng-

### 2. Nginx 配置支持 PHP
```
  location ~* \.php$ {
    fastcgi_index   index.php;
    fastcgi_pass    127.0.0.1:9000;
    include         fastcgi_params;
    fastcgi_param   SCRIPT_FILENAME    $document_root$fastcgi_script_name;
    fastcgi_param   SCRIPT_NAME        $fastcgi_script_name;
}
```
要注意php 放置的位置， $document_root 表示在 web 的根目录下
