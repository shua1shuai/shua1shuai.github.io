# day08 Django基础

django，web框架，别人写好了一些代码，我们在他的基础实现网站。

![image-20220511090615700](assets/image-20220511090615700.png)

Python中常见Web框架：

- Django，大而全，内部为我们提供了很多方便的组件，直接调用（积极支持异步非阻塞）
- Flask，小而精，自己内部提供的少+第三方组件。
- tornado/sanic/fastapi，小而精，自己内部提供的少+第三方组件 + 异步非阻塞



## 1.环境的搭建

```
pip install django==3
```

```
C:\Python39
	scripts
		- pip.exe
		- django-admin.exe    -> 搭建django项目
	Lib
		site-packages
			- django
			- requests
	python.exe
```

```
C:\Python39\Scripts\django-admin.exe   startproject  项目名称
```

```
django-admin  startproject  项目名称
```



### 1.1 创建项目

```
django-admin startproject mysite
```

```
mysite
├── manage.py           [管理项目文件，例如：运行、类自动生成数据表]
└── mysite
    ├── __init__.py
    ├── settings.py     [项目配置文件，例如：连接那个数据... ]
    ├── urls.py         [根路由，URL和函数的对应关系  /x1/login ->do_login ]
    ├── asgi.py         [异步运行项目，编写socket，处理网络请求]
    └── wsgi.py         [同步运行项目，编写socket，处理网络请求]
```





### 1.2 快速上手

urls.py

```python
from django.contrib import admin
from django.urls import path
from django.shortcuts import HttpResponse

def login(request):
    return HttpResponse("登录页面")


urlpatterns = [
    path('admin/', admin.site.urls),
    path('login/', login),
]
```



### 1.3 快速启动

网站启动起来，通过浏览器就可以访问。

- 打开终端并进入项目根目录（看到manage.py）

- 执行命令，启动网站

  ```
  python manage.py runserver 127.0.0.1:8000
  python manage.py runserver
  ```

![image-20220511093726547](assets/image-20220511093726547.png)

### 1.4 Pycharm

```
>>>pip install django==3
```

- 创建项目
- 启动项目



#### 1.4.1 创建项目

![image-20220511094243187](assets/image-20220511094243187.png)

![image-20220511094354137](assets/image-20220511094354137.png)



#### 1.4.2 可能BUG

是由于pycharm导致。

![image-20220511095332242](assets/image-20220511095332242.png)



#### 1.4.3 编写

![image-20220511095456903](assets/image-20220511095456903.png)



#### 1.4.4 启动项目

![image-20220511095629332](assets/image-20220511095629332.png)





### 1.5 不专业

![image-20220511100423106](assets/image-20220511100423106.png)



### 1.6 APP

在django项目中创建app，在app中编写项目中的具体业务。

```
day08
├── manage.py           [管理项目文件，例如：运行、类自动生成数据表]
└── day08
    ├── __init__.py
    ├── settings.py     [项目配置文件，例如：连接那个数据... ]
    ├── urls.py         [根路由，URL和函数的对应关系  /x1/login ->do_login ]
    ├── asgi.py         [异步运行项目，编写socket，处理网络请求]
    └── wsgi.py         [同步运行项目，编写socket，处理网络请求]
└── web，网站
    ├── __init__.py
    ├── admin.py        [内部后台管理的配置，不要懂]
    ├── apps.py         [App名字，不要动]
    ├── migrations      [迁移记录，不要修改他，自动生成]
    │   └── __init__.py
    ├── models.py       [数据库，类->SQL语句（ORM）]        【经常使用】
    ├── tests.py        [单元测试，不要动]
    └── views.py        [视图函数,do_login]               【经常使用】
```

```
python3.9 manage.py startapp web
```

![image-20220511101638677](assets/image-20220511101638677.png)

![image-20220511101657141](assets/image-20220511101657141.png)





### 小结

- 安装django框架

  ```
  pip install django==3
  ```

