### 函数

##### 1. 练习使用*args动态参数

- *arg的类型是一个元组

```python
def f(*args):
    print(args, type(args))

# 调用方法1
t = (1, 2, 3)
f(t)  # ((1, 2, 3),) <class 'tuple'>
li = [1, 2, 3]  
f(li)  # ([1, 2, 3],) <class 'tuple'>

# 调用方法2
f(*t) # (1, 2, 3) <class 'tuple'>
f(*l) # (1, 2, 3) <class 'tuple'>
```



##### 2.练习使用*arg动态参数

- **arg的类型是一个字典

```python
def f(**arg):
    print(arg, type(arg))
 
# 调用方法1
f(name='享学课堂', site='2xkt.com')
# {'name': '享学课堂', 'site': '2xkt.com'} <class 'dict'>
d = {'name':'享学课堂', 'site':'2xkt.com'}
f(k=d)
# {'k': {1: '享学课堂', 2: '2xkt.com'}} <class 'dict'>
 
# 调用方法2
f(**d)
# {'name': '享学课堂', 'site': '2xkt.com'} <class 'dict'>
```



##### 3. 将函数作为参数,实现函数回调

```python
def f1(f):
	f()
	
def f2():
	print("练习函数回调")

    
f1(f2)
```



##### 4.使用递归实现二分查找

- 打印出None的错误示范

```python
def binary_search(lst, find, low, high):
    mid = (low+high)//2
    if find == lst[mid]:
        return mid
    elif find > lst[mid]:
        low = mid
        binary_search(lst,find,low,high)
    else:
        high = mid
        binary_search(lst, find, low, high)


l = [1, 2, 3, 4, 5]
a = binary_search(l, 2, 0, 4)
print(a)
```

- 此时输出为None,为什么会这样?

  当我们最终查找到要寻找的数据时,此时会调用`return mid` 语句,但是由于该函数是递归的,所以此时实际上`return` 回去的只是上一个`binary_search` ,然后据需执行下面的代码,由于之后的代码并没有return语句,所以会导致返回的数据为None

- 正确的代码如下

```python
def binary_search(lst, find, low, high):
    mid = (low+high)//2
    if find == lst[mid]:
        return mid
    elif find > lst[mid]:
        low = mid
        return binary_search(lst,find,low,high)
    else:
        high = mid
        return binary_search(lst, find, low, high)


l = [1, 2, 3, 4, 5]
a = binary_search(l, 2, 0, 4)
print(a)
```

```python
# 1
```

### os模块相关方法

```python
os.getcwd()                 获取当前工作目录，即当前python脚本工作的目录路径
os.chdir("dirname")         改变当前脚本工作目录；相当于shell下cd
os.curdir                   返回当前目录: ('.')
os.pardir                   获取当前目录的父目录字符串名：('..')
os.makedirs('dir1/dir2')    可生成多层递归目录
os.removedirs('dirname1')   若目录为空，则删除，并递归到上一级目录，如若也为空，则删除，依此类推
os.mkdir('dirname')         生成单级目录；相当于shell中mkdir dirname
os.rmdir('dirname')         删除单级空目录，若目录不为空则无法删除，报错；相当于shell中rmdir dirname
os.listdir('dirname')       列出指定目录下的所有文件和子目录，包括隐藏文件，并以列表方式打印
os.remove()                 删除一个文件
os.rename("oldname","new")  重命名文件/目录
os.stat('path/filename')    获取文件/目录信息
os.sep                      操作系统特定的路径分隔符，win下为"\\",Linux下为"/"
os.linesep                  当前平台使用的行终止符，win下为"\t\n",Linux下为"\n"
os.pathsep                  用于分割文件路径的字符串
os.name                     字符串指示当前使用平台。win->'nt'; Linux->'posix'
os.system("bash command")   运行shell命令，直接显示,不能保存执行结果
os.popen("bash command").read()   运行shell命令,可以保存执行结果
os.environ                  获取系统环境变量
```

##### 1. os中的path模块的用法

- 首先导入:`from os import path`

1.`path.abspath`

```python
print(path.abspath("os_system.py"))
# G:\developemnt environment\PythonEnvironment\PtyhonStudyList\os_system.py
```

2.`path.split` 

- 将path分割成目录和文件名二元组返回

```python
print(path.split("G:\developemnt environment\PythonEnvironment\PtyhonStudyList\os_system.py"))
# ('G:\\developemnt environment\\PythonEnvironment\\PtyhonStudyList', 'os_system.py')
```

3.`path.dirname(path)` 

- 返回path的目录。其实就是os.path.split(path)的第一个元素

4.`path.basename(path)` 

- 返回path最后的文件名。如何path以／或\结尾，那么就会返回空值。即os.path.split(path)的第二个元素

5.`path.commonprefix(list)` 

- 返回list中，所有path共有的最长的路径。

```python
>>> os.path.commonprefix(['/home/td','/home/td/ff','/home/td/fff']) 
'/home/td' 
```

6.`path.exists(path)` 

- 如果path存在,返回True,否则返回False

7.`path.isfile`

- 如果path是一个存在的文件,返回True,否则返回False

8.`path.isdir`

- 如果path是一个存在的目录,则返回True,否则返回False

9.`path.join(path1[,path2[,...]])` 

- 将多个路径组合后返回，第一个绝对路径之前的参数将被忽略

```python
print(path.join("first","a","b","c"))  # first\a\b\c

print(path.join('windows\temp', 'c:\\', 'csv', 'test.csv') ) # 'c:\\csv\\test.csv' 

print(path.join("first","a:/","b/","c")) # a:/b/c
```

10.`path.splitext(path)` 

- 分离文件名与扩展名；默认返回(fname,fextension)元组，可做分片操作 

