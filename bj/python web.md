# web概述

web就是互联网上的一种应用程序 - 网页

## 典型的程序：
​	1.C/S
​		C:Client(客户端)
​		S:Server(服务端)
​	2.B/S
​		B:Brower(浏览器)
​		S:Server(服务端)

## web组成 & 运行流程

由服务器，浏览器和通信协议组成
服务器：处理用户的请求和响应
浏览器：代替用户向服务器发送请求(USER Agent)
通信协议：规范了数据是如何打包和传递的
	http:Hyper Text Transfer Protocal
		 超级   文本   传输	 协议

前端：HTML + CSS + JS
后端：Python + Django + MySQL

# HTML

## 概念

Hyper Text Markup Language
 超级  文本  标记    语言

超文本：具备特殊功能的文本
	普通文本a：普通字符a
	超文本a：表示超链接的功能
	普通文本b：普通字符b
	超文本b：表示文字加粗的功能

标记：超文本的组成形式
	普通文本：a
	超文本：<a></a>
	超文本：<b></b>

## HTML在计算机在的表项

所有网页(HTML)文件在计算机都是以.html或者.htm作为结尾的文件

## 语法

### 标记语法

标记：在网页中，用于表示功能的符号称为"标记/标签/元素"

语法：所有的标记在使用时，必须用<>括起来

分为单标记和双标记

  双标记：显示的开始和显示的结束

  <标记>内容</标记>
  ```html
  <a> . . .</a>
  ```


  注意：双标记，有开始，必须有结束，否则会报错

  单标记：只有一个标记，技能表示开始，也能表示结束
  <标记>或者<标记/>

```html
<br> 或者 <br/> ：换行
<hr> 或者 <hr/> : 水平线
<img> 或者 <img/>: 一幅图像
```

嵌套:在一对标记中，再嵌套其他的标记，相当于是功能的嵌套
加粗的超链接

```html
<a><b>百度</b></a>
<b><a>百度</a></b>
```

练习：
```html
<!--文档类型声明 -->
<!DOCTYPE html>
<!--网页根标记-->
<html lang="en">
    <!--网页头部-->
    <head>
        <!--网页编码-->
    	<meta charset="UTF-8">
    	<!--网页标题-->
        <title>bf</title>
    </head>
    <!--网页主体-->
    <body>
        bf
    </body>
</html>
```

```html
<html>--父元素/父标记
	<head></head>--子元素/子标记
	<body></body>--子元素/子标记
</html>
```

起始格式
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>bf</title>
    </head>
    <body>
        
    </body>
</html>
```



属性和值：在标记中，用来修饰标记显示效果的内容

语法：
	1、属性必须声明在开始标记中
		<标记属性的声明位置处></标记>
	2、属性和标记名称之间要用空格隔开
		k标记属性名称></标记>
	3、属性和值之间是用那个=连接，属性值要用“”或‘’引起来
		亚标记属性名称='值'>
	4、一个元素允许有多个属性，并且排名不分先后，多属性之间使用空格隔开即可
		<标记 属性1='值1'属性2='值2'>

练习：

```html
<!DOCTYPE html>
<html lang="en">
    <head>
    	<meta charset="UTF-8">
        <title>bf</title>
    </head>
    <body>
        <p align="center" id="p1">
            this is p
        </p>
    </body>
</html>
```

HTML中的注释
<!-- -->
注意：
注释不能出现在<>中
~~<p<!---->></p>~~
注释不能嵌套

### 文档结构

文档声明

出现在网页的最顶端的第一个标记
作用：告诉浏览器使用HTML的版本

```html
<!DOCTYPE html>或者<!doctype html> - 使用HTML5版本
```

HTML页面
在文档类型声明之下，使用一对html根标记组成
<html></html>
在html中包含两对子元素

```html
<head></head> - 表示网页的头部
<body></body> - 表示网页的主题
```

练习：
01_text.html

```html
<!doctype html>
<html>
    <head>
        <title></title>
        <meta charset="utf-8">
    </head>
    <body>
        <p>&nbsp;
            这是一段文本
        </p>
    </body>
