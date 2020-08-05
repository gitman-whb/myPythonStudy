# 类与对象

## 1. 对象 = 属性 + 方法

对象是类的实例。换句话说，类主要定义对象的结构，然后我们以类为模板创建对象。类不但包含方法定义，而且还包含所有实例共享的数据。

【一个简单类】（换汤不换药：类内的变量和函数==属性和方法）

```python
class Turtle:  # Python中的类名约定以大写字母开头
 
    # 属性
    color = 'green'
    weight = 10
    legs = 4
    shell = True
    mouth = '大嘴'

    # 方法
    def climb(self):
        print('我正在很努力的向前爬...')
    def run(self):
        print('我正在飞快的向前跑...')
    def bite(self):
        print('咬死你咬死你!!')
    def eat(self):
        print('有得吃，真满足...')
    def sleep(self):
        print('困了，睡了，晚安，zzz')

tt = Turtle()#声明一个对象时要带括号

print(tt)
# <__main__.Turtle object at 0x0000007C32D67F98>

print(type(tt))
# <class '__main__.Turtle'>#__main__代表当前模块是直接运行而不是被导入

print(tt.__class__)#__class__跟type()一样，都是查看对象所在的类
# <class '__main__.Turtle'>

print(tt.__class__.__name__)#获取类名
# Turtle

tt.climb()
# 我正在很努力的向前爬...
tt.run()
# 我正在飞快的向前跑...
tt.bite()
# 咬死你咬死你!!

# Python类也是对象。它们是type的实例
print(type(Turtle))
# <class 'type'>
```

- 继承：子类自动共享父类之间数据和方法的机制

【例子】

```python
class MyList(list):
    pass

lst = MyList([1, 5, 2, 7, 8])
lst.append(9)
lst.sort()
print(lst)
# [1, 2, 5, 7, 8, 9]
```

- 多态：不同对象对同一方法响应不同的行动

【例子】

```python
class Animal:
    def run(self):
        raise AttributeError('子类必须实现这个方法')
        
class People(Animal):
    def run(self):
        print('人正在走')
        
class Pig(Animal):
    def run(self):
        print('pig is walking')
        
class Dog(Animal):
    def run(self):
        print('dog is running')

def func(animal):
    animal.run()

func(Pig())
# pig is walking
```

## 2. self 是什么？

Python 的 `self` 相当于 C++ 的 `this` 指针。

类的方法与普通的函数只有一个特别的区别 ：它们**必须**有一个额外的第一个参数名称（默认是该对象本身即self）

```python
class Ball:
    def setName(self, name):#必须要有self
        self.name = name
    def kick(self):#必须要有self
        print("我叫%s,该死的，谁踢我..." % self.name)

a = Ball()
a.setName("球A")
b = Ball()
b.setName("球B")
c = Ball()
c.setName("球C")
a.kick()
# 我叫球A,该死的，谁踢我...
b.kick()
# 我叫球B,该死的，谁踢我...
```

## 4. 公有和私有

在 Python 中定义私有变量只需要在变量名或函数名前加上**“__”两个下划线**，那么这个函数或变量就会为私有的了。

【例子】类的私有属性实例

```python
class JustCounter:
    __secretCount = 0  # 私有变量
    publicCount = 0  # 公有变量

    def count(self):
        self.__secretCount += 1
        self.publicCount += 1
        print(self.__secretCount)


counter = JustCounter()
counter.count()  # 1
counter.count()  # 2#私有变量只能类内部引用

print(counter.publicCount)  # 2
print(counter._JustCounter__secretCount)  # 2 Python的私有为伪私有
print(counter.__secretCount)  #私有变量不能外部直接引用
# AttributeError: 'JustCounter' object has no attribute '__secretCount'
```

【例子】类的私有方法实例

__ init __方法使用与功能：

1.   用来构造初始化函数,用来给类的实例进行初始化属性，所以可以不需要返回值
2.   在创建类的实例时系统自动调用
3.   自定义类如果不定义的话，默认调用父类object的，同理继承也是，子类若无，调用父类，若有，调用自己的

```python
class Site:
    def __init__(self, name, url):
        self.name = name  # 公有变量
        self.__url = url  # 私有变量

    def who(self):
        print('name  : ', self.name)
        print('url : ', self.__url)

    def __foo(self):  # 私有方法
        print('这是私有方法')

    def foo(self):  # 公共方法
        print('这是公有方法')
        self.__foo()


x = Site('我的python之旅', 'https://github.com/gitman-whb/myPythonStudy')
x.who()
#name  :  我的python之旅
#url :  https://github.com/gitman-whb/myPythonStudy

x.foo()
# 这是公有方法
# 这是私有方法

x.__foo()#不能直接在外部调用私有方法
# AttributeError: 'Site' object has no attribute '__foo'
```

