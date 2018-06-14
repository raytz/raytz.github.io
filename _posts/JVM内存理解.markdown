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
* PermGen - 永久保留区，保存类定义、结构、字段、方法以及常量。
* CodeCache - 主要保存编译后生成的字节码，包括Class和Meta的信息。

#### 栈空间
* 每个线程独享栈内存。
* 主要存储局部变量、方法返回指针、入参指针。

#### 本地栈
* 全称应该是Native Method Stacks
* 保存Navtive方法




