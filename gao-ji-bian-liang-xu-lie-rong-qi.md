---
description: Sequence/Container
---

# 😍 高级变量：序列/容器

## 通用序列操作

| 运算                     | 结果：                                         |
| ---------------------- | ------------------------------------------- |
| `x in s`               | 如果 _s_ 中的某项等于 _x_ 则结果为 `True`，否则为 `False`   |
| `x not in s`           | 如果 _s_ 中的某项等于 _x_ 则结果为 `False`，否则为 `True`   |
| `s + t`                | _s_ 与 _t_ 相拼接                               |
| `s * n` 或 `n * s`      | 相当于 _s_ 与自身进行 _n_ 次拼接                       |
| `s[i]`                 | _s_ 的第 _i_ 项，起始为 0                          |
| `s[i:j]`               | _s_ 从 _i_ 到 _j_ 的切片                         |
| `s[i:j:k]`             | _s_ 从 _i_ 到 _j_ 步长为 _k_ 的切片                 |
| `len(s)`               | _s_ 的长度                                     |
| `min(s)`               | _s_ 的最小项                                    |
| `max(s)`               | _s_ 的最大项                                    |
| `s.index(x[, i[, j]])` | _x_ 在 _s_ 中首次出现项的索引号（索引号在 _i_ 或其后且在 _j_ 之前） |
| `s.count(x)`           | _x_ 在 _s_ 中出现的总次数                           |

## 可变序列操作

| 运算                       | 结果：                                             |
| ------------------------ | ----------------------------------------------- |
| `s[i] = x`               | 将 _s_ 的第 _i_ 项替换为 _x_                           |
| `s[i:j] = t`             | 将 _s_ 从 _i_ 到 _j_ 的切片替换为可迭代对象 _t_ 的内容           |
| `del s[i:j]`             | 等同于 `s[i:j] = []`                               |
| `s[i:j:k] = t`           | 将 `s[i:j:k]` 的元素替换为 _t_ 的元素                     |
| `del s[i:j:k]`           | 从列表中移除 `s[i:j:k]` 的元素                           |
| `s.append(x)`            | 将 _x_ 添加到序列的末尾 (等同于 `s[len(s):len(s)] = [x]`)   |
| `s.clear()`              | 从 _s_ 中移除所有项 (等同于 `del s[:]`)                   |
| `s.copy()`               | 创建 _s_ 的浅拷贝 (等同于 `s[:]`)                        |
| `s.extend(t)` 或 `s += t` | 用 _t_ 的内容扩展 _s_ (基本上等同于 `s[len(s):len(s)] = t`) |
| `s *= n`                 | 使用 _s_ 的内容重复 _n_ 次来对其进行更新                       |
| `s.insert(i, x)`         | 在由 _i_ 给出的索引位置将 _x_ 插入 _s_ (等同于 `s[i:i] = [x]`) |
| `s.pop()` 或 `s.pop(i)`   | 提取在 _i_ 位置上的项，并将其从 _s_ 中移除                      |
| `s.remove(x)`            | 删除 _s_ 中第一个 `s[i]` 等于 _x_ 的项目。                  |
| `s.reverse()`            | 就地将列表中的元素逆序。                                    |

## 列表

列表是最常用的 Python 数据类型，它可以作为一个方括号内的逗号分隔值出现。

列表的数据项不需要具有相同的类型，创建一个列表，只要把逗号分隔的不同的数据项使用方括号括起来即可。列表是经典的**可变容器**。

{% hint style="info" %}
对列表进行切片操作，会生成一个列表的部分**浅复制**。
{% endhint %}

### **list.sort**

原地稳定排序函数。

```
list.sort(key=None, reverse=False)
```

其中key为单参数函数，用于从每个列表元素中提取比较键。

reverse = True 降序， reverse = False 升序（默认值）

无返回值。

**实例**：假设有以下list：

`lst=[1, -2, 10, -12, -4, -5, 9, 2]`

要求排序时正数列前，符号相同则绝对值较大者列前。即输出

`[1, 2, 9, 10, -2, -4, -5, -12]`

使用key参数的简单方法如下：

`lst.sort(key=lambda x : (x < 0, abs(x)))`

## 元组

与列表类似，但元组的元素一经写成即不可修改。

所谓元组的不可变指的是元组所指向的内存中的内容不可变。

事实上，重新赋值的元组会绑定到新的对象，不是修改了原来的对象。

创建元组很简单，只需要在括号中添加元素，并使用逗号隔开即可。创建非空元组可以不加括号。

