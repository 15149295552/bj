# 一 内存布局

代码
```C
#include<stdio.h>
#include<stdlib.h>
int g = 10;
int g3;  //全局变量g3 未初始，bss段 bss段默认初始为0
int g2 = 20;
void add();
void add(){
  int c=30+20;
}
int main(int argc,char *argv[]){
    static int s=0; //局部可见 全局生命
    int a = 0;
    printf("argc地址=%p\n",&argc);
    printf("argv地址=%p\n",argv);
    printf("------------命令行参数-------------\n");
    printf("局部变量a地址 %p\n"&a);
    printf("---------------栈区---------------\n");
    int *pi=(int *)malloc(10*sizeof(int));
    printf("动态内存申请的内存地址 %p\n",pi);
    printf("---------------堆区---------------\n");
    printf("未初始全部变量g3地址 %p\n",&g3);
    printf("--------------bss段---------------\n");
    printf("静态局部变量s地址 %p\n",&s);
    printf("全部变量g2地址 %p\n",&g2);
    printf("全部变量g地址 %p\n",&g);
    printf("--------------数据段--------------\n");
    printf("字符串常量hello world内存地址 %p\n",pc);
    printf("------------只读数据段-------------\n");
    //函数就是指令首地址
    printf("main函数的内存地址 0x%p\n",main);
    printf("add函数的内存地址 0x%p\n",add);
    printf("--------------代码段--------------\n");
    printf("\n");
    printf("-----------------0---------------\n");
    return 0;
}
```
# 二 虚拟内存
## 1内存布局
    环境变量和命令行参数
    --------------------
    栈区
    ----
    V
    ^
    -
    堆区
    ----
    bss区
    -----数据区
    size命令:
    可以查看可执行程序代码区，数据区和bss区的大小
    代码区
    ------
    使用格式:
    size 可执行文件名称
    size a.out
    text    data    bss   edc   hex filename
    1182    552     8     1742  6ce a.out
    单位：字节
    代码区(test) 数据区(data) bss区
    dec:十进制
    hex:十六进制
    bin:二进制
    oct:八进制
## 2 内存壁垒
    虚拟内存大小为4GB
    将4GB字节大小的内存分为了两个部分：
    0 ~ 3G-1： 用户空间，存放程序员编写的程序中的代码和数据
    每个程序/进程 的用户空间都是0 ~ 3G-1，但不同进程所对应的物理内存确实各自独立的，
    Linux系统会为每个运行的程序的用户空间维护一张专属该程序的 内存映射表，
    记录的是 虚拟内存到物理内存之间的对应关系，因此在不同的进程（运行的程序）之间
    交换 虚拟内存的地址 是毫无意义的
    程序A 程序B
    3G ~ 4G-1：内核空间，存放Linux内核的代码和数据
    不同的程序运行的时候 访问的内核空间的代码和数据是同一份，
    用户空间的内存映射会随着进程的切换而切换
    内核空间的内存映射无需随着进程的切换而切换
    用户空间的代码不能直接访问内存空间的代码和数据
    但是可以通过系统调用，间接的和内核互换
### 2.1段错误
    一切对虚拟内存的 越权访问，都会导致 段错误
    试图访问没有映射到物理内存的虚拟内存
    试图以非法方式来访问虚拟内存，如：对只读内存做写操作 等
