### 爬虫安装各种依赖包

- 安装urlib(好像python自带有)
- 安装`requests`
- 安装`selenium`,有些界面是通过JS渲染的,通过`selenium`爬取js渲染后的网页,具体步骤如下:

```
pip install selenium
from selenium import webdriver
下载2.28的chromedriver包,如果包不可以,那么换一下.将chromedriver.exe复制到scripts目录下
driver = webdriver.Chorme() //弹出一个chrome窗口
driver.get("http://www.baidu.com")  //在弹出窗口里面出现百度界面
driver.page_source  //打印出网页源代码
```

- 安装`phantomjs`

```
去官网下载
与chromedriver不一样的是这个不会弹出界面来
下载好phantomjs后将bin目录配置到path中
然后可以在cmd中输入phantomjs
此时可以写js代码:console.log("aa")
在python中的用法有区别的地方在于: driver = webdriver.PhantomJS() 	
```

- 安装lxml(用来解析网页的)

```
pip install lxml
```

- 安装`beautifulsoup4`  (网页解析库, 依赖于lxml,所以应先安装lxml)

```
pip install beautifulsoup4
from bs4 import BeautifulSoup
soup = BeautifulSoup("<html></html>", "lxml")  
```

- 安装`pyquery` (网页解析库,和jquery语法相似)

```
 pip install pyquery
>>> from pyquery import PyQuery as pq
>>> doc  = pq("<html>hello</html>")
>>> result  = doc('html').text()
>>> result
'hello'
>>>
```

- 安装`pymysql` (python3操作mysql的库)

```
pip install pymysql
import pymysql 
>>> conn = pymysql.connect(host='localhost', user='root', password='123456', port=3306,db='my_mooc', charset='utf8')
>>> cursor = conn.cursor()
>>> cursor.execute('select * from users_userprofile')
2
>>> cursor.fetchone()
(1, 'pbkdf2_sha256$24000$HGqFgZqO87GD$QMtdWll2Al4ENsmxNWYxJbpf2z6kKuNeaQpGzsYfyu0=', datetime.datetime(2018, 4, 27, 23, 9, 26, 128719), 1, 'root', '韩卓', '韩', '1@1.com', 1, 1, datetime.datetime(2018, 3, 22, 22, 56), '云飞扬', datetime.date(1997, 5, 16), 'male', 'image/2018/04/1-130425101I6-50.jpg', '是否是', '13765903164', '篮球')
>>>
```

- 安装`pymongo` 以及安装`MongoDB`

```
pip install pymongo //安装之前首先安装MongoDB
安装MongoDB过程如下:
	1. 去官网下载MongoDB
	2. 解压安装
	3. 建立一个和bin目录同级的data文件夹,用来存储MongoDB的数据
	4. 在data文件夹下新建一个db文件夹,用来存储MongoDB的数据和配置
	5. 进入bin目录,右键-->"在此处打开命令窗口" -->在窗口内输入mongod --dbpath 你的db文件夹的路径,	   如果出错将mongod改为.\mongod
	6. 在浏览器中输入localhost:27017验证MongoDB是否启用成功
	7.配置MongoDB服务
		I: 新建一个和db文件夹同级的logs文件夹,用来存储MongoDB的日志信息,并在logs文件夹下新建一个
		   mongo.log日志文件 
		II: 右键管理员进入cmd, 在bin目录下敲入命令-->mongod --bind_ip 0.0.0.0 --logpath 				mongo.log的路径 --logappend --dbpath db文件夹的路径 --port 			          			  27017 --serviceName "MongoDB" --serviceDisplayName "MongoDB"  --install
	8. 下载可视化界面-->robomongo
	
用pymongo操作MongoDB
	import pymongo
	client = pymongo.MongoClient('localhost')
	db = client['newtestdb']
	db['table'].insert({'name': 'hello'{)
	db['table'].find_one(({'name': 'hello'}))
```

- 安装Redis

```
在安装Redis库之前首先要安装Redis这个镜像
redis下载地址:https://github.com/MicrosoftArchive/redis/releases
redis可视化工具下载地址: https://redisdesktop.com/download

pip install redis
>>> import redis
>>> r = redis.Redis('localhost', 6379)
>>> r.set('name', 'hanzhuo')
True
>>> r.get('name')
b'hanzhuo'
>>>
```

- 安装`flask`

```
pip install flask
```

- 安装django

```
pip install flask
```

- 安装`jupyter`  , 强大的记事本,可以调试,可以编辑等等

```
pip install jupyter
此时jupyter已经被加入到环境变量中去了(因为jupyter.exe在scripts)文件夹下
在命令行下输入 jupyter notebook会弹出一个浏览器,可以在里面编写代码和一些markdown格式的文本,使用ctrl+回车执行代码,使用b键新添加一行,其中使用的解释器就是你所安装的python版本的解释器
```