```python
path.splitext('c:\\csv\\test.csv') 
('c:\\csv\\test', '.csv') 
```

11.`path.getsize(path)`

- 返回path文件的大小(字节)

  ```
  print(path.getsize("os_system.py"))  # 390
  ```

12. `path.getatime(path)` 

- 返回path所指向的文件或者目录的最后存取时间

13. `path.getmtime(path)`

- 返回path所指向的文件或者目录的最后修改时间

14. `path.getctime(path)` 

- 返回文件创建时间

### 文件操作实例

##### 1.读取一个文件,过滤掉以#号开头的行

```python
f = open("abc.txt",encoding='utf-8')
```

- 方法一

```python
for line in f:
	if not line.startswidth("#"):
        print(line)
```

- 方法二

```python
while True:
    r = f.readline()
    if r:
        if not r.startswidth("#"):
            print(r)
    else:
        break
```

##### 2. 提示输入文件名称F和文件行N,读文件F的前N行

```python
f = input('请输入文件名称：')
n = int(input('请输入读取的行数：'))
f = open(f, encoding='utf-8')
while n > 0:
    r = f.readline()
    n-=1
```

### python异常处理

##### 1.assert断言

- 当assert函数中的表达式运算结果为False时,就会抛出一个AssertionError异常

```python
a = 100
assert(a == 101)
 
s = input('请输入你的年龄：')
age = int(s)
assert(age>0)
print(age)
```

##### 2.自定义异常

- 自定义异常需要两个步骤
  - 继承Exception
  - 重写init和str方法

```python
class MyException(Exception):
    def __init__(self, info):
        super().__init__(self)
        self.error_info = info

    def __str__(self):
        return "自定义异常" + self.error_info


a = 1
b = 2
try:
    if a < b:
        raise MyException("可以运行")
except MyException as my:
    print(my)
   
#  自定义异常可以运行
```



###  python面向对象

- python不支持方法重载



##### 1.python类方法,静态方法,实例方法

######  静态方法

- 使用@staticmethod标示,可以不用实例化,直接通过类名称调用
- 静态方法不能访问实例变量,也不能访问类变量,python没有静态变量

###### 实例方法

- 必须实例化才能调用

###### 类方法

- 使用@classmethod标示,但是第一个参数必须是类本身cls

##### 2. 实例

```python
class MyClass(object):
    def __init__(self, a):
        self.a = a
        print("这是对象初始化函数")

    def shi_li_method(self):
        print("我是实例方法")

    @staticmethod
        # 没有self
    def static_method():
        print("我是静态方法")

    @classmethod
    def class_method(cls):
        print("我是类方法")


clas = MyClass()  # 这是对象初始化函数
clas.class_method()  # 我是类方法
MyClass.class_method()  # 我是类方法
MyClass.static_method()  # 我是静态方法
# MyClass.shi_li_method()  # TypeError:
clas.shi_li_method()  # 我是实例方法

```

##### 3. 类属性和实例属性

###### 类属性

- 是在方法外面声明的属性,可以通过类名称或者实例名称访问

###### 实例属性

- 是在init方法中初始化的属性,必须实例化才能访问





```python
class Person(object):
    pid = 1
    name = 'tom'
    def __init__(self,name,age):
        self.name = name
        self.age = age
    def m(self):
        pass
 
p1 = Person('tom',20)
print(p1.name)
print(p1.age)
 
p2 = Person('kite',21)
print(p2.name)
print(p2.age)
 
 
Person.name = 'tom'
print(Person.name)
 
 
print(Person.pid)
p1 = Person()
print(p1.pid)
p2 = Person()
 
p1.pid = 100
Person.pid = 100
 
print(Person.pid)
print(p1.pid)
print(p2.pid)
```

##### 4. python的伪私有属性

- Python中要声明私有属性，需要在属性前加上双下划线（但是结尾处不能有双下划线），如：self.__a。然而这样的什么方式并不是真正私有，而是“伪私有”。
- Python的伪私有属性，实际是通过变量名压缩（mangling）来实现变量名局部化。变量名压缩的规则：在初始的变量名头部加上一个下划线，再加上类的名称，最后是初始变量名的名称。
- 执行以下代码来验证：

```python
class A(object):
    def __func(self):pass

if __name__ == '__main__':
    print(A.__dict__)
```

- 运行结果:

```python
{'__weakref__': <attribute '__weakref__' of 'A' objects>, '__module__': '__main__', '__doc__': None, '_A__func': <function A.__func at 0x10cfa037
8>, '__dict__': <attribute '__dict__' of 'A' objects>}
```

- 我们通过类的__dict__属性，将class A的所有属性打印出来，从打印的结果可以发现：原先定义的伪私有属性（方法）：__func 在__dict__中并不存在，取而代之的是_A_func这个方法，方法__func的变量名被压缩。
- 如此在外部调用class A的__func方法时，会提示无法找到。修改代码进行测试：

```python
class A(object):
    def __func(self):pass

if __name__ == '__main__':
    a = A()
    a.__func()
```

- 运行后出现异常，提示A没有属性__func，从而实现类似私有属性的功能。

```
AttributeError: 'A' object has no attribute '__func'
```

- 之所以说它是“伪私有”，是因为在了解伪私有变量的变量名压缩规则后，可以根据压缩规则进行调用。
- 再次修改代码进行验证：

```python
class A(object):
    def __func(self):print('Hello Python')

if __name__ == '__main__':
    a = A()
    a._A__func()
```

- 运行结果正常， 成功打印“Hello Python”字符串。

```
Hello Python
```

-  所以，Python的类并不存在正在的私有属性，通过双下划线实现的伪私有属性，本质上是对变量名进行压缩，使之无法直接在外部调用。

###### 为什么要使用伪私有属性

