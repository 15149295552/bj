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
