# 列表理解：列表推导<!-- omit in toc -->

- [1. 前言](#1-前言)
- [2. 什么是列表推导？](#2-什么是列表推导)
- [3. 嵌套列表推导](#3-嵌套列表推导)
- [4. 字典推导\&集合推导](#4-字典推导集合推导)

## 1. 前言

数学中有一个概念叫做集合构造符号，也叫集合推导式。受此原理的启发，Python 提供了列表推导式。事实上，Python 列表推导式是该语言的定义特性之一。它允许我们创建简洁、易读的代码，其性能优于 for 循环或 using 等较丑陋的替代方案 map()。

## 2. 什么是列表推导？

Python 列表推导是一种语言构造。它用于根据现有列表创建 Python 列表。列表推导的基本语法是：

```py
[ <expression> for item in list if <conditional> ]
```

if 语句是可选的，比如这是一个最简单的列表推导：

```py
>>> [x for x in [1, 2, 3, 4]]
[1, 2, 3, 4]
```

if 部分的作用类似于过滤器。如果 if 后面的条件解析为 True，则包含该项目。如果解析为 False，则省略该项目。比如：

```py
>>> [x for x in [1, 2, 3, 4] if x % 2 == 0]
[2, 4]
```

expression 可以是任何有效的 Python 代码，并被视为表达式。例如：

```py
>>> [x + 4 for x in [10, 20]]
[14, 24]
```

稍微复杂的示例：

```py
def some_function(a):
    return (a + 5) / 2

m = [some_function(x) for x in range(8)]
print(m)
# [2.5, 3.0, 3.5, 4.0, 4.5, 5.0, 5.5, 6.0]
```

## 3. 嵌套列表推导

expression 可以是任何有效的 Python 表达式，它也可以是另一个列表推导式。这在你想要创建矩阵时很有用：

```py
>>> m = [[j for j in range(3)] for i in range(4)]
>>> m
[[0, 1, 2], [0, 1, 2], [0, 1, 2], [0, 1, 2]]
```

或者，如果您想展平上面的矩阵：

```py
>>> [value for sublist in m for value in sublist]
[0, 1, 2, 0, 1, 2, 0, 1, 2, 0, 1, 2]
```

相同，但添加更多空格以使其更清晰：

```py
>>> [value
     for sublist in m
     for value in sublist]
[0, 1, 2, 0, 1, 2, 0, 1, 2, 0, 1, 2]
```

## 4. 字典推导&集合推导

Python 集合推导的语法没有太大区别。我们只是使用花括号代替方括号：

```py
{ <expression> for item in set if <conditional> }
```

例如：

```py
>>> {s for s in range(1,5) if s % 2}
{1, 3}
```

字典需要一个键和一个值。唯一的区别是我们在 expression 部分中定义了键和值：

```py
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
```
