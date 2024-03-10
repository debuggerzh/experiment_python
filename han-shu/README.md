# 函数

函数是组织好的、可重复使用的，用来实现单一或相关联功能的代码段。

函数能提高应用的模块性和代码的重复利用率。

## 定义

* 函数代码块以 **def** 关键词开头，后接函数标识符名称和圆括号 **()**，函数内容以冒号 **:** 起始，并且缩进。
* 任何传入参数和自变量必须放在圆括号中间，圆括号之间可以用于定义参数。
* 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
* **return \[表达式]** 结束函数，选择性地返回一个值给调用方，不带表达式的 return 相当于返回 None。

## 调用

可以通过另一个函数调用执行，也可以直接从 Python 命令提示符执行。

## 参数

### **必需参数**

必需参数须以正确的顺序传入函数。调用时的数量必须和声明时的一样。

### **关键字参数**

关键字参数和函数调用关系紧密，函数调用使用关键字参数来确定传入的参数值。

使用关键字参数允许函数调用时参数的顺序与声明时不一致，因为 Python 解释器能够用参数名匹配参数值。

定义及调用函数时，关键字参数后面不能再出现位置参数。

声明函数时，参数中星号 **\*** 可以单独出现。单独出现星号 **\*** 后的参数必须用**关键字**传入。

```
fun(参数名=参数值)
```

### **默认参数**

```python
def printinfo( name, age = 35 ):	# age为默认参数，默认值为35
    pass
```

### **不定长参数**

```python
def functionname([formal_args,] *var_args_tuple , **var_args_dict):
   "函数_文档字符串"
   function_suite
   return [expression]
```

加了一个星号 **\*** 的参数会以元组(tuple)的形式导入，存放所有未命名的变量参数。

加了两个星号 **\*\*** 的参数会以字典的形式导入。

### 强制位置参数（Python3.8新增）

声明函数时，参数中斜杠 **/** 可以单独出现。单独出现斜杠 **/** 之前的参数必须使用指定位置参数。

在以下的例子中，形参 a 和 b 必须使用指定位置参数，c 或 d 可以是位置形参或关键字形参，而 e 或 f 要求为关键字形参:

```python
def f(a, b, /, c, d, *, e, f):
    print(a, b, c, d, e, f)
```

### **参数传递**

* **不可变类型：**类似 C++ 的值传递，如整数、字符串、元组。如 fun(a)，传递的只是 a 的值，没有影响 a 对象本身。如果在 fun(a) 内部修改 a 的值，则是新生成一个 a 的对象。
* **可变类型：**类似 C++ 的引用传递，如 列表，字典。如 fun(la)，则是将 la 真正的传过去，修改后 fun 外部的 la 也会受影响

## 返回值

**return \[表达式]** 语句用于退出函数，选择性地向调用方返回一个表达式。不带参数值的return语句返回None。

## 匿名函数（lambda表达式）

python 使用 lambda 来创建匿名函数。所谓匿名，意即不再使用 def 语句这样标准的形式定义一个函数。

* lambda 只是一个表达式，函数体比 def 简单很多。
* lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
* lambda 函数拥有**自己的命名空间**，且不能访问自己参数列表之外或全局命名空间里的参数。
* 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

### **语法**

```python
fun = lambda [arg1 [,arg2,.....argn]] : expression
```

### **调用**

`fun(arg1 [,arg2,.....argn])`

## 数学函数

```python
abs(x)
ceil(x)
exp(x)
fabs(x)
floor(x)
log(x)
log10(x)
modf(x)	# 返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示。
pow(x,y[,z])	# 等效于pow(x,y) % z
sqrt(x)
```

### **sum**

```
sum(iterable, /, start=0)
```

从 _start_ 开始自左向右对 _iterable_ 的项求和并返回总计值。 _iterable_ 的项通常为数字，而 start 值则不允许为字符串。

