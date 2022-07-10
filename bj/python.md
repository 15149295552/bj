# print()输出函数

```python
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

```python
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

```python
name='玛丽亚'
print(name)
print('标识',id(name))
print('类型',type(name))
print('值',name)
```

```python
name='玛丽亚'
print(name)
name='楚溜冰'
print(name)
```

# 数据类型

## int：整数类型，表示正数，负数，0

```python
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

```python
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

```python
f1=Ture
f2=False
print(f1,type(f1))
print(f2,type(f2))
#布尔值可以转成整数计算
print(f1+1)#2	1+1的结果为2  True表示1
print(f2+1)#1	0+1的结果为2  False表示0
```

## 字符串类型

```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

```python
print(4&8)#按位&，同为1时，结果为1
print(4|8)#按位或，同为0时，结果为0
print(4<<1)#向左移动1位(移动一个位置)
print(4<<2)#向左移动2位
print(4>>1)#向右移动1位
print(4>>2)#向右移动2位
```

### 运算符优先级

先算术运算，然后位运算，最后比较运算

# 对象的布尔值d

```python
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

```python
money=1000
s=int(input('请输入取款金额'))
#判断余额是否充足
if money >= s:
    money-=s
    print('取款成功，余额为；',money)
```

## 双分支结构

```python
num=int(input('请输入一个整数'))
if num % 2 == 0:
    print(num,'是偶数')
else:
    print(num,'是奇数')
```

## 多分支结构

```python
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

```python
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

```python
num_a=int(input('请输入第一个整数'))
num_b=int(input('请输入第二个整数'))
if num_a>num_b:
    print(num_a,'大于等于',num_b)
else:
    print(num_a,'小于'，num_b)
print(str(num_a+'大于等于'+num_b) if num_a>=num_b else str(num_a+'小于'+num_b))
```

## pass语句

```python
answer=input('你是会员吗？y/n')
if answer=='y':
    pass
else:
    pass
```

```python
age=int(input('请输入年龄：'))
if age:
    print(age)
else:
    print('年龄为：',age)
```

## 内置函数

range()

```python
r=range(10)#从0开始，一直到10(不包括10)，步长默认1
print(r)
print(list(r))
r=range(1,10)#从1开始
print(list(r))
r=range(1,10,2)#步长为2
print(list(r))
print(10 in r)#False，10不在r整数列中
print(9 in r)#True，9在r整数列中
print(9 not in r)#False
print(range(1,20,1))
```

## 循环结构

```python
sum=0
a=0
while a<5:
    sum+=a
    a+=1
print(sum)
```

```python
sum=0
a=1
while a<=100:
    if not bool a%2:
        sum+=a
     a+=1
print(sum)
```

```python
for item in 'python':
    print(item)
for i in range(10):
    print(i)
for _ in range(5):
    print()
for item in range(1,10):
    if item %2==0:
        sum+=item
print(sum)
```

```python
for item in range(100,1000):
    fe=item%10
    shi=item
    bai=item
    print(bai,shi,ge)
    if ge**3+shi**3+bai**3==item:
        print(item)
```

## 流程控制语句

```python
for item in range(3):
    pwd=input('请输入密码')
    if pwd == '8888':
        print('密码正确')
        break
    else:
        print('密码不正确')
```

```python
a=0
while a<3:
     pwd=input('请输入密码')
    if pwd == '8888':
        print('密码正确')
        break
    else:
        print('密码不正确')
```

```python
for item in range(1,51):
    if item%5 == 0:
        print(item)
for item in range(1,51):
    if item%5 != 0:
        continue
    print(item)
```

```python
for item in range(3):
    pwd=input('请输入密码')
    if pwd=='8888':
        print('密码正确')
        break
    else:
        print('密码不正确')
else:
    print('三次密码均错误')
```

```python
a=0
while a<3:
    pwd=input('请输入密码')
    if pwd=='8888':
        print('密码正确')
        break
    else:
        print('密码不正确')
    a+=1
else:
    print('三次密码均错误')
```

