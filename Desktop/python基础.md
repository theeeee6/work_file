# python基础强化

# 数据类型和变量

python支持多种数据类型，可以把任何数据都抽象成对象，而变量在程序中用来指向这些数据对象，对变量赋值就是把数据和变量给关联起来



## 可变与不可变

ython的可变与不可变是指对象是否可以被修改，即内存中的那块空间是否可以被改变

可变类型：字典，列表，集合

不可变类型：数字，字符串，元组，布尔



## 整数

整数允许数字中间以_分割

10_000_000_000 和 10000000000完全一样

python对整数大小没有限制



## 浮点数

浮点数可以用科学计数法表示

0.000012 可以写成 1.2e-5

1.23 * 10的9次方 就是 1.23e9 或 1.23e8



**整数运算永远精确，浮点数运算可能会有四舍五入的误差**



## 字符串

转义字符串，在" 或 ' 前加\

```
'I\'m \"OK\"!'
```

的转义字符串为

I'm "OK"!

* \n 表示换行

* \t 表示制表

两个\在实际字符串中表示的是一个\

在字符串前加r默认不转义



表示多行

Python允许用`'''...'''`的格式表示多行内容

```py
print('''line1
... line2
... line3''')
line1
line2
line3
```



### 字符编码

* ASCII编码：采用一个字节，包括大小写英文字母，数字和一些符号
* GB2312编码：至少两个字节，用于编码中文

日文韩文都有对应的不同的编码方式



由于这些不同的编码格式，在多语言混合的文本中显示出来会有乱码，因此诞生了Unicode字符集

Unicode编码通常是两个字节



本着节约精神，出现了UTF-8编码，能把一个Unicode字符根据不同的数字大小编码成1-6个字节



在计算机的内存中，统一使用Unicode编码，当需要保存到硬盘或者需要转换为UTF-8编码