- 使用伪私有属性是为了避免在类树中，多个类赋值相同的属性引发冲突问题。
- 假设有两个类，C1 和 C2，他们都有相同的属性X。

```python
class C1():
    def meth1(self):
        self.x = 'Hello World'
    def meth2(self):
        print(self.x)
c1 = C1()
c1.meth1()
c1.meth2()
```

```python
class C2():
    def meth3(self):
        self.x = 'Hello Python'
    def meth4(self):
        print(self.x)
c2 = C2()
c2.meth3()
c2.meth4()
```

- 类C1和C2在单独调用时，输出结果没有问题，符合预期：调用meth2方法时，打印meth1的赋值结果；调用meth4方法时，打印meth3的赋值结果。

- 此时增加一个新的类C3，继承自C1、C2（多重继承）：

  ```python
  class C1():
      def meth1(self):
          self.x = 'Hello World'
      def meth2(self):
          print(self.x)

  class C2():
      def meth3(self):
          self.x = 'Hello Python'
      def meth4(self):
          print(self.x)

  class C3(C1, C2):
      pass

  c3 = C3()
  c3.meth1()
  c3.meth3()
  c3.meth2()
  c3.meth4()
  ```

- 从运行结果可以看出，每次 print(self.x)的内容，取决于 self.x 最后一次赋值的内容。

  ```
  Hello Python
  Hello Python
  ```

- 在示例代码中，先调用 c3.meth1() 进行赋值，self.x的值为“Hello World”，再调用 c3.meth3() 进行赋值时，self.x的值被覆盖，目前的值为“Hello Python”。

- 后续再调用c3.meth2()打印self.x的值时，实际上打印的是最后一次赋值结果，这在有些情况下跟类的设计初衷是相违背的：在C1中，meth2希望打印的是在meth1中赋值的内容：“Hello World”。

- 在使用伪私有属性后可以解决变量名self.x相互覆盖的问题（因为self.__x 被压缩成了 self._C1__x 和 self._C2__x，变量名不同，不会互相覆盖）：

```python
class C1():
    def meth1(self):
        self.__x = 'Hello World'
    def meth2(self):
        print(self.__x)

class C2():
    def meth3(self):
        self.__x = 'Hello Python'
    def meth4(self):
        print(self.__x)

class C3(C1, C2):
    pass

c3 = C3()
c3.meth1()
c3.meth3()
c3.meth2()
c3.meth4()
```

- 私有的属性、方法，不会被子类继承，也不能被访问
- 可以通过调用继承的父类的共有方法，间接的访问父类的私有方法、属性

##### 4. 抽象类

```python
import abc
class USB(metaclass=abc.ABCMeta):
    @abc.abstractmethod
    def read(self):
        pass

    def write(self):
        pass
```

##### 5. 接口

- 接口里面没有任何实现的方法,所有的方法都是抽象方法

```python
import abc
class USB(metaclass = abc.ABCMeta):
    @abc.abstractmethod
    def read (self):
        pass
    def write(self):
        pass
    
class Computer(USB):
    def read(self):
        print('from computer read...')
    def write(self):
        print('write to computer...')
 
c = Computer()
c.read()
c.write()
```

##### 6. python类实例的内建函数

###### `issubclass(sub, sup)`

```python
class Animal(object):
    pass

class Cat(Animal):
    pass

print(issubclass(Cat, Animal))  # True
print(issubclass(Animal, Cat))  # False
```

###### `isinstance(obj, cls)`

- 判断一个对象是否是一个类的实例

```python
class Animal(object):
    pass

class Cat(Animal):
    pass
    
print(isinstance(cat, Cat))  # True
```

###### `hasattr()/getattr()/setattr()/delattr`

- 属性操作,不限于类,在类中使用最频繁

```python

class Person(object):
    def __init__(self, name):
        self.name = name


p = Person("韩卓")
print(hasattr(p, 'name'))  # True
```

```python
print(getattr(p, 'name'))  # 韩卓
```

```python
setattr(p, 'name', 'hanzhuo')
print(getattr(p, 'name'))  # hanzhuo
```

```python
delattr(p, 'name')
print(p.name)  # AttributeError: 'Person' object has no attribute 'name'
```

###### `dir()`

- 显示模块/类/实例的属性

```python
class NewPerson(object):
    def __init__(self, name):
        self.name = name


p = Person('tom')
print(dir(p))
```

- 结果如下

```python
['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'name']
```

###### `vars()`

- 将实例对象的属性以字典形式输出

```python
class NewPerson(object):
    def __init__(self, name):
        self.name = name


p = Person('tom')
print(vars(p))  # {'name': 'tom'}
```

##### 7.python对象序列化和反序列化

- 对象序列化:就是把对象持久保存成文件格式
- 对象反序列化:就是把对象从文件转换成对象
- python提供两个模块
  - `cPikle`和`pickle` 。这两个模块的功能都是一样的，区别在于`cPickle`是C语言写的,速度快
  - `pickle`是纯python写的,速度慢
  - 使用`pickle` 的`dumps`或者`dump`反序列化
  - 使用`pickle` 的`load`方法反序列化
- 不光是对象,像列表,字典都可以

```python
try:
    import cPickle as pickle
except ImportError:
    import pickle

class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age


p = Person('tom', 20)

with open('demo.data', 'wb') as f:
    b = pickle.dumps(p)
    f.write(b)


with open('demo.data', 'rb') as f1:
    p = pickle.load(f1)
    print(p.name)
    print(p.age)
    
    
​```
tom
20
​```
```

##### 8.面向对象实例

- ######重写str方法输出两个实例变量

```python
class Animal(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return "two instance variable is {0} and {1}".format(self.name,self.age)


cat = Animal("猫", 20)
print(cat)

# two instance variable is猫 and20
```

### 进程和线程

##### 1.进程和线程的定义

