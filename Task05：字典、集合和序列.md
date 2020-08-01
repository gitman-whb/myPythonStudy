# 字典

## 1. 可变类型与不可变类型

- 序列是以连续的整数为索引，与此不同的是，字典以"关键字"为索引，关键字可以是任意不可变类型，通常用字符串或数值。
- 字典是 Python 唯一的一个 映射类型，字符串、元组、列表属于序列类型。

断一个数据类型 `X` 是不是可变类型？

- 麻烦方法：用 `id(X)` 函数，对 X 进行某种操作，比较操作前后的 `id`，如果不一样，则 `X` 不可变，如果一样，则 `X` 可变。
- 便捷方法：用 `hash(X)`，只要不报错，证明 `X` 可被哈希，即不可变，反过来不可被哈希，即可变。

```python
i = 1
print(id(i))  # 140732167000896
i = i + 2
print(id(i))  # 140732167000960
#整数 i 在加 1 之后的 id 和之前不一样，因此加完之后的这个 i (虽然名字没变)，但不是加之前的那个 i 了，因此整数是不可变类型。

l = [1, 2]
print(id(l))  # 4300825160
l.append('Python')
print(id(l))  # 4300825160
#列表l在附加 'Python' 之后的 id 和之前一样，因此列表是可变类型。
```

```python
print(hash('Name'))  # -9215951442099718823

print(hash((1, 2, 'Python')))  # 823362308207799471
print(hash([1, 2, 'Python']))
# TypeError: unhashable type: 'list'
print(hash({1, 2, 3}))
# TypeError: unhashable type: 'set'

#数值、字符和元组 都能被哈希，因此它们是不可变类型。
#列表、集合、字典不能被哈希，因此它是可变类型。
```

## 2. 字典的定义

字典 是无序的 键:值（`key:value`）对集合，键必须是互不相同的（在同一个字典之内）。

- `dict` 内部存放的顺序和 `key` 放入的顺序是没有关系的。
- `dict` 查找和插入的速度极快，不会随着 `key` 的增加而增加，但是需要占用大量的内存。

字典 定义语法为 `{元素1, 元素2, ..., 元素n}`，其中每一个元素是一个「键值对」-- 键:值 (`key:value`)。

## 3. 创建和访问字典

* 初始化，通过字符串或数值作为`key`来创建字典。

```python
dic = {'李宁': '一切皆有可能', '耐克': 'Just do it', '阿迪达斯': 'Impossible is nothing'}
print('耐克的口号是:', dic['耐克'])  
# 耐克的口号是: Just do it

dic1 = {1: 'one', 2: 'two', 3: 'three'}
print(dic1)  # {1: 'one', 2: 'two', 3: 'three'}
print(dic1[1])  # one
print(dic1[4])  # KeyError: 4 如果我们取的键在字典中不存在，会直接报错KeyError。
```

- `dict()` 构造函数，创建一个空的字典。

通过`key`直接把数据放入字典中，但一个`key`只能对应一个`value`，多次对一个`key`放入 `value`，后面的值会把前面的值冲掉。

```python
dic = dict()
dic['a'] = 1
dic['b'] = 2
dic['c'] = 3
print(dic)
# {'a': 1, 'b': 2, 'c': 3}
dic['a'] = 11
print(dic)
# {'a': 11, 'b': 2, 'c': 3}
```

## 4. 字典的内置方法

- `dict.fromkeys(seq[, value])` 用于创建一个新字典，以序列 `seq` 中元素做字典的键，`value` 为字典所有键对应的初始值。

```python
seq = ('name', 'age', 'sex')
dic1 = dict.fromkeys(seq)
print(dic1)
# {'name': None, 'age': None, 'sex': None}

dic2 = dict.fromkeys(seq, 10)
print(dic2)
# {'name': 10, 'age': 10, 'sex': 10}

dic3 = dict.fromkeys(seq, ('小马', '8', '男'))
print(dic3)
# {'name': ('小马', '8', '男'), 'age': ('小马', '8', '男'), 'sex': ('小马', '8', '男')}
```

- `dict.keys()`返回一个可迭代对象，可以使用 `list()` 来转换为列表，列表为字典中的**所有键**。
- `dict.items()`以列表返回可遍历的 (键, 值) 元组数组（**所有键值对**）

