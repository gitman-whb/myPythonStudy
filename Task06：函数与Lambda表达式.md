# 函数与Lambda表达式

## 1. 函数

 Python 里面“万物皆对象”！Python 把函数也当成对象，可以从另一个函数中返回出来而去构建高阶函数，比如：

- 参数是函数

- 返回值是函数

### 函数的定义

- 函数以`def`关键词开头，后接函数名和圆括号()。
- 函数执行的代码以冒号起始，并且缩进。
- return [表达式] 结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回`None`。

```python
#函数定义
def functionname(parameters):
    "函数_文档字符串"
    function_suite
    return [expression]
#例子
def MyFirstFunction(name):
    "这是本函数说明字符串"            
    print('传递进来的{0}叫做实参，因为Ta是具体的参数值！'.format(name))
    
MyFirstFunction('我的python之旅')  
# 传递进来的我的python之旅叫做实参，因为Ta是具体的参数值！

print(MyFirstFunction.__doc__)  
# 这是本函数说明字符串

help(MyFirstFunction)
# Help on function MyFirstFunction in module __main__:
# MyFirstFunction(name)
#    这是本函数说明字符串
```

### 函数参数

**1. 位置参数**

```python
def functionname(arg1, arg2):
    "函数_文档字符串"
    function_suite
    return [expression]
```

- `arg1,arg2` - 位置参数 ，这些参数在调用函数 (call function) 时位置要固定。

- 但是，Python 允许函数调用时参数的顺序与声明时不一致，因为 Python 解释器能够用参数名匹配参数值。

```python
def printinfo(name, age):
    print('Name:{0},Age:{1}'.format(name, age))

printinfo(age=8, name='小马')  # Name:小马,Age:8
```

**2. 默认参数**

```python
def functionname(arg1, arg2=v):
    "函数_文档字符串"
    function_suite
    return [expression]
```

- `arg2 = v` - 默认参数 = 默认值，调用函数时，默认参数的值如果没有传入，则被认为是默认值。
- 默认参数一定要放在位置参数 **后面**，不然程序会报错。

```python
def printinfo(name, age=8):
    print('Name:{0},Age:{1}'.format(name, age))


printinfo('小马')  # Name:小马,Age:8
printinfo('小马', 10)  # Name:小马,Age:10
```

**3. 可变参数**

顾名思义，可变参数就是传入的参数个数是可变的，可以是 0, 1, 2 到任意个，是不定长的参数。

```
def functionname(arg1, arg2=v, *args):
    "函数_文档字符串"
    function_suite
    return [expression]
```

- `*args` - 可变参数，可以是从零个到任意个，自动组装成**元组**。
- 加了星号（*）的变量名会存放所有未命名的变量参数。

```python
def printinfo(arg1, *args):
    print(arg1)
    for var in args:
        print(var,end='********')


printinfo(10)  # 10
printinfo(70, 60, 50)

#70
#60********50********
```

**4. 关键字参数**

```python
def functionname(arg1, arg2=v, *args, **kw):
    "函数_文档字符串"
    function_suite
    return [expression]
```

- `**kw` - 关键字参数，可以是从零个到任意个，自动组装成**字典**。

```python
def printinfo(arg1, *args, **kwargs):
    print(arg1)
    print(args)
    print(kwargs)


printinfo(70, 60, 50)
# 70
# (60, 50)
# {}
printinfo(70, 60, 50, a=1, b=2)
# 70
# (60, 50)
# {'a': 1, 'b': 2}
```

`「可变参数」和「关键字参数」`的同异总结如下：

- 可变参数允许传入零个到任意个参数，它们在函数调用时自动组装为一个元组 (tuple)。
- 关键字参数允许传入零个到任意个参数，它们在函数内部自动组装为一个字典 (dict)。

**5. 命名关键字参数**

```python
def functionname(arg1, arg2=v, *args, *, nkw, **kw):
    "函数_文档字符串"
    function_suite
    return [expression]
```

- 在【关键字参数】基础上，如果要限制关键字参数的名字，就可以用【命名关键字参数】,不过一项只代表一个参数。

- `*, nkw` - 【命名关键字参数】，用户想要输入的关键字参数，定义方式是在nkw 前面加一项分隔符 *。
- 使用时，要特别注意不能缺少参数名。