###	Urllib库的使用

- urlopen

```
urllib.request.urlopen(url, data=None, [timeout,]*, cafile=None, capath=None, cadefault=False, context=None)

url:请求网站的url
data:模拟post时所提交的数据
timeout:在timeout的时间内响应
```

- 参数详解

  - url

  ```python 
  import urllib.request

  response = urllib.request.urlopen("http://www.baidu.com")
  print(response.read().decode('utf-8'))

  read方法:读取响应体的内容,响应体是字节型的数据,调用decode给数据编码
  ```

  - data

  ```python
  import urllib.request
  import urllib.parse

  # bytes类型的数据,http://httpbin.org用于测试http请求的一个网站
  data = bytes(urllib.parse.urlencode({"world": "hello"}), encoding='utf8') 
  response = urllib.request.urlopen("http://httpbin.org/post", data=data)
  print(response.read()) 
  ```

  - timeout

  ```python 
  # __author__ = 'Administrator'
  # __date__ = 2018/5/5 05:35
  import urllib.request
  import urllib.parse
  import urllib.error
  import socket

  data = bytes(urllib.parse.urlencode({"world": "hello"}), encoding='utf8')
  try:
      response = urllib.request.urlopen("http://httpbin.org/post", data=data, timeout=0.1)
      print(response.read())
  except urllib.error.URLError as e:
      if isinstance(e.reason, socket.timeout):
          print("TIME OUT")
  ```

  - 响应,以`timeout`参数的例子加以说明

  ```python 
  将timeout参数改为1,让其可以正常响应
  print(type(response))  # <class 'http.client.HTTPResponse'>
  print(response.status) # 200
  print(response.getheaders()) #获取头部信息 
  [('Connection', 'close'), ('Server', 'gunicorn/19.7.1'), ('Date', 'Sat, 05 May 2018 09:50:39 GMT'), ('Content-Type', 'application/json'), ('Access-Control-Allow-Origin', '*'), ('Access-Control-Allow-Credentials', 'true'), ('X-Powered-By', 'Flask'), ('X-Processed-Time', '0'), ('Content-Length', '407'), ('Via', '1.1 vegur')]

  print(response.getheader('Server')) # 获取特定的头部--->gunicorn/19.7.1
  ```

- request

  - request可以发送请求头信息

```python
import urllib.request

request = urllib.request.Request("https://python.org")
response = urllib.request.urlopen(request)
print(response.read().decode('utf-8'))
```

```python
from urllib import request, parse

url = 'http://httpbin.org/post'
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64)',
    'Host': 'httpbin.org'
}
dict = {
    'name': 'hanzhuo'
}
# urllib库里面有个urlencode函数，可以把key-value这样的键值对转换成我们想要的格式，返回的是a=1&b=2这样的字符串
data = bytes(parse.urlencode(dict), encoding='utf-8')
req = request.Request(url=url, data=data, headers=headers, method='POST')
response = request.urlopen(req)
print(response.read().decode('utf-8'))
返回的信息:
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "name": "hanzhuo"
  }, 
  "headers": {
    "Accept-Encoding": "identity", 
    "Connection": "close", 
    "Content-Length": "12", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; WOW64)"
  }, 
  "json": null, 
  "origin": "58.16.41.24", 
  "url": "http://httpbin.org/post"
}

```

-  另外增加header的方法

```python
from urllib import request, parse

url = 'http://httpbin.org/post'
dict = {
    'name': 'hanzhuo'
}
data = bytes(parse.urlencode(dict), encoding='utf-8')
req = request.Request(url=url, data=data, method='POST')
req.add_header('User-Agent', 'Mozilla/5.0 (Windows NT 10.0; WOW64)')
response = request.urlopen(req)
print(response.read().decode('utf-8'))

```

- `Handler`代理
  - 使用不同的ip代理, 伪造多个地点请求访问服务器, 以免爬虫被封

```python
import urllib.request

# 使用代理这些ip才能使用
proxy_handler = urllib.request.ProxyHandler({
    'http': 'http://127.0.0.1:9743',
    'https': 'https://127.0.0.1:9743'
})
opener = urllib.request.build_opener(proxy_handler)
response = opener.open('http://www/baidu.com')
print(response.read())
```

- 使用`cookie`

```
import http.cookiejar, urllib.request

 #声明一个CookieJar对象来保存cookie
cookie = http.cookiejar.CookieJar()
#创建cookie处理器
handler = urllib.request.HTTPCookieProcessor(cookie)
  #构建opener
opener = urllib.request.build_opener(handler)
#创建请求
response = opener.open('http://www.baidu.com')
for item in cookie:
	print(item.name + '=' + item.value)
	
	
BAIDUID=C42975547EC74483CE755B1E51DBC423:FG=1
BIDUPSID=C42975547EC74483CE755B1E51DBC423
H_PS_PSSID=1459_21081_22075
PSTM=1525520795
BDSVRTM=0
BD_HOME=0
```