- 创建项目

  ```
  day08
  ├── manage.py           [管理项目文件，例如：运行、类自动生成数据表]
  └── day08
      ├── __init__.py
      ├── settings.py     [项目配置文件，例如：连接那个数据... ]
      ├── urls.py         [根路由，URL和函数的对应关系  /x1/login ->do_login ]
      ├── asgi.py         [异步运行项目，编写socket，处理网络请求]
      └── wsgi.py         [同步运行项目，编写socket，处理网络请求]
  ```

  - 命令

    ```
    django-admin startproject 项目名
    ```

  - Pycharm

- 创建app

  ```
  python3.9 manage.py startapp web
  ```

  ```
  day08
  ├── manage.py           [管理项目文件，例如：运行、类自动生成数据表]
  └── day08
      ├── __init__.py
      ├── settings.py     [项目配置文件，例如：连接那个数据... ]
      ├── urls.py         [根路由，URL和函数的对应关系  /x1/login ->do_login ]
      ├── asgi.py         [异步运行项目，编写socket，处理网络请求]
      └── wsgi.py         [同步运行项目，编写socket，处理网络请求]
  └── web，网站
      ├── __init__.py
      ├── admin.py        [内部后台管理的配置，不要懂]
      ├── apps.py         [App名字，不要动]
      ├── migrations      [迁移记录，不要修改他，自动生成]
      │   └── __init__.py
      ├── models.py       [数据库，类->SQL语句（ORM）]        【经常使用】
      ├── tests.py        [单元测试，不要动]
      └── views.py        [视图函数,do_login]               【经常使用】
  ```

- 编写业务代码

  - urls.py

    ```python
    from django.contrib import admin
    from django.urls import path
    from web.views import login
    
    urlpatterns = [
        path('admin/', admin.site.urls),
        path('login/', login),
    ]
    ```

  - views.py

    ```python
    from django.shortcuts import HttpResponse
    
    
    def login(request):
        return HttpResponse("登录页面")
    ```

- 启动项目

  - 命令

    ```
    python3.9 manage.py runserver 
    ```

  - Pycharm



## 2.初识视图函数

```python
from django.contrib import admin
from django.urls import path
from web.views import login

urlpatterns = [
    path('login/', login),
]
```

```python
from django.shortcuts import HttpResponse

def login(request):
    
    # ...例如：用户名、密码  -> 数据库校验
    
    return HttpResponse("登录页面")
```

- request是什么？用户请求相关的所有内容。

  ```
  去request中获取用户提交的数据等信息
  ```

- 中间，业务逻辑操作

- 返回值，返回的什么体现用户浏览器的行为不同。

  - `return HttpResponse("登录页面")`
  - `return render(request, "login.html")`
  - `return redirect("https://www.baidu.com")`



如果开发中用到了`return render(request, "login.html")` 寻找HTML模板：

- 根目录下的templates中找【优先】

  ```python
  TEMPLATES = [
      {
          'BACKEND': 'django.template.backends.django.DjangoTemplates',
          'DIRS': [os.path.join(BASE_DIR, 'templates')],
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

- 根据app的注册顺序，逐一去每个app目录下templates文件夹中寻找

  ```python
  INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      "web.apps.WebConfig"
  ]
  ```

  

### 小结

- 参数，去request中获取值

- 中间，...

- 返回值

  - settings.py

    ```python
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        "web.apps.WebConfig"
    ]
    
    ...
    
    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [os.path.join(BASE_DIR, 'templates')],
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

  - 单独app的模板，在app中写； 公共的就在最外层的templates中写HTML模板。



## 3.初识模板

web框架中都要用到模板的语法，用看的值是动态的。

```python
def user_list(request):
    # 1.数据库获取所有的用户列表
    data = ["武沛齐", "李立权", "张弛"]

    mapping = {"name": "武沛齐", "age": 19, "size": 18}

    # 2.打开文件并读取内容
    # 3.模板的渲染 -> 文本替换
    return render(request, "user_list.html", {"message": "标题来了", "data_list": data, "xx": mapping})

```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>{{ message }}</h1>
<ul>
    {% for item in data_list %}
        <li>{{ item }}</li>
    {% endfor %}
