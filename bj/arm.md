# 开发板

    电脑：开发主机，称为上位机
    开发板：运行主机，成为下位机
    ->核心三大件
        CPU ：分析CPU型号，方便后续寻找CPU的芯片手册
        内存：物理基地址 和大小
                将来软件可以直接访问内存
                基地址：物理内存的起始地址(0x40000000)大小：1GB
                    0x40000000 ~ 0x40000000 + 1GB
                有效物理地址空间范围：
                    0x40000000 ~ 0x7fffffff
                    1GB = 1024 * 1024 * 1024 = 0x40000000
                向内存地址为0x48000000写入4字节数据0x100;
                    (unsigned long *)0x48000000 ->0x48000000存储的是地址
                                                ->该地址存储了unsigned long类型数据
                    *(unsigned long *)0x48000000 ->获取地址上的数据
                    *(unsigned long *)0x48000000 ->0x100;
                从内存地址为0x48000000读取1字节数据，存储到变量data中
                    char data = *(unsigned char *)0x48000000;
                地址指针的方式访问内存
        闪存：
            常用的三类闪存
            1.norflash
                访问的形式和内存一样
                软件以地址指针的方式访问
            2.nandflash
                访问必须通过nand控制器
                软件不可以以地址指针的方式访问
            3.emmc(常用于手机)
                访问必须通过emmc控制器
                软件不可以以地址指针的方式访问
            X6818开发板闪存的类型为emmc 容量大小为8GB
              举例:
                int val = 100;
                0x100 101 102 104 ->4字节来储存val变量
        程序存储在闪存中，运行在内中
            内存：数据掉电丢失
            闪存：数据掉电不丢失
    ->外围设备
        根据用户的需求来决定需要分析哪个接口
        网卡：用于将上位机上的可执行程序下载到下位机上
        串口：实现下位机和上位机的通
            UART串口的传输速度很慢
        举例：
            uart串口的传输速度为115200bps(bit per second)
        假设要传输100MB文件
            1Byte = 8bit
            100 * 1024 * 1024 * 8 / 115200 = 7281s 约等于2小时
    原理图和芯片手册
        1.底板原理图分析：X6818vb2.pdf
            外设内部连接情况
        2.核心板原理图分析：x4418cv3_release20150713
            外设和CPU的连接情况
        3.CPU芯片手册分析：SEC_S5P6818X_Users_Manual_preliminary_Ver_0.00.pdf
            CPU的使用说明情况
    嵌入式处理器分类：
        arm处理器
        PowerPC处理器
        EPGA：Xilinx
        DSP：TI，达芬奇系列
        MIPS：北京君正
        单片机：51 430 stm32
    嵌入式处理器内部组成：
    CPU核
        功能：数据运算，访问外设(从外设读取数据/向外设写入数据)
        数据流：数据来自外设 -> CPU运算 -> 回归到外设
    控制器
        功能：CPU核不允许直接访问外设，要想访问外设需要通过
            对应的控制器来间接访问
    CPU核访问控制器内部的寄存器
        寄存器：各个硬件控制器内部都包含了一堆寄存器，每个寄存器都有一个唯一的物理地址
        寄存器本质是一个硬件单元，和内存是一样的，用于暂存数据
            CPU的寄存器，每个寄存器为4字节大小
        和内存一样 -> 怎么访问内存，就怎么访问寄存器
    编程：
        1.CPU核 -> 寄存器(软件)
        2.寄存器 -> 控制器(硬件)
        3.控制器 -> 外设(硬件)
    VCC3P3_SYS：3.3V电源
    3.3V/5V = 高电平(数字1)
    0V = 接地 = 低电平(数字0)
    引脚 = 管脚 = 外设和CPU连接点的名字
    复用功能：具备多种功能，但是同一时刻只能使用一个
    GPIO:General Purpose Input/Output 普通输入/输出功能
    作为输出或者输入都是相对CPU而言的
        输出：CPU输出高电平/低电平
            引脚电平由CPU控制为输出
        输入:外设输入高电平/低电平
            引脚电平由外设控制为输入
    alternate:复用的
    function:功能
    register:寄存器
    specify:指定
    点亮led灯
        1.三大件
            led灯 在开发板的位置
        2.底板原理图：分析外设的内部连接状况
            D26灯常亮 -> 电源指示灯
            D22：一头接3.3V，一头接GPIO_B26硬件连接线
                如果GPIO_B26为高电平，D22灯 灭
                如果GPIO_B26为低电平，D22灯 亮
            硬件连接线连接到CPU上
        3.核心板原理图：分析外设和CPU的连接情况
            3.3V - D22 - GPIO_B26 - SPI_WP - AC25 - CPU
            SD10/GPIOB26/TSIDATAO[2]
            选择：GPIOB26 (三个功能选一个)
                选择为输出(两个功能选一个)
                输入高低电平(控制led灯亮灭)
            CPU芯片手册：
            GPIO共分为5组：A/B/C/D/E
                GPIO引脚共160 -> 每组32个引脚 GPIOX[31,0]
                GPIO_B26 B组的第27个引脚
                1.GPIO -> GPIOX复用功能选择寄存器
                    GPIOBALTFN1     0XC001B024(地址,32bit)
                        [21:20]
                    芯片手册：搜索AC25
                    GPIOB26为复用功能1
                2.输出 -> GPIO输出使能寄存器
                    GPIOBOUTENB     0XC001B004(地址,32bit)
                    B组引脚：       B31  ... B0
                    GPIOBOUTENB:   31 30 ... 0
                        [26]        0,GPIOB26输入
                                    1,GPIOB26输出
                3.高低电平 -> GPIOX输出寄存器
                    GPIOBOU
                    T        0XC001B000(地址,32bit)
                        [26]        0,GPIOB26输出低电平
                                    1,GPIOB26输出高电平3.编辑程序
        此时所编辑的是裸板程序
        裸板程序：不使用任何的标准c库提供的函数
        编程框架：
            void ABC(void){
                ABC_init();
                //led_init();
                //uart_init();
                //i2c_init();
                //lcd_init();
                while(1){
                    //根据用户需求完成业务逻辑
                    led_on();
                    delay();
                    led_off();
                    delay();
                }
            }
            ABC：就是当前程序的入口函数，切记：裸板程序的入口函数名称不一定叫main函数
            ABC_init：初始化函数
                裸板程序上来先做各种外设的硬件初始化的工作
            根据用户需求完成业务逻辑：
                裸板程序最终必然进入到死循环
        GPIOBOUT        0XC001B000(地址,32bit)
            以地址指针的方式表示该寄存器的数据
                `#define GPIOBOUT (*(unsigned long *)0XC001B000)`
                `#define GPIOBOUTENB (*(unsigned long *)0XC001B004)`
                `#define GPIOBALTFN1 (*(unsigned long *)0XC001B024)`
        分析：
            1.想要修改寄存器中的数据
                前提 - 获取寄存器中的数据
            2.如何访问内存 - 如何访问寄存器
                以地址指针的方式访问内存 - 以地址指针的方式访问寄存器
                `#define GPIOBOUT (*(unsigned long *)0XC001B000)`
                `#define GPIOBOUTENB (*(unsigned long *)0XC001B004)`
                `#define GPIOBALTFN1 (*(unsigned long *)0XC001B024)`
                1.GPIO -> GPIOX复用功能选择寄存器
                    GPIOBALTFN1     0XC001B024(地址,32bit)
                           [21:20] = 01
                    芯片手册：搜索AC25
                    GPIOB26为复用功能1
                    GPIOBALTFN1 &= ~(1<<21);//[21]=0
                    GPIOBALTFN1 |=(1<<20);//[21=1]
                2.输出 -> GPIO输出使能寄存器
                    GPIOBOUTENB     0XC001B004(地址,32bit)
                    B组引脚：       B31  ... B0
                    GPIOBOUTENB:   31 30 ... 0
                        [26]        0,GPIOB26输入
                                    1,GPIOB26输出
                    GPIOBOUTENB |=(1<<26);
                3.高低电平 -> GPIOX输出寄存器
                    GPIOBOUT        0XC001B000(地址,32bit)
                        [26]        0,GPIOB26输出低电平     亮
                                    GPIOBOUT &= ~(1<<26);
                                    1,GPIOB26输出高电平     灭
                                    GPIOBOUT |=(1<<26);
    知识点: & |
        按位与 &
            An  Bn 结果 (An 数据A的第n位)
            1   1   1
            1   0   0
            0   1   0
            0   0   0
            两个数据进行按位与运算，两个bit都为1，结果为1；否则结果为0
        总结：
            1 & 1 = 1
            0 & 1 = 0
            任何数据和1做按位与，结果保持不变
            1 & 0 = 0
            0 & 0 = 0
                任何数据和0做按位与，结果一定为0
        按位或 |
            An  Bn 结果 (An 数据A的第n位)
            1   1   1
            1   0   1
            0   1   1
            0   0   0
            两个数据进行按位或运算，只要有一个bit为1，结果就为1；否则结果为0
        总结：
            1 | 1 = 1
            0 | 1 = 1
                任何数据和1做按位或，结果为1
            1 | 0 = 1
            0 | 0 = 0
                任何数据和0做按位或，结果保持不变
        给bit位清0和置1操作
            假设int类型变量a,a[5] = 0,其他bit保持不变
                1111 1111 1101 1111     a
                ————————————————————    &
                xxxx xxxx xx0x xxxx     a[5]=0
                    a &= 0xffffffdf;
                1111 1111 1101 1111     0xffffffdf
                ————————————————————    ~
                0000 0000 0010 0000     0x20
                    a &= ~0x20;
                0000 0000 0010 0000     0x20
                等价于
                0000 0000 0010 0000     1<<5
                    a &= ~(1<<5);
    结论：
    按位与 &
        a[n] = 0;
            a &= ~(1<<n);
    按位或 |
        a[n] = 1;
            a |= ~(1<<n);
    
    GPIOCOUT[12] = 0;
    GPIOCOUT &= ~(1<<12);

