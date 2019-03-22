# django框架初探

## 1.web框架介绍

### 本质是socket服务端.

​	我们在玩网络游戏时, 多个人同时在同一地图中做的操作能在各自的电脑上响应, 是因为游戏公司提供了一个服务端, 我们本地的电脑和服务端进行多次数据交互.

​	网络上信息传播99%都是基于TCP/IP协议, 它比较底层, 我们很多开发都不会接触到它. 所以计算机科学家对它进行了封装, 使其暴露出一个接口. 这个接口就是socket.

​	socket可以提供一台电脑到另一台电脑中的交互.

​	提供服务的叫socket服务, 和服务端进行交互的叫客户端.

​	做个比喻, 我们可以把服务端比喻成发电厂, 客户端比喻成电器, socket就是那些插头和插座, 电器只需要把插头插在插孔上, 就可以正常工作, 互联网中的数据流就可以比作电流.

### socket服务

### 真实的web程序来说会分为两个部分

-    #### 服务器程序


   		服务端, 负责对socket进行封装, 接受HTTP请求, 解析HTTP请求, 发送HTTP响应. 

   		通常这部分不会我们自己去写, 而是运用一些r软件, 如tomcat.

- ####    应用程序

  ##### 	wsgi网关接口

  ​		只要求提供一个函数

​	web框架就是将web应用开发中通用的部分抽象出来, 像做房子一样, 形成一个框架, 再去实现特定的功能.

​	广义来说, 就是一系列的库和一个主要的处理器.

##### 	常用的框架有

- django  全能型 (每年的web70%都是django框架)

- tornado 优秀的异步框架

- web.py 小巧的web框架

- flask 优秀的轻量级的web框架

  ##### 设计模式: 

  ##### mtv	

  m models模型  主要是负责数据对象与数据库对象

  t template模板  负责如何把数据展示给用户

  v view视图  主要负责业务逻辑, 在适当的时候调用另外两者

## 2.django框架的介绍

​	环境搭建, django安装

​	准备环境: 

 - ubuntu

 - python 3.5 +

 - pycharm 2017.1.5 + 专业版

 - MySQL

   每创建一个新的django项目, 都要新建一个新的python隔离环境

### 隔离环境

 - 查看 `workon`
 - 创建 `mkvirtualenv -p /usr/bin/python3.6 envname`
 - 进入`workon envname`
 - 退出 `deactivate`
 - 删除虚拟环境 `rmvirtualenv envname`

创建好了会自定切换进虚拟环境

​	安装一个`django`	`pip install django`

### 创建一个项目

 - 创建项目  `django-admin startproject <projectname>`

   - 首先选择一个存放项目的目录

   - 然后cd进去, 执行创建命令

   - tree查看树状图

     - crm目录, 项目的文件包
       - __init__.py 管理所有导入的库
       - settings.py django的配置页面
       - urls.py 整个项目url的跟配置
       - wsgi.py wsgi的接口

     - manage.py  管理页面, 管理整个django项目

- pycharm创建项目进行远程关联

  - new一个新的项目
  - 不要急着create
  - 配置远程解释器
  - 创建的隔离环境全部存放在用户+目录下的.virtualenvs目录下
  - 然后配置远程项目路径
  - 修改RemoteHost视图路径
  - 最后下载服务器的文件到本地

## 3.django项目简单操作

- 启动服务

  - 命令行: `python manage.py runserver` `ip:port ` (项目根目录下)

    ip 0.0.0.0/0`

  - Tools - Start SSH

    选择当前项目连接, 就可以连接到服务器了

    可能会乱码, 在SSH Terminal 中选择utr-8重新连接即可

- 初次运行可能会报错`DisallowedHost at /`

  - 在`settings.py`中的`ALLOWED_HOSTS`添加`'*'`即可

## 4.第一个试图

 - 项目

   有一些设置的django, 如crm

 - 应用

   包含了模型, 视图, 模板和url的组合

   - 创建一个应用: `python manage.py startapp _appname_`

     如果错误可以尝试python3

- 一个项目下可以拥有多个应用, 一个应用对应一个功能

- 创建一个简单的视图

  - 在`teacher - views.py`中定义一个`index`函数

    可以视为wsgi函数

  - `teacher`新建一个`urls.py`页面, 在其中定义`urlpatterns`变量

    变量名不可更改

    变量中输入 `path('index/', views.index)`

    `'index/'`代表路径`url`, `views.index`代表映射视图

  - 由于这是个子`url`配置, 在整个项目的根`url`也需要进行配置