# 计算机组成

## CPU

CPU的功能和结构：

1. 指令控制。完成取指令、分析指令和执行指令的操作，即程序的顺序控制。
2. 操作控制。一条指令的功能往往是由若干操作信号的组合来实现的。CPU管理并产生由内存取出的每条指令的操作信号，把各种操作信号送往相应的部件，从而控制这些部件按指令的要求进行动作。
3. 时间控制。对各种操作加以时间上的控制。时间控制为每条指令按时间顺序提供应有的控制信号。
4. 数据加工。对数据进行算数和逻辑运算。
5. 中断处理。对计算机运行过程中出现的异常情况和特殊请求进行处理。

![alt text](<src/Screenshot 2024-11-13 at 16.34.40.png>)

### 数据通路
**执行部件间传输信息的路径。**

建立由控制信号控制，受时钟驱动。

数据通路描述了信息从什么地方开始，中间经过哪个寄存器或多路开关，最后传送到哪个寄存器。

数据通路中专门进行数据运算的部件称为执行部件或功能部件；数据通路由控制部件控制。

数据通路的功能是实现 CPU 内部的运算器与寄存器及寄存器之间的数据交换。

![alt text](<src/image copy.png>)

### 数据通路与总线结构

![alt text](<src/Screenshot 2024-11-13 at 17.07.10.png>)

### 总线结构与CPU指令周期
在指令周期中，包含了：取指周期，在取指周期后需要判断是否有间址周期，如果没有就进入到执行周期，在执行周期后又需要判断是否有中断程序，如果有就响应中断并保存断点生成中断服务程序入口；如果没有就进入下一个取指周期。

![alt text](<src/Screenshot 2024-11-25 at 18.53.45.png>)
![alt text](<src/Screenshot 2024-11-25 at 18.54.16.png>)

### CPU中的主要寄存器

**数据寄存器**（Data Register，DR）又称数据缓冲寄存器，其主要功能是作为CPU和主存、外设之间信息传输的中转站，用以弥补CPU和主存、外设之间操作速度上的差异。

数据寄存器用来暂时存放由主存储器读出的一条指令或一个数据字；反之，当向主存存入一条指令或一个数据字时，也将它们暂时存放在数据寄存器中。

数据寄存器的作用是 ：

（1）作为CPU和主存、外围设备之间信息传送的中转站；

（2）弥补CPU和主存、外围设备之间在操作速度上的差异；

（3）在单累加器结构的运算器中，数据寄存器还可兼作操作数寄存器。

**指令寄存器**（Instruction Register，IR）用来保存当前正在执行的一条指令。

当执行一条指令时，首先把该指令从主存读取到数据寄存器中，然后再传送至指令寄存器。

指令包括操作码和地址码两个字段，为了执行指令，必须对操作码进行测试，识别出所要求的操作，指令译码器（Instruction Decoder，ID）就是完成这项工作的。指令译码器对指令寄存器的操作码部分进行译码，以产生指令所要求操作的控制电位，并将其送到微操作控制线路上，在时序部件定时信号的作用下，产生具体的操作控制信号。

指令寄存器中操作码字段的输出就是指令译码器的输入。操作码一经译码，即可向操作控制器发出具体操作的特定信号。

**程序计数器**（Program Counter，PC）用来指出下一条指令在主存储器中的地址。

在程序执行之前，首先必须将程序的首地址，即程序第一条指令所在主存单元的地址送入PC，因此PC的内容即是从主存提取的第一条指令的地址。

当执行指令时，CPU能自动递增PC的内容，使其始终保存将要执行的下一条指令的主存地址，为取下一条指令做好准备。若为单字长指令，则(PC)+1àPC，若为双字长指令，则(PC)+2àPC，以此类推。

但是，当遇到转移指令时，下一条指令的地址将由转移指令的地址码字段来指定，而不是像通常的那样通过顺序递增PC的内容来取得。

因此，程序计数器的结构应当是具有寄存信息和计数两种功能的结构。