```python
for i in range(1,4):
    for j in range(1,5):
        print('*',end='\t')
    print()
```

```python
for i in range(1,10):
    for j in range(1,i+1):
        print(i,'*',j,'=',i*j,end='\t')
	print()
```

```python
for i in range(5):
    for j in range(1,11):
        if j%2 == 0:
            continue
		print(j,end='\t')
	print()
```

# 列表

```python
a=10
lst=['hello','world',98]
print(id(lst))
print(type(lst))
print(lst)
```

## 列表创建

```python
lst=['hello','world',98]
lst2=list(['hello','world',98])
```

# 类与对象

## 定义类

```python
class Student:#Student - 类名：由一个或多个单词组成，每个单词第一个字母大写
    pass
#一切皆对象
print (id(Student))#2926222013040
print(type(Student))#<class type'>
print (Student)#<class'_main_.Student'>
```

```python
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

```python
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

```python
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

```python
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

```python
class Car:
    def __init__(self,brand):
        self.brand=brand
    def start(self):
        print('汽车启动了')
car=Car('x5')
car.start()
print(car.brand)
```

```python
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

```python
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

```python
class A(object):
    pass
class B(object):
    pass
class C(A,B):
    pass
```

### 方法重写

```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

```python
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

# 1 变量

变量就是一个存储数据的时候当前数据所在的内存地址的名字

## 1.1 标识符

+ 由数字、字母、下划线组成
+ 不能数字开头
+ 不能使用内置关键字
+ 严格区分大小写

## 1.2 命名习惯

- 大驼峰：每个单词首字母都大写，例如：MyName
- 小驼峰：第二个(含)以后的单词首字母大写，例如：myName
- 下划线：例如：my_name

## 1.3 使用变量

语法：变量名 = 值

代码

~~~python
#定义变量：存储数据TOM
my_name = 'TOM'
print(my_name)
#定义变量：存储数据 程序员
schoolName = '程序员'
print(schoolName)
~~~

## 1.4 认识bug

所谓bug，就是程序中的错误

代码

~~~python
#定义变量：存储数据TOM
my_name = 'TOM'
print(my_name)
#定义变量：存储数据 程序员
schoolName = '程序员'
print(schoolName)
#bug
schoolName = '程序员'
print(schoolname)#NameError:名字错误
schoolName = '程序员'
 print(schoolName)#IndentationError:缩进错误
print(schoolName)
schoolName = '程序员'#NameError
~~~

## 1.5 Debug工具

使用步骤

1. 打断点
2. Debug调试

# 2 数据类型

* int	整型
* float  浮点型
* str	字符串
* bool   布尔型
* list   列表
* set    集合
* dict   字典

# 3 格式化输出

## 3.1 格式符号

| 格式符号 |               转换                |
| :------: | :-------------------------------: |
|    %s    |              字符串               |
|    %d    |         有符号十进制整数          |
|   %02d   | 显示位数，不足以0补全超出原样输出 |
|    %f    |              浮点数               |
|   %.2f   |           小数点后两位            |
|    %c    |               字符                |
|    %u    |         无符号十进制整数          |
|    %o    |            八进制整数             |
|    %x    |       十六进制整数(小写ox)        |
|    %X    |       十六进制整数(大写OX)        |
|    %e    |        科学计数法(小写'e')        |
|    %E    |        科学计数法(大写'E')        |
|    %g    |           %f和%e的简写            |
|    %G    |           %f和%E的简写            |

~~~py
age = 18
name = 'TOM'
weight = 75.5
stu_id = 1
#1.今年我的年龄是xxx岁
print('今年我的年龄是%d岁' % age)
#2.我的名字是xxx
print('我的名字是%s' % name)
#3.我的体重是xxx公斤
print('我的体重是%.2f公斤' % weight)
#4.我的学号是
print('我的学号是%d' % stu_id)
#5.我的名字是xxx，今年xxx岁了
print('我的名字是%s，今年%d岁了' % (name, age))
#5.1我的名字是xxx，明年xxx岁了
print('我的名字是%s，明年%d岁了' % (name, age + 1))
#6.我的名字是xxx，今年xxx岁了，体重xxx公斤，学号是xxx
print('我的名字是%s，今年%d岁了，体重%.02f公斤，学号是%06d' % (name, age, weight, stu_id))
print('我的名字是%s，今年%s岁了，体重%s公斤' % (name, age, weight))
~~~