</ul>
<a>{{ data_list.0 }}</a>
<a>{{ data_list.1 }}</a>
<a>{{ data_list.2 }}</a>

<p>{{ xx.name }}</p>
<p>{{ xx.age }}</p>
<p>{{ xx.size }}</p>
<ul>
    {% for item in xx.keys %}
        <li>{{ item }}</li>
    {% endfor %}
</ul>

<hr/>

<ul>
    {% for item in xx.values %}
        <li>{{ item }}</li>
    {% endfor %}
</ul>

<hr/>
<ul>
    {% for k,v in xx.items %}
        <li>{{ k }}   {{ v }}</li>
    {% endfor %}
</ul>

</body>
</html>
```



## 案例：号码列表

- URL访问
- 去数据库获取号码列表
- 页面上展示

![image-20220511111746057](assets/image-20220511111746057.png)

![image-20220511111812195](assets/image-20220511111812195.png)

![image-20220511111825229](assets/image-20220511111825229.png)

![image-20220511111833728](assets/image-20220511111833728.png)



## 4.静态文件处理

图片、css、js等。

- 静态文件放在app目录下  static 文件夹中

- 页面中使用

  ```html
  {% load static %}
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <link rel="stylesheet" href="{% static 'bootstrap-3.4.1/css/bootstrap.min.css' %}">
  </head>
  <body>
  <div class="container">
      <h1>号码列表</h1>
  	...
      <script src="{% static 'jquery-3.6.0.min.js' %}"></script>
      <script src="{% static 'bootstrap-3.4.1/js/bootstrap.min.js' %}"></script>
  </div>
  </body>
  </html>
  ```

  

## 案例：登录&跳转

![image-20220511134219856](assets/image-20220511134219856.png)

- 移除

  ```python
  MIDDLEWARE = [
      'django.middleware.security.SecurityMiddleware',
      'django.contrib.sessions.middleware.SessionMiddleware',
      'django.middleware.common.CommonMiddleware',
      #'django.middleware.csrf.CsrfViewMiddleware',
      'django.contrib.auth.middleware.AuthenticationMiddleware',
      'django.contrib.messages.middleware.MessageMiddleware',
      'django.middleware.clickjacking.XFrameOptionsMiddleware',
  ]
  ```

- 生成token

  ```html
  <div class="login-box">
      <h2>用户登录</h2>
      <form method="post" action="/login/">
          {% csrf_token %}
          <div class="form-group">
              <label>用户名</label>
              <input type="text" class="form-control" placeholder="请输入用户名" name="user">
          </div>
          <div class="form-group">
              <label>密码</label>
              <input type="password" class="form-control" placeholder="请输入密码" name="pwd">
          </div>
          <button type="submit" class="btn btn-primary">提 交</button>
          <span style="color: red;">{{ error }}</span>
      </form>
  </div>
  ```

  

## 5.ORM

ORM，对象关系映射。

```python
class UserInfo:
    id = IntegerField
    name = CharField
    age = IntegerField
    email = CharField
```

```
obj1 = UserInfo(id=x,name=x,age=x,email=x)
obj2 = UserInfo(id=x,name=x,age=x,email=x)
obj3 = UserInfo(id=x,name=x,age=x,email=x)
obj4 = UserInfo(id=x,name=x,age=x,email=x)
```



出现的目的：便于项目中对数据库进行操作。

- 创建表机构 & 修改表结构。
- 表中的数据进行操作。



### 5.1 自己创建数据库

![image-20220511141821859](assets/image-20220511141821859.png)



### 5.2 创建表

去app下的models.py中创建指定的类 + 命令，自动创建表。

#### 5.2.1 编写类

```python
from django.db import models


class UserInfo(models.Model):
    name = models.CharField(verbose_name="姓名", max_length=16)  # varchar
    age = models.IntegerField(verbose_name="姓名")  # int
    email = models.CharField(verbose_name="邮箱", max_length=32)  # varchar
