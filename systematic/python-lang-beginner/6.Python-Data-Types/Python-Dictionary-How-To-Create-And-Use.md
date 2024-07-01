# Python 字典：如何创建和使用<!-- omit in toc -->

- [1. 创建 Python 字典](#1-创建-python-字典)
- [2. 访问和删除键值对](#2-访问和删除键值对)
- [3. 覆盖字典条目](#3-覆盖字典条目)
- [4. 访问不存在的键](#4-访问不存在的键)
- [5. 有效的字典值](#5-有效的字典值)
- [6. 有效的字典键](#6-有效的字典键)
- [7. 创建 Python 字典的更多方法](#7-创建-python-字典的更多方法)
- [8. 检查 Python 字典中是否存在某个键](#8-检查-python-字典中是否存在某个键)
- [9. 获取 Python 字典的长度](#9-获取-python-字典的长度)
- [10. 字典视图对象](#10-字典视图对象)
  - [10.1. `dict.keys()` 和 `dict.values()`](#101-dictkeys-和-dictvalues)
  - [10.2. `dict.items()`](#102-dictitems)
- [11. 合并词典](#11-合并词典)
- [12. 比较 Python 字典](#12-比较-python-字典)

## 1. 创建 Python 字典

字典是使用花括号创建的。在这些花括号内，我们可以添加一个或多个键值对，添加多个键值对时，键值对之间用逗号分隔。例如：

```py
>>> phone_numbers = { 'Jack': '070-02222748',
                      'Pete': '010-2488634' }
>>> my_empty_dict = { }
>>> phone_numbers['Jack']
'070-02222748'
>>> my_empty_dict
{}
```

## 2. 访问和删除键值对

访问和删除键值对：

```py
>>> phone_numbers = { 'Jack': '070-02222748', 'Pete': '010-2488634' }

# 添加键值对
>>> phone_numbers['Eric'] = '06-10101010'

# 删除键值对
>>> del(phone_numbers['Jack'])

>>> phone_numbers
{'Pete': '010-2488634', 'Eric': '06-10101010'}
```

从字典中检索单个值的另一种方法是使用 `s` 方法。优点是什么？如果未找到键，它将返回默认值 `None`。您也可以指定自己的默认值。

```py
>>> config = { 'host': 'example.org' }
>>> config.get('port', 80)
80
>>> config.get('schema')
>>>
```

## 3. 覆盖字典条目

要覆盖条目，只需为其分配一个新值即可。您无需先执行 `del()` 操作。例如：

```py
>>> phone_numbers = { 'Jack': '070-02222748',
                      'Pete': '010-2488634' }
>>> phone_numbers['Jack'] = '1234567'
```

## 4. 访问不存在的键

访问不存在的键，则会抛出 KeyError 异常：

```py
>>> phone_numbers['lisa']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'lisa'
```

## 5. 有效的字典值

可以将任何东西放入字典中。不限于数字或字符串。事实上，您可以将字典和 Python 列表放入字典中，并以非常自然的方式访问嵌套值：

```py
>>> a = { 'sub_dict': { 'b': True },
          'mylist': [100, 200, 300] }
>>> a['sub_dict']['b']
True
>>> a['mylist'][0]
100
```

## 6. 有效的字典键

你也可以对字典键进行任意设置。唯一的要求是键必须是可哈希的。可变类型（如列表、字典和集合）将不起作用，并会导错误。

```py
>>> my_dictionary = { int: 1, float: 2, dict: 3 }
>>> my_dictionary[dict]
3
>>> class P:
...     pass
...
>>> my_dictionary[P]=1
>>> p = P()
>>> my_dictionary[p]=2
```

## 7. 创建 Python 字典的更多方法

使用 `dict()` 函数根据键值对（元组）的序列或列表构建字典：

```py
>>> dict([ ('Jack', '070-02222748'),
           ('Pete', '010-2488634'),
           ('Eric', '06-10101010') ])
{'Jack': '070-02222748', 'Pete': '010-2488634', 'Eric': '06-10101010'}
```

使用 `dict.fromkeys(keys, value)` 方法根据 keys 提供给它的列表创建一个新字典。所有元素的值都将设置为提供的 value，或者 None（如果您不提供值）。

```py
>>> names = ['Eric', 'Martha', 'Ellen']
>>> phone_numbers = dict.fromkeys(names, None)
>>> phone_numbers
{'Ellen': None, 'Eric': None, 'Martha': None}
```

还可以将 JSON 数据解码为字典，如下所示：

```py
>>> import json
>>> jsonstring = '{ "name": "erik", "age": 38, "married": true}'
>>> json.loads(jsonstring)
{'name': 'erik', 'age': 38, 'married': True}
```

## 8. 检查 Python 字典中是否存在某个键

您可以使用 `in` 和 `not in` 关键字检查字典中是否存在某个键：

```py
>>> 'Jack' in phone_numbers
True
>>> 'Jack' not in phone_numbers
False
```

## 9. 获取 Python 字典的长度

```py
>>> phone_numbers = { 'Jack': '070-02222748',
                      'Pete': '010-2488634',
                      'Eric': '06-10101010' }
>>> len(phone_numbers)
3
```

## 10. 字典视图对象

一些内置字典方法会返回一个视图对象，提供字典键和值的窗口。在开始使用此类视图对象之前，您需要了解一个重要概念：视图对象中的值会随着字典内容的变化而变化。

### 10.1. `dict.keys()` 和 `dict.values()`

```py
phone_numbers = { 'Jack': '070-02222748',
                  'Pete': '010-2488634',
                  'Eric': '06-10101010' }

# 获取所有键
names = phone_numbers.keys()
# 获取所有值
numbers = phone_numbers.values()
# 改变源字典
phone_numbers['Linda'] = '030-987612312'

# 打印了新增的键值对
# dict_keys(['Jack', 'Pete', 'Eric', 'Linda'])
# dict_values(['070-02222748', '010-2488634', '06-10101010', '030-987612312'])
print(names)
print(numbers)

# 循环打印值
# 070-02222748
# 010-2488634
# 06-10101010
# 030-987612312
for number in numbers:
    print(number)
```

### 10.2. `dict.items()`

字典的方法 `items()` 返回一个可迭代的视图对象，提供键和值，如下所示。您可以使用简单的 Python for 循环遍历此对象：

```py
>>> phone_numbers.items()
dict_items([('Jack', '070-02222748'),
            ('Pete', '010-2488634'),
            ('Eric', '06-10101010')])
>>> for name, phonenr in phone_numbers.items():
...     print(name, ":", phonenr)
...
Jack : 070-02222748
Pete : 010-2488634
Eric : 06-10101010
```

## 11. 合并词典

如果您运行的是 Python 3.9 或更高版本，则可以使用新引入的字典合并运算符 “|”：

```py
dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}
print(dict1 | dict2)
# {'a': 1, 'b': 3, 'c': 4}
```

也可以使用以下方法合并两个字典：

```py
dict1 = { 'a': 1, 'b': 2 }
dict2 = { 'b': 3, 'c': 4 }
merged = { **dict1, **dict2 }
print (merged)
# {'a': 1, 'b': 3, 'c': 4}
```

## 12. 比较 Python 字典

如果需要比较两个字典，可以使用这样的比较运算符：

```py
>>> first_dict  = { 'a': 1, 'b': 2, 'c': 'a string' }
>>> second_dict = { 'a': 1, 'b': 2, 'c': 'a string' }
>>> first_dict == second_dict
True
```

这看起来和听起来都很简单，但事实并非如此！毕竟，字典可以包含任何类型的对象！因此，Python 必须遍历所有键和值并分别进行比较。

您可能想知道，如果字典中的键和值以其他顺序插入，是否相同。让我们检查一下：

```py
>>> first_dict  = { 'a': 1, 'b': 2, 'c': 'a string' }
>>> second_dict  = { 'b': 2, 'a': 1, 'c': 'a string' }
>>> first_dict == second_dict
True
```

需要了解的是：自 Python 3.7 起，字典的顺序保证与插入顺序一致。换句话说，这意味着字典的顺序由您插入项目的顺序决定。
