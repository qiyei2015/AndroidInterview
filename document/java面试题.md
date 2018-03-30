# java面试题汇总

熟练掌握java是很关键的，大公司不仅仅要求你会使用几个api，更多的是要你熟悉源码实现原理，甚至要你知道有哪些不足，怎么改进，还有一些java有关的一些算法，设计模式等等。

### 一、java基础面试知识点

* java中==和equals和hashCode的区别

    ==对于引用对象来说判断是不是同一个对象，即判断是否是指向堆中同一个对象。对于基本类型是判断值相等

    equals和hashCode是Object中的方法。equals用来判断两个对象是否相等(一般子类会复写该方法)，hashCode产生哈希码。

    ava要求重写equals必须复写hashCode方法(HashSet等集合需要)，两个对象相等，hashCode必定相等，hashCode不等的对象，肯定不相等

* int、char、long各占多少字节数

    4 2 8

* int与integer的区别

    Integer是int的包装类
    
* 探探对java多态的理解

    多态的定义：不同的对象接受同一消息而产生不同的行为

* String、StringBuffer、StringBuilder区别

    String 字符串 StringBuffer 和StringBuilder不产生无用的对象。StringBuilder为线程不安全，StringBuffer线程安全

* 什么是内部类？内部类的作用

    内部类：定义在一个类的内部的类。
    内部类可以大大弥补Java在多重继承上的不足。另外匿名内部类可以方便的实现闭包。
    静态内部类可以带来更好的代码聚合，提高代码可维护性
    
* 抽象类和接口区别

    抽象类中可以有私有的方法，变量。他具有子类的公共属性，接口往往用来约束行为
    
* 抽象类的意义

    一般做父类
    
* 抽象类与接口的应用场景

    略
    
* 抽象类是否可以没有方法和属性？

    可以
    
* 接口的意义

    行为约束
    
* 泛型中extends和super的区别

    extends指定 方向的上边界，super指定泛型的下边界

* 父类的静态方法能否被子类重写

    不能，编译过不了，提示找不到方法，静态方法属于类，不属于对象。对象可以多态，类不行
    
* 进程和线程的区别

    进程是一个独立的执行单元，线程是进程中调度的一个基本单元
    
* final，finally，finalize的区别

    final 修饰类，方法，变量，表示不可变 。finally是try catch中的关键字，表示最终会执行
    finalize是Object中的方法，垃圾回收器回收之前调用该方法。

* 序列化的方式

    序列化，表示将一个对象转换成可存储或可传输的状态。序列化后的对象可以在网络上进行传输，也可以存储到本地。
    
* Serializable 和Parcelable 的区别

    一个是java中的，一个是Android中的。Serializable代码量少，写起来方便,Parcelable用法较为复杂
    Serializable java用反射来序列化，Parcelable将复杂对象分解，效率更高
    
* 静态属性和静态方法是否可以被继承？是否可以被重写？以及原因？

    可以被继承，不能被重写。静态属于属于类，但是对象也可以访问
    
* 静态内部类的设计意图
    
    只是为了降低包的深度，方便类的使用，静态内部类适用于包含类当中，但又不依赖与外在的类

* string 转换成 integer的方式及原理
    参考 Integer.parseInt().

### 二、java深入源码级的面试题（有难度）

* 哪些情况下的对象会被垃圾回收机制处理掉？

    从root节点开始，无法访问的节点，不再被引用的对象
    
* JVM的内存回收机制
    Who：哪些是不再使用要被当做“垃圾”回收处理的对象？也就是要确定垃圾对象。
    根搜索算法
    分代回收算法
    Where：在哪里执行垃圾回收？明确要清理的内存区域。
    堆内存
    When：什么时候执行GC操作？即JVM触发GC的时机。
    根据算法
    How：怎么样进行垃圾对象处理？即GC的实现算法。
   https://blog.csdn.net/JKerving/article/details/50984952
* 讲一下常见编码方式？
    ASCII UTF-8 Big5 GB2312

* utf-8编码中的中文占几个字节:int型几个字节？

    3个字节 一个数字占一个字节

* 静态代理和动态代理的区别，什么场景使用？

    静态代理的代理类是事先创建的，静态代理往往代理的一个类，适合接口下实例或者方法较少的场景
    
    动态代理的代理类由程序运行期间由反射动态生成的，代理的是一个接口下的多个实例对象。Proxy.newProxyInstance创建

* Java的异常体系

    Throwable 两个子类Exception Error(jvm错误)
    
    Exception又分为运行时异常，非运行时异常

* 修改类A的equals方法的签名，那么使用HashMap存放这个对象实例的时候，会调用哪个equals方法？

    A

* Java中实现多态的机制是什么？

    类的继承

* 如何将一个Java对象序列化到文件里？

    ObjectOutputStream writeObject，可以将对象写入到输出流中，输出流关联文件

* 说说你对Java反射的理解

    可以从反射的用处，以及类的属性等机制

* 说说你对Java注解的理解

    注解分为编译时注解，运行时注解

* 说说你对依赖注入的理解
    A依赖B，用注解的方式来依赖B，节省很多重复性的代码。依赖注入和控制反转IOC是一个意思