对某些用例来说，存在 [`sum()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=eval#sum) 的更好替代。 拼接字符串序列的更好更快方式是调用 `''.join(sequence)`。

### **max函数(min同理)**

```
max(iterable, *[, key, default])
max(arg1, arg2, *args[, key])
```

函数功能为取传入的多个参数中的最大值，或者传入的可迭代对象元素中的最大值。

默认数值型参数，取值大者；字符型参数，取字母表排序靠后者。

还可以传入命名参数 key，其为一个函数，用来指定取最大值的方法。

```python
s = [  {'name': 'sumcet', 'age': 18},  {'name': 'bbu', 'age': 11}]
a = max(s, key=lambda x: x['age'])
print(a)	# {'name': 'sumcet', 'age': 18}
```

如果只传入一个参数，则该参数必须为可迭代对象，返回其中的最大元素。

传入可迭代对象为空时，必须指定参数 default，用来返回默认值输出。

对于序列型参数，会依次按照索引位置的值进行比较取最大者。

```python
>>> max([1,2],[3])
[3]
>>> max([1,2],[1,3])
[1, 3]
```

### 随机函数

主要依赖于`random`模块。

```python
random.random()	# 返回 [0.0, 1.0) 范围内的下一个随机浮点数# 几乎所有模块函数都依赖于这一基本函数
random.choice(seq)	# 从非空序列 seq 返回一个随机元素。 如果 seq 为空，则引发 IndexError
random.randrange(start, stop[, step = 1])	# 从 range(start, stop[, step]) 返回一个随机选择的元素# 这相当于 choice(range(start, stop, step)) ，但实际上并没有构建一个 range 对象
random.randint(a, b)	# 返回随机整数 N 满足 a <= N <= b# 相当于 randrange(a, b+1)
random.uniform(a, b)	# 用来生成 [a,b] 之间的随意浮点数，包括两个边界值# 取决于等式 a + (b-a) * random() 中的浮点舍入，终点 b 可能包括或不包括在该范围内
random.shuffle(x[, random])	# 将一个列表中的元素打乱# 可选参数 random 是一个0参数函数，在 [0.0, 1.0) 中返回随机浮点数；默认情况下，这是函数 random() 
random.sample(population/sequence, k, *, counts=None)# 返回从总体序列或集合中选择的 k 长度列表， 用于无重复的随机抽样# counts指定元素的权重。sample(['red', 'blue'], counts=[4, 2], k=5)# 等价于sample(['red', 'red', 'red', 'red', 'blue', 'blue'], k=5)# 要从一系列整数中选择样本，请使用 range() 对象作为参数。 对于从大量人群中采样，这种方法特别快速且节省空间sample(range(10000000), k=60)# 如果样本大小大于总体大小，则引发 ValueError 。
```

## 函数式编程

函数是 Python 内建支持的一种封装，我们通过把大段代码拆成函数，通过一层一层的函数调用，就可以把复杂任务分解成简单的任务，这种分解可以称之为面向过程的程序设计。

_**函数就是面向过程的程序设计的基本单元**_。

而函数式编程（请注意多了一个 “式” 字）——Functional Programming，虽然也可以归结到面向过程的程序设计，但其思想更接近**数学计算**。

函数式编程就是一种抽象程度很高的编程范式，纯粹的函数式编程语言编写的函数没有变量，因此，任意一个函数，只要输入是确定的，输出就是确定的，这种纯函数我们称之为没有副作用。而允许使用变量的程序设计语言，由于函数内部的变量状态不确定，同样的输入，可能得到不同的输出，因此，这种函数是有副作用的。

函数式编程的一个**特点**就是，允许把函数本身作为参数传入另一个函数，还允许返回一个函数！

Python 对函数式编程提供部分支持。由于 Python 允许使用变量，因此，Python 不是纯函数式编程语言。

### 高阶函数

#### map

```
map(function, iterable, ...)
```

返回一个将 _function_ 应用于 _iterable_ 中每一项并输出其结果的迭代器。

```python
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

&#x20;如果传入了额外的 _iterable_ 参数，_function_ 必须接受相同个数的实参并被应用于从所有可迭代对象中并行获取的项。 当有多个可迭代对象时，最短的可迭代对象耗尽则整个迭代就将结束。&#x20;

```python
>>> a = [1, 2, 3, 4, 5]
>>> b = [5, 4, 3, 2, 1]
>>> list(map(int.__add__, a, b))
[6, 6, 6, 6, 6]
```

#### filter

```
filter(function, iterable)
```

用 _iterable_ 中函数 _function_ 返回**真**的那些元素，构建一个新的迭代器。_iterable_ 可以是一个序列，一个支持迭代的容器，或一个迭代器。如果 _function_ 是 `None` ，则会假设它是一个身份函数，即 _iterable_ 中所有返回假的元素会被移除。

### 闭包

在一个内部函数中，对外部作用域的变量进行引用，(并且一般外部函数的返回值为内部函数)，那么内部函数就被认为是闭包。

![这里incrementBy就是一个闭包。](<../.gitbook/assets/image (1).png>)



### **修饰器（装饰器）：decorator**

返回值为另一个函数的函数，通常使用 `@wrapper` 语法形式来进行函数变换。也可理解为对函数进行变换。 装饰器的常见例子包括 [`classmethod()`](https://docs.python.org/zh-cn/3/library/functions.html#classmethod) 和 [`staticmethod()`](https://docs.python.org/zh-cn/3/library/functions.html#staticmethod)。

函数对象有一个`__name__`属性，可以拿到函数的名字。

```python
def now():
    ...     
    print('2015-3-25')
now.__name__
'now'
```

现在，假设我们要增强`now()`函数的功能，比如，在函数调用前后自动打印日志，但又不希望修改`now()`函数的定义，这种在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）。

装饰器语法只是一种**语法糖**，以下两个函数定义在语义上完全等价:

```python
def f(arg):
    ...
f = staticmethod(f)    # 等价于

@staticmethod
def f(arg):
    ...
```

**即**：`function = decorator(function)` ;&#x20;

`class = decorator(class)`

### functools模块

主要是为[函数式编程](https://so.csdn.net/so/search?q=%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BC%96%E7%A8%8B\&spm=1001.2101.3001.7020)而设计，用于增强函数功能。

#### partial：偏函数

```python
functools.partial(func, /, *args, **keywords)
```

返回一个新的 [部分对象](https://docs.python.org/zh-cn/3/library/functools.html?highlight=reduce#partial-objects)，当被调用时其行为类似于 _func_ 附带位置参数 _args_ 和关键字参数 _keywords_ 被调用。偏函数可以**固定**住原函数的部分参数，从而在调用时更简单。

[`partial()`](https://docs.python.org/zh-cn/3/library/functools.html?highlight=reduce#functools.partial) 会被“冻结了”一部分函数参数和/或关键字的部分函数应用所使用，从而得到一个具有简化签名的新对象。 例如，[`partial()`](https://docs.python.org/zh-cn/3/library/functools.html?highlight=reduce#functools.partial) 可用来创建一个行为类似于 [`int()`](https://docs.python.org/zh-cn/3/library/functions.html#int) 函数的可调用对象，其中 _base_ 参数默认为二：

```python
>>> from functools import partial
>>> basetwo = partial(int, base=2)
>>> basetwo.__doc__ = 'Convert base 2 string to an int.'
>>> basetwo('10010')
18
```

#### [reduce](./#undefined)

```python
functools.reduce(function, iterable[, initializer])
```

将两个参数的 _function_ 从左至右积累地应用到 _iterable_ 的条目，以便将该可迭代对象缩减为单一的值。 例如，`reduce(lambda x, y: x+y, [1, 2, 3, 4, 5])` 是计算 `((((1+2)+3)+4)+5)` 的值。

如果存在可选项 _initializer_，它会被放在参与计算的可迭代对象的条目之前，并在可迭代对象为空时作为默认值。 如果没有给出 _initializer_ 并且 _iterable_ 仅包含一个条目，则将返回第一项。

```python
from functools import reduce

l = range(1,50)
print(reduce(lambda x,y:x+y, l))
# 1225
```