```python
dic = {'Name': 'lsgogroup', 'Age': 7}
print(dic.keys())  # dict_keys(['Name', 'Age'])
lst = list(dic.keys())  # 转换为列表
print(lst)  # ['Name', 'Age']

dic = {'Name': 'Lsgogroup', 'Age': 7}
print(dic.items())
# dict_items([('Name', 'Lsgogroup'), ('Age', 7)])

print(tuple(dic.items()))
# (('Name', 'Lsgogroup'), ('Age', 7))

print(list(dic.items()))
# [('Name', 'Lsgogroup'), ('Age', 7)]
```

- `dict.get(key, default=None)` 返回指定键的值，如果值不在字典中返回默认值。
- `dict.setdefault(key, default=None)`和`get()`方法 类似, 如果键不存在于字典中，将会添加键并将值设为默认值。

```pyhton
dic = {'Name': 'Lsgogroup', 'Age': 27}
print("Age 值为 : %s" % dic.get('Age'))  # Age 值为 : 27
print("Sex 值为 : %s" % dic.get('Sex', "NA"))  # Sex 值为 : NA

print("Age 键的值为 : %s" % dic.setdefault('Age'))  # Age 键的值为 : 27
print("Sex 键的值为 : %s" % dic.setdefault('Sex', Male))  # Sex 键的值为 : Male
print(dic)  
# {'Age': 7, 'Name': 'Lsgogroup', 'Sex': Male}
```

- `dict.pop(key[,default])`删除字典给定键 `key` 所对应的值，返回值为被删除的值。`key` 值必须给出。若`key`不存在，则返回 `default` 值。
- `del dict[key]` 删除字典给定键 `key` 所对应的值。
- `dict.popitem()`随机返回并删除字典中的一对键和值，如果字典已经为空，却调用了此方法，就报出KeyError异常。
- `dict.clear()`用于删除字典内所有元素。

```python
dic1 = {1: "a", 2: [1, 2]}
print(dic1.pop(1), dic1)  # a {2: [1, 2]}
# 这时没有默认值，就会报错
print(dic1.pop(3, "nokey"), dic1)  # nokey {2: [1, 2]}

del dic1[2]
print(dic1)  # {}

dic1 = {1: "a", 2: [1, 2]}
print(dic1.popitem())  # (1, 'a')
print(dic1)  # {2: [1, 2]}

```

* `dict.copy()`返回一个字典的浅复制。

```python
dic1 = {'user': 'lsgogroup', 'num': [1, 2, 3]}

# 引用对象
dic2 = dic1  
# 浅拷贝父对象（一级目录），子对象（二级目录）不拷贝，还是引用
dic3 = dic1.copy()  

print(id(dic1))  # 148635574728
print(id(dic2))  # 148635574728
print(id(dic3))  # 148635574344

# 修改 data 数据
dic1['user'] = 'root'
dic1['num'].remove(1)

# 输出结果
print(dic1)  # {'user': 'root', 'num': [2, 3]}
print(dic2)  # {'user': 'root', 'num': [2, 3]}
print(dic3)  # {'user': 'lsgogroup', 'num': [2, 3]}
```

- `dict.update(dict2)`把字典参数 `dict2` 的 `key:value`对 更新到字典 `dict` 里。

【例子】

```python
dic = {'Name': 'Lsgogroup', 'Age': 7}
dic2 = {'Sex': 'female', 'Age': 8}
dic.update(dic2)
print(dic)  
# {'Sex': 'female', 'Age': 8, 'Name': 'Lsgogroup'}
#原来有的键就更新值，没有的话就连键带值就复制过来
```

**练习题**：

1、字典基本操作

字典内容如下:

```
dic = {
    'python': 95,
    'java': 99,
    'c': 100
    }
```

用程序解答下面的题目

- 字典的长度是多少
- 请修改'java' 这个key对应的value值为98
- 删除 c 这个key
- 增加一个key-value对，key值为 php, value是90
- 获取所有的key值，存储在列表里
- 获取所有的value值，存储在列表里
- 判断 javascript 是否在字典中
- 获得字典里所有value 的和
- 获取字典里最大的value
- 获取字典里最小的value
- 字典 dic1 = {'php': 97}， 将dic1的数据更新到dic中

***

