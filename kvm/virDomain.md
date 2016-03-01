## virDomain

### 1. 获取 virDomain 对象
```
  [ ] = conn.listAllDomains()
  [ ] = conn.listDefinedDomains()
  [ids] = conn.listDomainsID()
  domain = conn.lookupByID(id)
  domain = conn.lookupByName(name)
  domain = conn.lookupByUUID( uuid )
  domain = conn.lookupByUUIDString( uuidstr)
  
```

### 2. 获取 virDomain 的信息：
```
  domain.ID()  获取虚拟机的ID, 如果虚拟机停止了， 返回 -1
  domain.name() : 获取虚拟机的名称
  domain.UUID(): 获取虚拟机的UUID
  domain.UUIDString(): 获取虚拟机的 UUID 字符串
  domain.state(): 获取虚拟机的状态, 返回一个元组(5,0) state[0] 时虚拟机状态
  domaininfo = domain.info() : 返回一个元组[ time, maxmemory, memory, vcpu, state ], 返回[] 后，使用 id 访问, memory 的单位是KB
  domaininfo[1] 是 maxmemory
  domaininfo[2] 是 memory
  domaininfo[3] 是 vcpu
  
```

### 3. virtDomain 的 Event:
```
  libvirt.VIR_DOMAIN_EVENT_DEFINED	= 	0
  libvirt.VIR_DOMAIN_EVENT_UNDEFINED	= 	1
  libvirt.VIR_DOMAIN_EVENT_STARTED	= 	2
  libvirt.VIR_DOMAIN_EVENT_SUSPENDED	= 	3
  libvirt.VIR_DOMAIN_EVENT_RESUMED	= 	4
  libvirt.VIR_DOMAIN_EVENT_STOPPED	= 	5
  libvirt.VIR_DOMAIN_EVENT_SHUTDOWN	= 	6
  libvirt.VIR_DOMAIN_EVENT_PMSUSPENDED	= 	7
  libvirt.VIR_DOMAIN_EVENT_CRASHED	= 	8
  libvirt.VIR_DOMAIN_EVENT_LAST	= 	9
```
