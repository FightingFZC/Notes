---
title: NO.10 多线程
updated: 2023-01-21T17:33:05.0000000+08:00
created: 2021-02-05T08:41:48.0000000+08:00
---

NO.10 多线程
2021年2月5日
8:41
4、多线程

4.1、什么是进程？什么是线程？

进程是一个应用程序（1个进程是一个软件）。

线程是一个进程中的执行场景/执行单元。

一个进程可以启动多个线程。

**多线程三大特征：**

**原子性，可见性，有序性**

4.2、对于java程序来说，当在DOS命令窗口中输入：

java HelloWorld 回车之后。

会先启动JVM，而JVM就是一个进程。

JVM再启动一个主线程调用main方法。

同时再启动一个垃圾回收线程负责看护，回收垃圾。

最起码，现在的java程序中至少有两个线程并发，

一个是垃圾回收线程，一个是执行main方法的主线程。

4.3、进程和线程是什么关系？举个例子

阿里巴巴：进程

马云：阿里巴巴的一个线程

童文红:阿里巴巴的一个线程

京东：进程

强东：京东的一个线程

妹妹：京东的一个线程

进程可以看做是现实生活当中的公司。

线程可以看做是公司当中的某个员工。

注意：

进程A和进程B的内存独立不共享。（阿里巴巴和京东资源不会共享的！）

魔兽游戏是一个进程

酷狗音乐是一个进程

这两个进程是独立的，不共享资源。

线程A和线程B呢？

在java语言中：

线程A和线程B，堆内存和方法区内存共享。

但是栈内存独立，一个线程一个栈。

假设启动10个线程，会有10个栈空间，每个栈和每个栈之间，

互不干扰，各自执行各自的，这就是多线程并发。

火车站，可以看做是一个进程。

火车站中的每一个售票窗口可以看做是一个线程。

我在窗口1购票，你可以在窗口2购票，你不需要等我，我也不需要等你。

所以多线程并发可以提高效率。

java中之所以有多线程机制，目的就是为了提高程序的处理效率。

4.4、思考一个问题：

使用了多线程机制之后，main方法结束，是不是有可能程序也不会结束。

**main方法结束只是主线程结束了，主栈空了，其它的栈(线程)可能还在**

**压栈弹栈。**

4.5、分析一个问题：对于单核的CPU来说，真的可以做到真正的多线程并发吗？

对于多核的CPU电脑来说，真正的多线程并发是没问题的。

4核CPU表示同一个时间点上，可以真正的有4个进程并发执行。

什么是真正的多线程并发？

t1线程执行t1的。

t2线程执行t2的。

t1不会影响t2，t2也不会影响t1。这叫做真正的多线程并发。

单核的CPU表示只有一个大脑：

不能够做到真正的多线程并发，但是可以做到给人一种“多线程并发”的感觉。

对于单核的CPU来说，在某一个时间点上实际上只能处理一件事情，但是由于

CPU的处理速度极快，多个线程之间频繁切换执行，跟人来的感觉是：多个事情

同时在做！！！！！

线程A：播放音乐

线程B：运行魔兽游戏

线程A和线程B频繁切换执行，人类会感觉音乐一直在播放，游戏一直在运行，

给我们的感觉是同时并发的。

电影院采用胶卷播放电影，一个胶卷一个胶卷播放速度达到一定程度之后，

人类的眼睛产生了错觉，感觉是动画的。这说明人类的反应速度很慢，就像

一根钢针扎到手上，到最终感觉到疼，这个过程是需要“很长的”时间的，在

这个期间计算机可以进行亿万次的循环。所以计算机的执行速度很快。

5、java语言中，实现线程有两种方式（**其实有三种，第三种先不学**），那两种方式呢？

java支持多线程机制。并且java已经将多线程实现了，我们只需要继承就行了。

第一种方式：编写一个类，直接继承java.lang.Thread，**重写run方法**。

// 定义线程类