【例子】

```python
def printinfo(arg1, *, nkw, **kwargs):
    print(arg1)
    print(nkw)
    print(kwargs)


printinfo(70, nkw=10, a=1, b=2)
# 70
# 10
# {'a': 1, 'b': 2}

printinfo(70, 10, a=1, b=2)
# TypeError: printinfo() takes 1 positional argument but 2 were given
```

- 没有写参数名`nwk`，因此 10 被当成「位置参数」，而原函数只有 1 个位置函数，现在调用了 2 个，因此程序会报错。

**6. 参数组合**

- 位置参数 (positional argument)
- 默认参数 (default argument)
- 可变参数 (variable argument)
- 关键字参数 (keyword argument)
- 命名关键字参数 (name keyword argument)

在 Python 中定义函数，这 5 种参数中的 4 个都可以一起使用，但是注意，参数定义的顺序必须是：

- 位置参数、默认参数、可变参数和关键字参数。
- 位置参数、默认参数、命名关键字参数和关键字参数。

要注意定义可变参数和关键字参数的语法：

- `*args` 【可变参数】，`args` 接收的是一个 `tuple`
- `**kw` 【关键字参数】，`kw` 接收的是一个 `dict`

* `*, nkw`【命名关键字参数】是为了限制调用者可以传入的参数名，同时可以提供默认值。定义命名关键字参数不要忘了写分隔符 *，否则定义的是位置参数。

警告：虽然可以组合多达 5 种参数，但不要同时使用太多的组合，否则函数很难懂。

### 变量作用域

- Python 中，程序的变量也分局部变量（函数内部定义，作用域该函数）和全局变量（函数外部定义，作用域整个程序范围）。

- 当内部作用域想修改外部作用域的变量时，就要用到`global`和`nonlocal`关键字了。

【例子】

```python
num = 1


def fun1():
    global num  # 需要使用 global 关键字声明
    print(num)  # 1
    num = 123
    print(num)  # 123


fun1()
print(num)  # 123
```

**内嵌函数**

【例子】

```python
def outer():
    print('outer函数在这被调用')

    def inner():
        print('inner函数在这被调用')

    inner()  # 该函数只能在outer函数内部被调用


outer()
# outer函数在这被调用
# inner函数在这被调用
```

**闭包**

- 一种特殊的内嵌函数
- **闭包的特点就是该内部函数引用了外部函数中的变量。**被内部函数引用的变量，不会因为外部函数结束而被释放掉，而是一直存在内存中，直到内部函数被调用结束。这个作用域称为 **闭包作用域**。

【例子】

```python
def funX(x):
    def funY(y):
        return x * y

    return funY
#funY(y)是闭包，引用了外层非全局变量x

i = funX(8)#返回的是内部函数
print(type(i))  # <class 'function'>
print(i(5))  # 40
```

【例子】 如果要修改闭包作用域中的变量则需要 `nonlocal` 关键字

```python
def outer():
    num = 10

    def inner():
        nonlocal num  # nonlocal关键字声明
        num = 100
        print(num)

    inner()
    print(num)


outer()

# 100
# 100
```

特点：

* 让外部访问函数内部变量成为可能；

* 局部变量会常驻在内存中；

* 可以避免使用全局变量，防止全局变量污染；

* 会造成内存泄漏（有一块内存空间被长期占用，而不被释放）

**递归**

- 如果一个函数在内部调用自身本身，这个函数就是递归函数。

【例子】斐波那契数列 `f(n)=f(n-1)+f(n-2), f(0)=0 f(1)=1`

```python
# 利用循环
i = 0
j = 1
lst = list([i, j])
for k in range(2, 11):
    k = i + j
    lst.append(k)
    i = j
    j = k
print(lst)  
# [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

# 利用递归
def recur_fibo(n):
    if n <= 1:
        return n
    return recur_fibo(n - 1) + recur_fibo(n - 2)


lst = list()
for k in range(11):
    lst.append(recur_fibo(k))
print(lst)  
# [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```

## 2. Lambda 表达式

### 匿名函数的定义

在 Python 里有两类函数：

