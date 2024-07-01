# Python 继承<!-- omit in toc -->

- [1. Python 中的继承](#1-python-中的继承)
- [2. 覆盖构造方法](#2-覆盖构造方法)
- [3. 覆盖其他方法](#3-覆盖其他方法)

## 1. Python 中的继承

每个类都有一个构造方法（`__init__`），即使你没有定义它？这是因为每个类都继承自 Python 中最基本的类，`object`：

```py
>>> dir(object)
['__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__']
```

类可以从其他类继承属性和方法。例如，我们可以将通用的方法和变量定义到交通工具类中（Vehicle），然后通过继承的方式重新定义汽车类（Car）：

```py
# 可复制粘贴到 Python REPL

# 交通工具类
class Vehicle:
    def __init__(self, started = False, speed = 0):
        self.started = started
        self.speed = speed
    def start(self):
        self.started = True
        print("Started, let's ride!")
    def stop(self):
        self.speed = 0
    def increase_speed(self, delta):
        if self.started:
            self.speed = self.speed + delta
            print("Vrooooom!")
        else:
            print("You need to start me first")

# 使用继承来重新定义汽车类
# 继承了 Vehicle 类的所有方法和变量，并增加了一个额外的变量和两个方法来操作后备箱
class Car(Vehicle):
    trunk_open = False
    def open_trunk(self):
        self.trunk_open = True
    def close_trunk(self):
        self.trunk_open = False
```

## 2. 覆盖构造方法

可以通过重新定义 `__init__` 方法来覆盖父类的构造方法，不过此时，父类的构造方法将完全不会被调用。如果需要，可以通过 `super()` 来获取父类的引用，并调用父类构造方法。比如：

```py
# 摩托车类（Motorcycle）
class Motorcycle(Vehicle):
    def __init__(self, center_stand_out = False):
        self.center_stand_out = center_stand_out
        super().__init__()
```

## 3. 覆盖其他方法

就像 `__init__` 一样 ，我们也可以重写其他方法。例如：

```py
class Motorcycle(Vehicle):
    def __init__(self, center_stand_out = False):
        self.center_stand_out = center_stand_out
        super().__init__()
    def start(self):
        print("Sorry, out of fuel!")
```