- 进程是操作系统中的多个应用程序,现在的操作系统都是多进程的,例如,你可以同时在使用Word写文件,还可以打开QQ进行聊天,酷狗音乐也在用。这就是操作系统的多进程
- 线程是一个应用程序中的多个执行线路,例如:一个web服务器会针对不同的用户请求.启动不同的线程来响应,这样不会产生阻塞(用户等待)。

##### 2.thread模块

- 已被放弃,为了兼容性,重命名为_thread

###### `_thread.start_new_thread_(function, args[, kwargs])`

- 参数说明
  - function - 线程函数
  - args - 传递给线程函数的参数, 它必须是个tuple类型
  - kwargs - 可选参数

```python
import _thread
import time

def print_time(thread_name, delay):
    count = 0
    while count < 5:
        time.sleep(delay)
        count += 1
        print("%s:%s" % (thread_name, time.ctime(time.time())))


try:
    _thread.start_new_thread(print_time, ("T-1",2,))
    _thread.start_new_thread(print_time, ('T-2', 4))
except:
    print("无法启动线程")

while 1:
    pass

​```
T-1:Sat Mar 10 16:48:16 2018
T-2:Sat Mar 10 16:48:18 2018
T-1:Sat Mar 10 16:48:18 2018
T-1:Sat Mar 10 16:48:20 2018
T-2:Sat Mar 10 16:48:22 2018
T-1:Sat Mar 10 16:48:22 2018
T-1:Sat Mar 10 16:48:24 2018
T-2:Sat Mar 10 16:48:26 2018
T-2:Sat Mar 10 16:48:30 2018
T-2:Sat Mar 10 16:48:34 2018
​```
```

##### 3.threading模块

- 在python中，默认情况下（其实就是setDaemon(False)），主线程执行完自己的任务以后，就退出了，此时子线程会继续执行自己的任务，直到自己的任务结束

```python
#  默认情况
import threading
import time

def run():
    time.sleep(2)
    print('当前线程的名字是', threading.current_thread().name)
    time.sleep(2)

if __name__ == "__main__":
    start_time = time.time()
    print("这是主线程", threading.current_thread().name)

thread = []
for i in range(5):
    task = threading.Thread(target=run)  # 没有块作用域
    thread.append(task)


for item in thread:
    item.start()

print("主线程结束")
print("一共用时为:", time.time() - start_time)

​```
这是主线程 MainThread
主线程结束
一共用时为: 0.001001596450805664
当前线程的名字是 Thread-4
当前线程的名字是 Thread-2
当前线程的名字是 Thread-1
当前线程的名字是 Thread-3
当前线程的名字是 Thread-5
​```
```

- 当我们使用setDaemon(True)方法，设置子线程为守护线程时，主线程一旦执行结束，则全部线程全部被终止执行，可能出现的情况就是，子线程的任务还没有完全执行结束，就被迫停止

```python
#  默认情况
import threading
import time

def run():
    time.sleep(2)
    print('当前线程的名字是', threading.current_thread().name)
    time.sleep(2)

if __name__ == "__main__":
    start_time = time.time()
    print("这是主线程", threading.current_thread().name)

thread = []
for i in range(5):
    task = threading.Thread(target=run)  # 没有块作用域
    thread.append(task)


for item in thread:
    item.setDaemon(True)
    item.start()

print("主线程结束")
print("一共用时为:", time.time() - start_time)
'''
这是主线程 MainThread
主线程结束
一共用时为: 0.0015015602111816406
'''
```

**非常明显的看到，主线程结束以后，子线程还没有来得及执行，整个程序就退出了**

- 此时join的作用就凸显出来了，join所完成的工作就是线程同步，即主线程任务结束之后，进入阻塞状态，一直等待其他的子线程执行结束之后，主线程在终止

```python
#  默认情况
import threading
import time

def run():
    time.sleep(2)
    print('当前线程的名字是', threading.current_thread().name)
    time.sleep(2)

if __name__ == "__main__":
    start_time = time.time()
    print("这是主线程", threading.current_thread().name)

thread = []
for i in range(5):
    task = threading.Thread(target=run)  # 没有块作用域
    thread.append(task)


for item in thread:
    item.setDaemon(True)
    item.start()
    item.join()

print("主线程结束")
print("一共用时为:", time.time() - start_time)
'''
这是主线程 MainThread
当前线程的名字是 Thread-1
当前线程的名字是 Thread-2
当前线程的名字是 Thread-3
当前线程的名字是 Thread-4
当前线程的名字是 Thread-5
主线程结束
一共用时为: 20.006995677947998
'''
```

**可以看到，主线程一直等待全部的子线程结束之后，主线程自身才结束，程序退出**

- join有一个timeout参数：

  - 当设置守护线程时，含义是主线程对于子线程等待timeout的时间将会杀死该子线程，最后退出程序。所以说，如果有10个子线程，全部的等待时间就是每个timeout的累加和。简单的来说，就是给每个子线程一个timeout的时间，让他去执行，时间一到，不管任务有没有完成，直接杀死。
  - 没有设置守护线程时，主线程将会等待timeout的累加和这样的一段时间，时间一到，主线程结束，但是并没有杀死子线程，子线程依然可以继续执行，直到子线程全部结束，程序退出。

  ​

- 我们可以通过直接从 threading.Thread 继承创建一个新的子类，并实例化后调用 start() 方法启动新线程，即它调用了线程的 run() 方法：