- 第一类：用 `def` 关键词定义的正规函数
- 第二类：用 `lambda` 关键词定义的匿名函数（没有函数名）

```python
lambda argument_list: expression
```

- `lambda` - 定义匿名函数的关键词。
- `argument_list` - 函数参数，它们可以是位置参数、默认参数、关键字参数，和正规函数里的参数类型一样。
- `expression` - 只是一个表达式，输入函数参数，输出一些值。

注意：

- `expression` 中没有 return 语句，因为 lambda 不需要它来返回，表达式本身结果就是返回值。
- 匿名函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。

【例子】

```python
def sqr(x):
    return x ** 2
print(sqr)
# <function sqr at 0x000000BABD3A4400>
y = [sqr(x) for x in range(10)]
print(y)
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]


lbd_sqr = lambda x: x ** 2
print(lbd_sqr)
# <function <lambda> at 0x000000BABB6AC1E0>
y = [lbd_sqr(x) for x in range(10)]
print(y)
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]


sumary = lambda arg1, arg2: arg1 + arg2
print(sumary(10, 20))  # 30

func = lambda *args: sum(args)#可变参数
print(func(1, 2, 3, 4, 5))  # 15
```

### 匿名函数的应用

匿名函数 常常应用于函数式编程的高阶函数 (high-order function)中，主要有两种形式：

- 参数是函数 (filter, map)
- 返回值是函数 (closure)

如，在 `filter`和`map`函数中的应用：

- `filter(function, iterable)` 过滤序列，过滤掉不符合条件的元素，返回一个迭代器对象，如果要转换为列表，可以使用 `list()` 来转换。

【例子】

```python
odd = lambda x: x % 2 == 1
templist = filter(odd, [1, 2, 3, 4, 5, 6, 7, 8, 9])
print(list(templist))  # [1, 3, 5, 7, 9]
```

- `map(function, *iterables)` 根据提供的函数对指定序列做映射。

【例子】

```python
m1 = map(lambda x: x ** 2, [1, 2, 3, 4, 5])
print(list(m1))  
# [1, 4, 9, 16, 25]

m2 = map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10])
print(list(m2))  
# [3, 7, 11, 15, 19]
```

**练习题**：

1. 怎么给函数编写⽂档？

   在函数内部第一行写一个字符串作为函数文档，可以通过使用`help`来查看该函数的文档说明

   ```python 
   def test(a,b):
       "函数第⼀⾏写⼀个字符串作为函数⽂档"
   
   help(test)
   ```

2. 怎么给函数参数和返回值注解？

   在函数的形参后用冒号说明参数值，类型等

3. 闭包中，怎么对数字、字符串、元组等不可变元素更新。

   如果要修改闭包作用域中的变量则需要 `nonlocal` 关键字

4. 分别根据每一行的首元素和尾元素大小对二维列表 a = [[6, 5], [3, 7], [2, 8]] 排序。(利用lambda表达式)

   ```python
   a = [[6, 5], [3, 7], [2, 8]]
   b = sorted(a,key = lambda x:x[0], reverse = False) #根据每行首元素进行升序排列
   print(b) #[[2, 8], [3, 7], [6, 5]]
   
   c = sorted(a,key = lambda x:x[1], reverse = True) #根据每行尾元素进行降序排列
   print(c) #[[2, 8], [3, 7], [6, 5]]
   
   ```

5. 利用python解决汉诺塔问题？

> 有a、b、c三根柱子，在a柱子上从下往上按照大小顺序摞着64片圆盘，把圆盘从下面开始按大小顺序重新摆放在c柱子上，尝试用函数来模拟解决的过程。（提示：将问题简化为已经成功地将a柱上面的63个盘子移到了b柱）

```python
def hannuota(n:int,A:str,B:str,C:str):
    #该函数的意思就是把一共n块从A移至C以B作为辅助，注意位置参数的顺序
    if n == 1 :
        print(A+'->'+C)
    else:
        hannuota(n - 1, A,C,B) #第一步：把A上的n-1块移至B上，以C为辅助
        print(A+'->'+C) #第二步：把第n块从A移至C
        hannuota(n-1,B,A,C) #第三步：把B上的n-1块借助A移至C

hannuota(64, 'A', 'B', 'C')

```

# 