- 将`cookie`信息写入文件

```python
import http.cookiejar, urllib.request

#设置保存cookie的文件, 会自己创建
filename = 'G:\developemnt environment\PythonEnvironment\pythonEnvList\webPaChong\media\cookie.txt'
cookie = http.cookiejar.MozillaCookieJar(filename)

handler = urllib.request.HTTPCookieProcessor(cookie)

opener = urllib.request.build_opener(handler)

respose = opener.open('http://www.baidu.com')

#ignore_discard的意思是即使cookies将被丢弃也将它保存下来
#ignore_expires的意思是如果在该文件中cookies已经存在，则覆盖原文件写入
cookie.save(ignore_discard=True, ignore_expires=True)
```

- `LWP`格式保存cookie

```
import http.cookiejar,  urllib.request
filename = 'G:\developemnt environment\PythonEnvironment\pythonEnvList\webPaChong\media\cookie.txt'
# LWP格式
cookie = http.cookiejar.LWPCookieJar(filename)
handler = urllib.request.HTTPCookieProcessor(cookie)
opener = urllib.request.build_opener(handler)
response = opener.open('http://www.baidu.com')
cookie.save(ignore_discard=True, ignore_expires=True)
```

- 读取`cookie`	文件

```python 
import http.cookiejar,  urllib.request
filename = 'G:\developemnt environment\PythonEnvironment\pythonEnvList\webPaChong\media\cookie.txt'
cookie = http.cookiejar.LWPCookieJar()
#从文件中的读取cookie内容到变量
cookie.load(filename, ignore_discard=True, ignore_expires=True)
 #打印cookie内容,证明获取cookie成功
for item in cookie:
    print('name:' + item.name + '-value:' + item.value)
handler = urllib.request.HTTPCookieProcessor(cookie)
#利用获取到的cookie创建一个opener
opener = urllib.request.build_opener(handler)
response = opener.open('http://www.baidu.com')
print(response.read())

```

- 异常处理

```python
from urllib import request, error
try:
    response = request.urlopen('http://hanzhuo.com/index.htm')
except error.URLError as e:
    print("URL错误{0}".format(e.reason))


```

```python
from urllib import request, error
try:
    response = request.urlopen('http://hanzhuo.com/index.htm')
except error.HTTPError as e:
    print(e.reason, e.code, e.headers, sep='\n')

except error.URLError as e:
    print("URL错误{0}".format(e.reason))


```

```python
from urllib import request, error
import socket

try:
    response = request.urlopen('http://www.baidu.com', timeout=0.01)
except error.URLError as e:
    print(type(e.reason))  # <class 'socket.timeout'>
    if isinstance(e.reason, socket.timeout):
        print('time out')   # time out


```

- `url`解析

```
urllib.parse.urlparse(urlstring, scheme='', allow_fragments=True)
```

​	- 路径解析

```python
from urllib.parse import urlparse

result = urlparse('http://www.baidu.com/index.html;user?id=5#comment')
print(type(result), result)  # <class 'urllib.parse.ParseResult'> ParseResult
# (scheme='http', netloc='www.baidu.com', path='/index.html', params='user', query='id=5', fragment='comment')

```

​	- 协议类型

```python
from urllib.parse import urlparse

#如果链接为http://www.baidu.com/index.html时,scheme='https'无效, 默认为链接中的http
result = urlparse('www.baidu.com/index.html;user?id=5#comment', scheme='https')

print(type(result), result)  # <class 'urllib.parse.ParseResult'> ParseResult

# (scheme='https', netloc='', path='www.baidu.com/index.html', params='user', query='id=5', fragment='comment')
```

- `urlunparse`拼接地址

```python
from urllib.parse import urlunparse

data = ['http', 'www.baidu.com', 'index.html', 'user', 'a=5', 'comment']
print(urlunparse(data))  # # (scheme='https', netloc='', path='www.baidu.com/index.html', params='user', query='id=5', fragment='comment')
```

- `urljoin` 
- `urlunparse`

```python
from urllib.parse import urlencode

params = {
    'name': 'hanzhuo',
    'age': '21'
}
base_url = 'http://www.baidu.com?'
url = base_url+urlencode(params)
print(url)  # http://www.baidu.com?name=hanzhuo&age=21


```

### BeautifulSoup库的使用

- 基本使用

