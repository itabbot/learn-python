# Python For 循环和 While 循环<!-- omit in toc -->

- [1. 概述](#1-概述)
- [2. For 循环](#2-for-循环)
- [3. While 循环](#3-while-循环)

## 1. 概述

控制程序流程除了条件语句，另一种方法是使用 Python for 循环或 Python while 循环。本质上，循环允许您重复一段代码。

## 2. For 循环

Python 中 for 循环的语法如下。for 循环遍历可迭代对象（iterable），每次迭代时，会逐个将其成员赋值给 variable，此变量存在且只能在循环内使用。一旦没有剩余元素，循环就会停止，程序将继续执行下一行代码。

```
for <variable> in <iterable>:
    ... do something with variable
```

比如：

```python
# 文本字符串是可迭代的
>>> for letter in 'Hello':
...     print(letter)
...
H
e
l
l
o

# 迭代列表
>>> mylist = [1, 'a', 'Hello']
>>> for item in mylist:
...     print(item)
...
1
a
Hello
```

## 3. While 循环

Python 中 while 循环的语法如下。

```
while <expression evaluates to True>:
    do something
```

可以理解为：当这个表达式（expression）的计算结果为 True 时，继续执行下面的操作。比如：

```python
>>> i = 1
>>> while i <= 4:
...     print(i)
...     i = i + 1
...
1
2
3
4
```