* 说一下泛型原理，并举例说明


* Java中String的了解

* String为什么要设计成不可变的？

    1 String类本质上是char[]数组，并且也声明成了final，String声明成final可以防止被继承修改char[]数组的引用
    
    2 String类在java中用的很平凡，jdk设计者更希望String 在函数的传递中更像基本类型
    
    3 有人说声明成final ，JVM才不用对相关方法在虚函数表中查询，而直接定位到string类的相关方法上，提高了执行效率

* Object类的equal和hashCode方法重写，为什么？
    见上面

* HashMap的实现原理

    以散列表为基础的数据结构，通过计算key相应的hash值，存储到相应的位置上

* HashMap数据结构？

    散列表

* HashMap源码理解

   1 拉链法"实现的哈希表，默认初始容量大小是16 调整系数是0.75

   2 容量大小调整是 占用的桶 大于 capacity * load factor ，则将桶扩大两倍


* HashMap如何put数据（从HashMap源码角度讲解）？

    略

* HashMap怎么手写实现？

    1 存储数据的链表，初始容量
    2 需要考虑如何调整数据容量大小


* ConcurrentHashMap的实现原理

    1 采用锁分段的技术低版本
    2 高版本的是采用CAS算法及其他的同步技术


* ArrayMap和HashMap的对比

    ArrayMap是Android中提供的一个类，java中并没有。

    ArrayMap用两个数组来存储hash和key value(k-v存一个)，hashmap是链表数据来存储hash 和k-v

    ArrayMap的扩容是System.arrayCopy,HashMap是new,效率稍微差一点

    ArrayMap里面是正序排列的,因此查找是二分查找，在插入性能上比HashMap稍微高一点，查询性能上比不上HashMap

* HashTable实现原理

    在HashMap上加了同步锁

    HashTable不允许key和value为null

* TreeMap具体实现


* HashMap和HashTable的区别

    HashMap是线程不安全的，HashTable是线程安全的，在put等方法上加了同步关键字

* HashMap与HashSet的区别

    HashSet底层也是基于HashMap的

* HashSet与HashMap怎么判断集合元素重复？

    hashcode 还有equals：先判断K的hash值，然后判断key 时候相等，或者key equals 相等


* 集合Set实现Hash怎么防止碰撞

    判断两个key:如上

* ArrayList和LinkedList的区别，以及应用场景

    ArrayList是基于数组的(默认大小是10)，LinkList是基于链表的

    在插入，删除等上就是数组与链表的区别

* 什么是深拷贝和浅拷贝

    浅拷贝：基本类型拷贝值，引用类型拷贝引用地址。

    深拷贝：拷贝所有的属性，对于引用对象也要进行拷贝，可以使用串行操作

### 四、数据结构

* 常用数据结构简介

    线性表 栈 队列 树 散列表

* 数组和链表的区别

    略

* 二叉树的深度优先遍历和广度优先遍历的具体实现

* 堆的结构

* 堆和树的区别

* 堆和栈在内存中的区别是什么(解答提示：可以从数据结构方面以及实际实现方面两个方面去回答)？

* 手写链表逆序代码

* 讲一下对树，B+树的理解

* 讲一下对图的理解

* 判断单链表成环与否？

* 链表翻转（即：翻转一个单项链表）

* 合并多个单有序链表（假设都是递增的）


### 三、线程、多线程和线程池

* JVM内存模型

    JVM大体由三部分构成，堆，方法区，栈(VM栈，本地方法栈)，程序计数器。其中堆和方法区由线程共享，其他不共享。
    https://blog.csdn.net/qiyei2009/article/details/74838894

* 开启线程的三种方式？

    略

* 线程和进程的区别？

    略

* 为什么要有线程，而不是仅仅用进程？

    略

* run()和start()方法区别

    run()是线程体，线程正在运行，start()表示线程处于就绪态，可以由CPU来调度线程进行运行了。

* 如何控制某个方法允许并发访问线程的个数？

    ？？？？Semaphore,构造函数传递。acquire()用来获取一个许可

* 在Java中wait和seelp方法的不同；

    wait表示线程进入阻塞队列，sleep表示线程休眠
    
    wait会释放锁，sleep不会释放锁

* 谈谈wait/notify关键字的理解
    
    wait:释放锁，导致当前的线程等待，直到其他线程调用此对象的notify( ) 方法或 notifyAll( ) 方法
    
    notify:唤醒在此对象监视器上等待的单个线程

* 什么导致线程阻塞？

    耗时的操作，例如IO读取，网络请求，以及复杂的算法。大数据量运算等

* 线程如何关闭？

    线程执行完毕就自动关闭线程

* 讲一下java中的同步的方法

    synchronized volatile(轻量级) 锁

* 数据一致性如何保证？

    JMM的线程有序访问

* 如何保证线程安全？

    JMM线程有序性，可见性，加锁等

* 如何实现线程同步？

    略

* 两个进程同时要求写或者读，能不能实现？如何防止进程的同步？

    不能，用MappedByteBuffer或者socket实现同步，也可以借助操作系统的一些进程间通信方式来同步，例如共享内存，信号，管道等