```python
dic = {
    'python': 95,
    'java': 99,
    'c': 100
    }
print(len(dic))
#3
dic['java'] = 98
del dic['c']
print(dic)
#{'python': 95, 'java': 98}
dic['php']=90
print(list(dic.keys()))
#[95, 98, 90]
'javascript' in dic
#False
print(sum(dic.values()))
#283
print(max(dic.values()))
#98
print(min(dic.values()))
#90
dic1 = {'php':97}
dic.update(dic1)
print(dic)
#{'python': 95, 'java': 98, 'php': 97}
```

2、字典中的value

有一个字典，保存的是学生各个编程语言的成绩，内容如下

data = {
‘python’: {‘上学期’: ‘90’, ‘下学期’: ‘95’},
‘c++’: [‘95’, ‘96’, ‘97’],
‘java’: [{‘月考’:‘90’, ‘期中考试’: ‘94’, ‘期末考试’: ‘98’}]
}
各门课程的考试成绩存储方式并不相同，有的用字典，有的用列表，但是分数都是字符串类型，请实现函数transfer_score(score_dict)，将分数修改成int类型

```python
data = {
        'python': {'上学期': '90', '下学期': '95'},
        'c++': ['95', '96', '97'],
        'java': [{'月考':'90', '期中考试': '94', '期末考试': '98'}]
        }
        
for k in data['python']:
	data['python'][k] = int (data['python'][k])
	
data['c++'] = [int(x) for x in data['c++']]

for k in data['java'][0]:
	data['java'][0][k] = int (data['java'][0][k])
print(data)
```
# 集合

Python 中`set`与`dict`类似，也是一组`key`的集合，但不存储`value`。由于`key`不能重复，所以，在`set`中，也没有重复的`key`。

注意，`key`为不可变类型，即可哈希的值。

## 1. 集合的创建

- ①直接初始化：把一堆元素用花括号括起来`{元素1, 元素2, ..., 元素n}`，重复元素在`set`中会被自动被过滤。
- ②先创建对象再加入元素：在创建空集合的时候只能使用`s = set()`，因为`s = {}`创建的是空字典。

```python
#直接初始化
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
print(basket)  # {'banana', 'apple', 'pear', 'orange'}
#空集合再添加
basket = set()
basket.add('apple')
basket.add('banana')
print(basket)  # {'banana', 'apple'}
```

- 使用`set(value)`工厂函数，把列表或元组转换成集合。

【例子】

```python
a = set('abracadabra')
print(a)  
# {'r', 'b', 'd', 'c', 'a'}

b = set(("Google", "Lsgogroup", "Taobao", "Taobao"))
print(b)  
# {'Taobao', 'Lsgogroup', 'Google'}

c = set(["Google", "Lsgogroup", "Taobao", "Google"])
print(c)  
# {'Taobao', 'Lsgogroup', 'Google'}
```

集合的两个特点：无序 (unordered) 和唯一 (unique)。

由于 `set` 存储的是无序集合，所以我们不可以为集合创建索引或执行切片(slice)操作，也没有键(keys)可用来获取集合中元素的值，但是可以判断一个元素是否在集合中。

## 2. 访问集合中的值

集合大小：len(s)

遍历集合每个元素：

for item in s:

​	print(item)

判断是否存在：in和not in

## 3. 集合的内置方法

- `set.add(elmnt)`用于给集合**添加**元素，如果添加的元素在集合中已存在，则不执行任何操作。

* `set.update(set)`用于**修改**当前集合，可以添加新的元素或集合到当前集合中，如果添加的元素在集合中已存在，则该元素只会出现一次，重复的会忽略。

```python
fruits = {"apple", "banana", "cherry"}
fruits.add("orange") 
# {'orange', 'cherry', 'banana', 'apple'}
fruits.add("apple")
# {'orange', 'cherry', 'banana', 'apple'}

x = {"apple", "banana", "cherry"}
y = {"google", "baidu", "apple"}
x.update(y)
# {'cherry', 'banana', 'apple', 'google', 'baidu'}
y.update(["lsgo", "dreamtech"])#居然能用列表去更新集合！
# {'lsgo', 'baidu', 'dreamtech', 'apple', 'google'}
```

* `set.remove(item)` 用于移除集合中的**指定**元素。如果元素不存在，则会发生错误。

* `set.discard(value)` 用于移除**指定**的集合元素。`remove()` 方法在移除一个不存在的元素时会发生错误，而 `discard()` 方法**不会**。

* `set.pop()` 用于**随机**移除一个元素。