## 3虚拟内存的分配和释放
#### 3.1从底层硬件到上层应用，各层的逻辑
```
------------------------------------
应用程序           业务逻辑
stl               标准容器
c++               new/delete
c                 malloc/calloc/realloc/free
posix             sbrk/brk
Linux             mmap/munmap
------------------------------------
    ^---用户层
------------------------------------
    操作系统内核    kmalloc/vmalloc
    操作系统驱动    get_free_page
    硬件           硬件指令集
------------------------------------
    ^---系统层
从底层硬件到上层应用，各层提供了各自的 内存管理 接口，
    处于不同的开发层次，会使用不同层次的功能函数
```
### 3.2 sbrk函数
```
想要在虚拟内存分配一块空间，建立和物理内存之间的映射
    后续直接操作虚拟内存即可
后续不再想使用的时候，断开虚拟内存和物理内存之间的映射
```
```C
#include<unistd.h>
void *sbrk(intptr_t increment);
```
    功能：以相对的方式 分配 和 释放 虚拟内存
    参数：
    increment 内存的字节增量（单位：字节）
        >0    分配内存
        <0    释放内存
        =0    当前堆尾
    当前堆尾指针，需要向右移动increment个字节
    返回值：
    成功    返回调用该函数前的堆尾指针
    失败    返回-1
    分配和释放内存，操作的堆区
    由操作系统分配的，栈区/bss段/数据段
    由开发人员分配的，一定在堆区
    sbrk分配内存的底层实现；
    系统内存维护着一个指针，指向当前堆尾，即堆区最后一个字节的下一个位置
    是一个动态调整的指针
    sbrk函数根据增量参数来调整该指针的位置
    于此同时，会返回该指针在调整前的位置
    举例
    p1 = sbrk(4);  //BBBB ^--- ---- ---- ----
                    //BBBB BBBB ^--- ---- ----
    p2 = sbrk(4);  //BBBB BBBB ^--- ---- ----
                    //BBBB BBBB BBBB ^--- ----
    p3 = sbrk(0);  //BBBB BBBB BBBB ^--- ----
                    //BBBB BBBB BBBB ^--- ----
    p4 = sbrk(-8); //BBBB BBBB BBBB ^--- ----
                    //BBBB ^--- ---- ---- ----
    B；已分配的字节
    -；未分配的字节
    ^；当前堆尾位置
    int brk(void *addr);
    Linux终端：
    man 2 sbrk
    sbrk代码
```C
#include<stdio.h>
#include<string.h>
#include<unistd.h>
int main(void){
    void*p1 = sbrk(0);
    printf("p1 ：%p\n",p1);
    int*p2=sbrk(sizeof(int));
    *p2=520;
    printf("%d\n",*p2);
    double*p3 = sbrk(sizeof(double));
    *p3=13.14;
    printf("%lg\n",*p3);
    char*p4 = sbrk(16*sizeof(char));
    strcpy(p4,”hello,world");
    printf("%s\n",*p4);
    sbrk(-16*sizeof(char)-sizeof(double)-sizeof(int));
    void*p5 = sbrk(0);
    printf("%p\n",p5);
    return 0;
}
```
```C
#include<unistd.h>//unix standard
int brk(void *end_data_segment);
```
```
返回值：
    成功 返回 0
    失败 返回 -1
参数：
    直接来指定 新的堆尾指针，队尾指针前面的内存就是分配的内存
    >当前堆尾指针，表示分配虚拟内存
    <当前堆尾指针，表示释放虚拟内存
    =当前堆尾指针，空操作
注意：
    新堆尾指针 = 原堆尾指针 + 堆内存增量(可正可负)
分析：
    利用brk函数从 堆区 分配和释放内存的步骤
    void *p=sbrk(0);
    brk(p+4);
    brk(p);    //释放4字节内存
在分配和释放内存过程中，p没有发生变化
```
### 3.3 brk函数
    brk函数-虚拟内存的分配和释放
    该函数是以 绝对 的方式分配和释放内存
    brk代码
```C
#include<stdio.h>
#include<string.h>
#include<unistd.h>
int main(void){
    void*p1 = sbrk(0);
    int *p2 = p1;
    brk(p2 + 1);
    *p2 = 520;
    printf("%d\n",*p2);
    double*p3 = (double *)(p2 + 1);
    brk(p3 + 1);
    *p3 = 13.14;
    printf("%lg\n",*p3);
    brk(p2);
    return 0;
}
```
```C
#include <sys/mman.h>
//分配内存，并建立虚拟内存和物理内存映射关系
void *mmap(void *addr,size t length,int prot,int flags,
        int fd,off t offset);
```
    参数：
    addr：要建立映射关系的虚拟内存起始地址
    一般给NULL，操作系统在当前进程的3GB虚拟内存中的预留空间
    找一块空闲的虚拟内存来做映射
    length：要映射的虚拟内存区域的大小
    自动按页(4K)对齐映射
    10字节 - 4K - 4096
    4098字节 - 8K
    prot：对于映射区域的访问权限
    PROT_EXEC：  对于映射区可执行
    PROT_READ：  对于映射区可读
    PROT_WRITE： 对于映射区可写
    PROT_NONE：  对于映射区不可访问
    flags：映射标志，使用以下两个组合即刻：
    MAP_ANONYMOUS | MAP_PRIVATE：仅仅建立虚拟内存和物理内存的映射关系
    MAP_SHARED：建立虚拟内存和磁盘文件之间的映射关系
    fd：文件描述符
    offset：文件偏移量，自动按4KB对齐
    注意：如果建立虚拟内存和物理内存的映射，fd和offset参数都给0
    返回值：
    成功 放回映射的虚拟内存的起始地址
    失败 返回MAP_PAILED(-1)
    结果：
    一旦该函数调用成功，将来访问的虚拟地址就是对应的物理地址
    //释放内存，解除映射关系
