Change TimeZone in CentOS
=========================

In Linux using /etc/locatetime configuration timezone, and configuration file of different timezone store in "/usr/share/zoneinfo" directory
When you want to change the timezone, just create a link of timezone's configuration file in /etc/ directory

- backup the old timezone configuration
```
  mv /etc/localtime /etc/localtime.bak
```
- create a link of the timezone configuration file
```
  ln -s /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime
```

- Check the timezone using "Date" command
