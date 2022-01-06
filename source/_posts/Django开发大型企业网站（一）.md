---
title: Django开发大型企业网站（一）
date: 2019-11-15 14:57:20
tags:
- Django
copyright: true
categories: python
mathjax: true
---

**前言**

> 这篇博客的目的是通过python的web框架Django来搭建一个大型的企业网站。学习的课程来源于b站：https://www.bilibili.com/video/av60229021?p=6

<!-- more -->

## 介绍

### web服务器和应用服务器以及web应用框架

* **web服务器**：负责处理http请求，响应静态文件，常见的由Apache，Nginx以及微软的IIS
* **应用服务器**：负责处理逻辑的服务器。比如php、python的代码，是不能直接通过nginx这种web服务器来处理的，只能通过应用服务器来处理，常见的应用服务器由uwsgi、tomcat等。
* **web应用框架**：一般使用某种语言，封装了常用的web功能的框架就是web应用框架，flask、Django以及java中的SSH框架都是web应用框架。

### URL组成部分

URL即**统一资源定位符**。一个url由以下几个部分组成：

```python
scheme://host:post/path/?query-string=xxx#anchor
```

* **scheme**：代表的是访问的协议，一般为http或者https以及ftp等
* **host**：主机名，域名，比如：www.baidu.com
* **post**：端口号，当你访问一个网站的时候，浏览器默认使用80端口
* **path**：查找路径。比如：www.jianshu.com/trending/now ，后面的trending/now就是path
* **query-string**：查询字符串，比如：www.baidu.com/s?wd=python ，后面的wd=python就是查询字符串。
* **anchor**：锚点，后台一般不用管，前端用来做网页定位的

注意：URL中的所有字符串都是ASCII字符串，如果出现非ASCII字符串，比如中文，浏览器会进行编码再进行传输。

## 第一个Django项目

### 安装虚拟环境和Django

1、安装虚拟环境

打开cmd，在命令行中输入`mkvirtualenv django-env`，这样便在我们设置的默认路径中创建了一个名为django-env的虚拟环境

2、安装Django

在cmd中输入`workon django-env`来进入我们创建的虚拟环境，当然，如果当时创建的话，创建完就进入虚拟环境了，然后再输入`pip install django`来安装django

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Django%E5%BC%80%E5%8F%91%E5%A4%A7%E5%9E%8B%E4%BC%81%E4%B8%9A%E7%BD%91%E7%AB%99/%E5%AE%89%E8%A3%85django.png)

### 创建一个Django项目

#### 命令行方式

1. 创建项目：cmd首先workon进入django的虚拟环境（[python建虚拟环境](https://xiyouhujing.github.io/2019/12/05/%E5%88%9B%E5%BB%BApython%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83/)），然后输入`django-admin startproject first_project`命令，则在相应的目录下创建了一个名为`first_project`的Django项目，例如，我的项目路径为：`F:\DjangoProject\python_django\project01`。在sublime text中打开我们的项目，可以看到如下的项目结构：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Django%E5%BC%80%E5%8F%91%E5%A4%A7%E5%9E%8B%E4%BC%81%E4%B8%9A%E7%BD%91%E7%AB%99/%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84.png)

2. 创建应用（app）：一个项目类似于一个架子，但是真正起作用的是app，在终端进入项目所在的路径，然后用命令`python manage.py startapp [app名称]`创建一个app

#### 用pycharm创建

在pycharm页面中选择【File】->【New project】->【Django】

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Django%E5%BC%80%E5%8F%91%E5%A4%A7%E5%9E%8B%E4%BC%81%E4%B8%9A%E7%BD%91%E7%AB%99/pycharm%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE.png)

pycharm中可以在建django项目的同时新建虚拟环境，不用我们用virtualenvwrappe命令来新建，也可以选择已存在的环境，由于我已经用命令行新建了虚拟环境，所以直接选择就好。之后点击`create`，便创建了新的django项目，目录文件和我们用刚才用命令创建的项目相同。

### 运行项目

1. 命令行运行