代码:
    //led.h

```c
#ifdef _LED_H
#define _LED_H
//寄存器的宏定义
#define GPIOBOUT (*(unsigned long *)0XC001B000)
#define GPIOBOUTENB (*(unsigned long *)0XC001B004)
#define GPIOBALTFN1 (*(unsigned long *)0XC001B024)
//声明操作函数
extern void led_init(void);//初始化函数
extern void led_on(void);//开灯
extern void led_off(void);//关灯
extern void delay(int n);//延时函数声明
#endif 
```

    分析：
        初始化函数
        1.将AC25引脚配置为GPIO功能
        2.将AC25引脚配种为输出模式
        配置为GPIO输出模式
            GPIOBALTFN1[21:20] = 01;
                -> GPIO模式
            GPIOBOUTENB[26] = 1;
                ->输出模式

代码:
    //led.c

```c
#include"led.h"
//作为整个程序的入口函数
void led_test(void){
    //硬件的初始化
    led_init();
    while(1)[
        led_on();
        delay(0x1000000);
        led_off();
        delay(0x1000000);
    ]
}
void led_init(void){
    //1.GPIO功能
    GPIOBALTFN1 &= ~(1<<>21);//[21]=0
    GPIOBANTFN1 |= (1<<20);//[20]=1
    //2.输出模式
    GPIOOUTENB |= (1<<26);//[26]=1
    //3.输出高电平 - 灭
    GPIOBOUT |= (1<<26);
}
void led_on(void){
    GPIOBOUT &= ~(1<<26);//[26]=0
}
void led_off(void){
    GPIOBOUT |= ~(1<<26);//[26]=1
}
//delay(10000);
void delay(int n){
    int i=n;
    for(; i != 0;i--);
    //while(i--); -> while(0);
}
```

