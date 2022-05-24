# 结构体

## 概念

```
    int a = 100;//一次性分配4字节内存空间
    int arr[4];//一次性分配大量内存 元素 数据类型必须一致
    有些场合需要不同种类的 数据类型
    举例：
    分配一段内存来描述学生的信息 ：姓名 年龄 学号 分号
    信息        数据类型
    姓名        字符串 char * / char name[20];
    年龄        unsigned char / int
    学号        unsigned int
    分数        float
    c语言中使用 结构体 来定义用户自己的数据类型
    结构体类似于数组，但是结构中的成员类型可以不一样
```
## 语法格式

```
struct 结构体名称{
    成员列表；
    }
    举例；
    声明一个结构体(不占用内存空间)
    struct student{
    char name[20];
    unsigned char age;
    unsigned int id;
    float score;
    }
    声明一个结构体：声明一个结构体数据类型
    本质上和 int char short long float double 是一个地位
    而struct student 数据类型是开发人员自己定义的
```
### 定义结构体变量

```
-> 方式一
    struct student{
    char name[20];
    unsigned char age;
    unsigned int id;
    float score;
} zs，lisi；
使用s_t作为上述内容替换
s_t zs，lisi；
-> 方式二
a.先声明结构体数据类型
struct student{
char name[20];
unsigned char age;
unsigned int id;
float score;
} zs ，lisi；
b.定义结构体数据变量
struct student zs, lisi;
-> 方式三
typedef关键字
作用：给数据类型起别名
typedef int s32;
int val = 100;
等价于
s32 val = 100;
typedef char s8;
char c = 100;
等价于
s8 c = 100;
//给结构体起别名
//typedef 给struct student 起别名为：stu_t
typedef struct student{
char name[20];
unsigned char age;
unsigned int id;
float score;
}stu_t;
//定义变量
stu_t zs,lidi;
等价于
struct student zs,lisi;
//结构体类型起别名
struct student{
char name[20];
unsigned char age;
unsigned int id;
float score;
}
typedef struct stu_t;
代码:struct2.c
```
```c
#include<stdio.h>
//声明结构体数据类型：描述学生信息 不占用内存空间
typedef struct student{
    char name[20];
    unsigned char age;
    unsigned int id;
    float score;
}stu_t;
int main(void){
    //定义结构体类型变量,且初始化
    //struct student zs = {"张三",19,10086,99.5};
    stu_t zs = {"张三",19,10086,99.5};
    //将变量的内容打印出来
    zs.age = 22;
    printf("%s: %hhu %u %g \n",zs.name,zs.age,zs.id,zs.score)
    return 0;
};
```
代码:
```c
#include<stdio.h>
//声明结构体数据类型：描述学生信息 不占用内存空间
struct student{
    char name[20];
    unsigned char age;
    unsigned int id;
    float score;
}
int main(void){
    //定义结构体类型变量,且初始化
    struct student zs = {"张三",19,10086,99.5};
    //将变量的内容打印出来
    zs.age = 22;
    printf("%s: %hhu %u %g \n",zs.name,zs.age,zs.id,zs.score)
    return 0;
};
```
### 结构体类型变量的初始化
```
->方式一
    struct student zs = {"张三",19,10086,99.5}；
    给结构体中所有成员变量，按照次序依次赋值
    不同变量之间使用，隔开
    ->方式二
    有点时候初始化，不要全部初始化
    初始化的时候，不想按照顺序初始化
    不同成员变量初始化需要使用","隔开
    标记初始化
    格式：
     成员变量名 = 值
    stu_t zs = {
    .score = 100,
    .name  = "张三",
    .id    = 10086
    };
代码:
```
```c
#include<stdio.h>
//声明结构体数据类型：描述学生信息 不占用内存空间
typedef struct student{
    char name[20];
    unsigned char age;
    unsigned int id;
    float score;
}stu_t;
int main(void){
    //定义结构体类型变量,且初始化
    //struct student zs = {"张三",19,10086,99.5};
    stu_t zs = {"张三",19,10086,99.5};
    stu_t xb = {
        .age =25,
        .name = "蜡笔小新",
        .id   = 10010
    };
    //将变量的内容打印出来
    zs.age = 22;
    printf("%s: %hhu %u %g \n",zs.name,zs.age,zs.id,zs.score);
    pritnf("%s: %hhu %u \n",xb.name,xb.age,xb.id);
    return 0;
};
```
### 结构体变量的使用

