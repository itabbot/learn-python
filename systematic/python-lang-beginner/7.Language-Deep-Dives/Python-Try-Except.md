# Python 异常处理<!-- omit in toc -->

- [1. 什么是异常？](#1-什么是异常)
- [2. try except](#2-try-except)
- [3. finally 和 else 块](#3-finally-和-else-块)
- [4. 创建自定义异常](#4-创建自定义异常)
- [5. 抛出异常](#5-抛出异常)
- [6. 如何打印 Python 异常](#6-如何打印-python-异常)

## 1. 什么是异常？

异常是程序执行过程中出现的一种情况。这是发生意外情况的信号。Python 用特定类型的对象表示异常。

在 Python 中，所有内置的非系统退出异常都派生自该 Exception 类。异常有自己的描述性名称。例如，如果您尝试将数字除以零，您将得到一个 ZeroDivisionError 异常，它也是该 Exception 类的子类。

## 2. try except

当引发异常时，Python 会停止当前执行流程并开始寻找可以处理该异常的异常处理程序。那么什么是异常处理程序？这就是 try except 语句发挥作用的地方。

-   try： 可以用 try 语句创建一个代码块。这意味着：尝试运行此代码，但可能会发生异常。
-   except： 在 try 块之后，必须跟有一个或多个 except 块。这些 except 块可以捕获异常（事实上，许多其他编程语言使用名为 的语句 catch 而不是 except）。每个 except 块可以处理特定类型的异常。except 块必须从最具体到不太具体进行，否则有些 except 块可能永远不会执行。

比如，我们不能除以零。如果我们这样做，Python 将抛出一个名为的异常 ZeroDivisionError，它是的子类 ArithmeticError：

```py
try:
    print(2/0)
except ZeroDivisionError as e:
    print("You can't divide by zero!", e)
```

```py
# 错误示范
try:
    print(2/0)
except Exception as e:
    print("Exception", e)
except ZeroDivisionError as e:
    # 这里永远不会被执行
    print("You can't divide by zero!", e)
```

## 3. finally 和 else 块

finally 无论是否发生异常，都会执行该块。例如，无论发生什么情况，您都想清理资源以防止内存泄漏：

```py
try:
    f = open("myfile.txt", 'w')
    f.write("Hello World!")
except IOError as e:
    print("An error occurred:", e)
finally:
    print("Closing the file now")
    f.close()
```

else 块仅在未发生异常时执行。

什么时候应该使用 else 块？为什么不直接在 try 块中添加额外的代码？好问题！

根据 Python 手册，使用 else 子句比在 try 子句中添加额外代码更好。但为什么呢？原因是它可以避免意外捕获由 try 和 except 语句保护的代码未引发的异常。我发现它们有点令人困惑，尤其是对于来自其他语言的人来说。

## 4. 创建自定义异常

正如我们之前所学，所有内置的、非系统退出的异常都是从 Exception 类派生的。所有用户定义的异常也应该从该类派生。因此，如果我们想创建自己的异常，我们需要创建 Exception 类的子类。

例如，如果您想要创建一个异常来表示未找到用户，则可以创建一个 UserNotFoundError 异常。其最基本的形式如下：

```py
class UserNotFoundError(Exception):
    pass
```

它继承了 Exception 的所有属性和方法，但我们给它起了一个新名字，以区别于 Exception 类。这样，我们就可以用 except 块专门捕获它。

## 5. 抛出异常

我们知道了一些内置异常以及如何创建自定义异常。我们还知道如何使用 try 和 except 捕获异常。剩下的就是所谓的引发或抛出异常。您可以使用 raise 关键字自行引发异常。

比如：

```py
raise Exception('Error')
```

## 6. 如何打印 Python 异常

只要您正确捕获异常，就可以直接打印异常。您可能已经看过上面的示例。比如：

```py
try:
    ...
except Exception as e:
    print("There was an error: ", e)
```

如果你想打印调用堆栈，就像 Python 在你自己没有捕获异常时所做的那样，你可以导入 traceback 模块：

```py
import traceback
try:
    ...
except Exception:
    traceback.print_exc()
```
