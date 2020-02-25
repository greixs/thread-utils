# thread-utils

simple interface class for web requests with threading 

Features
--------

- Support Pythong 3 and above 
- Customizable Thread Id
- Built in printing format (Info, Warning & Error) and normal Print including the time and thread ID
- Built in requests support (GET, POST, PUT) with common erros handling including Timeout & ConnectionError
- Included simple 2Captcha library
- Proxy parser from txt file
- Session creator with proxy support for Http and Socks5
- Session proxy changer

Install
-------

```
pip install frenox-thread-utils
```

Usage
-----

Create the custom thread. 
```
from thread_utils.threading import CustomThread
from thread_utils.session_handler import get_session

class Test(CustomThread):
	def __init__(self, _id):
		super(Test, self).__init__(_id)

	def run(self):
		self.s = get_session()
```

CustomThread have built in printing functions with more information than standard print
```python
	# self.p is the built in printer 
 
	self.p.info("this is info")
	self.p.warning("this is warning")
	self.p.error("this is erro")
```

getting proxy, for now it only supports txt file
```python
from thread_utils.session_handler import get_proxies

# example content of proxies.txt 
#
# 127.0.0.1:31337
# 127.0.0.1:31337:username:password

# if no params it will find proxies 
proxies = get_proxies()

# or use your own proxy file name
proxies = get_proxies=(path="./mkdir/newProxies.txt")

```

Initialize the session
```python
headers = {"accept": "*/*"}
proxy = "test@test:127.0.0.1:8888"
self.s = get_session(headers=headers, proxy=proxy)
```

Do some requests, it have the same parameters with the requests libary but with built in Timeout & ConnectionError handling
```python
self.get("https://github.com/greixs/thread-utils", timeout=30)
self.post("https://github.com/greixs/thread-utils", timeout=30)
self.put("https://github.com/greixs/thread-utils", timeout=30)
```

get proxies, it will parse the proxies <IP:port:user:pass> and save it in global "proxies" variable to be used in getting proxy method
```python
from thread_utils.session_handler import get_proxies, get_proxy
get_proxies() # it will be saved in global variable
print(get_proxy()) it will take the proxy from global variable

```

change proxy of a session
```python
from thread_utils.session_handler import change_proxy
s = change_proxy(s, "username:password@127.0.0.1:31337")
```

To-Do
-----

- add more features


Feedback
--------

This is my first ever public library so any feedback on fix or new feature will be very appreciated. To do so you can open a new thred in issue.