**地址寄存器**（Address Register，AR）用来保存CPU当前所访问的主存单元的地址。

由于在主存和CPU之间存在操作速度上的差异，所以必须使用地址寄存器来暂时保存主存的地址信息，直到主存的存取操作完成为止。

当CPU和主存进行信息交换，即CPU向主存存入数据/指令或者从主存读出数据/指令时，都要使用地址寄存器和数据寄存器。

如果我们把外围设备与主存单元进行统一编址，那么，当CPU和外围设备交换信息时，我们同样要使用地址寄存器和数据寄存器。

**累加寄存器**通常简称累加器（Accumulator，AC），是一个通用寄存器。

累加器的功能是：当运算器的算术逻辑单元ALU执行算术或逻辑运算时，为ALU提供一个工作区，可以为ALU暂时保存一个操作数或运算结果。

**程序状态字**（Program Status Word，PSW）用来表征当前运算的状态及程序的工作方式。

程序状态字寄存器用来保存由算术/逻辑指令运行或测试的结果所建立起来的各种条件码内容，如运算结果进/借位标志（C）、运算结果溢出标志（O）、运算结果为零标志（Z）、运算结果为负标志（N）、运算结果符号标志（S）等，这些标志位通常用1位触发器来保存。

除此之外，程序状态字寄存器还用来保存中断和系统工作状态等信息，以便CPU和系统及时了解机器运行状态和程序运行状态。

因此，程序状态字寄存器是一个保存各种状态条件标志的寄存器。

### 硬布线控制器设计

根据指令操作码、目前的机器周期、节拍信号、机器状态条件，即可确定现在这个节拍应该发出哪些”微命令“

![alt text](<src/image copy 6.png>)

硬布线控制器的特点：

1. 指令越多，设计和实现就越复杂（逻辑图很复杂），因此一般使用RISC。
2. 如果扩充一条新的指令，则控制器的设计就需要大改，因此扩充指令较为困难。
3. 由于使用存纯硬件实现控制，因此执行速度很快。

![alt text](<src/Screenshot 2024-11-28 at 15.35.37.png>)

###  微程序控制器的基本原理

微地址寄存器CMAR，微指令寄存器CMDR,控制存储器CM

微命令：控制器部件向执行部件发出的控制命令，是构成控制序列的最小单位，例如打开或者关闭控制门的电位信号。是各部件完成某个基本微操作的命令

微操作：执行部件接受微命令后所进行的操作，和微操作是一一对应的。 （实际上，微命令是微操作的控制信号，微操作是微命令的执行过程，微操作是执行部件中最基本的操作）

微指令：若干微命令的集合，存放在一个控制存储器中，而存放微指令的控制存储器的单元成为微地址。在同一CPU周期内，并行执行的一组微命令，存储在控制存储器上面，称为一条微指令。

微周期：从读取一条微指令，到执行执行完毕所需要的时间称为微周期。

控制存储器：主存储器，主要用来存放程序和数据，位于CPU的外部，使用的是RAM。而控制存储器，则主要用于存储微程序，位于CPU内部，采用的是ROM。

微程序：实现一条机器指令功能的微指令序列。

程序与微程序：程序由机器指令构成，编写好以后放到主存中运行，可以改写。而微程序由微指令构成，事先编写好在CM（控制存储器）中，一般是不可改写的。微程序的作用就是实现一条对应的机器指令。

微程序>微指令>微命令=微操作是微命令的执行过程。

采用“存储程序”的思想，CPU出厂前将所有指令的“微程序”存入“控制器存储器”中。

![alt text](<src/Screenshot 2024-11-28 at 16.39.59.png>)

### 微指令的设计及编码方式

微命令与微操作一一对应，一个微命令对应一根输出线

有的微命令可以并行执行，因此一条微指令可以包含多个微命令

相容性微命令：可以并行完成的微命令。

互斥性微命令：不允许并行完成的微命令。

![alt text](<src/Screenshot 2024-11-28 at 19.07.18.png>)

### 指令流水线

一条指令的执行过程可以分成多个阶段（或过程）。根据计算机的不同，具体的分法也不同。

