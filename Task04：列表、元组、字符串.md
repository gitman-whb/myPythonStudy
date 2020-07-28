简单数据类型

- 整型`<class 'int'>`
- 浮点型`<class 'float'>`
- 布尔型`<class 'bool'>`

容器数据类型

- 列表`<class 'list'>`
- 元组`<class 'tuple'>`
- 字典`<class 'dict'>`
- 集合`<class 'set'>`
- 字符串`<class 'str'>`

# 1.列表

列表是有序集合，没有固定大小，能够保存任意数量任意类型的 Python 对象，语法为 `[元素1, 元素2, ..., 元素n]`。

## 1.1 创建

```python
#创建普通列表
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
print(x, type(x))
# ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'] <class 'list'>

#利用range()创建列表
x = list(range(1, 11, 2))
print(x, type(x))
# [1, 3, 5, 7, 9] <class 'list'>

#利用推导式创建列表
x = [i for i in range(100) if (i % 2) != 0 and (i % 3) == 0]
print(x, type(x))
# [3, 9, 15, 21, 27, 33, 39, 45, 51, 57, 63, 69, 75, 81, 87, 93, 99] <class 'list'>

#创建一个4*3的二维数组
x = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [0, 0, 0]]
print(x, type(x))
# [[1, 2, 3], [4, 5, 6], [7, 8, 9], [0, 0, 0]] <class 'list'>
for i in x:
    print(i, type(i))
# [1, 2, 3] <class 'list'>  二维数组里的元素是一维数组
# [4, 5, 6] <class 'list'>
# [7, 8, 9] <class 'list'>
# [0, 0, 0] <class 'list'>

x = [[0 for col in range(3)] for row in range(4)]#推导式+两个range
print(x, type(x))
# [[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]] <class 'list'> 
x[0][0] = 1
print(x, type(x))
# [[1, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]] <class 'list'>

x = [list(range(3)) for row in range(4)]
print(x, type(x))
#[[0, 1, 2], [0, 1, 2], [0, 1, 2], [0, 1, 2]] <class 'list'>

x = [[0] * 3] * 4
print(x, type(x))
# [[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]] <class 'list'> 简单粗暴[0]*3=[0,0,0]

#创建一个混合列表 非常强大
mix = [1, 'lsgo', 3.14, [1, 2, 3]]
print(mix, type(mix))  
# [1, 'lsgo', 3.14, [1, 2, 3]] <class 'list'>
```

## 1.2 向列表中添加元素

`list.append(obj)` 在列表末尾添加新的对象，只接受一个参数，参数可以是任何数据类型，被追加的元素在 list 中保持着原结构类型。

```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.append('Thursday')
print(x)  
# ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Thursday']
```

注意`append（追加）`和`extend（扩展)`的区别：

* x.append追加的元素如果是一个 list，那么这个 list 将作为一个整体进行追加

* x.extend在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）

```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.append(['Thursday', 'Sunday'])
print(x)  
# ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', ['Thursday', 'Sunday']]
print(len(x))  # 6

x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.extend(['Thursday', 'Sunday'])
print(x)  
# ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Thursday', 'Sunday']
print(len(x))  # 7
```

* ` list.insert(index, obj)` 在编号 `index` 位置插入 `obj`。

```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.insert(2, 'Sunday')
print(x)
# ['Monday', 'Tuesday', 'Sunday', 'Wednesday', 'Thursday', 'Friday']
print(len(x))  # 6
```

## 1.3 删除列表中的元素

* `list.remove(obj)` 移除列表中某个值的第一个匹配项

```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.remove('Monday')
print(x)  # ['Tuesday', 'Wednesday', 'Thursday', 'Friday']
```

* `list.pop([index=-1])` 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值

```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
y = x.pop()
print(y)  # Friday

y = x.pop(0)
print(y)  # Monday

y = x.pop(-2)
print(y)  # Wednesday
print(x)  # ['Tuesday', 'Thursday']
```

* `del var1[, var2 ……]` 删除单个或多个对象

