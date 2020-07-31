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