取指：根据PC内容访问主存储器，取出一条指令送到IR中。

分析：对指令操作码进行译码，按照给定的寻址方式和地址字段中的内容形成操作数的有效地址EA，并从有效地址EA中取出操作数。

执行：根据操作码字段，完成指令规定的功能，即把运算结果写到通用寄存器或主存中。

指令流水线的概念：把指令执行过程划分为不同的阶段，占用不同的资源，就能使多条指令同时执行。

## 存储器
 寄存器：制作在CPU中，其中数直接在CPU内部参与运算

 高速缓存cache：也制作在CPU中，速度快于内存，容量小于内存

 内存：存放将要参与运行的程序和数据，可以直接和CPU交换信息

 辅助存储器：用来存放暂时未用到的程序和数据文件，CPU不能直接访问辅存，辅存只能与主存交换信息

存储容量：存储字数 x 存储字长（如 1M x 8位 ）。
MAR反映存储字数，MDR反映了存储字长。

存储速度：数据传输率 = 数据的宽度/存储周期

存取时间：存取时间 + 恢复时间 = 存取周期，计算机进行一次读写操作后需要一段恢复时间才能进行下一次的读写操作。

主存带宽：就是上面的数据传输率，表示每秒从主存进出信息的最大数量，单位为字/秒，字节/秒，位/秒。
### 随机存储器RAM

DRAM芯片：使用栅极电容来存储信息

SRAM芯片：使用双稳态触发器来存储信息


 由于静态RAM是用触发器工作原理存储信息，因此即使信息读出后，它任保持其原状态，不需要再生。

 但掉电后原存信息丢失，故它属于易失性半导体存储器

动态RAM刷新

刷新的过程实质上是先将原存信息读出，再由刷新放大器形成原信息并重新写入的再生过程

为什么需要刷新

    由于存储单元被访问是随机的，有可能某些存储单元长期得不到访问，不进行存储器的读/写操作，其存储单元内的原信息将会慢慢消失。
    所以必须采用定时刷新的方法，规定在一定时间内，对动态RAM全部基本单元电路必作一次刷新
    一般刷新周期为2ms
    刷新是一行一行的进行，必须在刷新周期内，用专门的刷新电路来完成对基本单元电路的逐行刷新

只读存储器的特点是只能读出而不能写入信息，通常在电脑主板的ROM里面固化
一个基本输入/输出系统，称为BIOS（基本输入输出系统）。其主要作用是完成对系统的加电自检、
系统中各功能模块的初始化、系统的基本输入/输出的驱动程序及引导操作系统。

由于DRAM存储容量较大，存储单元数目多，所需地址线也就比较多，为了简化硬件，采用地址线复用技术，行地址和列地址分成两次进行传送到译码器中。

### 存储芯片与CPU的连接

位扩展——增加存储字长

位扩展的关键就是将两个存储芯片当成一个存储芯片来用，让两个存储芯片同时工作，同时被选中，
同时做读操作，同时做写操作，要想保证同时，就是把两个芯片的片选CS，用相同的信号进行连接。

字扩展——增加存储字的数量

位扩展和字扩展 同时扩展

![alt text](<src/image copy 3.png>)

### 双端口RAM和多模块存储器

存取周期 = 存取时间 + 恢复时间

DRAM由于电容的特性，每次进行读操作后需要进行重写，也就是需要一定的恢复时间，导致DRAM的存取周期比较长，并且这个恢复时间往往还比存取时间长。

这两个问题分别对应接下来的内容：双端口RAM 和 多模块存储器。
![alt text](<src/image copy 2.png>)

高位交叉编址：每个存储体遍历完了之后再遍历下一个存储体。仅仅相当于扩容。

低位交叉编址：以横向方式遍历存储体，也就是每次都是遍历不同存储体的不同存储单元。这样，在读取其他存储体的存储单元时，之前读取过的存储单元可以利用这段时间进行恢复，达到一种并行的效果。