```python
html = '''
<html lang="zh-cn"><head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>python—cookielib模块对cookies的操作 - eric-lu - 博客园</title>
<link type="text/css" rel="stylesheet" href="/bundles/blog-common.css?v=-hy83QNg62d4qYibixJzxMJkbf1P9fTBlqv7SK5zVL01">
<script async="" src="https://www.google-analytics.com/analytics.js"></script>
</head>
<body>
<a name="top"></a>

<!--done-->
<div id="home">
<div id="header">
<div id="blogTitle">
<a id="lnkBlogLogo" href="http://www.cnblogs.com/isuifeng/"><img id="blogLogo" 
src="/Skins/custom/images/logo.gif" alt="返回主页"></a>
'''
from bs4 import BeautifulSoup
soup = BeautifulSoup(html, 'lxml')
print(soup.prettify())  # 可以将没有闭合的标签自动补全
print(soup.title.string)  # python—cookielib模块对cookies的操作 - eric-lu - 博客园

```

- 标签选择器

```python
html = '''
<html lang="zh-cn"><head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>python—cookielib模块对cookies的操作 - eric-lu - 博客园</title>
<link type="text/css" rel="stylesheet" href="/bundles/blog-common.css?v=-hy83QNg62d4qYibixJzxMJkbf1P9fTBlqv7SK5zVL01">
<script async="" src="https://www.google-analytics.com/analytics.js"></script><script type="text/javascript" src="https://common.cnblogs.com/script/encoder.js"></script><script src="//common.cnblogs.com/scripts/jquery-2.2.0.min.js"></script>
<script type="text/javascript">var currentBlogApp = 'isuifeng', cb_enable_mathjax=false;var isLogined=true;</script>
<script src="/bundles/blog-common.js?v=d16NGD79qD3qnJt25hXDZ2sGoojamz2W5Rl4vT0CGVg1" type="text/javascript"></script>
</head>
<body>
<a name="top"></a>

<!--done-->
<div id="home">
<div id="header">
<div id="blogTitle">
<a id="lnkBlogLogo" href="http://www.cnblogs.com/isuifeng/"><img id="blogLogo" 
src="/Skins/custom/images/logo.gif" alt="返回主页"></a>
'''
from bs4 import BeautifulSoup
soup = BeautifulSoup(html, 'lxml')
print(soup.prettify())  # 可以将没有闭合的标签自动补全
print(soup.title)  # <title>python—cookielib模块对cookies的操作 - eric-lu - 博客园</title>
print(type(soup.title))  # <class 'bs4.element.Tag'>
print(soup.script)  # <script async="" src="https://www.google-analytics.com/analytics.js"></script>,当有多个script标签时, 只会返回第一个出现的标签
print(soup.div)  # 出现<div id="home">标签包裹的所有东西
print(soup.div.string)  # None
 
```

- 获取名称

```python
print(soup.div.name)  # div
```

- 获取属性

```python
print(soup.script.attrs['src'])  # https://www.google-analytics.com/analytics.js
print(soup.script['src'])  # https://www.google-analytics.com/analytics.js
```

- 嵌套选择

```
print(soup.head.title.string)  # python—cookielib模块对cookies的操作 - eric-lu - 博客园
```

- 子节点和子孙节点

```python
print(soup.div.contents) # 以列表的形式返回, 换行符会作为其中一个元素

['\n', <div id="header"><div id="blogTitle">
<a href="http://www.cnblogs.com/isuifeng/" id="lnkBlogLogo"><img alt="返回主页" id="blogLogo" src="/Skins/custom/images/logo.gif"/></a>
</div></div>]

print(soup.div.contents[1].contents)
['\n', <div id="blogTitle">
<a href="http://www.cnblogs.com/isuifeng/" id="lnkBlogLogo"><img alt="返回主页" id="blogLogo" src="/Skins/custom/images/logo.gif"/></a>
</div>]

----使用children
print(soup.div.children)  # <list_iterator object at 0x05431A30> 迭代器
for i, child in enumerate(soup.div.children):
    print(i, child)
'''
0 

1 <div id="header">
<div id="blogTitle">
<a href="http://www.cnblogs.com/isuifeng/" id="lnkBlogLogo"><img alt="返回主页" id="blogLogo" src="/Skins/custom/images/logo.gif"/></a>
</div></div>
'''
空白行表示换行符


----使用descendants
print(soup.div.descendants)  # <generator object descendants at 0x05BF2B70> 迭代器
# 会将所有的子节点和孙节点一起输出
for i, child in enumerate(soup.div.descendants):
    print(i, child)

'''
0 

1 <div id="header">
<div id="blogTitle">
<a href="http://www.cnblogs.com/isuifeng/" id="lnkBlogLogo"><img alt="返回主页" id="blogLogo" src="/Skins/custom/images/logo.gif"/></a>
</div></div>
2 

3 <div id="blogTitle">
<a href="http://www.cnblogs.com/isuifeng/" id="lnkBlogLogo"><img alt="返回主页" id="blogLogo" src="/Skins/custom/images/logo.gif"/></a>
</div>
4 

5 <a href="http://www.cnblogs.com/isuifeng/" id="lnkBlogLogo"><img alt="返回主页" id="blogLogo" src="/Skins/custom/images/logo.gif"/></a>
6 <img alt="返回主页" id="blogLogo" src="/Skins/custom/images/logo.gif"/>
7 


'''
```