</html>
```

标记
特殊字符

```html
&nbsp;  表示一个空格
&lt;	表示 <
&gt		表示 >
&copy;  表示 ©
&yen;	表示 ￥
```

样式标记
作用：修改文本在网页中的表现形式

```html
<i></i> :斜体显示文本
<u></u> :下划线显示文本
<s></s> :删除线的方式显示文本
<b></b> :加粗显示文本
<sup></sup>:以上标的形式显示文本
<sub></sub>:以下标的形式显示文本
```

标题标记
作用：以不同的文章大小以及加粗的方式显示文本
语法：

```html
<h#></h#>
#:1-6
h1:一级标题
h2:二级标题
...
h6:六级标题
```

```html
<!doctype html>
<html>
    <head>
        <title></title>
        <meta charset="utf-8">
    </head>
    <body>
        <p>&nbsp;
            这是一段文本
        </p>
        <h1 align="left">
           静夜思
        </h1>
        <h3 align="center">
            李白
        </h3>
        <h2 align="right">
            床前明月光
        </h2>
        <h2>
            疑是地上霜
        </h2>
		<h2>
            举头望明月
        </h2>
		<h2>
            低头思故乡
        </h2>
    </body>
</html>
```

段落元素
作用：突显一段文本，每段文本独占一行/块，并且每个段落都会具备一小段的垂直空白距离
语法：

```html
<p></p>
属性：align
取值：left/center/right
```

练习：
```html
<p align="center">
    天长地久有时尽
	<br>此恨绵绵无绝期
</p>
```

换行元素
```html
<br>或</br>
```

分区元素
快分区

```html
<div>
    
</div>
```

特点：独占一行/块
作用：在网页中做布局（配合css)

行内分区元素

```html 
<span></span>
```

特点：允许在一行内显示多个span,并能够与其他的文本在一行内显示
作用：设置同一行文本的不同样式（配合css)

```html
<div>
    这是快分区元素
</div>
<span>这是行内分区元素</span>
```

行内元素与块级元素

块元素：只要能在网页中能独占一行的元素就都是块元素
div,p,h1…h6
所以元素都具备align属性，取值为left/center/right

行内元素：多个元素能够在一行内显示，就是行内元素
span,i,b,s,u,sup,sub

列表
	类型
	有序 - <ol></ol>
	无序 - <ul></ul>

列表项 - <li></li>
```html
<ol>
    <li>内容</li>
</ol>
<ul>
    <li>内容</li>
</ul>
```

练习：
```html
<!doctype html>
<html>
    <head>
        <title></title>
        <meta charset="utf-8">
    </head>
    <body>
        <ol>
            <li>西游记</li>
    		<l1>三国演义</Li>
			<1i>红楼梦</Li>
			<1i>水浒传</Li>
		</ol>
		<ul>
            <li>金毛狮王</li>
			<li>白眉鹰王</li>
   			<li>青翼蝠王</li>
			<li>紫衫龙王</li>
		</ul>
    </body>
</html>
```

列表属性

```html
<ol>
    
</ol>
```

属性：type
取值：
1、1:按数字方式排列，默认值
2、A:按大写英文字符方式排列
3、a:按小写英文字符方式排列
4、I:按大写罗马数字方式排列
5、1:按小写罗马数字方式排列

```html
<ul>
    
</ul>
```

属性：type
取值：
1、disc:实心圆点，默认值
2、circle:空心圆点
3、square:实心方块
4、none:不显示任何标识

列表的嵌套：在一个列表项中，又出现一个列表
```html
<ul>
    <li><ol>
        <li></li>
        </ol>
    </li>
</ul>
```

图像和超链接

URL
Uniform Resource Locator
  统一	资源	定位符
用于标识网络中资源的位置，俗称路径

URL分类
绝对路径：访问互联网上的资源时，使用绝对路径
相对路径：从当前文件所在的位置处去查找资源文件所经过的路径
	1.同目录下
	2.在子目录下
	3.在父目录刊
	./ 表示当前路径 ../ 表示上一级路径

注意：
UrL中不能出现中文
UrL是严格分区大小写

图像
标记：<img>
属性：
src：指定要显示的图片的URT
width：宽度，以px为单位的数值（允许省略px)
height：高度，以px为单位的数值（允许省略px)

```html
<img src="img/1.jpg"width="600",height="400">
```

练习：
```html
<!doctype html>
<html long="en">
    <head>
        <meta charset="utf-8">
        <title>Title</title>      
    </head>
    <body>
        <h1 align="center">HTML5 &lt;Day02&gt;</h1>
		<hr>
        <h2>
            1 HTML 文档片段
        </h2>
        <h3>
            1.1 问题
        </h3>
        <p>
            创建如图-1所示的html页面
        </p>
        <div>
            <img src="img/page,JPG">
        </div>
        <h4>
            图-1
        </h4>
		<h3>
            1.2方案
        </h3>
		<p>
            使用HTML完成效果
        </p>
        <div align="center">
            <a href="https://www.baidu.com/"target="_blank">
			<img src="img/page_struct.JPG">
			</a>
			<h4>
                图-2
            </h4>
		</div>
    </body>