```
4.编译程序
    交叉编译：在一个平台生成另一个平台的可执行程序
        x86 -> arm运行
    步骤：
    1.安装交叉编译器
        将交叉编译器拷贝到虚拟机中
        //向上位机Linux系统添加交叉编译命令的环境变量
        sudo vim /etc/environment
        将交叉编译器文件的bin目录添加到PATH环境变量中
            PATH是由一个一个的路径构成，路径之间使用分号隔开
        保存退出
        重启上位机
        重启后验证：
            arm-cortex_a9-linux-gnueabi-acc -v(可以arm+tab键)
    2.交叉编译程序
        1.arm-cortex_a9-linux-gnueabi-gcc -nostdlib -c -o led.o led.c
        2.arm-cortex_a9-linux-gnueabi-ld -nostartfiles -nostdlib -Ttext=0x48000000 -eled_test -o led.elf led.o
        3.arm-cortex_a9-linux-gnueabi-objcopy -O binary led.elf led.bin
        分析：
            1.arm-cortex_a9-linux-gnueabi-gcc -nostdlib -c -o led.o led.c
                arm-...-gcc：c语言交叉编译器
                -nostdlib：no standard library - 编译的时候不使用标准c库的内容
                -c：只编译不链接
                -o led.o led.c：由led.c得到led.o，二进制内容
            2.arm-cortex_a9-linux-gnueabi-ld -nostartfiles -nostdlib -Ttext=0x48000000 -eled_test -o led.elf led.
                arm-...-le：链接器
                -nostartfiles：链接的时候，不要链接开始相关代码
                -nostdlib：链接的时候，不链接标准库的内容
                -Ttext=0x48000000：将来运行在开发板的内存地址为0x48000000
                                   将来程序要下载到下位机内存为0x48000000地址上，并且从0x48000000地址上运行
                -eled_text：告诉链接器，裸板程序的入口函数为led_test
                -o led.elf：最初生成一个ELF格式的可执行二进制文件
                                该elf格式的二进制文件只能运行在Linux操作系统
                        构成：ELF信息|纯二进制信息
                            Linux系统：识别ELF信息 - 剥离ELF信息 - 执行纯二进制信息
                            裸板程序：无法识别ELF信息并剥离，无法执行该程序
            3.arm-cortex_a9-linux-gnueabi-objcopy -O binary led.elf led.bin
                arm-...-objcopy：二进制文件拷贝处理命令
                -O binary：只保留二进制的内容
                led.elf：带elf信息的二进制可执行文件
                led.bin：纯正的二进制文件
5.测试运行
    D25灯 - 3.3V -- D25 -- GPIOC12 --w15 --CPU -- SA12/GPIOC12/SPITXD2/SDnRST2
        GPIOC12 为高电平 灭
                为低电平 亮
        将w15引脚配置为：
            GPIO功能
                复用功能选择寄存器
                GPIOCALTFN0     0XC001C020
                搜索：w15   GPIOC12 - alternate function 1
                    选择复用功能1
                    GPIOCALTFN0[25:24]=01
            输出模式
                GPIO输出使能寄存器
                GPIOCOUENB      0XC001C004
                    [12]        1输出
            输出高底电平
                GPIO输出寄存器
                GPIOCOUT        0XC001C000
                    [12]        0,low level
                    [12]        1,high level
```