然后进入我们的项目文件夹`first_project`输入命令`python manage.py runserver`来运行我们的项目，出现如下界面则表示运行成功：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Django%E5%BC%80%E5%8F%91%E5%A4%A7%E5%9E%8B%E4%BC%81%E4%B8%9A%E7%BD%91%E7%AB%99/Django%E6%88%90%E5%8A%9F%E8%BF%90%E8%A1%8C.png)

2. python中运行

点击pycharm右上角的绿色三角符号。**注意：在pycharm中运行项目，要避免一个项目运行多次**，在项目配置中，把“只用单一实例”的选项勾选上避免多次运行的问题。

3. 运行成功浏览器界面

红色框起来的是我们要在浏览器中需要访问的url，在浏览器中输入：http://127.0.0:8000/ ，出现如下界面就表示django没有问题：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Django%E5%BC%80%E5%8F%91%E5%A4%A7%E5%9E%8B%E4%BC%81%E4%B8%9A%E7%BD%91%E7%AB%99/%E6%B5%8F%E8%A7%88%E5%99%A8%E7%95%8C%E9%9D%A2.png)

### 改变端口号

1. 在终端：运行的时候加上一个端口号就可以了，命令为`python manage.py runserver 9000`
2. 在pycharm中：右上角->【Edit configurations】->【port】，改成你想要的端口号

### 让同局域网中的其他电脑访问本机项目

1. 让项目运行的时候，host改为0.0.0.0
   * 在终端，使用命令`python manage.py runserver 0.0.0.0:8000`
   * 在pychram中，右上角->【Edit configurations】->【host】，改为`0.0.0.0`
2. 在项目文件夹下的`settings.py`文件中，配置`ALLOWED_HOSTS`，将本机的ip地址添加进去。**注意：要关闭自己电脑的防火墙才行**

### 项目结构介绍

1. `manage.py`：以后和项目交互基本上都是基于这个文件，一般都是在线输入`python manage.py [命令]`，可以通过`python manage.py help`可以查看由哪些命令，都是什么命令。
2. `settings.py`：保存项目的配置信息，以后所有和项目相关的配置都是放在这个里面的。
3. `urls.py`：这个文件是用来配置URL路由的。以后来了一个请求，就会从这个文件中找到匹配的试图函数。
4. `wsgi.py`：项目与WSGI协议兼容的web服务器入口，部署的时候需要用到，一般情况下不需要修改。

### DEBUG模式

开启debug模式，修改项目文件夹下的setting.py，找到DEBUG，修改为`DEBUG=True`。

1. 如果开启了degug模式，那么以后我们修改了django项目的代码代码，然后按下ctrl+s，那么django就会自动的给我们重启项目，不需要手动重启。
2. 如果开启了debug模式，那么以后django项目中的代码出现bug了，那么在浏览器中和控制台会打印出错信息。
3. 在生产环境中，禁止开启debug模式，不然又很大的安全隐患。

关闭debug模式，修改为`DEBUG=False`。关闭了之后，就必须设置`ALLOWED_HOSTS`变量，这个变量是用来设置以后别人只能通过这个变量中的IP地址或者域名来进行访问。

## 视图与URL

### 视图函数

视图函数一般都写在`app`的`views.py`中，并且视图中的第一个参数永远都是`request`（一个HttpRequest）对象。这个对象存储了请求过来的所有信息，包括携带的参数以及一些头部信息等。在视图中，一般都是完成逻辑相关的操作。比如这个请求时添加一篇博客，那么可以通过request来接收这些数据，然后存储到数据库中，最后再把执行的结果返回给浏览器。视图函数的返回结果必须时`HttpResponseBase`对象或者子类的对象，示例代码如下：

```python
from django.http import HttpResponse
def book_list(request):
    return HttpResponse("图书列表")
```

### URL映射

1. 因为在`setting.py`文件中配置了`ROOT_URLCONF`为`urls.py`，所以会去`urls.py`中寻找url映射
2. 在`urls.py`中我们所有的映射，都应该放在`urlpatterns`这个变量中。
3. 所有的映射不是随便写写的，而是使用`path`函数或者`re_path`函数进行包装的。

