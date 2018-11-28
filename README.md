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

![image-20181128220701815](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181128220701815.png)

### 启动内置服务器

``` python
python manage.py runserver
```

![image-20181128220805744](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181128220805744.png)

![image-20181128220844901](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181128220844901.png)

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

![image-20181128222731616](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181128222731616.png)

![image-20181128222745813](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181128222745813.png)

创建完了 app 以后我们还需要告诉Django 需要使用它.我们在 settings 中添加它

![image-20181128222912397](/Users/yaakovazat/Library/Application Support/typora-user-images/image-20181128222912397.png)