```c
int munmap (void *addr,size t length);
```
参数：
addr：指定映射区的起始地址
length：指定映射区的长度
放回置：
成功 返回0
失败 返回1
注意：
p = 0x100;
int * p;p+1;  //0x104
char * p;p+1;  //0x101
double * p;p+1;  //0x108
short * p;p+1;  //0x102
### 3.4总结
    sbrk和brk函数都是在堆尾指针(malloc / free 也是在操作堆尾指针)
    使用sbrk 函数分配内存比较方便
    使用brk函数释放内存比较方便
    如果后续使用这两个函数从堆区分配内存，建议
    用sbrk 分配内存
    用brk释放内存
## 4分配内存
    1. 将一段 虚拟地址范围 标记为"占用"状态
    2. 将这段 虚拟内存和物理内存做映射，一次映射的最小单位是4KB
    每次映射至少4KB，如果用完了，继续4KB映射
    操作系统的功能：屏蔽硬件操作细节，让应用无需关注底层的硬件操作
## 5系统调用函数 mmap
mmap代码
```C
#include<stdio.h>
#include<sys/mman.h>
int main(void){
    //分配虚拟内存建立和物理内存的映射关系
    char*psz = mmap（NULL,//操作系统找一块空闲的虚拟内存做映射
                4096+4096,//映射区的大小为2页，8192字节
                PROT_READ | PROT_WRITE,//映射区访问权限可读可写
                MAP_PRIVATE | MAP_ANONYMOUS,//仅仅建立地址映射
                0,0);
    if(psz ==MAP_FAILED){
        perror("mmap");
        return -1;
        }
        //向缓冲区(内存)中写入字符串：sprintf
        //向映射区写入字符串
        sprintf（psz，"hello world");
        printf("%s\n",psz);
        if(munmap(psz,4096)==-1){
            perror("munmap");
            return 0;
        }
        //获取后面4096字节有效内存的首地址，保存到psz中
        psz += 4096;
        sprintf(psz,"hello,Saturday");
        printf("%s\n",psz);
        //释放剩余的4096字节，解除地址映射
        munmap(psz,4096) == 0-1){
            perror("munmap");
            return -1;
        }
        return 0;
}
```
    内存壁垒：
    0 ~ 3G-1  ： 用户空间
    3G ~ 4G-1：内核空间
    内核空间和用户空间不能够相互调用
    系统调用 - 互相访问
    Unix/Linux系统的大部分的功能都是通过系统调用来实现的
    Unix/Linux的系统调用被封装成c函数的形式，它们隶属于Linux/Unix系统，不属于标准c库函数
    这些系统调用函数也是位于库文件的：libgcc_s.so
    说明：
    man3+函数名
    man3所加函数，该函数属于c库函数
    man2+函数名
    man2所加函数，该函数属于系统调用函数
    系统调用函数层次关系：
    标准库函数大部分时间运行在用户态(用户空间)，但部分库函数偶尔会 调用系统调用，
    进入到内核态(内核空间)，
    程序员自己编写的代码可以跳过标准库，直接使用系统调用
    直接与操作系统内核交互，进入内核态
    程序：
    访问内核
    程序-库函数-系统调用-内核
    程序-系统调用-内核
    不访问内核
    程序-库函数
    系统调用在内核中实现，其外部接口定义在c库中，该接口的实现借助于软中断进入内核
    一个进程在运行中的时候，时而在用户空间，时而在内核空间，进程在这两种空间中所消耗的时候，
    分别称之为用户时间和系统时间
    通过time命令：测试进程所消耗的时间
    格式：time可执行程序的命令
    举例：time ls /  //查看ls /这个命令所消耗的时间
    real：总的执行时间
    user：用户时间
    sys  ：系统时间
# 三 文件系统
## 1 概念
    Linux理念：一切皆文件
    文件系统的分类：NTFS，FAT32，EXT2，EXT4，UTS，CRAMFDS，...
    不同的文件系统管理的方式不一样
    使用管理系统来管理文件，组织文件的流程
    硬盘：分区(windows)|分区|分区
    c盘        D盘 E盘
## 2文件系统的逻辑结构
    一个磁盘驱动器被分为多个分区
    拿出一个分区，解剖：
    分区：引导块|超级块|柱面组1|柱面组2|...|
