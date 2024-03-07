# Python基础

## 注释

### 单行注释

Python中单行注释以 **#** 开头。

### 多行注释

多行注释用三个单引号 **'''** 或者三个双引号 **"""** 将注释括起来。

## 变量 & 类型

变量在使用前必须先"定义"。要注意变量名的命名规则。

如果改变变量的数据类型，将重新分配内存空间。

像Python这种变量本身类型不固定的语言称之为*动态语言*，与之对应的是*静态语言*。

在交互模式中，最后被输出的表达式结果被赋值给变量 **_** 。

可以通过使用`del`语句删除单个或多个对象的引用，例如

```python
del var_a, var_b
```

### 可变对象 & 不可变对象

可变对象可以在其 id() 保持固定的情况下改变其取值。

不可变对象则正相反，是具有固定值的对象，包括数字、字符串和元组。这样的对象不能被改变。如果必须存储一个不同的值，则必须创建新的对象。它们在需要常量哈希值的地方起着重要作用，例如作为字典中的键。

### 可哈希 & 不可哈希

一个对象的哈希值如果在其生命周期内绝不改变，就被称为可哈希 （它需要具有 **hash**() 方法），并可以同其他对象进行比较（它需要具有 **eq**() 方法）。

可哈希对象必须具有相同的哈希值比较结果才会相同。一个对象的哈希值在生命周期内不改变，就称为可哈希。

可哈希性使得对象能够作为字典键或集合成员使用，因为这些数据结构要在内部使用哈希值。
可变容器（例如列表或字典）都不可哈希。只有可哈希对象才能作为字典的键。

### 数字

不同类型的数混合运算时会将整数转换为浮点数。

#### 整数

布尔(bool)是整型的子类型。Python3 整型是没有限制大小的，可以当作 Long 类型使用。

可以在数字前加前缀`0x`表示16进制数。

Python允许在数字中间以`_`分隔，因此，写成`10_000_000_000`和`10000000000`是完全一样的。十六进制数也可以写成`0xa1b2_c3d4`。

#### 浮点数

可以使用科学计数法表示。

#### 复数

由实数部分和虚数部分构成，可以用`a + bj`,或者`complex(a,b)`表示， 复数的实部a和虚部b都是浮点型。

### 布尔值

一个布尔值只有`True`、`False`两种值。可以使用逻辑运算符。经常用在条件判断中。

### 空值

空值是Python里一个特殊的值，用`None`表示。

空值作为判断条件时，视为`False`。

### 数字类型转换

- **int(x)** 将x转换为一个整数。
- **float(x)** 将x转换到一个浮点数。
- **complex(x)** 将x转换到一个复数，实数部分为 x，虚数部分为 0。
- **complex(x, y)** 将 x 和 y 转换到一个复数，实数部分为 x，虚数部分为 y。x 和 y 是数字表达式。

### 数学常量

```python
>>> import math>>> math.pi3.141592653589793>>> math.exp(1)2.718281828459045
```

### 联合类型——*union*

## 运算符

### 算术运算符

#### 除法相关

在整数除法中，除法 **/** 总是返回一个浮点数，如果只想得到整数的结果，丢弃可能的分数部分，可以使用运算符 **//** ：

```python
>>> 17 / 3  # 整数除法返回浮点型5.666666666666667>>>>>> 17 // 3  # 整数除法返回向下取整后的结果5>>> 17 % 3  # ％操作符返回除法的余数2
```

**注意：//** 得到的并不一定是整数类型的数，它与分母分子的数据类型有关系。

```python
>>> 7//23>>> 7.0//23.0>>> 7//2.03.0>>> 7.0//2.03.0
```

#### 幂运算

Python 可以使用 `**`操作来进行幂运算：

```python
>>> 5 ** 2  # 5 的平方25>>> 2 ** 7  # 2的7次方128
```

### 关系/比较运算符

`== != > < >= <=`

### 赋值运算符

在Python中，赋值语句不会返回值。

#### 复合/序列赋值

**a, b = b, a+b**等价于

```python
n=bm=a+ba=nb=m
```

```python
>>> [a, b] = (1, 2)>>> a,b,c='abc'
```

#### 序列扩展

可以使用 * 来作为通配符，代表余下的数据项

```python
>>> a,*b='abcd'>>> a,b('a', ['b', 'c', 'd'])>>> *a,b='abcd'>>> a,b(['a', 'b', 'c'], 'd')
```

#### 海象运算符`:=`

可在表达式内部为变量赋值。

### 逻辑运算符

`and or not`

### 位运算符

`& | ^ ~ << >>`

### 成员运算符

`in 和not in`

### 身份运算符

用于比较两个对象的存储单元，判断两个标识符是不是引用自一个对象。

- **x is y**, 类似 **id(x) == id(y)** , 如果引用的是同一个对象则返回 True，否则返回 False
- **x is not y** ， 类似 **id(a) != id(b)**。如果引用的不是同一个对象则返回结果 True，否则返回 False。

**注**： id() 函数用于获取对象内存地址。

*is 与 == 区别：*

*is 用于判断两个变量引用对象是否为同一个， == 用于判断引用变量的值是否相等。*

### 优先级

| 运算符                   | 描述                                                   |
| :----------------------- | :----------------------------------------------------- |
| **                       | 指数 (最高优先级)                                      |
| ~ + -                    | 按位翻转, 一元正号和负号 (最后两个的方法名为 +@ 和 -@) |
| * / % //                 | 乘，除，求余数和取整除                                 |
| + -                      | 加减法                                                 |
| >> <<                    | 右移，左移运算符                                       |
| &                        | 位 'AND'                                               |
| ^ \|                     | 位运算符                                               |
| <= < > >=                | 比较运算符                                             |
| == !=                    | 等于运算符                                             |
| = %= /= //= -= += *= **= | 赋值运算符                                             |
| is is not                | 身份运算符                                             |
| in not in                | 成员运算符                                             |
| not and or               | 逻辑运算符                                             |

## 流程控制

### 条件控制语句

```python
if condition_1:    statement_block_1elif condition_2:    statement_block_2else:    statement_block_3
```

Python 中用 **elif** 代替了 **else if**，所以if语句的关键字为：**if – elif – else**。

可以嵌套使用。

**注意**：

1. 每个条件后面要使用冒号 **:** 表示接下来是满足条件后要执行的语句块。

2. 使用缩进来划分语句块，相同缩进数的语句在一起组成一个语句块。

3. 在Python中**没有**switch – case语句。

### 循环语句

循环语句**可以有 else 子句**，它在穷尽列表(以for循环)或条件变为 false (以while循环)导致循环终止时被执行，**但循环被 break 终止时不执行**。

#### while循环

```python
while <expr>:    <statement(s)>else:    <additional_statement(s)>
```

同样需要注意冒号和缩进。另外，在 Python 中没有 do..while 循环。

expr 条件语句为 true 则执行 statement(s) 语句块，如果为 false，则执行 additional_statement(s)，并退出循环。

#### for循环

Python for 循环可以遍历任何可迭代对象，如一个列表或者一个字符串。

```python
for <variable> in <sequence>:    <statements>else:    <statements>
```

#### 特殊语句

##### pass

Python pass是空语句，是为了保持程序结构的完整性。

pass 不做任何事情，一般用做占位语句。

##### break

##### continue

## 高级变量：序列（***Sequence***）

### 列表

列表是最常用的 Python 数据类型，它可以作为一个方括号内的逗号分隔值出现。

列表的数据项不需要具有相同的类型，创建一个列表，只要把逗号分隔的不同的数据项使用方括号括起来即可。

#### 常用方法

1. 索引

![image-20211017192120961](C:\Users\zihao\Pictures\Camera Roll\mfOFZ2eKydz746W.png)

2. 切片：可以使用方括号 **[]** 的形式截取序列，又名切片（slice）。左闭右开区间。

`list[start=0:end=len(list):span=1]`

其中`span`为步长值，可以为负数。例如使用`list[::-1]`就可以反转列表。

3. 更新：使用`append()`方法添加列表项。

4. 删除：可以使用 `del` 语句来删除列表的元素。

5. 求长度：`len(list)`

6. 组合

`list1 + list2`

`list1 += list2`

7. 重复

`list * n`，其中n为正整数，小于 `0` 的 *n* 值会被当作 `0` 来处理 (生成一个同类型的空序列)。

8. 存在性

`x in list`

`x not in list`

9. *遍历/迭代*：`for x in [1, 2, 3]:`
10. 转换至列表：`list(seq)`可以把元组、字符串、集合、range对象等转换为列表。

```python
list.count(obj)list.index(obj) # 找出某个值第一个匹配项的索引位置list.insert(index, obj)list.pop([index=-1]) # 该函数会返回被删除的值list.remove(obj)list.reverse()list.sort(key=None, reverse=False) # 原地稳定排序其中key为单参数函数，用于从每个列表元素中提取比较键# reverse = True 降序， reverse = False 升序（默认值）# 无返回值list.clear()	# 等价于del list[:]# 如果写成del list，会把列表对象抹除，而非清空列表
```

### 元组

与列表类似，但元组的元素一经写成即不可修改。

所谓元组的不可变指的是元组所指向的内存中的内容不可变。

事实上，重新赋值的元组会绑定到新的对象，不是修改了原来的对象。

创建元组很简单，只需要在括号中添加元素，并使用逗号隔开即可。创建非空元组可以不加括号。

**注**：元组中只包含一个元素时，需要在元素后面添加逗号 **,** 否则括号会被当作运算符使用

#### 常用方法

1. 索引
2. 切片
3. 删除整个元组
4. 求长度
5. 连接
6. 复制
7. 存在性
8. 迭代
9. 转换至元组：`tuple(seq)`

### Range

`range`类型表示不可变的数字序列，通常用于在 `for`循环中循环指定的次数。

```python
class range(start=0, stop[, step=1])
```

range 构造器的参数必须为整数。如果 step 为零则会引发 `ValueError`。左闭右开。

range 类型相比常规 list 或 tuple 的优势在于一个 range 对象总是占用固定数量的**较小**内存，不论其所表示的范围有多大（因为它只保存了 start, stop 和 step 值，并会根据需要计算具体单项或子范围的值）。

### 字典

#### 定义

字典是另一种可变容器模型，且可存储任意类型对象。

字典的每个键值 **key=>value** 对用冒号 **:** 分割，每个对之间用逗号(**,**)分割，整个字典包括在花括号 **{}** 中 ,格式如下所示

```python
dic = {key1 : value1, key2 : value2, key3 : value3 }
```

键必须是**唯一**的，但值则不必。

值可以取任何数据类型，但键必须不可变，所以可以用数字，字符串或元组充当，而用列表就不行。

#### 常用方法

1. 判断key的存在性：`in/not in`操作符

   Python 字典 **in** 操作符用于判断键是否存在于字典中，如果键在字典 `dict `里返回 true，否则返回 false。

   而 **not in** 操作符刚好相反，如果键在字典 `dict `里返回 false，否则返回 true。

2. 由键访问值

3. 删除键/字典

4. 清空

5. 求长度

6. 删除键并返回值：`pop(key[,default])`

#### 遍历

```python
xiaoming = {"name": "小明",            "age": 18,            "gender": True,            "height": 1.75}# 1.可以仅遍历keyfor k in xiaoming:    print(f'{k}:{xiaoming[k]}')# 2.也可以通过items()方法返回的视图对象进行遍历for k, v in xiaoming.items():    print(f'{k}:{v}')
```

### 字符串

字符串是 Python 中最常用的数据类型。我们可以使用引号( **'** 或 **"** )来创建字符串。

Python 不支持单字符类型，单字符在 Python 中也是作为一个字符串使用。

#### 转义字符

| 转义字符 | 描述                                                         | 实例                                                         |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| \\       | (在行尾时)续行符                                             | `>>> print("line1 \ ... line2 \ ... line3") `                |
| \\\\     | 反斜杠符号                                                   | `>>> print("\\") `                                           |
| \\'      | 单引号                                                       | `>>> print('\'') '`                                          |
| \\"      | 双引号                                                       | `>>> print("\"") "`                                          |
| \a       | 响铃(Alarm)                                                  | `>>> print("\a")`执行后电脑有响声。                          |
| \b       | 退格(Backspace)                                              | `>>> print("Hello \b World!") Hello World!`                  |
| \000     | 空                                                           | `>>> print("\000") >>> `                                     |
| \n       | 换行(new line)                                               | `>>> print("\n")  >>>`                                       |
| \v       | 纵向(vertical)制表符                                         | `>>> print("Hello \v World!") Hello        World! >>>`       |
| \t       | 横向制表符                                                   | `>>> print("Hello \t World!") Hello    World! >>>`           |
| \r       | 回车，将 **\r** 后面的内容移到字符串开头，并逐一替换开头部分的字符，直至将 **\r** 后面的内容完全替换完成。 | `>>> print("Hello\rWorld!") World! `                         |
| \f       | 换页                                                         | `>>> print("Hello \f World!") Hello        World! >>> `      |
| \yyy     | 八进制数，y 代表 0~7 的字符，例如：\012 代表换行。           | `>>> print("\110\145\154\154\157\40\127\157\162\154\144\41") Hello World!` |
| \xyy     | 十六进制数，以 \x 开头，y 代表的字符，例如：\x0a 代表换行    | `>>> print("\x48\x65\x6c\x6c\x6f\x20\x57\x6f\x72\x6c\x64\x21") Hello World!` |

#### 格式化

##### %格式化

##### `str.format`

Python2.6 开始，新增了一种格式化字符串的函数 **str.format()**，它增强了字符串格式化的功能。

基本语法是通过 **{}** 和 **:** 来代替以前的 **%** 。

format 函数可以接受不限个参数，位置可以不按顺序。

```python
>>>"{} {}".format("hello", "world")    # 不设置指定位置，按默认顺序'hello world' >>> "{0} {1}".format("hello", "world")  # 设置指定位置'hello world' >>> "{1} {0} {1}".format("hello", "world")  # 设置指定位置'world hello world'print("网站名：{name}, 地址 {url}".format(name="菜鸟教程", url="www.runoob.com")) # 通过字典设置参数site = {"name": "菜鸟教程", "url": "www.runoob.com"}print("网站名：{name}, 地址 {url}".format(**site)) # 通过列表索引设置参数my_list = ['菜鸟教程', 'www.runoob.com']print("网站名：{0[0]}, 地址 {0[1]}".format(my_list))  # "0" 是必须的
```

也可以向 **str.format()** 传入对象。

```python
class AssignValue(object):    def __init__(self, value):        self.value = valuemy_value = AssignValue(6)print('value 为: {0.value}'.format(my_value))  # "0" 是可选的
```

##### f-string

字面量格式化字符串。

**f-string** 格式化字符串以 **f** 开头，后面跟着字符串，字符串中的表达式用大括号 {} 包起来，它会将变量或表达式计算后的值替换进去。

可以指定输出变量的格式，如下所示：

```python
>>> r = 2.5>>> s = 3.14 * r ** 2>>> print(f'The area of a circle with radius {r} is {s:.2f}') # 两位小数The area of a circle with radius 2.5 is 19.62
```

在 Python 3.8 的版本中可以使用 **=** 符号来拼接运算表达式与结果：

```python
>>> x = 1>>> print(f'{x+1=}')   # Python 3.8x+1=2
```

#### 多行字符串

python三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符。

三引号让程序员从引号和特殊字符串的泥潭里面解脱出来，自始至终保持一小块字符串的格式是所谓的WYSIWYG（所见即所得）格式的。

一个典型的用例是，当你需要一块HTML或者SQL时，这时特殊字符串转义将会非常的繁琐。

#### 常用方法

1. 索引

2. 切片

3. 连接

4. 重复

5. 存在性

6. 求长度

7. 原义字符串（无转义）

   所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。 原始字符串除在字符串的第一个引号前加上字母 **r**（可以大小写）以外，与普通字符串有着几乎完全相同的语法。

```python
encode(encoding='UTF-8',errors='strict')endswith(suffix, beg=0, end=len(string))isdigit() # 如果字符串只包含数字则返回 True 否则返回 Falseisupper()islower()lower() # 转换字符串中所有大写字符为小写strip([chars]) # 移除字符串头尾指定的字符（默认为空格）或字符序列replace(old, new [, max])startswith(substr, beg=0,end=len(string))translate(table, deletechars="")title()	# 将每个单词首字母大写
```

##### join

`join(seq)`

`join() `方法获取可迭代对象中的所有项目，将它们连接为一个字符串返回。

必须将字符串指定为分隔符。可迭代对象中的元素必须是字符串。

```python
myTuple = ("Bill", "Steve", "Elon")x = "#".join(myTuple)print(x)# Bill#Steve#Elon
```

##### split

`split(str="", num=string.count(str)) # 返回分割后的字符串列表`

`split() `方法将字符串拆分为列表。您可以指定分隔符，默认分隔符是任何**空白**字符。

```python
txt = "hello, my name is Bill, I am 63 years old"x = txt.split(", ")print(x)# ['hello', 'my name is Bill', 'I am 63 years old']
```

##### find

`find(str, beg=0, end=len(string))`

`find() `方法查找指定子串的首次出现位置。如果找不到该值，则 `find() `方法返回 -1。

### Bytes

bytes 对象是由单个字节构成的不可变序列。 由于许多主要二进制协议都基于 ASCII 文本编码，因此 bytes 对象提供了一些仅在处理 ASCII 兼容数据时可用，并且在许多特性上与字符串对象紧密相关的方法。

首先，表示 bytes 字面值的语法与字符串字面值的大致相同，只是添加了一个 `b` 前缀：

- 单引号: `b'同样允许嵌入 "双" 引号'`。
- 双引号: `b"同样允许嵌入 '单' 引号"`。
- 三重引号: `b'''三重单引号'''`, `b"""三重双引号"""`

像字符串字面值一样，bytes 字面值也可以使用 `r` 前缀来禁用转义序列处理。

在`bytes`中，无法显示为ASCII字符的字节，用`\x##`显示。

除了字面值形式，bytes 对象还可以通过其他几种方式来创建：

- 指定长度的以零值填充的 bytes 对象: `bytes(10)`
- 通过由整数组成的可迭代对象: `bytes(range(20))`
- 通过缓冲区协议复制现有的二进制数据: `bytes(obj)`

#### 常用方法

![image-20220325165538548](C:\Users\zihao\Pictures\Camera Roll\image-20220325165538548.png)

```python
# 返回从给定 bytes 解码出来的字符串bytes.decode(encoding="utf-8", errors="strict")# 以Unicode表示的str通过encode()方法可以编码为指定的bytes>>> '中文'.encode('utf-8')b'\xe4\xb8\xad\xe6\x96\x87'
```

| 字符 | ASCII    | Unicode           | UTF-8                      |
| ---- | -------- | ----------------- | -------------------------- |
| A    | 01000001 | 00000000 01000001 | 01000001                   |
| 中   | x        | 01001110 00101101 | 11100100 10111000 10101101 |



### 集合

集合（set）是一个**无序**的**不重复**元素序列。

可以使用大括号 **{ }** 或者 **set()** 函数创建集合。

```python
class set([iterable])
```

**注意**：创建一个空集合必须用 **set()** 而不是 **{ }**，因为 **{ }** 是用来创建一个空字典。

#### 运算

```python
>>> a = set('abracadabra')>>> b = set('alacazam')>>> a                                  {'a', 'r', 'b', 'c', 'd'}              # 去重>>> b{'c', 'm', 'a', 'z', 'l'}>>> a - b                              # 差集，集合a中包含而集合b中不包含的元素{'r', 'd', 'b'}>>> a | b                              # 并集，集合a或b中包含的所有元素{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}>>> a & b                              # 交集，集合a和b中都包含了的元素{'a', 'c'}>>> a ^ b                              # 对称差，不同时包含于a和b的元素{'r', 'd', 'b', 'm', 'z', 'l'}
```

#### 常用方法

1. 添加元素：`s.add(x)` 如果元素已存在，则不进行任何操作。

   `s.update(iterable)` 其参数可以是列表，元组，字典等可迭代对象。

2. 移除元素：`s.remove(x)`如果元素不存在，则会发生错误。

   `s.discard(x)`如果元素不存在，不会发生错误。

   `s.pop()`会对集合进行无序的排列，然后将这个无序排列集合的左面第一个元素进行删除。

3. 求长度

4. 清空

5. 存在性

### 推导式

#### 列表推导式

列表推导式可以利用 range 区间、元组、列表、字典和集合等数据类型，快速生成一个满足指定需求的列表。

```python
[表达式 for 迭代变量 in 可迭代对象 [if 条件表达式] ]# 相当于for 迭代变量 in 可迭代对象:    if 条件表达式 == True:    append()    [exp1 if condition else exp2 for x in data]	# 此处if...else主要起赋值作用# 当data中的数据满足if条件时将其做exp1处理，否则按照exp2处理，最后统一生成为一个数据列表
```

实际上，列表推导式也可使用多个循环，就像嵌套循环一样。

#### 集合推导式

把外层的中括号改为大括号即可。

#### 字典推导式

Python 中，使用字典推导式可以借助列表、元组、字典、集合以及 range 区间，快速生成符合需求的字典。

```python
{表达式1:表达式2 for 迭代变量 in 可迭代对象 [if 条件表达式]}
```

#### 生成器推导式

把列表推导式外层的中括号改为小括号即可。这样就得到了一个生成器。

## 迭代器

迭代是Python最强大的功能之一，是访问集合元素的一种方式。迭代器是一个可以记住遍历的位置的对象。

迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。（拱卒）

迭代器有两个基本的方法：**iter()** 和 **next()**。

### 创建迭代器

可迭代对象指能够逐一返回其成员项的对象。 可迭代对象的例子包括所有序列类型 (例如 `list`, `str` 和 `tuple`) 以及某些非序列类型例如 `dict`, 文件对象 以及定义了 __iter__() 方法或是实现了序列语义的 __getitem__() 方法的任意自定义类对象。

字符串，列表或元组对象都可用于创建迭代器。

```python
iter(iterable)next(iterator)>>> list=[1,2,3,4]>>> it = iter(list)    # 创建迭代器对象>>> print (next(it))   # 输出迭代器的下一个元素1>>> print (next(it))2
```

把一个类作为一个迭代器使用需要在类中实现两个方法 \_\_iter\__() 与 \_\_next__() 。

\_\_iter\__() 方法返回一个特殊的迭代器对象， 这个迭代器对象实现了 \_\_next\_\_() 方法并通过 StopIteration 异常标识迭代的完成。

\_\_next__() 方法（Python 2 里是 next()）会返回下一个迭代器对象。

```python
class MyNumbers:    def __iter__(self):        self.a = 1        return self    def __next__(self):        self.a += 1        return self.a    myclass = MyNumbers()myiter = iter(myclass)print(next(myiter))print(next(myiter))print(next(myiter))print(next(myiter))print(next(myiter))
```

### StopIteration

`StopIteration `异常用于标识迭代的完成，防止出现无限循环的情况，在 \_\_next\_\_() 方法中我们可以设置在完成指定循环次数后触发 `StopIteration `异常来结束迭代。

### 遍历

可以使用`for`语句遍历迭代器。

## 生成器

在 Python 中，使用了 yield 的函数被称为生成器（generator）。可以做到一边循环一边计算。

跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器。

在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回 yield 的值, 并在下一次执行 next() 方法时从当前位置继续运行。

调用一个生成器函数，返回的是一个迭代器对象。

generator 保存的是算法，每次调用`next(g)`，就计算出`g`的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出`StopIteration`的错误。

## 函数

函数是组织好的，可重复使用的，用来实现单一，或相关联功能的代码段。

函数能提高应用的模块性，和代码的重复利用率。

### 定义

- 函数代码块以 **def** 关键词开头，后接函数标识符名称和圆括号 **()**，函数内容以冒号 **:** 起始，并且缩进。
- 任何传入参数和自变量必须放在圆括号中间，圆括号之间可以用于定义参数。
- 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
- **return [表达式]** 结束函数，选择性地返回一个值给调用方，不带表达式的 return 相当于返回 None。

### 调用

可以通过另一个函数调用执行，也可以直接从 Python 命令提示符执行。

### 参数

#### 必需参数

必需参数须以正确的顺序传入函数。调用时的数量必须和声明时的一样。

#### 关键字参数

关键字参数和函数调用关系紧密，函数调用使用关键字参数来确定传入的参数值。

使用关键字参数允许函数调用时参数的顺序与声明时不一致，因为 Python 解释器能够用参数名匹配参数值。

```python
fun(参数名=参数值)
```

#### 默认参数

```python
def printinfo( name, age = 35 ):	# age为默认参数，默认值为35	pass
```

#### 不定长参数

```python
def functionname([formal_args,] *var_args_tuple , **var_args_dict):   "函数_文档字符串"   function_suite   return [expression]
```

加了星号 ***** 的参数会以元组(tuple)的形式导入，存放所有未命名的变量参数。

加了两个星号 ****** 的参数会以字典的形式导入。

声明函数时，参数中星号 ***** 可以单独出现。如果单独出现星号 ***** 后的参数必须用关键字传入。

#### 参数传递

- **不可变类型：**类似 C++ 的值传递，如整数、字符串、元组。如 fun(a)，传递的只是 a 的值，没有影响 a 对象本身。如果在 fun(a) 内部修改 a 的值，则是新生成一个 a 的对象。
- **可变类型：**类似 C++ 的引用传递，如 列表，字典。如 fun(la)，则是将 la 真正的传过去，修改后 fun 外部的 la 也会受影响

### 返回值

**return [表达式]** 语句用于退出函数，选择性地向调用方返回一个表达式。不带参数值的return语句返回None。

### 强制位置参数

### 匿名函数（lambda表达式）

python 使用 lambda 来创建匿名函数。所谓匿名，意即不再使用 def 语句这样标准的形式定义一个函数。

- lambda 只是一个表达式，函数体比 def 简单很多。
- lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
- lambda 函数拥有**自己的命名空间**，且不能访问自己参数列表之外或全局命名空间里的参数。
- 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

#### 语法

```python
lambda [arg1 [,arg2,.....argn]]:expression
```

#### 调用

`fun(arg1 [,arg2,.....argn])`

### 内置函数

#### sorted

```python
sorted(iterable, key=None, reverse=False)  
```

- iterable -- 可迭代对象。
- key -- 取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
- reverse -- 排序规则，reverse = True 降序 ， reverse = False 升序（默认）。

返回排序后的**列表**。

#### reversed

reversed() 函数返回反向的**迭代器**对象。

```python
alph = ["a", "b", "c", "d"]ralph = reversed(alph)for x in ralph:  print(x)# d# c# b# a
```

#### repr

repr() 函数将对象转化为供**解释器**读取的形式。

##### 语法

以下是 repr() 方法的语法:

```
repr(object)
```

##### 参数

- object -- 对象。

##### 返回值

返回一个对象的 string 格式。

#### eval

```python
eval(expression[, globals[, locals]])
```

实参是一个字符串，以及可选的 globals 和 locals。

表达式解析参数 *expression* 并作为 Python 表达式进行求值（从技术上说是一个条件列表），采用 *globals* 和 *locals* 字典作为全局和局部命名空间。

如果给出的源数据是个字符串，那么其前后的空格和制表符将被剔除。

通常情况下`obj==eval(repr(obj))`这个等式是成立的。

##### 用法

1. 可以直接用来提取用户输入的多个值。

   ```python
   a, b = eval(input('请输入逗号隔开的两个数'))
   ```

   输入：**10,5**，得到 **a=10，b=5**。

2. eval() 函数可将看起来像列表的字符串重新转换为列表。

   ```python
   zifu=" ['1709020230', '1707030416', '0', '0', '0']  "ls = eval(zifu)
   ```

#### chr

chr() 用一个整数作参数，返回一个对应的字符。

##### 语法

以下是 chr() 方法的语法:

```python
chr(i)
```

##### 参数

- i -- 可以是 10 进制也可以是 16 进制的形式的数字，数字范围为 0 到 1,114,111 (16 进制为0x10FFFF)。

##### 返回值

返回值是当前整数对应的 ASCII 字符。

#### ord

ord() 函数是 chr() 函数（对于 8 位的 ASCII 字符串）的配对函数，它以一个字符串（Unicode 字符）作为参数，返回对应的 ASCII 数值，或者 Unicode 数值。

##### 语法

以下是 ord() 方法的语法:

```python
ord(c)
```

##### 参数

- c -- 字符。

##### 返回值

返回值是对应的十进制整数。

#### sum

```python
sum(iterable, /, start=0)
```

从 *start* 开始自左向右对 *iterable* 的项求和并返回总计值。 *iterable* 的项通常为数字，而 start 值则不允许为字符串。

对某些用例来说，存在 [`sum()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=eval#sum) 的更好替代。 拼接字符串序列的更好更快方式是调用 `''.join(sequence)`。

### 数学函数

```python
abs(x)ceil(x)exp(x)fabs(x)floor(x)log(x)log10(x)modf(x)	# 返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示。pow(x,y[,z])	# 等效于pow(x,y) %zsqrt(x)
```

#### max函数(min同理)

```python
max(iterable, *[, key, default])max(arg1, arg2, *args[, key])
```

函数功能为取传入的多个参数中的最大值，或者传入的可迭代对象元素中的最大值。

默认数值型参数，取值大者；字符型参数，取字母表排序靠后者。

还可以传入命名参数 key，其为一个函数，用来指定取最大值的方法。

```python
s = [  {'name': 'sumcet', 'age': 18},  {'name': 'bbu', 'age': 11}]a = max(s, key=lambda x: x['age'])print(a)	# {'name': 'sumcet', 'age': 18}
```

如果只传入一个参数，则该参数必须为可迭代对象，返回其中的最大元素。

传入可迭代对象为空时，必须指定参数 default，用来返回默认值输出。

对于序列型参数，会依次按照索引位置的值进行比较取最大者。

```python
>>> max([1,2],[3])[3]>>> max([1,2],[1,3])[1, 3]
```

### 随机函数

主要依赖于`random`模块。

```python
random.random()	# 返回 [0.0, 1.0) 范围内的下一个随机浮点数# 几乎所有模块函数都依赖于这一基本函数random.choice(seq)	# 从非空序列 seq 返回一个随机元素。 如果 seq 为空，则引发 IndexErrorrandom.randrange(start, stop[, step = 1])	# 从 range(start, stop[, step]) 返回一个随机选择的元素# 这相当于 choice(range(start, stop, step)) ，但实际上并没有构建一个 range 对象random.randint(a, b)	# 返回随机整数 N 满足 a <= N <= b# 相当于 randrange(a, b+1)random.uniform(a, b)	# 用来生成 [a,b] 之间的随意浮点数，包括两个边界值# 取决于等式 a + (b-a) * random() 中的浮点舍入，终点 b 可能包括或不包括在该范围内random.shuffle(x[, random])	# 将一个列表中的元素打乱# 可选参数 random 是一个0参数函数，在 [0.0, 1.0) 中返回随机浮点数；默认情况下，这是函数 random() random.sample(population/sequence, k, *, counts=None)# 返回从总体序列或集合中选择的 k 长度列表， 用于无重复的随机抽样# counts指定元素的权重。sample(['red', 'blue'], counts=[4, 2], k=5)# 等价于sample(['red', 'red', 'red', 'red', 'blue', 'blue'], k=5)# 要从一系列整数中选择样本，请使用 range() 对象作为参数。 对于从大量人群中采样，这种方法特别快速且节省空间sample(range(10000000), k=60)# 如果样本大小大于总体大小，则引发 ValueError 。
```

### 函数式编程

函数是 Python 内建支持的一种封装，我们通过把大段代码拆成函数，通过一层一层的函数调用，就可以把复杂任务分解成简单的任务，这种分解可以称之为面向过程的程序设计。***函数就是面向过程的程序设计的基本单元***。

而函数式编程（请注意多了一个 “式” 字）——Functional Programming，虽然也可以归结到面向过程的程序设计，但其思想更接近**数学计算**。

函数式编程就是一种抽象程度很高的编程范式，纯粹的函数式编程语言编写的函数没有变量，因此，任意一个函数，只要输入是确定的，输出就是确定的，这种纯函数我们称之为没有副作用。而允许使用变量的程序设计语言，由于函数内部的变量状态不确定，同样的输入，可能得到不同的输出，因此，这种函数是有副作用的。

函数式编程的一个**特点**就是，允许把函数本身作为参数传入另一个函数，还允许返回一个函数！

Python 对函数式编程提供部分支持。由于 Python 允许使用变量，因此，Python 不是纯函数式编程语言。

#### 修饰器（装饰器）：decorator

返回值为另一个函数的函数，通常使用 `@wrapper` 语法形式来进行函数变换。 装饰器的常见例子包括 [`classmethod()`](https://docs.python.org/zh-cn/3/library/functions.html#classmethod) 和 [`staticmethod()`](https://docs.python.org/zh-cn/3/library/functions.html#staticmethod)。

函数对象有一个`__name__`属性，可以拿到函数的名字。

```python
>>> def now():...     print('2015-3-25')>>> now.__name__'now'
```

现在，假设我们要增强`now()`函数的功能，比如，在函数调用前后自动打印日志，但又不希望修改`now()`函数的定义，这种在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）。

装饰器语法只是一种**语法糖**，以下两个函数定义在语义上完全等价:

```python
def f(arg):    ...f = staticmethod(f)# 等价于@staticmethoddef f(arg):    ...
```

## 文件与I/O

### *print*

#### 语法

`print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)`

#### 参数

- `objects` – 表示可以一次输出多个对象。输出多个对象时，需要用 , 分隔。
- `sep` – 用来间隔多个对象，默认值是一个空格。
- `end` – 用来设定以什么结尾。默认值是换行符 \n，我们可以换成其他字符串。
- `file`– 要写入的文件对象。
- `flush` – 输出是否被缓存通常决定于 file，但如果 flush 关键字参数为 True，流会被强制刷新。

### *input*

```
input([prompt])
```

Python3.x 中 input() 函数将所有输入默认为***字符串***处理，返回为 string 类型。

需要输入多个参数时，一般搭配split()函数使用。

参数说明：

- prompt: 提示信息

### *StringIO*模块

字符流。很多时候，数据读写不一定是文件，也可以在内存中读写。

StringIO 顾名思义就是在内存中读写 str。

要把 str 写入 StringIO，我们需要先创建一个 StringIO，然后，像文件一样写入即可：

```python
>>> from io import StringIO>>> f = StringIO()>>> f.write('hello')>>> print(f.getvalue())
```

要读取 StringIO，可以用一个 str 初始化 StringIO，然后像读文件一样读取。

### *BytesIO*模块

StringIO 操作的只能是 str，如果要操作二进制数据，就需要使用 BytesIO。

BytesIO 实现了在内存中读写 bytes。

```python
>>> from io import BytesIO>>> f = BytesIO()>>> f.write('中文'.encode('utf-8'))6>>> print(f.getvalue())b'\xe4\xb8\xad\xe6\x96\x87'
```

### 打开文件——***open***

#### 语法

```python
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
```

#### 参数值

| 参数   | 描述                                                         |
| :----- | :----------------------------------------------------------- |
| *file* | 文件的路径或名称。                                           |
| *mode* | 字符串，定义您要在哪种模式下打开文件：<br />"r" - 读取 - 默认值。打开文件进行读取，如果文件不存在，则发生错误。<br />"a" - 追加 - 打开文件进行追加，如果不存在则创建文件。<br />"w" - 写入 - 打开文件进行写入，如果不存在则创建文件。<br />"x" - 创建 - 创建指定的文件，如果文件存在则返回错误。<br />**另外**，您可以指定文件应以二进制还是文本模式处理：<br />"t" - 文本 - 默认值。文字模式。<br />"b" - 二进制 - 二进制模式（例如图像）。 |
| errors | "ignore"表示忽略编码错误                                     |

如果文件不存在，`open()`函数就会抛出一个`IOError`的错误。

#### 返回值

返回文件对象。

### 写文件——***write***

**write()** 方法用于向文件中写入指定字符串。

在文件关闭前或缓冲区刷新前，字符串内容存储在缓冲区中，这时你在文件中是看不到写入的内容的。

如果文件打开模式带 b，则写入文件内容时，str (参数)要用 encode 方法转为 bytes 形式，否则报错：

TypeError: a bytes-like object is required, not 'str'。

同样适用with语句。

#### 语法

write() 方法语法如下：

```python
fileObject.write( str )
```

#### 参数

- **str** -- 要写入文件的字符串。

#### 返回值

返回的是写入的字符长度。

### 读取文件

#### read

##### 概述

**read()** 方法用于从文件读取指定的字符数（文本模式 **t**）或字节数（二进制模式 **b**），如果未给定参数 **size** 或 **size** 为负数则读取文件所有内容。

##### 语法

read() 方法语法如下：

```python
fileObject.read([size]); 
```

##### 参数

- **size** -- 从文件中读取的字符数（文本模式）或字节数（二进制模式），默认为 **-1**，表示读取整个文件。

##### 返回值

返回从字符串中读取的字节。（str或bytes）

#### readline

**readline()** 方法用于从文件读取整行，包括 "\n" 字符。如果指定了一个非负数的参数，则返回指定大小的字节数，包括 "\n" 字符。

##### 语法

readline() 方法语法如下：

```
fileObject.readline(size); 
```

##### 参数

- **size** -- 从文件中读取的字节数。

##### 返回值

返回从字符串中读取的字节。

#### readlines

**readlines()** 方法用于读取所有行(直到结束符 EOF)并返回列表，该列表可以由 Python 的 for... in ... 结构进行处理。 如果碰到结束符 EOF 则返回空字符串。

### 关闭文件——***close***

#### 概述

**close()** 方法用于关闭一个已打开的文件。关闭后的文件不能再进行读写操作， 否则会触发 *ValueError* 错误。 close() 方法允许调用多次。

当 file 对象，被引用到操作另外一个文件时，Python 会自动关闭之前的 file 对象。 使用 close() 方法关闭文件是一个好的习惯。

#### 语法

close() 方法语法如下：

```
fileObject.close();
```

### 补：*with*关键字

Python 中的 **with** 语句用于异常处理，封装了 **try…except…finally** 编码范式，提高了易用性。

**with** 语句使代码更清晰、更具可读性， 它简化了文件流等公共资源的管理。

由于文件读写时都有可能产生`IOError`，一旦出错，后面的`f.close()`就不会调用，因此在处理文件对象时使用 with 关键字是一种很好的做法。

```python
with open('/path/to/file', 'r') as f:    print(f.read())
```

### file-like Object

像`open()`函数返回的这种有个`read()`方法的对象，在 Python 中统称为 file-like Object（类文件对象，可读对象）。除了 file 外，还可以是内存的字节流，网络流，自定义流等等。file-like Object 不要求从特定类继承，只要写个`read()`方法就行。

`StringIO`就是在内存中创建的 file-like Object，常用作临时缓冲。

### 操作文件和目录——*os*模块

操作文件和目录的函数一部分放在`os`模块中，一部分放在`os.path`模块中。

这些合并、拆分路径的函数并不要求目录和文件要真实存在，它们只对字符串进行操作。

#### 环境变量

在操作系统中定义的环境变量，全部保存在`os.environ : dict`这个变量中，可以直接查看。

#### os.listdir——ls

os.listdir() 方法用于返回指定的文件夹包含的文件或文件夹的名字的列表。这个列表以字母顺序。 它不包括 **.** 和 **..** 即使它在文件夹中。

只支持在 Unix, Windows 下使用。

##### 语法

**listdir()**方法语法格式如下：

```
os.listdir(path='.')
```

##### 参数

- **path** -- 需要列出的目录路径，默认为当前目录

##### 返回值

返回指定路径下的文件和文件夹**列表**。

#### os.rename

os.rename() 方法用于命名文件或目录，从 src 到 dst,如果dst是一个存在的目录, 将抛出OSError。

##### 语法

**rename()**方法语法格式如下：

```
os.rename(src, dst)
```

##### 参数

- **src** -- 要修改的目录名
- **dst** -- 修改后的目录名

#### os.remove

os.remove() 方法用于删除指定路径的文件。如果指定的路径是一个目录，将抛出OSError。

##### 语法

**remove()**方法语法格式如下：

```
os.remove(path)
```

##### 参数

- **path** -- 要移除的文件路径

#### os.mkdir

os.mkdir() 方法用于以数字权限模式创建目录。默认的模式为 0777 (八进制)。

如果目录有多级，则创建最后一级，如果最后一级目录的上级目录有不存在的，则会抛出一个 OSError。

##### 语法

**mkdir()**方法语法格式如下：

```
os.mkdir(path[, mode])
```

##### 参数

- **path** -- 要创建的目录，可以是相对或者绝对路径。
- **mode** -- 要为目录设置的权限数字模式

#### os.rmdir

os.rmdir() 方法用于删除指定路径的目录。仅当这文件夹是***空的***才可以, 否则, 抛出OSError。

##### 语法

**rmdir()**方法语法格式如下：

```
os.rmdir(path)
```

##### 参数

- **path** -- 要删除的目录路径

#### os.path.abspath

`os.path.abspath(path)`

返回路径 *path* 的绝对路径。

#### os.path.join

`os.path.join(path, *paths)`

智能地拼接一个或多个路径部分。 返回值是 *path* 和 **paths* 的所有成员的拼接，其中每个非空部分后面都紧跟一个目录分隔符，最后一个部分除外，这意味着如果最后一个部分为空，则结果将以分隔符结尾。 如果某个部分为绝对路径，则之前的所有部分会被丢弃并从绝对路径部分开始继续拼接。

#### os.path.split

`os.path.split(path)`

同样的道理，要拆分路径时，也不要直接去拆字符串，而要通过`os.path.split()`函数。

该函数将路径 *path* 拆分为一对，即 `(head, tail)`，其中，*tail* 是路径的最后一部分，而 *head* 里是除最后部分外的所有内容。*tail* 部分不会包含斜杠，如果 *path* 以斜杠结尾，则 *tail* 将为空。

如果 *path* 中没有斜杠，*head* 将为空。

如果 *path* 为空，则 *head* 和 *tail* 均为空。

*head* 末尾的斜杠会被去掉，除非它是根目录（即它仅包含一个或多个斜杠）。

在所有情况下，`join(head, tail)` 指向的位置都与 *path* 相同（但字符串可能不同）。

#### os.path.splitext

`os.path.splitext(path)`

将路径名称 *path* 拆分为 `(root, ext)` 对使得 `root + ext == path`，并且扩展名 *ext* 为空或以句点打头并最多只包含一个句点。如果路径 path 不包含扩展名，则 *ext* 将为 `''`:

```python
>>> splitext('bar')('bar', '')
```

如果路径 path 包含扩展名，则 *ext* 将被设为该扩展名，包括打头的句点。 请注意在其之前的句点将被忽略。

#### os.path.isdir

```python
os.path.isdir(path)
```

如果 *path* 是 [`现有的`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.exists) 目录，则返回 `True`。本方法会跟踪符号链接，因此，对于同一路径，[`islink()`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.islink) 和 [`isdir()`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.isdir) 都可能为 `True`。

#### os.path.isfile

```
os.path.isfile(path)
```

如果 *path* 是 [`现有的`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.exists) 常规文件，则返回 `True`。本方法会跟踪符号链接，因此，对于同一路径，[`islink()`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.islink) 和 [`isfile()`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.isfile) 都可能为 `True`。

### *shutil*（**shell utility**）模块

作为os模块的有力补充，shutil 模块提供了一系列对文件和文件集合的高阶操作，特别是提供了一些支持文件拷贝和删除的函数。

#### shutil.copyfile

`shutil.copyfile(src, dst, *, follow_symlinks=True)`

将名为 *src* 的文件的内容（不包括元数据）拷贝到名为 *dst* 的文件并以尽可能高效的方式返回 *dst*。 *src* 和 *dst* 均为路径类对象或以字符串形式给出的路径名。

#### shutil.copytree

```python
shutil.copytree(src, dst, symlinks=False, ignore=None, copy_function=copy2, ignore_dangling_symlinks=False, dirs_exist_ok=False)
```

将以 *src* 为根起点的整个目录树拷贝到名为 *dst* 的目录并返回目标目录。 *dirs_exist_ok* 指明是否要在 *dst* 或任何丢失的父目录已存在的情况下引发异常。

目录的权限和时间会通过 [`copystat()`](https://docs.python.org/zh-cn/3/library/shutil.html?highlight=shutil#shutil.copystat) 来拷贝，单个文件则会使用 [`copy2()`](https://docs.python.org/zh-cn/3/library/shutil.html?highlight=shutil#shutil.copy2) 来拷贝。

#### shutil.rmtree

```python
shutil.rmtree(path, ignore_errors=False, onerror=None)
```

删除一个完整的目录树；*path* 必须指向一个目录（但不能是一个目录的符号链接）。 如果 *ignore_errors* 为真值，删除失败导致的错误将被忽略；如果为假值或是省略，此类错误将通过调用由 *onerror* 所指定的处理程序来处理，或者如果此参数被省略则将引发一个异常。

#### shutil.move

```python
shutil.move(src, dst, copy_function=copy2)
```

递归地将一个文件或目录 (*src*) 移至另一位置 (*dst*) 并返回目标位置。

如果目标是已存在的目录，则 *src* 会被移至该目录下。 

## 面向对象

面向对象编程——Object Oriented Programming，简称 ***OOP***，是一种程序设计思想。OOP 把对象作为程序的基本单元，一个对象包含了数据和操作数据的函数。

面向过程的程序设计把计算机程序视为一系列的命令集合，即一组函数的顺序执行。为了简化程序设计，面向过程把函数继续切分为子函数，即把大块函数通过切割成小块函数来降低系统的复杂度。

而面向对象的程序设计把计算机程序视为***一组对象的集合***，而每个对象都可以接收其他对象发过来的***消息***，并处理这些消息，计算机程序的执行就是一系列消息在各个对象之间传递。

在 Python 中，***所有数据类型都可以视为对象***（一切皆对象），当然也可以自定义对象。自定义的对象数据类型就是面向对象中的类（Class）的概念。

面向对象的设计思想是从自然界中来的，因为在自然界中，类（Class）和实例（Instance）的概念是很自然的。Class 是一种抽象概念，比如我们定义的 Class——Student，是指学生这个概念，而实例（Instance）则是一个个具体的 Student，比如，Bart Simpson 和 Lisa Simpson 是两个具体的 Student。

所以，面向对象的设计思想是抽象出 Class，根据 Class 创建 Instance。

面向对象的抽象程度又比函数要高，因为一个 Class 既包含数据，又包含操作数据的方法。

数据***封装***、***继承***和***多态***是面向对象的三大特点，我们后面会详细讲解。

### 类和实例

面向对象最重要的概念就是类（Class）和实例（Instance），必须牢记类是抽象的模板，比如 Student 类，而实例是根据类创建出来的一个个具体的 “对象”，每个对象都拥有相同的方法，但各自的数据可能不同。

以 Student 类为例，在 Python 中，定义类是通过`class`关键字：

```python
class Student(object):	# 括号中的object是父类    pass
```

定义好了`Student`类，就可以根据`Student`类创建出`Student`的实例，创建实例是通过类名 +() 实现的。

可以自由地给一个实例变量绑定属性，比如，给实例`bart`绑定一个`name`属性：

```python
>>> bart.name = 'Bart Simpson'>>> bart.name'Bart Simpson'
```

#### `__init__`方法

由于类可以起到模板的作用，因此，可以在创建实例的时候，把一些我们认为必须绑定的属性强制填写进去。通过定义一个特殊的`__init__`方法，在创建实例的时候，就把`name`，`score`等属性绑上去：

```python
class Student(object):    def __init__(self, name, score):        self.name = name        self.score = score
```

**注意**：特殊方法 “__init__” 前后分别有***两个***下划线！！！

注意到`__init__`方法的第一个参数永远是`self`，表示创建的实例本身，因此，在`__init__`方法内部，就可以把各种属性绑定到`self`，因为`self`就指向创建的实例本身。（相当于自动绑定）

有了`__init__`方法，在创建实例的时候，就不能传入空的参数了，必须传入与`__init__`方法匹配的参数，但`self`不需要传，Python 解释器自己会把实例变量传进去。

和普通的函数相比，在类中定义的函数只有一点不同，就是第一个参数永远是实例变量`self`，并且调用时不用传递该参数。除此之外，类的方法和普通函数没有什么区别，所以，你仍然可以用默认参数、可变参数、关键字参数和命名关键字参数。

#### 数据*封装*

面向对象编程的一个重要特点就是数据封装。在上面的`Student`类中，每个实例就拥有各自的`name`和`score`这些数据。我们可以通过函数来访问这些数据。

类是创建实例的模板，而实例则是一个一个具体的对象，各个实例拥有的数据都互相独立，互不影响。

方法就是与实例绑定的函数，和普通函数不同，方法可以直接访问实例的数据；

通过在实例上调用方法，我们就直接操作了对象内部的数据，但无需知道方法内部的实现细节。

和静态语言不同，Python 允许对实例变量绑定任何数据，也就是说，对于两个实例变量，虽然它们都是同一个类的不同实例，但拥有的变量名称都可能不同。

### 访问限制

如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线`__`，在 Python 中，实例的变量名如果以`__`开头，就变成了一个私有变量（**private**），只有内部可以访问，外部不能访问。

需要特别注意的是，在 Python 中，变量名类似`__xxx__`的，也就是以双下划线开头，并且以双下划线结尾的，是**特殊变量**，特殊变量是可以直接访问的，不是 private 变量，所以，不能用`__name__`、`__score__`这样的变量名。

有些时候，你会看到以一个下划线开头的实例变量名，比如`_name`，这样的实例变量外部是可以访问的，但是，**按照约定俗成的规定**，当你看到这样的变量时，意思就是，“虽然我可以被访问，但是，*请把我视为私有变量，不要随意访问*”。

双下划线开头的实例变量是不是一定不能从外部访问呢？其实也不是。不能直接访问`__name`是因为 Python 解释器对外把`__name`变量改成了`_Student__name`，所以，仍然可以通过`_Student__name`来访问`__name`变量。

但是不同版本的 Python 解释器可能会把`__name`改成不同的变量名。因此强烈不推荐这种强行访问的做法。

### 继承和多态

在 OOP 程序设计中，当我们定义一个 class 的时候，可以从某个现有的 class 继承，新的 class 称为子类（Subclass），而被继承的 class 称为基类、父类或**超类**（Base class、Super class）。

继承有什么好处？最大的好处是子类获得了父类的全部功能。由于`Animal`实现了`run()`方法，因此，`Dog`和`Cat`作为它的子类，什么事也没干，就自动拥有了`run()`方法。

当子类和父类都存在相同的`run()`方法时，我们说，子类的`run()`覆盖了父类的`run()`，在代码运行的时候，总是会调用子类的`run()`。这样，我们就获得了继承的另一个好处：**多态**。

判断一个变量是否是某个类型可以用`isinstance()`判断：

```python
>>> isinstance(a, list)True>>> isinstance(b, Animal)True>>> isinstance(c, Dog)True
```

所以在继承关系中，如果一个实例的数据类型是某个子类，那它的数据类型也可以被看做是父类。但是，反过来就不行：

```python
>>> b = Animal()>>> isinstance(b, Dog)False
```

新增一个`Animal`的子类，不必对`run_twice()`做任何修改，实际上，任何依赖`Animal`作为参数的函数或者方法都可以不加修改地正常运行，原因就在于多态。

多态的好处就是，当我们需要传入`Dog`、`Cat`、`Tortoise`…… 时，我们只需要接收`Animal`类型就可以了，因为`Dog`、`Cat`、`Tortoise`…… 都是`Animal`类型，然后，按照`Animal`类型进行操作即可。由于`Animal`类型有`run()`方法，因此，传入的任意类型，只要是`Animal`类或者子类，就会自动调用实际类型的`run()`方法，这就是多态的意思：

对于一个变量，我们只需要知道它是`Animal`类型，无需确切地知道它的子类型，就可以放心地调用`run()`方法，而具体调用的`run()`方法是作用在`Animal`、`Dog`、`Cat`还是`Tortoise`对象上，由运行时该对象的确切类型决定，这就是多态真正的威力：调用方只管调用，不管细节，而当我们新增一种`Animal`的子类时，只要确保`run()`方法编写正确，不用管原来的代码是如何调用的。这就是著名的 “开闭” 原则：

> 对扩展开放：允许新增`Animal`子类；
>
> 对修改封闭：不需要修改依赖`Animal`类型的`run_twice()`等函数。

继承还可以一级一级地继承下来，就好比从爷爷到爸爸、再到儿子这样的关系。而任何类，最终都可以追溯到根类 object，这些继承关系看上去就像一颗倒着的树。

对于静态语言（例如 Java）来说，如果需要传入`Animal`类型，则传入的对象必须是`Animal`类型或者它的子类，否则，将无法调用`run()`方法。

对于 Python 这样的动态语言来说，则不一定需要传入`Animal`类型。只需要保证传入的对象有一个`run()`方法就可以了：

```python
class Timer(object):    def run(self):        print('Start...')
```

> If it looks like a duck, walks like a duck, and quacks like a duck, it must be a duck!
>
> 如果它看起来像鸭子、游泳像鸭子、叫声像鸭子，那么它可能就是只鸭子。

这就是动态语言的 “**鸭子类型**”，它并不要求严格的继承体系，一个对象只要 “看起来像鸭子，走起路来像鸭子”，那它就可以被看做是鸭子。

Python 的 “file-like object“就是一种鸭子类型。对真正的文件对象，它有一个`read()`方法，返回其内容。但是，许多对象，只要有`read()`方法，都被视为 “file-like object“。许多函数接收的参数就是 “file-like object“，你不一定要传入真正的文件对象，完全可以传入任何实现了`read()`方法的对象。

继承可以把父类的所有功能都直接拿过来，这样就不必重零做起，子类只需要新增自己特有的方法，也可以把父类不适合的方法**覆盖**重写。动态语言的鸭子类型特点决定了继承不像静态语言那样是必须的。

### 获取对象信息

#### type

`type()`函数返回对应的 Class 类型或者基本类型。

##### 类型常量

```python
types.NoneTypeNone 的类型。types.FunctionTypetypes.LambdaType用户自定义函数以及由 lambda 表达式所创建函数的类型。types.GeneratorTypegenerator 迭代器对象的类型，由生成器函数创建。
```

```python
>>> import types>>> def fn():...     pass...>>> type(fn)==types.FunctionTypeTrue>>> type(abs)==types.BuiltinFunctionTypeTrue>>> type(lambda x: x)==types.LambdaTypeTrue>>> type((x for x in range(10)))==types.GeneratorTypeTrue
```

#### isinstance

```python
isinstance(object, classinfo)
```

主要用于判断自建对象的类型，当然也可以判断基本数据类型。

如果 *object* 参数是 *classinfo* 参数的实例，或其（直接、间接或 [virtual](https://docs.python.org/zh-cn/3/glossary.html#term-abstract-base-class) ）子类的实例，则返回 `True`。 如果 *object* 不是给定类型的对象，则总是返回 `False`。如果 *classinfo* 是类型对象的元组（或由该类元组递归生成）或多个类型的 [union 类型](https://docs.python.org/zh-cn/3/library/stdtypes.html#types-union)，那么当 *object* 是其中任一类型的实例时就会返回 `True`。如果 *classinfo* 不是某个类型或类型元组，将会触发 [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError) 异常。

#### dir

如果要获得一个对象的所有属性和方法，可以使用`dir()`函数，它返回一个包含字符串的 list，比如，获得一个 str 对象的所有属性和方法：

```python
>>> dir('ABC')['__add__', '__class__',..., '__subclasshook__', 'capitalize', 'casefold',..., 'zfill']
```

类似`__xxx__`的属性和方法在 Python 中都是有特殊用途的，比如`__len__`方法返回长度。在 Python 中，如果你调用`len()`函数试图获取一个对象的长度，实际上，在`len()`函数内部，它自动去调用该对象的`__len__()`方法。

配合`getattr()`、`setattr()`以及`hasattr()`，我们可以直接操作一个对象的状态，紧接着，可以测试该对象的属性。

##### getattr

```python
getattr(object, name[, default])
```

返回对象命名属性的值。*name* 必须是字符串。如果该字符串是对象的属性之一，则返回该属性的值。例如， `getattr(x, 'foobar')` 等同于 `x.foobar`。如果指定的属性不存在，且提供了 *default* 值，则返回它，否则触发 [`AttributeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError)。

##### setattr

```python
setattr(object, name, value)
```

本函数与 [`getattr()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=getattr#getattr) 相对应。其参数为一个对象、一个字符串和一个任意值。字符串可以为某现有属性的名称，或为新属性。只要对象允许，函数会将值赋给属性。如 `setattr(x, 'foobar', 123)` 等价于 `x.foobar = 123`。

##### hasattr

```python
hasattr(object, name)
```

该实参是一个对象和一个字符串。如果字符串是对象的属性之一的名称，则返回 `True`，否则返回 `False`。

*（此功能是通过调用 `getattr(object, name)` 看是否有 [`AttributeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError) 异常来实现的。）*

### 实例属性和类属性

可以直接在 class 中定义属性，这种属性是类属性，归`Student`类所有：

```python
class Student(object):    count = 0    def __init__(self, name):        self.name = name        Student.count += 1 # 前面的类名不可省略
```

当我们定义了一个类属性后，这个属性虽然归类所有，但类的所有实例都可以访问到。

在编写程序的时候，千万不要对实例属性和类属性使用相同的名字，因为相同名称的实例属性将屏蔽掉类属性，但是当你删除实例属性后，再使用相同的名称，访问到的将是类属性。

### 类方法和静态方法

#### 类方法

```python
@classmethoddef 类方法名(cls):    pass
```

* 类方法需要用 **修饰器** `@classmethod` 来标识，告诉解释器这是一个类方法
* 类方法的 **第一个参数** 应该是 `cls`
  * 由 **哪一个类** 调用的方法，方法内的 `cls` 就是 **哪一个类的引用**
  * 这个参数和 **实例方法** 的第一个参数是 `self` 类似
  * **提示** 使用其他名称也可以，不过习惯使用 `cls`

3. 通过 **类名.** 调用 类方法，调用方法时**不需要**传递 `cls` 参数
4. **在类方法内部**
   * 可以通过 `cls.` **访问类的属性**
   * 也可以通过 `cls.` **调用其他的类方法**

#### 静态方法

* 在开发时，如果需要在 **类** 中封装一个方法，这个方法：
  * 既 **不需要** 访问 **实例属性** 或者调用 **实例方法**
  * 也 **不需要** 访问 **类属性** 或者调用 **类方法**

* 这个时候，可以把这个方法封装成一个 **静态方法**

**语法如下**

```python
@staticmethoddef 静态方法名():    pass
```

* **静态方法** 需要用 **修饰器** `@staticmethod` 来标识，**告诉解释器这是一个静态方法**
* 通过 **类名.** 调用 **静态方法**

### 限制实例属性：`__slots__`

为了达到限制的目的，Python 允许在定义 class 的时候，定义一个特殊的`__slots__`变量，来限制该 class 实例能添加的属性：

```python
class Student(object):    __slots__ = ('name', 'age') 
```

使用`__slots__`要注意，`__slots__`定义的属性仅对当前类实例起作用，对继承的子类是不起作用的。

除非在子类中也定义`__slots__`，这样，子类实例允许定义的属性就是自身的`__slots__`加上父类的`__slots__`。

### 封装扩展：@property

对于类的方法，装饰器一样起作用。Python内置的`@property`装饰器就是负责把一个方法变成属性调用的：

```python
class Student(object):    @property    def score(self):        return self._score    @score.setter    def score(self, value):        if not isinstance(value, int):            raise ValueError('score must be an integer!')        if value < 0 or value > 100:            raise ValueError('score must between 0 ~ 100!')        self._score = value
```

把一个getter方法变成属性，只需要加上`@property`就可以了，此时，`@property`本身又创建了另一个装饰器`@score.setter`，负责把一个setter方法变成属性赋值，于是，我们就拥有了一个可控的属性操作。

还可以定义只读属性，只定义getter方法，不定义setter方法就是一个只读属性。

**要特别注意**：属性的方法名不要和实例变量重名。例如，以下的代码是错误的：

```python
class Student(object):    # 方法名称和实例变量均为birth:    @property    def birth(self):        return self.birth
```

这是因为调用`s.birth`时，首先转换为方法调用，在执行`return self.birth`时，又视为访问`self`的属性，于是又转换为方法调用，造成**无限递归**，最终导致栈溢出报错`RecursionError`。

### 多继承

首先，主要的类层次仍按照哺乳类和鸟类设计：

```python
class Animal(object):    passclass Mammal(Animal):    passclass Bird(Animal):    passclass Dog(Mammal):    passclass Bat(Mammal):    passclass Parrot(Bird):    passclass Ostrich(Bird):    pass
```

现在，我们要给动物再加上`Runnable`和`Flyable`的功能，只需要先定义好`Runnable`和`Flyable`的类：

```python
class Runnable(object):    def run(self):        print('Running...')class Flyable(object):    def fly(self):        print('Flying...')
```

对于需要`Runnable`功能的动物，就多继承一个`Runnable`，例如`Dog`：

```python
class Dog(Mammal, Runnable):    pass
```

对于需要`Flyable`功能的动物，就多继承一个`Flyable`，例如`Bat`：

```python
class Bat(Mammal, Flyable):    pass
```

通过多重继承，一个子类就可以同时获得多个父类的所有功能。

#### Mixin：混入

在设计类的继承关系时，通常，主线都是单一继承下来的，例如，`Ostrich`继承自`Bird`。但是，如果需要 “混入” 额外的功能，通过多重继承就可以实现，比如，让`Ostrich`除了继承自`Bird`外，再同时继承`Runnable`。这种设计通常称之为 MixIn。

为了更好地看出继承关系，我们把`Runnable`和`Flyable`改为`RunnableMixIn`和`FlyableMixIn`。类似的，你还可以定义出肉食动物`CarnivorousMixIn`和植食动物`HerbivoresMixIn`，让某个动物同时拥有好几个 MixIn：

```python
class Dog(Mammal, RunnableMixIn, CarnivorousMixIn):    pass
```

MixIn 的目的就是给一个类增加多个功能，这样，在设计类的时候，我们优先考虑通过多重继承来组合多个 MixIn 的功能，而不是设计多层次的复杂的继承关系。

Python 自带的很多库也使用了 MixIn。举个例子，Python 自带了`TCPServer`和`UDPServer`这两类网络服务，而要同时服务多个用户就必须使用多进程或多线程模型，这两种模型由`ForkingMixIn`和`ThreadingMixIn`提供。通过组合，我们就可以创造出合适的服务来。

只允许单继承的语言（如 Java）不能使用 MixIn 的设计。

### 特殊函数：定制类

#### `__str__`

```python
>>> class Student(object):...     def __init__(self, name):...         self.name = name...     def __str__(self):...         return 'Student object (name: %s)' % self.name...>>> print(Student('Michael'))Student object (name: Michael)
```

#### `__repr__`

`__str__()`返回用户看到的字符串，而`__repr__()`返回程序开发者看到的字符串，也就是说，`__repr__()`是为调试服务的。

```python
class Student(object):    def __init__(self, name):        self.name = name    def __str__(self):        return 'Student object (name=%s)' % self.name    __repr__ = __str__	# 简化写法
```

#### `__iter__`

如果一个类想被用于`for ... in`循环，类似list或tuple那样，就必须实现一个`__iter__()`方法，该方法返回一个迭代对象，然后，Python的for循环就会不断调用该迭代对象的`__next__()`方法拿到循环的下一个值，直到遇到`StopIteration`错误时退出循环。

```python
class Fib(object):    def __init__(self):        self.a, self.b = 0, 1 # 初始化两个计数器a，b    def __iter__(self):        return self # 实例本身就是迭代对象，故返回自己    def __next__(self):        self.a, self.b = self.b, self.a + self.b # 计算下一个值        if self.a > 100000: # 退出循环的条件            raise StopIteration()        return self.a # 返回下一个值    if __name__ == '__main__':    f = Fib()    for a in f:        print(a)
```

#### `__call__`

任何类，只需要定义一个`__call__()`方法，就可以直接对实例进行调用。请看示例：

```python
class Student(object):    def __init__(self, name):        self.name = name    def __call__(self):        print('My name is %s.' % self.name)
```

调用方式如下：

```python
>>> s = Student('Michael')>>> s() My name is Michael.
```

`__call__()`还可以定义参数。对实例进行直接调用就好比对一个函数进行调用一样，所以你完全可以把对象看成函数，把函数看成对象，因为这两者之间本来就没啥根本的区别。

如果你把对象看成函数，那么函数本身其实也可以在运行期动态创建出来，因为类的实例都是运行期创建出来的，这么一来，我们就模糊了对象和函数的界限。

那么，怎么判断一个变量是对象还是函数呢？其实，更多的时候，我们需要判断一个对象是否能被调用，能被调用的对象就是一个`Callable`对象。

```python
>>> callable(Student())True>>> callable(max)True>>> callable([1, 2, 3])False>>> callable(None)False>>> callable('str')False
```

通过`callable()`函数，我们就可以判断一个对象是否是 “可调用” 对象。

#### `__getitem__`

要表现得像 list 那样按照下标取出元素（随机访问），需要实现`__getitem__()`方法。

```python
class Fib(object):    def __getitem__(self, n):        a, b = 1, 1        for x in range(n):            a, b = b, a + b        return a
```

事实上，要正确实现一个`__getitem__()`还是有很多工作要做的，比如切片等。

此外，如果把对象看成`dict`，`__getitem__()`的参数也可能是一个可以作 key 的 object，例如`str`。

与之对应的是`__setitem__()`方法，把对象视作 list 或 dict 来对集合赋值。最后，还有一个`__delitem__()`方法，用于删除某个元素。

总之，通过上面的方法，我们自己定义的类表现得和 Python 自带的 list、tuple、dict 没什么区别，这完全归功于动态语言的 “鸭子类型”，不需要强制继承某个接口。

#### `__getattr__`

Python 还有另一个机制，那就是写一个`__getattr__()`方法，动态返回一个属性。修改如下：

```python
class Student(object):    def __init__(self):        self.name = 'Michael'    def __getattr__(self, attr):        if attr == 'score':            return 99
```

当调用不存在的属性时，比如`score`，Python 解释器会试图调用`__getattr__(self, 'score')`来尝试获得属性，这样，我们就有机会返回`score`的值。

返回函数也是完全可以的：

```python
class Student(object):    def __getattr__(self, attr):        if attr=='age':            return lambda: 25
```

注意，只有在没有找到属性的情况下，才调用`__getattr__`，已有的属性，比如`name`，不会在`__getattr__`中查找。

此外，注意到任意调用如`s.abc`都会返回`None`，这是因为我们定义的`__getattr__`默认返回就是`None`。要让 class 只响应特定的几个属性，我们就要按照约定，抛出`AttributeError`的错误：

```python
class Student(object):    def __getattr__(self, attr):        if attr=='age':            return lambda: 25        raise AttributeError('\'Student\' object has no attribute \'%s\'' % attr)
```

这种完全动态调用的特性有什么实际作用呢？作用就是，可以针对完全动态的情况作调用。

##### 实例：RESTful API链式调用生成API

利用完全动态的`__getattr__`，我们可以写出一个链式调用：

```python
class Chain(object):    def __init__(self, path=''):       self.__path = path   def __getattr__(self, path):       return Chain('%s/%s' % (self.__path, path)) # 非常巧妙地实现了链式调用   def __call__(self, path):       return Chain('%s/%s' % (self.__path, path)) # 加入__call__是为了方便带参数的构造   def __str__(self):       return self.__path   __repr__ = __str__print(Chain().api('login'))>>>/api/login
```

### 枚举：Enum

### 元类：Metaclass

## 异常处理

`SyntaxError`：语法错误

执行时检测到的错误称为 *异常*，异常并不一定导致严重的后果。

```python
while True:     try:         x = int(input("Please enter a number: "))         break     except ValueError:         print("Oops!  That was no valid number.  Try again...")
```

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句的工作原理如下：

- 首先，执行 *try 子句* （[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 和 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 关键字之间的（多行）语句）。
- 如果没有触发异常，则跳过 *except 子句*，[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句执行完毕。
- 如果在执行 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 子句时发生了异常，则跳过该子句中剩下的部分。 如果异常的类型与 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 关键字后指定的异常相匹配，则会执行 *except 子句*，然后跳到 try/except 代码块之后继续执行。
- 如果发生的异常与 *except 子句* 中指定的异常不匹配，则它会被传递到外部的 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句中；如果没有找到处理程序，则它是一个 *未处理异常* 且执行将终止并输出错误消息。

可以有多个 *except 子句* 来为不同的异常指定处理程序， 但最多只有一个处理程序会被执行。 处理程序只处理对应的 *try 子句* 中发生的异常，而不处理同一 `try` 语句内其他处理程序中的异常。 *except 子句* 可以用带圆括号的元组来指定多个异常，例如:

```python
except (RuntimeError, TypeError, NameError):    pass
```

except子句中的类和异常类相同或者是其父类时，它们相兼容。

```python
class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

for cls in [B, C, D]:
    try:
        raise cls()
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")
 # B C D
```

如果颠倒 *except 子句* 的顺序（把 `except B` 放在最前），则会输出 B, B, B ，即触发了第一个匹配的 *except 子句*。

可以选择让最后一个 except 子句省略异常名称，但在此之后异常值必须从 `sys.exc_info()[1]` 获取。

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) ... [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 语句具有可选的 *else 子句*，该子句如果存在，它必须放在所有 *except 子句* 之后。 

它适用于 *try 子句* **没有引发异常但又必须要执行**的代码。 

发生的异常可能具有关联值，即异常 *参数* 。是否需要参数，以及参数的类型取决于异常的类型。

*except 子句* 可以在异常名称后面指定一个变量。 这个变量会绑定到一个异常实例并将参数存储在 `instance.args` 中。 为了方便起见，该异常实例定义了 `__str__()` 以便能直接打印参数而无需引用 `.args`。 也可以在引发异常之前先实例化一个异常并根据需要向其添加任何属性。

异常处理程序不仅会处理在 *try 子句* 中发生的异常，还会处理在 *try 子句* 中调用（包括间接调用）的函数。

### 主动触发异常

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 语句支持强制触发指定的异常。例如：

```python
>>> raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere
```

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 唯一的参数就是要触发的异常。这个参数必须是异常实例或异常类（派生自 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) 类）。如果传递的是异常类，将通过调用没有参数的构造函数来隐式实例化。

如果只想判断是否触发了异常，但并不打算处理该异常，则可以使用更简单的 [`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 语句重新触发异常。

```python
>>> try:
        raise NameError('HiThere')
    except NameError:
        print('An exception flew by!')
        raise
   
An exception flew by!
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
NameError: HiThere
```

### 异常链

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 语句支持可选的 [`from`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 子句，该子句用于启用链式异常。

进行异常转换时，这种方式很有用。

```python
>>> def func():
...     raise ConnectionError
...
>>> try:
...     func()
... except ConnectionError as exc:
...     raise RuntimeError('Failed to open database') from exc
...
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
  File "<stdin>", line 2, in func
ConnectionError

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "<stdin>", line 4, in <module>
RuntimeError: Failed to open database
```

异常链会在 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 或 [`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 子句内部引发异常时自动生成。 这可以通过使用 `from None` 这样的写法来禁用。

不论是以直接还是间接的方式，异常都应从 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) 类派生。

```python
class InputError(Exception):
    '''当输出有误时，抛出此异常'''
    #自定义异常类型的初始化
    def __init__(self, value):
        self.value = value
    # 返回异常类对象的说明信息
    def __str__(self):
        return ("{} is invalid input".format(self.value))
   
try:
    raise InputError(1) # 抛出 MyInputError 这个异常
except InputError as err:
    print('error: {}'.format(err))
```

### 最后的清理操作

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句还有一个可选子句，用于定义在所有情况下都必须要执行的清理操作。例如：

```python
>>> try:
...     raise KeyboardInterrupt
... finally:
...     print('Goodbye, world!')
...
Goodbye, world!
KeyboardInterrupt
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
```

如果存在 [`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 子句，则 `finally` 子句是 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句结束前执行的最后一项任务。不论 `try` 语句是否触发异常，都会执行 `finally` 子句。以下内容介绍了几种比较复杂的触发异常情景：

- 如果执行 `try` 子句期间触发了某个异常，则某个 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 子句应处理该异常。如果该异常没有 `except` 子句处理，在 `finally` 子句执行后会被重新触发。
- `except` 或 `else` 子句执行期间也会触发异常。 同样，该异常会在 `finally` 子句执行之后被重新触发。
- 如果 `finally` 子句中包含 [`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break)、[`continue`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#continue) 或 [`return`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#return) 等语句，异常将不会被重新引发。
- 如果执行 `try` 语句时遇到 [`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break),、[`continue`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#continue) 或 [`return`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#return) 语句，则 `finally` 子句在执行 `break`、`continue` 或 `return` 语句之前执行。
- 如果 `finally` 子句中包含 `return` 语句，则返回值来自 `finally` 子句的某个 `return` 语句的返回值，而不是来自 `try` 子句的 `return` 语句的返回值。

```python
>>> def divide(x, y):
...     try:
...         result = x / y
...     except ZeroDivisionError:
...         print("division by zero!")
...     else:
...         print("result is", result)
...     finally:
...         print("executing finally clause")
...
>>> divide(2, 1)
result is 2.0
executing finally clause
>>> divide(2, 0)
division by zero!
executing finally clause
>>> divide("2", "1")
executing finally clause
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in divide
TypeError: unsupported operand type(s) for /: 'str' and 'str'
```

如上所示，任何情况下都会执行 [`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 子句。[`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 子句不处理两个字符串相除触发的 [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError)，因此会在 `finally` 子句执行后被重新触发。

在实际应用程序中，[`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 子句对于释放外部资源（例如文件或者网络连接）非常有用，无论是否成功使用资源。

## 多线程