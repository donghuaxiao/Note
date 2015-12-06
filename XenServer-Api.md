# XenServer API Interface

## Connect to XenServer

### connect to XenServer using local unix socket

	```
	import XenAPI

	session = XenAPI.local_xapi()
	session.login_with_password('root','')
	```

### Connect to XenServer remote
	```
	import XenAPI

	session = XenAPI.Session(url)
	try:
		session.login_with_password(user, password)
	except XenAPI.Failure as e:
		if e.details[0] = 'HOST_IS_SLAVE':
			master = e.details[1]
			url= "http://" + master
			session = XenAPI.Session(url)
			session.login_with_password(user,password)

	```

### 查看 XenAPI 的 远程调用方法
```
	import xmlrpclib
	
	server = xmlrpclib.ServerProxy(http://ip)
	methods = server.system.methods()
	with open('xen-api.txt', 'w') as f:
		for m in methods:
			f.write( m + '\n' )
```
这样就把XenAPI的方法写入文件： xen-api.txt 中