### 概念
   1. 引导块：计算机通上电之后，自动运行存储在这里的代码，(BIOS,BOOTLOADER),加载和启动操作系统(操作系统自举)
   2. 超级块：记录文件系统的整体信息，例如：文件系统格式，分区大小，i节点和数据块的总量等
   3. 若干柱面组：就是一大块储存区域，将来文件的信息就是存于此处
      柱面组：超级块副本|柱面组信息| i节点映射表|块位图| i节点表|数据块集
      1. 超级块副本：就是将分区中的超级块拷贝了一份，将来通过超级块副本来检索文件可以提高效率
      2. 柱面组信息：对这个柱面组的整体描述
      3. i节点映射表：通过一个文件名称来寻找文件在软件中比较难实现，文件名就是一个字符串，字符串的长度有长有短，无形中浪费了内存，给i节点指定了一个编号(i节点：用来描述文件本身信息的，一个文件有对于的一个i节点，通过i节点来找到对应的文件)
         使用一个int类型的数据来表示这个文件对应的i节点的编号，长度是固定的，容易表示，节省内存
         每个文件对应的i节点编号简称为i节点号，通过该i节点号获取文件的信息
         命令：ls -i  //查看文件的i节点号
      4. 块位图：数据块，储存区域是由一个一个的数据块来组成，一个数据的大小为512字节/1KB
         也是一个大数组，这个数组中每个元素的每个bit位对应一个数据块，使用0/1表示该块处于空闲还是占用的状态
      5. i节点表：大数组，包含一堆i节点，每个i节点记录着文件的元数据和数据块索引表
         通过i节点号在i节点映射表中找到的就是i节点在i节点表的下标位置
         通过下标可以找到对应的i节点 - 找到文件
         i节点：元数据|数据块索引表
         元数据：描述文件的信息，文件类型，文件权限，文件的硬链接数，用户和组的信息
         三组
         用户       RW—
         组         R—
         其他人     R—
         数据块索引表：大数组，索引就是下标，就是将数据块的编号(下标)放在一起，把这些下标对应的数据块最终合并在一起组成一个完整的文件
         通过i节点的数据块索引表的数据块索引号找到对应的数据块
      6. 数据块集：数据块的集合
         数据块的大小512/1024/4096个字节，一个i节点最多包含13个数据块
         数据块分类
         直接块：储存文件的实际数据
         间接块：储存下级文件数据块索引表
### 文件访问流程:
文件名 - 目录 - i节点号 - i节点映射表 - i节点位置(下标) - i节点 - 数据块索引 - 数据块+数据块(文件内容)

### 文件类型：
普通文件
源代码文件；编译器，汇编器，链接器 - 汇编文件(.s)，目标文件(.o)，可执行文件
系统配置文件；shell脚本文件；音频/视频  数字内容的多媒体文件；数据库文件
文件的大小：最大值受限于Linux内核中用于管理文件的c语言代码数据类型的大小，某些文件系统还可能强加自己的限制，将其限定在更小的值
操作系统内核没有堆并发文件访问强加限制，不同的进程可以同时读写一个文件，并发访问的结果取决于独立操作的顺序，通常不可预测
一个文件分为两部分
1. 元数据    ——i节点
2. 内容数据 ——数据块
   目录文件
   目录本质是一个普通文件，存储文件名和i节点号的映射，每一个这样的映射，使用目录中的一个条目表示，叫做硬链接
   目录也是文件，目录文件的i节点号储存在它的父目录中
   每个目录的i节点号都是存储在其父目录中，而在根目录/是没有父目录的
   根目录的i节点号i节点表中的位置是固定的，即使没有父目录，根目录也能被正常检索
   每个目录中 . 和 ..
   . 映射该目录本身的i节点号 ..映射其父目录的i节点号
   符号链接文件
   看上去像普通文件，每个符号链接文件都有自己的i节点和包含被链接文件完整路径名的数据块
   命令：ln - s
   特殊文件
   特殊文件以文件形式表示的内核对象
   本地套接字：网络编程的基础
   字符设备：char  键盘，摄像头
   块设备：block  硬盘
   有名管道：是进程间通信的一种机制(IPC)
   通过ls -l查看文件类型
   —         普通文件
   d         目录文件
   s         本地套接字
   c         字符设备
   b         块设备
   l         符号链接
   p         有名管道
