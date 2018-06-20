#  Java内存结构
## Java内存分为5个虚拟区域

![avatar](https://raw.githubusercontent.com/raytz/raytz.github.io/master/_data/20141021141849_243.jpg)

### 堆的概念
* 大白话说就是new操作符申请的内存
* 堆内存线程共享
* 堆内存耗尽时，JVM抛出OOM异常
* 堆内存可以通过 -Xms -Xmx调整

#### 堆内存
* Eden - 负责保存新对象或生命周期很短的，YoungGC主要是清理该区域
* Survivor - YoungGC清理后，幸存下来的就在Survivor区
* Old - YoungGC清理了好多好多次，依然能存活的对象，对象就会被转移到Old区。Old区的回收是依赖major GC进行


#### 方法区
* PermGen - 永久保留区，也叫持久代。保存类定义、结构、字段、方法以及常量。
> 注：PermGen在Java8已经被彻底删除了，取代他的另一个内存区域叫MetaSpace。

* CodeCache - 主要保存编译后生成的字节码，包括Class和Meta的信息。
> 注：运行常量池也是保存在该区域，静态。

#### 栈空间
* 每个线程独享栈内存。
* 主要存储局部变量、当前线程上下文、操作指令

#### 本地栈
* 全称应该是Native Method Stacks
* 从Java调用Native方法时，使用NativeStack

![avatar](https://raw.githubusercontent.com/raytz/raytz.github.io/master/_data/03231458_sjaE.jpg)

#### PC寄存器
* 线程启动的时候会一个PC寄存器。
* PC寄存器里面保存当前正在执行的JVM指令地址，如果是Native方法，这里是Undefined。
* 在当前命令执行前、执行中，PC寄存器保存的是当前指令地址。
* 在当前命令执行完，PC寄存器会保存下一个执行执行的地址。


# 一个Integer的内存占用
## Java对象的内存布局
* 类加载检查
JVM遇到一条new指令时，首先检查这个指令的参数是否能在常量池中定位到一个类的符号引用，并且检查这个符号引用代表的类是否已被加载、解析和初始化过。如果没有，那必须先执行相应的类的加载过程ClassLoader。

* 对象头（Header）
> 在32位系统上占用8bytes，在64位系统上占用16bytes
> 包括了mark word和klass pointer
> markWord在32位系统上占用了4bytes，64位系统占用了8bytes，包括了哈希码、GC分代年龄、锁状态标志、线程持有锁、偏向线程ID、偏向时间戳
> 
> klass pointer
> 类元数据指针，可以理解成类的Description
> 
![avatar](https://raw.githubusercontent.com/raytz/raytz.github.io/master/_data/20151217151455512.jpeg)

  
* 实例数据（Instance Data）
> 原始类型 Primitive type 内存占用如下:

Primitive Type | Memory Required(bytes)
---- | ----
boolean | 1
byte | 1
short | 2
char | 2
int | 4
float | 4
long | 8
double | 8

> 引用类型 Reference
> 
> 32位系统上每个占用4bytes
> 64位系统上每个占用8bytes

* 对齐填充（Padding）
>  HotSpot的对齐方式为8个字节对齐
> 
##### 一个Object占用的内存大小
* new Object() : Header 16 
* class A { int a; } : Header 16 + int 4 + padding 4 = 24
* class A { Integer a; } : Header 16 + Reference 8 = 24
* new Integer[1] : Header 24 + Refrence 8 = 32


## Jvm启动的时候内存占用
1. Java程序的堆内存，最大就是 -Xmx设置的这个值
2. Garbage Collection在垃圾回收的时候使用的内存
3. JIT optimization使用的内存
4. Java程序的Off-heap所使用的内存
5. Java程序的Metaspace所使用的内存
6. JNI Code所占用的内存
7. Jvm启动的时候所占用的内存。


## 参考链接
https://stackoverflow.com/questions/26357186/what-is-in-java-object-header