![rw-file-utf-8](https://www.liaoxuefeng.com/files/attachments/923923787018816/0)



```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```

第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；

第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。



占位符

| 占位符 | 替换内容     |
| :----- | :----------- |
| %d     | 整数         |
| %f     | 浮点数       |
| %s     | 字符串       |
| %x     | 十六进制整数 |

```
>>> 'Hello, %s' % 'world'
'Hello, world'
>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
'Hi, Michael, you have $1000000.'
```

如果只输出%这个字符，需要使用两个%（%%）进行转义



* format() 传入的参数依次替换字符串内的占位符`{0}`、`{1}`……

```
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
'Hello, 小明, 成绩提升了 17.1%'
```

* f-string

```
>>> r = 2.5
>>> s = 3.14 * r ** 2
>>> print(f'The area of a circle with radius {r} is {s:.2f}')
The area of a circle with radius 2.5 is 19.62
```



str是不可变对象

```
>>> a = 'abc'
>>> a.replace('a', 'A')
'Abc'
>>> a
'abc'
```

可以用一个参数来承接返回值，此时返回的结果发生变化

```
>>> a = 'abc'
>>> b = a.replace('a', 'A')
>>> b
'Abc'
>>> a
'abc'
```



`a`是变量，而`'abc'`才是字符串对象，对象`a`的内容是`'abc'`，但其实是指，`a`本身是一个变量，它指向的对象的内容才是`'abc'`：

```ascii
┌───┐                  ┌───────┐
│ a │─────────────────>│ 'abc' │
└───┘                  └───────┘
```

调用`a.replace('a', 'A')`时，实际上调用方法`replace`是作用在字符串对象`'abc'`上的，而这个方法虽然名字叫`replace`，但却没有改变字符串`'abc'`的内容。

**相反**，`replace`方法创建了一个新字符串`'Abc'`并返回，如果我们用变量`b`指向该新字符串，就容易理解了，变量`a`仍指向原有的字符串`'abc'`，但变量`b`却指向新字符串`'Abc'`了：

```ascii
┌───┐                  ┌───────┐
│ a │─────────────────>│ 'abc' │
└───┘                  └───────┘
┌───┐                  ┌───────┐
│ b │─────────────────>│ 'Abc' │
└───┘                  └───────┘
```

## 





## 布尔值

True or Forse

## 空值

None，不能等效于0



## 变量和常量

### 变量

此处引入静态语言和动态语言

java是静态语言（带int、string等）不能随意改变变量类型，即变量本身类型固定

python是动态语言，变量本身类型不固定

### 常量

一个/的除法计算结果为浮点数，即使是两个整数恰好整除，结果也是浮点数

两个除法符号的计算结果为整数，向下舍去余数



## tuple

tuple一旦初始化就不能修改

tuple所谓的不变是指向不变

```
>>> t = ('a', 'b', ['A', 'B'])
>>> t[2][0] = 'X'
>>> t[2][1] = 'Y'
>>> t
('a', 'b', ['X', 'Y'])
```

在这段代码中，指向的list没变，list可以改变，因为list是可变的



```
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
d['Michael'] = 96
print(e)
({'Michael': 96, 'Bob': 75, 'Tracy': 85},)
```

dict也可以改变



当元组中只含有一个元素时，必须要在元素之后添加一个逗号

```
a = (1)
print(type(a))
b= (1,)
print(type(b))
c= (1,2)
print(type(c))
```

原因：括号`()`既可以表示tuple，又可以表示数学公式中的小括号，这就产生了歧义；因此，Python规定，这种情况下，按小括号进行计算，计算结果是`1`，不是元组

所以，只有1个元素的tuple定义时必须加一个逗号`,`，来消除歧义



## dict

python内置了字典，在其他语言中称为map，使用key-value存储

```
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95
>>> d.get('Michael')
```



删除key时，使用pop(key)方法，对应的**value**也会被删除



dict vs list

|          | list | dict |
| -------- | ---- | ---- |
| 速度     | 慢   | 快   |
| 占用内存 | 小   | 大   |

原因解释：dict的实现原理和查字典是一样的。先在字典的索引表里（比如部首表）查这个字对应的页码，然后直接翻到该页，找到这个字。无论找哪个字，这种查找速度都非常快，不会随着字典大小的增加而变慢。

list的实现原理：假设字典包含了1万个汉字，我们要查某一个字，一个办法是把字典从第一页往后翻，直到找到我们想要的字为止，这种方法就是在list中查找元素的方法，list越大，查找越慢。



字典的key必须是不可变的



## set

重复元素在set中自动被过滤

```
>>> s = set([1, 1, 2, 2, 3, 3])
>>> s
{1, 2, 3}
```

s.add()可以增加

s.remove()可以删除



两个set可以做数学意义上的交集、并集等操作

```
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2
{2, 3}
>>> s1 | s2
{1, 2, 3, 4}
```



**set与dict的唯一区别仅在于没有存储对应的key**，特别注意：set是无序的



## list

```
list1 = [1,2,3,4]
```

array是numpy.array()

二者不是同一个东西



Python内置的`enumerate`函数可以把一个`list`变成索引-元素对，这样就可以在`for`循环中同时迭代索引和元素本身：

```
>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
...
0 A
1 B
2 C
```





## 函数

如果想定义一个什么事也不做的空函数，可以用`pass`语句：

```
def nop():
    pass
```

**pass什么都不做，用来做占位符**

在空函数中缺少了pass代码运行就会有语法错误



返回多个值其实上是一个tuple



默认参数：在函数声明时直接进行写入：age=6等等



默认参数的大坑

```
>>> add_end()
['END']
>>> add_end()
['END', 'END']
>>> add_end()
['END', 'END', 'END']
```

Python函数在定义的时候，默认参数`L`的值就被计算出来了，即`[]`，**因为默认参数`L`也是一个变量**，它指向对象`[]`，每次调用该函数，如果改变了`L`的内容，则下次调用时，默认参数的内容就变了，不再是函数定义时的`[]`了。即：

**默认参数指向不变对象**



修改大坑的例子（None是不变对象）

不变对象一旦创建，对象内部的数据就不能修改

```
def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L
```

```
>>> add_end()
['END']
>>> add_end()
['END']
```



函数变量的✳️与✳️✳️

一个✳️

将函数的参数定义为可变参数（参数个数可变），**这个参数会把传入的所有参数打包成一个元组**

不可变参数直接进行声明

```
def test(a):
    for i in a:
        print(i)
test(1,2,3,4,5)
会报错
```

使用一个星号后，可以通过编译

```
def test(*a):
    for i in a:
        print(i)
test(1,2,3,4,5)
```

加深理解：

```
def test(*a):
    print(a)
    for i in a:
        print(i)
test([1,2,3,4,5])
运行结果为：
([1, 2, 3, 4, 5],)
[1, 2, 3, 4, 5]
```

修改之后

```
def test(*a):
    print(a)
    for i in a:
        print(i)
test(*[1,2,3,4,5])
运行结果为：
(1, 2, 3, 4, 5)
1
2
3
4
5
```

两个✳️，关键字参数，表示传入的参数是一个字典

关键字参数允许传入0个或任意个**含参数名**的参数，这些关键字参数在函数内部自动组装为一个dict，参数名是key，参数值是value



多余的参数必须是key-value的类型，否则会报错



将多余的参数打包为字典

```
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
```

```
>>> person('Michael', 30)
name: Michael age: 30 other: {}
```

```
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
```



命名关键字参数

如果要限制关键字参数的名字，就可以用命名关键字参数，例如，只接收`city`和`job`作为关键字参数。这种方式定义的函数如下：

```
def person(name, age, *, city, job):
    print(name, age, city, job)
```

和关键字参数`**kw`不同，命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数。



如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符`*`了：

```
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```

city和job为命名关键字参数



在*号之后，有默认值的参数可以不传入



参数组合

```
def f1(a, b, c=0, *args, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)
```

```
>>> f1(1, 2, 3, 'a', 'b', x=99)
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {'x': 99}
>>> f2(1, 2, d=99, ext=None)
a = 1 b = 2 c = 0 d = 99 kw = {'ext': None}
```



函数返回函数

```
def lazy_sum(*args):
    def sum():
        ax = 0
        for n in args:
            ax = ax + n
        return ax
    return sum
```

```
>>> f = lazy_sum(1, 3, 5, 7, 9)
>>> f
<function lazy_sum.<locals>.sum at 0x101c6ed90>
>>> f()
25
```



# 生成器

一边循环一边计算，生成器保存的是算法

根据算法按需进行计算，节省空间



如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator函数，调用一个generator函数将返回一个generator：

普通函数是顺序执行，遇到`return`语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用`next()`的时候执行，遇到`yield`语句返回，再次执行时**从上次返回的`yield`语句处继续执行**。



# 迭代器

生成器都是`Iterator`对象

`list`、`dict`、`str`虽然是`Iterable`，却不是`Iterator`。

把`list`、`dict`、`str`等`Iterable`变成`Iterator`可以使用`iter()`函数：

```
>>> isinstance(iter([]), Iterator)
True
>>> isinstance(iter('abc'), Iterator)
True
```

Python的`Iterator`对象表示的是一个数据流，Iterator对象可以被`next()`函数调用并不断返回下一个数据，直到没有数据时抛出`StopIteration`错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过`next()`函数实现按需计算下一个数据，所以`Iterator`的计算是惰性的，只有在需要返回下一个数据时它才会计算。



凡是可作用于`for`循环的对象都是`Iterable`类型；

凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；

集合数据类型如`list`、`dict`、`str`等是`Iterable`但不是`Iterator`，不过可以通过`iter()`函数获得一个`Iterator`对象。

Python的`for`循环本质上就是通过不断调用`next()`函数实现的，例如：

```
for x in [1, 2, 3, 4, 5]:
    pass
```

实际上完全等价于：

```
# 首先获得Iterator对象:
it = iter([1, 2, 3, 4, 5])
# 循环:
while True:
    try:
        # 获得下一个值:
        x = next(it)
    except StopIteration:
        # 遇到StopIteration就退出循环
        break
```



# 装饰器

装饰器就是一个返回函数的高阶函数

一层嵌套、两层嵌套、三层嵌套

一层嵌套的装饰器

直接放函数

```
def log(func):
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper
```

```
@log
def now():
    print('2015-3-25')
```

```
>>> now()
call now():
2015-3-25
```



两层嵌套的装饰器

```
def log(text):
    def decorator(func):
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```

第一层放文本，第二层放函数

```
@log('execute')
def now():
    print('2015-3-25')
```

```
>>> now()
execute now():
2015-3-25
```



# 偏函数

简化函数参数

```
>>> import functools
>>> int2 = functools.partial(int, base=2)
>>> int2('1000000')
64
>>> int2('1010101')
85
```

# 模块

在Python中，一个.py文件就称之为一个模块（Module）

模块是一组Python代码的集合

含有`__init__.py`的文件的文件夹可以理解为一个包

每个包目录下都有一个`__init__.py`的文件，这个文件是必须存在的，否则，Python就把这个目录当成普通目录，而不是一个包。



# 命令行加参数运行python文件

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

' a test module '

__author__ = 'Michael Liao'

import sys

def test():
    args = sys.argv
    if len(args)==1:
        print('Hello, world!')
    elif len(args)==2:
        print('Hello, %s!' % args[1])
    else:
        print('Too many arguments!')

if __name__=='__main__':
    test()
```

```
$ python3 hello.py
Hello, world!
$ python hello.py Michael
Hello, Michael!
```



# 面向对象

```
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score

    def print_score(self):
        print('%s: %s' % (self.name, self.score))
```

```
bart = Student('Bart Simpson', 65)
lisa = Student('Lisa Simpson', 87)
bart.print_score()
lisa.print_score()
```

面向对象的设计思想是抽象出Class，根据Class创建Instance。

面向对象的三大特点：数据封装，继承和多态

## 封装

private

类似`__xxx`和`___xxx`这样的函数或变量就是非公开的（private），不应该被直接引用

这种方法出现的原因是：Python并没有一种方法可以完全限制访问private函数或变量，但是，从编程习惯上不应该引用private函数或变量。

变量名前出现两个及以上的`_`表示其为私有变量



如果要让内部属性不被外部属性访问，可以把属性的名称前加上几个下划线



在Python中，变量名类似`__xxx__`的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量



以一个下划线开头的实例变量名，比如`_name`，这样的实例变量外部是可以访问的，但是建议不要直接访问，通过类的公共接口来访问



## 继承

```
class Animal(object):
    def run(self):
        print('Animal is running...')
```

编写`Dog`和`Cat`类时，就可以直接从`Animal`类继承：

```
class Dog(Animal):
    pass

class Cat(Animal):
    pass
```

对于`Dog`来说，`Animal`就是它的父类，对于`Animal`来说，`Dog`就是它的子类。`Cat`和`Dog`类似。



`Dog`可以看成`Animal`，但`Animal`不可以看成`Dog`。



### 多重继承

```
class Bat(Mammal, Flyable):
    pass
```

通过多重继承，一个子类可以同时获得多个父类的所有功能



Mixin

Mixin是一种设计思想，给好多类名字中加上Mixin，表示其扮演父类角色，允许继承和使用





# __slots__

Python允许在定义class的时候，定义一个特殊的`__slots__`变量，来限制该class实例能添加的属性

```
class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
```

```
>>> s = Student() # 创建新的实例
>>> s.name = 'Michael' # 绑定属性'name'
>>> s.age = 25 # 绑定属性'age'
>>> s.score = 99 # 绑定属性'score'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Student' object has no attribute 'score'
```

子类实例允许定义的属性就是自身的`__slots__`加上父类的`__slots__`



Python内置的`@property`装饰器就是负责把一个方法变成属性调用的：



# @property

python内置的@property装饰器负责把一个方法变成属性调用

**把类里的方法伪装成属性**



```
class Rectangle:
	def __init__(self, length, width)
		self.length = length
		sele.width = width
		self.area = length * width 
```

这样的代码会有一个问题：area属性被暴露出来

可以直接通过

```
rectangle = Rectangle(5,2)
rectangle.area = 20
```

来对area进行修改



解决方法一（不建议）：

将属性转换为函数

```
def get_area(self):
	return self.length * self.width
```

方法可行，但是需要将代码中所有的rectangle.area 修改为 rectangle.get_area()



解决方法二：@property

```
@property
def area(self)
	return self.length * self.width
```

像使用属性一样去使用这个方法

通过rectangle.area可以直接调用area()这个函数





setter和getter方法

```
@property
def name(self):
	return self._name

@name.setter
def name(self, name)
	self._name = name
```

执行book.name = '123'

实际上执行的是def name(self, name)



# 定制类

在python中看到`__xxx__`的变量或者函数名就要注意，这些在Python中有特殊用途



# 枚举类

```
from enum import Enum
Month = Enum('Month', ('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'))
for name, member in Month.__members__.items():
    print(name, '=>', member, ',', member.value)
```

运行结果：

```
Jan => Month.Jan , 1
Feb => Month.Feb , 2
Mar => Month.Mar , 3
Apr => Month.Apr , 4
May => Month.May , 5
Jun => Month.Jun , 6
Jul => Month.Jul , 7
Aug => Month.Aug , 8
Sep => Month.Sep , 9
Oct => Month.Oct , 10
Nov => Month.Nov , 11
Dec => Month.Dec , 12
```



`value`属性则是自动赋给成员的`int`常量，默认从`1`开始计数。



`@unique`装饰器可以帮助检查保证没有重复值。



# type()

动态语言和静态语言最大的不同是函数和类的定义不是编译时定义的，而是**运行时动态创建的**



# 序列化

程序运行的过程中，所有的变量都是在内存中，一旦程序结束，变量所占用的内存就被操作系统全部回收

把变量从内存中变成可存储或传输的过程称之为序列化

Python中叫pickling，在其他语言中也被称之为serialization，marshalling，flattening等等



# 多进程

```
import os

print('Process (%s) start...' % os.getpid())
# Only works on Unix/Linux/Mac:
pid = os.fork()
if pid == 0:
    print('I am child process (%s) and my parent is %s.' % (os.getpid(), os.getppid()))
else:
    print('I (%s) just created a child process (%s).' % (os.getpid(), pid))
```



运行结果

```
Process (2792) start...
I (2792) just created a child process (2793).
I am child process (2793) and my parent is 2792.
```



使用multiprocessing库

`join` 用来阻塞主进程

```
from multiprocessing import Process
import os
import time

def now():
    return str(time.strftime('%Y-%m-%d %H:%M:%S', time.localtime()))


def func_1(name):
    print(now() + ' Run child process %s (%s)...' % (name, os.getpid()))
    time.sleep(4)
    print(now() + ' Stop child process %s (%s)...\n' % (name, os.getpid()))


def func_2(name):
    print(now() + ' Run child process %s (%s)...' % (name, os.getpid()))
    time.sleep(8)
    print(now() + ' hello world!')
    print(now() + ' Stop child process %s (%s)...\n' % (name, os.getpid()))


if __name__ == '__main__':
    print ('Parent process %s.' % os.getpid())
    p1 = Process(target=func_1, args=('func_1',))
    p2 = Process(target=func_2, args=('func_2',))
    print now() + ' Process start.'
    p1.start()
    p2.start()
    p1.join()
    p2.join()
    print now() + ' Process end .'
```



运行结果

```
Parent process 5711.
2023-04-28 11:31:24 Process start.
2023-04-28 11:31:24 Run child process func_1 (5713)...
2023-04-28 11:31:24 Run child process func_2 (5714)...
2023-04-28 11:31:28 Stop child process func_1 (5713)...

2023-04-28 11:31:32 hello world!
2023-04-28 11:31:32 Stop child process func_2 (5714)...

2023-04-28 11:31:32 Process end .
```





# 多线程

多任务可以由多进程完成，也可以由一个进程内的多线程完成，一个进程至少有一个线程。

多线程和多进程最大的不同在于，多进程中，同一个变量，各自有一份拷贝存在于每个进程中，互不影响，而多线程中，所有变量都由所有线程共享，所以，任何一个变量都可以被任何一个线程修改，因此，线程之间共享数据最大的危险在于多个线程同时改一个变量，把内容给改乱了。

解决冲突的方法：创建一个锁：通过`threading.Lock()`来实现

```
balance = 0
lock = threading.Lock()

def run_thread(n):
    for i in range(100000):
        # 先要获取锁:
        lock.acquire()
        try:
            # 放心地改吧:
            change_it(n)
        finally:
            # 改完了一定要释放锁:
            lock.release()
```

当多个线程同时执行`lock.acquire()`时，只有一个线程能成功地获取锁，然后继续执行代码，其他线程就继续等待直到获得锁为止。

获得锁的线程用完后一定要释放锁，否则那些苦苦等待锁的线程将永远等待下去，成为死线程。所以我们用`try...finally`来确保锁一定会被释放。



Python的线程虽然是真正的线程，但解释器执行代码时，有一个GIL锁：Global Interpreter Lock

任何Python线程执行前，必须先获得GIL锁

每执行100条字节码，解释器就自动释放GIL锁，让别的线程有机会执行

这个GIL全局锁实际上把所有线程的执行代码都给上了锁，所以，多线程在Python中只能交替执行，即使100个线程跑在100核CPU上，也只能用到1个核。

如果一定要通过多线程利用多核，那只能通过C扩展来实现

Python虽然不能利用多线程实现多核任务，但可以通过多进程实现多核任务。多个Python进程有各自独立的GIL锁，互不影响。



# 协程

单线程的异步编程模型称为协程

在Python中，协程通过`asyncio`库来实现

协程可以使用`async def`定义，并在其中使用`await`关键字来等待其他协程或异步操作的完成。

```
import asyncio

async def hello():
    print("Hello")
    await asyncio.sleep(1)
    print("World")

async def main():
    await asyncio.gather(hello(), hello(), hello())

asyncio.run(main())
```