```python
fruits = {"apple", "banana", "cherry"}
######################
fruits.remove("banana")
print(fruits)  # {'apple', 'cherry'}

fruits.discard("banana")
print(fruits)  # {'apple', 'cherry'}

x = fruits.pop()#随机弹一个
print(fruits)  # {'cherry', 'apple'}
print(x)  # banana
```

由于 set 是无序和无重复元素的集合，所以两个或多个 set 可以做数学意义上的**集合操作**。

- `set.intersection(set1, set2...)` 返回与括号内集合共同的交集。
- `set1 & set2` 返回这两个集合的交集。
- `set.intersection_update(set1, set2...)` 交集，在原始的集合上移除不重叠的元素。

```python
a = set('abracadabra')
b = set('alacazam')
print(a)  # {'r', 'a', 'c', 'b', 'd'}
print(b)  # {'c', 'a', 'l', 'm', 'z'}

c = a.intersection(b)
print(c)  # {'a', 'c'}
print(a & b)  # {'c', 'a'}
print(a)  # {'a', 'r', 'c', 'b', 'd'}

a.intersection_update(b)
print(a)  # {'a', 'c'}
```

并集

- `set.union(set1, set2)` 返回两个集合的并集。
- `set1 | set2` 返回两个集合的并集。

差集

- `set.difference(set)` 返回集合的差集。
- `set1 - set2` 返回集合的差集。
- `set.difference_update(set)` 集合的差集，直接在原来的集合中移除元素，没有返回值。

异或

- `set.symmetric_difference(set)`返回集合的异或。
- `set1 ^ set2` 返回集合的异或。

包含

- `set1.issubset(set2)`判断set1是不是被set2包含，如果是则返回 True，否则返回 False。
- `set1 <= set2` 判断集合是不是被其他集合包含，如果是则返回 True，否则返回 False。

- `set1.issuperset(set2)`用于判断set1是不是包含set2，如果是则返回 True，否则返回 False。
- `set1 >= set2` 判断集合是不是包含其他集合，如果是则返回 True，否则返回 False。

## 4. 集合的转换

```python
se = set(range(4))
li = list(se)
tu = tuple(se)

print(se, type(se))  # {0, 1, 2, 3} <class 'set'>
print(li, type(li))  # [0, 1, 2, 3] <class 'list'>
print(tu, type(tu))  # (0, 1, 2, 3) <class 'tuple'>
```

## 5. 不可变集合

Python 提供了不能改变元素的集合的实现版本，即不能增加或删除元素，类型名叫`frozenset`。需要注意的是`frozenset`仍然可以进行集合操作，只是不能用带有`update`的方法。

- `frozenset([iterable])` 返回一个**冻结**的集合，冻结后集合不能再添加或删除任何元素。

【例子】

```python
a = frozenset(range(10))  # 生成一个新的不可变集合
print(a)  
# frozenset({0, 1, 2, 3, 4, 5, 6, 7, 8, 9})

b = frozenset('lsgogroup')
print(b)  
# frozenset({'g', 's', 'p', 'r', 'u', 'o', 'l'})
```

**练习题**：

1. 怎么表示只包含⼀个数字1的元组。
2. 创建一个空集合，增加 {‘x’,‘y’,‘z’} 三个元素。
3. 列表['A', 'B', 'A', 'B']去重。
4. 求两个集合{6, 7, 8}，{7, 8, 9}中不重复的元素（差集指的是两个集合交集外的部分）。
5. 求{'A', 'B', 'C'}中元素在 {'B', 'C', 'D'}中出现的次数。

***

```python
t=(1,)
print(t)
#(1,)

s1=set()
s1.add('x')
s1.add('y')
s1.add('z')
print(s1)
#{'z', 'x', 'y'}

lst=['A', 'B', 'A', 'B']
lst=list(set(lst))#利用集合不重复的特性
print(lst)
#['B', 'A']

s2={6, 7, 8}
s3={7, 8, 9}
print(s2-s3,s3-s2)
#{6} {9}

s4={'A', 'B', 'C'}
s5={'B', 'C', 'D'}
count=0
for i in s4:
    if i in s5:
        count+=1
        print('元素%r出现了'%i)
print('重复次数%d次'%count)
'''
元素'C'出现了
元素'B'出现了
重复次数2次
'''
```

# 序列

在 Python 中，序列类型包括字符串、列表、元组、集合和字典，这些序列支持一些通用的操作，但比较特殊的是，集合和字典不支持索引、切片、相加和相乘操作。

