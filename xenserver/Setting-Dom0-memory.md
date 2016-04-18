## 设置和查看 XenServer Dom0 的内存
 XenServer Dom0 是XenServer 上的一个虚拟机， 安装XenServer 时， 自动安装的， 我们登录XenServer就是登录到 Dom0 上，
 Dom0 的系统的内存参数是在 /boot/extlinux.conf 中设置的, 配置参数为： dom0_mem=725M, max:752M
 
 ```
 label xe
  # XenServer
  kernel mboot.c32
  append /boot/xen.gz dom0_mem=752M,max:752M watchdog dom0_max_vcpus=1 crashkernel=128M@32M cpuid_mask_xsave_eax=0 console=vga 
  vga=mode-0x0311 --- /boot/vmlinuz-3.10-xen root=LABEL=root-qvcoinzp ro hpet=disable xencons=hvc console=hvc0 console=tty0 quiet 
  vga=785 splash --- /boot/initrd-3.10-xen.img

 ```
 修改 Dom0 的内存， 就是修改 dom0_mem 这个参数， 然后重启
 
在XenServer 中，提供了一个查看 和设置Dom0系统参数的命令 /opt/xensource/libexec/xen-cmdline

这个 xen-cmdline 就是解析和设置 /boot/extlinux.conf 这个配置文件

### 1. 查询Dom0 的 内存
```
/opt/xensource/libexec/xen-cmdline --get-xen dom0_mem
```

### 2. 设置 Dom0 的内存
```
  /opt/xensource/libexec/xen-cmdline --set-xen dom0_mem=1024M,max:1024M
```
 
 ### 3. 查询 Dom0 的 vCPU 个数
 ```
  /opt/xensource/libexec/xen-cmdline --get-xen dom0_max_vcpus
 ```
 ### 4. 设置 Dom0 的VCpu个数
 ```
  /opt/xensource/libexec/xen-cmdline --set-xen dom0_max_vcpus=2
 ```
 