```python
import threading
import time

exitFlag = 0

class myThread (threading.Thread):
    def __init__(self, threadID, name, counter):
        threading.Thread.__init__(self)
        self.threadID = threadID
        self.name = name
        self.counter = counter
    def run(self):
        print ("开始线程：" + self.name)
        print_time(self.name, self.counter, 5)
        print ("退出线程：" + self.name)

def print_time(threadName, delay, counter):
    while counter:
        if exitFlag:
            threadName.exit()
        time.sleep(delay)
        print ("%s: %s" % (threadName, time.ctime(time.time())))
        counter -= 1

# 创建新线程
thread1 = myThread(1, "Thread-1", 1)
thread2 = myThread(2, "Thread-2", 2)

# 开启新线程
thread1.start()
thread2.start()
thread1.join()
thread2.join()
print ("退出主线程")
```

- 结果如下:

```python
'''
开始线程：Thread-1
开始线程：Thread-2
Thread-1: Wed Apr  6 11:46:46 2016
Thread-1: Wed Apr  6 11:46:47 2016
Thread-2: Wed Apr  6 11:46:47 2016
Thread-1: Wed Apr  6 11:46:48 2016
Thread-1: Wed Apr  6 11:46:49 2016
Thread-2: Wed Apr  6 11:46:49 2016
Thread-1: Wed Apr  6 11:46:50 2016
退出线程：Thread-1
Thread-2: Wed Apr  6 11:46:51 2016
Thread-2: Wed Apr  6 11:46:53 2016
Thread-2: Wed Apr  6 11:46:55 2016
退出线程：Thread-2
退出主线程
'''
```

**将以上线程加在一个列表中,则线程会顺序执行,如下:**

```python
# 创建新线程
task_list = []
thread1 = myThread(1, "Thread-1", 1)
thread2 = myThread(2, "Thread-2", 2)
task_list.append(thread1)
task_list.append(thread2)

# 开启新线程
for item in task_list:
    item.start()
    item.join()
```

- 结果如下:

```python
'''
开始线程：Thread-1
Thread-1: Sun Mar 11 10:43:09 2018
Thread-1: Sun Mar 11 10:43:10 2018
Thread-1: Sun Mar 11 10:43:11 2018
Thread-1: Sun Mar 11 10:43:12 2018
Thread-1: Sun Mar 11 10:43:13 2018
退出线程：Thread-1
开始线程：Thread-2
Thread-2: Sun Mar 11 10:43:15 2018
Thread-2: Sun Mar 11 10:43:17 2018
Thread-2: Sun Mar 11 10:43:19 2018
Thread-2: Sun Mar 11 10:43:21 2018
Thread-2: Sun Mar 11 10:43:23 2018
退出线程：Thread-2
退出主线程
'''
```

##### 4.Lock用法

- 如果多个线程共同对某个数据修改，则可能出现不可预料的结果，为了保证数据的正确性，需要对多个线程进行同步。

  使用 Thread 对象的 Lock 和 Rlock 可以实现简单的线程同步，这两个对象都有 acquire 方法和 release 方法，对于那些需要每次只允许一个线程操作的数据，可以将其操作放到 acquire 和 release 方法之间。如下：

  多线程的优势在于可以同时运行多个任务（至少感觉起来是这样）。但是当线程需要共享数据时，可能存在数据不同步的问题。

  考虑这样一种情况：一个列表里所有元素都是0，线程"set"从后向前把所有元素改成1，而线程"print"负责从前往后读取列表并打印。

  那么，可能线程"set"开始改的时候，线程"print"便来打印列表了，输出就成了一半0一半1，这就是数据的不同步。为了避免这种情况，引入了锁的概念。

  锁有两种状态——锁定和未锁定。每当一个线程比如"set"要访问共享数据时，必须先获得锁定；如果已经有别的线程比如"print"获得锁定了，那么就让线程"set"暂停，也就是同步阻塞；等到线程"print"访问完毕，释放锁以后，再让线程"set"继续。

  经过这样的处理，打印列表时要么全部输出0，要么全部输出1，不会再出现一半0一半1的尴尬场面。

```python
import threading
import time

class MyThread(threading.Thread):

    def __init__(self, threadId, name, counter):
        super().__init__(self)
        self.threadId = threadId
        self.name = name
        self.counter = counter

    def run(self):
        print("开启线程",self.name)
        # 获取锁,用于线程同步
        threadLock.acquire()
        print_time(self.name, self.counter, 3)
        # 释放锁,开启下一个线程
        threadLock.release()


def print_time(threadName, delay, counter):
    while counter:
        time.sleep(3)
        print("%s: %s" % (threadName, time.ctime(time.time())))
        counter -= 1

threadLock = threading.Lock()
threads = []
# 创建新线程
thread1 = MyThread(1, "Thread-1", 1)
thread2 = MyThread(2, "Thread-2", 2)

# 开启新线程
thread1.start()
thread2.start()

# 添加线程到线程列表
threads.append(thread1)
threads.append(thread2)

# 等待所有线程完成
for t in threads:
    t.join()
print("退出主线程")
'''
开始线程：Thread-1
Thread-1: Sun Mar 11 11:39:59 2018
Thread-1: Sun Mar 11 11:40:00 2018
Thread-1: Sun Mar 11 11:40:01 2018
Thread-1: Sun Mar 11 11:40:02 2018
Thread-1: Sun Mar 11 11:40:03 2018
退出线程：Thread-1
开始线程：Thread-2
Thread-2: Sun Mar 11 11:40:05 2018
Thread-2: Sun Mar 11 11:40:07 2018
Thread-2: Sun Mar 11 11:40:09 2018
Thread-2: Sun Mar 11 11:40:11 2018
Thread-2: Sun Mar 11 11:40:13 2018
退出线程：Thread-2
退出主线程
'''
```



### time模块

- 首先要引入`time`模块

  ```python
  import time
  ```

`time.sleep(secs)`

- 获取当前时间戳

  ```
  time.time() # 1520669363.6301014
  ```

  ​

`time.localtime(seconds)`

