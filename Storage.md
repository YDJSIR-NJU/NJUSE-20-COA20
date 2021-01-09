# Storage

> - Lecture07
> - Lecture09

存储器由一定数量的单元构成，每个单元可以被唯一标识，每个单元都有存储一个数值的能力。

地址：单元的唯一标识符（采用二进制）

地址空间：可唯一标识的单元总数

寻址能力：存储在每个单元中的信息的位数

大多数存储器是字节寻址的，而执行科学计算的计算机通常是 64 位寻址的。

## 引子

### 存储体系金字塔

![image-20210108205640069](C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108205640069.png)





## 硬件

> 下面的“不能随机存取”指的常规情况下。利用特殊手段可以实现逻辑上“随机存取”，但是性能受存储实现原理一般也不怎么样。

### 磁存储技术

> - Lecture09

#### HDD - 机械盘

性能实测（YDJSIR的4T 希捷酷狼盘，50MB的读写大小）

![image-20210108221105071](C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108221105071.png)

**随机存取效率低**

#### 磁带



**不能随机存取**

### 光存储技术

> - Lecture09

#### 光盘



**不能随机存取**

### 半导体存储技术

> - Lecture07
>
> 注意到这章节内讲到的内容不止包含冯诺依曼架构包含的"内存"！本章涉及到的存储技术同样可能用作外部存储，如Flash芯片也用在我们的U盘和固态硬盘中。这里总结的内容对Cache和内存只介绍其物理原理！

**这里涉及的存储器类型都可以随机存取。**

#### Memory Cell - 位元 - 基本单元

<img src="C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108210011903.png" alt="image-20210108210011903" style="zoom: 50%;" />

- 两个稳定/半稳定状态以代表0和1；
- 至少能写入一次去设置状态；
- 能够读取其状态

#### 分类

![image-20210108210450495](C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108210450495.png)

#### ROM

非容失性

###### ROM

只能写一次不能改（既是优点也是缺点）

写入需要特殊设备甚至通常只能在工厂进行，大批量生产成本低

适合于只读场景（系统程序、子例程库等）

###### PROM

只能写一次不能改（既是优点也是缺点）

能用电子方式去烧了，但需要特殊设备

成本仍然较低，可以大批量生产

###### EPROM

###### EEPROM

> 如上表所示，价格越来越贵，写入越发容易。

#### RAM

- 读取速度最快最容易
- 数据易丢失（必须维持供电）

###### 实机展示对比

![image-20210108212332414](C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108212332414.png)

可见SRAM还是比DRAM不知道高到哪里去了。

##### DRAM - Dynamic RAM - 用作内存

用电容充电存储数据，有电荷代表1，反之代表0。

它在本质上是一个模拟设备，需要用一个门槛值区分它存储的到底是0还是1。

<img src="C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108211232572.png" alt="image-20210108211232572" style="zoom: 67%;" />

###### 优点

- 比SRAM便宜；
- 比SRAM体积小，更容易大规模集成；

###### 缺点

- 由于电容会漏电，需要定期通电刷新，刷新期间无法读写；

  > 读取的时候也会消耗电荷，故读取后也需要重新存储。

- 比SRAM慢；

###### DRAM的刷新

- 集中式刷新

  停止所有读写操作，刷新每一行；

- 分散式刷新

  每个存储周期都刷新每一行（会增加每个存储周期的时间）

- 异步刷新（常见）

  每个`某时间间隔`刷新每一行（效率高）

具体方式请仔细读题。



##### SRAM - Static RAM - 用作Cache

用逻辑门电路存储数据，是数字设备。

（计基学过的R/S 锁存器、门控D锁存器还记得吗?）

<img src="C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108212439482.png" alt="image-20210108212439482" style="zoom:67%;" />

###### 优点

- 比DRAM快；
- 不需要刷新；

###### 缺点

- 难以大规模集成；
- 比SRAM贵；

#### Flash

> 是现在常用的USB和固态硬盘采用的技术

是EPROM和EEPROM在开销和性能上的平衡

- 擦除比EPROM快
- 密度能达到EPROM水平，比EEPROM高

Flash的速度可以很快很快，当然也可以比较慢。下面是YDJSIR的固态。

![image-20210108221409001](C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108221409001.png)

#### 从位元到主存

##### 寻址

![image-20210108214950629](C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108214950629.png)

为什么内存序列做成方的？大大减少选择线的数量（上图只需要一纵一横的坐标就可以定位了）

###### 地址解码器

<img src="C:\Users\YuDongjun\Desktop\NJU\2020-Fall\COA\NJUSE-COA20\Storage.assets\image-20210108215130335.png" alt="image-20210108215130335" style="zoom:33%;" />

每次只有一个输出

##### 芯片-引脚

##### 模块组织

###### 字拓展

###### 位拓展

###### 多个插槽拼起来做上面两种拓展

###### Main Memory
$Main\ memory = RAM + ROM$

$Main\ memory\ capacity = RAM\ capacity$

## 软件

此处主要指的是磁盘（可以是机械，可以是固态）的RAID。Cache和RAM的高级组织不在此处展开。

### RAID

> - Lecture11



### 纠错

> - Lecture10

