# Django 学习过程记录

参考链接：https://docs.djangoproject.com/zh-hans/3.0/intro/tutorial02/

# 安装Django

Terminal中

```python
pip install django
```



## 验证

```python
import django
print(django.get_version())
```



# Django简介

Django采用MVT设计模式

MVT设计模式：

M:model 模型

V:View 视图

T:Template 模版



创建完项目后，在项目同名的project目录内有一个**settings.py** 文件，这个配置文件用于配置和管理Django项目的运维信息。

settings.py配置文件中的所有配置项都是大写的，项目创建时，就初始化了一些默认配置，这些默认配置承载着最基础的项目信息。

其中常用的配置项有：

  DATABASES ：数据库配置

  TEMPLATES：配置HTML页面的模板地址templates

  STATICFILES_DIRS ：配置静态文件

  MIDDLEWARE ：配置中间件

  DEBUG：默认为True，项目上线时改为False

  ALLOWED_HOSTS：限定请求中的host值



# 查看版本

```
python -m django --version
```

python -m用来执行Python模块的命令

django是要执行的模块名

--version是该模块对应的参数，表示输出Django的版本号



## cmd常见参数

一些比较常见的参数

`startproject`: 创建一个新的Django项目。

`startapp`: 在当前项目中创建一个新的Django应用程序。

`runserver`: 启动Django开发服务器，用于开发和测试。

`makemigrations`: 生成数据库迁移文件，用于修改数据库模型。

`migrate`: 执行数据库迁移，将数据库模式更新到最新版本。

`shell`: 启动Django shell，用于交互式地执行Python代码。

`test`: 运行Django测试套件，用于自动化测试。



## project与app区别

startproject与startapp的区别：

- `startproject`用于创建一个新的Django项目，它会在指定的目录下创建一个包含一些默认文件和目录的项目结构，包括`settings.py`、`urls.py`、`wsgi.py`等文件。一个Django项目可以包含多个应用程序。
- `startapp`用于在当前Django项目中创建一个新的应用程序，它会在指定的目录下创建一个包含一些默认文件和目录的应用程序结构，包括`models.py`、`views.py`、`urls.py`等文件。一个Django应用程序通常是一个特定功能的模块

startproject用于创建整个Django项目的基础结构，startapp用于创建单个应用程序的基础结构



# 创建项目

terminal中进入目录

执行

```
django-admin startproject mysite
```



django和django-admin的区别：

Django是一个Web框架

django-admin是Django框架自带的命令行工具





将会在当前目录下创建一个 `mysite` 目录

创建后的目录结构：

![image-20230428162901329](/Users/lidawei/Library/Application Support/typora-user-images/image-20230428162901329.png)

## 目录文件

- 最外层的 `mysite/` 根目录只是项目的容器， 根目录名称对Django没有影响，可以将它重命名为任何名称。
- manage.py对应的文档地址：https://docs.djangoproject.com/zh-hans/3.0/ref/django-admin/
- 子目录mysite是一个纯python包
- `mysite/__init__.py`：一个空文件，告诉 Python 这个目录应该被认为是一个 Python 包
- `mysite/settings.py`是项目的配置文件，对应的文档地址：https://docs.djangoproject.com/zh-hans/3.0/topics/settings/
- `mysite/urls.py`：Django 项目的 URL 声明，对应的文档地址：https://docs.djangoproject.com/zh-hans/3.0/topics/http/urls/
- `mysite/asgi.py`：项目运行在 ASGI 兼容的Web服务器上的入口，
- `mysite/wsgi.py`：项目的运行在 WSGI 兼容的Web服务器上的入口



ASGI和WSGI都是Python Web应用程序的接口规范，用于定义Web服务器和Web应用程序之间的通信协议

WSGI（Web Server Gateway Interface）

ASGI（Asynchronous Server Gateway Interface）

WSGI适用于传统的同步Web应用程序，ASGI是WSGI的升级版，它支持异步处理请求和响应，适用于异步Web应用程序



# 启动django服务器

```
python manage.py runserver
```

默认为8000端口

更换端口

```
python manage.py runserver 8080
```

更换ip及端口

```
python manage.py runserver 0:8000
```



用于开发的服务器在需要的情况下会对每一次的访问请求重新载入一遍 Python 代码。所以你不需要为了让修改的代码生效而频繁的重新启动服务器。然而，一些动作，比如添加新文件，将不会触发自动重新加载，这时你得自己手动重启服务器。



# 创建应用

```
python manage.py startapp polls
```

创建后的目录结构

![image-20230428165219130](/Users/lidawei/Desktop/assets/image-20230428165219130.png)



# 编写视图

```
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```



# url映射

<u>创建视图之后需要将一个url映射到它</u>, 此时需要使用URLconf，对应为urls.py文件

## app中的映射

在app中新建urls.py

