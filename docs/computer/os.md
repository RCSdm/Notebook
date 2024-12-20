# 操作系统

## 计算机系统概述

​操作系统（Operating System，OS）是指控制和管理整个计算机系统的硬件和软件资源，并合理地组织调度计算机的工作和资源的分配；以提供给用户和其他软件方便的接口和环境；它是计算机系统中最基本的系统软件。

### 操作系统的特征
最基本的特征，互为存在条件：并发，共享；

（1）并行：指两个或多个事件可以在同一个时刻发生，多核CPU可以实现并行，一个cpu同一时刻只有一个程序在运行；

（2）并发：指两个或多个事件可以在同一个时间间隔发生，用户看起来是每个程序都在运行，实际上是每个程序都交替执行。

（3）共享性：操作系统的中资源可供多个并发的程序共同使用，这种形式称之为资源共享。

互斥共享：当资源被程序占用时，其它想使用的程序只能等待。

同时访问：某种资源并发的被多个程序访问。

虚拟和异步特性前提是具有并发性。

（4）虚拟性：表现为把一个物理实体转变为若干个逻辑实体。

时分复用技术：资源在时间上进行复用，不同程序并发使用，多道程序分时使用计算机的硬件资源，提高资源的利用率。

空分复用技术：用来实现虚拟磁盘（物理磁盘虚拟为逻辑磁盘，电脑上的C盘、D盘等）、虚拟内存（在逻辑上扩大程序的存储容量）等，提高资源的利用率，提高编程效率。

（5）异步性：在多道程序环境下，允许多个进程并发执行，但由于资源等因素的限制，使进程的执行以“停停走走”的方式运行，而且每个进程执行的情况（运行、暂停、速度、完成）也是未知的。

![alt text](<pic/Screenshot 2024-12-01 at 16.52.00.png>)

BIOS 程序（Basic Input/Output System）

BIOS 是固化在主板上的基本输入输出系统，是计算机启动第一个运行的软件，存放在ROM中。它会进行硬件初始化和自检，然后查找引导程序并执行。

引导程序（Boot）

引导程序是存储在主存ROM中的一段小程序，它的作用是将操作系统的内核文件从硬盘中读取到内存中，并跳转到内核入口点开始执行。

主引导记录(MBR)

MBR是硬盘的主引导记录，位于硬盘的第一个扇区。它包含了磁盘引导程序和分区表。该引导程序会找到活动分区并读取其分区引导记录，完成硬盘的引导。

分区引导记录(PBR)

PBR是分区引导记录，位于每个分区的第一个扇区。PBR中包含了一个引导程序，可以寻找并激活分区根目录下的启动管理器，完成分区的引导过程。


## 进程与线程
**进程的概念:**

进程是进程实体的运行过程，是系统进行资源分配和调度的一个独立单位。

进程实现操作系统的并发性和共享性。

程序：是静态的，就是个存放在磁盘里的可执行文件，如：QQ.exe。

进程：是动态的，是程序的一次执行过程，或者是一个正在运行的程序，如：可同时启动多次QQ程序。

进程实体：即进程映像，是静态的，可理解为进程的一次时刻的状态。

作业：用户向计算机提交的一项任务，是静态的，它通常是一个批处理程序或一个后台程序。

### 进程实体的组成
PCB是进程存在的唯一标志，当进程被创建时，操作系统为其创建PCB，当进程结束时，会回收其PCB。

    动态性：进程是程序的一次执行过程，是动态地产生、变化和消亡的；动态性是进程最基本的特征。
    并发性：内存中有多个进程实体，各进程可并发执行
    独立性：进程是能独立运行、独立获得资源、独立接受调度的基本单位
    异步性：各进程按各自独立的、不可预知的速度向前推进，异步性会导致并发程序执行结果的不确定性。
    结构性：每个进程都会配置一个PCB。结构上看，进程由程序段、数据段、PCB组成

### 进程的状态与转换

    就绪态一>运行态：进程被调度
    运行态一>就绪态：时间片到 or CPU被其他进程抢占
    运行态一>阻塞态：等待系统资源分配or等待某事件发生（主动行为）
    阻塞态一>就绪态：资源分配到位，等待的事件发生（被动行为）
    创建态一>就绪态：系统完成创建进程相关的工作
    运行态一>终止态：进程运行结束 or 运行过程中遇到不可修复的错误

    就绪状态：其它资源（进程控制块、内存、栈空间、堆空间等）都准备好、只差CPU的状态。
    执行状态：进程获得CPU，其程序正在执行。
    阻塞状态：进程因某种原因放弃CPU的状态，阻塞进程以队列的形式放置。
    创建状态：创建进程时拥有PCB但其它资源尚未就绪。
    终止状态：进程结束由系统清理或者归还PCB的状态。