语法：f'{表达式}'

~~~python
print(f'我的名字是{name}')
~~~

## 3.2 转义字符

\n:换行
\t:制表符

## 3.3 结束符

print('输出的内容'， end="\n")
默认自带end="\n"

~~~python
print('hello', end="\n")
print('world', end="\t")
print('python', end="...")
~~~

# 4 输入

程序接收用户输入的数据的功能

语法：input("提示信息")

~~~python
password = input("输入密码：")
print(f'密码:{password}')
~~~

# 5 转换数据类型

|     函数      |                         说明                         |
| :-----------: | :--------------------------------------------------: |
| int(x[,base]) |                  将x转换为一个整数                   |
|   float(x)    |                 将x转换为一个浮点数                  |
|    str(x)     |                 将对象x转换为字符串                  |
|   eval(str)   | 用来计算在字符串中的有效Python表达式，并返回一个对象 |
|   tuple(s)    |                将序列s转换为一个元组                 |
|    list(s)    |                将序列s转换为一个列表                 |

~~~python
num = input("请输入一个数")
print(num)#str
print(int(num))#int
~~~

# 6 运算符

- 算数运算符
- 赋值运算符
- 复合赋值运算符
- 比较运算符
- 逻辑运算符

# 7 条件语句

## 7.1 if语句

语法
if 条件:
	条件成立执行代码1
	条件成立执行代码2

代码
~~~python
age = 20
if age >= 18:
    print('已经成年，可以上网')    
~~~

~~~python
age = int(input('请输入您的年龄：'))
if age >= 18:
    print(f'您输入的年龄是{age}, 已经成年, 可以上网')
~~~

## 7.2 if…else…语句

~~~python
age = int(input('请输入您的年龄：'))
if age >= 18:
    print(f'您输入的年龄是{age}, 已经成年, 可以上网')
else:
    print(f'您输入的年龄是{age}, 小朋友, 回家写作业去')
~~~

## 7.3 多重判断

语法
if 条件1:
	条件1成立执行的代码1
	条件1成立执行的代码2
elif 条件2:
	条件2成立执行的代码1
	条件2成立执行的代码2
else:
	以上条件都不成立执行的代码

~~~python
age = int(input('请输入您的年龄：'))
if age < 18:
    print(f'您输入的年龄是{age}, 童工')
elif (age >= 18) and (age <= 60):
    print(f'您输入的年龄是{age}, 合法')
elif age > 60:
    print(f'您输入的年龄是{age}, 退休年龄')
~~~

## 7.4 if嵌套

语法
if 条件1:
	条件1成立执行的代码1
	条件1成立执行的代码2
	if 条件2:
		条件2成立执行的代码1
		条件2成立执行的代码2

~~~python
money = 1
seat = 1
if money == 1:
    print('土豪，请上车')
    if seat == 1:
        print('有空座，坐下了')
    else:
        print('没有座位，站着等')
else:
    print('朋友，没带钱，跟着跑，跑快点')
~~~

### 7.4.1 猜拳游戏

~~~python
import random
player = int(input('请出拳:0--石头:1--剪刀:2--布:'))
computer = random.randint(0, 2)
if ((player == 0) and (computer == 1)) or ((player == 1) and (computer == 2)) or ((player == 2) and (computer == 0)):
    print('玩家获胜，哈哈哈哈')
elif player == computer:
    print('平局，别走，再来一局')
else:
    print('电脑获胜')
~~~

### 7.4.2 随机数

~~~python
import random
num = random.randint(0, 2)
print(num)
~~~

## 7.5 三目运算符

条件成立执行的表达式 if 条件 else 条件不成立执行的表达式