## 5. 继承

Python 同样支持类的继承，派生类的定义如下所示：

```python
#BaseClassName（示例中的基类名）与派生类定义在一个作用域内
class DerivedClassName(BaseClassName):
    <statement-1>
    .
    .
    .
    <statement-N>
# 基类定义在另一个模块中时   
 class DerivedClassName(modname.BaseClassName):
    <statement-1>
    .
    .
    .
    <statement-N>
```

【单继承例子】如果子类中定义与父类同名的方法或属性，则会自动覆盖父类对应的方法或属性。

```python
# 类定义
class People:
    # 定义基本属性
    name = ''
    age = 0
    # 定义私有属性,私有属性在类外部无法直接进行访问
    __weight = 0

    # 定义构造方法
    def __init__(self, n, a, w):
        self.name = n
        self.age = a
        self.__weight = w

    def speak(self):
        print("%s 说: 我 %d 岁。" % (self.name, self.age))


# 单继承示例
class Student(People):
    grade = ''

    def __init__(self, n, a, w, g):
        # 调用父类的构函,不调用就会覆盖（因为两个函数同名）
        People.__init__(self, n, a, w)
        self.grade = g

    # 覆写父类的方法
    def speak(self):
        print("%s 说: 我 %d 岁了，我在读 %d 年级" % (self.name, self.age, self.grade))


s = Student('小马', 10, 60, 3)
s.speak()
# 小马 说: 我 10 岁了，我在读 3 年级
```

注意：如果上面的程序去掉：`People.__init__(self, n, a, w)`，则输出：

` 说: 我 0 岁了，我在读 3 年级`

因为子类的构造方法把父类的构造方法覆盖了。

【多继承例子】Python 虽然支持多继承的形式，但我们一般不使用多继承，因为容易引起混乱。

```python
# 另一个类，多重继承之前的准备
class Speaker:
    topic = ''
    name = ''

    def __init__(self, n, t):
        self.name = n
        self.topic = t

    def speak(self):
        print("我叫 %s，我是一个演说家，我演讲的主题是 %s" % (self.name, self.topic))


# 多重继承
class Sample01(Speaker, Student):
    a = ''

    def __init__(self, n, a, w, g, t):
        Student.__init__(self, n, a, w, g)
        Speaker.__init__(self, n, t)

# 方法名同，默认调用的是在括号中排前面父类(Speaker)的方法
test = Sample01("Tim", 25, 80, 4, "Python")
test.speak()  
# 我叫 Tim，我是一个演说家，我演讲的主题是 Python

class Sample02(Student, Speaker):
    a = ''

    def __init__(self, n, a, w, g, t):
        Student.__init__(self, n, a, w, g)
        Speaker.__init__(self, n, t)

# 方法名同，默认调用的是在括号中排前面父类(Student)的方法
test = Sample02("Tim", 25, 80, 4, "Python")
test.speak()  
# Tim 说: 我 25 岁了，我在读 4 年级
```

## 6. 组合

【例子】这与继承不同

```python
class Turtle:
    def __init__(self, x):
        self.num = x


class Fish:
    def __init__(self, x):
        self.num = x


class Pool:
    def __init__(self, x, y):
        self.turtle = Turtle(x)
        self.fish = Fish(y)

    def print_num(self):
        print("水池里面有乌龟%s只，小鱼%s条" % (self.turtle.num, self.fish.num))


p = Pool(2, 3)
p.print_num()
# 水池里面有乌龟2只，小鱼3条
```

## 7. 类、类对象和实例对象

