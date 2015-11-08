# XenServer API Interface

## Connect to XenServer

### connect to XenServer using local unix socket
	'''
	import XenAPI

	session = XenAPI.local_xapi()
	session.login_with_password('root','')
	'''
	then the session is connect to XenServer, you can do other with the session object


### Connect to XenServer remote
	'''
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

	'''