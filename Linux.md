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


### [Linux VLAN 配置](https://github.com/donghuaxiao/Note/blob/master/linux/VLAN.md)

### 使用rpm 查看一个软件安装了什么文件

```
  rpm -ql packageName
```

```
[root@localhost ~]# rpm -ql scsi-target-utils
/etc/rc.d/init.d/tgtd
/etc/sysconfig/tgtd
/etc/tgt/targets.conf
/usr/sbin/tgt-admin
/usr/sbin/tgt-setup-lun
/usr/sbin/tgtadm
/usr/sbin/tgtd
/usr/sbin/tgtimg
/usr/share/doc/scsi-target-utils-1.0.24
/usr/share/doc/scsi-target-utils-1.0.24/README
/usr/share/doc/scsi-target-utils-1.0.24/README.iscsi
/usr/share/doc/scsi-target-utils-1.0.24/README.iser
/usr/share/doc/scsi-target-utils-1.0.24/README.lu_configuration
/usr/share/doc/scsi-target-utils-1.0.24/README.mmc
/usr/share/man/man5/targets.conf.5.gz
/usr/share/man/man8/tgt-admin.8.gz
/usr/share/man/man8/tgt-setup-lun.8.gz
/usr/share/man/man8/tgtadm.8.gz
```
