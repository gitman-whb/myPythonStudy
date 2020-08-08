**练习题**：

1、打开中文字符的文档时，会出现乱码，Python自带的打开文件是否可以指定文字编码？还是只能用相关函数？

linux使用’utf-8’编码方式，window使用’GBK’编码方式。平台编码（UTF-8）与window平台（GBK）不一样。
可以使用open(encoding=xx)进行转码

2、编写程序查找最长的单词

输入文档: res/test.txt

题目说明:

```python
"""
   
Input file
   test.txt
   
Output file
   ['general-purpose,', 'object-oriented,']
   
"""
def longest_word(filename):
    # your code here
        pass
```

代码实现：

```python
def longest_word(filename):
    f = open(filename, 'r')
    max_list = []
    count = 0
    for each in f:
        split_list = each.split(',')
        for elem in split_list:
            if len(elem) > count:
                count = len(elem)
                if max_list == []:
                    max_list.append(elem)
                else:
                    max_list = []
                    max_list.append(elem)
            elif len(elem) == count:
                max_list.append(elem)
    
    f.close()
    return max_list

longest_word('test.txt')
```