# 设置蜂鸣器的鸣叫

    3.3V电源 - 蜂鸣器 - 三极管(Q1) - GND
    Q1 / Q2 / Q3 / ...
        Q三极管，下标数字代表三极管的序号
    D1 / D2 / D3 / ...
        D二极管，下标数字代表二极管的序号
    三极管的应用：
        电流放大
        无触点开关
            原理：基极电流控制集电极电流导通和截止
       材料：
        硅管和锗管
       分类：
        NPN PNP
        工作原理相同：使用两个PN节将半导体分为三部分
        NPN：
                    c集电极
                      |
                      |
                     /
            B基极————
                     \
                      |
                      V
                      |
                    E发射极
         PNP：
                     c集电极
                      |
                      |
                      /
            B基极————
                    ^
                      \
                      |
                      |
                    E发射极
        使用最多的：
            硅管 - NPN
            锗管 - PNP
    基极电流 - 流过来 - 三极管接通
    基极电流 - 没过来 - 三极管截止
                3.3V
                 |
                 LS(蜂鸣器)
                 |
                 V
                 |
        PWM2 ——> Q1
                 |
                 V
                 |
                GND
    PWM2连接到了CPU - 核心板原理图
    PWM2 - AD12 - SA14/GPIOC14/PWM2/VICLK2
    选择：GPIOC14 功能
        配置为输出
                       3.3V
                        |
                        LS(蜂鸣器)
                        |
                        V
                        |
    CPU - AD12 - PWM2 - Q1
                        |
                       V
                       |
                       GND
    输出高电平，输出电流到Q1 - 接通 - 蜂鸣器鸣叫
    输出低电平，没有电流到Q1 - 截止 - 蜂鸣器不叫
    配置给引脚 为GPIO功能
        GPIOCALTFN0     0XC001C020
            [29:28] = 01
        GPIOC14引脚为复用功能1
    配置该引脚 为输出模式
        GPIOCOUTENB     0X001C004
            [14] = 1 输出模式
    配置该引脚 输出高低电平
        GPIOCOUT        0XC001C000
            [14] = 0 输出低电平 - 截止 - 蜂鸣器不叫
            [14] = 1 输出高电平 - 接通 - 蜂鸣器鸣叫
        - CPU芯片手册

