- [进程和线程](#进程和线程)
- [python线程和进程的使用](#python线程和进程的使用)
- [练习](#练习)
- [线程间变量的共享](#线程间变量的共享)

# 进程和线程
我们打开我们的计算机就会看到进程和线程

![](https://camo.githubusercontent.com/e0c96d16e6655e948fd4720958b0681e37c415def82a047656d46bb43c5b2066/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139303430393232303333323435362e706e67)


>那什么是进程什么是线程?

我的理解是进程是指在系统中正在运行的一个应用程序；程序一旦运行就是进程，或者更专业化来说：进程是指程序执行时的一个实例。

**线程是进程的一个实体。**

**进程——资源分配的最小单位，线程——程序执行的最小单位。**

我举个例子，比如打开qq，就是一个线程，有很多个qq上号就是进程.

# python线程和进程的使用

>python线程和进程的使用

Python通过两个标准库```_thread```和```threading```提供对线程的支持, threading对_thread进行了封装。threading模块中提供了Thread，Lock，RLock，Condition等组件。

在Python中线程和进程的使用就是通过```Thread```这个类。这个类在我们的_thread和threading模块中。

Thread类:
|常用参数|说明|
|----|----|
|```target```|表示调用对象，即子线程要执行的任务|
|```name```|子线程的名称|
|```args```|传入target函数中的位置参数，是一个元组，参数后必须加逗号|

|常用实例方法|说明|
|----|----|
|```Thread.run(self)```|线程启动时运行的方法，由该方法调用target参数所指定的函数|
|```Thread.start(self)```|启动进程，start方法就是去帮你调用run方法|
|```Thread.terminate(self)```|强制终止线程|
|```Thread.join(self,timeout=None)```|阻塞调用，主线程进程等待|
|```Thread.setDaemon(self,daemonic)```|将子线程设置为守护线程|
|```Thread.getName(self,Name)```|获取线程名称|
|```Thread.setName(self,Name)```|设置线程名称|

看一个标准的多线程的例子：
```py
import threading
import time

#定义线程要运行的函数
def func(name,a):
    time.sleep(2)#为了便于观察，让他睡两秒
    print("I am %s" % name)

#创建一个线程实例，args参数是一个元组，必须加逗号
t1 = threading.Thread(target=func, args=("wangxian",0))
#在创建一个线程实例
t2 = threading.Thread(target=func, args=("jianye",0))
#启动线程
t1.setDaemon(true)
#t2.setDaemon(true)
t1.start()
#启动另一个线程
t2.start()
#打印线程名字
print(t1.getName())
print(t2.getName())
```

# 练习
下面我们来练习下， 加深hreading模块的使用。

我写了下面的代码
```py
# -*- coding：utf-8 -*-
# time ：2019/4/9 21:52
# author: Runsen
import threading
import time
def fun1():
    print('hello')
    time.sleep(2)
    print('Bye')
def fun2():
    print('hi')
    time.sleep(2)
    print('OUT')
t1 = threading.Thread(target=fun1())
t2 = threading.Thread(target=fun2())
t1.start()
t2.start()
# t1.join()
# t2.join()
print('主线程完毕')
```
我们先不加join()来阻塞，t1和t2两个线程同时执行，由于位置先打印hello，再打印hi，这个时候都sleep2秒钟，但是他sleep2秒钟，主程序还是在执行，所以下面打印print('主线程完毕')，最后才打印Bye和OUT
```markdown
hello
hi
主线程完毕
Bye
OUT
```

# 线程间变量的共享

在多线程中，所有变量对于所有线程都是共享的，因此，线程之间共享数据最大的危险在于多个线程同时修改一个变量，那就乱套了，所以需要互斥所，来锁住数据。

线程间全局变量的共享:
```py
from threading import Thread
a = 1

def func():
    global a
    a = 2

t = Thread(target=func())
t.start()
t.join()

print(a)
```

代码如上图所示，打印的a是1还是2?

答案是 ：2。因为出现了global，线程间变量的共享，在func中的a是全局变量。

**注意:** 因为线程属于同一个进程，因此它们之间共享内存区域。因此全局变量是公共的。

下面，我们提高一点点难度，代码如下图所示，还是猜一猜a是啥东西。注意:这里出现了join来阻塞来增加了加和减的操作。

```py
from threading import Thread
a = 0
n = 1000000#指定加减次数

def incr(n):
    global a
    for i in range(n):#对全局变量做n次加1
        a += 1

def decr(n):
    global a
    for i in range(n):#对全局变量做n次减1
        a -= 1

t_incr = Thread(target=incr, args=(n, ))
t_decr = Thread(target=decr, args=(n, ))
t_incr.start()
t_decr.start()

t_incr.join()
t_decr.join()

print(a)
```
相信很多人都认为是0，其实这个a的值是变化的，可能这次是0 ，下次是1，还有可能是1000000，a就是在[-1000000，1000000]中的一个随机数。

为什么呢？这是因为虽然他们是同时运行的，但是同时在修改我们的a，那就乱了。这是导致a，for i in range(1000000)，就是遍历了1000000，incr和decr的方法都加上一起了，在这1000000次遍历中，不知道有多少加，多少减，比如，我1000000都是加，没有减，a就是1000000。

如果你就是想出现0，其实加一个互斥锁就可以了。这样你加多少次，我就减多少次，加减的次数不会叠加。因此来了lock的用法

```py
from threading import Thread
a = 0
n = 1000000
lock = Lock()#线程锁

def incr(n):
    global a
    for i in range(n):#对全局变量做n次加1
        with lock:
            a += 1

def decr(n):
    global a
    for i in range(n):#对全局变量做n次减1
        with lock:
            a -= 1
t_incr = Thread(target=incr, args=(n, ))
t_decr = Thread(target=decr, args=(n, ))
t_incr.start()
t_decr.start()

t_incr.join()
t_decr.join()

print(a)
```

这个a怎么运行都是 0。因为我们把这个a锁上了，这样就加1000000次，减1000000次，怎么出来都是我们的0。