```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
del x[0:2]#关键字指令，不是x的函数
print(x)  # ['Wednesday', 'Thursday', 'Friday']
```

总结：

remove指定删除具体元素名：x.remove(单个元素名)

pop指定一个索引，并且有返回值，删除该元素后还可以使用：x.pop（单个索引号）

del指定一个索引序列，可删除多个元素，删除后不能再使用：del x[索引序列]

## 1.4 获取列表中的元素

- 列表索引值是从0开始的。通过将索引指定为-1，可让Python返回最后一个列表元素，索引 -2 返回倒数第二个列表元素，以此类推。

* 切片的通用写法是 `start : stop : step`，使用时三个参数均可省略，默认值为第一个列表元素：最后一个列表元素：1。注意当指定stop时，不切到stop这个位置；不指定就能切到最后一个元素。 step为负则反方向切片。

```python
week = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
print(week[3:])  # ['Thursday', 'Friday']
print(week[:3])  # ['Monday', 'Tuesday', 'Wednesday']
print(week[::-1])  
# ['Friday', 'Thursday', 'Wednesday', 'Tuesday', 'Monday']
print(week[1:3])  # ['Tuesday', 'Wednesday']
print(week[:4:2])  # ['Monday', 'Wednesday']
print(week[1::2])  # ['Tuesday', 'Thursday']
print(week[:])  
# ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
```

* 【赋值、浅拷贝、深拷贝】

alist=[1,2,3,["a","b"]]

1）直接赋值,实际上是拷贝了这个对象的引用而已,原始列表改变，被赋值的b也会做相同的改变

b=alist

2）copy浅拷贝，新对象有独立于原对象的内存，但没有拷贝子对象，所以原始列表里的子对象改变，新列表的子对象会改变

import copy

c=copy.copy(alist)

3）deepcopy深拷贝，包含对象里面的子对象的拷贝，所以原始对象的改变不会造成深拷贝里任何子元素的改变

import copy

d=copy.deepcopy(alist)

```python
alist=[1,2,3,["a","b"]]
b=alist
import copy
c=copy.copy(alist)
d=copy.deepcopy(alist)
print(alist,b, c, d,'\n',sep='\n')
alist.append(5)
print(alist,b, c, d,'原对象添一个元素',sep='\n')
alist[3].append('cccc')
print(alist,b, c, d,'原对象里的子对象添一个元素',sep='\n')

'''
[1, 2, 3, ['a', 'b']]
[1, 2, 3, ['a', 'b']]
[1, 2, 3, ['a', 'b']]
[1, 2, 3, ['a', 'b']]


[1, 2, 3, ['a', 'b'], 5]
[1, 2, 3, ['a', 'b'], 5]
[1, 2, 3, ['a', 'b']]
[1, 2, 3, ['a', 'b']]
原对象添一个元素
[1, 2, 3, ['a', 'b', 'cccc'], 5]
[1, 2, 3, ['a', 'b', 'cccc'], 5]
[1, 2, 3, ['a', 'b', 'cccc']]
[1, 2, 3, ['a', 'b']]
原对象里的子对象添一个元素
'''
```

## 1.5 列表的常用操作符

- 等号操作符：`==`
- 连接操作符 `+`
- 重复操作符 `*`
- 成员关系操作符 `in`、`not in`

「等号 ==」，只有成员、成员位置都相同时才返回True。

列表拼接有两种方式，用「加号 +」和「乘号 *」，前者首尾拼接，后者复制拼接。

前面三种方法（`append`, `extend`, `insert`）可对列表增加元素，它们没有返回值，是直接修改了原数据对象。 而将两个list相加，需要创建新的 list 对象，从而需要消耗额外的内存，特别是当 list 较大时，尽量不要使用 “+” 来添加list。

## 1.6 列表其他方法

`list.count(obj)` 统计某个元素在列表中出现的次数

```python
list1 = [123, 456] * 3
print(list1)  # [123, 456, 123, 456, 123, 456]
num = list1.count(123)
print(num)  # 3
```

