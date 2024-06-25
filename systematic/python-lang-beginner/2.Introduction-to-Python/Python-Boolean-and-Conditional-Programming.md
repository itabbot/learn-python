# Python 布尔和条件编程<!-- omit in toc -->

- [1. 什么是布尔值？](#1-什么是布尔值)
- [2. 条件语句](#2-条件语句)
- [3. 比较运算符和逻辑运算符](#3-比较运算符和逻辑运算符)
- [4. 比较 Python 中的不同类型](#4-比较-python-中的不同类型)

## 1. 什么是布尔值？

布尔值是最简单的数据类型。它是 “非此即彼”，要么是真（True），要么是假（False）。

在计算机科学中，布尔值被广泛使用，这与计算机内部的工作方式有关，计算机内部的许多操作都归结为简单的 “真或假”。值得注意的是，在 Python 中，布尔值以大写字母开头：True 或 False。这与大多数其他以小写字母开头的编程语言不同。

## 2. 条件语句

在 Python 中，我们将布尔值与条件语句结合使用来控制程序流程：

```python
# 仅有 if
>>> door_is_locked = True
>>> if door_is_locked:
...     print("Mum, open the door!")
...
Mum, open the door!

# 有 if 和 else
>>> door_is_locked = False
>>> if door_is_locked:
...     print("Mum, open the door!")
... else:
...     print("Let's go inside")
...
Let's go inside
```

## 3. 比较运算符和逻辑运算符

条件语句的能力是计算机运转的关键，它们使软件变得智能，并允许它根据外部输入改变其行为。

| 比较运算符 | 说明       |
| ---------- | ---------- |
| `>`        | 大于       |
| `<`        | 小于       |
| `>=`       | 大于或等于 |
| `<=`       | 小于或等于 |
| `==`       | 等于       |
| `!=`       | 不等于     |

```python
>>> 2 > 1
True
>>> 2 < 1
False
>>> 2 < 3 < 4 < 5 < 6
True
>>> 2 < 3 > 2
True
>>> 3 <= 3
True
>>> 3 >= 2
True
>>> 2 == 2
True
>>> 4 != 5
True
>>> 'a' == 'a'
True
>>> 'a' > 'b'
False
```

| 逻辑运算符 | 说明 |
| ---------- | ---- |
| `and`      | 且   |
| `or`       | 或   |
| `not`      | 非   |

```python
>>> not True
False
>>> not False
True
>>> True and True
True
>>> True and False
False
```

## 4. 比较 Python 中的不同类型

当你尝试比较不同的类型时，你经常会遇到错误。假设你想比较一个整数和一个字符串：

```python
>>> 1 < 'a'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: '<' not supported between instances of 'int' and 'str'
>>>
```

这就是 Python 告诉你它不能将整数与字符串进行比较的方式。但有些类型可以混合搭配。我不建议这样做，因为它会使你的代码难以理解，但为了演示，让我们比较一个布尔值和一个整数：

```python
>>> True == 1
True
>>> False == 0
True
>>> True + True
2
>>> False + False
0
>>> False + True
1
>>> True + 3
4
```
