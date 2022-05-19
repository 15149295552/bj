# print()输出函数

```py
#输出数字
print(520)
print(98.5)
#输出字符串
print('hello world')
print("hello world")
#输出含有运算符的表达式
print(3+1)
#将数据输出到文件中，如果文件不存在就创建，存在就继续追加
fp=open('D/text.txt','a+')
print('hello world'.file=fp)
fp.close()
#不进行换行输出(输出内容在一行中)
print('hello','world','Python')
```
# 转义字符

```py
print('hello\nworld') #\n表示换行
print('hello\tworld') #\t制表符
print('helloooo\tworld')
print('hello\rworld')#\r表示world将hello覆盖
print('hello\bwordl')#\b表示退一个格，将o退没了
print('http:\\\\baidu.com')
print('老师说:\'大家好\'')
#原字符,不希望字符串中的转义字符起作用，就使用原字符，就是在字符串之前加上r/R
print(r'hello\nworld')
#注意事项：最后一个字符不能是反斜线
print(r'hello\nworld\')
```
# 字符编码
```py
print(chr(0b100111001011000))
print(ord('乘'))
```
# 标识符和保留字
```py
import keyword
print(keyword.kwlist)
```
# 变量
```py
name='玛丽亚'
print(name)
print('标识',id(name))
print('类型',type(name))
print('值',name)
```
```py
name='玛丽亚'
print(name)
name='楚溜冰'
print(name)
```
# 数据类型
## int：整数类型，表示正数，负数，0
```py
n1=90
n2=-2
n3=0
print(n1)
print(n2)
print(n3)
print('十进制',118)
print('二进制',0b01110110)
print('八进制',0o166)
print('十六进制',0x76)
```
## float：浮点类型
```py
a=3.13159
print(a,type(a))
n1=1.1
n2=2.2
n3=2.1
print(n1+n2)
print(n1+n3)
from decimal import Decimal
print(Decimal('1.1')+Decimal('2.2))
```
## bool布尔类型

```py
f1=Ture
f2=False
print(f1,type(f1))
print(f2,type(f2))
#布尔值可以转成整数计算
print(f1+1)#2	1+1的结果为2  True表示1
print(f2+1)#1	0+1的结果为2  False表示0
```

## 字符串类型

```py
str1='我用python'
str2="我用python"
str3="""我用
python"""
str4='''我用
python'''
print(str1,type(str1))
print(str2,type(str2))
print(str3,type(str3))
print(str4,type(str4))
```

# 数据类型转换

```py
name='张三'
age=20
print(type(name),type(age))
print('我叫'+name+'今年'+age+'岁')#当将str类型与int类型进行连接时，报错，解决方案，类型转换
print('我叫'+name+'今年'+str(age)+'岁')#将int类型通过str()函数转成了str类型
#str()将其它类型转成str类型
a=10
b=198.8
c=False
print(type(a),type(b),type(c))
print(str(a),str(b),str(c),type(str(a)),type(str(b)),type(str(c)))
#int()将其他类型转成int类型
s1='126'
f1=98.6
s2='67.44'
ff=Ture
s3='hello'
print(type(s1),type(f1),type(s2),type(ff),type(s2))
print(int(s1),type(int(s1)))#将str转成int，字符串为数字串
print(int(f1),type(int(f1)))#将float转成int，截取整数部分，舍掉小鼠
print(int(s2),type(int(s2)))#将str转成int类型，报错，因为字符串为小数串
print(int(ff),type(int(ff)))
print(int(s3),type(int(s3)))#将str转成int类型时，字符串必须为数字串(整数)，非数字串是不允许转换
#float()将其它数据类型转成float类型
s1='126.25'
s2='67.'
ff=Ture
s3='hello'
i=98
print(type(s1),type(s2),type(ff),type(s3),type)
print(float(s1),type(float(s1)))
print(float(s2),type(float(s2)))
print(float(ff),type(float(ff)))
print(float(s3),type(float(s3)))#字符串中的数据如果是非数字串，则不允许转换
print(float(i),type(float(i)))
```

# 函数

## input()函数

```py
present=input('想要什么礼物呢')
print(present,type(present))
a=int(input('请输入一个加数'))
#a=int(a)#将转换之后的结果储存a中
b=int(input('请输入另一个加数'))
#b=int(b)
print(type(a),type(b))
print(a+b)
```

## 运算符

### 算数运算符

```py
print(1+1)#加法运算
print(1-1)#减法运算
print(2*3)#乘法运算
print(1/2)#除法运算
print(11//2)# =5 整除运算
print(11%2)# =1 取余运算
print(2**3)# =8 表示2的3次方
print(9//4)# =2
print(-9//-4)# =2
print(9//-4)# =-3
print(-9//4)# =-3 一正一负的整数公式，向下取整
print(9%-4)# =-3 余数=被除数-除数*商  9-(-4)*(-3)
print(-9%4)# =3	-9-(4)*(-3) 商为10行，11行的//
```