在模块数的选取上需要保证模块数 m >= T/r，这样才能保证存储体有足够的时间进行恢复。

### Cache

**空间局部性：** 在最近的未来要用到的信息，很有可能与正在使用的信息在存储空间上是临近的。（信息的存储一般都是顺序的）

**时间局部性：** 在最近的未来要用到的信息，很可能是现在正在使用的信息。（程序中很可能存在大量的循环结构，需要重复访问）

故Cache能够工作的理论依据：从上面两个局部性可以分析到，我们可以把CPU目前访问的地址周围的部分数据放到Cache中。

设 **tc**为访问一次Cache所需时间，**tm**为访问一次主存所需时间。

CPU能够直接在Cache中找到所需信息，称为命中。

**命中率 H：** CPU欲访问的信息已在Cache中的比率。

**缺失率（未命中率）M：** M = 1 - H

**CPU平均访问时间 t 为：** t = H tc + ( 1-H ) ( tc+tm )

将主存的存储空间进行分块，主存与Cache之间以块为单位进行数据交换。

这样主存地址就可分为两部分：块号 和 块内地址。

在操作系统中，通常将主存中的 “一个块” 也称为 “一个页/页面/页框” 。

Cache中的 “块” 也称为 “行” 。

Cache和主存之间仍然存在一些问题：

如何区分Cache和主存之间的数据块对应关系？ ——Cache和主存的映射方式

Cache很小，主存很大。如果Cache满了怎么办？ ——替换算法

CPU修改了Cache中的数据副本，如何确保主存中数据母本的一致性？ ——Cache写策略
### Cache和主存的映射方式
（1）全相联映射

任何一个主存块可以放在Cache的任意位置。

给每一个Cache块增加一个标记位，记录对应的主存块号。

还需要一个有效位，有效位为1时表示标记位有效，有效位为0时表示标记位无效。

优点：Cache存储空间利用充分，命中率高。

缺点：查找速度较慢

（2）直接映射

每个主存块只能放到特定的一个位置：Cache块号 = 主存块号 % Cache总块数。

于是对于Cache所保存的标记号可以不用保存主存中对应的整个地址，可以只保留主存块号m前面（m-n）个二进制数。

（3）组相联映射

将Cache块分为若干组，每个主存块可放到特定分组中的任意一个位置。

每个主存块对应的组号 = 主存块号 % 分组数

### 替换算法
1.随机算法（RAND）

若Cache已满，则随机选择一块替换。

2.先进先出算法（FIFO）

若Cache已满，则替换最先被调入Cache的块。

3.近期最少使用（LRU）

为每一个Cache块设置一个”计数器“，用于记录每个Cache块已经多久没被访问过了。当Cache满了之后替换”计数器“最大的。

计数规则：

命中时，所命中的行的计数器清零，比其低的计时器加1，其余不变（加一没有意义）。

未命中且还有空闲行时，新装入的行的计数器置0，其余非空闲行全加1。

未命中且没有空闲行时，计数值最大的行的信息块被淘汰，新装行的块的计数器置0，其余全加1。

4.最近不经常使用（LFU）

为每一个Cache块设置一个”计数器“，用于记录每个Cache块被访问过几次。当Cache满后替换“计数值”最小的。

新调入的块计数器=0，之后每被访问过一次计数器+1。

### Cache写策略
1.写命中

（1）写回法：

当CPU对Cache写命中时，只修改Cache的内容，而不立即写入主存，只有当此Cache块被替换时才写回主存。

需要增加一位脏位，用于标记该Cache块是否被修改了。

减少了访存的次数，但存在数据不一致的隐患。

（2）全写法：

当CPU对Cache块写命中时，必须把数据同时写入Cache和主存中，一般使用写缓冲（write buffer）。

访存次数增加，速度变慢，但能保证数据的一致性。

2.写不命中
（1）写分配法：

当CPU对Cache写不命中时，把主存中的块调入Cache中，在Cache中修改，通常搭配写回法使用。
也就是发生替换时才写回主存。

（2）非写分配法：