- 父节点

```
---获取单个父节点
print(soup.a.parent)
--获取所有的父节点
pring(soup.a.parents)
```

- 兄弟节点

```
print(list(enumerate(soup.a.next_siblings)))  # 获取找到的a标签之后的所有的兄弟节点, 并不是只找到一个
print(list(enumerate(soup.a.previous_siblings)))  # 获取找到的a标签之前的所有的兄弟节点, 并不是只找到一个
```

- 标准选择器
  - `find_all`

```python 
html = '''
<html lang="zh-cn">
<head>
<meta charset="utf-8">
</head>
<body>
    <ul class='list' id='list-1'>
        <li>Foo</li>
        <li>Foodf</li>
        <li>Fo</li>
        <li>dfoo</li>
    </ul>
    <ul class='list list-small' id='list-2'>
        <li>Bar</li>
        <li>Foo</li>
        <li>Fodfgo</li>
        <li>Fdsoo</li>
    </ul>
'''
from bs4 import BeautifulSoup
soup = BeautifulSoup(html, 'lxml')
print(soup.find_all('ul'))
for ul in soup.find_all('ul'):
    print(ul.find_all('li'))
    
[<ul class="list" id="list-1">
<li>Foo</li>
<li>Foodf</li>
<li>Fo</li>
<li>dfoo</li>
</ul>, <ul class="list list-small" id="list-2">
<li>Bar</li>
<li>Foo</li>
<li>Fodfgo</li>
<li>Fdsoo</li>
</ul>]


[<li>Foo</li>, <li>Foodf</li>, <li>Fo</li>, <li>dfoo</li>]
[<li>Bar</li>, <li>Foo</li>, <li>Fodfgo</li>, <li>Fdsoo</li>]
```

- `attrs`

```python
print(soup.find_all(attrs={'id': 'list-1'}))
'''
[<ul class="list" id="list-1">
<li>Foo</li>
<li>Foodf</li>
<li>Fo</li>
<li>dfoo</li>
</ul>]
'''

----对于特殊的属性的处理方法
print(soup.find_all(id='list-1'))
print(soup.find_all(class_='element'))  # 选择class为element的标签元素

---通过文本内容获取标签
print(soup.find_all(text='Foo'))  # 以列表的结果返回

```

- find方法
- css选择器

```
print(soup.select('.panel .panel-heading'))  
print('ul li)  # 标签
print('#list-2') # id

```

- 获取子类的所有文本内容`get_text()`

```python
html = '''
<html lang="zh-cn">
<head>
<meta charset="utf-8">
</head>
<body>
    <ul class='list' id='list-1'>
        <li>Foo</li>
        <li>Foodf</li>
        <li>Fo</li>
        <li>dfoo</li>
        sdfsd
        sdfd
    </ul>
    <ul class='list list-small' id='list-2'>
        <li>Bar</li>
        <li>Foo</li>
        <li>Fodfgo</li>
        <li>Fdsoo</li>
    </ul>
'''
from bs4 import BeautifulSoup
soup = BeautifulSoup(html, 'lxml')
for ul in soup.find_all(attrs={'id': 'list-1'}):
    print(ul)
	print(ul.get_text())

'''
<ul class="list" id="list-1">
<li>Foo</li>
<li>Foodf</li>
<li>Fo</li>
<li>dfoo</li>
        sdfsd
        sdfd
    </ul>
---所有子标签的文本内容
Foo
Foodf
Fo
dfoo
        sdfsd
        sdfd
    

'''

```

### pyquery库

- 字符串初始化

```python
html = '''
<html lang="zh-cn">
<head>
<meta charset="utf-8">
</head>
<body>
    <ul class='list' id='list-1'>
        <li>Foo</li>
        <li>Foodf</li>
        <li>Fo</li>
        <li>dfoo</li>
        sdfsd
        sdfd
    </ul>
    <ul class='list list-small' id='list-2'>
        <li>Bar</li>
        <li>Foo</li>
        <li>Fodfgo</li>
        <li>Fdsoo</li>
        
    </ul>
'''
from pyquery import PyQuery as pq
doc = pq(html)
print(doc('li'))

'''
<li>Foo</li>
        <li>Foodf</li>
        <li>Fo</li>
        <li>dfoo</li>
        sdfsd
        sdfd
    <li>Bar</li>
        <li>Foo</li>
        <li>Fodfgo</li>
        <li>Fdsoo</li>
'''
```

- `url`初始化

