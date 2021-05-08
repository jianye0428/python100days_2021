- [队列](#队列)
- [线程池](#线程池)
- [多线程典型例子](#多线程典型例子)

# 队列
上文锁能解决问题，但是不常见

**队列的基本概念**
一个入口，一个出口，先入先出(FIFO)。

![](https://camo.githubusercontent.com/6491a62896de5c74132efd51fcf3d698bfc84bf66fd808faa3aa7d7928bb63aa/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139303430393232333430373933312e706e67)

导入:```from queue import Queue```

```py
from queue import Queue
from threading import Thread
from random import randint
my_queue = Queue(3)
def f1(my_queus):
    for i in range(3):
        num = randint(0,10)
        print(num)
        my_queue.put(num)
def f2(my_queus):
    for i in range(3):
        num = my_queue.get()
        print(num)
t1 = Thread(target=f1,args=(my_queue,))
t2 = Thread(target=f2,args=(my_queue,))
t1.start()
t2.start()
t1.join()
t2.join()
```
0 5 10 0 5 10

![](https://camo.githubusercontent.com/579e00447b924630ef00b4c4e69fc22e42287e9367f2905dd18039f2c780a608/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139303430393232343431393332392e706e67)

# 线程池

```py
from multiprocessing.pool import ThreadPool
import time
def hello(name):
    print('hello,{}'.format(name))
    time.sleep(2)
    print('Bye')
t = ThreadPool(3)
for i in range(3):
    t.apply_async(hello,args=(i,))
t.close()
t.join()
```

OUT： 几乎一起完成 hello,0 hello,1 hello,2 几乎一起完成 Bye Bye Bye

```py
from multiprocessing.pool import ThreadPool
import time

t = ThreadPool(2) #直接使用内置的

def task1():
    time.sleep(2)
    print('任务完成')
def task(*args, **kwargs):
    time.sleep(2)
    print('任务完成:',args,kwargs)

pool.apply_async(task1)
pool.apply_async(task2, args=(1,2), kwds={'a':1,'b':2})
print('任务提交完')#要求: 在join前必须要close，这样就不允许在提交任务了
pool.close()
pool.join()
print('任务完成')
```

对于进程和线程，可以提高爬虫速度

# 多线程典型例子

```py
# -*- coding：utf-8 -*-
# time ：2019/4/23 10:13
# author: 毛利

import threading
import time
import random
MONEY = 0
gLock = threading.Lock()

def Procuder():
    while True:
        global MONEY
        random_money = random.randint(10,100)
        gLock.acquire()
        MONEY += random_money
        gLock.release()
        print ('生产者%s-生产了%d' % (threading.current_thread,random_money))
        time.sleep(0.5)

def Customer():
    while True:
        global MONEY
        random_money = random.randint(10,100)
        if MONEY > random_money:
            print ('消费者%s-消费了：%d' % (threading.current_thread,random_money))
            gLock.acquire()
            MONEY -= random_money
            gLock.release()
        else:
            print ('需要消费的钱为：%d，余额为：%d，' % (random_money,MONEY))
        time.sleep(0.5)

def p_c_test():
    # 执行3个线程，来当作生产者
    for x in range(3):
        th = threading.Thread(target=Procuder)
        th.start()
    # 执行3个线程，来当作消费者
    for x in range(3):
        th = threading.Thread(target=Customer)
        th.start()

if __name__ == "__main__":
    p_c_test()
```

![](https://camo.githubusercontent.com/23a0718a1019a8c2242a38135d7d17f179bd86535e3a2c206da9a9319eb97eea/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139303432343231343133323332372e706e67)