## 3文件的打开和关闭
open    -  打开文件
```C
#include <fcntl.h>
int open (const char *pathname,int flags,mode t mode);
参数：
    pathname：文件路径名
    flags：
        O_RDONLY    - 只读
        O_WRONLY    - 只写
        O_RDWR      - 可读可写
        O_CREAT     - 不存在就创建，已存在 打开
        O_EXCL      - 不存在就创建，已存在 报错
        O_TRUNC     - 不存在就创建，已存在 清空
        O_APPEND    - 追加
    mode：权限模式
        仅仅在创建新文件有效
        使用形如OXYZ的三位八进制表示
        X  拥有者用户权限
        Y  同组用户的权限
        Z  其他用户的权限
        读权限    4 表示
        写权限    2 表示
         执行权限  1 表示
    返回值：
        成功    返回未使用的，最小的文件描述符 - 使用文件描述符来表示该文件[0，∞(整数)]
        失败    返回-1
```
close    -  关闭文件
```C
#include <unistd.h>
int close(int fd);
参数：
    fd：open的返回值，关闭某个文件
```
代码:
```C
#include<stdio.h>
#include<fcntl.h>
#include<unistd.h>
int main(void){
    int fd1 = open("open.txt",O_RDWR | O_CREAT | O_TRUNC,0666);
    if(-1 == fd1){
        perror("open");
        return -1;
    }
    printf("fd1=%d\n",fd1);
    int fd2 = open("open.txt",O_RDONLY);
    if(-1 == fd2){
        perror("open");
        return -1;
    }
    printf("fd2=%d\n",fd2);
    close(fd2);
    close(fd1);
    return 0;
}
```
```
使用open函数打开某个文件的时候，会使用文件描述符来表示某个文件
fd  --文件
i节点  --文件
文件的内核结构：
V节点和V节点表：
进程打开某个文件的时候，将文件的节点读入内存，并且辅以其他的表要信息形成一个专门的数据结构，
使用数据结构来存储这些必要信息，包含1节点信息的数据结构称为V节点
所有的V节点会以链表的形式构成V节点表
文件表项：
V节点指针 + 文件状态标志(open函数flags参数) + 文件读写位置(最后一次读写的最后一个自己的下一个位置)
由上述三项组成的新的数据结构称为文件表项
优点：通过文件表项可以记录每次读写的位置，也可以通过V节点指针访问改文件的各种元数据和节点信息
open("a.txt",...)
特性：
1.多次打开同一个文件，无论是在同一个进程个进程还是在不同的进程中，都只会在系统内核中产生一个V节点
2.每次打开文件都会产生一个新的文件表项，每一个文件表项各自维护各自的文件状态标志和文件读写位置
可能因为打开的是同一个文件而共享同一个V节点
3.打开一个文件意味着内存资源(V节点，文件表项等)的分配，而关闭一个文件就是为了释放这些资源
但是如果要关闭的文件处于打开状态（其他进程也在使用），此时其V节点不会被释放，仅仅使用该进程独有的文件表项被释放的文件表项被释放，直到系统中打开该文件的进程都显式或者隐式的将其关闭，此时v节点才会被真正释放
4.一个处于打开状态的文件也可以被删除，但其所占用的磁盘空间直到其V节点彻底消失后才会被标记为自由
进程a:open("b.txt",...)
进程b:open("b.txt",...)
进程b关闭了文件，b.txt对应的v节点不会被释放，释放的仅仅是文件表项
文件描述符：
由文件的内核结构可知，一个被打开的文件在系统内核中通过文件表项和V节点加以表识
有关该文件的所以操作，都需要依赖于文件表项和V节点
需要将文件表项和V节点体现在完成这些后续操作的函数的参数中
内核空间的内存地址会暴露给运行与用户空间的程序代码
一旦某个用户进程出现操作失误，极有可能造成系统内核失稳，进而影响其他用户进程的运行，对操作系统的稳定性造成极大的威胁
解决内核对象在可访问性和安全性之间的矛盾，内核会维护一张存有各进程信息的列表，称为进程表
系统中的每个进程在进程表中都有一个表项，每个表项中包含了对于特定进程的描述信息，例如 进程id 线程id 组id...，其中也包含了一个被称为文件描述符表的数据结构
作为文件描述表项在文件描述符表的下标，称为文件描述符
合法的文件描述符一定是一个大于0的整数
文件描述符0 1 2 3都是处于使用状态
使用进程打开一个文件 - 分配文件描述符为4
每次一个新的文件描述符表项，系统总是从下标0开始在文件描述符表中寻找最小的未使用项
每关闭一个文件描述符，无论其被索引的文件表项和V节点是否被删除，与之对应的文件描述符表项一定会被标记为未使用，并且在后续操作中为新的文件描述符所占用
系统内核缺省(默认)为每个进程打开了三个文件描述符，它们在unistd.h头文件中被定义为三个宏
#define STDIN_FILENO        0//标准输入
int val = 0;
scanf("%d",&val);
STDIN_FILENO - 0 - 文件表项指针 - 文件表项 - v节点 - i节点 - 标准输入文件 - 键盘
#define STDOUT_FILENO       1//标准输出
printf("hello,world\n");
STDOUT_FILENO - 1 - 文件表项指针 - 文件表项 - v节点 - i节点 - 标准输出文件 - 显示器
#define STDERR_FILENO       2//标准错误输出
malloc(0xfffffffff); ->分配0xffffffffff字符 -> 无法分配 -> 报错
STDERR_FILENO - 2 - 件表项指针 - 文件表项 - v节点 - i节点 - 标准错误
输出文件 - 显示器
系统内核缺省(默认)为每个进程打开了三个文件描述符,它们在 unistd.h 头文件中被定义为了三个宏
#define STDIN FILENO 	0 //标准输入
#define STDOUT FILENO	1 //标准输出
#define STDERR FTLENO	2 //标准错误输出
打开a.txt文件,分配一个新的文件描述符表项,分配的下标为最小的未使用项，分配的文件描述符为3 - 目前的最小的未使用项
打开b.txt文件,分配一个新的文件描述符表项,分配的下标为最小的未使用项，分配的文件描述符为4 - 目前的最小的未使用项
关闭文件描述符0，打开i.txt，该文件对应的文件描述符为0
    1.关闭文件描述符0-文件描述符0处于空闲/未使用状态
    2.打开1.txt,分配最小的未使用的文件描述符-
```
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<fcntl.h>
void redir(void){
    close(STDIN_FILENO);//close(0)
    open("i.txt",O_RDINLY);//0 -> i.txt
    close(STDOUT_FILENO);//close(1)
    creat("o.txt",0644);//1 -> o.txt
    close(STDERR_FILENO);//close(2)
    creat("e.txt",0644);//2 -> e.txt
}
void doio(void){
    int x,y;
    //标准输入
    scanf("%d%d",&x,&y);
    //标准输出
    printf("%d+%d=%d\n",x,y,x+y);
    //标准错误输出
    malloc(0XFFFFFFF);
    perror("malloc");
}
int main(void){
    redir();
    doio();
    return 0;
}
```
    分析
    int creat (const char *pathname,mode t mode);
    open(pathname,O_WRONLY | O_CREAT | O_TRUNC,mode);
    creat("o.txt",0644)
    open("o.txt",O_WRONLY | O_CREAT | O_TRUNC,0644);
## 文件的读写
```c
#include<unistd.h>
ssize_t write(int fd,const void *buf,size_t count);
    功能：向指定文件写入数据
    参数：
        fd：文件描述符
        buf：内存缓冲区,要写入的数据
        count：期望写入的字节数
    返回值：
        成功    返回实际写入的字节数
        失败    返回-1