```python
doc = pq(url='http://www.baidu.com')
print(doc('head'))
```

- 文件初始化

```python
doc = pq(filename='dome.html')
print(doc('li'))
```

- 基本css选择器

```
print(doc('#container .list li'))
```

- 查找元素

```
items.find('li')  # 找到items下的所有li标签

items.children()  # 找到items标签下的直接子元素
items.children('.active')  # 带有选择器

items.parent()
items.parents()

items.siblings()  # 获取所有的兄弟元素
items.siblings('.active')


```

- 遍历

```python
html = '''
<html lang="zh-cn">
<head>
<meta charset="utf-8">
</head>
<body>
    <ul class='list' id='list-1'>
        <li>Foo</li>
        <li>Foodf</li>
        <li>Fo</li>
        <li>dfoo</li>
    </ul>
    <ul class='list list-small' id='list-2'>
        <li>Bar</li>
        <li>Foo</li>
        <li>Fodfgo</li>
        <li>Fdsoo</li>
        
    </ul>
'''
from pyquery import PyQuery as pq
doc = pq(html)
li_list = doc('li').items()
print(type(li_list))  # <class 'generator'>
for li in li_list:
    print(li)

'''
<li>Foo</li>
        
<li>Foodf</li>
        
<li>Fo</li>
        
<li>dfoo</li>
    
<li>Bar</li>
        
<li>Foo</li>
        
<li>Fodfgo</li>
'''

```

- 获取信息

```
----获取属性
print(a.attr('href'))
print(a.attr.href)

----获取文本
a.text()

----获取html
a.html()

```

- DOM操作

```
----addClass
li.addClass('active')

----removeClass
li.removeClass('active')

----attr
li.attr('name', 'link')

----css
li.css('font-size', '14px')

----remove
wrap.find('p').remvoe()

----其他DOM方法
http://pyquery.readthedocs.io/en/latest/api.html
```

- 伪类选择器

```
li = doc('li:first-child')
li = doc('li:last-child')
li = doc('li:nth-child(2)')
li = doc('li:gt(2)')   # 获取第二个以后的li标签
li = doc('li:nth-child(2n)')  # 获取偶数标签
li = doc('li:contains(second)')  # 获取包含'second'文本的li标签
```