### 赋值运算符

```py
#顺序从右到左
i=3+4
print(i)
a=b=c=20#链式赋值
print(a,id(a))
print(b,id(b))
print(c,id(c))
#参数赋值
a=20
a+=30#a=a+30
print(a)
a-=10#a=a-=10
print(a)
a*=2#a=a*2
print(a)
a/=3
print(a)
a//=2
print(a)
a%=3
print(a)
a,b,c=20,30,40
print(a,b,c)
#a,b=20,30,40  报错，因为左右变量的个数和值的个数不对应
#交换两个变量的值
a,b=10,20
print('交换之前：',a,b)
#交换
a,b=b,a
print('交换之后：',a,b)
```

### 比较运算符

```py
a,b=10,20
print('a>b?',a>b)#False
print('a<b?',a<b)#True
print('a<=b?',a<=b)#True
print('a>=b?',a>=b)#False
print('a==b?',a==b)#False
print('a!=b?',a!=b)#True
a=10
b=10
print(a==b)#True  说明a与b的value相等
print(a is b)#True  说明a与b的id相等
lst1=[11,22,33,44]
lst2=[11,22,33,44]
print(lst1==lst2)#value -> True
print(lst1 is lst2)#id -> False
print(a is not b)#False
print(lst1 is not lst2)#True
```

### 布尔运算符

```py
a,b=1,2
#and 并且
print(a==1 and b==2)#True
print(a==1 and b<2)#False
print(a!=1 and b==2)#False
print(a!=1 and b!=2)#False
#or或者
print(a==1 or b==2)#True
print(a==1 or b<2)#True
print(a!=1 or b==2)#True
print(a!=1 or b!=2)#False
#not  对bool类型的操作数取反
f=True
f2=False
print(not f)
print(not f2)
#in与not in
s='helloworld'
print('w' in s)
print('k' in s)
print('w' not in s)
print('k' not in s)
```

### 位运算符

```py
print(4&8)#按位&，同为1时，结果为1
print(4|8)#按位或，同为0时，结果为0
print(4<<1)#向左移动1位(移动一个位置)
print(4<<2)#向左移动2位
print(4>>1)#向右移动1位
print(4>>2)#向右移动2位
```

### 运算符优先级

先算术运算，然后位运算，最后比较运算

# 对象的布尔值

```py
print(bool(False))#False
print(bool(0))#False
print(bool(0.0))#False
print(bool(None))#False
print(bool(''))#False
print(bool(""))#False
print(bool([]))#空列表 - False
pinrt(bool(list()))#空列表 - False
print(bool(()))#空元组 - False
print(bool(tuple()))#空元组 - False
print(bool({}))#空字典 - False
print(bool(dict()))#空字典 - False
print(bool(set(g)))#空集合 - False
#除了上面的其他的都为True
print(bool(18))
print(bool(True))
print(bool('helleworld'))
```

# 结构

## 单分支结构

```py
money=1000
s=int(input('请输入取款金额'))
#判断余额是否充足
if money >= s:
    money-=s
    print('取款成功，余额为；',money)
```

## 双分支结构

```py
num=int(input('请输入一个整数'))
if num % 2 == 0:
    print(num,'是偶数')
else:
    print(num,'是奇数')
```

## 多分支结构

```py
score=input('请输入一个成绩：')
if score >= 90 and score <= 100:
    print('A')
elif score >= 80 and score <=89:
    print('B')
elif score >= 70 and score <=79:
    print('C')
elif score >= 60 and score <=69:
    print('D')
elif score >=0 and score <= 59:
    print('不及格')
else:
    print('成绩有误，请重新输入')
```

## 嵌套if

```py
answer=input('你是会员吗?y/n')
money=float(input('请输入购物金额'))
if answer=='y':
    if money>=200:
        print('打8折，付款金额为：',money*0.8)
    elif money>=100:
        print('打9折，付款金额为：',money*0.9)
    else:
        print('打9.5折，付款金额为：'，money*0.95)
else:
    if money>=150:
        print('打9.9折，付款金额为：',money*9.9)
    else:
        print('不打折，付款金额为：',money)
```

## 条件表达式

```py

```

# 类与对象