```
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

path的参数格式：

```
path(route, view, kwargs=None, name=None)
```

* route：一个字符串，表示URL模式。可以包含变量和正则表达式。

- 
  view：一个视图函数或类的名称或引用。
- kwargs：一个字典，包含额外的参数传递给视图函数或类。例如，{'id': 1}表示将id=1作为参数传递给视图函数。
- name：一个可选的URL名称，用于在模板中引用URL。例如，name='article_detail'表示将URL命名为article_detail，可以在模板中使用{% url 'article_detail' %}引用该URL。



## project中的映射

```
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```

需要在初始代码中额外import了include函数

函数参数

```
include(module, namespace=None)
```

- module：一个URLconf模块的名称或路径，可以是一个字符串或者一个Python模块对象。例如，'myapp.urls'表示引用myapp应用程序中的urls.py文件中的URL模式。
- namespace：一个可选的命名空间，用于在模板中引用包含的URL模式。例如，namespace='myapp'表示将包含的URL模式命名为myapp，可以在模板中使用{% url 'myapp:article_detail' %}引用该URL。

include函数只是将其他URLconf模块中的URL模式包含到当前URLconf中，不会对URL模式进行修改。因此，包含的URL模式可以使用与当前URLconf相同的命名空间和前缀。

当包括其它 URL 模式时应该**总是**使用 `include()` ， `admin.site.urls` 是唯一例外。



## 效果

启动服务后进入url：

http://127.0.0.1:8082/polls/

效果如下

![image-20230428172055640](/Users/lidawei/Desktop/assets/image-20230428172055640.png)



# 配置文件

配置文件对应`settings.py`文件

文件中的 `INSTALLED_APPS`默认包括了以下 Django 的自带应用

```
INSTALLED_APPS = [
    'django.contrib.admin', 管理员站点
    'django.contrib.auth', 认证授权系统
    'django.contrib.contenttypes', 内容类型框架
    'django.contrib.sessions', 会话框架
    'django.contrib.messages', 消息框架
    'django.contrib.staticfiles', 管理静态文件的框架
]
```

使用

```
python manage.py migrate
```

检查`INSTALLED_APPS`的设置，为其中的每个应用创建需要的数据表，至于具体会创建什么，这取决于 `mysite/settings.py` 设置文件和每个应用的数据库迁移文件

 `migrate`命令只会为在 `INSTALLED_APPS`里声明了的应用进行数据库迁移



# 数据库驱动的Web应用

Django 里写一个数据库驱动的 Web 应用的第一步是定义模型：也就是数据库结构设计和附加的其它元数据



对于一个投票应用，需要创建两个模型：问题 `Question` 和选项 `Choice`。`Question` 模型包括问题描述和发布时间。`Choice` 模型有两个字段，选项描述和当前得票数。每个选项属于一个问题。

这些概念可以通过一个 Python 类来描述

```
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

每个模型都继承django.db.models.Model

`django.db.models.Model`是Django中用于定义模型的基类。它是一个抽象类，用于定义数据库表结构和数据操作方法。

每个模型的类变量都表示模型里的一个数据库字段



通过上述代码，Django可以为这个应用创建数据库 schema（生成 `CREATE TABLE` 语句），创建可以与 `Question` 和 `Choice` 对象进行交互的 Python 数据库 API。



在INSTALLED_APPS中添加polls的设置

```
'polls.apps.PollsConfig'
```



执行

```
python manage.py makemigrations polls
```

通过运行 `makemigrations` 命令，Django 会检测对模型文件的修改，并且把修改的部分储存为一次 **迁移**。

迁移是 Django 对于模型定义（也就是你的数据库结构）的变化的储存形式 - 是一些磁盘上的文件。

模型的迁移数据存储在migrations中

![image-20230428175632691](/Users/lidawei/Desktop/assets/image-20230428175632691.png)



自动执行数据库迁移并同步管理数据库结构

```
python manage.py sqlmigrate polls 0001
```

```
BEGIN;
--
-- Create model Question
--
CREATE TABLE "polls_question" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "question_text" varchar(200) NOT NULL, "pub_date" datetime NOT NULL);
--
-- Create model Choice
--
CREATE TABLE "polls_choice" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "choice_text" varchar(200) NOT NULL, "votes" integer NOT NULL, "question_id" bigint NOT NULL REFERENCES "polls_question" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE INDEX "polls_choice_question_id_c5b4b260" ON "polls_choice" ("question_id");
COMMIT;

```



sqlmigrate命令并没有真正在数据库中执行迁移，只是把命令输出到屏幕上，看Django认为需要执行哪些SQL语句



```
python manage.py check
```

检查项目中的问题，检查过程中不会对数据库进行任何操作



再次执行migrate在数据库里创建定义的模型的数据表

该命令选中所有还没有执行过的迁移，并应用在数据库上



总结：

改变模型的步骤：

- 编辑 `models.py` 文件，改变模型。
- 运行 `python manage.py makemigrations` 为模型的改变生成迁移文件。
- 运行 `python manage.py migrate`来应用数据库迁移。



# 管理界面

创建登录管理页面的用户



在admin中进行注册：

```
from .models import Question
admin.site.register(Question)
```

单机后即可看到"Questions" 对象的列表 "change list" 并进行修改