### 线程和多线程模型

线程可理解为轻量级进程，它是一个基本的CPU执行单元，也是程序执行流的最小单位。

线程由线程ID、程序计数器、寄存器集合和堆栈组成。

引入进程的目的是更好地使多道程序并发执行，提高资源利用率和系统吞吐量；

而引入线程的目的则是减小程序在并发执行时所付出的时空开销，提高操作系统的并发性能。

引入线程后，进程只作为除CPU外的系统资源的分配单位，线程则作为处理机的分配单元

线程的三种状态：（1）执行（2）就绪（3）阻塞

线程控制块TCB：将所有用于控制和管理线程的信息记录其中

多线程OS中的进程属性：

（1）进程是一个可拥有资源的基本单位

（2）多个线程可以并发执行

（3）进程已不是可执行的实体，在多线程OS中，是把线程作为独立运行的基本单位

## 处理机调度与死锁
进程调度方式

非剥夺调度方式

又称非抢占方式。即，只允许进程主动放弃处理机。在运行过程中即便有更紧迫的任务到达，当前进程依然会继续使用处理机，直到该进程终止或主动要求进入阻塞态。

实现简单，系统开销小但是无法及时处理紧急任务，适合于早期的批处理系统

剥夺调度方式

又称抢占方式。当一个进程正在处理机上执行时，如果有一个更重要或更紧迫的进程需要使用处理机，则立即暂停在执行的进程，将处理机分配给更重要紧迫的那个进程。

可以优先处理更紧急的进程，也可实现让各进程按时间片轮流执行的功能（通过时钟中断）。适合于分时操作系统、实时操作系统
### 调度算法
1.先来先服务（FCFS）

算法思想：主要从“公平”的角度考虑（类似于我们生活中排队买东西的例子）

算法规则：按照作业/进程到达的先后顺序进行服务

用于作业/进程调度：

用于作业调度时，考虑是哪作业先达后备队列；

用于进程调度时，考虑的是哪个进程先到达就绪队列

优缺点：

优点：公平、算法实现简单

缺点：排在长作业（进程）后面的短作业需要等待很长时间，带权周转时间很大，对短作业来说用户体验不好。即，FCFS算法对长作业有利，对作（Eg：排队。）

2.短作业优先（SJF）

算法思想：追求最少的平均等待时间，最少的平均周转时间、最少的平均平均带权周转时间

算法规则：最短的作业/进程优先得到服务（所谓“最短”，是指要求服务时间最短）

用于作业/进程调度

即可用于作业调度，也可用于进程调度。

用于进程调度时为"短进程优先"（SPF，Shortest Process First）

优缺点

优点：“最短的”平均等待时间、平均周转时间；

在所有进程都几乎同时到达时，采用SJF调度算法的平均等待时间、平均周转时间最少；

“抢占式的短作业/进程优先调度算法（最短剩余时间优先，SRNT算法）的平均等待时间、平均周转时间最少”

缺点：不公平。对短作业有利，对长作业不利。可能产生饥饿现象。另外，作业进程的运行时间是由用户提供的，并不一定真实，不一定能做到真正的短作业优先。

抢占式的算法；会导致饥饿

3.高响应比优先（HRRN）

算法思想：要综合考虑作业/进程的等待时间和要求服务的时间

算法规则：在每次调度时先计算各个作业/进程的响应比，选择响应比最高的作业/进程为其服务
$$
响应比=\frac{等待时间+要求服务时间}{要求服务时间}
$$
高响应比优先算法：非抢占式的调度算法，只有当前运行的进程主动放CPU（常/常成，主动阻塞），需行调度，调度时计算所有就绪进程的响应比，选响应比最高的进程上处理机。

用于作业/进程调度：即可用于作业调度，也可用于进程调度

优缺点

综合考虑了等待时间和运行时间（要求服务时间）等待时间相同时，要求服务时间短的优先（SJF的优点）；

要求服务时间相同时，等待时间长的优先（FCFS的优点）

对于长作业来说，随着等待时间越来越久，其响应比也会越来越大，从而避免了长作业饥饿的问题