public class MyThread extends Thread{

public void run(){

}

}

// 创建线程对象

MyThread t = new MyThread();

// 启动线程。 在JVM中开辟一个新的栈空间，然后该方法结束，

t.start();

**启动成功的线程会自动调用run方法，在支线程的地位和main方法一样。**

**PS：不要直接调用run方法，否则压根就变成了单线程，不能并发。**

第二种方式：编写一个类，实现java.lang.Runnable接口，实现run方法。

// 定义一个可运行的类（**还不是线程类**）

public class MyRunnable implements Runnable {

public void run(){

}

}

// 创建线程对象（t才是线程对象的引用。）

Thread t = new Thread(new MyRunnable());

// 启动线程

t.start();

注意：第二种方式实现接口比较常用，因为一个类实现了接口，它还可以去继承

其它的类，更灵活。

6、关于线程对象的生命周期？
新建状态

就绪状态

运行状态

阻塞状态

死亡状态

![image1](resources/image1-8.png)

7、线程需要知道的一些方法
1.  Thread中的String getName()
    1.  返回当前线程的名字
2.  Thread中的void setName()
    1.  设置当前线程的名字
3.  Thread中的public static Thread currentThread()
    1.  返回当前线程的引用，然后使用一些方法。
    2.  和this很像。不过前者有局限性
    3.  例如main方法调用其他类的方法。实际线程是main，而this.getName()就没用了。
    4.  ![image2](resources/image2-7.png)
4.  Thread中的public static void sleep(long time)
    1.  让当前线程休眠time毫秒，变成阻塞状态
5.  Thread中的void interrupt()
    1.  调用此方法的引用代表的线程结束睡眠，开始干活！
    2.  之后会爆异常，说睡眠被终止，不过我觉得可以无视哦！
    3.  这个异常是被catch住然后打印出来的，不想要可以不打印
6.  void stop()
    1.  结束进程
    2.  过时了
    3.  缺点：会丢失数据。接下来讲更合理的终止线程
7.  这是一种终止线程进行的思想，而不是方法。
    1.  线程执行的时候添加一个条件，条件默认为true，当需要结束线程的时候，在外部把这个线程执行条件改为false即可
    2.  不过最好在再加个else，在保存需要保存的数据。
1、(这部分内容属于了解)关于线程的调度

1.1、常见的线程调度模型有哪些？

抢占式调度模型：

那个线程的优先级比较高，抢到的CPU时间片的概率就高一些/多一些。

java采用的就是抢占式调度模型。

均分式调度模型：

平均分配CPU时间片。每个线程占有的CPU时间片时间长度一样。

平均分配，一切平等。

有一些编程语言，线程调度模型采用的是这种方式。

1.2、java中提供了哪些方法是和线程调度有关系的呢？

实例方法：

void setPriority(int newPriority) 设置线程的优先级

int getPriority() 获取线程优先级

最低优先级1

默认优先级是5

最高优先级10

优先级比较高的获取CPU时间片可能会多一些。（但也不完全是，大概率是多的。）

静态方法：

static void yield() 让位方法

暂停当前正在执行的线程对象，并执行其他线程

yield()方法不是阻塞方法。让当前线程让位，让给其它线程使用。

yield()方法的执行会让当前线程从“运行状态”回到“就绪状态”。

注意：在回到就绪之后，有可能还会再次抢到。

实例方法：

void join()

合并线程

class MyThread1 extends Thread {

public void doSome(){

MyThread2 t = new MyThread2();

t.join(); // 当前线程进入阻塞，t线程执行，直到t线程结束。当前线程才可以继续。(类似插队）

}

}

class MyThread2 extends Thread{

}

2、关于多线程并发环境下，数据的安全问题。

2.1、为什么这个是重点？

以后在开发中，我们的项目都是运行在服务器当中，

而服务器已经将线程的定义，线程对象的创建，线程

的启动等，都已经实现完了。这些代码我们都不需要

编写。

