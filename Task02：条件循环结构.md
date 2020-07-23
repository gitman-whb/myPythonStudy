

# 02 条件循环结构

##  条件语句 

**if语句**：

条件表达式可以通过布尔操作符 `and`，`or`和`not` 实现**多重条件**判断。

```python
if 2 > 1 and not 2 > 3:
    print('Correct Judgement!')
else:
    print("判断错误")
# Correct Judgement!
```

`if`语句支持嵌套，即在一个`if`语句中嵌入另一个`if`语句，从而构成不同层次的选择结构。Python 使用缩进而不是大括号来标记代码块边界，因此要特别注意`else`的悬挂问题。

**if - elif - else 语句**

`elif 语句即为 else if`，用来检查多个表达式是否为真，并在为真时执行特定代码块中的代码。

```python
temp = input('请输入成绩:')#input将接收的任何数据类型都默认为str
source = int(temp)
if 100 >= source >= 90:
    print('A')
elif 90 > source >= 80:
    print('B')
elif 80 > source >= 60:
    print('C')
elif 60 > source >= 0:
    print('D')
else:
    print('输入错误！')
#请输入成绩: 88
#B
```

**assert关键词**

`assert`这个关键词我们称之为“断言”，当这个关键词后边的条件为 False 时，程序自动崩溃并抛出`AssertionError`的异常。

在进行单元测试时，可以用来在程序中置入检查点，只有条件为 True 才能让程序正常工作。

```python
assert 3 > 7

# AssertionError
```

## 循环语句

**while循环**

```python
string = 'abcd'
while string:
    print(string)
    string = string[1:]

# abcd
# bcd
# cd
# d
```

**while-else循环**

当`while`循环正常执行完的情况下，执行`else`输出，如果`while`循环中执行了跳出循环的语句，比如 `break`，将不执行`else`代码块的内容。

```python
count = 0
while count < 5:
    print("%d is  less than 5" % count)
    count = count + 1
else:
    print("%d is not less than 5" % count)
    
# 0 is  less than 5
# 1 is  less than 5
# 2 is  less than 5
# 3 is  less than 5
# 4 is  less than 5
# 5 is not less than 5
```

**for循环**

可以遍历任何有序序列，如`str、list、tuple`等，也可以遍历任何可迭代对象，如`dict`。

```python
for i in 'ILoveLSGO':
    print(i, end=' ')  # 不换行输出
# I L o v e L S G O

member = ['张三', '李四', '刘德华', '刘六', '周润发']
for each in member:
    print(each)
# 张三
# 李四
# 刘德华
# 刘六
# 周润发
```

**for-else循环**

与`while - else`语句一样。(`break`)

**range（）函数**

```python
range([start=0,] stop,[,step=1])
```

- 有三个参数，其中用中括号括起来的两个表示这两个参数是可选的。
- `start=0和step=1` 表示默认值是0和1。
- 作用是生成一个从`start`参数的值开始到`stop`参数的值结束的数字序列，该序列包含`start`的值但不包含`stop`的值。

```python
for i in range(2,9,2):  #不含9 
    print(i，end=' ')
# 2 4 6 8

for i in range(2,9):  #默认step=1
    print(i，end=' ')
# 2 3 4 5 6 7 8

for i in range(5):  #默认start=0 step=1
    print(i，end=' ')
# 0 1 2 3 4 5
```

**enumerate()函数**

```
enumerate(sequence, [start=0])
```

- sequence -- 一个序列、迭代器或其他支持迭代对象。
- start -- 下标起始位置。
- 返回 enumerate(枚举) 对象

 ```python
#用 enumerate(A)不仅返回了 A 中的元素，还顺便给该元素一个索引值 (默认从 0 开始)。此外，用 enumerate(A, j) 还可以确定索引起始值为 j。
  seasons = ['Spring', 'Summer', 'Fall', 'Winter']
  lst = list(enumerate(seasons))
  print(lst)
  # [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
  lst = list(enumerate(seasons, start=1))  # 下标从 1 开始
  print(lst)
  # [(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
 ```