```

![image-20220511142312246](assets/image-20220511142312246.png)



#### 5.2.2 命令

- 先连接数据库：day08

  ```python
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.mysql',
          'NAME': 'day08',
          'USER': 'root',
          'PASSWORD': 'root123',
          'HOST': '127.0.0.1',
          'PORT': 3306,
      }
  }
  ```

- python代码连接数据库：pymysql、mysqlclient

  ```
  pip3.9 install mysqlclient
  ```

  



接下来，再去执行以下命令：

```
python3.9 manage.py makemigrations
python3.9 manage.py migrate
```

- makemigrations，读取已经注册所有的app中的models.py文件，根据类生成配置文件并放到app下的migrations目录

- migrate，根据配置文件自动生成相应的SQL语句。

  ```
  create table demo_userinfo(
  	id int ....,
  	name ..,
  	age ..,
  	email ..
  )
  ```

  

#### 小结

- 自己创建数据库

- django配置连接数据库

  ```python
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.mysql',
          'NAME': 'day08',
          'USER': 'root',
          'PASSWORD': 'root123',
          'HOST': '127.0.0.1',
          'PORT': 3306,
      }
  }
  ```

- python操作msyql模块

  ```
  pip3.9 install mysqlclient
  ```

- models.py【经常】

  ```python
  from django.db import models
  
  
  class UserInfo(models.Model):
      name = models.CharField(verbose_name="用户名", max_length=16)  # varchar
      pwd = models.CharField(verbose_name="密码", max_length=64) # varchar
      age = models.IntegerField(verbose_name="姓名")  # int
      email = models.CharField(verbose_name="邮箱", max_length=32)  # varchar
  
  
  class Department(models.Model):
      caption = models.CharField(verbose_name="标题", max_length=32)
  ```

- 命令【经常】

  ```python
  python3.9 manage.py makemigrations
  python3.9 manage.py migrate
  ```

  

### 5.3 数据操作

```python
# models.py

from django.db import models


class UserInfo(models.Model):
    name = models.CharField(verbose_name="用户名", max_length=16)  # varchar
    pwd = models.CharField(verbose_name="密码", max_length=64) # varchar
    age = models.IntegerField(verbose_name="姓名")  # int
    email = models.CharField(verbose_name="邮箱", max_length=32)  # varchar
```

- 新增

  ```python
  models.UserInfo.objects.create(name="wupeiqi",pwd="123",age=19,email='xxx@live.com')
  
  models.UserInfo.objects.create(**{"name":"wupeiqi","pwd":"123","age":19,"email":"xxx@live.com"})
  ```

- 查询

  ```python
  # queryset=[ obj,obj,obj,obj ]     obj.id  obj.name  obj.age  obj.pwd    []
  v1 = models.UserInfo.objects.filter(name="wupeiqi",age=19)
  
  
  # queryset=[ obj,obj,obj,obj ]     obj.id  obj.name  obj.age  obj.pwd   []
  v2 = models.UserInfo.objects.all()
  
  
  # obj        obj.id  obj.name
  v3 = models.UserInfo.objects.filter(name="wupeiqi",age=19).first()
  # 注意：未查询到数据时候返回None
  ```

- 删除

  ```python
  models.UserInfo.objects.all().delete()
  
  models.UserInfo.objects.filter(name="wupeiqi",age=19).delete()
  ```

- 修改

  ```python
  models.UserInfo.objects.all().update(age=19)
  
  models.UserInfo.objects.filter(id=10).update(age=19)
  ```

  





## 案例：部门信息

![image-20220511145938903](assets/image-20220511145938903.png)

![image-20220511150553058](assets/image-20220511150553058.png)

![image-20220511150613726](assets/image-20220511150613726.png)

![image-20220511151336175](assets/image-20220511151336175.png)















## 总结

- Django框架

  ```
  pip install django==3
  ```

- 创建项目

- 配置

  - 注册App
  - MySQL连接（数据库先创建）

- 在app目录下的models.py中创建表结构

  - 写models
  - 命令

- 写功能代码

  - urls.py
  - views.py 【基于ORM对数据库中的表数据进行操作】
  - templates

- 静态文件配置（CSS、JS、图片）















































































































