# 使用 virsh console 连接 VM

##  连接 CentOS6 虚拟机  
要使用virsh console domainID 从 KVM主机连接Linux虚拟机控制台， 需要在虚拟机中进行如下配置：

#### 1. 添加 tty 到 /etc/securetty

添加 ttyS0 安全许可， 允许 root 用户登陆

```
  echo "ttyS0" >> /etc/securetty
```

#### 2. 配置 inittab
修改 grub.conf 让内核把输出定向至 ttyS0
```
  echo "S0:12345:respawn:/sbin/agetty ttyS0 115200" >> /etc/inittab
```

#### 3. /etc/grub.conf文件中为内核添加参数
在inittab里加一个ttyS0在系统启动时会生成一个ttyS0来接收内核的数据
```
  console=ttyS0
```

#### 4. reboot 虚拟机


## Guest of CentOS7 access text Console using virsh console Command
run the following command, and then reboot the guest virtual machine.
```
  grubby --update-kernel=ALL --args="console=ttyS0"
```
