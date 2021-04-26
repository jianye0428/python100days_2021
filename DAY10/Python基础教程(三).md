- [7. 面向对象编程](#7-面向对象编程)

# 7. 面向对象编程

万物皆是对象，Python当然支持面向对象编程。类和对象是面向对象编程的两个主要方面，类创建一个新的对象，对象是这个类的实例。

对象可以使用类的变量，属于对象或类的变量被称为域；对象也可以使用属于类的函数，这样的函数称为类的方法；域和方法可以合称为类的属性。

域有两种类型:
- 属于实例的
- 属于类本身

它们分别被称为实例变量和类变量。

类使用关键字```class```创建，类的域和方法被列在一个缩进块中。

类的方法必须有一个额外的第一个参数，但是在调用时不为这个参数赋值，这个特殊变量指对象本身，按照惯例它的名称是```self```，类似Java中的this。


在类中下面两个特都方法需要注意：
- ```__init__```方法：在类的一个对象被创建时调用该方法；相当于c++中的构造函数，就是当这个类调用了，那么这个__init__ 方法就要执行。
-```__del__```方法：在类的对象被销毁时调用该方法；相当于c++中的析构函数。在使用del删除一个对象时也就调用__del__方法，__del__是最后调用的。

Python中所有的类成员(包括数据成员)都是public的，没有Java的私有类，也就是人人都有调用类，虽然编写变成很简单， 但是资源人人都可以随意分配访问，在项目中确实一个不好的东西。

但是Python类的却有*私有变量*和*私有方法*之说，这个是一个例外，**如果使用的数据成员以双下划线为前缀，则为私有变量**。

你实例化这个类，访问不了。这是很多人忽略的

比如:

```
class public():
    _name = 'protected类型的变量'
    __info = '私有类型的变量'
    def _f(self):
        print("这是一个protected类型的方法")
    def __f2(self):
        print('这是一个私有类型的方法')
    def get(self):
        return(self.__info)
pub = public()
# 先打印可以访问的
print(pub._name)
pub._f()
####结果如下####
protected类型的变量
这是一个protected类型的方法


# 打印下类 私有变量和私有方法
print(pub.__info)
报错：'public' object has no attribute '__info'
pub._f2()
报错：pub._f2()
```

但是私有属性和方法可以在同一个类中被调用

```
pub.get()
#######
'私有类型的变量'
```

上面是很多人不知道的，下面，我来声明一个Person类
```
class Person():
    Count = 0
    def __init__(self, name, age):
        Person.Count += 1
        self.name = name
        self.__age = age
    
p = Person("Runsen", 20)

print(p.Count)

# 1 说明我实例化，这个__init__方法就要执行


print(p.name) #Runsen
print (p.__age) 
#AttributeError: Person instance has no attribute '__age'
#私有变量访问不了，报错
```