1.通过"."运算符来访问结构体变量的成员
语法格式：
变量名.成员变量名
2.通过"->" 运算来访问结构体变量的成员
语法格式：
指针->成员变量名
举例：
stu_t zs = {"张三",19,10086,99.5};
stu_t*p = &zs;//p存储的是zs变量的地址
p->age = 22;
代码:
```c
#include<stdio.h>
//声明结构体数据类型：描述学生信息 不占用内存空间
typedef struct student{
    char name[20];
    unsigned char age;
    unsigned int id;
    float score;
}stu_t;
int main(void){
    //定义结构体类型变量,且初始化
    //struct student zs = {"张三",19,10086,99.5};
    stu_t zs = {"张三",19,10086,99.5};
    stu_t xb = {
        .age =25,
        .name = "蜡笔小新",
        .id   = 10010
    };
    stu_t*p = &xb;
    //将变量的内容打印出来
    zs.age = 22;
    p->age = 26;
    printf("%s: %hhu %u %g \n",zs.name,zs.age,zs.id,zs.score);
    pritnf("%s: %hhu %u \n",xb.name,xb.age,xb.id);
    return 0;
};
```
typedef struct student{
char name[20];
unsigned char age;
unsigned int id;
float score;
}stu_t;
结构体之间的赋值
普通变量的赋值操作：
int a = 100;
int b;
b = a;
结构体之间的赋值操作：
stu_t zs = {
.id  = 10000,
.age = 18
};
stu_t*p = &zs;
stu_t s1 = zs; //将zs结构体变量 对应内存中的数据拷贝一份到s1对应的内存中
stu_t s2 = *p; //将zs结构体变量 对应内存中的数据拷贝一份到s2对应的内存中
//先获取变量p的内容 - zs的地址 - *zs的地址 - 获取的是结构体变量zs的内容
代码:
```c
#include<stdio.h>
//声明结构体数据类型：描述学生信息 不占用内存空间
typedef struct student{
    char name[20];
    unsigned char age;
    unsigned int id;
    float score;
}stu_t;
int main(void){
    //定义结构体类型变量,且初始化
    //struct student zs = {"张三",19,10086,99.5};
    stu_t zs = {"张三",19,10086,99.5};
    stu_t xb = {
        .age =25,
        .name = "蜡笔小新",
        .id   = 10010
    };
    stu_t*p = &xb;
    //将变量的内容打印出来
    zs.age = 22;
    p->age = 26;
    printf("%s: %hhu %u %g \n",zs.name,zs.age,zs.id,zs.score);
    pritnf("%s: %hhu %u \n",xb.name,xb.age,xb.id);
    //结构体变量之间的赋值操作
    stu_t s1 = zs;
    stu_t s2 = *p;
    printf("s1:name:%s,age:%d\n",s1.name,s1.age);
    printf("s2:name:%s,age:%d\n",s2.name,s2.age);
    return 0;
};
```
### 结构体嵌套

