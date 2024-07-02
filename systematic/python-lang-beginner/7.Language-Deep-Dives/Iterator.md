# 迭代器<!-- omit in toc -->

- [1. 什么是 Python 迭代器](#1-什么是-python-迭代器)
- [2. 为什么迭代器和可迭代对象是独立的对象？](#2-为什么迭代器和可迭代对象是独立的对象)
- [3. 内置 Python 迭代器](#3-内置-python-迭代器)
- [4. 如何使用 Python 迭代器](#4-如何使用-python-迭代器)
  - [4.1. for 循环中的迭代器](#41-for-循环中的迭代器)
  - [4.2. 推导式中的迭代器](#42-推导式中的迭代器)
  - [4.3. 迭代字典键](#43-迭代字典键)
  - [4.4. 迭代字典值](#44-迭代字典值)
  - [4.5. 迭代字典中的键和值](#45-迭代字典中的键和值)
  - [4.6. 将迭代器转换为列表、元组、字典或集合](#46-将迭代器转换为列表元组字典或集合)
  - [4.7. 使用 Python 逐行读取文件](#47-使用-python-逐行读取文件)
- [5. 创建自己的 Python 迭代器](#5-创建自己的-python-迭代器)

## 1. 什么是 Python 迭代器

迭代器和可迭代：

-   迭代器： 一个可迭代的对象，可以使用名为 `__next__` 的方法不断向其请求新元素，直到没有元素为止，此时会引发 StopIteration 异常。
-   可迭代对象： 实现另一个特殊 `__iter__` 方法的对象。此函数返回一个迭代器。

以下演示了它们内部的工作方式：

```py
# 定义一个列表，列表是可迭代对象
my_list = [1, 2]
# 获取其迭代器
my_iterator = my_list.__iter__()
# 不断向其请求新元素
print(my_iterator.__next__())
print(my_iterator.__next__())
print(my_iterator.__next__())

# 输出：
# 1
# 2
# Traceback (most recent call last):
#   File "/root/codes/python-test/test.py", line 9, in <module>
#     print(my_iterator.__next__())
# StopIteration
```

当然，这不是实际使用迭代器的方式。如果需要手动获取迭代器，请使用 `iter()` 函数。如果您需要手动调用 `__next__` 方法，则可以使用 Python 的 `next()` 函数：

```py
my_list = [1, 2]
my_iterator = iter(my_list)

print(next(my_iterator))
print(next(my_iterator))
print(next(my_iterator))

# 输出：
# 1
# 2
# Traceback (most recent call last):
#   File "/root/codes/python-test/test.py", line 6, in <module>
#     print(next(my_iterator))
# StopIteration
```

## 2. 为什么迭代器和可迭代对象是独立的对象？

迭代器和可迭代对象可以是单独的对象，但并非必须如此。没有什么可以阻止我们。如果您愿意，您可以创建一个既是迭代器又是可迭代对象的对象。您只需要实现 `__iter__` 和 `__next__`。

那么，为什么创建该语言的聪明人决定拆分这些概念呢？这与保持状态有关。迭代器需要维护位置信息，例如指向列表等内部数据对象的指针。换句话说：它必须跟踪下一个要返回的元素。

如果可迭代对象本身保持该状态，则您一次只能在一个循环中使用它。否则，其他循环会干扰第一个循环的状态。通过返回具有其自身状态的新迭代器对象，我们就不会遇到这个问题。这很方便，尤其是在处理并发时。

## 3. 内置 Python 迭代器

很多 Python 类型都是可迭代的。以下是 Python 原生的一些可迭代类型：

-   Python 列表
-   Python 集合
-   Python 字典
-   Python 元组
-   范围
-   字符串

## 4. 如何使用 Python 迭代器

### 4.1. for 循环中的迭代器

与其他编程语言不同，for 循环需要可迭代对象：

```py
>>> mystring = "ABC"
>>> for letter in mystring:
...     print(letter)
...
A
B
C

>>> mylist = ['A', 'B', 'C']
>>> for letter in mylist:
...     print(letter)
...
A
B
C
```

### 4.2. 推导式中的迭代器

就像 for 循环一样，推导式也需要一个可迭代对象：

```py
>>> [x for x in 'ABC']
['A', 'B', 'C']
>>> [x for x in [1, 2, 3,4] if x > 2]
[3, 4]
>>>
```

### 4.3. 迭代字典键

Python 字典是可迭代的，因此我们可以循环遍历字典的所有键。字典迭代器仅返回键，而不返回值。以下是示例：

```py
>>> d = {'name': 'Alice', 'age': 23, 'country': 'NL' }
>>> for k in d:
...     print(k)
...
name
age
country
```

### 4.4. 迭代字典值

要迭代 Python 字典值，可以使用 values() 方法：

```py
>>> for k in d.values():
...     print(k)
...
Alice
23
NL
```

### 4.5. 迭代字典中的键和值

```py
>>> for k,v in d.items():
...     print(k, v)
...
name Alice
age 23
country NL

>>> [f'{k}: {v}' for k, v in d.items()]
['name: Alice', 'age: 23', 'country: NL']
```

### 4.6. 将迭代器转换为列表、元组、字典或集合

```py
>>> list(range(1, 4))
[1, 2, 3]
>>> set(range(1, 4))
{1, 2, 3}
>>> tuple(range(1, 4))
(1, 2, 3)
```

### 4.7. 使用 Python 逐行读取文件

```py
with open('cities.txt') as cities:
    for line in cities:
        proccess_city(line)
```

## 5. 创建自己的 Python 迭代器

创建自己的迭代器并没有什么神奇之处。一个返回偶数的简单迭代器类示例：

```py
class EvenNumbers:
    last = 0

    def __iter__(self):
        return self

    def __next__(self):
        self.last += 2
        if self.last > 8:
            raise StopIteration
        return self.last


even_numbers = EvenNumbers()
for num in even_numbers:
    print(num)

# 输出：
# 2
# 4
# 6
# 8
```
