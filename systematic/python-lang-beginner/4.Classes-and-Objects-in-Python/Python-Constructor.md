# Python 构造方法<!-- omit in toc -->

- [1. 默认构造方法](#1-默认构造方法)
- [2. 创建你自己的 Python 构造方法](#2-创建你自己的-python-构造方法)

## 1. 默认构造方法

构造方法是在创建对象时自动调用的方法。每个类都默认有一个构造方法，名为 `__init__`，它构造并初始化对象。

```python
# 这会自动调用 Car 类的构造方法
car = Car()
```

## 2. 创建你自己的 Python 构造方法

我们可以重写该 `__init__` 方法，通过接受参数赋予它额外的能力。比如：

```Python
# 可复制粘贴到 Python REPL
class Car:
    def __init__(self, started = False, speed = 0):
        self.started = started
        self.speed = speed
    def start(self):
        self.started = True
        print("Car started, let's ride!")
    def increase_speed(self, delta):
        if self.started:
            self.speed = self.speed + delta
            print("Vrooooom!")
        else:
            print("You need to start the car first")
    def stop(self):
        self.speed = 0
```

我们的自定义 Python 构造函数具有带有默认值的命名参数，因此我们可以通过多种方式创建该类的实例：

```Python
>>> c1 = Car()
>>> c2 = Car(True)
>>> c3 = Car(True, 50)
>>> c4 = Car(started=True, speed=40)
```