结构体的成员还是结构体
typedef struct B {
int a;
int b;
}B_t;
typedef struct C {
int c;
int b;
B_t e; //说明结构体c包含结构体B
}C_t;
C_t zhangsan;
初始化具有 结构体成员变量的 结构体变量并访问其成员变量
代码:
```c
#include<stdio.h>
typedef struct birthday {
    int year;
    int month;
    int day;
}birth_t;
//声明学生结构体数据类型
typedef struct student {
    char name[20];
    unsigned char age;
    unsigned int id;
    float score;
    birth_t birth;//描述学生的出生日期
}stu_t;
int main(void){
    //包含结构体成员变量的初始化
    stu_t s1 = {"张飞",20,1003,99.5,{2002,4,20}};
    printf("%s: %hhu, %d, %f, %d-%d-%d \n",s1.name,s1.age,s1.id,s1.score,s1.birth.year,s1.birth.month,s1.birth.day);
    stu_t*p = &s1;
    printf("%s: %hhu, %d, %f %d-%d-%d\n",p->name,p->age,p->id,p->score,
    p->birth.year,p->birth.month,p->birth.day);
    return 0;
}
```
访问成员变量方式
typedef struct student {
char name[20];
unsigned char age;
unsigned int id;
float score;
birth_t birth;//描述学生的出生日期
}stu_t;
stu_t s1 = {"张飞",20,1003,99.5,{2002,4,20}};
stu_t*p  = &s1;
s1.name
<<<<<<< HEAD
p->name
```
内存，地址 - 指针，函数，结构体
变量：数据，可以修改，存储在内存中
内存：数据(变量)，存储在内存中
内存分布：有一格一格组成的，每一格 - 字节 - 用于存储数字
                                   |
                                  编号：从0开始依次递增，到4G
                                   |
                                  地址：内存字节地址 内存地址
    需要一个或者多个字节，存储数据
               |
        连续一个/多个字节 形成的存储单元
               |
          存储区/缓冲区
               |
        单字节 - 字节编号 - 地址
        多字节 - 存储区 - 寻找字节第一个自己的编号 - 地址(首地址：存储单元的第一个字节的地址)
    通过定义变量来分配内存空间储存数字
        定义变量实质：
            integer 整数
            int -> 编译器就会在内存分配4字节的存储空间
    通过地址编号的方式来访问 变量 中的数据
        &val - val这块存储区的地址
        * - 解引用 - *&val - 获取地址上的数据
    数组：存储多个数据的方法
    int arr[5] = [1,2,3,4,5];
    数据：1   2   3   4   5
         ———————————————————
    下标：0   1   2   3   4
```
```c
#include<stdio.h>
int main(void){
    int arr[5] = {1,2,3,4,5};
    arr[5] = 100;
    printf("%d\n",arr[5]);
    return 0;
}
```
```
数组越界访问，会造成严重后果，往往程序崩溃
    打印数组中的所以元素：
    for(int i=0; i<5;i++){
    printf("%d",a[i]);
    }
    printf("\n");
    0   1   2   3   4 ->数组的下标递增，步长为1
    打印数组中下标为偶数的所有数据；arr[5]
    for(int i=0;i<5;i+=2){
    printf("%d",arr[i]);
    }
    printf("\n");
    arr[0] arr[1] arr[2]...
    看做是普通变量 - 也是存储区的名字 - 存储区地址 - &arr[i]
    数组名，也是数组的首地址，也是第一个地址的首地址
    arr[1] - *(arr+1)
**指针**：存储地址的方法
    地址 - 编号 - 数字 - 指针就是地址
    指针变量 - 存储地址的变量 - 存储的是内存的一个编号
    int*p = & val;//定义指针变量p，存储的是val变量的地址
    *p = & val;
    p存储val变量的地址
    *p - p获取val的变量地址 - 再获取地址上的数据
    指针的运算：
    指针 + 数字 = 地址 + n * sizeof(type)
    char c ='m';
    char *pc = & c;//假如c的地址为0x1000
    pc++; //pc+=1; 0x1000 + 1 * sizeof(char) = 0x1000 + 1 = 0x1001
    int i = 100
    char*pi = *& i;//&i = 0x1000
    pi++; //pi +=1 pi = 0x1004
```


代码:

```c
#include<stdio.h>
int main(void){
    int arr[5] = {1,2,3,4,5};
    for(int i=0;i<5;i++){
        printf("%d",*(arr+i));
    }
    printf("\n-----------------------\n");
    printf("arr=%p\n",arr);
    printf("&arr[0]=%p\n",&arr[0]);
}
```
结构体数组
```
typedef struct student{
int age;
int id;
}stu_t;
stu_t xx = {...};
stu_t zd = {...};
stu_t qw = {...};
定义大量结构体变量，代码将会变得及其繁琐
采用结构体数组的方式优化
//其中每一个元素都是stu_t类型的结构体变量
stu_t arr[39] = { //结构体类型变量d初始化
{19,1001},
{19,1002},
{20,1003},
{...}
}
```
代码：
```c
#include<stdio.h>
typedef struct{
    char name[20];
    unsigned char age;
}stu_t;
int main(void){
    //定义结构体数组记录学生的信息
    stu_t arr[] = {
        {.age = 46, .name = "皇叔"},
        {"二哥",45},
        {"豆芽儿",44}
    };
    for(int i=0;i<3;i++){
        printf("%s: %d \n",arr[i].name, arr[i].age);
        printf("%s: %d \n",(*(arr+i)).name,(*(arr+i)).age);
    }
    //指针p指向了arr[0] p指向了一个stu_t类型的结构体变量
    stu_t*p = arr;
    for(int i=0;i<3;i++){
        printf("%s: %d \n",(p+i)->name,(p+i)->age);
    }
    return 0;
}
```
数组：
```
int arr[5] = {1,2,3,4,5};
arr：   1   2   3   4   5
———————————————————
下标：  0   1   2   3   4
数组名称：arr 数组的首地址
*(arr+0)第0个元素的数据
*(arr+1)第1个元素的数据
结构体内存对齐/补齐问题
结构体内存对齐：
结构体中每个成员的起始地址必须是自己内存大小(字节)的整数倍
超过int的按4算
结构体变量的起始地址必须是4的倍数
代码:
```
```c
#include<stdio.h>
struct A{
    char a;
    int b;
};
struct B{
    char a;
    short C;
    int b;
};
int main(void){
    printf("sizeof(struct A)=%d\n",sizeof(struct A)); //8
    printf("sizeof(struct B)=%d\n",sizeof(struct B)); //8
    return 0;
}
```
```
结构体和函数
    结构体变量可以作为函数的参数进行传递
    结构体变量地址可以作为函数的参数进行传递
        如果需要结构体信息作为函数的参数，建议使用传递结构体变量的地址方式来实现
函数的形参，可以看做该函数的局部变量，而传递实参就是在给该形参赋值的过程
当使用结构体变量指针作为函数形参的时候，不想修改结构体变量的值，
    可是从实际上，是可以修改的
    void pshow(stu t *pst)
    {
        printf("%s:%d\n",pst->name,pst->age);
        pst->age++;
    }
```


代码:

```c
//01struct.c
#include<stdio.h>
//声明结构数据类型
struct student{
    unsigned char age;
    char name[20];
};
typedef struct student stu_t;
void show(stu_t st){
    printf("%s:%d\n",st.name,st.age);
}
void grow(stu_t st){
    st.age++;
}
void pshow(stu_t *pst){
    printf("%s:%d\n",pst->name,pst->age);
}
void pgrow(stu_t *pst){
    pst->age++;
}
int main(void){
    stu_t s1={21,"xb"};
    show(s1);
    grow(s1);
    pshow(&s1);
    pgrow(&s1);
    pshow(&s1);
    retrun 0;
}
```
计算长方形面积
A(x1,y1),B(x2,y2)
//描述一个点坐标的结构体
typedef struct{
    int row;
    int col;
}pt_t;
//描述一个长方体的结构体
typedef struct{
    pt_t p1;
    pt_t p2;
}rect_t;
定义变量：
rect_t r = {0};
printf("请输入长方形的位置:");
    1 x y
    2 x y
代码:
```c
#include <stdio.h>
typedef struct {
    int row;
    int col;
} pt;
typedef struct {
    pt pt1;
    pt pt2;
} rect;
int main() {
    int area = 0;
    rect r = {0}, *p_r = NULL;
    printf("请输入水平长方形的位置：");
    / * scanf("%d%d%d%d", &(r.pt1.row), &(r.pt1.col), &(r.pt2.row), &(r.pt2.col));
    area = (r.pt1.row - r.pt2.row) * (r.pt1.col - r.pt2.col); * /
    p_r = &r;
    scanf("%d%d%d%d", &(p_r->pt1.row), &(p_r->pt1.col), &(p_r->pt2.row), &(p_r->pt2.col));
    area = (p_r->pt1.row - p_r->pt2.row) * (p_r->pt1.col - p_r->pt2.col);
    area = area >= 0 ? area : 0 - area;
    printf("面积是%d\n", area);
    return 0;
}
```

联合体（联合/共用体）
	1.基本语法
		和结构体非常类似，将关键字struct换成union
		联合体中所以的成员共用一块内存，优点是省内存
		联合体中占用内存按照成员中占用内存最大的来计算
		定义初始化联合体变量
		union A test ={.c=100};//强制

代码:
union.c