**注**：元组中只包含一个元素时，需要在元素后面添加逗号 **,** 否则括号会被当作运算符使用

**常用方法**

1. 索引
2. 切片
3. 删除整个元组
4. 求长度
5. 连接
6. 复制
7. 存在性
8. 迭代
9. 转换至元组：`tuple(seq)`

## Range

`range`类型表示不可变的数字序列，通常用于在 `for`循环中循环指定的次数。

```
class range(start=0, stop[, step=1])
```

range 构造器的参数必须为整数。如果 step 为零则会引发 `ValueError`。左闭右开。

range 类型相比常规 list 或 tuple 的优势在于一个 range 对象总是占用固定数量的**较小**内存，不论其所表示的范围有多大（因为它只保存了 start, stop 和 step 值，并会根据需要计算具体单项或子范围的值）。

## 字典

### **定义**

字典是另一种**可变容器**模型，且可存储任意类型对象。

字典的每个键值 **key=>value** 对用冒号 **:** 分割，每个对之间用逗号(**,**)分割，整个字典包括在花括号 **{}** 中 ,格式如下所示

```
dic = {key1 : value1, key2 : value2, key3 : value3 }
```

键必须是**唯一**的，但值则不必。

值可以取任何数据类型，但键必须不可变，所以可以用**数字**，**字符串**或**元组**充当，而用列表就不行。

### **常用方法**

1.  判断key的存在性：`in/not in`操作符

    Python 字典 **in** 操作符用于判断键是否存在于字典中，如果键在字典 `dict`里返回 true，否则返回 false。

    而 **not in** 操作符刚好相反，如果键在字典 `dict`里返回 false，否则返回 true。
2. 由键访问值，可用中括号和`get`两种方法
3. 删除键/字典
4. 清空
5. 求长度
6. 删除键并返回值：`pop(key[,default])`

### **遍历**

```python
xiaoming = {"name": "小明", "age": 18, "gender": True, "height": 1.75}
# 1.可以仅遍历key
for k in xiaoming:
    print(f'{k}:{xiaoming[k]}')
# 2.也可以通过items()方法返回的视图对象进行遍历
for k, v in xiaoming.items():
    print(f'{k}:{v}')
```

## 字符串

字符串是 Python 中最常用的数据类型。我们可以使用引号( **'** 或 **"** )来创建字符串。

Python 不支持单字符类型，单字符在 Python 中也是作为一个字符串使用。

### **转义字符**

<table data-header-hidden><thead><tr><th width="150"></th><th></th><th></th></tr></thead><tbody><tr><td>转义字符</td><td>描述</td><td>实例</td></tr><tr><td>\</td><td>(在行尾时)<strong>续行符</strong></td><td><code>>>> print("line1 \ ... line2 \ ... line3")</code></td></tr><tr><td>\\</td><td>反斜杠符号</td><td><code>>>> print("\\")</code></td></tr><tr><td>\'</td><td>单引号</td><td><code>>>> print('\'') '</code></td></tr><tr><td>\"</td><td>双引号</td><td><code>>>> print("\"") "</code></td></tr><tr><td>\a</td><td>响铃(Alarm)</td><td><code>>>> print("\a")</code>执行后电脑有响声。</td></tr><tr><td>\b</td><td>退格(Backspace)</td><td><code>>>> print("Hello \b World!") Hello World!</code></td></tr><tr><td>\000</td><td>空</td><td><code>>>> print("\000") >>></code></td></tr><tr><td></td><td>换行(new line)</td><td><code>>>> print("\n") >>></code></td></tr><tr><td>\v</td><td>纵向(vertical)制表符</td><td><code>>>> print("Hello \v World!") Hello World! >>></code></td></tr><tr><td>\t</td><td>横向制表符</td><td><code>>>> print("Hello \t World!") Hello World! >>></code></td></tr><tr><td>\r</td><td>回车，将  后面的内容移到字符串开头，并逐一替换开头部分的字符，直至将  后面的内容完全替换完成。</td><td><code>>>> print("Hello\rWorld!") World!</code></td></tr><tr><td>\f</td><td>换页</td><td><code>>>> print("Hello \f World!") Hello World! >>></code></td></tr><tr><td>\yyy</td><td>八进制数，y 代表 0~7 的字符，例如：\012 代表换行。</td><td><code>>>> print("\110\145\154\154\157\40\127\157\162\154\144\41") Hello World!</code></td></tr><tr><td>\xyy</td><td>十六进制数，以 \x 开头，y 代表的字符，例如：\x0a 代表换行</td><td><code>>>> print("\x48\x65\x6c\x6c\x6f\x20\x57\x6f\x72\x6c\x64\x21") Hello World!</code></td></tr></tbody></table>