~~~python
a = 1
b = 2
c = a if a > b else b
print(c)
aa = 10
bb = 6
cc = aa - bb if aa > bb else bb - aa
print(cc)
~~~

# 8 循环

1. 作用：让代码更高效的重复执行
2. 分类：while和for

## 8.1 while循环

语法
while条件:
	条件成立重复执行的代码1
	条件成立重复执行的代码2
	.\.\.\.\.\.

~~~python
i = 0
while i < 5:
    print('1')
    i += 1
print('2')
~~~

#### 8.1.0.1 while循环应用

 ~~~python
 i = 1
 result = 0
 while i <= 100:
     result = result + i
     i += 1
 print(result)
 ~~~

```python
i = 1
result = 0
while i <= 100:
    if i % 2 == 0:
        result += i
	i += 1
print(result)
```

~~~python
i = 2
result = 0
while i <= 100:
    result += i
    i += 2
print(result)
~~~

### 8.1.1 break和continue终止while循环

break和continue是循环中满足一定条件退出循环的两种不同方式

break：终止此循环
continue：退出当前一次循环继而执行下一次循环代码

~~~python
i = 1
while i <= 5:
    if i == 4:
        print('吃饱了，不吃了')
        break
    print(f'吃了第{i}个苹果')
    i += 1
~~~

```python
i = 1
while i <= 5:
    if i == 3:
        print('吃出一个大虫子，这个苹果不吃了')
        i += 1
        continue
    print(f'吃了第{i}个苹果')
    i += 1
```

### 8.1.2 while循环嵌套

语法
while 条件1:
	条件1成立执行的代码
	while 条件2:
		条件2成立执行的代码

~~~python
j = 0
while j < 3:
    i = 0
    while i < 3:
        print('1')
        i += 1
    print('2')
    print('3')
    j += 1
~~~

#### 8.1.2.1 while嵌套应用

~~~python
j = 0
while j < 5:
    i = 0
    while i <= j:
        print('*', end='')
        i += 1
    print()
    j += 1
~~~

~~~python
j = 1
while j <= 9:
    i = 1
    while i <= j:
    	print(f'{i} * {j} = {i*j}', end='\t')
    	i += 1
    print()
    j += 1
~~~

## 8.2 for循环

语法
for 临时变量 in 序列:
	重复执行的代码1
	重复执行的代码2

~~~python
str1 = 'abcdef'
for a in str1:
    print(a)
~~~

### 8.2.1 break和continue终止for循环

~~~python
str1 = 'abcdef'
for a in str1:
    if a == 'd':
        print('遇到d不打印')
        break
    print(a)
~~~

~~~python
str1 = 'abcdef'
for a in str1:
    if a == 'd':
        print('遇到d不打印')
        continue
	print(a)
~~~

## 8.3 else

循环可以和else配合使用，else下方缩进的代码指的是当循环正常结束之后要执行的代码

语法
while 条件:
	条件成立重复执行的代码
else:
	循环正常结束之后要执行的代码

~~~python
i = 1
while i <= 5:
    print('1')
    i += 1
else:
    print('2')
~~~

### 8.3.1 while…else

#### 8.3.1.1 退出while循环

~~~python
i = 1
while i <= 5:
    if i == 3:
        break
    print('1')
    i += 1
else:
    print('2')
~~~

~~~python
i = 1
while i <= 5:
    if i == 3:
        continue
    print('1')
    i += 1
else:
    print('2')
~~~

break  不执行 else
continue 执行 else

### 8.3.2 for…else

语法
for 临时变量 in 序列:
	重复执行的代码
else:
	循环正常结束之后要执行的代码

~~~python
str1 = 'abcdef'
for a in str1:
    print(a)
else:
    print('循环正常结束之后执行的代码')
~~~

#### 8.3.2.1 退出for循环

~~~python
str1 = 'abcdef'
for a in str1:
    if a == 'd':
        break
	print(a)
else:
    print('循环正常结束之后执行的代码')
~~~

~~~python
str1 = 'abcdef'
for a in str1:
    if a == 'd':
        continue
	print(a)
