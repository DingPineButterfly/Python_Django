# 路由分配及模板渲染

##### 测试项目: `crm`



## 1. 路由系统

​	用来分发请求

​	网络上用来区分电脑的是`ip`, 端口

### `url`全球统一资源定位符(网址)

`http://www.aspxfans.com:8080/news/index.asp?boardID=5&IDpage=1#name`

如上就是一个`url`, 所有的`url`都是由这几部分组成

- `http://`  协议	互联网传输协议 `http`默认`80`端口. `https`默认`443`端口
- `www.aspxfans.com:8080/` 域名(IP地址和端口)
- `news/index.asp` 路径	路由就是通过这个路径进行请求的分发
- `?`后面跟着的是参数, 没有`?`表示没有参数
- `#`代表锚点

`URLconf`模块`url.py`, 项目文件夹下的叫根配置文件

​	当有一个请求来时, `django`首先会到项目文件目录下`urls.,py`中去找`urlpatterns`定义路由规则, 前面有部分时路径. 如果路径对应, 则会调用后面的方法

### `path(route, view, kwargs=None, name=None)`

- `route`代表字符串 `url`规则
- `view` 视图, 是一个函数, 不是函数执行, 不能加括号
- `kwargs` 额外的参数, 是一个字典
- `name` `url`规则的名字

### 在url中捕获参数

```python
path('student_detail/<pk>/', views.student_detail_view)
```

`crm` 获取某个学生的详情

格式为<pk>

### 转换器

```python
path('student_detail/<int:pk>/', views.student_detail_view)
```

- `str` 匹配除了路径分隔符`'/'`之外的所有字符串, 如果不写转换器, 默认就是`str`
- `int` 匹配0或任何正整数
- `slug` 匹配任意的ASCII字符或数字组成的`slug`字符串, 连字符`'-'`和`'_'`
- `path` 匹配任何非空字符串, 包括路径分隔符`'/'`

除了匹配函数参数之外还会把参数转换成整数

### 使用正则表达式

#### `re_path(route, view. kwargs=None, name=None)`

​	和`path()`参数是一样的

​	在写新的路由后需要注释前面的路由, 因为路由秉正只要匹配到就返回的原则

​	注意: 正则表达式匹配的参数都会转换成字符串

​	如果正则没有错但是在规定范围内只匹配到了一位数, 加上`^`和`&`再次尝试

​	`path`只会匹配路径

### `URL`命名

#### 重定向

## 2. 模板系统

​	`django`	提供了一套模板渲染机制, 存放在特定的文件夹

​	在项目文件夹的`settings`中, TEMPLATES用来设置模板配置

​	模板通常放在项目根文件夹, 一般名为`templates`

​	配置完`settings`后需要到`templates`下创建一个和`app`文件夹同名的文件夹

​	`html`文件放在此处