# UART通信

    常见CPU和外设之间的通信方式
        GPIO接口：LED灯 蜂鸣器 按键等
        UART串口接口：BT蓝牙 GPS(定位) GPRS(打电话 发短信)
        I2C接口：触摸屏 重力传感器
        SPI接口：NORFLASH SD卡等
        1 - Wire(一线式)接口：DS18B20温度传感器 EEPROM存储器
    UART串口 定义：
        九个字：通用串行异步收发器
        通用：UART串口应用非常广泛
        串行：说明CPU和外设通信只需要一根信号线，该信号线一定是数据线
            用于传输数据
                数据传输时一个bit位一个bit位传输
            UART数据传输从低位开始
                CPU通过UART给BT发送数据0X95(10010101)
                    数据线上的电平序列(波形图)为：
                        1 - 0 - 1 - 0 - 1 - 0 - 0 - 1
                        高——底——高——底——高——底——底——高
                CPU通过UART给BT发送数据0x76(01110110)
                    数据线上的电平序列(波形图)为：
                        0 - 1 - 1 - 0 - 1 - 1 - 1 - 0
                        底——高——高——底——高——高——高——底
                CPU通过UART给BT发送数据0x58(01011000)
                    数据线上的电平序列(波形图)为：
                        0 - 0 - 0 - 1 - 1 - 0 - 1 - 0
                        底——底——底——高——高——底——高——底
            明确：信号线分类
                    数据线：此信号线只能传输数据
                        如果要传递的数据为1，将数据线拉成高电平
                        如果要传递的数据为0，将数据线拉成低电平
                    地址线：该信号线只能传输地址
                    控制信号线：该信号先用于实现数据双方同步数据，例如：时钟控制信号线
        并行：多根信号线(数据线)
            CPU和外设之间连接了多根信号线(8/16/32)
                CPU和外设一次性传输1/2/4字节
        并行和串行的对比：
            传输速度：并行>串行
            传输距离：串行>并行
            抗干扰性：串行>并行
        异步：同步数据的一种方式
            明确：计算机中，CPU的数据出来速度要远远快于外设的数据处理速度
                如果保证双方的数据传输正确，需要考虑到数据同步
                数据同步：一方发送数据，要保证对方接收到数据之后才能发送下一个
            计算机中同步数据的方式有两种：
                异步：异步靠协议(CPU和外设达成协议，规范，标准)
                    UART为异步方式
                    UART必然会有对应的数据传输协议
                同步：同步依靠时钟控制信号线(12c接口)
        收发器：接收和发送的硬件单元
            CPU -> 外设：CPU为发送器；外设为接收器
            外设 -> CPU：外设为发送器；CPU为接收器
    UART数据传输协议
    空闲位：如果CPU和外设不进行数据传输，此时数据线持续传输空闲位
        位数为1位，为高电平
    起始位：如果CPU和外设要进行数据传输，首先发送起始位
        位数为1位，为低电平
    数据位：表示双方数据传输时的数据有效位数，形式：5/6/7/8
        常用8bit
    奇偶校验位：用于检测双方数据传输时是否发生了错误
        校验的方式有三种：奇校验(odd)偶校验(even)不校验(none)
        位数位1位，可以时高电平，可以是低电平
        如果采用的是不校验，双方无需传输校验位
        奇校验：
            数据位"1"的个数+校验位"1"的个数=奇数
        偶校验:
            数据位"1"的个数+校验位"1"的个数=偶数
        举例：CPU给BT发送数据0x95(10010101),数据位为8位，校验采用奇校验
        校验位：高电平，低电平
        CPU端：
            1.CPU首先将数据0x95发送到数据线上
            2.判断数据0x95中"1"的个数-4个-数据位"1"的个数-偶数
            3.数据位"1"的个数+校验位"1"的个数=奇数
                    4       +      0/1     =奇数
                    校验位发送：1-高电平(4+1=5 - 奇数)
            4.CPU段最终给BT发送校验位为1
        BT端：
            1.BT首先从数据线上接收数据0x95
            2.判断数据0x95中"1"的个数-4个-数据位"1"的个数-偶数
            3.采用奇校验，判断校验位中应该是高电平(1)
            4.读取校验位的值，判断数据传输是否发生了错误
    停止位：如果CPU和外设数据传输结束，最后发送停止位即可
        位数1位/2位为高电平
    波特率：CPU和外设数据传输的速率
        常用的两个波特率为 9600bps和 115200bps
            bps = bit per second
    RTS/CTS:RTS和CTS分别对应两根信号线类似于时钟控制信号线CLK
        如果CPU和外设连接了这两根信号线
        UART会以同步的方式来同步数据
    使用UART传输多个字节
        如果CPU和外设传输多个字节，一次性也只能传输1个字节
        具体传输规则如下：
            数据a 数据b 数据c ...
            空闲-起始-数据a-(校验)-停止-起始-数据b-(校验)-停止-...-空闲位
    CPU和外设的配置必须一致
    UART的三种工作方式：
        单工：数据传输用于一个方向传输
        半双工：数据传输可以双向，但同一时刻只能朝一个方向
        全双工：数据传输可以同时双向传输
            一般UART采用全双工方式，所以UART数据传输时，需要两根数据线：
                TX:transmit,发送数据线，永远用于发送数据
                RX:receive,接收数据线，永远用于接收数据
                GND:CPU和外设之间需要一根地线

