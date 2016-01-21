## Control Nginx

### 1. start nginx
```
  nginx installed at /usr/local/ directory by default.
  
  nginx command has three arguments:
  
  -t : test
  -c : specify the nginx config file
  -V : print the version of nginx
  -V : print the version of nginx , compile arguments and compiler version
  
  
  start nginx:
  /usr/local/nginx/sbin/nginx
```

### 2. stop nginx:
nginx can be controlled with signals. The process ID of the master process is written bo the file
/usr/local/nginx/logs/nginx.pd by default. this name may be changed at configuration time, or in nginx.conf 
using the pid directive.

signals  nginx support:
TERM,  INT fast shutdown
QUIT   graceful shutdown
USR1   re-opening log files
USR2    upgrading an executable file
WINCH   graceful shutdown of worker processes
HUP      reaload configuration file
         graceful shutdown worker process 
         
shutdown nginx graceful:
```
  kill -QUIT `cat /usr/local/nginx/logs/nginx.pid`
```

fast shutdown nginx:
```
  kill -TERM `cat /usr/local/nginx/logs/nginx.pid`
```


shutdown nginx by force:
```
  kill -9 `cat /usr/local/nginx/logs/nginx.pid`
```

### 3. restart nginx
```
  kill -QUIT `cat /usr/local/nginx/logs/nginx.pid`
  /usr/local/nginx/sbin/nginx
```