</html>
```

### 表格

语法：
```html
<table>
    <tr>表行</tr>
    <td>单元格(列)</td>
</table>
```

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>bf</title>
    </head>
    <body>
        <table border="1" width="400" height="300" align="center">
            <tr align="center">
                <td>姓名</td>
                <td>语文</td>
                <td>数学</td>
                <td>英语</td>
            </tr>
            <tr align="center">
                <td>老王</td>
                <td>85</td>
                <td>72</td>
                <td>63</td>
            </tr>
            <tr align="center">
                <td>张三</td>
                <td>76</td>
                <td>78</td>
                <td>79</td>
            </tr>
            <tr align="center">
                <td>李四</td>
                <td>98</td>
                <td>45</td>
                <td>56</td>
            </tr>
        </table>
    </body>
</html>
```

属性
table属性
border：指定表格边框的宽度
width：指定表格的宽度
height：指定表格的高度
align：指定表格在其父元素中的水平对齐方式
	取值：left/center/right
cellpadding：单元格内边距，内容与单元格边框之间的距离
cellspacing：单元格外边距，单元格与单元格之间的距离

tr属性
align：控制当前行的内容的水平对齐方式
	取值：left/center/right
valign：控制当前行的内容垂直对齐方式
	取值：top/middle/bottom
bgcolor：指定当前行的背景颜色
	取值：颜色的英文单词
td属性：
width
height
align
valign
bgcolor
colspan:跨列/合并列
rowspan:跨行/合并行

行分组
表头行分组：<thread></thread>
表主题分组：<tbody></tbody>

### 表单

作用：用于接收用户的数据并提交给服务器

要素：
form元素 - 表单：收集用户的信息
表单控件：提供能够与用户进行数据交互的可是黄组件

form
语法：

```html
<form>
    
</form>
```

属性：
action：指定要提交给服务器程序的地址
method：提交方式
	get(默认方式)：表示向服务器要数据时使用
		特点：会将提交的数据显示在地址栏上；安全性较低
	post：表示要将数据提交给服务器进行处理时使用
		特点：隐式提交，看不到提交的数据；安全性较高

表单控件
文本框：<input type="text">
密码框：<input type="password">
属性：
name：定义控件的名称(提交给服务器使用，如果没有name的话则无法提交)
value:值
maxlength:限制输入的最大字符数
readonly:只读
placeholder:占位符，用户未输入任何数据时所显示的内容

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>bf</title>
    </head>
    <body>
        <form action="" method="get">
            <p>
                用户名称:<input type="text" name="uname" placeholder="请输入用户名">
            </p>
            <p>
                用户密码:<input type="password" name="upwd" placeholder="请输入密码">
            </p>
        </form>
    </body>
</html>
```

按钮
提交按钮：<input type="submit">
将表单的数据提交给服务器

重置按钮：<input type="reset">
将表单的内容恢复到初始化状态

普通按钮：<input type="button">
允许通过js自定义按钮
属性：
value:指定按钮上的文本

```html
<button>
    也可以定义为按钮
</button>
```

属性：type
	取值submit/reset/button

单选框和复选框
单选按钮：<input type="radio">
复选按钮：<input type="checkbox">
属性：
name：除了定义名称，还可以分组
		一组中的单选按钮或复选按钮,name属性必须一致

value：值，提前声明好

checked：设置预选中

文件选择框：上传文件时使用
语法：<input type="file">
属性：name,控件名称

多行文本域
标记：

```html
<textarea></textarea>
```

属性：
name：控件名称
cols：指定文本域默认显示的列数
rows：指定文本域默认显示的行数

下拉选择框
语法：

```html
<select>
    <option>显示</option>
    <option>1</option>
