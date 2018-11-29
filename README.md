## Django Girls

### 虚拟环境

安装虚拟环境

``` python
python3.7 -m venv venv
```

激活虚拟环境

``` python
source venv/bin/activate
```

### Django

``` python
pip install django
```

![image-20181128215414691](https://ws4.sinaimg.cn/large/006tNbRwgy1fxo7s72gzbj315205qmyc.jpg)

### 第一个 Django 项目

```python
django-admin startproject demo .
```

![image-20181128215904111](https://ws1.sinaimg.cn/large/006tNbRwgy1fxo7x7u34bj30qo0cwq3v.jpg)

Django-admin.py 是一个脚本,将自动给我们创建目录和文件. 这里是我的文件目录情况.

### 更改设置

1. 更改时区

从 [wikipedia timezones list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) 找到自己对应地区的时区 (TZ). 并填写到 settings.py

2. 添加静态文件路径

``` python
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```

### 设置数据库

我们这里默认使用的是 sqlite3这个数据库,一般应用的话其实这个数据库就已经足够了.

若要为我们的博客创建一个数据库我们需要运行`migrate` 代码,如下:

```python
python manage.py migrate
```

![image-20181128220701815](/Users/yaakovazat/Library/Application%20Support/typora-user-images/image-20181128220701815.png)

### 启动内置服务器

``` python
python manage.py runserver
```

![image-20181128220805744](/Users/yaakovazat/Library/Application%20Support/typora-user-images/image-20181128220805744.png)

![image-20181128220844901](https://ws4.sinaimg.cn/large/006tNbRwgy1fxor44zf85j31200k842r.jpg)

### Django 模型:对象

面向对象编程:为事物建立模型,然后定义他们是怎样相互交互的.

对象: 就是属性和操作的集合.

我们需要回答一个问题,什么是一片博文?他应该包含哪些属性呢?

我们的文章需要一些文本,包括内容和标题,需要知道谁写的,也就是需要知道作者是谁,最后我们需要知道这个文章是什么时候需要发表的.

```
Post
-------------
title
text
author
created_date
published_date
```

一篇文章应该可以干什么?应该有一些正确的方法来 发布文章,因此我们需要一个 `publish` 的方法.

### Django 模型

现在我们可以为我们的博客创建一个 Django 模型

Django 里的 模型是一种特殊的对象,它保存在数据库当中.

### 创建应用程序

为了让一切保持整洁,我们将我们的项目内部创建单独的应用程序,.

``` python
python manage.py startapp blog
```

![image-20181128222731616](https://ws1.sinaimg.cn/large/006tNbRwgy1fxor479wllj30s600saa8.jpg)

![image-20181128222745813](https://ws3.sinaimg.cn/large/006tNbRwgy1fxor47wtbdj315b0u00xw.jpg)

创建完了 app 以后我们还需要告诉Django 需要使用它.我们在 settings 中添加它

![image-20181128222912397](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181128222912397.png)

### 创建一个博客文章模型

我们在 blog/models.py 中定义所有的 models 对象.我们打开 models.py 删除原来的内容并且填写如下信息:

``` python
from django.db import models
from django.utils import timezone
# Create your models here.

class Post(models.Model):
    author = models.ForeignKey('auth.User', on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateField(
        default=timezone.now
    )
    published_date =models.DateField(
        blank=True, null=True
    )


    def publish(self):
        self.published_date = timezone.now()
        self.save()

    def __str__(self):
        return self.title
```

所有 以 `from` 或者`import` 开始的地方,都是从其他文件中添加一些内容.所以跟复制粘贴就是一样的.

class Post(models.Model): 这一行是用来定义我们的一个模型(这是一个`对象`)

* class 是一个特殊的关键字,表明我们在定义一个对象
* Post 是我们的模型的一个名字,我们可以给他去任何一个我们想要的名字,但是比我们必须避免使用特殊字符或者空格.总是以首字母大学来作为类的名字.
* models.Model 表明 post 是一个 Django 模型. 所以 Django 知道它应该保存在数据库中,

现在我么定义了我们曾经提到的那些属性. `title` ,`text` , `created_date`, `published_date` ,和'author'. 为了做到那样我们需要为我们的每一个字段定义一个类型,告诉电脑, 他是文本么? 是数字吗? 是日期? 到另一个对象的关联,比如用户吗?

* models.Charfield 这是你如何用位数邮箱的字符来定义个文本
* models.TextField 这是没有长度限制的文本. 这听起来用在博客文章的内容是挺适合的.
* models.DateTimeField 这是日期和时间
* models.ForeignKey 这是指向另一个模型的链接.

def publish(self) :又怎样呢,这正是我们之前提到的 publish 的方法. def 表明这是一个函数或者方法, publish 是这个方法的名字,命名的规则是小写字母加下划线,而且一般都是以小写字母开始.