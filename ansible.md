## Ansible

### 1. Ansible 是什么？
Ansible 是一个主机批量管理工具，
###2 . Ansible 的特点
Ansible 没有Agent, 不用再管理的主机上安装Agent, 直接通过ssh 进行命令
###3. Ansible 安装
#### 1. 使用yum 安装 ansible
  - 安装 epel 包, 在安装 ansible
  
  ```
    yum install epel-package
    yum install ansible
  ```
  
  - 使用 pip 安装
  
  ```
    pip install ansible
  ```
#### 2. 基本配置
  ansible 是使用 ssh 来执行命令的， 要配置 ssh 使用密钥连接
  在ansible 主机上 生成 sshkey, 再使用 ssh-copy-id 命令分发 sshkey
  假设有 kvmnode1, kvmnode2, kvmnode3三台主机，要使用ansible 来批量管理
  ```
    编辑 /etc/hosts
    192.168.10.142 kvmnode1.cloud.com kvmnode1
    192.168.10.143 kvmnode2.cloud.com kvmnode2
    192.168.10.144 kvmnode3.cloud.com kvmnode3
  ```
  
  分别执行：
  ```
    ssh-copy-id -i kvmnode1
    ssh-copy-id -i kvmnode2
    ssh-copy-id -i kvmnode3
  ```
  
#### 3. 配置ansible 操作组
  vim /etc/ansible/hosts
  
  ```
    [kvmnode]
    kvmnode1
    kvmnode2
    kvmnode3
  ```

### 4. 基本操作
####1. 被管理主机的连通性检测
```
  ansible kvmnode -m ping
```

####2. 执行shell 命令
使用 command 模块
```
  ansible kvmnode -m command -a "shell command"
```
-m command : 表示使用command 模块
-a : 表示使用参数
"shell command" ： 中的就是要执行的命令

使用 shell 模块： 执行命令， 执行 shell 脚本,
```
  ansible kvmnode -m shell -a "shell script | shell command"
```

注意： command 模块只能执行单个命令， 不能执行多个使用管道连接起来的命令。比如：
```
  rpm -qa | grep httpd
```
####3. 安装 软件

```
  ansible kvmnode -m yum -a "name=package state=latest"
```


####4. Service 模块
Service 模块用来启动， 停止， 重启 各种服务和启用服务开机自启动
参数：
- name : name of service
- state: started | stopped | restarted | reloaded(启动 | 停止 | 重启 | 重新加载)
- enabled: yes|no ( 开机自动|开机不启动) (chkconfig servicename on | off)

playbook example
```
  service: name=libvirtd state=started
```

CLI:
```
  ansible kvmnode -m service -a "name=libvirtd state=started"
```