</select>
```

属性：
name
value

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>bf</title>
    </head>
    <body>
        <form action="" method="get">
            <p>
                用户名称:<input type="text" name="uname" placeholder="请输入用户名">
            </p>
            <p>
                用户密码:<input type="password" name="upwd" placeholder="请输入密码">
            </p>
            <p>
                <input type="checkbox" name="hobby" value="1">1
                <input type="checkbox" name="hobby" value="2">2
                <input type="checkbox" name="hobby" value="3">3
                <input type="checkbox" name="hobby" value="4">4
            </p>
            <p>
                上传头像：
                <input type="file" name="uimg">
            </p>
            <p>
                自我介绍：
                <textarea name="intro" id="" cols="30" rows="10"></textarea>
            </p>
            <p>
                <select name="city">
                    <option value="0">北京</option>
                    <option value="1">上海</option>
                </select>
            </p>
            <p>
                <input type="submit">
                <input type="button">
                <input type="reset">
            </p>
        </form>
    </body>
</html>
```

# CSS

CSS - 样式表
HTML：搭建网页结构
CSS：修饰和美化网页

内联方式
将CSS的内容定义在单独的HTML标签中
语法：

```html
<ANY style="样式声明"></ANY>
```

样式声明：由样式属性和样式值来组成
属性和值之间使用：连接
<ANY style="属性：值">
在style中允许有多个样式声明，多个样式声明之间使用;隔开
<ANY style="属性:值;属性:值">

文字大小：font-size
	取值：以px为单位的数字
	ex:设置某元素的文字大小为18px
	<ANY style="font-size:18px;">

文本颜色：color
	取值：颜色英语单词
	ex:设置某元素的文字大小为18px,文本颜色为红色
	<ANY style="font-size:18px;color:red;">

背景颜色：background-color
	取值：表示颜色的英文单词
	<ANY style="background-color:yeLlow;">

练习：
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>bf</title>
    </head>
    <body>
        <div style="font-size:24px;color:red;background-color:yellow">
            这是一个测试的div标记
        </div>
    </body>
</html>
```

内部样式表：让定义好的样式能够使用在当前页面中的多个元素上
语法：

```html
<head>
    <style>
        样式规则
        样式规则
        ...
    </style>
</head>
```

样式规则
语法：由选择器和样式声明组成
选择器：规范页面中哪些元素能够使用声明好的样式
选择器{
	属性1:值1
	属性2:值2
}

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>bf</title>
        <style>
            div{
                font-size:24px;
                color:red;
                background-color:yellow;
            }
        </style>
    </head>
    <body>
        <div>
            这是一个测试的div标记
        </div>
        <div>
            这是一个又测试的div标记
        </div>
    </body>
</html>
```

外部样式表：将声明好的样式应用在多个网页中
		   将样式规则声明在独立的css文件中(***.css)
			在使用的网页中对css文件进行引用

使用步骤

1. 创建css文件，并编写样式规则

2. 引出css文件
   ```html
   <head>
       <link rel="stylesheet" href="style.css">
   </head>
   ```

```css
p{
    font-size:18px;
    color:red;
    background-color:green;
}
div{
    ...
}
```

内联方式，最高；内部样式表和外部样式同样高(就近原则：后定义者优先)

css选择器：规范了页面中哪些元素能够使用声明好的的样式
			目的为了匹配页面的元素
选择器详解
元素选择器
特点：由标记名称作为选择器，主要匹配页面中指定标记所对应的所有元素
语法：
标记{
样式声明；
}

类选择器
特点：允许被任意一个元素所引用的选择器
语法：
.类名{
	…
}
类名：字母、数字、_ 、-组成；数组不能开头
引用：<ANY class="类名">

特殊用法
分类选择器的定义方式
允许将元素选择器和类选择器结合到一起使用，为了实现对某种元素不同样式的细分控制
语法：
元素选择器.类选择器{
…
}
div.font{
	匹配页面中所有class为font的div元素
}

多类选择器的引用方式
  允许让一个元素同时引用多个类选择器，多个类选择器之间使用空格隔开
  <ANY class="c1 c2 c3">

练习：
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>bf</title>
    </head>
    <body>
       <div>
           这是div中的内容
        </div>
        <h3>
            h3的内容
        </h3>
        <p>
            p的内容
        </p>
        <span>
        	span的内容
        </span>
    </body>
