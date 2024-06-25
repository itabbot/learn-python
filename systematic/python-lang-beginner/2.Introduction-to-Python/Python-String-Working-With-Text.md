# Python 字符串：处理文本<!-- omit in toc -->

- [1. 什么是字符串？](#1-什么是字符串)
- [2. 如何创建字符串](#2-如何创建字符串)
- [3. 单引号还是双引号？](#3-单引号还是双引号)
- [4. 多行字符串](#4-多行字符串)
- [5. 字符串操作](#5-字符串操作)
- [6. 使用 f 字符串进行 Python 字符串格式化](#6-使用-f-字符串进行-python-字符串格式化)

## 1. 什么是字符串？

字符串是字符序列，更简单地说，字符串就是一段文本。字符串不仅仅是 Python 的东西。它是计算机科学中一个众所周知的术语，在大多数其他语言中含义相同。

## 2. 如何创建字符串

Python 字符串需要用引号引起来才能被识别：

```shell
>>> 'Hello, World'
'Hello, World'
```

之前学到的一些运算符也适用于 Python 字符串：

```shell
# 加号运算符将两个 Python 字符串粘合在一起
>>> 'a' + 'b'
'ab'

# 乘法运算符将 Python 字符串重复给定的次数
>>> 'ab' * 4
'abababab'

# 减号运算符不适用于 Python 字符串，会产生错误
>>> 'a' - 'b'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for -: 'str' and 'str'
```

## 3. 单引号还是双引号？

Python 接受使用 “单引号” 或 “双引号” 括住字符串：

```shell
>>> 'a' + 'b'
'ab'
>>> "a" + "b"
'ab'
```

从答案中可以看出，Python REPL 更喜欢单引号。它看起来更清晰，而且 Python 试图尽可能清晰易读。那么为什么它同时支持两者呢？这是因为它允许您使用包含引号的字符串：

```shell
>>> mystring = "It's a string, with a single quote!"
>>> mystring = 'It's a string, with a single quote!'
  File "<stdin>", line 1
    mystring = 'It's a string, with a single quote!'
                   ^
SyntaxError: invalid syntax
```

也可以使用反斜杠转义特殊字符（如引号）：

```shell
>>> mystring = 'It\'s an escaped quote!'
>>> mystring
"It's an escaped quote!"

>>> mystring = "I'm a so-called \"script kiddie\""
>>> mystring
'I\'m a so-called "script kiddie"'
```

## 4. 多行字符串

Python 支持使用三引号创建多行字符串，可以是三个双引号或三个单引号：

```shell
>>> """This is line 1,
... this is line 2,
... this is line 3."""
'This is line 1,\nthis is line 2,\nthis is line 3.'
```

三引号的优点在于，你可以在其中使用单引号和双引号。因此，你可以使用三引号干净地创建包含单引号和双引号的字符串，而无需进行转义：

```shell
>>> line = """He said: "Hello, I've got a question" from the audience"""
```

## 5. 字符串操作

在 REPL 中，有时可以使用自动完成功能。它是否有效取决于您安装 Python 时使用的安装程序以及您使用的操作系统。比如，我们创建一个字符串 mystring，并在下一行输入它的名称和 “.”，然后按两次 TAB 键，会得到一个可以对字符串执行的操作列表：

```shell
>>> mystring = "Hello world"
>>> mystring.
mystring.capitalize()    mystring.isalpha()       mystring.ljust(          mystring.rsplit(
mystring.casefold()      mystring.isascii()       mystring.lower()         mystring.rstrip(
mystring.center(         mystring.isdecimal()     mystring.lstrip(         mystring.split(
mystring.count(          mystring.isdigit()       mystring.maketrans(      mystring.splitlines(
mystring.encode(         mystring.isidentifier()  mystring.partition(      mystring.startswith(
mystring.endswith(       mystring.islower()       mystring.removeprefix(   mystring.strip(
mystring.expandtabs(     mystring.isnumeric()     mystring.removesuffix(   mystring.swapcase()
mystring.find(           mystring.isprintable()   mystring.replace(        mystring.title()
mystring.format(         mystring.isspace()       mystring.rfind(          mystring.translate(
mystring.format_map(     mystring.istitle()       mystring.rindex(         mystring.upper()
mystring.index(          mystring.isupper()       mystring.rjust(          mystring.zfill(
mystring.isalnum()       mystring.join(           mystring.rpartition(
```

一些例子：

```shell
# 获取字符串长度
>>> len("I wonder how long this string will be...")
40
>>> len(mystring)
11

# 拆分字符串
>>> 'Hello world'.split(' ')
['Hello', 'world']

# 替换字符串的部分内容
>>> 'Hello world'.replace('H', 'h')
'hello world'
>>> 'Hello world'.replace('l', '_')
'He__o wor_d
>>> 'Hello world'.replace('world', 'readers')
'Hello readers'
```

## 6. 使用 f 字符串进行 Python 字符串格式化

有时需要合并一些文本字符串或在字符串中使用变量或表达式。有几种方法可以做到这一点，但最现代的方法是使用 f 字符串，它是 “format” 缩写。比如：

```shell
# 使用变量
>>> my_age = 40
>>> f'My age is {my_age}'
My age is 40

# 使用表达式
>>> f'3 + 4 = {3+4}'
'3 + 4 = 7'
>>> my_age = 40
>>> f'My age is, unfortunately, not {my_age-8}'
'My age is, unfortunately, not 32'
```

f 字符串允许我们快速打印变量的名称和内容。这在调试代码时非常有用：

```shell
>>> name = "John"
>>> age = 56
>>> print(f"{name=}, {age=}")
name='John', age=56
```
