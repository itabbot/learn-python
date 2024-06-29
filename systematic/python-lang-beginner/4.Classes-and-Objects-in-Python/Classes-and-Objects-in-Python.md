# Python 中的类和对象<!-- omit in toc -->

- [1. Python 对象底层解析](#1-python-对象底层解析)
- [2. 什么是 Python 对象？](#2-什么是-python-对象)
- [3. 什么是 Python 类？](#3-什么是-python-类)
- [4. 创建 Python 类](#4-创建-python-类)
- [5. 创建 Python 对象](#5-创建-python-对象)
- [6. Python 中的 self 是什么？](#6-python-中的-self-是什么)
- [7. 创建多个 Python 对象](#7-创建多个-python-对象)

## 1. Python 对象底层解析

您可能知道内置 `len()` 函数，它只是返回您提供的对象的长度。但是，比如说数字 5 的长度是多少？让我们问 Python：

```Python
>>> len(5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: object of type 'int' has no len()
```

这个错误描述了 Python 内部的工作方式。Python 告诉我们 5 是一个对象，并且它没有 `len()` 方法。

在 Python 中，一切都是对象。字符串、布尔值、数字，甚至 Python 函数都是对象。我们使用内置函数 `dir()` 来检查数字 5，它用于返回指定对象的属性和方法列表，它们是任何数字类型对象的一部分：

```Python
>>> dir(5)
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'as_integer_ratio', 'bit_count', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
```

可以看到其中有一些包含下划线的奇怪命名函数，这些称为魔术方法，例如 `__abs__`。如果仔细观察，您会发现 int 类型的对象并没有 `__len__` 魔术方法。这就是 `len()` 函数知道数字没有长度的原因。`len()` 所做的就是调用对象上的 `__len__()` 方法。这也是 Python 抛出 “类型为 'int' 的对象没有 len()” 的原因。

字符串确实有长度，所以字符串一定有 `__len__` 方法吗？让我们来找出答案：

```Python
>>> dir("test")
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'removeprefix', 'removesuffix', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```

是的，就是这样的。由于这是一个方法，我们也可以调用它：

```Python
# 这相当于 len("test")
>>> "test".__len__()
4
```

## 2. 什么是 Python 对象？

Python 对象是数据（变量）和操作该数据的方法的集合，由 Python 类定义。

对象和面向对象编程是 20 世纪 90 年代初流行的概念。早期的计算机语言（如 C）没有对象的概念。然而，事实证明，对象是人类易于理解的范式。对象可用于模拟许多现实生活中的概念和情况。如今，大多数新语言都具有对象的概念。因此，您将要学习的内容在概念上也将适用于其他语言：这是基础计算机科学。

## 3. 什么是 Python 类？

对象是 Python 语言的构建块，因此您也可以自己创建对象，这很合乎逻辑。如果您想创建自己的对象类型，首先需要定义其方法以及它可以容纳哪些数据。这个蓝图称为类。

所有 Python 对象都基于类。当我们创建一个对象时，我们称之为 “创建类的实例”。字符串、数字甚至布尔值也是类的实例。让我们使用内置函数进行探索：

```python
>>> type('a')
<class 'str'>
>>> type(1)
<class 'int'>
>>> type(True)
<class 'bool'>
```

显然，有名为 str、 int 和 bool 的类，这些是 Python 的一些原生类。

## 4. 创建 Python 类

比如创建一个代表汽车的 Python 类：

```python
# 可复制粘贴到 Python REPL
class Car:
    speed = 0
    started = False
    def start(self):
        self.started = True
        print("Car started, let's ride!")
    def increase_speed(self, delta):
        if self.started:
            self.speed = self.speed + delta
            print('Vrooooom!')
        else:
            print("You need to start the car first")
    def stop(self):
        self.speed = 0
        print('Halting')
```

## 5. 创建 Python 对象

使用上述的 Car 类创建 Python 对象：

```python
>>> car = Car()
>>> car.increase_speed(10)
You need to start the car first
>>> car.start()
Car started, let's ride!
>>> car.increase_speed(40)
Vrooooom!
```

## 6. Python 中的 self 是什么？

是这样的：

-   当我们调用 Python 对象上的方法时，Python 会自动填充第一个变量，按照惯例我们称之为 self。
-   第一个变量是对对象本身的引用，因此得名。
-   我们可以使用该变量来引用该对象的其他实例变量和函数，如 self.speed 和 self.start()。

因此，只有在 Python 类定义中，我们才使用 self 来引用属于实例的变量。比如要修改属于类的变量 started，我们使用 self.started 而不仅仅是 started。通过使用 self，可以非常清楚地表明，我们操作的是属于此实例的变量，而不是在对象外部定义且恰好具有相同名称的其他变量。

## 7. 创建多个 Python 对象

由于 Python 类只是一个蓝图，因此你可以使用它来创建多个对象，就像你可以制造多辆外观相同的汽车一样。它们的行为都很相似，但它们都有自己的数据，并且不会在对象之间共享：

```python
>>> car1 = Car()
>>> car2 = Car()
>>> id(car1)
139771129539104
>>> id(car2)
139771129539160
```

我们在这里创建了两个汽车对象，car1 和 car2，并使用内置方法 `id()` 获取它们的 id。Python 中的每个对象都有一个唯一的标识符，所以我们只是证明了我们从同一个类创建了两个不同的对象。我们可以独立使用它们：

```python
>>> car1.start()
Car started, let's ride!
>>> car1.increase_speed(10)
Vrooooom!
>>> car1.speed
10
>>> car2.speed
0
```
