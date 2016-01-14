## VETH Device

### 1. 什么是Veth 设备
 VETH( Virtual Ethernet): 虚拟网卡,它的作用是反转通讯数据的方向，
 需要发送的数据会被转换成需要收到的数据重新送入内核网络层进行处理，从而间接的完成数据的注入
 
 VETH 设备总是成对出现，送到一端请求发送的数据总是从另一端以请求接受的形式出现。该设备不能被用户程序直接操作，但使用起来比较简单。
 创建并配置正确后，向其一端输入数据，VETH 会改变数据的方向并将其送入内核网络核心，完成数据的注入。在另一端能读到此数据。
 
 
### 2. 创建 VETH 设备：
```
  ip link add  veth0 type veth peer name veth1
  ip link delete veth0 type veth 
```

### 3. 使用 VETH 连接网桥(Linux Bridge, OpenVswitch) 
有两个网卡 eth0 eth1

#### 1. Linux Bridge
```
  #create bridge
  brctl addbr br0
  brctl addif br0 eth0
  brctl addbr br1
  brctl addif br1 eth1
  ip link add veth0 type veth peer name veth1 #create a peer Veth device
  
  brctl addif br0 veth0
  brctl addif br1 veth1
```

#### 2. OpenVswitch
```
  ovs-vsctl add-br br0
  ovs-vsctl add-port br0 eth0
  ovs-vsctl add-br br1
  ovs-vsctl add-port br1 eth1
  ip link add veth0 type veth peer name veth1
  ovs-vsctl add-port br0 veth0
  ovs-vsctl add-port br1 veth1
  
```