更多css选择器可以查看[http://www.w3school.com.cn/css/index.asp](http://www.w3school.com.cn/css/index.asp)



### Selenium库

- 主要用来解决JAVASCRIPT渲染的问题
- 基本使用

````python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.wait import WebDriverWait


brower = webdriver.Chrome()
try:
    brower.get('https://www.baidu.com')
    input = brower.find_element_by_id('kw')
    input.send_keys('python')
    wait = WebDriverWait(brower, 1000)
    wait.until(EC.presence_of_element_located((By.ID, 'content_left')))
    print(brower.current_url)
    print(brower.get_cookies())
    print(brower.page_source)

finally:
    print('ok')
````



- 声明浏览器对象

```python
form selenium import webdirver

browser = webdriver.Chrome()
browser = webdriver.Firefox()
browser = webdriver.Edge()
browser = webdriver.PhantomJS()
browser = webdriver.Safari()

```

- 访问页面

```
from selenium import webdriver

browser = webdriver.Chrome()
browser.get('https://www.baidu.com')
print(browser.page_source)
browser.close()
```

- 查找元素

```python
from selenium import webdriver

browser = webdriver.Chrome()
browser.get('https://www.baidu.com')
input_first = browser.find_element_by_id('wrapper')  # 通过id
input_second = browser.find_element_by_css_selector('#wrapper')
input_third = browser.find_element_by_xpath('//*[@id="wrapper"]')
print(input_first, input_second, input_third)

'''
<selenium.webdriver.remote.webelement.WebElement (session="919822d1ba977bef04480df0e5cf077a", element="0.6614331157067188-1")> <selenium.webdriver.remote.webelement.WebElement (session="919822d1ba977bef04480df0e5cf077a", element="0.6614331157067188-1")> <selenium.webdriver.remote.webelement.WebElement (session="919822d1ba977bef04480df0e5cf077a", element="0.6614331157067188-1")>
'''
)
```

```

browser.find_element_by_class_name()
browser.find_element_by_name()
browser.find_element_by_link_text()
browser.find_element_by_partial_link_text()
browser.find_element_by_tag_name()
browser.find_element_by_css_selector()

```

- 通用的选择器

```
browser = find_element(By.ID, 'q')
```

- 多个元素

```
将element变为elements
find_elements(By.CSS_SELECTOR, 'servive')
```

- 元素交互操作

```python
from selenium import webdriver
import time

browser = webdriver.Chrome()
browser.get('https://www.taobao.com')
getTag = browser.find_element_by_id('q')  # 找到id为q的标签, 也就是淘宝的输入框
getTag.send_keys('iPhone')  # 在输入框中输入iPhone,如果这里报错, 请检查你的chromedriver是否和你的chrome版本一致
time.sleep(2)  # 等待两秒
getTag.clear()  # 清空搜索框
getTag.send_keys('iPad')  # 像搜索框中输入iPad
button = browser.find_element_by_class_name('btn-search')  # 找到搜索按钮
button.click()  # 点击搜索按钮,得到iPad搜索结果

```

更多操作:[http://selenium-python.readthedocs.io/api.html#module-selenium.webdriver.remote.webelement](http://selenium-python.readthedocs.io/api.html#module-selenium.webdriver.remote.webelement)

- 交互动作
  - 将动作附加到动作链中串行执行

```python
from selenium import webdriver
from selenium.webdriver import ActionChains

browser = webdriver.Chrome()
url = 'http://www.runoob.com/try/try.php?filename=jqueryui-api-droppable'
browser.get(url=url)
browser.switch_to.frame('iframeResult')  # 切换到frame标签
source = browser.find_element_by_css_selector('#draggable')
target = browser.find_element_by_css_selector('#droppable')

actions = ActionChains(browser)
actions.drag_and_drop(source, target)  # 从源拖放当目标
actions.perform()  # 执行

```

更多操作[http://selenium-python.readthedocs.io/api.html#module-selenium.webdriver.common.action_chains](http://selenium-python.readthedocs.io/api.html#module-selenium.webdriver.common.action_chains)

- 执行`JavaScript`

```python
from selenium import webdriver

browser = webdriver.Chrome()

browser.get('https://www.zhihu.com/explore')
browser.execute_script('window.scrollTo(0, document.body.scrollHeight)')  # 下拉到底部
browser.execute_script('alert("To Bottom")')  # 下拉到底部之后弹出一个消息
 
```

- 获取元素信息

```python
from selenium import webdriver

----获取属性
browser = webdriver.Chrome()
browser.get('https://www.zhihu.com/explore')
logo = browser.find_element_by_id('zh-top-link-logo')
print(logo.get_attribute('class'))  # 获取class的内容  zu-top-link-logo



----获取文本值
from selenium import webdriver

browser = webdriver.Chrome()

browser.get('https://www.zhihu.com/explore')
content = browser.find_element_by_class_name('zu-top-add-question')
print(content.text)  # 获取内容---->提问


----获取ID, 位置等
print(content.id)   # 获取返回的selenium对象的id-->0.26710575510805357-1
print(content.location)  # 该标签在浏览器当中的位置-->{'x': 759, 'y': 7}
print(content.tag_name)  # 标签名字-->button
print(content.size)  # 控件的大小-->{'height': 32, 'width': 66}

```

- `frame`之间的切换
  - 每一个`frame`都相当于独立的网页, 要想获取一个`frame`中的标签,就必须切换

```python
from selenium import webdriver
import time
from selenium.common.exceptions import NoSuchElementException

browser = webdriver.Chrome()
url = 'http://www.runoob.com/try/try.php?filename=jqueryui-api-droppable'
browser.get(url)
browser.switch_to.frame('iframeResult')
source = browser.find_element_by_css_selector('#draggable')
try:
    logo = browser.find_element_by_class_name('logo')
except NoSuchElementException:
    print("NO LOGO")

browser.switch_to.parent_frame()  # 切换到父frame
logo = browser.find_element_by_class_name('logo')
print(logo)
print(logo.text)  # RUNOOB.COM
'''
<selenium.webdriver.remote.webelement.WebElement (session="2ff03b970e10388e6e92f9962ded58f7", element="0.8612936230506747-2")>

'''

```

- 前进后退 

```
browser.get('http://www.baidu.com')
browser.get('http://www.taobao.com')
browser.get('http://www.zhihu.com')

browser.back()
browser.forward()
```

- `cookies`

```python
from selenium import webdriver

browser = webdriver.Chrome()
url = 'https://www.zhihu.com/explore'
browser.get(url)
print(browser.get_cookies())
browser.add_cookie({'name': 'name', 'domain': 'www.zhihu.com', 'value': 'germey'})
print(browser.get_cookies())
browser.delete_all_cookies()
print(browser.get_cookies())

```

- 选项卡

```python
from selenium import webdriver

browser = webdriver.Chrome()
url = 'https://www.zhihu.com/explore'
browser.get(url)  # 加载完成之后才能执行下面的代码
browser.execute_script('window.open()')  # 执行JS打开一个新的浏览器窗口
print(browser.window_handles)
browser.switch_to.window(browser.window_handles[1])  # 切换到第二个选项卡
browser.get("https://www.taobao.com")
browser.switch_to.window(browser.window_handles[0])  # 切换回第一个选项卡
browser.get('https://python.org')
```



### 使用requests库爬取今日头条街拍美图

- 配置文件

```
MONGO_URL = 'localhost'
MONGO_DB = 'toutiao'
MONGO_TABLE = 'toutiao'

# 起始页面
START_OFFSET = 0
END_OFFSET = 10
# 搜索关键词
KEYWORD = '街拍美图'
```

- 完整代码

```python
import json
from _md5 import md5
from multiprocessing.pool import Pool
from urllib.parse import urlencode

import re

import os
import pymongo
import requests
from bs4 import BeautifulSoup
from requests import RequestException

from mongoConfig import *

HEADERS = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36',
    'x-requested-with': 'XMLHttpRequest'
}

client = pymongo.MongoClient(MONGO_URL)
db = client[MONGO_DB]


def get_page_index(offset, keyword):
    data = {
        'offset': offset,
        'format': 'json',
        'keyword': keyword,
        'autoload': 'true',
        'count': 20,
        'cur_tab': 1,

    }
    url = 'https://www.toutiao.com/search_content/?' + urlencode(data)
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.text
            return None
    except RequestException:
        print('请求索引页出错')
        return None


def parse_page_index(html):
    # 将json字符串转换为字典对象
    data = json.loads(html)
    if data and 'data' in data.keys():
        for item in data['data']:
            # 使用item['article_url'] 当找不到键时,或报KeyError错误,而get方法会输出None
            yield item.get('article_url')


# 请求详情页
def get_page_detail(url):
    try:
        # 注意要加headers=HEADERS, 不然只能返回<html><head></head><body></body></html>
        response = requests.get(url, headers=HEADERS)
        if response.status_code == 200:
            return response.text
        return None
    except RequestException:
        print("请求详情页错误")
        return None


# 解析详情页
def parse_page_detail(detail_html, url):
    soup = BeautifulSoup(detail_html, 'lxml')
    title = soup.select('title')[0].get_text()
    pattern = re.compile('articleInfo.*?content:(.*?)groupId', re.S)
    image_group = re.findall(pattern, detail_html)
    # 获取真正的图片路径
    image_pattern = re.compile('http://(.*?)&quot; img_width')
    # 没有http://的url路径
    if image_group:
        image_url_group = re.findall(image_pattern, image_group[0])
        # 加一个http头并将其转为list
        image_url_group = list(map(format_image_url, image_url_group))
        return {
            'title': title,
            'url': url,
            'image': image_url_group
        }
    return None


# 格式化url,并下载
def format_image_url(url):
    url = 'http://' + url
    download_image(url)
    return url


def save_to_mongo(result):
    # 以url作为标识, 如果数据库中存在则更新, 不存在则插入
    for item in result:
        if item == 'url':
            is_exists_records = db[MONGO_TABLE].find({'url': result.get(item)})
            # 如果存在
            for records in is_exists_records:
                '''
                              my_set.update(
                             <query>,    #查询条件
                             <update>,    #update的对象和一些更新的操作符
                             {
                               upsert: <boolean>,    #如果不存在update的记录，是否插入
                               multi: <boolean>,        #可选，mongodb 默认是false,只更新找到的第一条记录
                               writeConcern: <document>    #可选，抛出异常的级别。
                             }
                          )
                              '''
                db[MONGO_TABLE].update({'url': item}, {'$set': result})
                # db[MONGO_TABLE].insert(result)
                print('更新到MongGo成功')

                return True
            else:
                db[MONGO_TABLE].insert(result)
                print('存储到MongGo成功')
                return True
    return False


def download_image(url):
    try:
        response = requests.get(url, headers=HEADERS)
        # 图片得到二进制信息
        content = response.content
        # 获取当前路径的上一个路径
        root_path = os.path.join(os.path.dirname(os.getcwd()), 'media')
        # md5获取32位的哈希字符串
        file_path = '{0}/images/{1}.{2}'.format(root_path, md5(content).hexdigest(), 'jpg')

        image_dir = '{0}/images'.format(root_path)
        # 如果不存在目录,则创建
        if not os.path.exists(image_dir):
            os.mkdir(image_dir)
        if not os.path.exists(file_path):
            # 以二进制流写入文件
            with open(file_path, 'wb') as f:
                f.write(content)
            print('图片保存成功:', url)
    except Exception as e:
        return None


def main(offset):
    html = get_page_index(offset, KEYWORD)
    url = parse_page_index(html)
    for url in parse_page_index(html):
        if url:
            detail_html = get_page_detail(url)
            image = parse_page_detail(detail_html, url)
            if image:
                save_to_mongo(image)


if __name__ == '__main__':
    # 偏移列表
    page = [i * 20 for i in range(START_OFFSET, END_OFFSET)]
    # 开启一个线程池
    pool = Pool()
    pool.map(main, page)

```

























