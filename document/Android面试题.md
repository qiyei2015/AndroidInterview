# Android面试题

Android面试题除了Android基础之外，更多的问的是一些源码级别的、原理这些等。所以想去大公司面试，一定要多看看源码和实现方式，常用框架可以试试自己能不能手写实现一下，锻炼一下自己。

### 一、Android基础知识点

* 四大组件是什么

 Activity Service BroadcastReceiver ContentProvider

* 四大组件的生命周期和简单用法

activity:onCreate onStart onResume onPause onStop onDestory

service: start:onCreate onStartCommand onDestory    bind:[onCreate] onBind onUnbind [onDestory]

receiver:onReceive

contentProvider: onCreate

* Activity之间的通信方式

    intent

* Activity各种情况下的生命周期

    略

* 横竖屏切换的时候，Activity 各种情况下的生命周期

    onCreate onStart onResume onPause onStop onDestory

* Activity与Fragment之间生命周期比较

    Activity:onCreate onStart onResume onPause onStop onDestory

    Fragment:onAttach() onCreate onCreateView onStart onResume onPause onStop onDestoryView onDestory

* Activity上有Dialog的时候按Home键时的生命周期

    普通dialog: onPause onStop
    ActivityDialog: 弹出对话框时已经调用onPause 后面直接调用 onStop

* 两个Activity 之间跳转时必然会执行的是哪几个方法？

   一般 onPause onStop  --> [onCreate] onStart onResume

    特殊情况：onPause --> onStart onResume


* 前台切换到后台，然后再回到前台，Activity生命周期回调方法。弹出Dialog，生命值周期回调方法。

    前台到后台：onPause onStop

    后台到前台：onStart onResume

    弹出Activity Dialog: onPause 结束dialog onResume


* Activity的四种启动模式对比

    standard:标准启动模式 栈类实例

    singleTop:栈顶单例

    singleTask:栈内单例

    singleInstance:单独一个栈


* Activity状态保存于恢复

    保存：onSaveInstanceState

    恢复：onCreate中的Bundle参数

* fragment各种情况下的生命周期

    Fragment:onAttach() onCreate onCreateView onStart onResume onPause onStop onDestoryView onDestory

* Fragment状态保存startActivityForResult是哪个类的方法，在什么情况下使用？

    context,在启动的Activity需要返回时调用

* 如何实现Fragment的滑动？

    ViewPager

* fragment之间传递数据的方式？

    构造时：setArguments Bundle


* Activity 怎么和Service 绑定？

    bindService


* 怎么在Activity 中启动自己对应的Service？

    bindService?

* service和activity怎么进行数据交互？

    startService:intent

* Service的开启方式

    startService:

    BindService:

* 请描述一下Service 的生命周期

    service: onCreate onStartCommand onDestory   [onCreate] onBind onUnbind [onDestory]

* 谈谈你对ContentProvider的理解

    数据提供者，一般结合数据库使用

* 说说ContentProvider、ContentResolver、ContentObserver 之间的关系

    ContentProvider是内容提供者，主要用于实现数据访问的接口

    ContentResolver是内容解析者，用于对ContentProvider的访问

    ContentObserver是内容观察者，用于观察uri数据的变化

* 请描述一下广播BroadcastReceiver的理解

    android提供的一种通讯方式

* 广播的分类

    静态广播，动态广播

    全局广播，本地广播

* 广播使用的方式和场景

    略

* 在manifest 和代码中如何注册和使用BroadcastReceiver?

    静态注册，动态注册

* 本地广播和全局广播有什么差别？

    作用域范围不同，全局广播是整个系统，本地广播只有本进程内有效

* BroadcastReceiver，LocalBroadcastReceiver 区别

    略，没有LocalBroadcastReceiver这个类吧？

* AlertDialog,popupWindow,Activity区别

    对话框 弹窗

    这几种窗口的窗口类型和主序不同，都受WMS管理

* Application 和 Activity 的 Context 对象的区别

    两种不同的context,生命周期不同

* Android属性动画特性

    能对View的属性做动画，保留了View这些监听之类的属性


* 如何导入外部数据库?

    不太明白啥意思？

* LinearLayout、RelativeLayout、FrameLayout的特性及对比，并介绍使用场景。

    略

* 谈谈对接口与回调的理解

    略

* 回调的原理

    略

* 写一个回调demo

    略

* 介绍下SurfView

    一个View控件 生命周期分别为surfaceCreated（创建）   surfaceChanged（改变）   surfaceDestroyed（销毁）
    绘图是由SurfaceHolder来完成的，不受必须在主线程更新UI的限制，常用作复杂界面，例如游戏，相机等界面图像的绘制

* RecycleView的使用

    略

* 序列化的作用，以及Android两种序列化的区别

    略

* 差值器



* 估值器


* Android中数据存储方式

    略

### 二、Android源码相关分析

* Android动画框架实现原理

    属性动画主要是调用setXxx改变属性

* Android各个版本API的区别

    略

* Requestlayout，onlayout，onDraw，DrawChild区别与联系

    请求布局，布局回调，draw回调 绘制child

* invalidate和postInvalidate的区别及使用

    invalidate:UI线程使用，使整个UI重绘
    postInvalidate：非UI线程使用

* Activity-Window-View三者的差别

    window包含activity,activity包含View

* 谈谈对Volley的理解

    后面再讲

* 如何优化自定义View

    onDraw中不要有耗时的操作

* 低版本SDK如何实现高版本api？

    1 support 包中去找相应的api替代

    2 @TargeApi()解决编译错误，使用版本判断

* 描述一次网络请求的流程

    发起请求 tcp握手 写入流 获取response tcp连接关闭