int fd=open("a.txt");
const char* text = "hello,world";
write(fd,text,100);
```
代码:
```c
//write.c
#include<stdio.h>
#include<string.h>
#include<unistd.h>
#include<fcntl.h>
int main(void){
    // == int fd = creat("write.txt",0644)
    int fd = open("write.txt",O_WRONLY | O_CREAT | O_TRUNC,0644);
    if(-1==fd){
        perror("open");
        return -1;
    }
    const char* text="helle,world";
    printf("要写入内容：%s\n",text);
    size_t towrite = strlen(text) * sizeof(text[0]);
    size_t written = write(fd,text,towrite);
    if(-1 == written){
        perror("write");
        return -1;
    }
    printf("期望写入%u个字节，实际写入%d个字节\n",towrite,written);
    write(fd,text,);
    close(fd);
    return 0;
}
```
    向xx.txt文件写入非字符串类型内容
    char name[128]="James";
    unsigned int age=35;
    double salary=2000000;
        方法：将非字符串类型内容 - 转换为字符串类型
    printf("%s %u %.2lf\n",name,age,salary);
        将这些非字符串类型内容输出到屏幕上
        - 前提：已经将这些内容转换为字符串
    将这些内容转化为字符串，然后输出到字符数组
    char buf[1024];
    sprintf(buf , "%s %u %.2lf\n",name,age,salary);
        s=string
代码:
```c
#include<stdio.h>
#include<string.h>
#include<unistd.h>
#include<fcntl.h>
int main(void){
    // == int fd = creat("write.txt",0644)
    int fd = open("write.txt",O_WRONLY | O_CREAT | O_TRUNC,0644);
    if(-1==fd){
        perror("open");
        return -1;
    }
    const char* text="helle,world";
    printf("要写入内容：%s\n",text);
    size_t towrite = strlen(text) * sizeof(text[0]);
    char name[128]="James";
    unsigned int age=30;
    double salary=200000;
    printf("%s%u%.2lf\n",name,age,salary);
    if(write(fd.buf,strlen(buf)*sizeof(buf[0]))==-1){
        perror("write");
        return -1;
    }
    size_t written = write(fd,text,towrite);
    if(-1 == written){
        perror("write");
        return -1;
    }
    printf("期望写入%u个字节，实际写入%d个字节\n",towrite,written);
    write(fd,text,);
    close(fd);
    return 0;
}
```
读取-read
    #include <unistd.h>
    ssize t read(int fd,void *buf,size t count);
    功能：从文件中读取内容
        参数：
            fd：文件描述符，表示从哪个文件中读取数据
            buf：存储读取数据的内存缓冲区首地址
            count:期望读取的字节数
        返回值：
            成功
                返回实际读取的字节数
                返回0，读取到了文件尾部
            失败返回-1
代码:
```c
//read.c
#include<stdio.h>
#include<string.h>
#include<unistd.h>
#include<fcntl.h>
int main(void){
    int fd = open("read.txt",O_RDONLY);
    if(-1 == fd){
        perror("open");
        return -1;
    }
    char text[256];
    size_t toread=sizeof(text)-sizeof(text[0]);
    ssize_t readed=read(fd,text,toread);
    printf("期望读取%u字节，实际读取%d字节\n",toread,readed);
    text[readed/sizeof(text[0])]='\0';
    printf("读取内容为%s\n",text)
    close(fd);
    return 0;
}
```
    writei和read都是基于系统调用的文件读写，是面向于二进制字节流的
    对二进制文件读写,无需做额外的工作
    对文本文件读写，需要按照特定的格式，将二进制形式的数据转换为文本字符串
代码:
```c
//binary.c
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
int main(void){
    int fd = open("binary.dat", O_WRONLY|O_CREAT|O_TRUNC, 0644);
    if(-1 == fd){
        perror("open");
        return -1;
    }
    char name[128] = "James";
    if(write(fd, name, sizeof(name)) == -1){
        perror("write");
        return -1;
    }
    unsigned int age = 30;
    if(write(fd, &age, sizeof(age)) == -1){
        perror("write");
        return -1;
    }
    double salary = 200000;
    if(write(fd, &salary, sizeof(salary)) == -1){
        perror("write");
        return -1;
    }
    close(fd);
    if((fd = open("binary.dat",  O_RDONLY)) == -1){
        perror("open");
        return -1;
    }
    if(read(fd, name, sizeof(name)) == -1){
        perror("read");
        return -1;
    }
    printf("name:%s\n", name);
    if(read(fd, &age, sizeof(age)) == -1){
        perror("read");
        return -1;
    }
    printf("age:%u\n", age);
    if(read(fd, &salary, sizeof(salary)) == -1){
        perror("read");
        return -1;
    }
    printf("salary:%.2lf\n", salary);
    close(fd);
    return 0;
}
```

## 顺序读写和随机读写

lseek - 调整文件读写位置

每个打开的文件都有一个与其相关的文件读写位置保存在文件表项中，用以记录从文件头开始计算的字节便宜
	文件读写位置往往是一个非负的整数，
	使用off_t类型表示
		32位系统，long int
		64位系统，long long int

每一次读写操作都是从当前的文件读写位置开始，且根据所读写的字节数，同步增加文件读写位置，为下一次读写做准备

打开一个文件的时候，设置O_APPEND标志，否则文件的读写位置一律被设为0，也就是文件首字节的位置

设置文件都读写位置

```c
#include <sys/types.h>
#include <unistd.h>
off_t lseek(int fd,off_t offset,int whence);
```

功能：认为调整文件读写位置
参数：
	fd：文件描述符
	offset：文件读写位置便宜字数
			0 返回当前读写位置
			正数 向后偏移字节数
			负数 向前便宜字节数
	whence:offset参数的扁移延点，可以取以下三个值
		SEEK_SET-从文件头开始
		SEEK_CUR-从当前位置开始,最后被读写位置的下一个字节
		SEEK_END-从文件尾开始
返回值：
	成功	返回-1
	失败	返回调整后的文件读写位置

int fd=open(“hello.txt”);

​	0	1	2	3	4	5	6	7	8	9	10
---------------------------------------

​	^

默认在0位置上，文件的起始位置

read(fd,buf,3);

​	0	1	2	3	4	5	6	7	8	9	10

---------------------------------------

​				   ^
​					此时读写位置变了3个位置

read(fd,buf,1);

​	0	1	2	3	4	5	6	7	8	9	10

---------------------------------------

​				   	 ^
​						此时读写位置变了3个位置

lseek(fd,-4,SEEK_CUR);//文件读写位置从当前位置开始向左(文件头部)偏移4字节

​	0	1	2	3	4	5	6	7	8	9	10

---------------------------------------

​	^

lseek(fd,5,SEEK_SET);//从文件开始向右移动5个字节

​	0	1	2	3	4	5	6	7	8	9	10

---------------------------------------

​				   	  	^

lseek(fd,8,SEEK_CUR);

​	0	1	2	3	4	5	6	7	8	9	10

---------------------------------------

​				   	  							  				 ^
​				可以通过lseek函数将文件读写位置设置到文件尾之后，在超过文件尾的位置上写入数据，将在文件中形成空洞，位于文件中但没有被写过的字节都被设置为0，文件空洞不会占用磁盘空间，但是会被计算在文件大小之内

write(fd,”789”,3);

​	0	1	2	3	4	5	6	7	8	9	10	\0	\0	7	8	9	

---------------------------------------

​				   	  											   			   ^

lseed(fd,-7,SEEK_END);

​	0	1	2	3	4	5	6	7	8	9	10	\0	\0	7	8	9	

---------------------------------------

​				   	  						^
​												 从文件末尾向前移动7个字节，到了9这个位置上

代码:
seek.c

```c
#include<stdio.h>
#include<string.h>
#include<unistd.h>
#include<fcntl.h>
int main(void){
    int fd = open("seek.txt",O_RDWR|O_CREAT|O_TRUNC,0644);
    if(-1 == fd){
        perror("open");
        return -1;
    }
    const char* text = "hello,world";
    if(write(fd,text,strlen(text)*sizeof(text[0]))==-1){
        perror("write");
        return -1;
    }
    if(lseek(fd,-6,SEEK_CUR)==-1){
        perror("lseek");
        return -1;
    }
    off_t pos = lseek(fd,0,SEEK_CUR);
    if(-1 == pos){
        perror("lseek");
        return -1;
    }
    printf("当前读写位置%d\n",pos);
    text = "Linux";
    if(write(fd,text,strlen(text)*sizeof(text[0]))==-1){
        perror("write");
        return -1;
    }
    if(lseek(fd,8,SEEK_END)==-1){
        perror("lseek");
        return -1;
    }
    text="这里有一圈洞洞"
        if(write(fd,text,strlen(text)*sizeof(text[0]))==-1){
        perror("write");
        return -1;
    }
    off_t size = lseek(fd,0,SEEK_END);
    if(-1 == size){
        perror("lseek");
        return -1;
    }
    printf("文件大小:%ld字节\n", size);
    close(fd);
    return 0;
}
```

h	e	l	l	o	,	w	o	r	l	d
													   ^

h	e	l	l	o	,	w	o	r	l	d
							  ^

h	e	l	l	o	,	L	i	n	u	x
							  					^

off_t pos = lseek(fd, 0,SEEK_END);
	pos 意思 文件大小

文件的读写位置不能位于文件头之前
—lseek(fd,-8,SEEK_SET);—

系统I/O和标准I/O
系统调用提供的文件I/O函数
	open/close read /write/lseek ..
标准C语言库提供了文件I/O函数：
	fopen/fclose/fread/fwrite/...

当系统调用函数被执行的时候，需要在用户态和内核态之间来回切换，频繁执行影响程序的运行性能
标准库函数做了必要的优化，内核会维护一个缓冲区，只有在满足特定条件的时候才将缓冲区和系统内核同步
	减少进程在用户态和内核态之间来回切换的次数，提高运行性能

代码:
sysio.c

```c
#include<stdio.h>
#include<unistd.h>
#incluse<fcntl.h>
int main(void){
    int fd = open("sysio.dat",O_WRONLY|O_CREAT|O_TRUNC,0644);
    if(-1 == fd){
       perror("open");
           return -1;
    }
    unsigned int i;
    for(i=0;i<1000000,i++){
        write(fd,&i,sizeof(i));
    }
    close(fd);
    re
}
```