### URL添加参数

1. 采用在url中使用变量的方式：在path的第一个参数中，使用`<参数名>`的方式可以传递参数。然后在视图函数中也要写一个参数，视图函数中的参数必须和url中的参数名称保持一致，不然就找不到这个参数，另外，url中可以传递多个参数。`urls.py`中示例代码如下：

   ```python
   urlpatterns = [
       path('admin/', admin.site.urls),
       path('', index),
       path('book/', views.book),
       path('book/detail/<book_id>/<category_id>/', views.book_detail),
   ]
   ```

   `views.py`中示例代码如下：

   ```python
   def book_detail(request, book_id, category_id):
       text = "您获取的图书id是：%s，图书分类是%s" % (book_id, category_id)
       return HttpResponse(text)
   ```

   

2. 采用查询字符串的方式：在url中不需要单独的匹配查询字符串的部分，只需要在视图函数中使用`request.GET.get('参数名称')`的方式来获取，`urls.py`中示例代码如下：

   ```python
   urlpatterns = [
       path('admin/', admin.site.urls),
       path('', index),
       path('book/', views.book)，
       path('book/author/', views.author_detail),
   ]
   ```

   `views.py`中示例代码如下：

   ```python
   def author_detail(request):
       author_id = request.GET.get('id')
       text = "作者的id是：%s" % author_id
       return HttpResponse(text)
   ```

   因为查询字符串使用的是`GET`请求，所以我们通过`request.GET`来获取，并且因为`GET`是一个类似于字典的数据类型，所以获取值跟字典的方式都是一样的。

   以后在访问的时候可以通过`/book/author/?id=1`即可将参数传递过去

###  URL参数的转换器

1. str：除了斜杠`/`以外所有的字符都是可以的
2. int：只有是一个或者多个的阿拉伯数字
3. path：所有的字符都是满足的
4. uuid：只有满足`uuid.uuid4()`这个函数返回的字符串格式
5. slug：英文中的横杠或者英文字符或者阿拉伯数字或者下划线才满足

### URLS模块化

如果项目变得越来越大，那么url会变得越来越多，如果都放在主`urls.py`文件中，那么将会不太好管理，因此我们可以将每个app自己的urls放到自己的app中进行管理，一般我们会在app中新建一个`urls.py`文件用来存储所有和这个app相关的子url。需要注意的地方：

1. 应该使用`include`函数包含子`urls.py`，并且这个`urls.py`的路径是相对于项目的路径。

   项目路径下的`urls.py`示例代码如下：

   ```python
   urlpatterns = [
       path('admin/', admin.site.urls),
       path('book/', include('book.urls')),
   ]
   ```

2. 在`app`的`urls.py`中，所有的url匹配也要放在一个叫做`urlpatterns`的变量中，否则找不到，`app`路径下新建的`urls.py`示例代码如下：

   ```python
   urlpatterns = [
       path('', views.book),
       path('detail/<book_id>/', views.book_detail),
       path('list/', views.book_list),
   ]
   ```

3. `url`是会根据主`urls.py`和app中的`urls.py`进行拼接的，因此注意不要多加斜杠。

### URL命名

#### 为什么需要url命名

因为url是经常变化的，如果在代码中写死可能会经常改代码，给url取个名字，以后使用url的时候就使用它的名字进行反转就可以了，就不需要写死url了。

#### 如何给一个url指定名称

在`path`函数中，传递一个`name`参数就可以指定了，示例代码如下：

```python
urlpatterns = [
    path('', views.index, name='index'),
    path('login/', views.login, name='login'),
]
```

#### 应用命名空间

在多个app直接，有可能产生同名的url，这时候为了避免反转url的时候产生混淆，可以使用应用命名空间来做区分，定义应用命名空间只要在`app`的`urls.py`中定义一个叫做`app_name`的变量，来指定这个应用的命名空间即可，示例代码如下：

```python
app_name = 'front'

urlpatterns = [
    path('', views.index, name='index'),
    path('login/', views.login, name='login'),
]
```

以后再做反转的时候就可以使用`应用命名空间：url名称`的方式进行反正，示例代码如下：

