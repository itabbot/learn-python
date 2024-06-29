# Python 函数：代码重用的基础<!-- omit in toc -->

- [1. Python 中的函数是什么？](#1-python-中的函数是什么)
- [2. 内置函数](#2-内置函数)
- [3. 形参和实参](#3-形参和实参)
- [4. 返回值](#4-返回值)
- [5. 默认值和命名参数](#5-默认值和命名参数)

## 1. Python 中的函数是什么？

函数是程序中命名的部分，用于执行特定任务。Python 中定义函数：

-   使用 def 关键字来定义 Python 函数。
-   使用缩进来区分属于同一组的代码块，缩进相同的连续行属于同一组代码块，以区分函数主体。
-   函数后面必须始终跟一个空行，以表示函数的结束。

关于缩进：

-   在 Python 中，使用四个空格进行缩进是一种良好的风格。整个 Python 社区都是这样做的。
-   如果您按下 TAB 键，Python REPL 和所有合适的编辑器都会自动缩进四个空格。

示例：

```python
>>> def say_hi():
...     print('Hi!')
...
>>> say_hi()
Hi!
```

## 2. 内置函数

Python 内置了一些函数可供直接使用。比如 `print` 函数，它接收参数并将其打印到屏幕上：

```python
>>> print('Hello, readers!')
Hello, readers!
>>> print(1, 2, 3)
1 2 3
```

内置函数是 `len`，它返回传入内容的长度：

```python
>>> mylength = len('Hello')
>>> print(mylength)
5
```

## 3. 形参和实参

函数接受一些值，这些值被分配给变量，我们将这样的变量称为参数（形参）。调用函数时传入的实际值称为实参：

```python
>>> def say_hi(name):
...     print('Hi', name)
...
>>> say_hi('Erik')
Hi Erik
```

具有多个参数的 Python 函数：

```python
>>> def welcome(name, location):
...     print("Hi", name, "welcome to", location)
...
>>> welcome('Erik', 'this tutorial')
Hi Erik welcome to this tutorial
```

## 4. 返回值

可以使用关键字 return 为函数返回值：

```python
>>> def add(a, b):
...     return a + b
...
>>> result = add(4, 8)
>>> print(result)
12
```

有返回值的函数可以在任何可以使用表达式的地方使用，比如可以在 if 语句中使用：

```python
>>> if add(1, 1) == 2:
...     print("That's what you'd expect!")
...
That's what you'd expect!
```

空的返回语句：

```python
>>> def optional_greeter(name):
...     if name.startswith('X'):
...             return
...     print('Hi there, ', name)
...
>>> optional_greeter('Xander')
>>> optional_greeter('Aander')
Hi there,  Aander
```

## 5. 默认值和命名参数

Python 能够为函数参数提供默认值：

```python
>>> def welcome(name='learner', location='this tutorial'):
...     print("Hi", name, "welcome to", location)
...
>>> welcome()
Hi learner welcome to this tutorial
>>> welcome(name='John')
Hi John welcome to this tutorial
```

调用 Python 函数时可以显式命名参数，这些参数被称为命名参数，因为我们指定名称和值，而不仅仅是值。由于这些命名参数，我们提供它们的顺序并不重要：

```python
>>> welcome(location='this epic tutorial')
Hi learner welcome to this epic tutorial
>>> welcome(name='John', location='this epic tutorial')
Hi John welcome to this epic tutorial
```
