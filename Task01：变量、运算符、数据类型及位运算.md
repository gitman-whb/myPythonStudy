# 01 变量、运算符与数据类型

## 随笔，只记录与C++中不同之处

```python3
#这是单行注释
print("Hello World")
'''
这是多行注释
这是多行注释
这是多行注释
'''
```

| 操作符 | 名称         | 示例                     |
| ------ | ------------ | ------------------------ |
| /      | 除（带小数） | 11//3=3.666666666665     |
| //     | 整除         | 11//3=3                  |
| %      | 取余         | 11%3=2                   |
| **     | 幂           | 2**3                     |
| and    | 与           | (2>1) and (3>7)          |
| or     | 或           | (1>3) or (2<9)           |
| not    | 非           | not(2>1)                 |
| is     | 是           | 'hello' is 'hello'       |
| is not | 不是         | 3 is not 5               |
| in     | 存在         | 5 in [1, 2, 3, 4, 5]     |
| not in | 不存在       | 2 not in [1, 2, 3, 4, 5] |

**注意**：

1.is，is not对比的是两个变量的内存地址，即是不是自身。

2.==，!=对比的是两个变量的值

3.比较的两个变量：地址不可变（str）则is和=等价；地址可变（list，dict，tuple）则不等价

**运算符优先级：**

与C++类似：一元》二元（算术）》移位》位运算》逻辑运算

**变量命名：**

与C++类似：字母、数字、下划线，不能以数字开头

**数据类型与转换**

```python
a = 1031
print(a, type(a))# 1031 <class 'int'>
print(bin(a)) # 0b10000000111
print(a.bit_length()) # 11
```

python里万物皆对象（object），包括数据类型，有相应的属性(attribute)和方法(methods)。

bool(x)，x只要不是整型0，浮点型0.0，空的容器变量，就是True,否则就是False。

**print函数**

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

将对象object以字符串的形式格式化输出到流文件对象File里,可以是多个对象。

- 关键字参数`sep`是实现分隔符，比如多个参数输出时想要输出中间的分隔字符；
- 关键字参数`end`是输出结束时的字符，默认是换行符`\n`；
- 关键字参数`file`是定义流输出的文件，可以是标准的系统输出`sys.stdout`，也可以重定义为别的文件；
- 关键字参数`flush`是立即把内容输出到流文件，不作缓存。

```python
shoplist = ['apple', 'mango', 'carrot', 'banana']
for item in shoplist:
 print(item)
# apple
# mango
# carrot
# banana
for item in shoplist:
 print(item, end='&')
# apple&mango&carrot&banana&
for item in shoplist:
 print(item, 'another string', sep='&')
# apple&another string
# mango&another string
# carrot&another string
# banana&another string
#我才发现py里面字符串是用单引号。。。。
```

**练习题**

1. 怎样对python中的代码进行注释？

   单行注释#，多行注释三个'或者"


2. python有哪些运算符，这些运算符的优先级是怎样的？

   算术运算符、比较运算符、逻辑运算符、位运算符

   一元》二元（算术）》移位》位运算》逻辑

3. python 中 `is`, `is not` 与 `==`, `!=` 的区别是什么？

   `is`, `is not`对比的是两个变量的内存地址； `==`, `!=` 对比的是两个变量的值

4. python 中包含哪些数据类型？这些数据类型之间如何转换？

    int整型，float浮点型，bool布尔型

   1. 转换为整型int(x,base=10)
   2. 转换成字符串str(object='')
   3. 转换成浮点型float(x)

PS:头一回笔记使用Markdown这种格式，有点不太适应写法。。过两天应该就好了，话说Typora，写作预览合一，值得推荐。
#  位运算（与C++类似）
二进制有三种表示形式：原码、反码、补码，计算机内部用补码来表示。
|二进制表示形式 | 正数      | 反数                     |
| ------   | ------------ | ------------------------ |
| 原码     | 二进制表示 | 二进制表示  |
| 反码     | 即原码        | 符号位不变，其余位取反    |
| 补码     | 即原码        | 反码+1                   |

按位非~，按位I与&，按位或|，按位异或^，按位左移num<<i,按位右移num>>i
```python
print(bin(3))  # 0b11
print(bin(-3))  # -0b1
```
* Python中bin一个负数（十进制表示），输出的是它的原码的二进制表示加上个负号，巨坑。
* Python中的整型是补码形式存储的。
* Python中整型是不限制长度的不会超范围溢出

**练习题**<br>
leetcode 习题 136. 只出现一次的数字
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。
尝试使用位运算解决此题。

---
* 交换律：a ^ b ^ c <=> a ^ c ^ b
* 相同的数异或为0: n ^ n => 0
* 任何数于0异或为任何数 0 ^ n => n

var a = [2,3,2,4,4]
2 ^ 3 ^ 2 ^ 4 ^ 4等价于 2 ^ 2 ^ 4 ^ 4 ^ 3 => 0 ^ 0 ^3 => 3
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        result=0
        for i in nums:
            result=result^i
        return result    
 ```
