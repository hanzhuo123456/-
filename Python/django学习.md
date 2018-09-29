### Django安装

```
pip install django
```

- 查看版本

```
>>> import django
>>> django.get_version()
```

- 使用 django-admin.py 来创建 HelloWorld 项目：

```
django-admin startproject HelloWorld
```

##### 目录说明：

- **HelloWorld:** 项目的容器。
- **manage.py:** 一个实用的命令行工具，可让你以各种方式与该 Django 项目进行交互。
- **HelloWorld/__init__.py:** 一个空文件，告诉 Python 该目录是一个 Python 包。
- **HelloWorld/settings.py:** 该 Django 项目的设置/配置。
- **HelloWorld/urls.py:** 该 Django 项目的 URL 声明; 一份由 Django 驱动的网站"目录"。
- **HelloWorld/wsgi.py:** 一个 WSGI 兼容的 Web 服务器的入口，以便运行你的项目。

#####启动服务器

```
python manage.py runserver 0.0.0.0:8000
```

![jt](C:\Users\Administrator\Desktop\jt.png)

##### 在pycharm使用django

```
settting->project interpreter->换python解释器为当前虚拟环境的解释器->点击+号>搜索django->安装
```

### 视图和 URL 配置

在先前创建的 HelloWorld 目录下的 HelloWorld 目录新建一个 view.py 文件，并输入代码：

```python
from django.http import HttpResponse 

def hello(request):    
    return HttpResponse("Hello world ! ")
```



接着，绑定 URL 与视图函数。打开 urls.py 文件，删除原来代码，将以下代码复制粘贴到 urls.py 文件中：



```python
from django.conf.urls import url 
from . import view 
urlpatterns = [   
    url(r'^$', view.hello),
]
```



整个目录结构如下：

```
$ tree
.
|-- HelloWorld
|   |-- __init__.py
|   |-- __init__.pyc
|   |-- settings.py
|   |-- settings.pyc
|   |-- urls.py              # url 配置
|   |-- urls.pyc
|   |-- view.py              # 添加的视图文件
|   |-- view.pyc             # 编译后的视图文件
|   |-- wsgi.py
|   `-- wsgi.pyc
`-- manage.py
```

完成后，启动 Django 开发服务器，并在浏览器访问打开浏览器并访问：

