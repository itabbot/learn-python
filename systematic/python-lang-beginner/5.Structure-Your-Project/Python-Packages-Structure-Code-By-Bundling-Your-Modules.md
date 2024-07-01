# Python 包：通过捆绑模块来构建代码<!-- omit in toc -->

- [1. 什么是 Python 包？](#1-什么是-python-包)
- [2. Python 包中的 `__init__.py` 是什么？](#2-python-包中的-__init__py-是什么)
- [3. 在 `__init__.py` 中导入模块](#3-在-__init__py-中导入模块)
- [4. 使用 `__main__.py` 创建可运行的包](#4-使用-__main__py-创建可运行的包)
- [5. 模块与包](#5-模块与包)

## 1. 什么是 Python 包？

Python 包是一个包含零个或多个 Python 模块的目录。且每个包始终包含一个名为 `__init__.py` 的特殊文件。比如，包含两个模块的简单 Python 包的结构如下：

```
.
└── package_name
    ├── __init__.py
    ├── module1.py
    └── module2.py
```

Python 包可以包含子包，子包也是包含模块和 `__init__.py` 的目录。比如带有子包的包的结构：

```
.
└── package_name
    ├── __init__.py
    ├── subpackage1
    |   ├── __init__.py
    |   └── module1.py
    └── subpackage2
        ├── __init__.py
        └── module2.py
```

## 2. Python 包中的 `__init__.py` 是什么？

该 `__init__.py` 文件是一个特殊文件，在导入包时始终会执行。如果导入子包时，父级的 `__init__.py` 文件也会被执行，且按照由外到内的顺序执行。

例如这样的包结构：

```
.
└── package1
    ├── __init__.py
    ├── module1.py
    └── package2
        ├── __init__.py
        ├── module2.py
        └── package3
            ├── __init__.py
            └── module3.py
```

在每个 `__init__.py` 中打印了模块名，然后：

```py
>>> import package1.package2.package3
package1
package2
package3
```

## 3. 在 `__init__.py` 中导入模块

这是 Python 中的常见模式。最好在 `__init__.py` 文件中导入所需的所有模块。

## 4. 使用 `__main__.py` 创建可运行的包

可以使用此命令来运行包或包中的模块：

```py
python -m <包名或模块名>
```

运行包中的模块，比如：

```
python -m package1.module1
```

运行包则需要在包的根目录创建一个`__main__.py` 文件，运行包时会运作此文件：

```
python -m package1
```

## 5. 模块与包

总结一下 Python 包以及 Python 模块。经常出现的一个问题是：模块和包有什么区别？

-   模块始终是一个单独的文件，而包可以包含多个模块。
-   模块用于捆绑 Python 函数、类、常量以及任何您想要重复使用的内容。而包则捆绑模块。
-   模块可以独立存在，不需要成为包的一部分，而包需要模块才有用。
-   包和模块共同构成了组织代码的强大方式。