* HttpUrlConnection 和 okhttp关系

 HttpUrlConnection 是java的网络连接的api okhttp是一个高效的网络库

* Bitmap对象的理解

    位图，利用每一个字节来表示像素

* looper架构

    MessageQueue Handler Message Looper ThreadLocal

* ActivityThread，AMS，WMS的工作原理

    后续会重点讲

* 自定义View如何考虑机型适配

    不明白问题想问的，要匹配什么？布局不要写死，view大小不要写死

* 自定义View的事件

    View事件分发流程？

* AstncTask+HttpClient 与 AsyncHttpClient有什么区别？


* LaunchMode应用场景

    启动模式，参考四种启动模式

* AsyncTask 如何使用?

    略

* SpareArray原理

    参考java

* 请介绍下ContentProvider 是如何实现数据共享的？

    待定

* AndroidService与Activity之间通信的几种方式

    bindservice intent 广播

* IntentService原理及作用是什么？

    thread service

* 说说Activity、Intent、Service 是什么关系

    略

* ApplicationContext和ActivityContext的区别

    略

* SP是进程同步的吗?有什么方法做到同步？

    不是，低版本支持多进程读写。MODE_MULTI_PROCESS 使用ContentProvider来替代和同步

* 谈谈多线程在Android中的使用

    略

* 进程和 Application 的生命周期

    略

* 封装View的时候怎么知道view的大小

    不太理解题目，怎么获取View的大小？handle post ViewTree监听

* RecycleView原理

    略

* AndroidManifest的作用与理解

    资源清单文件，打包，和安装的时候都会用到

### 三、常见的一些原理性问题

* Handler机制和底层实现

    略

* Handler、Thread和HandlerThread的差别

    略

* handler发消息给子线程，looper怎么启动？

    略

* 关于Handler，在任何地方new Handler 都是什么线程下?

    要看Looper

* ThreadLocal原理，实现及如何保证Local属性？

    jvm

* 请解释下在单线程模型中Message、Handler、Message Queue、Looper之间的关系

    略

* 请描述一下View事件传递分发机制

    略

* Touch事件传递流程

    略

* 事件分发中的onTouch 和onTouchEvent 有什么区别，又该如何使用？

    略

* View和ViewGroup分别有哪些事件分发相关的回调方法

    略

* View刷新机制

    requestLayout invalite()

* View绘制流程

    略

* 自定义控件原理

    略

* 自定义View如何提供获取View属性的接口？

    略

* Android代码中实现WAP方式联网
* AsyncTask机制

    略

* AsyncTask原理及不足

    略

* 如何取消AsyncTask？

    略

* 为什么不能在子线程更新UI？

    ViewRootImpl View不是线程安全的

* ANR产生的原因是什么？

    三种

* ANR定位和修正

  StrictMode BlockCanary
  
* oom是什么？

    略

* 什么情况导致oom？

    略

* 有什么解决方法可以避免OOM？

    略

* Oom 是否可以try catch？为什么？

    应该可以，需要试验一下。https://www.jianshu.com/p/e574f0ffdb42

* 内存泄漏是什么？

    略

* 什么情况导致内存泄漏？

    略

* 如何防止线程的内存泄漏？

    略

* 内存泄露场的解决方法

    略

* 内存泄漏和内存溢出区别？

    略

* LruCache默认缓存大小

    默认0，构造方法就需要指定大小

* ContentProvider的权限管理(解答：读写分离，权限控制-精确到表级，URL控制)

    不懂

* 如何通过广播拦截和abort一条短信？

    不懂

* 广播是否可以请求网络？

    不行，广播中不能有耗时的操作

* 广播引起anr的时间限制是多少？

    15秒

* 计算一个view的嵌套层级

    略

* Activity栈

    略

* Android线程有没有上限？

    有 ，Linux句柄数

* 线程池有没有上限？

    有

* ListView重用的是什么？

    View

* Android为什么引入Parcelable？

    更搞笑

* 有没有尝试简化Parcelable的使用？

    略

### 四、开发中常见的一些问题

* ListView 中图片错位的问题是如何产生的?

    可以重点关注

* 混合开发有了解吗？

    略

* 知道哪些混合开发的方式？说出它们的优缺点和各自使用场景？（解答：比如:RN，weex，H5，小程序，WPA等。做Android的了解一些前端js等还是很有好处的)；

    略

* 屏幕适配的处理技巧都有哪些?

    关注

* 服务器只提供数据接收接口，在多线程或多进程条件下，如何保证数据的有序到达？

    线程同步，数据分片

* 动态布局的理解

    略

* 怎么去除重复代码？

    略 工具

* 画出 Android 的大体架构图

    略

* Recycleview和ListView的区别

    重点关注

* ListView图片加载错乱的原理和解决方案

    略 设置tag

* 动态权限适配方案，权限组的概念

    略

* Android系统为什么会设计ContentProvider？

    进程间共享数据

* 下拉状态栏是不是影响activity的生命周期

    不会

* 如果在onStop的时候做了网络请求，onResume的时候怎么恢复？

    ？？？？

* Bitmap 使用时候注意什么？

    重点关注

* Bitmap的recycler()

    略

* Android中开启摄像头的主要步骤

    略

* ViewPager使用细节，如何设置成每次只初始化当前的Fragment，其他的不初始化？

    略

* 点击事件被拦截，但是想传到下面的View，如何操作？

    略 return flase

* 微信主页面的实现方式

    略

* 微信上消息小红点的原理

    重点关注

* CAS介绍（这是阿里巴巴的面试题，我不是很了解，可以参考博客: [CAS简介](http://blog.csdn.net/jly4758/article/details/46673835)）

    多线程的？