```python
login_url = reverse('front:login')
```

#### 应用（app）命名空间和实例命名空间

一个app可以创建多个实例，可以使用多个url映射一个app，所以就会产生一个问题，以后在做反转的时候，如果使用应用命名空间，那么将会发生混淆，为了避免这个问题，可以使用实例命名空间，只要在`include`函数中传递一个`namespace`变量即可，示例代码如下：

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('cms1/', include('cms.urls', namespace='cms1')),
    path('cms2/', include('cms.urls', namespace='cms2')),
]
```

以后再做反转的时候，就可以根据实例命名空间来指定具体的url，示例代码如下：

```python
def index(request):
    username = request.GET.get('username')
    if username:
        return HttpResponse("CMS首页")
    else:
        # 获取当前的命名空间
        current_spacename = request.resolver_match.namespace
        return redirect('%s:login'%current_spacename)
```

### include函数的用法

1. `include(module, namespace=None)`:

   * module：子url的模块字符串
   * namespace：实例命名空间。这个地方需要注意一点，如果指定实例命名空间，那么前提必须是要先指定应用命名空间，也就是在子`urls.py`中添加`app_name`变量。

2. `include((pattern_list, app_namespace), namespace=None)`:

   `include`函数的第一个参数既可以为一个字符串，也可以是一个元组，如果是元组，那么元组的第一个参数是子`urls.py`模块的字符串，元组的第二个参数是应用命名空间，也就是说，应用命名空间既可以在子`urls.py`中通过`app_name`指定，也可以在`include`函数中指定。

3. `include(pattern_list)`:

   `pattern_list`是一个列表，这个列表中装的是`path`或者`re_path`函数，示例代码如下：

   ```python
       path('movie/', include([
           path('', views.movie),
           path('list/', views.movie_list),
       ]))
   ```

### re_path函数

1. re_path和path的作用是一样的，只不过`re_path`是在写url的时候可以用正则表达式，功能更强大。

2. 写正则表达式都推荐使用原生字符串，也就是以`r`开头的字符串

3. 在正则表达式中定义变量，需要使用圆括号括起来，这个参数是有名字的，那么需要使用`?P<参数名字>`，然后在后面添加正则表达式的规则，示例代码如下：

   ```python
   from django.urls import re_path
   from . import views
   
   urlpatterns = [
       # r''：代表的是原生字符串（raw）
       re_path(r'^$', views.article),
       # /article/list/<year>/
       re_path(r'^list/(?P<year>\d{4})/$', views.article_list),
       re_path(r'^list/(?P<month>\d{2})/$', views.article_list_month),
   ]
   ```

4. 如果不是特别要求，直接使用`path`就够了，避免将代码弄得很复杂。除非是url中确实是需要使用正则表达式来解决才使用`re_path`

### reverse函数

1. 如果在反转url的时候，需要添加参数，那么可以传递`kwargs`参数到`reverse`函数中，示例代码如下：

   ```python
   detail_url = reverse('detail', kwargs={"article_id":1, "page":2})
   ```

2. 如果想要添加查询字符串的参数，则必须手动进行拼接，示例代码如下：

   ```python
   login_url = reverse('login' ) + "?next=/"
   ```

### 自定义URL（PATH）转换器

#### 需求

实现一个获取文章列表的demo，用户可以根据`/articles/文章分类/`的方式来获取文章，其中文章分类采用的是`分类1+分类2+分类3...`的方式拼接的，并且如果只有一个分类，就不需要加号，示例如下：

```
# 1. 第一种：获取python分类下的文章
/articles/python/
# 2. 第二种：获取python和django分类下的文章
/articles/python+django/
# 3. 第三种：获取python和django和flask分类下的文章
/articles/python+django+flask/
以此类推...
```

在“文章分类”参数传到视图函数之前，要把这些分类分开来存储到列表中，比如参数是`python+django`，那么传到视图函数的时候就要变成`['python', 'django']`。

以后再使用`reverse`反转的时候，限制传递“文章分类”的参数应该是一个列表，并且将这个列表变成`python+django`的形式。