`list.index(x[, start[, end]])` 从列表中找出某个值第一个匹配项的索引位置

```python
list1 = [123, 456] * 5
print(list1.index(123))  # 0
print(list1.index(123, 1))  # 2
print(list1.index(123, 3, 7))  # 4
```

`list.reverse()` 反向列表中元素

```
x = [123, 456, 789]
x.reverse()
print(x)  # [789, 456, 123]
```

`list.sort(key=None, reverse=False)` 对原列表进行排序。

- `key` -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
- `reverse` -- 排序规则，`reverse = True` 降序， `reverse = False` 升序（默认）。
- 该方法没有返回值，但是会对列表的对象进行排序。

```python
x = [123, 456, 789, 213]
x.sort()
print(x)
#[123, 213, 456, 789]
x.sort(reverse=True)
print(x)
#[789, 456, 213, 123]

#获取列表第二个元素
def takeSecond(oneList):
    return oneList[1]
x = [(2, 2), (3, 4), (4, 1), (1, 3)]
#指定第二个元素排序
x.sort(key=takeSecond)
print(x)
#[(4, 1), (2, 2), (1, 3), (3, 4)]
```

## 练习题

1、列表操作练习

列表lst 内容如下

lst = [2, 5, 6, 7, 8, 9, 2, 9, 9]

请写程序完成下列操作：

1. 在列表的末尾增加元素15
2. 在列表的中间位置插入元素20
3. 将列表[2, 5, 6]合并到lst中
4. 移除列表中索引为3的元素
5. 翻转列表里的所有元素
6. 对列表里的元素进行排序，从小到大一次，从大到小一次

```python
lst = [2, 5, 6, 7, 8, 9, 2, 9, 9]
lst.append(15)
print(lst)
lst.insert(int(len(lst)/2),20)
print(lst)
lst.extend([2,5,6])
print(lst)
lst.pop(3)
print(lst)
lst.reverse()
print(lst)
lst.sort()
print(lst)
lst.sort(reverse=True)
print(lst)
'''
[2, 5, 6, 7, 8, 9, 2, 9, 9, 15]
[2, 5, 6, 7, 8, 20, 9, 2, 9, 9, 15]
[2, 5, 6, 7, 8, 20, 9, 2, 9, 9, 15, 2, 5, 6]
[2, 5, 6, 8, 20, 9, 2, 9, 9, 15, 2, 5, 6]
[6, 5, 2, 15, 9, 9, 2, 9, 20, 8, 6, 5, 2]
[2, 2, 2, 5, 5, 6, 6, 8, 9, 9, 9, 15, 20]
[20, 15, 9, 9, 9, 8, 6, 6, 5, 5, 2, 2, 2]
'''
```

2、修改列表

问题描述：

lst = [1, [4, 6], True]

请将列表里所有数字修改成原来的两倍

```python
lst = [1, [4, 6], True]
lst[0]*=2
lst[1][0]*=2
lst[1][1]*=2
print(lst)
#[2, [8, 12], True]
```

3、leetcode 852题 山脉数组的峰顶索引

```python
#不用判断是不是山脉数组，直接返回最大值索引就完事了。。。
class Solution:
    def peakIndexInMountainArray(self, A: List[int]) -> int:
        return A.index(max(A))
```

# 2 元组

「元组」定义语法为：`(元素1, 元素2, ..., 元素n)`

## 2.1 创建和访问一个元组

- Python 的元组与列表类似，不同之处在于tuple被创建后就不能对其进行修改，类似字符串。
- 元组使用小括号，列表使用方括号。
- 元组与列表类似，也用整数来对它进行索引 (indexing) 和切片 (slicing)。

