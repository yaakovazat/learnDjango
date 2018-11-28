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

从 [wikipedia timezones list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) 找到自己对应地区的时区 (TZ). 并填写到 settings.py