当CPU对Cache写不命中时，只写入主存，不调入Cache中。搭配全写法使用。

![alt text](<src/image copy 4.png>)

### 虚拟存储系统
有时候一个程序比较大，无法将它顺序地存放在主存中的各个块中，因此操作系统会将它分成若干个页面，页面的大小和块的大小相同，每个页面可以离散地放入不同的主存块中。

逻辑地址（虚地址）：程序员看到的地址。

物理地址（实地址）：实际在主存中的地址。

对于一条机器指令：000001  001000000011（操作码+地址码），其地址码所使用的就是 逻辑地址。

页表：记录了每个逻辑页面存放在哪个主存块中，页表的数据放在主存中。

假设此时执行一条取指令操作，该指令为 000001 001000000011，所以要取的数据的逻辑地址为 001000000011

![alt text](<src/image copy 5.png>)

**虚拟存储系统：** 辅存中的数据并不是一次性全部加载到主存中的，而是和 Cache——主存 类似，根据局部性原理加载一部分数据到主存中。

## 指令系统

### 指令格式
指令（又称机器指令）：是指计算机执行的某种操作的命令，是计算机运行的最小功能单位。

一台计算机的所有指令的集合构成该机的指令系统，也称为指令集。

注：一台计算机只能执行自己的指令系统，不能执行其他系统的指令。

按操作数个数分：

Ⅰ、零地址指令：不需要操作数，如空操作、停机、关中断等指令

Ⅱ、一地址指令：只需要单个操作数，如自增，自减，取反，求补，需要两个操作数，但其中一个隐含在某个寄存器中

Ⅲ、二地址指令：常用于两个操作数的算术运算、逻辑运算相关指令。

完成一条指令需要访存四次，分别为取值，读第一个操作数，读第二个操作数，写回第一个操作数。

Ⅳ、三地址指令：常用于两个操作数的计算，结果放在第三个地址中。

完成一条指令需要访存四次，分别为取值，读读一个操作数，读第二个操作数，写到第三个操作数。

※若指令长度不变，地址码数量越多，寻址能力就越差

按指令长度是机器指令的多少倍分：

Ⅰ、半长指令：是机器指令长度一半

Ⅱ、单字长指令：与机器指令长度一样

Ⅲ、双字长指令：是机器指令长度两倍


![alt text](<src/Screenshot 2024-11-27 at 11.43.26.png>)

### 寻址方式
Ⅰ、顺序寻址

PC+”1“，这里的1指指令字长，每次取值结束后PC会+1

Ⅱ、跳跃寻址

执行转移类指令导致的PC值改变

![alt text](<src/Screenshot 2024-11-27 at 16.18.32.png>)

**偏移寻址**

Ⅰ、基址寻址

将CPU中基址寄存器(BR)/通用寄存器的内容加上指令格式中的形式地址A，而形成操作数的有效地址，即EA=(BR)+A

采用通用寄存器作为基址寄存器 
的位数，根据通用寄存器的总数判断，程序运行前，CPU将BR的值修改为该程序的起始地址。

基址寄存器是面向操作系统的，其内容由操作系统或管理程序确定。用户无法修改，在程序执行过程中，基址寄存器的内容不变（作为基地址），形式地址可变（作为偏移量）。

当采用通用寄存器作为基址寄存器时，可由用户决定哪个寄存器作为基址寄存器，但其内容仍由操作系统确定。

优点：可扩大寻址范围（基址寄存器的位数大于形式地址A的位数）

Ⅱ、变址寻址

有效地址EA等于指令字中的形式地址A与变址寄存器IX的内容相加之和，即EA= (IX)+A，其中IX可为变址寄存器（专用），也可用通用寄存器作为变址寄存器 。

变址寄存器是面向用户的，在执行过程中，变址寄存器的内容可由用户改变（IX作为偏移量），形式地址A不变（作为基地址）。刚好与基址寻址相反。

在针对数组处理过程中，不断改变IX的值，便很容易形成数组中任一数据的地址，特别适合编制循环程序。