[![类对象和实例对象](https://camo.githubusercontent.com/48b47c3cb3792358534e773eb02c630b209ca779/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139313030373039303331363436322e706e67)](https://camo.githubusercontent.com/48b47c3cb3792358534e773eb02c630b209ca779/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139313030373039303331363436322e706e67)

类对象：创建一个类，其实也是一个对象也在内存开辟了一块空间，称为类对象，类对象只有一个。

实例对象：就是通过实例化类创建的对象，称为实例对象，实例对象可以有多个。

类属性：**类里面、方法外面**定义的变量称为类属性。类属性所属于**类对象**并且**多个实例对象之间共享**同一个类属性，说白了就是类属性所有的通过该类实例化的对象都能共享。

实例属性：定义在在**方法里面**或者**类外面**，实例属性和具体的某个实例对象有关系，并且一个实例对象和另外一个实例对象是不共享属性的，说白了实例属性只能在自己的对象里面使用，其他的对象不能直接使用，因为`self`是谁调用，它的值就属于该对象。

```python
# 类对象
class C(object):
    pass

# 实例化对象 a、b、c都属于实例对象。
a = C()
b = C()
c = C()

class A():
    a = 0  # 类属性
    def __init__(self, xx):
        # 使用类属性可以不用self,直接通过 【类名.类属性】调用。
        A.a = xx
        
class 类名():
    def __init__(self)：
        self.name = xx #【self.实例属性】
```

类属性和实例属性区别

- 类属性：类外面，可以通过【`实例对象.类属性`】和【`类名.类属性`】进行调用。类里面，通过【`self.类属性`】和【`类名.类属性`】进行调用。
- 实例属性 ：类外面，可以通过【`实例对象.实例属性`】调用。类里面，通过【`self.实例属性`】调用。
- 实例属性就相当于局部变量。出了这个类或者这个类的实例对象，就没有作用了。
- 类属性就相当于类里面的全局变量，可以和这个类的所有实例对象共享。

【例子】

```python
# 创建类对象
class Test(object):
    class_attr = 100  # 类属性

    def __init__(self):
        self.sl_attr = 100  # 实例属性

    def func(self):
        print('类对象.类属性的值:', Test.class_attr)  # 调用类属性
        print('self.类属性的值', self.class_attr)  # 相当于把类属性 变成实例属性
        print('self.实例属性的值', self.sl_attr)  # 调用实例属性


a = Test()
a.func()

# 类对象.类属性的值: 100
# self.类属性的值 100
# self.实例属性的值 100

b = Test()
b.func()

# 类对象.类属性的值: 100
# self.类属性的值 100
# self.实例属性的值 100

a.class_attr = 200#通过实例去修改类属性：会产生一个同名的实例属性，不会影响到类属性，且这个实例属性会强制屏蔽掉类属性
a.sl_attr = 200
a.func()

# 类对象.类属性的值: 100
# self.类属性的值 200
# self.实例属性的值 200

b.func()

# 类对象.类属性的值: 100
# self.类属性的值 100
# self.实例属性的值 100

Test.class_attr = 300#类对象去修改类属性才是真正的修改
a.func()

# 类对象.类属性的值: 300
# self.类属性的值 200
# self.实例属性的值 200

b.func()
# 类对象.类属性的值: 300
# self.类属性的值 300
# self.实例属性的值 100
```

如果需要在**类外修改类属性，必须通过类对象去引用然后进行修改**。如果通过实例对象去引用，会产生一个同名的`实例属性`，这种方式修改的是`实例属性`，不会影响到`类属性`，并且之后如果通过实例对象去引用该名称的属性，**实例属性会强制屏蔽掉类属性**，即引用的是`实例属性`，除非删除了该`实例属性`。

```python
class People(object):
    country = 'china'  # 类属性

print(People.country)   #china
p = People()
print(p.country)    #china
p.country = 'japan'
print(p.country)  # 实例属性会屏蔽掉同名的类属性：japan
print(People.country)   #china
del p.country  # 删除实例属性
print(p.country)    #实例属性被删除后，再调用同名称的属性，会调用类属性：china
```

## 8. 什么是绑定？

Python 严格要求方法需要有实例才能被调用，这种限制其实就是 Python 所谓的绑定概念。

Python 对象的数据属性通常存储在名为`__ dict__`的字典中，我们可以直接访问`.__dict__`，或利用 Python 的内置函数`vars()`获取`.__ dict__`。

```python
class CC:
    def setXY(self, x, y):
        self.x = x
        self.y = y

    def printXY(self):
        print(self.x, self.y)


dd = CC()
print(dd.__dict__)
# {}

print(vars(dd))
# {}

print(CC.__dict__)
# {'__module__': '__main__', 'setXY': <function CC.setXY at 0x000000C3473DA048>, 'printXY': <function CC.printXY at 0x000000C3473C4F28>, '__dict__': <attribute '__dict__' of 'CC' objects>, '__weakref__': <attribute '__weakref__' of 'CC' objects>, '__doc__': None}

dd.setXY(4, 5)
print(dd.__dict__)
# {'x': 4, 'y': 5}

print(vars(CC))
# {'__module__': '__main__', 'setXY': <function CC.setXY at 0x000000632CA9B048>, 'printXY': <function CC.printXY at 0x000000632CA83048>, '__dict__': <attribute '__dict__' of 'CC' objects>, '__weakref__': <attribute '__weakref__' of 'CC' objects>, '__doc__': None}

print(CC.__dict__)
# {'__module__': '__main__', 'setXY': <function CC.setXY at 0x000000632CA9B048>, 'printXY': <function CC.printXY at 0x000000632CA83048>, '__dict__': <attribute '__dict__' of 'CC' objects>, '__weakref__': <attribute '__weakref__' of 'CC' objects>, '__doc__': None}
```

## 9. 一些相关的内置函数（BIF）

- `issubclass(class, classinfo)` 方法用于判断参数 class 是否是类型参数 classinfo 的子类。
- 一个类被认为是其自身的子类。
- `classinfo`可以是类对象的元组，只要class是其中**任何一个候选类**的子类，则返回`True`。

【例子】

```python
class A:
    pass
class B(A):
    pass


print(issubclass(B, A))  # True
print(issubclass(B, B))  # True
print(issubclass(A, B))  # False
print(issubclass(B, object))  # True
```

- `isinstance(object, classinfo)` 方法用于判断一个对象是否是一个已知的类型，类似`type()`。
- `type()`不会认为子类是一种父类类型，不考虑继承关系。
- `isinstance()`会认为子类是一种父类类型，考虑继承关系。
- 如果第一个参数不是对象，则永远返回`False`。
- 如果第二个参数不是类或者由类对象组成的元组，会抛出一个`TypeError`异常。

【例子】

```python
a = 2
print(isinstance(a, int))  # True
print(isinstance(a, str))  # False
print(isinstance(a, (str, int, list)))  # True


class A:
    pass
class B(A):
    pass
print(isinstance(A(), A))  # True
print(type(A()) == A)  # True
print(isinstance(B(), A))  # True
print(type(B()) == A)  # False
```

- `hasattr(object, name)`用于判断对象是否包含对应的属性。

【例子】

```python
class Coordinate:
    x = 10
    y = -5
    z = 0


point1 = Coordinate()
print(hasattr(point1, 'x'))  # True
print(hasattr(point1, 'y'))  # True
print(hasattr(point1, 'z'))  # True
print(hasattr(point1, 'no'))  # False
```

- `getattr(object, name[, default])`用于返回一个对象属性值。

【例子】

```python
class A(object):
    bar = 1


a = A()
print(getattr(a, 'bar'))  # 1
print(getattr(a, 'bar2', 3))  # 3
print(getattr(a, 'bar2'))
# AttributeError: 'A' object has no attribute 'bar2'
```

* `delattr(object, name)`用于删除属性。`delattr(object, name)`用于删除属性。

**练习题**：

1、以下类定义中哪些是类属性，哪些是实例属性？

```python
class C:
    num = 0#类属性
    def __init__(self):
        self.x = 4#实例属性
        self.y = 5#实例属性
        C.count = 6#实例属性
```

2、怎么定义私有⽅法？

在变量名或函数名前加上**“__”两个下划线**

扩展：

 1、 `_xx` 以单下划线开头的表示的是protected类型的变量。即保护类型只能允许其本身与子类进行访问。若内部变量标示，如： 当使用“from M import”时，不会将以一个下划线开头的对象引入 。

 2、 `__xx` 双下划线的表示的是私有类型的变量。只能允许这个类本身进行访问了，连子类也不可以用于命名一个类属性（类变量），调用时名字被改变（在类FooBar内部，`__boo`变成`_FooBar__boo`,如`self._FooBar__boo`）

3、` __xx__`定义的是特列方法。用户控制的命名空间内的变量或是属性，如`__init__ `, `__import__`或是`__file __`。只有当文档有说明时使用，不要自己定义这类变量。 （就是说这些是python内部定义的变量名）

【Python内置类属性】:

` __dict__` : 类的属性（包含一个字典，由类的数据属性组成） 

`__doc__ `:类的文档字符串

` __module__`: 类定义所在的模块（类的全名是`__main__.className`，如果类位于一个导入模块mymod中，那么className.`__module__ `等于 mymod）

` __bases__ `: 类的所有父类构成元素（包含了一个由所有父类组成的元组）

3、尝试执行以下代码，并解释错误原因：

```python
class C:
    def myFun():
        print('Hello!')
    c = C()
    c.myFun()
############################
#首先由于关于c最后两行代码没有缩进，使得python的判断c=C( )为定义类C的一部分，其次没有在定义方法时注明self（方法的自身，但不需参数引入），导致错误。
class C:
    def myFun(self):
        print('Hello!')
c = C()
c.myFun()
#Hello!
```

4、按照以下要求定义一个游乐园门票的类，并尝试计算2个成人+1个小孩平日票价。

要求:

- 平日票价100元
- 周末票价为平日的120%
- 儿童票半价

```python
class Ticket():
    # your code here

class Ticket():
   
    def  __init__(self,day,m,n):
        p=100 * m + 50 * n
        if day>=1 and day<=5:
            self.day="非周末"
            self.adultnum=m
            self.kidnum=n
            self.price= p
        else:
            self.day="周末"
            self.price=1.2 * p
            
    def pri(self):
        print(self.day)
        print("总票价为 %d" % self.price)

bill=Ticket(2,2,1)
bill.pri( )
#非周末
#总票价为 250   
```