```
1.需求
  	下位机X6818通过UART0串口循环给上位机发送一个字符串,
    	上位机通过串口工具来捕获下位机发送的字符串信息 

2.确认下位机硬件信息 
  			确认UART0的位置 
  			USB转串口线 :
   		   串口(9针) : 连接到UART0位置上
    		  USB口 : 连接到PC机上   
  	1.串口座形式
   		 优点 : 结实 稳定 可靠 
    		缺点 : 占用空间比较大 
 	 2.USB转串口 
  		  优点 : 占用空间比较小 
 		   缺点 : 不牢靠 
  	3.插针式 
		    只有三根插针, TX/RX/GND 
			    优点 : 省空间 
  			  缺点 : 不牢靠, 关键是无法区分RX/TX/GND的线序(除非标注)
      			 如果插反了, 很容易烧毁 
细看 : 
  1.底板原理图 
    串口座有九根插针, 实质上只有三根插针是使用的
    确认UART0的连接位置
    确认上位机和下位机通过UART0实际的硬件连接线的连接方式 : 
    上位机的RX->串口线->UART0串口座的PC_TXD1->SP3232E芯片的T2OUT引脚->
      SP3232E芯片的T2IN->S5P6818芯片的UARTTXD0,作为数据发送引脚 
    上位机的TX->串口线->UART0串口座的PC_RXD1->SP3232E芯片的R2IN引脚 ->
      SP3232E芯片的R2OUT引脚->S5P6818芯片的UARTRXD0,作为数据接收引脚 
    分析 : 核心板原理图, 分析CPU提供的功能

  2.核心板原理图 
    UARTRXD0 - AE19 - GPIOD14/UARTRXD0/ISO7816 
    UARTTXD0 - AD19 - GPIOD18/UARTTXD0/ISO7816/SDWP2
    对于UART,应该选择为 : UARTTXD0 和 UARTRXD0 
    问 : 使用什么寄存器来配置为UARTTXD0 UARTRXD0 
    答 : 使用 复用功能选择寄存器来配置 
      GPIODALTFN0 GPIODALTFN1 

    芯片手册 :
      搜索 : AE19 复用功能1 UARTTXD0 
        AE19引脚配置为复用功能1 
      问 : 配置谁为复用功能1呢 ?
      答 : GPIOD14 配置为复用功能1 
      GPIODALTFN0   0XC001D020 
        [29:28] = 01 配置为复用功能1 -> 配置为了UARTRXD0 
  2.1.SP3232E芯片功能 
    电平转换线芯片, 电平转换, 将TTL电平转换为EIA电平,将EIA电平转换为TTL电平 
    TTL电平 : 开发板上电压/PC机, CPU和芯片所需要的电压 
      0-1.4V  对应数字0 
      1.8-3.3V 对应数字1
    EIA电平 : 串口线上的电压 
      3-15V  对应数字0 
      -3~-15V 对应数字1 
  	pc发送数据0给CPU, 到串口线上数据0(3V),没有电平转换, 直接将3V给CPU,
    CPU接收到后发现是3V, 认为是高电平, 为数据1 

    如果pc发送数据0给CPU, 到串口线上数据0(15V),没有电平转换, CPU直接烧了

  转换过程 : 
  开发板上TTL电压-SP3232E(升压)-串口线EIA电平-SP3232E-PC机主板上的TTL电平(降压)
  PC机主板的TTL电压-SP3232E-串口线上EIA电平-SP3232E-开发板上的TTL电平 

  3.芯片手册 
  3.1.S5P6818共支持6个串口 
    目前使用的是UART0 
  3.2.每个UART控制器内部包含了两个64字节容量的FIFO缓冲区 
    一个用于暂存接收到的数据
    一个用于暂存要发送的数据 
  3.3.每个UART控制器内部包含 
   	一个发送器
	   一个64字节的FIF0发送缓冲区
	   一个发送移位器
	   一个接收器
       一个64字节的FIFo接收缓冲区
	   一个接收移位器
	   一个波特率产生器
	   一个控制单元
  3.4.发送器
		1.CPU核以地址指针的方式将要发送的数据放到发送缓冲区
		2.UART控制器硬件在硬件上自动将发送缓冲区中的数据拷贝到发送移位器中
		3.发送移位器根据给定的波特率将数据一位一位的放到TX发送数据线上
  3.5.接收器
		1.接收移位器根据给定的波特率从X接收数据线一位一位的将数据接收到
		2.UART控制器硬件上将接收移位器接收到的数据拷贝到接收缓冲区中
		3.CPU核最终以地址指针的方式从接收缓冲区中奖数据读走
  3.6.注意
		接收缓冲区和发送缓冲区，处于FIFO模式，缓冲区的大小最多64字节
		目前NON-FIFO模式，缓冲区大小为1字节
  3.7.波特率配置公式
		UBRDIVn和UFRACVALn两个数据决定了波特率
		B UBRDIVn
		F =UFRACVALn
		S=SCLK UART
		bps=波特率
		DIV VAL B F/16					公式1
		DIV VAL (S/(bps * 16))-1	  公式2
		B+F/16=(S/(bps * 16))-1	   公式3
  3.8.寄存器分析
		1.UART寄存器
				ULCONO0		0XC00A1000
					[1:0]=11,配置数据位为8位
					[2]=0,配置停止位为1位
					[5:3]=000,配置不校验
					[6]=0,配置为普通模式
				UCON0		0XC00A1004
					[1:0]CPU核以轮训方式读取数据
						明确：计算机中，CPU核的数据处理速度（指针）要远远快于外设（接收移位器以115200的速度读取数据)
									如果此时外设还没准备好数据，CPU可以采用三种方式
											1.轮训方式(po1ling)：CPU核什么也不错，就是原地空转死等，直到外设准备好了数据
											2.中断方式(interrupt):CPU核先去做其他事情，等到外设准备好书记，再来读取数据
											3.DMA(direct memory access):基于硬件，速度最快，只能读取数据;中断基于软件，读取数据，还能处理异常
					[3:2]=01 - CPU核以轮训方式读取数据
							采用NoN-FIFo模式，如果发送缓冲区中目前有数据，不能再向其中放入数据，只能等到发送缓冲区为空的时候才能放数据
					[4]=0，普通模式
					[5]=0，普通模式
						loop-back mode:回环模式（自发自收，应用于调试阶段）
UTRSTAT0		0XC00A1010
	[0]=0：缓冲区为空
	   =1：缓冲区有数据了
		while(!(UTRSTAT0 & 0X01));
			[0]=0,按位与结果为0，!取反，结果为真，陷入到死循环
				接收缓冲区为空，陷入到死循环
			[0]=1,按位与结果非0，!取反，结果为假，跳出循环
				接收缓冲区非空，跳出循环，读取数据
	[1]=0,发送缓冲区有数据，
       		死等，直到发送缓冲区中没有数据
	   =1,发送缓冲区为空
			向发送缓冲区中写入数据
		while(!(UTRSTAT0 & 0X02));
UTXH0:发送缓冲区寄存器
地址：0XC00A1020
UTXH0=要发送的数据
将字符'h'发送到PC机
	//将'h'字符写入到发送缓冲区，后续操作无需关注，硬件自动完成
	UTXHO ='h';
UTXH0:接收缓冲寄存器
地址：0XC00A1024
URXH0[7:0]:保存接收到的数据
	unsigned char data =URXH0;
UBRDIV0:波特率配置寄存器
地址：0XC00A1028
UBRDIVO=根据公式计算
UFRACVAL0：波特率配置寄存器
地址：0XC00A102C
UFRACVALO=根据公式计算
```

