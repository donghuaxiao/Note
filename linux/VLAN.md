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
在Linux 中，可以使用 vconfig 命令来创建 vlan

```
  vconfig add eth0 5 
```
这个命令会创建yig eth0.5 的子设备
配置 eth0.5: 可以使用 ifconfig 或 ip 命令各eth0.5 配置ip, 还可以通过创建 ifcfg-eth0.5 的配置文件来配置IP信息。

```
  ifconfig eth0.5 192.168.1.100 netmask 255.255.255.0 broadcast 192.168.1.255 up
```

获取 eth0.5 的详细信息：

```
  cat /proc/net/vlan/eth0.5
```

删除 vlan:

```
  ifconfig eth0.5 down
  vconfig rem eth0.5
```
####3. 使用ip 命令创建 VLAN
创建VLAN

```
# ip link add link eth0 name eth0.5 type vlan id 5
# ip link
# ip -d link show eth0.5
```

配置VLAN:

```
# ip addr add 192.168.1.200/24 brd 192.168.1.255 dev eth0.5
# ip link set dev eth0.5 up
```

删除VLAN:

```
# ip link set dev eth0.5 down
# ip link delete eth0.5
```

###3 Debian 和 ubuntu　配置 VLAN

编辑 interface 配置文件：sudo vi /etc/network/interfaces

```
auto eth0.5
iface eth0.5 inet static
    address 192.168.1.200
    netmask 255.255.255.0
    vlan-raw-device eth0
```