### **格式化**

#### **%格式化**

在 Python 中，字符串格式化使用与 C 中 printf 函数一样的语法。

| 符   号    | 描述                  |
| -------- | ------------------- |
|       %c |  格式化字符及其ASCII码      |
|       %s |  格式化字符串             |
|       %d |  格式化整数              |
|       %u |  格式化无符号整型           |
|       %o |  格式化无符号八进制数         |
|       %x |  格式化无符号十六进制数        |
|       %X |  格式化无符号十六进制数（大写）    |
|       %f |  格式化浮点数字，可指定小数点后的精度 |
|       %e |  用科学计数法格式化浮点数       |
|       %E |  作用同%e，用科学计数法格式化浮点数 |
|       %g |  %f和%e的简写           |
|       %G |  %f 和 %E 的简写        |
|       %p |  用十六进制数格式化变量的地址     |

**辅助指令符号：**

| 符号    | 功能                                                  |
| ----- | --------------------------------------------------- |
| \*    | 定义宽度或者小数点精度                                         |
| -     | 用做左对齐                                               |
| +     | 在正数前面显示加号( + )                                      |
| \<sp> | 在正数前面显示空格                                           |
| #     | 在八进制数前面显示零('0')，在十六进制前面显示'0x'或者'0X'(取决于用的是'x'还是'X') |
| 0     | 显示的数字前面填充'0'而不是默认的空格                                |
| %     | '%%'输出一个单一的'%'                                      |
| (var) | 映射变量(字典参数)                                          |
| m.n.  | m 是显示的最小总宽度,n 是小数点后的位数(如果可用的话)                      |

#### **`str.format`**

Python2.6 开始，新增了一种格式化字符串的函数 **str.format()**，它增强了字符串格式化的功能。

基本语法是通过 **{}** 和 **:** 来代替以前的 **%** 。该语法在大多数情况下与旧式的 `%` 格式化类似，只是增加了 `{}` 和 `:` 来取代 `%`。 例如，，`'%03.2f'` 可以被改写为 `'{:03.2f}'`。

**简化语法格式如下：**

```
replacement_field ::=  "{" [field_name] ["!" conversion] [":" format_spec] "}"
field_name        ::=  arg_name ("." attribute_name | "[" element_index "]")*
arg_name          ::=  [identifier | digit+]
attribute_name    ::=  identifier
element_index     ::=  digit+ | index_string
index_string      ::=  <any source character except "]"> +
conversion        ::=  "r" | "s" | "a"
```

