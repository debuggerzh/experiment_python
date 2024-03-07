# 内置函数

### callable

如果参数 _object_ 是可调用的就返回 [`True`](https://docs.python.org/zh-cn/3/library/constants.html#True)，否则返回 [`False`](https://docs.python.org/zh-cn/3/library/constants.html#False)。 如果返回 `True`，调用仍可能失败，但如果返回 `False`，则调用 _object_ 将肯定不会成功。&#x20;

{% hint style="info" %}
请注意类是可调用的（调用类将返回一个新的实例）；

如果实例所属的类实现了 `__call__()` 则它就是可调用的。
{% endhint %}

### **sorted**

```
sorted(iterable, key=None, reverse=False)  
```

* iterable -- 可迭代对象。
* key --指定带有**单个参数**的函数，用于从 _iterable_ 的每个元素中提取用于比较的键
* reverse -- 排序规则，reverse = True 降序 ， reverse = False 升序（默认）。

返回排序后的**列表**。内置的 [`sorted()`](https://docs.python.org/zh-cn/3/library/functions.html#sorted) 确保是稳定的。 如果一个排序确保不会改变比较结果相等的元素的相对顺序就称其为稳定的。

### **reversed**

reversed() 函数返回反向的**迭代器**对象。

```
alph = ["a", "b", "c", "d"]ralph = reversed(alph)for x in ralph:  print(x)# d# c# b# a
```

### **repr**

repr() 函数将对象转化为供**解释器**读取的形式。

**语法**

以下是 repr() 方法的语法:

```
repr(object)
```

**参数**

* object -- 对象。

**返回值**

返回一个对象的 string 格式。

### **eval**

```
eval(expression[, globals[, locals]])
```

实参是一个字符串，以及可选的 globals 和 locals。

表达式解析参数 _expression_ 并作为 Python 表达式进行求值（从技术上说是一个条件列表），采用 _globals_ 和 _locals_ 字典作为全局和局部命名空间。

如果给出的源数据是个字符串，那么其前后的空格和制表符将被剔除。

通常情况下`obj==eval(repr(obj))`这个等式是成立的。

**用法**

1.  可以直接用来提取用户输入的多个值。

    ```
    a, b = eval(input('请输入逗号隔开的两个数'))
    ```

    输入：**10,5**，得到 **a=10，b=5**。
2.  eval() 函数可将看起来像列表的字符串重新转换为列表。

    ```
    zifu=" ['1709020230', '1707030416', '0', '0', '0']  "​ls = eval(zifu)
    ```

### **chr**

chr() 用一个整数作参数，返回一个对应的字符。

**语法**

以下是 chr() 方法的语法:

```
chr(i)
```

**参数**

* i -- 可以是 10 进制也可以是 16 进制的形式的数字，数字范围为 0 到 1,114,111 (16 进制为0x10FFFF)。

**返回值**

返回值是当前整数对应的 ASCII 字符。

### **ord**

ord() 函数是 chr() 函数（对于 8 位的 ASCII 字符串）的配对函数，它以一个字符串（Unicode 字符）作为参数，返回对应的 ASCII 数值，或者 Unicode 数值。

**语法**

以下是 ord() 方法的语法:

```
ord(c)
```

**参数**

* c -- 字符。

**返回值**

返回值是对应的十进制整数。

### zip

`zip(`_`*iterables`_`,`` `_`strict=False`_`)`

在多个迭代器上并行迭代，从每个迭代器返回一个数据项组成元组。

示例:

```python
>>> for item in zip([1, 2, 3], ['sugar', 'spice', 'everything nice']):
...     print(item)
...
(1, 'sugar')
(2, 'spice')
(3, 'everything nice')
```

更正式的说法： [`zip()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=all#zip) 返回元组的迭代器，其中第 _i_ 个元组包含的是每个参数迭代器的第 _i_ 个元素。

不妨换一种方式认识 [`zip()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=all#zip) ：它会把行变成列，把列变成行。这类似于 [矩阵转置](https://en.wikipedia.org/wiki/Transpose) 。

*   默认情况下，[`zip()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=all#zip) 在最短的迭代完成后停止。较长可迭代对象中的剩余项将被忽略，结果会裁切至最短可迭代对象的长度：

    ```
    >>> list(zip(range(3), ['fee', 'fi', 'fo', 'fum']))
    [(0, 'fee'), (1, 'fi'), (2, 'fo')]
    ```
* 通常 [`zip()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=all#zip) 用于可迭代对象等长的情况下。这时建议用 `strict=True` 的选项。输出与普通的 [`zip()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=all#zip) 相同。

对于`zip(args)`这个函数，Python还提供了一种逆操作。例如，我们有

```python
result = zip(a, b)
```

那么，只要调用

```python
a, b = zip(*result)  #前面加*号，事实上*号也是一个特殊的运算符，叫解包运算符
```

就可以得到原来的`a`和`b`了。

### enumerate

`enumerate(`_`iterable`_`,`` `_`start=0`_`)`

返回一个枚举对象。_iterable_ 必须是一个序列或 [iterator](https://docs.python.org/zh-cn/3/glossary.html#term-iterator)，或其他支持迭代的对象。 [`enumerate()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=all#enumerate) 返回的迭代器的 [`__next__()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#iterator.\_\_next\_\_) 方法返回一个元组，里面包含一个计数值（从 _start_ 开始，默认为 0）和通过迭代 _iterable_ 获得的值。

等价于:

```
def enumerate(sequence, start=0):
    n = start
    for elem in sequence:
        yield n, elem
        n += 1
```

### all

`all(`_`iterable`_`)`

如果 _iterable_ 的所有元素均为真值（或可迭代对象为空）则返回 `True` 。 等价于：

```python
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True
```

##