## 1. 针对序列的内置函数

**以下函数均不需要某个对象，可直接调用**

- `list(sub)` 把一个可迭代对象转换为列表。

* `tuple(sub)` 把一个可迭代对象转换为元组。

* `str(obj)` 把obj对象转换为字符串

* `len(s)` 返回对象（字符、列表、元组等）长度或元素个数。

* `max(sub)`返回序列或者参数集合中的最大值

* `min(sub)`返回序列或参数集合中的最小值

* `sum(iterable[, start=0])` 返回序列`iterable`与可选参数`start`的总和。

- sorted(iterable, key=None, reverse=False) 

  对所有可迭代的对象进行排序操作。

  - `iterable` -- 可迭代对象。
  - `key` -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
  - `reverse` -- 排序规则，`reverse = True` 降序 ， `reverse = False` 升序（默认）。
  - 返回重新排序的列表。

```python
x = [-8, 99, 3, 7, 83]
print(sorted(x))  # [-8, 3, 7, 83, 99]
print(sorted(x, reverse=True))  # [99, 83, 7, 3, -8]

t = ({"age": 20, "name": "a"}, {"age": 25, "name": "b"}, {"age": 10, "name": "c"})
x = sorted(t, key=lambda a: a["age"])
print(x)
# [{'age': 10, 'name': 'c'}, {'age': 20, 'name': 'a'}, {'age': 25, 'name': 'b'}]
```

* `reversed(seq)` 函数返回一个反转的迭代器，`seq` -- 要转换的序列，可以是 tuple, string, list 或 range。

- `enumerate(sequence, [start=0])`

  用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个**索引序列**，同时列出**数据下标和数据**，一般用在 for 循环当中。

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
a = list(enumerate(seasons))
print(a)  
# [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]

b = list(enumerate(seasons, 1))#设置索引从1开始
print(b)  
# [(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]

for i, element in a:
    print('{0},{1}'.format(i, element))#格式化输出（位置参数）
# 0,Spring
# 1,Summer
# 2,Fall
# 3,Winter
```

- ```
  zip(iter1 [,iter2 [...]])
  ```

  - 用于将可迭代的对象作为参数，将对象中**对应的元素打包成一个个元组**，然后返回由这些元组组成的对象，这样做的好处是节约了不少的内存。
  - 我们可以使用 `list()` 转换来输出列表。
  - 如果各个迭代器的**元素个数不一致**，则返回列表长度与最短的对象相同，利用 `*` 号操作符，可以将元组解压为列表。

```python
a = [1, 2, 3]
b = [4, 5, 6]
c = [4, 5, 6, 7, 8]

zipped = zip(a, b)
print(zipped)  # <zip object at 0x000000C5D89EDD88>
print(list(zipped))  # [(1, 4), (2, 5), (3, 6)]
zipped = zip(a, c)
print(list(zipped))  # [(1, 4), (2, 5), (3, 6)]

a1, a2 = zip(*zip(a, b))
print(list(a1))  # [1, 2, 3]
print(list(a2))  # [4, 5, 6]
```

**练习题**：

1. 怎么找出序列中的最⼤、⼩值？

   max(sub)返回序列或者参数集合中的最大值
   min(sub)返回序列或参数集合中的最小值

2. sort() 和 sorted() 区别

   L.sort() 函数只适用于列表排序，而sorted()函数适用于任意可以迭代的对象排序。

   L.sort() 函数无返回值，直接改变原有的待排序列表，而sorted()函数则不会改变，有返回。

```python
   x = [-8, 99, 3, 7, 83]
   x1=sorted(x)
   x.sort()
   print(x1,x)
   #[-8, 3, 7, 83, 99] [-8, 3, 7, 83, 99]
```

3. 怎么快速求 1 到 100 所有整数相加之和？

```python
   x=range(1,100)
   print(sum(x))
```

4. 求列表 [2,3,4,5] 中每个元素的立方根。

```python
lst=[2,3,4,5]
lst=[i**3 for i in lst]
print(lst)
```

5. 将[‘x’,‘y’,‘z’] 和 [1,2,3] 转成 [(‘x’,1),(‘y’,2),(‘z’,3)] 的形式。

```python
lst1=['x','y','z']
lst2=[1,2,3]
lst3=zip(lst1,lst2)
print(list(lst3))
```

   