2.GPIO寄存器

​	AD19 - UARTTXD0
​		GPIODALTFN1
​		[5:4]=01 UARTTXD0功能
​		选择复用功能1，UARTTXD0

​	AE19 - UARTTXD0
​		GPIODALTFN0
​		[29:28]=01 UARTRXD0功能
​		选择复用功能1，UARTTXD0

​	复用功能配置 使用GPIO复用功能选择寄存器

3.时钟寄存器

​	UART：控制器适宜频率50MHz

UART使用的时钟源PLL[0]/PLL[1]，为800MHz，被UBOOT指定了

UARTCLKENB 0XC00A9000
[2]=0,禁止时钟
   =1,使能时钟

UARTCLKGENOL OXCO0A9004
[4:2]时钟源选择
	000p11[0]
	001p11[1]
		->ok uboot初始化为了800MHz
	要SCLK UART=50MHz
	分频系数n=800/50=16

分频系数计算
	公式：分频系数n=CLKDIV0+1
			      =[12:5]+1

代码：
vim uart.c //定义
void uart_init(void){
	//1.关闭uart时钟
	//2.配置复用功能：UARTTXD0 UARTRXDO
	//3.配置数据线功能：ULCON0
	//4.配置读写方式（轮训）UCoN0
	//5.配置波特率为
	//5.1.配置时钟为50MHz
	//5.2.配置UBRDIV0 UFRACVAL0
	//n.打开uart时钟
}