```c
#include<stdio.h>
typedef union A{
    int a;
    double b;
}A_t;
int main(void){
    A_t data1={200};
    A_t data2={.b=1.2};
    printf("datal.a=%d\n",datal.a);
    printf("data2.b=%lg\n",data2.b);
    printf("a的地址为：%p\n",&data1.a);
    printf("b的地址为：%p\n",&data2.b);
    printf("sizeof(data1)=%d\n",sizeof(data1));
    return 0;
}
```

经典使用
struct Student{
	char name[20];
    char sex;
    char job;
}

代码:
union2.c

```c
#include<stdio.h>
struct Student{
    char name[20];
    char sex;
    char job;
    union{
        int class;//班级
        char position[10];//位置
    }category;//定义了联合体类型变量category
};
int main(void){
    struct person persons[2]={
        {.name="xm",.sex='m',.job='s,.category.class=1903'},
        {.name="lz",.sex='f',.job='tf',.category.position="教授"}
    };
    for(int i=0;i<2;i++){
        if(persons[i.job]=='s'){
            printf("姓名：%s，性别：%c，班级:%d\n",persons[i].name,persons[i].sex.persons[i].category.class)
        }else{
            printf("姓名：%s，性别：%c，职称:%s\n",persons[i].name,persons[i].sex,persons[i].catego.position)
        }
    }
    return 0;
}
```

arm架构，既支持大端模式，也支持小端模式
X86架构，也是都支持的
PowerPC，大端模式 
网络字节序，大端模式 

代码:
union3.c

```c
#include<stdio.h>
union{
    int a;
    char c[4];
}test;
int main(void){
    test.a = 1;
    if(test.c[0] == 1){
        printf("小端\n");
    }else{
        printf("大端\n");
    }
    return 0;
}
```

枚举
	枚举是一个整型常量列表，每个值都是枚举常量（整型）
枚举的值默认从0开始，向后依次递增（每次加1）
	但是可以赋值改变
语法格式
	enum枚举类型名称（枚举值列表）；

代码:
enum.c

```c
#include<stdio.h>
int main(void){
    enum COLOR {RED,GREEN=200,BLUE};
    printf("%d%d%d\n",RED,GREEN,BLUE);
    ruturn 0;
}
```

函数指针
	可以使用指针指向整型变量字符串数组，也可以指向一个函数
	一个函数在编译的时候会被分配一个入口地址，这个入口地址就称为函数的指针(地址)

```c
int add(int a,int b){
printf("enter $s\n",func )
return a+b;
```

以上函数add在内存中的地址就是函数名add,add代表函数的入口地址

__ func __：标准库提供的宏，表示当前函数名称

函数指针变量的定义
语法：返回值类型(*var_name)(形参列表)；

举例 :
    int (*pfunc)(int, int);
      定义了一个指针变量 
      该变量占据了4字节内存空间
      该4字节内存空间存储一个函数的地址 
      存储的函数有什么要求吗?
      存储的函数 : 返回值为int类型, 参数为int,int类型的函数的地址

  赋值 : 
    函数指针 = 函数名 ;

  举例 :
    pfunc = add;

  调用 :
    函数指针(形参表);

​    pfunc(10, 20); 
​    == 
​    add(10, 20);
​    ==
​    (*pfunc)(10, 20);

​    int* pfunc(int, int); 
​      定义了一个函数
​      返回值是一个 int* 

程序编译 

arm-cortex_a9-linux-gnueabi-gcc -nostdlib -c -o uart.o uart.c
arm-cortex_a9-linux-gnueabi-gcc -nostdlib -c -o main.o main.c
arm-cortex_a9-linux-gnueabi-ld -nostartfiles -nostdlib -Ttext=0x48000000 -emain -o uart.elf main.o uart.o
arm-cortex_a9-linux-gnueabi-objcopy -O binary uart.elf uart.bin
cp uart.bin /tftpboot

代码：
pfunc.c

```c
#include<stdio.h>
int add(int a,int b){
	printf("enter %s\n",__func__)
	return a+b;
}
int sub(int a,int b){
	printf("enter %s\n",__func__)
	return a-b;
}
int main(void){
	printf("add函数的地址p\n"i,add);
//定义函数指针
	int (*pfunc)(int,int)NULL;
	pfunc add;
	int ret (*pfunc)(10,20);
	printf("ret=%d\n",ret);
    pfunc=sub;
    printf("sub函数地址：%p %p %p %p\n",sub,*sub,pfunc,*pfunc);
    ret =pfunc(20,10);
    printf("ret=%d\n",ret);
	return 0;
}
```