```python
t1 = (1, 10.31, 'python')
t2 = 1, 10.31, 'python'
print(t1, type(t1))
# (1, 10.31, 'python') <class 'tuple'>
print(t2, type(t2))
# (1, 10.31, 'python') <class 'tuple'>
#创建元组可以用小括号 ()，也可以什么都不用，为了可读性，建议还是用 ()。

tuple1 = (1, 2, 3, 4, 5, 6, 7, 8)
print(tuple1[1])  # 2
print(tuple1[5:])  # (6, 7, 8)
print(tuple1[:5])  # (1, 2, 3, 4, 5)
tuple2 = tuple1[:]
print(tuple2)  # (1, 2, 3, 4, 5, 6, 7, 8)
#切片访问元素时也还是得用[]
```

* **【注意】**元组中只包含一个元素时，需要在元素后面添加逗号，否则括号会被当作运算符使用。

```python
x = (1)
print(type(x))  # <class 'int'>
x = (1,)
print(type(x))  # <class 'tuple'>

print(8 * (8))  # 64
print(8 * (8,))  # (8, 8, 8, 8, 8, 8, 8, 8)
```

* 创建和访问二维元组的形式也与列表相似，创建的时候用[]替代（），访问同样用[]

## 2.2 更新和删除一个元组

* 元组有不可更改 (immutable) 的性质，因此不能直接给元组的元素赋值，但是只要元组中的元素是可更改 (mutable)，那么我们可以直接更改其子元素。

```python
t1 = (1, 2, 3, [4, 5, 6])
print(t1)  # (1, 2, 3, [4, 5, 6])

t1[0]=9#这是违法操作
t1[3][0] = 9#子元素可以更改
print(t1)  # (1, 2, 3, [9, 5, 6]) 
```

* 元组本身不能更改元素，但可以对元组进行连接，得到新元组

```python
tup1 = (12, 34.56);
tup2 = ('abc', 'xyz');
tup3 = tup1 + tup2;
print tup3;
#(12, 34.56, 'abc', 'xyz')
```

* 元组中的元素是不允许删除的，但我们可以使用del语句来删除整个元组: del tup

## 2.3 元组相关的操作符

- 等号操作符：`==`
- 连接操作符 `+`
- 重复操作符 `*`
- 成员关系操作符 `in`、`not in`

使用与列表相同。

## 2.4 内置方法

* 元组大小和内容都不可更改，因此只有 `count` 和 `index` 两种方法,与列表相同。

## 2.5 解压元组

```python
#解压（unpack）一维元组（有几个元素左边括号定义几个变量）
t = (1, 10.31, 'python')
(a, b, c) = t
print(a, b, c)
# 1 10.31 python

#解压二维元组（按照元组里的元组结构来定义变量）
t = (1, 10.31, ('OK', 'python'))
(a, b, (c, d)) = t
print(a, b, c, d)
# 1 10.31 OK python

#如果你只想要元组其中几个元素，用通配符「*」，在计算机语言中代表一个或多个元素。下例就是把多个元素丢给了 rest 变量。
t = 1, 2, 3, 4, 5
a, b, *rest, c = t
print(a, b, c)  # 1 2 5
print(rest)  # [3, 4]注意：这里的是列表
#如果你根本不在乎 rest 变量，那么就用通配符「*」加上下划线「_」。
t = 1, 2, 3, 4, 5
a, b, *_ = t
print(a, b)  # 1 2
```

## 练习题

1、元组概念

写出下面代码的执行结果和最终结果的类型

```
(1, 2)*2
(1, )*2
(1)*2
```

分析为什么会出现这样的结果.

***

```python
(1, 2, 1, 2) <class 'tuple'>
(1, 1) <class 'tuple'>
2 <class 'int'>
#*重复操作符，元组跟列表是一样的
#单个元素不加逗号被认成整型数据了呗
```

2、拆包过程是什么？

```
a, b = 1, 2
```

上述过程属于拆包吗？

可迭代对象拆包时，怎么赋值给占位符？

***

拆包过程是指利用一句赋值语句按顺序将元组中的各元素赋值给=左边的各个变量，属于拆包。

在可迭代对象拆包时，使用`_`(单个元素)，`*_`(连续多个元素)进行占位。