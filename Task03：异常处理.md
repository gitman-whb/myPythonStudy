# 异常处理

异常就是运行期检测到的错误。计算机语言针对可能出现的错误定义了异常类型，某种错误引发对应的异常时，异常处理程序将被启动，从而恢复程序的正常运行。

python有标准异常和标准警告：

BaseException：所有异常的 基类
Exception：常规异常的 基类
其他基本上的对象形式就是‘异常名+Error’
如ArithmeticError：所有数值计算异常的基类

​    OSError：打开文件出错

​    TypeError：类型出错

​    ValueError：数值出错

## 1.try - except 语句

```python
try:
    检测范围
except Exception[as reason]:#Exception异常类型 reason官方的异常理由
    出现异常后的处理代码
```

* 首先执行执行`try`子句，如果没有异常发生，忽略`except`子句，`try`子句执行后结束。
* 如果在执行`try`子句的过程中发生了异常，那么`try`子句余下的部分将被忽略。如果异常的类型和`except`之后的名称相符，那么对应的`except`子句将被执行。最后执行`try`语句之后的代码。
* 如果一个异常没有与任何的`except`匹配，那么这个异常将会传递给上层的`try`中。

一个`try`语句可能包含多个`except`子句，分别来处理不同的特定的异常。最多只有一个分支会被执行。

```python
try:
    int("abc")
    s = 1 + '1'
    f = open('test.txt')
    print(f.read())
    f.close()
except OSError as error:
    print('打开文件出错\n原因是：' + str(error))
except TypeError as error:
    print('类型出错\n原因是：' + str(error))
except ValueError as error:
    print('数值出错\n原因是：' + str(error))

# 数值出错
# 原因是：invalid literal for int() with base 10: 'abc'
```

一个 `except` 子句可以同时处理多个异常，这些异常将被放在一个括号里成为一个元组。

```python
try:
    s = 1 + '1'
    int("abc")
    f = open('test.txt')
    print(f.read())
    f.close()
except (OSError, TypeError, ValueError) as error:
    print('出错了！\n原因是：' + str(error))

# 出错了！
# 原因是：unsupported operand type(s) for +: 'int' and 'str'
```

## 2.try - except - finally 语句

```python
try:
    检测范围
except Exception[as reason]:
    出现异常后的处理代码
finally:
    无论如何都会被执行的代码
```

不管`try`子句里面有没有发生异常，`finally`子句都会执行。

如果一个异常在`try`子句里被抛出，而又没有任何的`except`把它截住，那么这个异常会在`finally`子句执行后被抛出。

```python
def divide(x, y):
    try:
        result = x / y
        print("result is", result)
    except ZeroDivisionError:
        print("division by zero!")
    finally:
        print("executing finally clause")


divide(2, 1)
# result is 2.0
# executing finally clause
divide(2, 0)
# division by zero!
# executing finally clause
divide("2", "1")
# executing finally clause
# TypeError: unsupported operand type(s) for /: 'str' and 'str'
```

```python
try:
    检测范围
except:
    出现异常后的处理代码
else:
    如果没有异常执行这块代码
```

## 3. try - except - else 语句

如果在`try`子句执行时没有发生异常，Python将执行`else`子句。

```python
try:
    检测范围
except:
    出现异常后的处理代码
else:
    如果没有异常执行这块代码
```

使用`except`而不带任何异常类型，这不是一个很好的方式，我们不能通过该程序识别出具体的异常信息，因为它捕获所有的异常。

```python
try:
    检测范围
except(Exception1[, Exception2[,...ExceptionN]]]):
   发生以上多个异常中的一个，执行这块代码
else:
    如果没有异常执行这块代码
```

```python
try:
    fh = open("testfile", "w")
    fh.write("这是一个测试文件，用于测试异常!!")
except IOError:
    print("Error: 没有找到文件或读取文件失败")
else:
    print("内容写入文件成功")
    fh.close()

# 内容写入文件成功
```

## 4. raise语句

Python 使用`raise`语句抛出一个指定的异常。

【例子】

```python
try:
    raise NameError('HiThere')
except NameError:
    print('An exception flew by!')
    
# An exception flew by!
```

**练习题**

猜数字游戏

题目描述:

电脑产生一个零到100之间的随机数字，然后让用户来猜，如果用户猜的数字比这个数字大，提示太大，否则提示太小，当用户正好猜中电脑会提示，“恭喜你猜到了这个数是…”。在用户每次猜测之前程序会输出用户是第几次猜测，如果用户输入的根本不是一个数字，程序会告诉用户"输入无效"。

(尝试使用try catch异常处理结构对输入情况进行处理)

获取随机数采用random模块。


```python
import random
anwser=random.randint(1,100)
i=1
while True:
    print('这是第%d次猜测'%i)
    try:
        temp = input("请输入数字：")
        guess = int(temp)
    except ValueError:
        print('输入无效')
    else:
        if guess == anwser:
            print('恭喜你猜到了这个数是%d'%anwser)
            break
        elif guess > anwser:
            print('猜大了')
        else:
            print('猜小了')
        i+=1
print('游戏结束')
```

