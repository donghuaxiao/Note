## TUN/TAP
#### 1. TUN/TAP 是什么？
TUN/TAP 是 Linux 虚拟网络设备, 用来为用户空间的程序提供发送和接受数据包的功能。

TUN(network TUNnel) 模拟一个3层设备，操作IP数据包， 用来作路由。 用来创建 VPN， 例如: openVpn 

TAP(network TAP) 模拟一个 link layer 设备，工作在数据链路层， 用来创建虚拟网桥。 在linux 中， 创建一个 tap 设备，添加到 网桥上， 可以使用该tap
设备连接虚拟机。

#### 2. TUN/TAP 的工作原理？

当创建一个 TUN/TAP 设备时， 可以在 /sys/class/net/目录下，看到该虚拟设备，创建后，默认的状态 Down 的， 可以通过 ifconfig 或 ip 命令
设置该设备 UP 状态。

用户程序怎样向虚拟网络设备发送和接受数据包？

在 linux 中，有一个字符设备文件： /dev/net/tun,  这个设备作为用户空间和内核空间数据交换的接口。 用户程序通过向这个字符设备读写
达到接受和发送数据。

系统中有多个TUN/TAP 设备, 怎样来区别这些设备？

 首先打开 /dev/net/tun 这个字符设备， 获取一个文件描述符fd, 通过 虚拟机网络设备的名称 和 fd 调用 ioctl把 虚拟设备和 /dev/net/tun关联起来，
 然后对这个fd 进行读写操作。
当内核将数据包发送到虚拟网络设备时，数据包被保存在设备相关的一个队 列中，直到用户空间程序通过打开的字符设备tun的描述符读取时，
它才会被拷贝到用户空间的缓冲区中，其效果就相当于，数据包直接发送到了用户空间。通过 系统调用write发送数据包时其原理与此类似。

#### 3. 创建/打开 虚拟网络设备代码

```
  int tun_alloc(char *dev, int flags) {

    struct ifreq ifr;
    int fd, err;
    char *clonedev = "/dev/net/tun";

    /* open the clone device */
    if( (fd = open(clonedev, O_RDWR)) < 0 ) {
      return fd;
    }

    /* preparation of the struct ifr, of type "struct ifreq" */
    memset(&ifr, 0, sizeof(ifr));

    ifr.ifr_flags = flags;   /* IFF_TUN or IFF_TAP, plus maybe IFF_NO_PI */

    if (*dev) {
      strncpy(ifr.ifr_name, dev, IFNAMSIZ);
    }

    /* try to create the device */
    if( (err = ioctl(fd, TUNSETIFF, (void *) &ifr)) < 0 ) {
      close(fd);
      return err;
    }

    strcpy(dev, ifr.ifr_name);
   return fd;
}
```

###  命令行创建 TUN/TAP 设备
```
Usage: ip tuntap { add | del } [ dev PHYS_DEV ] 
          [ mode { tun | tap } ] [ user USER ] [ group GROUP ]
          [ one_queue ] [ pi ] [ vnet_hdr ] [ multi_queue ]

Where: USER  := { STRING | NUMBER }
       GROUP := { STRING | NUMBER }

```

创建tap| tun 设备：
```
  ip tuntap add dev  tap0 mode tap
  ip tuntap add dev tun0 mode tun
```
删除 tap | tun 设备:
```
  ip tuntap del dev tap0 mode tap
  ip tuntap del dev tun0 mode tun
```