代码：
uart.h

```c
#ifndef  _UART_H
#define  _UART_H
//寄存器声明 
//uart
#define     ULCON0       (*(unsigned long *)0XC00A1000)
#define     UCON0        (*(unsigned long *)0XC00A1004)
#define     UTRSTAT0     (*(unsigned long *)0XC00A1010)
#define     UTXH0        (*(unsigned long *)0XC00A1020)
#define     URXH0        (*(unsigned long *)0XC00A1024)
#define     UBRDIV0      (*(unsigned long *)0XC00A1028)
#define     UFRACVAL0    (*(unsigned long *)0XC00A102C)
//gpio
#define     GPIODALTFN0  (*(unsigned long *)0XC001D020)
#define     GPIODALTFN1  (*(unsigned long *)0XC001D024)
//时钟
#define     UARTCLKENB   (*(unsigned long *)0XC00A9000)
#define     UARTCLKGEN0L (*(unsigned long *)0XC00A9004)
//函数声明
extern void uart_init(void);
extern void uart_putc(char c);
extern void uart_puts(char* str);
#endif
```

uart.c

```c
#include"uart.h"
void uart_init(void){
    //关闭uart时钟
    UARTCLKENB &= ~(1<<2);
    //配置复用功能
    GPIODALTFN1 &= ~(3<<4);
    GPIODALTFN1 |= (1<<4);
    GPIODALTFN0 &= ~(3<<28);
    GPIODALTFN0 |= (1<<28);
    //配置ULCON0
    ULCON0=3;
    //配置UCON0
    UCON0=5;
    //配置波特率
    //配置SCLK_UART 50MHz
    UARTCLKGEN0L &= ~(0x7<<2);
    UARTCLKGEN0L &= ~(0xff<<5);
    //配置UBRDIV0
    UBRDIV0=26;
    UFRACVAL0=2;
    //打开uart时钟
    UARTCLKENB |= (1<<2);
}
void uart_putc(char c){
    whil(!(UTRSTAT0 & 0X02))
    //将要发送的字符放到发送缓冲区寄存器中
    UTXH0=0;
    //追加回车字符
    if('\n'==c)
        uart_putc('\r');
}
//发送字符串函数定义
void uart_puts(char* str){
    while(*str){
        uart_putc(*str);
        str++;
    }
}
```

```c
#include "uart.h"
void main(void){
    uart_init();
    while(1){
        uart_puts("hello, everyone\n");
    }
}
```