* 线程间操作List

    略

* Java中对象的生命周期

    对象的整个生命周期大致可以分为7个阶段：创建阶段（Creation）、应用阶段（Using）、不可视阶段（Invisible）、不可到达阶段（Unreachable）、可收集阶段（Collected）、终结阶段（Finalized）与释放阶段（Free）。上面的这7个阶段，构成了 JVM中对象的完整的生命周期

* Synchronized用法

    略

* synchronize的原理

    加锁

* 谈谈对Synchronized关键字，类锁，方法锁，重入锁的理解

    见下面

* static synchronized 方法的多线程访问和作用
        
    锁的是类对象    
    
* 同一个类里面两个synchronized方法，两个线程同时访问的问题

   具体例子具体分析


* volatile的原理

    保证了多线程内存的可见性

* 谈谈volatile关键字的用法

    线程的可见性，操作具有原子性，例如基本变量的赋值，boolean int 等

* 谈谈volatile关键字的作用

    jvm中轻量级的同步手段

* 谈谈NIO的理解

    New IO
    
* synchronized 和volatile 关键字的区别

    略

* synchronized与Lock的区别

    略

* ReentrantLock 、synchronized和volatile比较
    可重入锁，需要看一下

* ReentrantLock的内部实现

* lock原理

* 死锁的四个必要条件？

    互斥条件：一个资源每次只能被一个进程使用，即在一段时间内某 资源仅为一个进程所占有。此时若有其他进程请求该资源，则请求进程只能等待。
    请求与保持条件：进程已经保持了至少一个资源，但又提出了新的资源请求，而该资源 已被其他进程占有，此时请求进程被阻塞，但对自己已获得的资源保持不放。
    不可剥夺条件:进程所获得的资源在未使用完毕之前，不能被其他进程强行夺走，即只能 由获得该资源的进程自己来释放（只能是主动释放)。
    循环等待条件: 若干进程间形成首尾相接循环等待资源的关系

* 怎么避免死锁？

    我们可以通过破坏死锁产生的4个必要条件来 预防死锁，由于资源互斥是资源使用的固有特性是无法改变的。
    
    破坏“不可剥夺”条件：一个进程不能获得所需要的全部资源时便处于等待状态，等待期间他占有的资源将被隐式的释放重新加入到 系统的资源列表中，可以被其他的进程使用，而等待的进程只有重新获得自己原有的资源以及新申请的资源才可以重新启动，执行。
    破坏”请求与保持条件“：第一种方法静态分配即每个进程在开始执行时就申请他所需要的全部资源。第二种是动态分配即每个进程在申请所需要的资源时他本身不占用系统资源。
    破坏“循环等待”条件：采用资源有序分配其基本思想是将系统中的所有资源顺序编号，将紧缺的，稀少的采用较大的编号，在申请资源时必须按照编号的顺序进行，一个进程只有获得较小编号的进程才能申请较大编号的进程。

    死锁避免的基本思想：系统对进程发出的每一个系统能够满足的资源申请进行动态检查，并根据检查结果决定是否分配资源，如果分配后系统可能发生死锁，则不予分配，否则予以分配，这是一种保证系统不进入死锁状态的动态策略。 
    如果操作系统能保证所有进程在有限时间内得到需要的全部资源，则系统处于安全状态否则系统是不安全的。
    
* 对象锁和类锁是否会互相影响？

    略

* 什么是线程池，如何使用?

* Java的并发、多线程、线程模型

* 谈谈对多线程的理解

* 多线程有什么要注意的问题？

* 谈谈你对并发编程的理解并举例说明

* 谈谈你对多线程同步机制的理解？

* 如何保证多线程读写文件的安全？

* 多线程断点续传原理


----

### 并发编程有关知识点（这个是一般Android开发用的少的，所以建议多去看看）：

平时Android开发中对并发编程可以做得比较少，Thread这个类经常会用到，但是我们想提升自己的话，一定不能停留在表面，,我们也应该去了解一下java的关于线程相关的源码级别的东西。


**学习的参考资料如下：**

> Java 内存模型

* [java线程安全总结](http://www.iteye.com/topic/806990)
* [深入理解java内存模型系列文章](http://ifeve.com/java-memory-model-0/)

> 线程状态：

* [一张图让你看懂JAVA线程间的状态转换](https://my.oschina.net/mingdongcheng/blog/139263)

> 锁：

* [锁机制：synchronized、Lock、Condition](http://blog.csdn.net/vking_wang/article/details/9952063)
* [Java 中的锁](http://wiki.jikexueyuan.com/project/java-concurrent/locks-in-java.html)

> 并发编程：

* [Java并发编程：Thread类的使用](http://www.cnblogs.com/dolphin0520/p/3920357.html)
* [Java多线程编程总结](http://blog.51cto.com/lavasoft/27069)
* [Java并发编程的总结与思考](https://www.jianshu.com/p/053943a425c3#)
* [Java并发编程实战-----synchronized](http://www.cnblogs.com/chenssy/p/4701027.html)
* [深入分析ConcurrentHashMap](http://www.infoq.com/cn/articles/ConcurrentHashMap#)
