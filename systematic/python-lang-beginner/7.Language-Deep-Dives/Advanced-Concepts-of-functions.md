# 函数高级概念<!-- omit in toc -->

- [1. 强制关键字参数](#1-强制关键字参数)
- [2. 使用 `*` 和 `**` 作为函数参数](#2-使用--和--作为函数参数)
- [3. 装饰你的函数](#3-装饰你的函数)
- [4. 匿名函数](#4-匿名函数)

## 1. 强制关键字参数

关键字参数有许多优点：

-   你不需要按照特定的顺序来提供你的参数，重要的是名称，而不是位置。
-   关键字参数提供了清晰度。无需查找函数本身，您通常可以通过查看名称来猜测参数的用途。

可以强制使用关键字参数：

-   在你想要强制作为关键字参数的参数前使用星号。
-   或者，在所有内容之前，强制所有参数为关键字参数。

示例：

```py
>>> def f(a, *, b):
...     print(a, b)
...

>>> f(1, 2)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: f() takes 1 positional argument but 2 were given

>>> f(1, b=2)
1 2
```

```py
>>> def f(*, a, b):
...     print(a, b)
...

>>> f(1, 2)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: f() takes 0 positional arguments but 2 were given

>>> f(a=1, b=2)
1 2
```

## 2. 使用 `*` 和 `**` 作为函数参数

有些函数需要一长串参数。虽然应该完全避免这种情况，例如通过使用数据类，但这并不总是由您决定。在这种情况下，次优选择是创建一个包含所有命名参数的字典，并将其传递给函数。它通常会使您的代码更具可读性。您可以使用前缀解包字典以与命名关键字一起使用 `**` ：

```py
>>> def f(a, b):
...     print(a, b)
...
>>> args = { "a": 1, "b": 2 }
>>> f(**args)
1 2
```

类似地，我们可以使用单个 `*` 来解包列表并将其内容作为位置参数提供给函数：

```py
>>> def f(a, b, c):
...    print(a, b, c)
...
>>> l = [1, 2, 3]
>>> f(*l)
1 2 3
```

## 3. 装饰你的函数

装饰器是函数的包装器，可以以某种方式修改函数的行为。

如下，在 `print_argument` 中，定义了一个包装函数。此函数打印参数和被调用函数的名称。接下来，它执行实际函数并返回其结果，就像定期调用该函数一样。`@print_argument` 我们将装饰器应用于函数。也许不用说：这个装饰器也可以重新用于其他函数。

```py
def print_argument(func):
    def wrapper(the_number):
        print("Argument for", func.__name__, "is", the_number)
        return func(the_number)
    return wrapper
@print_argument
def add_one(x):
    return x + 1
print(add_one(1))

# 输出：
# Argument for add_one is 1
# 2
```

## 4. 匿名函数

有时，命名函数并不值得。例如，当您确定该函数只会使用一次时。对于这种情况，Python 为我们提供了匿名函数，也称为 lambda 函数。

可以将 lambda 函数分配给变量，从而创建一种定义函数的简洁方法：

```py
>>> add_one = lambda x: x + 1
>>> add_one(3)
4
```

当你需要使用函数作为参数时，事情会变得更加有趣。在这种情况下，函数通常只使用一次。你可能知道，map 将函数应用于可迭代对象的所有元素。我们可以在调用 map 时使用 lambda：

```py
>>> numbers = [1, 2, 3, 4]
>>> times_two = map(lambda x: x * 2, numbers)
>>> list(times_two)
[2, 4, 6, 8]
>>>
```
