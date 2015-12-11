## Linux VLAN

Linux VLAN 需要网卡支持8021q 协议支持，首先要检查是否加载 8021q 模块

### 1. 加载 8021q 模块

```
  //查看是否加载8021q 模块
  lsmod | grep 8021q

  //加载 8021q 模块
  modprobe 8021q
```

### 2. 创建VLAN

####1. CentOS/RHLE/Fedora 创建 VLAN
在网卡 eth0 上 创建一个VLAN ID 为5的VLAN

- 复制 eth0 的配置文件为 ifcfg-eth0.5
- 编辑 /etc/sysconfig/network-scripts/ifcfg-eth0.5

  ```
    # VLAN configuration for my eth0  with ID - 5 #
    DEVICE=eth0.5
    BOOTPROTO=none
    ONBOOT=yes
    IPADDR=192.168.1.5
    NETMASK=255.255.255.0
    USERCTL=no
    NETWORK=192.168.1.0
    VLAN=yes
  ```
注意： DEVICE= eth0.5, VLAN=yes

####2. 使用vconfig 命令创建 VLAN

####3. 使用ip 命令创建 VLAN