- 用元组装起来的9组数字处理时间

  ```python
  print(time.localtime(1520669363.6301014))  
  # time.struct_time(tm_year=2018, tm_mon=3, tm_mday=10, tm_hour=16, tm_min=9, tm_sec=23, tm_wday=5, tm_yday=69, tm_isdst=0)
  ```

`time.strftime`

- 按需求格式化时间

  ```python
  print time.strftime("%Y-%m-%d %H:%M:%S",time.localtime())
  print time.strftime("%a %b %d %H:%M:%S %Y", time.localtime()) 
  print time.strftime("%Y%m%d",time.localtime())
  ```



- 将字符串转换为时间戳

  ```python
  timeArry = time.strptime(s, "%Y-%m-%d %H:%M:%S")  # 将其转换为时间数组
  print(timeArry)  # time.struct_time(tm_year=2018, tm_mon=3, tm_mday=10, tm_hour=16, tm_min=16, tm_sec=42, tm_wday=5, tm_yday=69, tm_isdst=-1)

  timestamp = int(time.mktime(timeArry))  # 1520669802
  ```

- 字符串格式更改

  -   如a = "2013-10-10 23:40:00",想改为 a = "2013/10/10 23:40:00"
    ​    方法:先转换为时间数组,然后转换为其他格式

  ```python
      timeArray = time.strptime(a, "%Y-%m-%d %H:%M:%S")
      otherStyleTime = time.strftime("%Y/%m/%d %H:%M:%S", timeArray)
  ```

- 时间戳转换为指定格式日期

  - 利用localtime()转化为时间数组,然后格式化为需要的格式

  ```python
  timestamp = 1520669802
  timeArray = time.localtime(timestamp)
  fomatTime = time.strftime("%Y-%m-%d %H:%M:%S", timeArray)
  print(fomatTime)  # 2018-03-10 16:16:42
  ```

  - 使用datetime模块

  ```python
  import datetime
  now = datetime.datetime.now()  # 时间数组
  stamp = now.strftime("%Y-%m-%d %H:%M:%S") 
  print(stamp)  # 2018-03-10 16:26:36
  ```

- 获得三天前的时间

  - 方法一

          import time
          import datetime
          # 先获得时间数组格式的日期
          threeDayAgo = (datetime.datetime.now() - datetime.timedelta(days = 3))
          # 转换为时间戳:
              timeStamp = int(time.mktime(threeDayAgo.timetuple()))
          # 转换为其他字符串格式:
              otherStyleTime = threeDayAgo.strftime("%Y-%m-%d %H:%M:%S")
      # 注:timedelta()的参数有:days,hours,seconds,microseconds
  - 方法二(给定时间戳,计算该时间的几天前时间)

  ```python
    timeStamp = 1381419600
      # 先转换为datetime
      import datetime
      import time
      dateArray = datetime.datetime.utcfromtimestamp(timeStamp)
      threeDayAgo = dateArray - datetime.timedelta(days = 3)
      # 参考5,可以转换为其他的任意格式了
  ```

- python中时间日期格式化符号：

```
   %y 两位数的年份表示（00-99）
    %Y 四位数的年份表示（000-9999）
    %m 月份（01-12）
    %d 月内中的一天（0-31）
    %H 24小时制小时数（0-23）
    %I 12小时制小时数（01-12）
    %M 分钟数（00=59）
    %S 秒（00-59）
    %a 本地简化星期名称
    %A 本地完整星期名称
    %b 本地简化的月份名称
    %B 本地完整的月份名称
    %c 本地相应的日期表示和时间表示
    %j 年内的一天（001-366）
    %p 本地A.M.或P.M.的等价符
    %U 一年中的星期数（00-53）星期天为星期的开始
    %w 星期（0-6），星期天为星期的开始
    %W 一年中的星期数（00-53）星期一为星期的开始
    %x 本地相应的日期表示
    %X 本地相应的时间表示
    %Z 当前时区的名称
    %% %号本身
```

### 正则表达式

##### 1.正则表达式基础

