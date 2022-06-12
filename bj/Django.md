#项目结构

##创建项目

django-admin startproject mysite1

##运行项目

python3 manage.py runserver
python3 manage.py runserver 端口号

##关闭服务

1. Ctrl + c
2. sudo lsof -i:端口号 - 查看PID
   sudo kill -9 PID

## manage

python3 manage.py - 查看所有子命令

##URL

###构成

protocol(协议)

1. http://
2. https://
3. file:/// - 本地文件

hostname(主机名)

port(端口)
:80 - 默认端口

path(路由地址)
由零个或多个"/"隔开的字符串

query(查询字符串)
"?"开头后面的都是用于给动态网页传递参数，可有多个参数，用“&”符号隔开，每个参数的名和值用“=”符号隔开。

fragment(信息断片)
"#"开始

###URL请求处理

主路由 - urls.py
找urlpatterns变量(包含许多路由的数组)：从上到下逐一匹配，找到直接截止

### 视图函数

用于接收一个浏览器请求(HttpRequest对象)并通过HttpResponse对象返回响应的函数
语法
def xxx_view(request[,其他参数.\.\.]):
	return HttpResponse(对象)

#模板层

##模板的变量

1. {{变量名}}
2. {{变量名.index}}
3. {{变量名.key}}
4. {{变量.方发}}
5. {{函数名}}

## 标签

{% 便签 %}
{% 结束标签 %}

### if标签

语法：
{% if 条件表达式1 %}
{% elif 条件表达式2 %}
{% else %}
{% endif %}

### for标签

语法：
{% for 变量 in 可迭代对象%}
{% empty %}
{% endfor %}