else:
    print('循环正常结束之后执行的代码')
~~~

break  不执行 else
continue 执行 else

# 9 字符串

## 9.1 下标

下标作用是通过下标快速找到对应的数据
~~~python
str1 = 'abcdefg'
print(str1)
print(str1[0])
print(str1[1])
~~~

## 9.2 切片

语法：序列[开始位置下标:结束位置下标:步长]

~~~python
str1 = 'abcdefg'
print(str1)
print(str1[2])
print(str1[0:3:1])
~~~

## 9.3 常用操作方法

字符串的常用操作方法有查找、修改、判断三大类

### 9.3.1 查找

字符串查找方法即是查找子串在字符串中的位置或出现的次数

* find():检测某个子串是否包含在这个字符串中，如果在返回这个子串开始的位置下标，否则返回-1
  语法：字符串序列.find(子串, 开始位置下标, 结束位置下标)
  注意：开始和结束位置下标可以省略，表示在整个字符串序列中查找

  ```python
  mystr = "hello world and it and zx and Python"
  print(mystr.find('and'))# 12
  print(mystr.find('and', 15, 30))# 23
  print(mystr.find('ands'))# -1
  ```

* index()
  ```python
  mystr = "hello world and it and zx and Python"
  print(mystr.index('and'))# 12
  print(mystr.index('and', 15, 30))# 23
  print(mystr.index('ands'))# index查找子串不存在，报错
  ```

* count()
  ```python
  mystr = "hello world and it and zx and Python"
  print(mystr.count('and', 15, 30))# 1
  print(mystr.count('and'))# 3
  print(mystr.count('ands'))# 0
  ```

rfind()和find功能相同，从右侧开始
rindex()和index功能相同，从右侧开始

### 9.3.2 修改

所谓修改字符串，指的就是通过函数的形式修改字符串中的数据

* replace():替换
  语法：字符串序列.replace(旧子串, 新子串, 替换次数)

  ```python
  mystr = "hello world and it and zx and Python"
  new_str = mystr.replace('and', 'he')
  new_str = mystr.replace('and', 'he', 1)
  new_str = mystr.replace('and', 'he', 10)
  print(new_str)
  ```

  注意：数据按照是否能直接修改分为可变类型和不可变类型两种。字符串类型的数据修改的时候不能改变原有字符串，属于不能直接修改数据的类型即是不可变类型

* split()：按照指定字符分割字符串
  语法：字符串序列.split(分割字符, num)

  ```python
  mystr = "hello world and it and zx and Python"
  list1 = mystr.split('and')
  list1 = mystr.split('and', 2)
  print(list1)# 丢失分割字符
  ```

  注意：如果分割字符是原有字符串中的子串，分割后则丢失该子串

* join()：用一个字符或子串合并字符串，即是将多个字符串合并为一个新的字符串
  语法：字符串.join(过字符串组成的序列)

  ```python
  mylist = ['aa', 'bb', 'cc']
  new_str = '...'.join(mylist)
  print(mylist)
  ```

* capitalize()：将字符串第一个字符转换成大写
* lower()：将字符串中大写转小写
* upper()：将字符串中小写转大写
* lstrip()：删除字符串左侧空白字符
* rstrip()：删除字符串右侧空白字符
* strip()：删除字符串两侧空白字符