typedef给函数指针类型起别名
	typedef返回值类型(*type name)(形参列表)；
		此时type_name 而是函数指针类型的数据类型

举例 :
    typedef int (*pfunc_t)(int, int);
      起了个别名为 pfunc_t
      给 int (*)(int) 起了个别名
      给返回值为int, 参数为int,int的函数指针起了别名 
      不分配内存空间的

​    pfunc_t pfunc;
​      定义了一个指针变量 
​      该变量占据了4字节内存空间 
​      该4字节内存空间存储一个函数的地址 
​      存储的函数有什么要求吗?
​      存储的函数 : 返回值为int类型, 参数为int,int类型的函数的地址

​    pfunc = add;

代码：
02pfunc.c

```c
#include <stdio.h>
typedef int (*pfunc_t)(int, int);
int add(int a, int b){
    printf("enter %s\n", __func__);
    return a+b;
}
int sub(int a, int b){
    printf("enter %s\n", __func__);
    return a-b;
}
// 形参相当于局部变量
// int a;
// int b;
// pfunc_t pfunc;
// 调用实参
// clac(100, 200, add);
// int a= 100
// int b= 200;
// pfunc_t pfunc = add;
// pfunc == add == NULL ?? 
// return pfunc(a,b); == return add(a,b);
int calc(int a, int b, pfunc_t pfunc){
    if(NULL == pfunc){
        return a*b;
    }else{
        return pfunc(a,b);
    }
}
int main(void){
    int ret = 0;
    ret = calc(100, 200, add);
    printf("ret=%d\n", ret);
    ret = calc(100, 200, sub);
    printf("ret=%d\n", ret);
    ret = calc(100, 200, NULL);
    printf("ret=%d\n", ret);
    return 0;
}
```

03pfunc.c

```c
#include <stdio.h>
typedef int (*pfunc_t)(int, int);
int add(int a, int b){
    printf("enter %s\n", __func__);
    return a+b;
}
int sub(int a, int b){
    printf("enter %s\n", __func__);
    return a-b;
}
int mul(int a, int b){
    printf("enter %s\n", __func__);
    return a*b;
}
int div(int a, int b){
    printf("enter %s\n", __func__);
    return a/b;
}
int mod(int a, int b){
    printf("enter %s\n", __func__);
    return a%b;
}
// 定义函数指针数组 数组中每个元素都是一个函数的地址
pfunc_t arr[] = {add, sub, mul, div, mod};
int main(void){
    int len = sizeof(arr) / sizeof(arr[0]);
    pfunc_t pfunc = NULL;
    int ret = 0;
    for(int i=0; i<len; i++){
        pfunc = arr[i];
        ret = pfunc(200, 20);
        printf("ret=%d\n", ret);
    }
    return 0;
}
```

函数指针的经典使用场景 
  利用函数指针数组实现遍历调用所有的指定函数 

  嵌入式中一般系统上电 先做一系列的硬件初始化功能 
    cpu dram time net flash ...

代码：
04pfunc.c

```c
```



多级指针 : 二级指针 
回顾 一级指针 
  指向普通变量的内存区域 
  int a = 200;
  int* p = &a; //p保存了变量a的地址 p指向a 
  int b = *p; //读取p指向内存中的数据 
  *p = 100; //修改p指向内存中的数据 

二级指针 
  指向一级指针变量的指针 
  也就是二级指针存储一级指针变量的地址 

  语法格式 :
    数据类型 **二级指针变量名 = 一级指针变量的地址;

  举例 :
    int a = 200;
    int *p = &a;
    //pp:二级指针 
    // 存储的是指针变量p的地址 
    int **pp = &p;
    //*pp = p 
    **pp = 100; // 等价于 a = 100, *p = 100

代码：
ppointer.c