## 定义类
```py
class Student:#Student - 类名：由一个或多个单词组成，每个单词第一个字母大写
    pass
#一切皆对象
print (id(Student))#2926222013040
print(type(Student))#<class type'>
print (Student)#<class'_main_.Student'>
```
```py
class Student:
    native_pace='abc'#直接写在类里的变量，称为类属性
    def __init__(self,name,age):#初始化方法
        self.name=name#self.name - 实体属性，进行了一个赋值操作，将局部变量的name的值赋给实体属性
        self.age=age
    def eat(self):#实例方法
        print('在吃饭')
    @staticmethod
    def method():#静态方法
        print('我使用了static method进行修饰，所以我是静态方法')
    @classmethod
    def cm(cls):#类方法
        print('我是类方法，因为我使用了class method进行修饰')
#在类之内称为方法，类之外称为函数
def dreak:#函数
    print('水')
```
## 对象的创建
```py
class Student:
    native_pace='abc'#直接写在类里的变量，称为类属性
    def __init__(self,name,age):
        self.name=name#self.name - 实体属性，进行了一个赋值操作，将局部变量的name的值赋给实体属性
        self.age=age
    def eat(self):#实例方法
        print('在吃饭')
stu1=Student('zhangsan',20)#stu1 -> Student：根据类对象(Student)创建实例对象(stu1)
stu1.eat()#实例对象名.方法名()
print(stu1.name)
print(stu1.age)
Student.eat(stu1)#类名.方法名(类的对象) -> 实际就是方法定义处的self
#Student.eat(stu1)与stu1.eat()代码功能相同，都是调用Student中的eat方法
```
## 类属性
```py
class Student:
    native_pace='abc'#直接写在类里的变量，称为类属性
    def __init__(self,name,age):
        self.name=name#self.name - 实体属性，进行了一个赋值操作，将局部变量的name的值赋给实体属性
        self.age=age
    def eat(self):#实例方法
        print('在吃饭')
print(Student.native_pace)
stu1=Student('zhangsan',20)
stu2=Student('lisi',30)
print(stu1.native_pace)
print(stu2.native_pace)
```
## 类方法
```py
Student.cm()
```



## 静态方法

```py
Student.method
```