最重要的是：你要知道，你编写的程序需要放到一个

多线程的环境下运行，你更需要关注的是这些数据

在多线程并发的环境下是否是安全的。（重点：\*\*\*\*\*）

2.2、什么时候数据在多线程并发的环境下会存在安全问题呢？

三个条件：

**条件1：多线程并发。**

**条件2：有共享数据。**

**条件3：共享数据有修改的行为。**

满足以上3个条件之后，就会存在线程安全问题。

2.3、怎么解决线程安全问题呢？

当多线程并发的环境下，有共享数据，并且这个数据还会被修改，此时就存在

线程安全问题，怎么解决这个问题？

线程排队执行。（不能并发）。

用排队执行解决线程安全问题。

**这种机制被称为：线程同步机制。**

专业术语叫做：线程同步，实际上就是线程**不能并发**了，线程必须排队执行。

**怎么解决线程安全问题呀？**

**使用“线程同步机制”。**

线程同步就是线程排队了，线程排队了就会牺牲一部分效率，没办法，数据安全

第一位，只有数据安全了，我们才可以谈效率。数据不安全，没有效率的事儿。

2.4、说到线程同步这块，涉及到这两个专业术语：

异步编程模型：

线程t1和线程t2，各自执行各自的，t1不管t2，t2不管t1，

谁也不需要等谁，这种编程模型叫做：异步编程模型。

**其实就是：多线程并发（效率较高。）**

**异步就是并发。**

同步编程模型：

线程t1和线程t2，在线程t1执行的时候，必须等待t2线程执行

结束，或者说在t2线程执行的时候，必须等待t1线程执行结束，

两个线程之间发生了等待关系，这就是同步编程模型。

**效率较低。线程排队执行。**

**同步就是排队。**

3、Java中有三大变量？【重要的内容。】

实例变量：在堆中。

静态变量：在方法区。

局部变量：在栈中。

以上三大变量中：

局部变量永远都不会存在线程安全问题。

因为局部变量不共享。（一个线程一个栈。）

局部变量在栈中。所以局部变量永远都不会共享。

实例变量在堆中，堆只有1个。

静态变量在方法区中，方法区只有1个。

堆和方法区都是多线程共享的，所以可能存在线程安全问题。

局部变量+**常量**：不会有线程安全问题，常量改不了，共享也没事

成员变量：可能会有线程安全问题。

4、如果使用局部变量的话：
建议使用：StringBuilder。

因为局部变量不存在线程安全问题。选择StringBuilder。

StringBuffer效率比较低。

ArrayList是非线程安全的。

Vector是线程安全的。

HashMap HashSet是非线程安全的。

Hashtable是线程安全的。

5、总结：
synchronized就是有把锁来锁住里面的东西，

**synchronized有三种写法：**

**第一种：同步代码块**

**灵活**

**synchronized(线程共享对象){**

**同步代码块;**

**}**

**第二种：在实例方法上使用synchronized**

**表示共享对象一定是this**

**并且同步代码块是整个方法体，可能导致无故扩大执行时间**

**优点：代码简洁了**

**重点！！！：若有多个实例方法被写上synchronized，那就如同可以写方法的synchronized同步代码块，只要有一个线程访问了其中一个实例方法，那么其他线程不能访问被synchronized修饰的任何一个实例方法**

**第三种：在静态方法上使用synchronized**

**表示找类锁。**

**类锁永远只有1把。（毕竟静态方法需要使用类名访问的嘛。）**

**就算创建了100个对象，那类锁也只有一把。（这里可能想说的是通过引用.访问静态方法）**

synchronized是怎么实现作用的：当一个线程访问到被synchronized修饰的代码块后，别的线程也访问到，这时候会停在门口，不运行。。

**对象锁：1个对象1把锁，100个对象100把锁。**

**类锁：100个对象，也可能只是1把类锁。**

6、聊一聊，我们以后开发中应该怎么解决线程安全问题？