```c
#include<stdio.h>
int main(void){
    int a=200;
    int *p=&a;
    int **pp=&p;
    printf("a=%d,%d",a,*p,**pp);
    int b 20;
	p=&b;
	printf("%d\n",**pp);//20
	int *pl &b;
	pp &p1;
	printf("%d\n",**pp);//20
	pp &p;
	*pp &a;
	printf("%d\n",**pp);//200
	return 0;
}
```

使用场景
定义函数swap 实现字符串的交换
char* pa=“hello”;
char* pb=“world”;

定义swap函数，效果：
	pa -> “world”;
	pb -> “hello”;
代码：
swap.c

```c
#include<stdio.h>
void swap(char** ps1,char** ps2){
    char* tmp=*ps1;
    *ps1=*ps2;
    *ps2=tmp;
}
int main(void){
    char* pa="hello";
    char* pb="world";
    swap(&pa,&pb);
    printf("pa=%s\n", pa);
    printf("pb=%s\n", pb);
    return 0;
}
```

实现两个数据的交换：
实现变量的交换 - 一级指针
实现指针的交换 - 二级指针

二级指针和字符数组
char* arr[]={"hello", "world"};
	arr[0] char* 类型的数据，也就是“hello”字符串的首地址
	arr[1] char* 类型的数据，也就是“world”字符串的首地址

数组中每个元素都是char*类型的指针(地址)
arr是数组中第0元素的地址，char*类型的地址
	arr存储的是char*类型的地址，具有二级指针的意思

所以，可以定义一个二级指针变了来保存字符指针数组的首地址
char** parr = arr;

代码：
ppstring.c

```c
#include <stdio.h>
int main(void){
    char* arr[] = {"hello", "world"};
    //char** p = arr[0];//p指向了"hello"
    char** p = arr;//p指向了arr数组
    printf("%s %s\n", arr[0], arr[1]);// hello world
    printf("%s %s\n", p[0], p[1]);// hello world
    printf("%s %s\n", *(arr+0), *(arr+1));
    printf("%s %s\n", *(p+0), *(p+1));
    return 0;
}
```

p++; ok 
arr++; //error 

sizeof(arr) / sizeof(arr[0])
数组总字节数    第一个元素字节数  数组元素个数
sizeof(p) / sizeof(p[0])  error 
   4/8           4