## 动态绑定属性和方法
```py
class Student:
    def __init__(self,name,age):
        self.name=name
        self.age=age
    def eat(self):
        print(self.name+'在吃饭')
stu1=Student('zhangsan',20)
stu2=Student('lisi',30)
print(id(stu1))
print(id(stu2))
#为stu1动态绑定属性
stu1.gender='nan'
print(stu1.name,stu1.age,stu1.gender)
print(stu2.name,stu2.age)#stu2未绑定
stu1.eat()
stu2.eat()
def show():
    print('定义在类之外的，成为函数')
#stu1绑定show方法
stu1.show=show
stu1.show()
```
# 面向对象
## 封装
```py
class Car:
    def __init__(self,brand):
        self.brand=brand
    def start(self):
        print('汽车启动了')
car=Car('x5')
car.start()
print(car.brand)
```
```py
class Student:
    def __init__(self,name,age):
        self.name=name
        self.__age=age#年龄不希望在类的外部别使用，所以加了两个__
    def show(self):
        print(self.name,self.__age)
stu=Student('zhangsan',20)
stu.show()
#在类的外部使用name与age
print(stu.name)
print(stu.__age)#error
print(dir(stu))
print(stu._Student__age)#在类之外通过 _Student__age 进行访问
```
## 继承
```py
class Person(object):#Person继承object类
    def __init__(self,name,age):
        self.name=name
        self.age=age
    def info(self):
        print(self.name,self.age)
class Student(Person):
    def __init__(self,name,age,sut_no):
        super().__init__(name,age)
        self.stu_no=stu_no
class Teacher(Person):
    def __init__(self,name,age,teachofyear):
        super().__init__(name,age)
        self.teachofyear=teachofyear
stu=Student('zhangsan',20,'1001')
teacher=Teacher('lisi',34,10)
stu.info()
teacher.info()
```
```py
class A(object):
    pass
class B(object):
    pass
class C(A,B):
    pass
```
### 方法重写
```py
class Person(object):#Person继承object类
    def __init__(self,name,age):
        self.name=name
        self.age=age
    def info(self):
        print(self.name,self.age)
class Student(Person):
    def __init__(self,name,age,sut_no):
        super().__init__(name,age)
        self.stu_no=stu_no
    def info(self):
        super().info()
        print(self.stu_no)
class Teacher(Person):
    def __init__(self,name,age,teachofyear):
        super().__init__(name,age)
    def info(self):
        super().info()
        print(self.teachofyear)
        self.teachofyear=teachofyear
stu=Student('zhangsan',20,'1001')
teacher=Teacher('lisi',34,10)
stu.info()
teacher.info()
```
```py
class Student:
    def __init__(self,name,age):
        self.name=name
        self.age=age
    def __str__(self):
        return'mz{0},jn{1}'.format(self.name,self.age)
stu=Student('zhangsan',20)
print(dif(stu))
print(stu)
```
## 多态
```py
class Animal(object):
    def eat(self):
        print('dwhc')
class Dog(Animal):
    def eat(self):
        print('gcgt')
class Cat(Animal):
    def eat(self):
        print('mcy')
class Person:
    def eat(self):
        print('rcwgzl')
#定义一个函数
def fun(obj):
    obj.eat()
#开始调用函数
fun(Cat())
fun(Dog())
fun(Animal())
fun(Person())
```
```py
class A:
    pass
class C:
    pass
class C(A,B):
    def __init__(self,name,age):
        self.name=name
        self.age=age
class D(A):
    pass
x=C('jack',20)#x是C类型的一个实例对象
print(x.__dict__)#实例对象的属性字典
print(C.__dict__)
print(x.__class__)#输出对象所属的类
print(C.__bases__)#C类的父类类型的元素
print(C.__base__)#类的基类：谁在前输出谁
print(C.__mro__)#类的层次结构
print(A.__subclasses__())#子类列表
```
```py
a=20
b=100
c=a+b#两个整数类型的对象的相加操作
d=a.__add__(b)
print(c)
print(d)
class Student:
    def __init(self,name):
        self.name=name
    def __add__(self,other):
        return self.name+other.name
    def __len__(self,name):
        return len(self.name)
stu1=Student('zhangsan')
stu2=Student('lisi')
s=stu1+stu2#实现两个对象的加法运算(因为在Student类中，编写 __add__() 特殊方法)
print(s)
s=stu1.__add__(stu2)
print(s)
lst=[11,22,33,44]
print(len(lst))#len是内容函数
print(lst.__len__())
print(len(stu1))
```
```py
class Person(object):
    def __init__(self,name,age):
        self.name=name
        self.age=age
    def __new__(cls,*args,**kwargs):
        print('__new__被调用执行了，cls的id值为{0}'.format(id(cls)))
        obj=super().__new__(cls)
        print('创建的对象的id为：{0}'.format(id(obj)))
        return obj
    def __init__(self,name,age):
        print('__init__被调用了，self的id为：{0}'.formage(id(self)))
        self.name=name
        self.age=age
print('object这个类对象的id为：{0}'.format(id(object)))
print('Person这个对象的id为：{0}'.format(id(Person)))
p1=Person('zhangsan',20)
print('p1这个Person类的实例对象的id：{0}'.format(id(p1)))
```
```py
class CPU:
    pass
class Disk:
    pass
class Computer:
    def __init__(self,cpu,disk):
        self.cpu=cpu
        self.disk=disk
cpu1=CPU()
cpu2=cpu1
print(cpu1)
print(cpu2)
#类的浅拷贝
disk=Disk()
computer=Computer(cpu1,disk)
#浅拷贝：源对象和拷贝对象引用同一个子对象
import copy
computer2=copy.copy(computer)
print(computer,computer.cpu,computer.disk)
print(computer2.computer2.cpu,computer2.disk)
#深拷贝：同时拷贝源对象的子对象
computer3=copy.deepcopy(computer)
print(computer,computer.cpu,computer.disk)
print(computer3.computer3.cpu,computer3.disk)
```
## 模块

```py
def fun():
    pass
def fun2():
    pass
class Student:
    native_place='abf'#类属性
    def eat(self,name,age):
        self.name=name
        self.age=age
    @classmethod
    def cm(cls):
        pass
    @staticmethod
    def sm():
        pass
a=10
b=20
print(a+b)
#导入模块
import math
print(math.pi)
print(dir(math))
from math import  pi
print(pi)
```
```py
#新建模块：可以是创建一个.py的文件
#新建模块：calc.py
def add(a,b):
    return a+b
def div(a,b):
    return a/b
#导入自定义模块,在另一个.py文件打开
from calc import add
print(add(10,20))
```
## 以主程序运行

```py
#新建模块：calc2.py
def add(a,b):
    return a+b
if __name__=='__main__':#只有点击运行calc2时，才会运行
    print(add(10,20))
#导入模块
import calc2
print(calc2.add(100,200))
```
## 包
```py
#包包含模块
#directory：目录
#创建包 - package：包
#directory和package区别：package有__init__.py的文件，而directory没有
#创建模块
#module_A.py
a=10
#module_B.py
b=100
#导入pageage包
import pageage.module_A as ma#ma是pageage.module_A的别名
print(ma.a)
#使用import方式导入时，只能跟包名或模块名,使用from...import导入包，模块，函数，变量
```
## 常用模块
```py
import sys
import time
import urllib.request
print(sys.getsizeof(24))
print(sys.getsizeof(True))
print(sys.getsizeof(False))
print(time.time())
print(time.localtime(time.time()))
print(urllib.request.urlopen('http://www.baidu.com').read)
```