```python
#enumerate()与 for 循环的结合使用
languages = ['Python', 'R', 'Matlab', 'C++']
for language in languages:
    print('I love', language)
print('Done!')

'''
I love Python
I love R
I love Matlab
I love C++
Done!
'''

for i, language in enumerate(languages, 2):
    print(i, 'I love', language)
print('Done!')

'''
2 I love Python
3 I love R
4 I love Matlab
5 I love C++
Done!
'''
```

**break语句**

`break`语句可以跳出当前所在层的循环。

**continue语句**

`continue`终止本轮循环并开始下一轮循环。

**pass语句**

`pass` 语句的意思是“不做任何事”，如果你在需要有语句的地方不写任何语句，那么解释器会提示出错，而 `pass` 语句就是用来解决这些问题的，只起到占位作用，不做任何操作。

**推导式**

对列表、元组、字典、集合等中的每个元素都做相同操作（expr：生成新元素表达式，也可以是有返回值的函数。）

**列表推导式**

```python
[ expr for value in collection [if condition] ]
```

```python
x = [i ** 2 for i in range(1, 10)]
print(x)
# [1, 4, 9, 16, 25, 36, 49, 64, 81]

x = [(i, i ** 2) for i in range(6)]
print(x)
# [(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]

a = [(i, j) for i in range(0, 3) for j in range(0, 3)]#两个for
print(a)
# [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]

a = [(i, j) for i in range(0, 3) if i < 1 for j in range(0, 3) if j > 1]#两个for,带if条件
print(a)
# [(0, 2)]
```

**元组推导式**

```python
( expr for value in collection [if condition] )
```

**字典推导式**

```python
{ key_expr: value_expr for value in collection [if condition] }
```

**集合推导式**

```python
{ expr for value in collection [if condition] }
```

综合例子：可输入三次密码的密码锁

```python
passwdList=['123','456','789']
valid = False
count=3
while count>0:
    password = input('enter password')
    for item in passwdList:
        if password == item:
            valid = True
            print('congratulatons!')
            break
    if not valid:
        print('invalid input')
        count-=1
        continue
    else:
        break
```

**练习题**

1、编写一个Python程序来查找那些既可以被7整除又可以被5整除的数字，介于1500和2700之间。

```python
for num in range(1500,2700,1):
    if num%7==0 and num%5==0:
        print(num,end=' ')
#1505 1540 1575 1610 1645 1680 1715 1750 1785 1820 1855 1890 1925 1960 1995 2030 2065 2100 2135 2170 2205 2240 2275 2310 2345 2380 2415 2450 2485 2520 2555 2590 2625 2660 2695 
```

2、龟兔赛跑游戏

```python
v1, v2,t,s,l = map(int,input().split())
l1=0#兔子走的路程
l2=0#乌龟走的路程
time=0#比赛进行的时间
while l1<l and l2<l:
    l1+=v1
    l2+=v2
    time=time+1#时间加一秒
    if l1==l|l2==l:#任意一个到达终点即比赛结束
        break
    if l1-l2 >=t:
        l1=l1-s*v1#兔子路程减少s秒所走的
if l1>l2:
    print('R')
elif l1<l2:
    print('T') 
else:
    print('R')
print(time)

#输入：10 5 5 2 20
#输出：R
#     4
```

扩展：利用map和split在一行中读多个数据

1.map
map函数接收两个参数，一个是函数，一个是序列，它将传入的函数依次作用到序列的每个元素，并把结果作为新的list返回。
2.split
split函数负责拆分字符串，通过指定分隔符(默认为空格)对字符串进行分隔，并返回分割后的字符串列表list

```python
a, b = input().split()
#Python默认为字符串型，所以这里的a, b为字符串型
a, b = map(int, input().split())
#这里我们用map函数将其转换为int型，此时的a, b为int型
a, b = map(float, input().split())
#此时的a, b为float型
```