</html>
```

id选择器
id作用：在HTML中，每个元素都允许设置一个1d属性，主要用于表示该元素在网页中独一无二的标识<div id="main"></div>
语法：

```html
# id选择器值
#main{

}
```

群组选择器
作用：定义多个选择器们的共有的样式
	  定义方式是一个以，隔开的选择器列表
语法：
选择器1，选择器2，选择器3，…{

}

# Django框架

web与服务器

web：表示用户可以浏览的网页内容(HTML，CSS，JS)

服务器：能够给用户提供的机器
硬件范畴：一台机器
软件范畴：一个能够接收用户请求并给出相应的程序
作用：存储web所需要的信息(HTML，图片，音频)
	  能够处理用户的请求request，并给出响应response
	  执行服务器端的程序：查找数据库
Django框架：使用Python语音开发服务器端处理程序

框架：框架是一个为了解决开放性问题而存在的一种结构
	框架本身提供一些最基本的功能，我们只需要在基础功能上搭建属于自己的操作即可

Python中的框架
Django：重量级的web框架
Tornado：异步框架
Flask：轻量级框架

Django框架：是一个开源框架，采用Python语言开发
模式 - MTV
M:Models层
	模型层，负责数据库的建模以及CRUD的操作
T:Templatets层
	模板层，用于处理显示用户显示的内容，录：html
V:Views层
	视图层，处理与用户交互的部分内容，从模型中获取数据，再将数据发送给模板，显示给用户

使用
创建Django
django-admin startproject 项目名

启动服务 用于访问
在创建好的项目中，找到manage.py文件
通过manage.py启动项目(服务)
python3 manage.py runserver

启动服务之后，在浏览器中，通过网址访问
http://127.0.0.1:8000
http://localhost:8000

项目结构
manage.py
负责执行django中的各项操作的文件
如：
	启动服务
	创建应用
	数据库的同步

2、主文件夹(名称与项目名称相同)
__ init __.py
项目初始化文件，每当服务器启动的时候，都会自动执行

urls.py
项目的基础url(路由)配置文件

wsgi.py
应用服务器配置文件，暂时不用

settings.py
项目的主设置文件:应用，模板，数据库，语言，时区，... ...
BASE_DIR : 获取当前项目的绝对路径
DEBUG : 调试模式
	开发过程：推荐使用 True
	上线运行：必须改为 False
ALLOWED_HOSTS
	设置允许访问本项目的地址列表。
	如果不设置的话，只有本机(localhost/127.0.0.1)能访问。
	推荐写 '*',任何表示该机器的地址都可以访问当前项目
INSTALLED_APPS
	指定已安装的应用，如果有自定义的应用的话，需要在此注册
MIDDLEWARE:注册中间件
ROOT_URLCONF:指定项目的基础路由配置文件
TEMPLATES:指定模板的信息
DATABASES:指定数据库的信息
LANGUAGE_CODE:指定语言，允许修改为zh-Hans
TIME_ZONE:指定时区，建议改为 Asia/Shanghai

URL的使用
urls.py
默认在主文件夹中，主路由位置文件，包含所有的地址映射
每一个请求到达之后，都会由urls.py中的urlpatterns列表中的url()进行匹配
url()函数匹配上之后，可能将请求转交给其他的Views(视图)或其他的urls.py去处理

python3 manage.py migrate

创建超级管理员
python3 manage.py createsuperuser
1.用户名
2.邮箱
3.密码
4.确认密码

url函数的语法
url(regex,views,kwargs=None,name=None)
1.regex
正则表达式模板，匹配请求的url
2.views
URL处理的视图函数
3.kwargs
字典，用来向views传参的，没有参数可以省略
4.name
字符串，给url()起别名，主要在模板中使用

Django应用
应用就是网站中的一个独立的模块程序
在Django中，主目录一般不处理用户的请求，主要做的是项目的初始
化以及请求的分发

创建应用
命令
python3 manage.py startapp 应用名称

在settings.py中进行注册
在INSTALLED_APPS中追加应用名称
INSTALLED_APPS =[
'django.contrib.admin',
'应用名称'
]

结构组成
migrations目录
存放数据库中间文件的目录（日志文件）

\__init__.py
应用的初始化文件

admin.py
应用的后台管理配置文件

apps.py
应用的属性配置文件，不需改动

modets.py
Models文件

tests.py
测试模块

views.py
定义视图的文件

Django模板(Template)
模板是要动态给用户呈现的网页内容
可以由Views(视图)呈现给用户
其实就是网页 - 前后端结合的一个网页

模板设置
在setting.py中TEMPLATES 变量
TEMPLATES = [
	{
		'BACKEND':'... ...',
		'DIRS':[... ..],
		... ..
	},
]

BACKEND:指定模板的搜索引擎，不用动
DIRS:指定模板所存放的目录们
DIRS ['index.temp','music.temp']

模板加载方式
使用render直接加载并返回模板
from django.shortcuts import render
def xxx_views(request):
return render(request,'模板名称',{})