* ljust()：返回一个原字符串左对齐，并使用指定字符（默认空格）填充至对应长度的新字符串
  语法：字符串序列.ljust(长度, 填充字符

* rjust()：左对齐
* center()：居中对齐

### 9.3.3 判断

所谓判断即是判断真假，返回的结果是布尔型数据类型：True或False

* startwith()：检查字符串是否是以指定子串开头，是则返回True,否则返回False。如果设置开始和结束位置下标，则在指定范围内检查。
  语法：字符串序列.startwith(子串, 开始位置下标, 结束为止下标)

  ```python
  mystr = "hello world and it and zx and Python"
  print(mystr.startwith('hello'))
  ```

* endwith()
  ```python
  mystr = "hello world and it and zx and Python"
  print(mystr.endwith('Python'))
  ```

* isalpha()：如果字符串至少有一个字符并且所有字符都是字母则返回True,否则返回False
* isdigit()：如果字符串只包含数字则返回True否则返回False
* isalnum()：如果字符串至少有一个字符并且所有字符都是字母或数字则返回True,否则返回False
* isspace()：如果字符串中只包含空白，则返回True,否则返回False

# 10 列表

[数据1, 数据2, 数据3, 数据4 \.\.\.]
列表可以一次性存储多个数据，且可以为不同数据类型

## 10.1 列表的常用操作

### 10.1.1 查找

#### 10.1.1.1 下标

~~~python
name_list = ['TOM', 'Lily', 'ROSE']
print(name_list[1])
print(name_list[0])
~~~

#### 10.1.1.2 函数

* index()：返回指定数据所在位置的下标
  语法：列表序列.index(数据, 开始位置下标, 结束位置下标)

* count()：统计指定数据在当前列表中出现的次数
* len()：访问列表长度，即列表中数据的个数

~~~python
name_list = ['TOM', 'Lily', 'ROSE']
print(name_list.index('TOM'))
print(name_list.count('TOM'))
print(len(name_list))
~~~

### 10.1.2 判断是否存在

* in：判断指定数据在某个列表序列，如果在返回True,否则返回False
* not in：判断指定数据不在某个列表序列，如果不在返回True,否则返回False

~~~python
name_list = ['TOM', 'Lily', 'ROSE']
print('TOM' in name_list)
pritn('TOM' not in name_list)
~~~

#### 10.1.2.1 判断案例

~~~python
name_list = ['TOM', 'Lily', 'ROSE']
name = input('请输入您的邮箱账号名')
if name in name_list:
    print(f'您输入的名字是{name}, 此用户已经存在')
else:
    print(f'您输入的名字是{name}, 名字不存在')
~~~

### 10.1.3 增加

增加指定数据到列表中

* append()：列表结尾追加数据
  语法：列表序列.append(数据)
  注意：如果append()追加的数据是一个序列，则追加整个序列到列表

  ```python
  name_list = ['TOM', 'Lily', 'ROSE']
  name_list.append('xiaoming')
  name_list.append([11, 22f])
  print(name_list)
  ```

* extend()：列表结尾追加数据，如果数据是一个序列，则将这个序列的数据逐一添加到列表
  语法：列表序列.extend(数据)

  ~~~python
  name_list = ['TOM', 'Lily', 'ROSE']
  name_list.extend('xiaoming')
  name_list.extend('xiaoming', 'xiaohong')
  print(name_list)
  ~~~

  

* insert()：指定位置新增数据
  语法：列表序列.insert(位置下标, 数据)

  ```python
  name_list = ['TOM', 'Lily', 'ROSE']
  name_list.insert(1, 'aaa')
  print(name_list)
  ```

### 10.1.4 删除

* del
  语法：del 目标

* pop()：删除指定下标的数据（默认为最后一个），并返回该数据
  语法：列表序列.pop(下标)

* remove()：移除列表中某个数据的第一个匹配项
  语法：列表序列.remove(数据)

* clear()：清空

~~~python
name_list = ['TOM', 'Lily', 'ROSE']
del(name_list)
del(name_list[0])
print(name_list)
del_name = name_list.pop()
print(del_name)
print(name_list)
name_list.remove('ROSE')
print(name_list)
name_list.clear()
print(name_list)
~~~

### 10.1.5 修改

* 逆置：reverse()
* 排序：sort()
  语法：列表序列.sort(key=None, reverse=False)
  注意：reverse表示排序规则，reverse=True降序，reverse=False升序（默认）

~~~python
name_list = ['TOM', 'Lily', 'ROSE']
name_list[0] = 'aaa'
print(name_list)
list1 = [1, 3, 2, 5, 4, 6]
list1.reverse()
print(list1)
list1.sort()
print(list1)
list1.sort(reverse=True)
print(list1)
~~~

### 10.1.6 复制

函数：copy()