是一上来就选择线程同步吗？synchronized

不是，synchronized会让程序的执行效率降低，用户体验不好。

系统的用户吞吐量降低。用户体验差。在不得已的情况下再选择

线程同步机制。

第一种方案：尽量使用局部变量代替“实例变量和静态变量”。

第二种方案：如果必须是实例变量，那么可以考虑创建多个对象，这样

实例变量的内存就不共享了。（一个线程对应1个对象，100个线程对应100个对象，

对象不共享，就没有数据安全问题了。）

第三种方案：如果不能使用局部变量，对象也不能创建多个，这个时候

就只能选择synchronized了。线程同步机制。

7、线程这块还有那些内容呢？列举一下
7.1、守护线程

7.2、定时器

7.3、实现线程的**第三种方式**：FutureTask方式，实现Callable接口。（JDK8新特性。）

7.4、关于Object类中的wait和notify方法。（生产者和消费者模式！）

8、线程这块还有那些内容呢？列举一下

1.1、守护线程

java语言中线程分为两大类：

一类是：用户线程

一类是：守护线程（后台线程）

其中具有代表性的就是：垃圾回收线程（守护线程）。

守护线程的特点：

一般守护线程是一个死循环，所有的用户线程只要结束，

守护线程自动结束。

使用：

setDaemon(boolean isDaemon)

注意：主线程main方法是一个用户线程。

守护线程用在什么地方呢？

每天00:00的时候系统数据自动备份。

这个需要使用到定时器，并且我们可以将定时器设置为守护线程。

一直在那里看着，没到00:00的时候就备份一次。所有的用户线程

如果结束了，守护线程自动退出，没有必要进行数据备份了。

1.2、定时器

定时器的作用：

间隔特定的时间，执行特定的程序。

每周要进行银行账户的总账操作。

每天要进行数据的备份操作。

在实际的开发中，每隔多久执行一段特定的程序，这种需求是很常见的，

那么在java中其实可以采用多种方式实现：

可以使用sleep方法，睡眠，设置睡眠时间，没到这个时间点醒来，执行

任务。这种方式是最原始的定时器。（比较low）

在java的类库中已经写好了一个定时器：java.util.Timer，可以直接拿来用。

不过，这种方式在目前的开发中也很少用，因为现在有很多高级框架都是支持

定时任务的。

在实际的开发中，目前使用较多的是Spring框架中提供的SpringTask框架，

这个框架只要进行简单的配置，就可以完成定时器的任务。

1.3、实现线程的第三种方式：实现Callable接口。（JDK8新特性。）

这种方式实现的线程可以获取线程的返回值。

之前讲解的那两种方式是无法获取线程返回值的，因为run方法返回void。

![image3](resources/image3-5.png)

![image4](resources/image4-4.png)

![image5](resources/image5-4.png)

思考：

系统委派一个线程去执行一个任务，该线程执行完任务之后，可能

会有一个执行结果，我们怎么能拿到这个执行结果呢？

使用第三种方式：实现Callable接口方式。

1.4、关于Object类中的wait和notify方法。（生产者和消费者模式！）

第一：wait和notify方法不是线程对象的方法，是java中任何一个java对象

都有的方法，因为这两个方式是Object类中自带的。

wait方法和notify方法不是通过线程对象调用，

不是这样的：t.wait()，也不是这样的：t.notify()..不对。

第二：wait()方法作用？

Object o = new Object();

o.wait();

表示：

让正在o对象上活动的线程进入等待状态，无期限等待，

直到被唤醒为止。

o.wait();方法的调用，会让“当前线程（正在o对象上

活动的线程）”进入等待状态。

第三：notify()方法作用？

Object o = new Object();

o.notify();

表示：

唤醒正在o对象上等待的线程。

还有一个notifyAll()方法：

这个方法是唤醒o对象上处于等待的所有线程。
![image6](resources/image6-4.png)![image7](resources/image7-4.png)![image8](resources/image8-3.png)
