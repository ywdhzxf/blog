
---
title: python 中__init__ ,__new__ ,__call__,__del__ 方法
date: 2019-05-06 12:36:15
tags: Python
---


## python 中`__init__` ,`__new__` ,`__call__`,`__del__` 方法

### 三个方法的作用

```
__new__   负责创建一个实例对象
__init__  负责将该实例对象初始化
__call__  使实例能够像函数一样被调用，同时不影响实例本身的生命周期（__call__()不影响一个实例的构造和析构）。但是__call__()可以用来改变实例的内部成员的值。
```

### `__init__()`

```
负责初始化, 在Python中，__init__()函数的意义等同于类的构造器（同理，__del__()等同于类的析构函数）。因此，__init__()方法的作用是创建一个类的实例
```

###`__call__()`

```
在Python中, 函数其实就是对象, 所有的函数都是一级对象, 也叫可调用对象, 这意味着Python中的函数的引用可以作为输入传递到其他的函数/方法中，并在其中被执行。 
而Python中类的实例（对象）可以被当做函数对待。 一个类实例也可以变成一个可调用对象，只需要实现一个特殊方法__call__()。 也就是说，我们可以将它们作为输入传递到其他的函数/方法中并调用他们，正如我们调用一个正常的函数那样。而类中__call__()函数的意义正在于此。为了将一个类实例当做函数调用，我们需要在类中实现__call__()方法。也就是我们要在类中实现如下方法：def __call__(self, *args)。这个方法接受一定数量的变量作为输入。 
假设x是X类的一个实例。那么调用x.__call__(1,2)等同于调用x(1,2)。这个实例本身在这里相当于一个函数。

```

### `__del__`

```
在对象的生命周期结束时, __del__会被调用,可以将__del__理解为"析构函数".
__del__定义的是当一个对象进行垃圾回收时候的行为。

有一点容易被人误解, 实际上，x.__del__() 并不是对于del x的实现,但是往往执行del x时会调用x.__del__();
调用x.__del__, 并不会删除这个对象, 但是如果你 del x,他会自动调用__del__方法, x这个对象就不存在了
```



## `__new__()`

```
官方文档的说法, __new__方法主要是当你继承一些不可变的class时(比如int, str, tuple)， 提供给你一个自定义这些类的实例化过程的途径。还有就是实现自定义的metaclass。
可以参考两段代码
class PositiveInteger(int):
    def __init__(self, value):
        super(PositiveInteger, self).__init__(self, abs(value))
i = PositiveInteger(-3)
print i
结果是 -3, 因为 int 是不可变的对象, 我们必须要重载__new__的方法才能起到自定义的作用
class PositiveInteger(int):
    def __new__(cls, value):
        return super(PositiveInteger, cls).__new__(cls, abs(value))
 i = PositiveInteger(-3)

```

new方法可以做很多有趣的事情, 比如我最喜欢用new来实现单例模式

```
因为类每一次实例化后产生的过程都是通过__new__来控制的，所以通过重载__new__方法，我们 可以很简单的实现单例模式
class ChromeDriver(object):
    _instance = None
    def __new__(cls, *args, **kw):
        if not cls._instance:
            cls._instance = super(ChromeDriver, cls).__new__(cls, *args, **kw)
        return cls._instance
 这是我在爬虫中间件中加的一个chromedrive 中间件, 实现了单例模式, 因为如果不用单例我开多并发的话可能会导致实例很多浏览器, 造成服务器压力过大(因为浏览器很吃内存), 实现单例模式就可以避免这个问题, 只会实例一个浏览器来进行页面请求.
```

### 单例模式

```
单例模式（Singleton Pattern）是一种常用的软件设计模式，该模式的主要目的是确保某一个类只有一个实例存在。当你希望在整个系统中，某个类只能出现一个实例时，单例对象就能派上用场。
具体的python实现单例模式的几种方法可以参考下面博客:
	https://www.cnblogs.com/huchong/p/8244279.html
不过, 我感觉应该用__new__来实现单例模式应该是比较简单的一种了
```

## 比较

```
1  执行顺序  __new__, __init__, __call__

2  __new__在创建一个实例的过程中必定会被调用,但__init__就不一定, __new__()决定是否要使用该__init__()方法，因为__new__()可以调用其他类的构造方法或者直接返回别的对象来作为本类 的实例。

3  __new__方法总是需要返回该类的一个实例，而__init__不能返回除了None的任何值。比如下面例子:
    class Doo(object):
        def __init__(self):
            print('aa')
            return None   (TypeError: __init__() should return None, 只能返回None)
```







###参考文档: 

https://www.cnblogs.com/superxuezhazha/p/5793536.html

https://blog.csdn.net/yaokai_assultmaster/article/details/70256621

https://www.cnblogs.com/34fj/p/6358702.html

https://segmentfault.com/a/1190000007256392(这篇对魔术方法介绍的很详细)

    