二级指针和main函数
int main (void){..
int main(int argc,char**argv){...]
等价于
int main (int argc,char*argv[]){...]

代码：
main.c

```c
#include<stdio.h>
int main(int argc,char** argv){
    for(int i = 0; i<argc; i++){
        printf("%s\n",argv[i]);
    }
    if(!(strcmp(argv[1],"add"))){
        printf("add\n");
    }
    return 0;
}
```

main2.c
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
int add(int a, int b){
    return a+b;
}
int sub(int a, int b){
    return a-b;
}
int mul(int a, int b){
    return a*b;
}
int div2(int a, int b){
    return a/b;
}
int calc(int a, int b,pfunc_t pfunc){
    if(NULL == pfunc){
        return 0;
    }else{
        pfunc(a, b);
    }
}
int main(int argc, char** argv){
    if(argc != 4){
        printf("usage:<%s> add/sub/mul/div num1 num2\n", argv[0]);
        return -1;
    }
    int ret = 0;
    int val1 = strtoul(argv[2], 0, 10);
    int val2 = strtoul(argv[3], 0, 10);
    if(!(strcmp(argv[1], "add"))){
        ret = add(val1, val2);
        printf("%d+%d=%d\n", val1, val2, ret);
    }else if(!strcmp(argv[1],"sub")){
        ret = calc(val1, val2,sub);
        printf("%d-%d=%d\n", val1, val2, ret);
    }else if(!strcmp(argv[1],"mul")){
        ret = calc(val1, val2,mul);
        printf("%d*%d=%d\n", val1, val2, ret);
    }else if(!strcmp(argv[1],"div2")){
        ret = calc(val1, val2,div2);
        printf("%d/%d=%d\n", val1, val2, ret);
    }else{
        printf("please input valid command!\n");
    }
    return 0;
}
```

动态内存分配和释放
int val = 100;
int arr[10];

结构体变量：都属于静态内存分配的方式
占据的内存空间大小已经定死

动态分配内存，自定义内存空间大小
使用maalloc/free这一组函数

mal1oc/free函数详解
```c
#include <stdlib.h>
void *malloc(size t size);
```

功能：从堆区中分配内存
参数：size:size_t,unsigned long
	需要分配size个字节
返回值：
失败	返回NULL
成功	返回该内存块的起始地址

void free(void *ptr);
功能：释放内存空间
参数：ptr：malloc函数返回值
	内存分配空间首地址

注意：
释放后记得p赋值为NULL，否则否则p就变为了野指针 
  free(p);
  p = NULL;
申请了内存空间, 要记得释放内存
申请一次, 释放一次, 切记不要释放两次, 导致段错误出现

代码：
malloc.c

```c
#include<stdlib.h>
#include<stdio.h>
int main(void){
    int *p = NULL;
    p = (int *)malloc(8);
    if(NULL == p){
        printf("失败\n");
        return -1;
    }
    *(p+0) = 100;
    *(p+1) = 200;
    printf("%d %d\n", *(p+0), *(p+1));
    free(p);
    P = NULL;
    return 0;
}
```

malloc动态申请的内存空间的生命周期
	malloc申请的内存，生命周期开始
	当free或者程序结束后生命周期结束

代码：
malloc.c

```c
#include<stdio.h>
void* func (int size){
    return malloc(size);
}
int main(void){
    int *p = NULL;
    p = func(8);
    if( NULL == p){
        printf("失败\n");
        return -1;
    }
    *(p+0) = 100;
    *(p+1) = 200;
    printf("%d %d\n",*(p+0),*(p+1));
    free(p);
    return 0;
}
```

02malloc.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
typedef struct student{
    int age;
    char name[20];
}stu_t;
stu_t* get_stu_info(void){
    stu_t* p = (stu_t*)malloc(sizeof(stu_t));
    if(NULL == p){
        printf("分配内存失败.\n");
        return NULL;
    }
    p->age = 18;
    strcpy(p->name, "吕布");
    return p;
}
int main(void){
    stu_t* pstu = get_stu_info();
    printf("%s : %d \n", pstu->name, pstu->age);
    free(pstu);
    pstu = NULL;
    return 0;
}
```

03malloc.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
typedef struct student{
    int age;
    char name[20];
}stu_t;
stu_t* get_stu_info(const char* name, int age){
    stu_t* p = (stu_t*)malloc(sizeof(stu_t));
    if(NULL == p){
        printf("分配内存失败.\n");
        return NULL;
    }
    p->age = age;
    strcpy(p->name, name);
    return p;
}
#define LEN (4)
int main(void){
    stu_t* arr[LEN] = {NULL};
    char name[20] = {0};
    for(int i = 0; i < LEN; i++){
        printf("请输入学生的姓名:");
        scanf("%s", name);
        arr[i] = get_stu_info(name, i+18);
    }
    for(int i = 0; i < LEN; i++){
        printf("%s : %d\n", arr[i]->name, arr[i]->age);
    }
    for(int i = 0; i < LEN; i++){
        free(arr[i]);
        arr[i] = NULL;
    }
    return 0;
}
```

calloc函数 
\#include <stdlib.h>
void *calloc(size_t nmemb, size_t size);
参数:
  nmemb:n member,从堆区中分配包含nmemb个元素的数组
  size:每个元素占据size个字节 
返回值:
  失败  返回NULL
  成功  返回该数组的起始地址 

和malloc最大的区别 :
  calloc得到的内存的值被全部初始化为对应类型的0 
  malloc得到的内存空间存储的值不可预知(随机数)

calloc.c

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
int main(void){
    int *a = (int *)calloc(5, sizeof(int));
    if(NULL == a){
        printf("失败\n");
        return -1;
    }
    printf("成功，首地址%p\n",a);
    a[0] = 520;
    *(a+1) = 521;
    for(int i = 0;i<5;i++){
        printf("%d",a[i]);
    }
    printf("\n");
    free(a);
    a = NULL;
    struct point{
        int x;
        int y;
    }*p;
    p = calloc(3, sizeof(struct point));
    (p+0)->x = 1;
    (p+0)->y = 2;
    (p+1)->x = 10;
    (p+1)->y = 20;
    for(int i = 0; i < 3; i++){
        printf("%d, %d\n", p[i].x, p[i].y);
    }
    free(p);
    p = NULL;
    return 0;
}
```