基址变址复合执行。EA=(IX)+(BR)+A。

Ⅲ、相对寻址

相对寻址：把程序计数器PC的内容加上指令格式中的形式地址A而形成操作数的有效地址，即EA=(PC)+A，其中A是相对于PC所指地址的位移量，可正可负，补码表示 。

优点：这段代码在程序内浮动时不用更改跳转指令的地址码

相对寻址广泛应用于转移指令

注意：对于JMP A转移指令，当从CPU中取出一字节时，会自动执行PC+1。若指令的地址为X，且占2B，在取出该指令后，会自定跳转到X+2+A。


*堆栈寻址*

操作数存放在堆栈中，隐含使用堆栈指针作为操作数地址。

硬堆栈是将寄存器作为栈，成本很高；软堆栈是将主存作为栈，成本低。
硬堆栈不访存，软堆栈访存一次

### 高级语言程序与机器级代码之间的对应

对操作数的操作地址只涉及三种：寄存器到寄存器，主存到寄存器，立即数到寄存器。

dword 32bit ；word 16bit ；byte 8bit

通用寄存器 eax ebx ecx edx 变址寄存器 esi edi 堆栈寄存器 ebp esp。

![alt text](<src/Screenshot 2024-11-27 at 19.37.03.png>)

## 总线

片内总线：芯片内部的总线，是CPU芯片内部寄存器与寄存器之间，寄存器与ALU之间的公共连接线

系统总线：计算机系统内部功能部件（CPU、主存、I/O接口）之间相互连接的总线，可分为三类，数据总线，地址总线，控制总线

通信总线：计算机系统之间或计算机系统与其它系统之间的信息传送的总线

![alt text](<src/Screenshot 2024-11-30 at 10.33.43.png>)

## I/O系统

I/O接口就是负责协调主机与外部设备之间的数据传输。

显存VRAM（就是显示存储器）

显存是为了提高刷新图像的信号，会提前把需要显示的数据放入显存中。如今的计算机很多都有独立显存，就这可以避免，显存占用主存的空间。

程序中断是指在计算机执行现行程序的过程中，出现某些急需处理的异常情况或特殊请求，CPU暂时中断现行程序，而转去执行这些异常情况或特殊请求进行处理。处理完毕后又自动返回到现行程序的断点处，继续执行原程序。

中断服务程序的任务：

①保护现场。保存通用寄存器和状态寄存器的内容。

②中断服务。主体部分。例如将需要打印的字符传送到打印机的缓冲存储器中。

③恢复现场。通过出栈或取值把之前保存的信息传送回寄存器中。

④中断返回。通过中断返回指令回到原程序断点处。

DMA（Direct Memory Access）控制器是一种在系统内部转移数据的独特外设，可以将其视为一种能够通过一组专用总线将内部和外部存储器与每个具有DMA能力的外设连接起来的控制器。它之所以属于外设，是因为它是在处理器的编程控制下来 执行传输的。

机器字长：计算机能直接处理的二进制数据的位数，机器字长一般等于内部寄存器的大小，它决定了计算机的运算精度。

指令字长：一个指令字中包含的二进制代码的位数。

存储字长：一个存储单元存储的二进制代码的长度。等于MDR的位数， 它们都必须是字节的整数倍。

数据字长：数据总线一次能传送信息的位数，它可以不等于MDR的位数。

指令字长一般取存储字长的整数倍，若指令字长等于存储字长的2倍，则需要2次访存来取出一条指令，因此取指周期为机器周期的2倍；若指令字长等于存储字长，则取指周期等于机器周期。

早期的计算机存储字长一般和机器的指令字长与数据字长相等，因此访问一次主存便可取出一条指令或一个数据。随着计算机的发展，指令字长可变，数据字长也可变，但它们必须都是字节的整数倍。

请注意64位操作系统是指特别为64位架构的计算机而设计的操作系统，它能够利用64位处理器的优势。
但64位机器既可以使用64位操作系统，又可以使用32位操作系统。而32位处理器是无法使用64位操作系统的。