- 基础知识学习链接

  [正则基础学习](http://deerchao.net/tutorials/regex/regex.htm)


- `\b` 代表着单词的开头或结尾，也就是单词的分界处

```python
s = "hi luck"
m = re.match(r'\bhi\b.*\bluck\b', s)
print(m.group())  # hi luck
```

- `\s`匹配任意的空白符，包括空格，制表符(Tab)，换行符，中文全角空格等
- `\w`匹配字母或数字或下划线或汉字等
- 如果你想查找元字符本身的话，比如你查找.,或者*,就出现了问题：你没办法指定它们，因为它们会被解释成别的意思。这时你就得使用\来取消这些字符的特殊意义。因此，你应该使用\.和\*。当然，要查找\本身，你也得用\\.

```
例如：deerchao\.net匹配deerchao.net，C:\\Windows匹配C:\Windows。
```

- **实例**

```python
s = '(010)88886666'
s1 = '022-22334455'
s3 = '02912345678'
m = re.match(r'\(?\d{3}[)-]?\d{8}',s3)
print(m.group())  # 02912345678
```

```
首先是一个转义字符\(,它能出现0次或1次(?),然后是一个0，后面跟着2个数字(\d{2})，然后是)或-或空格中的一个，它出现1次或不出现(?)，最后是8个数字(\d{8})。
```

- 不幸的是，刚才那个表达式也能匹配010)12345678或(022-87654321这样的“不正确”的格式。

- 要解决这个问题，我们需要用到分枝条件。

- **分支条件**

  - 正则表达式里的分枝条件指的是有几种规则，如果满足其中任意一种规则都应该当成匹配，具体方法是用|把不同的规则分隔开。
  - 匹配分枝条件时，将会从左到右地测试每个条件，如果满足了某个分枝的话，就不会去再管其它的条件了。

  ```python
  # 分支条件
  def condition(str, flag="first"):
      if flag == 'first':
          m = re.match(r'\d{5}-\d{4}|\d{5}', str)
          if m:
              return m.group()
          else:
              return False
      else:
          m = re.match(r'\d{5}|\d{5}-\d{4}', str)
          if m:
              return m.group()

  print(condition('12345-6789'))  # 12345-6789
  print(condition('12345-6789', 'second'))  # 12345
  ```

- **分组**

  - 如果想要重复多个字符又该怎么办？你可以用小括号来指定子表达式(也叫做分组)，然后你就可以指定这个子表达式的重复次数了，你也可以对子表达式进行其它一些操作(后面会有介绍)。

  ```
  (\d{1,3}\.){3}\d{1,3}是一个简单的IP地址匹配表达式。要理解这个表达式，请按下列顺序分析它：\d{1,3}匹配1到3位的数字，(\d{1,3}\.){3}匹配三位数字加上一个英文句号(这个整体也就是这个分组)重复3次，最后再加上一个一到三位的数字(\d{1,3})。
  ```

- **反义**

| 代码/语法 |                    说明                    |
| :-------: | :----------------------------------------: |
|    \W     | 匹配任意不是字母，数字，下划线，汉字的字符 |
|    \S     |          匹配任意不是空白符的字符          |
|    \D     |            匹配任意非数字的字符            |
|    \B     |        匹配不是单词开头或结束的位置        |
|  [ ^x ]   |          匹配除了x以外的任意字符           |

```
<a[^>]+>匹配用尖括号括起来的以a开头的字符串。
```

- **后向引用**

  - 使用小括号指定一个子表达式后，**匹配这个子表达式的文本**(也就是此分组捕获的内容)可以在表达式或其它程序中作进一步的处理。默认情况下，每个分组会自动拥有一个组号，规则是：从左向右，以分组的左括号为标志，第一个出现的分组的组号为1，第二个为2，以此类推。
  - 后向引用用于重复搜索前面某个分组匹配的文本。例如，\1代表分组1匹配的文本。

  ```
  \b(\w+)\b\s+\1\b可以用来匹配重复的单词，像go go, 或者kitty kitty。
  ```

  ```
  这个表达式首先是一个单词，也就是单词开始处和结束处之间的多于一个的字母或数字(\b(\w+)\b)，这个单词会被捕获到编号为1的分组中，然后是1个或几个空白符(\s+)，最后是分组1中捕获的内容（也就是前面匹配的那个单词）(\1)。
  ```

  - 你也可以自己指定子表达式的组名。

  ```
  要指定一个子表达式的组名，请使用这样的语法：(?<Word>\w+)(或者把尖括号换成'也行：(?'Word'\w+)),这样就把\w+的组名指定为Word了。
  ```

  ```
  要反向引用这个分组捕获的内容，你可以使用\k<Word>,所以上一个例子也可以写成这样：\b(?<Word>\w+)\b\s+\k<Word>\b。
  ```

- **使用小括号的时候，还有很多特定用途的语法。**

![img](file:///C:\Users\Administrator\Documents\Tencent Files\1298648980\Image\C2C\5N%}E%0RHQC`I]99X[@J@G7.png)

- **零宽断言**

  - ###### 零宽度正预测先行断言

  ```
  (?=exp)也叫零宽度正预测先行断言，它断言自身出现的位置的后面能匹配表达式exp。比如\b\w+(?=ing\b)，匹配以ing结尾的单词的前面部分(除了ing以外的部分)，如查找I'm singing while you're dancing.时，它会匹配sing和danc。
  ```

  ```python
  # 零宽断言
  s = "i'm singing while you're dancing"
  m = re.findall(r'\b\w+(?=ing\b)', s)
  print(m)  # ['sing', 'danc']
  ```

  - ###### 零宽度正回顾后发断言]

  ```
  (?<=exp)也叫零宽度正回顾后发断言，它断言自身出现的位置的前面能匹配表达式exp。比如(?<=\bre)\w+\b会匹配以re开头的单词的后半部分(除了re以外的部分)，例如在查找reading a book时，它匹配ading。
  ```

  ```
  s = 'reading a book'
  m = re.findall(r'(?<=\bre)\w+\b', s)
  print(m)  # ['ading']
  ```

  - ###### 二者结合匹配空格中间的字符

  ```python
  s = '123 456 789 234 567'
  m = re.findall(r'(?<=\s)\d+(?=\s)', s)
  print(m)  # ['456', '789', '234']
  ```

- **负向零宽断言**

  - \b\w*q[ ^u ]\w*\b匹配包含**后面不是字母u的字母q**的单词。

  ```
  但是如果多做测试(或者你思维足够敏锐，直接就观察出来了)，你会发现，如果q出现在单词的结尾的话，像Iraq,Benq，这个表达式就会出错。
  ```

  ```
  这是因为[^u]总要匹配一个字符，所以如果q是单词的最后一个字符的话，后面的[^u]将会匹配q后面的单词分隔符(可能是空格，或者是句号或其它的什么)，后面的\w*\b将会匹配下一个单词，于是\b\w*q[^u]\w*\b就能匹配整个Iraq fighting。
  ```

  ```
  负向零宽断言能解决这样的问题，因为它只匹配一个位置，并不消费任何字符
  ```

  - 现在，我们可以这样来解决这个问题：\b\w*q(?!u)\w*\b。
  - 例如,要找出**g后面不能有a**的所有单词组

  ```python

  s = 'the guy who is playing gameboy is a gay'
  m = re.findall(r'\b\w*g(?!a)\w*\b', s)
  print(m)  # ['guy', 'playing']
  ```

  ```
  \d{3}(?!\d)匹配三位数字，而且这三位数字的后面不能是数字；\b((?!abc)\w)+\b匹配不包含连续字符串abc的单词。
  ```

  ```
  同理，我们可以用(?<!exp),零宽度负回顾后发断言来断言此位置的前面不能匹配表达式exp：(?<![a-z])\d{7}匹配前面不是小写字母的七位数字。
  ```

- **注释**

```
小括号的另一种用途是通过语法(?#comment)来包含注释。例如：2[0-4]\d(?#200-249)|25[0-5](?#250-255)|[01]?\d\d?(?#0-199)。

要包含注释的话，最好是启用“忽略模式里的空白符”选项，这样在编写表达式时能任意的添加空格，Tab，换行，而实际使用时这些都将被忽略。启用这个选项后，在#后面到这一行结束的所有文本都将被当成注释忽略掉。例如，我们可以前面的一个表达式写成这样：
  (?<=    # 断言要匹配的文本的前缀
      <(\w+)> # 查找尖括号括起来的字母或数字(即HTML/XML标签)
      )       # 前缀结束
      .*      # 匹配任意文本
      (?=     # 断言要匹配的文本的后缀
      <\/\1>  # 查找尖括号括起来的内容：前面是一个"/"，后面是先前捕获的标签
      )       # 后缀结束
```



##### 2.贪婪匹配和惰性匹配

- 原理深入分析

  [正则贪婪和惰性原理深入讲解](http://www.jb51.net/article/31491.htm)


- **量词匹配优先与忽略优先**

  ```
  正则表达式，量词是匹配优先的，也就是说，量词会尽量地吃，直到由于吃得太多，导致后面没法匹配，才吐出来一个。
  举例来说，文本ab1cd2,正则表达式 .*[0-9] 
  匹配过程：*一直吃到2，发现坏了，数字没法匹配了，于是突出2，匹配成功，结束。也就是说.*匹配了ab1cd
  如果我想让.*[0-9]匹配ab1cd2两次，怎么办？
  忽略量词优先，.*?[0-9]，量词后面加一个问号。也就是说，让*尽量地少吃。
  匹配过程：*不吃，不吃不行啊，a不能匹配数字，于是吃下a，b不能匹配数字，于是再吃下b，1匹配数字，结束。开始下一个匹配。
  ```

- ###### 贪婪量词

先看整个字符串是不是一个匹配。如果没有发现匹配，它去掉最后字符串中的最后一个字符，并再次尝试。如果还是没有发现匹配，那么    再次去掉最后一个字符串，这个过程会一直重复直到发现一个匹配或者字符串不剩任何字符。简单量词都是贪婪量词。

- ###### 惰性量词

先看字符串中的第一个字母是不是一个匹配，如果单独着一个字符还不够，就读入下一个字符，组成两个字符的字符串。如果还没有发现匹配，惰性量词继续从字符串中添加字符直到发现一个匹配或者整个字符串都检查过也没有匹配。惰性量词和贪婪量词的工作方式恰好相反。

| 贪婪量词 | 惰性量词 |              描述               |
| :------: | :------: | :-----------------------------: |
|    ?     |    ??    | 可以出现0次或1次，但至多出现1次 |
|    *     |    *?    |  可以出现任意次，也可以不出现   |
|    +     |    +?    |  出现1次或多次，但至少出现1次   |
|   {n}    |   {n}?   |           一定出现n次           |
|  {n, m}  | {n, m}?  | 至少出现n次，但至多不能超过m次  |
|  {n, }   |  {n,}?   |  可以出现任意次，但至少出现n次  |

- 我们要从字符串`abbbaabbbaaabbb1234`中获得`abbb`，`aabbb`，`aaabbb`的匹配


- ######惰性量词工作原理

```python
s = "abbbaabbbaaabbb1234"
m = re.findall(r'.*?bbb', s)
print(m)   # ['abbb', 'aabbb', 'aaabbb']
```

```
 惰性量词的工作过程可以这样表示：
      a)a
      b)ab
      c)abb
      d)abbb //保存结果，并从下一个位置重新开始
  
      e)a 
      f)aa 
      g)aab
      h)aabb
      j)aabbb //保存结果，并从下一个位置重新开始
  
      e)a
      e)aa
      e)aaa
      e)aaab 
      e)aaabb 
      e)aaabbb  //保存结果，并从下一个位置重新开始
```

- **(?# …)就表示一个注释，里面的内容会被忽略**



##### 2. re模块

###### `m.group()`

```python 
import re
p = 'foo'

s = 'like football'
m = re.search(p, s)
print(m.group())  # foo
```

###### `m. start()`

```python
print(m.start())  # 5 (匹配到的字符串的索引值)
```

###### `m.end()`

```python
print(m.end())    # 8
```

###### `m.span()`

```python
print(m.span())   # (5, 8) 范围
```

###### `m.string`

```python
print(m.string)   # like football
```

```python
print(m)  # <_sre.SRE_Match object; span=(5, 8), match='foo'>
```

- 匹配单个字符

```python
# 匹配单个字符
p = 'h.t'
s = 'hat'
s1 = 'hit'
s2 = 'pig'
s3 = 'hit pig'

m = re.match(p, s3)

if m:
    print(m.group())  # hit
    print(m.span())  # (0, 3)
    print(m.string)  # hit pig
else:
    print("匹配失败")
```

- 匹配任意字符

```python
p = 'hello|hi|test'
s = 'hello world'
s1 = 'hi world'
s2 = 'world hi'
s3 = 'test test'
# m = re.match(p,s2)
m = re.search(p,s3)
if m:
    print(m.group())   # test
    print(m.span())    # (0, 4)
    print(m.string)    # test test
else:
    print('匹配失败')
```

- **match方法是从第一个字符开始匹配**

```python
print(re.match("www", "www.baidu.com").span()) # (0, 3)
print(re.match("baidu", "www.baidu.com"))  # None
```

















































