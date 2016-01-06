## 使用 virsh console 连接 VM

###  要使用virsh console domainID 从 KVM主机连接Linux虚拟机控制台， 需要在虚拟机中进行如下配置：

#### 1. 添加 tty 到 /etc/securetty
```
  echo "ttyS0" >> /etc/securetty
```

#### 2. 配置 inittab

```
  echo "S0:12345:respawn:/sbin/agetty ttyS0 115200" >> /etc/inittab
```

#### 3. /etc/grub.conf文件中为内核添加参数

```
  console=ttyS0
```

#### 4. reboot 虚拟机