![img](http://www.runoob.com/wp-content/uploads/2015/01/BD259D4C-2DBE-4657-8761-D8C3508E8A94.jpg)

我们也可以修改以下规则：

```python
from django.conf.urls import url 
from . import view 
urlpatterns = [    
url(r'^hello$', view.hello),
]
```

通过浏览器打开 http://127.0.0.1:8000/hello，输出结果如下：

![img](http://www.runoob.com/wp-content/uploads/2015/01/344A94C7-8D7D-4A69-9963-00D28A69CD56.jpg)

**注意：**项目中如果代码有改动，服务器会自动监测代码的改动并自动重新载入，所以如果你已经启动了服务器则不需手动重启。

##### url函数

Django url() 可以接收四个参数，分别是两个必选参数：regex、view 和两个可选参数：kwargs、name，接下来详细介绍这四个参数。

- regex: 正则表达式，与之匹配的 URL 会执行对应的第二个参数 view。
- view: 用于执行与正则表达式匹配的 URL 请求。
- kwargs: 视图使用的字典类型的参数。
- name: 用来反向获取 URL。


### python django模型

##### 1.python django模型内部类meta详解

Django 模型类的Meta是一个内部类，它用于定义一些Django模型类的行为特性。以下对此作一总结：

- **abstract**

​     这个属性是定义当前的模型类是不是一个抽象类。所谓抽象类是不会对应数据库表的。一般我们用它来归纳一些公共属性字段，然后继承它的子类可以继承这些字段。比如下面的代码中Human是一个抽象类，Employee是一个继承了Human的子类，那么在运行syncdb命令时，不会生成Human表，但是会生成一个Employee表，它包含了Human中继承来的字段，以后如果再添加一个Customer模型类，它可以同样继承Human的公共属性：

```python
class Human(models.Model):

    name=models.CharField(max_length=100)

    GENDER_CHOICE=((u'M',u'Male'),(u'F',u'Female'),)

    gender=models.CharField(max_length=2,choices=GENDER_CHOICE,null=True)

    class Meta:

        abstract=True

```

```python
class Employee(Human):

    joint_date=models.DateField()

class Customer(Human):

    first_name=models.CharField(max_length=100)

    birth_day=models.DateField()

```



上面的代码，执行python manage.py syncdb 后的输出结果入下，可以看出Human表并没有被创建:

```python
$ python manage.py syncdb

Creating tables ...

Creating table myapp_employee

Creating table myapp_customer

Installing custom SQL ...

Installing indexes ...

No fixtures found.

```



- **app_label**

app_label这个选项只在一种情况下使用，就是你的模型类不在默认的应用程序包下的models.py文件中，这时候你需要指定你这个模型类是那个应用程序的。比如你在其他地方写了一个模型类，而这个模型类是属于myapp的，那么你这是需要指定为：

app_label='myapp'

- **db_table**

db_table是用于指定自定义数据库表名的。Django有一套默认的按照一定规则生成数据模型对应的数据库表名，如果你想使用自定义的表名，就通过这个属性指定，比如：

table_name='my_owner_table'

- **db_tablespace**

有些数据库有数据库表空间，比如Oracle。你可以通过db_tablespace来指定这个模型对应的数据库表放在哪个数据库表空间。

- **get_latest_by**

由于Django的管理方法中有个lastest()方法，就是得到最近一行记录。如果你的数据模型中有 DateField 或 DateTimeField 类型的字段，你可以通过这个选项来指定lastest()是按照哪个字段进行选取的。

- **managed**

由于Django会自动根据模型类生成映射的数据库表，如果你不希望Django这么做，可以把managed的值设置为False。

- order_with_respect_to


- **ordering**

这个字段是告诉Django模型对象返回的记录结果集是按照哪个字段排序的。比如下面的代码：

ordering=['order_date'] # 按订单升序排列
ordering=['-order_date'] # 按订单降序排列，-表示降序
ordering=['?order_date'] # 随机排序，？表示随机

- **permissions**

permissions主要是为了在Django Admin管理模块下使用的，如果你设置了这个属性可以让指定的方法权限描述更清晰可读。

- **proxy**

这是为了实现代理模型使用的，这里先不讲随后的文章介绍。

- **unique_together**

unique_together这个选项用于：当你需要通过两个字段保持唯一性时使用。比如假设你希望，一个Person的FirstName和LastName两者的组合必须是唯一的，那么需要这样设置：

unique_together = (("first_name", "last_name"),)

- **verbose_name**

verbose_name的意思很简单，就是给你的模型类起一个更可读的名字：

verbose_name = "pizza"

- **verbose_name_plural**

这个选项是指定，模型的复数形式是什么，比如：

verbose_name_plural = "stories"

如果不指定Django会自动在模型名称后加一个’s’

##### 2.django中两张表有外键关系的相互查找方法，自定义json编码方法

- [django中两张表有外键关系的相互查找方法，自定义json编码方法](http://www.cnblogs.com/zhaopengcheng/p/5608328.html)


##### 3.在models中通过外键去获取关联的数量,并在模板中使用

```python
class Course(models.Model):
    course_org = models.ForeignKey(CourseOrg, verbose_name=u'课程机构', null=True, blank=True)
    name = models.CharField(max_length=50, verbose_name=u'课程名')
    desc = models.CharField(max_length=300, verbose_name=u'课程描述')
    detail = models.TextField(verbose_name=u'课程详情')
    difficult_degree = models.CharField(max_length=10, choices=(('primary', u'初级'), ('intermediate', u'中级'),
                                                                ('advanced',  u'高级')))
    learn_times = models.IntegerField(default=0, verbose_name=u'学习时长')
    students = models.IntegerField(default=0, verbose_name=u'学习人数')
    fav_nums = models.IntegerField(default=0, verbose_name=u'收藏人数')
    image = models.ImageField(upload_to='courses/%Y/%m', verbose_name=u'课程封面')
    click_nums = models.IntegerField(default=0, verbose_name=u'点击数')
    add_time = models.DateTimeField(default=datetime.now)

    class Meta:
        verbose_name = u'课程'
        verbose_name_plural = verbose_name

    def get_section_nums(self):
        return self.section_set.all().count()  //通过函数获取数量
```



##### 使用user_id__in这个获取数据

```python

class CourseInfoView(LoginRequiredMixin, View):
    """
    课程章节信息
    """
    def get(self, request, course_id):
        course = Course.objects.get(id=int(course_id))
        course.students += 1
        course.save()
        #查询用户是否已经关联了该课程
        user_courses = UserCourse.objects.filter(user=request.user, course=course)
        if not user_courses:
            user_course = UserCourse(user=request.user, course=course)
            user_course.save()

        user_cousers = UserCourse.objects.filter(course=course)
        user_ids = [user_couser.user.id for user_couser in user_cousers]
        # 就是这儿,这儿的骚操作,其中user_ids是一个list,相当于是select * from usercourse where user_id in user_ids
        all_user_courses = UserCourse.objects.filter(user_id__in=user_ids) # 两个下划线
        #取出所有课程id
        course_ids = [user_couser.course.id for user_couser in all_user_courses]
        #获取学过该用户学过其他的所有课程
        relate_courses = Course.objects.filter(id__in=course_ids).order_by("-click_nums")[:5]
        all_resources = CourseResource.objects.filter(course=course)
        return render(request, "course-video.html", {
            "course":course,
            "course_resources":all_resources,
            "relate_courses":relate_courses
        })
```



- 在模板中这样获取

```
 return render(request, 'course-detail.html', {
            'course': cur_course,
        })
   <li><span class="pram word3">章&nbsp;节&nbsp;数：</span><span>
		 {{ course.get_section_nums }}
		 
	</span>
	</li>
```



##### 通过`__icontains`作不区分大小写的查询

```
all_course = all_course.filter(name_icontains=search_keywords)  # 其中icontains中的i表示不区分大小写
```

##### 通过`Q`来实现数据库的`or`操作

```python
from django.db.models import Q
  user = UserProfile.objects.get(Q(username=username) | Q(email=username))
```




### 遇到的错误以及解决办法

##### 1.当创建模型使用外键时发生的错误

```python
contact = models.ForeignKey(Contact)
```

正确的代码如下:

```python
contact = models.ForeignKey(Contact, on_delete=models.CASCADE)
```

##### 2.当通过`python manage.py migrate YourModel`时不能创建表的错误

```
 python manage.py makemigrations TestModel  # 让 Django 知道我们在我们的模型有一些变更
 python manage.py migrate TestModel   # 创建表结构
```

- 以上方法在使用一次然后再次使用时会发生错误`no migrations to apply`	

```
# 解决办法
1. 去数据库的django_migratins删掉与该模型有关的所有数据
   delete from django_migrations where app = 'YourModel'
2.删掉项目中的migrations文件夹下的所有的除了__init__.py的文件

*附加：如果Models文件里面有许多表而无法创建的情况，去数据库里面把表删除重新migrations就行了

3.重新使用 
 python manage.py makemigrations TestModel  # 让 Django 知道我们在我们的模型有一些变更
 python manage.py migrate TestModel   # 创建表结构
```

##### 3.解决pycharm无法导入包的问题

- mark包名
- 在`setting.py`下全局搜索路径

```python
import os
import sys
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
sys.path.insert(0, os.path.join(BASE_DIR, 'apps'))
```

##### 4.local host：8000打不开网页的原因

- 可能是动了urls.py，将里面的include删除后重新加载网页就可以了，然后把include加回去

### on_delete方法的取值

```
on_delete=None,               # 删除关联表中的数据时,当前表与其关联的field的行为
on_delete=models.CASCADE,     # 删除关联数据,与之关联也删除
on_delete=models.DO_NOTHING,  # 删除关联数据,什么也不做
on_delete=models.PROTECT,     # 删除关联数据,引发错误ProtectedError
# models.ForeignKey('关联表', on_delete=models.SET_NULL, blank=True, null=True)
on_delete=models.SET_NULL,    # 删除关联数据,与之关联的值设置为null（前提FK字段需要设置为可空,一对一同理）
# models.ForeignKey('关联表', on_delete=models.SET_DEFAULT, default='默认值')
on_delete=models.SET_DEFAULT, # 删除关联数据,与之关联的值设置为默认值（前提FK字段需要设置默认值,一对一同理）
on_delete=models.SET,         # 删除关联数据,
 a. 与之关联的值设置为指定值,设置：models.SET(值)
 b. 与之关联的值设置为可执行对象的返回值,设置：models.SET(可执行对象)
```

### 通过xadmin快速搭建后台管理系统

- 首先,确保django的版本为1.9.8,具体的安装django方法如下:

```
pip install django==1.9.8
```

- 然后新建项目

```
django-admin startproject myproject
```

- 安装xadmin(pip install xadmin安装会出错)

```python
1.从github上下载xadmin的源码包

2.命令行进入解压包的路径

3.然后运行python setup.py install,这样会将xadmin的所有依赖包安装上去,因为源码安装对于项目更友好,所以此时需要将安装好的xadmin卸载

4.pip uninstall xadmin

5.卸载xadmin时不会卸载掉其对应的依赖包,此时将源码里面的xadmin拷贝到项目中即可

6.将xadmin和crispy_forms注册到apps当中,配置xadmin的url

注:安装mysqlclient时应指定版本 pip install mysqlclient==1.3.12

7.通过makemigrations和migrate将xadmin对应的表迁移到数据库中

8.运行服务,通过url访问xadmin的后台登录界面

9.修改英文为中文

10.具体的修改配置如下
	LANGUAGE_CODE = 'zh-hans'    # 设置为中文

	TIME_ZONE = 'Asia/shanghai'  # 时区改为上海时区

	USE_TZ = False  # 不让其设置国际时间
	
11.通过命令python manage.py createsuperuser创建登录的用户名和密码
```

###### @浅析xadmin中的关联搜索(过滤器搜索以及普通搜索)

- 当我们有如下两张表时

```python
class Course(models.Model):
    name = models.CharField(max_length=50, verbose_name=u'课程名')
    desc = models.CharField(max_length=300, verbose_name=u'课程描述')
    detail = models.TextField(verbose_name=u'课程详情')
    difficult_degree = models.CharField(max_length=10, choices=(('primary', u'初级'), ('intermediate', u'中级'), ('advanced', u'高级')))
    learn_times = models.IntegerField(default=0, verbose_name=u'学习时长')
    students = models.IntegerField(default=0, verbose_name=u'学习人数')
    fav_nums = models.IntegerField(default=0, verbose_name=u'收藏人数')
    image = models.ImageField(upload_to='courses/%Y/%m', verbose_name=u'课程封面')
    click_nums = models.IntegerField(default=0, verbose_name=u'点击数')
    add_time = models.DateTimeField(default=datetime.now)

    class Meta:
        verbose_name = u'课程'
        verbose_name_plural = verbose_name

    def __str__(self):
        return self.name
```

```python
class Section(models.Model):
    course = models.ForeignKey(Course, verbose_name=u'课程ID', on_delete=models.DO_NOTHING)
    name = models.CharField(max_length=50, verbose_name=u'章节名')
    add_time = models.DateTimeField(default=datetime.now)

    class Meta:
        verbose_name = u'章节'
        verbose_name_plural = verbose_name

    def __str__(self):
        return self.name
```

- 从上可以看出,`Section`的外键为`course`,在章节的xadmin后台管理中,我们如何在`Section`后台管理界面中通过`Course`的字段搜索到章节的信息呢?章节的管理界面如下:

![img](https://images2018.cnblogs.com/blog/1188720/201803/1188720-20180324171024481-752323638.png)

- 我们搜索计算机网络,那么此时会出现一条数据,然而计算机网络这个内容是`Course`表里面的,如果我们单纯这样写,能不能达到效果呢?

```python
class SectionAdmin(object):
    list_display = ['course', 'name', 'add_time']
    search_fields = ['course', 'name']
    list_filter = ['course', 'name', 'add_time']
```

- 以上写法是错误的,补充一下,在`search_fields`字段当中使用时间搜索是不行的,会报错
- 正确的写法如下

```python
class SectionAdmin(object):
    list_display = ['course', 'name', 'add_time']
    search_fields = ['course__name', 'name']
    list_filter = ['course__desc', 'name', 'add_time']
```

- 从上可以看到.有一个`course__name`字段,这是什么意思呢?
- 首先,course是外键,它关联到`Course`表的`name`字段
- 其搜索的大致原理可以如下:

```
1. 我输入'计算机网络'五个字

2. 搜索引擎去Course表里面找`name`字段是否存在'计算机网络'

3.如果存在,那么再去匹配Section表里面所有课程ID为计算机网络的章节记录

4.将所有章节记录显示出来

5.注意,如果章节名为'计算机网络02',课程为'计算机网络',而在该课程下还有'第三章'这个章节名,当我们搜索'计算机网络'的时候,会出现两条记录,而不仅仅是计算机网络02这一条记录

6.同时,course_name还可以改成Course表里面的任何一个字段,除了时间,如:course_desc
```



######@xadmin的全局配置

- 添加主题

```python
from xadmin import views


class BaseSetting(object):
    enable_themes = True
    use_bootswatch = True
    
xadmin.site.register(views.BaseAdminView, BaseSetting)
```

- 修改头部和底部的标题以及折叠左边的菜单栏

```python
from xadmin import views

class GlobalSetting(object):
    site_title = '在线学堂后台管理系统'
    site_footer = 'hanzhuo'
    menu_style = 'accordion'  # 折叠
    
xadmin.site.register(views.CommAdminView, GlobalSetting)
```

- 修改左边菜单栏为中文

```python
1.修改apps文件
class CoursesConfig(AppConfig):
    name = 'courses'
    verbose_name = u'用户操作'
    
2.修改__init__文件

default_app_config = 'courses.apps.CoursesConfig'

```

###### @django加载静态文件以及静态文件路径配置

- 配置好静态文件的目录

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR+'/templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

- 添加静态文件设置

```python
STATIC_URL = '/static/'
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, "static"),   # 将static加入搜索路径当中去
)
```

- 配置urls.py

```python
from django.views.generic import TemplateView

urlpatterns = [
    url(r'^xadmin/', xadmin.site.urls),
    url(r'^$', TemplateView.as_view(template_name='index.html'), name='index')
]
```

- 静态文件当中引用

```python
{% load staticfiles %} 
<img src='{% static "images/01.jpg" %}' alt="">
```

### pycharm的一些使用技巧

###### - 如何在模板语言中提示django代码?

```
setting -> Languages & Frameworks -> python Template Languages选择Django
```

### django模板语言的一些稀有特性

- 判断用户是否登录

```django
{% if request.user.is_authenticated %}
```

```python
{% request.path | slice:7 == 'something'%}
# 获取url的想对路径,比如:http:localhost:8000/course/list
得到的是 /course/list, 然后通过过滤器slice获取前7位得到course
```

- 使用`request.user.`获取数据库的字段

````django
request.user.name  ===>获取当前用户的名字
{% request.user.birthday %}
````

- 在模板中给值为none的字段填充一个默认值

```
{%  request.user.birthday| default_if_none: ''  %}
```

 	

### 用户注册和发送邮件

- [用户注册和发送邮件](https://blog.csdn.net/brynao/article/details/76268725)



### django文档

- [django-1.11文档](https://yiyibooks.cn/xx/Django_1.11.6/contents.html)




### django第三方库的文档及使用方法

- [django分页](https://pypi.python.org/pypi/django-pure-pagination)

  ​

### django的Ajax技巧

- 无需通过表单名字就可以获取到表单的数据,如下:

```
<form class="rightform" id="jsStayForm">
```

```javascript
console.log($('#jsStayForm').serialize())

//name=%E6%98%AF%E7%9A%84&mobile=121212&course_name=1212121&csrfmiddlewaretoken=NGVks6TAedrFZ1UBkWr98i8p6CmNZywN
```

- 后台可以通过post方法获取值


##### 1.ajax提交到后台并在后台返回JSON数据

- ajax代码

```js
<script>
    $(function(){
        $('#jsStayBtn').on('click', function(){
            $.ajax({
                cache: false,
                type: "POST",
                dataType:'json',
                url:"{% url 'org:user_ask' %}",
                data:$('#jsStayForm').serialize(),
                success: function(data) {
                    if(data.status == 'success'){
                        $('#jsStayForm')[0].reset();// 重置表单
                        alert("提交成功")
                    }else if(data.status == 'fail'){
                        $('#jsCompanyTips').html(data.msg)
                    }
                },
            });
        });
    })

</script>
```

- 后台接收代码如下:

```python
import json

class UserAskView(View):
    def post(self, request):
        user_ask_form = UserAskForm(request.POST)
        if user_ask_form.is_valid():
            user_ask_form.save(commit=True)
            json_return = {'status': 'success'}
            return HttpResponse(json.dumps(json_return), content_type="application/json")
        else:
            json_str = {'status': 'fail', 'msg': user_ask_form.errors}
            return_json = json.dumps(json_str)
            return HttpResponse(return_json, content_type='application/json')

```

- 发送之前将`csfr_token`发送出去

```js
   $.ajax({
        cache: false,
        type: "POST",
        url:"",
        data:{'fav_id':fav_id, 'fav_type':fav_type},
        async: true,
        beforeSend:function(xhr, settings){
            xhr.setRequestHeader("X-CSRFToken", "{{ csrf_token }}");
        },
        success: function(data) {
            if(data.status == 'fail'){
                if(data.msg == '用户未登录'){
                    window.location.href="/login/";
                }else{
                    alert(data.msg)
                }

            }else if(data.status == 'success'){
                current_elem.text(data.msg)
            }
        },
    });
```






