非抢占式的算法；不会导致饥饿

4.时间片轮转调度算法（RR）

算法思想：公平地、轮流地为各个进程服务，让每个进程在一定时间间隔内都可以得到响应

算法规则：按照各进程到达就绪队列的顺序，轮流让各个进程执行一个时间片（如100ms）。若进程未在一个时间片内执行完，则剥夺处理机，将进程重新放到就绪队列队尾重新排队。

用于作业/进程调度：用于进程调度（只有作业放入内存建立了相应的进程后，才能被分配处理机时间片）

优缺点

优点：公平；响应快，适用于分时操作系统；

缺点：由于高频率的进程切换，因此有一定开销；不区分任务的紧急程度。

抢占式的算法；不会导致饥饿

5.优先级调度算法

算法思想：随着计算机的发展，特别是实时操作系统的出现，越来越多的应用场景需要根据任务的紧急程度来决定处理顺序

算法规则：每个作业/进程有各自的优先级，调度时选择优先级最高的作业/进程

用于作业/进程调度：既可用于作业调度，也可用于进程调度。甚至，还会用于在之后会学习的I/O调度中

优缺点

优点：用优先级区分紧急程度、重要程度，适用于实时操作系统。可灵活地调整对各种作业/进程的偏好程度

缺点：若源源不断地有高优先级进程到来，则可能导致饥饿

抢占式/非抢占式的算法；会导致饥饿

6.多级队列调度算法

系统中按进程类型设置多个队列，进程创建成功后插入某个队列


队列之间可采取固定优先级，或时间片划分

固定优先级：高优先级空时低优先级进程才能被调度

时间片划分：如三个队列分配时间50%、40%、10%

各队列可采用不同的调度策略，如

系统进程队列采用优先级调度、交互式队列采用RR、批处理队列采用FCFS

### 进程互斥
![alt text](<pic/Screenshot 2024-12-04 at 11.05.27.png>)
临界资源：一次仅允许一个进程使用的资源

类型：物理设备，如打印机等；可被进程共享的许多变量、数据等

临界区：访问临界资源的那段代码。

为了保证临界资源的正确使用，可把临界资源的访问过程分成4个部分：

    1）进入区。为了进入临界区使用临界资源，在进入区要检查可否进入临界区，若能进入临界区，则应设置正在访问临界区的标志，以阻止其他进程同时进入临界区。
    2）临界区。进程中访问临界资源的那段代码，又称临界段。
    3）退出区。将正在访问临界区的标志清除。
    4）剩余区。代码中的其余部分。

​ 互斥也称间接制约关系。当一个进程进入临界区使用临界资源，另一进程必须等待当占用临界资源的进程退出临界区后，另一进程才能访问此临界资源。

遵循原则：

* 空闲让进。临界区空闲时，可以允许一个请求进入临界区的进程立即进入临界区；
* 忙则等待。当已有进程进入临界区时，其他图进入临界区进必须等待
* 有限等待。对请求访问的进程，应保证能在有限时间内进入临界区（保证不会饥饿）
* 让权等待。当进程不能进入临界区时，应立即释放处理机，防止进程忙等待。

## 虚拟存储器
虚拟存储器的定义和特征

程序不需全部装入即可运行，运行时根据需要动态调入数据，若内存不够，还需换出一些数据。系统好像为用户提供了一个比实际内存容量大得多的存储器，称为虚拟存储器。

* 多次性：无需在作业运行时一次性全部装入内存，而是允许被分成多次调入内存。
* 对换性：无需在作业运行时一直常驻内存，而是允许在作业运行过程中，将作业换入、换出。
* 虚拟性：从逻辑上扩充了内存的容量，使用户看到的内存容量，远大于实际的容量。

虚拟内存技术的实现

虚拟内存的实现需要建立在离散分配的内存管理方式的基础上。

访问的信息不在内存时，由操作系统负责将所需信息从外存调入内存（请求调页功能）

内存空间不够时，将内存中暂时用不到的信息换出到外存（页面置换功能）

虚拟内存的实现方式：

    请求分页存储管理
    请求分段存储管理
    请求段页式存储管理

所需要的硬件支持

    一定容量的内存和外存。
    页表机制（或段表机制），作为主要的数据结构。
    中断机构，当用户程序要访问的部分尚未调入内存时，则产生中断。
    地址变换机构，逻辑地址到物理地址的变换。