`field_name`指定了此处字符串的来源。其中arg\_name如果为数字，则它指向一个位置参数，而如果为关键字，则它指向一个命名关键字参数。`'.name'` 形式的表达式会使用 [`getattr(name)`](https://docs.python.org/zh-cn/3/library/functions.html#getattr) 选择命名属性，而 `'[index]'` 形式的表达式会使用 `__getitem__(index)` 执行索引查找。

使用 _conversion_ 字段，可以在格式化之前进行类型强制转换。 通常，格式化值的工作由值本身的 `__format__()` 方法来完成。 但是，在某些情况下最好强制将类型格式化为一个字符串，覆盖其本身的格式化定义。 通过在调用 `__format__()` 之前将值转换为字符串，可以绕过正常的格式化逻辑。

目前支持的转换旗标有三种:

* &#x20;`'!s'` 会对值调用 [`str()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str)
* `'!r'` 调用 [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr) ；
* &#x20;`'!a'` 则调用 [`ascii()`](https://docs.python.org/zh-cn/3/library/functions.html#ascii)。

_format\_spec_ 字段包含值应如何呈现的规格描述，例如**字段宽度**、**对齐**、**填充**、**小数精度**等细节信息。 每种值类型可以定义自己的“格式化迷你语言”或对 _format\_spec_ 的解读方式。

format 函数可以接受不限个参数，位置可以不按顺序。

{% code overflow="wrap" %}
```python
>>>"{} {}".format("hello", "world")    # Version3.1+ 不设置指定位置，按默认顺序
'hello world' 
>>> "{0} {1}".format("hello", "world")  # 设置指定位置
'hello world' 
>>> "{1} {0} {1}".format("hello", "world")  # 设置指定位置
'world hello world'

print("网站名：{name}, 地址 {url}".format(name="菜鸟教程", url="www.runoob.com")) # 通过字典设置参数

site = {"name": "菜鸟教程", "url": "www.runoob.com"}
print("网站名：{name}, 地址 {url}".format(**site)) # 通过列表索引设置参数

my_list = ['菜鸟教程', 'www.runoob.com']
print("网站名：{0[0]}, 地址 {0[1]}".format(my_list))  # "0" 是必须的
```
{% endcode %}

也可以向 **str.format()** 传入对象。

```python
class AssignValue(object):
    def __init__(self, value):
         self.value = value
my_value = AssignValue(6)
print('value 为: {0.value}'.format(my_value))  # "0" 是可选的
```

#### **f-string**

字面量格式化字符串。

**f-string** 格式化字符串以 **f** 开头，后面跟着字符串，字符串中的表达式用大括号 {} 包起来，它会将变量或表达式计算后的值替换进去。

可以指定输出变量的格式，如下所示：

```python
>>> r = 2.5
>>> s = 3.14 * r ** 2
>>> print(f'The area of a circle with radius {r} is {s:.2f}') # 两位小数
The area of a circle with radius 2.5 is 19.62
```

在 Python 3.8 的版本中可以使用 **=** 符号来拼接运算表达式与结果：

```python
>>> x = 1
>>> print(f'{x+1=}')   # Python 3.8
x+1=2
```

### **多行字符串**

python三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符。

三引号让程序员从引号和特殊字符串的泥潭里面解脱出来，自始至终保持一小块字符串的格式是所谓的WYSIWYG（所见即所得）格式的。

一个典型的用例是，当你需要一块HTML或者SQL时，这时特殊字符串转义将会非常的繁琐。

### **常用方法**

1. 索引
2. 切片
3. 连接
4. 重复
5. 存在性
6. 求长度
7.  原义字符串（无转义）

    所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。 原始字符串除在字符串的第一个引号前加上字母 **r**（可以大小写）以外，与普通字符串有着几乎完全相同的语法。

```python
encode(encoding='UTF-8',errors='strict')
startswith(substr, beg=0,end=len(string))
endswith(suffix, beg=0, end=len(string))
isdigit() # 如果字符串只包含数字则返回 True,否则返回 False
isupper()
islower()
lower() # 转换字符串中所有大写字符为小写
strip([chars]) # 移除字符串头尾指定的字符（默认为空格）或字符序列
replace(old, new [, max])

translate(table, deletechars="")
title()  # 将每个单词首字母大写
```

### str.maketrans

maketrans() 方法用于创建字符映射的转换表，对于接受两个参数的最简单的调用方式，第一个参数是字符串，表示需要转换的字符，第二个参数也是字符串表示转换的目标。

如果只有**一个参数**，则它必须是一个将 Unicode 码位序号（整数）或字符（长度为 1 的字符串）映射到 Unicode 码位序号、（任意长度的）字符串或 `None` 的**字典**。

如果有第三个参数，它必须是一个字符串，其中的字符将在结果中被映射到`None`（表示删除）。

两个字符串的长度必须相同，为一一对应的关系。

### translate

translate() 方法根据参数 table 给出的表(包含 256 个字符)转换字符串的字符,要过滤掉的字符放到 **deletechars** 参数中。

```python
str.translate(table)
bytes.translate(table[, delete])    
bytearray.translate(table[, delete]) 
```

* table -- 翻译表，翻译表是通过 [maketrans()](https://www.runoob.com/python3/python3-string-maketrans.html) 方法转换而来。
* deletechars -- 字符串中要过滤的字符列表。

函数返回翻译后的字符串,若给出了 delete 参数，则将原来的bytes中的属于delete的字符删除，剩下的字符要按照table中给出的映射来进行映射 。

```python
intab = "aeiou"
outtab = "12345"
trantab = str.maketrans(intab, outtab)   # 制作翻译表
 
str = "this is string example....wow!!!"
print (str.translate(trantab))

# th3s 3s str3ng 2x1mpl2....w4w!!!
```

### **join**

`join(seq)`

`join()`方法获取可迭代对象中的所有项目，将它们连接为一个字符串返回。

必须将字符串指定为分隔符。可迭代对象中的元素必须是字符串。

```
myTuple = ("Bill", "Steve", "Elon")x = "#".join(myTuple)print(x)# Bill#Steve#Elon
```

### **split**

`split(str="", num=string.count(str)) # 返回分割后的字符串列表`

`split()`方法将字符串拆分为列表。您可以指定分隔符，默认分隔符是任何**空白**字符。

```
txt = "hello, my name is Bill, I am 63 years old"x = txt.split(", ")print(x)# ['hello', 'my name is Bill', 'I am 63 years old']
```

### **find**

`find(str, beg=0, end=len(string))`

`find()`方法查找指定子串的**首次**出现位置。如果找不到该值，则 `find()`方法返回 -1。

## Bytes

bytes 对象是由单个字节构成的不可变序列。 由于许多主要二进制协议都基于 ASCII 文本编码，因此 bytes 对象提供了一些仅在处理 ASCII 兼容数据时可用，并且在许多特性上与字符串对象紧密相关的方法。

首先，表示 bytes 字面值的语法与字符串字面值的大致相同，只是添加了一个 `b` 前缀：

* 单引号: `b'同样允许嵌入 "双" 引号'`。
* 双引号: `b"同样允许嵌入 '单' 引号"`。
* 三重引号: `b'''三重单引号'''`, `b"""三重双引号"""`

像字符串字面值一样，bytes 字面值也可以使用 `r` 前缀来禁用转义序列处理。

在`bytes`中，无法显示为ASCII字符的字节，用`\x##`显示。

除了字面值形式，bytes 对象还可以通过其他几种方式来创建：

* 指定长度的以零值填充的 bytes 对象: `bytes(10)`
* 通过由整数组成的可迭代对象: `bytes(range(20))`
* 通过缓冲区协议复制现有的二进制数据: `bytes(obj)`

### **常用方法**

```python
# 返回从给定 bytes 解码出来的字符串
bytes.decode(encoding="utf-8", errors="strict")
# 以Unicode表示的str通过encode()方法可以编码为指定的bytes
>>> '中文'.encode('utf-8')
b'\xe4\xb8\xad\xe6\x96\x87'
```

<table data-header-hidden><thead><tr><th width="150"></th><th width="150"></th><th width="150"></th><th></th></tr></thead><tbody><tr><td>字符</td><td>ASCII</td><td>Unicode</td><td>UTF-8</td></tr><tr><td>A</td><td>01000001</td><td>00000000 01000001</td><td>01000001</td></tr><tr><td>中</td><td>x</td><td>01001110 00101101</td><td>11100100 10111000 10101101</td></tr></tbody></table>

## 集合

集合（set）是一个**无序**的**不重复**元素序列。

可以使用大括号 **{ }** 或者 **set()** 函数创建集合。

```python
class set([iterable])
```

{% hint style="info" %}
创建一个空集合必须用 **set()** 而不是 **{ }**，因为 **{ }** 是用来创建一个空字典。
{% endhint %}

### **集合运算**

```python
>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  
{'a', 'r', 'b', 'c', 'd'}              # 去重
>>> b
{'c', 'm', 'a', 'z', 'l'}
>>> a - b                              # 差集，集合a中包含而集合b中不包含的元素
{'r', 'd', 'b'}
>>> a | b                              # 并集，集合a或b中包含的所有元素
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
>>> a & b                              # 交集，集合a和b中都包含了的元素
{'a', 'c'}
>>> a ^ b                              # 对称差，不同时包含于a和b的元素
{'r', 'd', 'b', 'm', 'z', 'l'}
```

### **常用方法**

1.  添加元素：`s.add(x)` 如果元素已存在，则不进行任何操作。

    `s.update(iterable)` 其参数可以是列表，元组，字典等可迭代对象。当参数为字典时，具体被添加的元素是字典的键。
2.  移除元素：`s.remove(x)`如果元素不存在，则会发生错误。

    `s.discard(x)`如果元素不存在，不会发生错误。

    `s.pop()`会对集合进行无序的排列，然后删除这个无序集合的左数第一个元素。
3. 求长度
4. 清空
5. 存在性

## 推导式

### **列表推导式**

列表推导式可以利用 range 区间、元组、列表、字典和集合等数据类型，快速生成一个满足指定需求的列表。

```python
[表达式 for 迭代变量 in 可迭代对象 [if 条件表达式] ]
[exp1 if condition else exp2 for x in data]  
# 此处if...else主要起赋值作用
# 当data中的数据满足if条件时将其做exp1处理，否则按照exp2处理，最后统一生成为一个数据列表
```

当然，列表推导式也可使用多个循环，就像嵌套循环一样。

### **集合推导式**

集合的生成同样可以通过推导式来实现，把外层的中括号改为大括号即可。

### **字典推导式**

Python 中，可以借助列表、元组、字典、集合以及 range 区间，快速生成符合需求的字典。

```
{表达式1:表达式2 for 迭代变量 in 可迭代对象 [if 条件表达式]}
```

### **生成器推导式**

把列表推导式外层的中括号改为小括号即可。这样就得到了一个生成器。
