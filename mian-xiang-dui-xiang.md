---
description: Object Oriented Programming, OOP
---

# 😖 面向对象

面向对象编程——Object Oriented Programming，简称 _**OOP**_，是一种程序设计思想。OOP 把对象作为程序的基本单元，一个对象包含了数据和操作数据的函数。

面向过程的程序设计把计算机程序视为一系列的命令集合，即一组函数的顺序执行。为了简化程序设计，面向过程把函数继续切分为子函数，即把大块函数通过切割成小块函数来降低系统的复杂度。

而面向对象的程序设计把计算机程序视为_**一组对象的集合**_，而每个对象都可以接收其他对象发过来的_**消息**_，并处理这些消息，计算机程序的执行就是一系列消息在各个对象之间传递。

在 Python 中，_**所有数据类型都可以视为对象**_（一切皆对象），当然也可以自定义对象。自定义的对象数据类型就是面向对象中的类（Class）的概念。

面向对象的设计思想是从自然界中来的，因为在自然界中，类（Class）和实例（Instance）的概念是很自然的。Class 是一种抽象概念，比如我们定义的 Class——Student，是指学生这个概念，而实例（Instance）则是一个个具体的 Student，比如，Bart Simpson 和 Lisa Simpson 是两个具体的 Student。

所以，面向对象的设计思想是抽象出 Class，根据 Class 创建 Instance。

面向对象的抽象程度又比函数要高，因为一个 Class 既包含数据，又包含操作数据的方法。

数据_**封装**_、_**继承**_和_**多态**_是面向对象的三大特点，我们后面会详细讲解。

## 类和实例

面向对象最重要的概念就是类（Class）和实例（Instance），必须牢记类是抽象的模板，比如 Student 类，而实例是根据类创建出来的一个个具体的 “对象”，每个对象都拥有相同的方法，但各自的数据可能不同。

以 Student 类为例，在 Python 中，定义类是通过`class`关键字：

```python
class Student(object):	# 括号中的object是父类
    pass
```

定义好了`Student`类，就可以根据`Student`类创建出`Student`的实例，创建实例是通过类名 +() 实现的。

可以自由地给一个实例变量绑定属性，比如，给实例`bart`绑定一个`name`属性：

```python
>>> bart.name = 'Bart Simpson'
>>> bart.name
'Bart Simpson'
```

### **`__init__`方法**

由于类可以起到模板的作用，因此，可以在创建实例的时候，把一些我们认为必须绑定的属性强制填写进去。通过定义一个特殊的`__init__`方法，在创建实例的时候，就把`name`，`score`等属性绑上去：

```python
class Student(object):
    def __init__(self, name, score):  
          self.name = name        
          self.score = score
```

**注意**：特殊方法 “**init**” 前后分别有_**两个**_下划线！！！

注意到`__init__`方法的第一个参数永远是`self`，表示创建的实例本身，因此，在`__init__`方法内部，就可以把各种属性绑定到`self`，因为`self`就指向创建的实例本身。（相当于自动绑定）

有了`__init__`方法，在创建实例的时候，就不能传入空的参数了，必须传入与`__init__`方法匹配的参数，但`self`不需要传，Python 解释器自己会把实例变量传进去。

和普通的函数相比，在类中定义的函数只有一点不同，就是第一个参数永远是实例变量`self`，并且调用时不用传递该参数。除此之外，类的方法和普通函数没有什么区别，所以，你仍然可以用默认参数、可变参数、关键字参数和命名关键字参数。

### **数据**_**封装**_

面向对象编程的一个重要特点就是数据封装。在上面的`Student`类中，每个实例就拥有各自的`name`和`score`这些数据。我们可以通过函数来访问这些数据。

类是创建实例的模板，而实例则是一个一个具体的对象，各个实例拥有的数据都互相独立，互不影响。

方法就是与实例绑定的函数，和普通函数不同，方法可以直接访问实例的数据；

通过在实例上调用方法，我们就直接操作了对象内部的数据，但无需知道方法内部的实现细节。

和静态语言不同，Python 允许对实例变量绑定任何数据，也就是说，对于两个实例变量，虽然它们都是同一个类的不同实例，但拥有的变量名称都可能不同。

## 访问限制

如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线`__`，在 Python 中，实例的变量名如果以`__`开头，就变成了一个私有变量（**private**），只有内部可以访问，外部不能访问。

需要特别注意的是，在 Python 中，变量名类似`__xxx__`的，也就是以双下划线开头，并且以双下划线结尾的，是**特殊变量**，特殊变量是可以直接访问的，不是 private 变量，所以，不能用`__name__`、`__score__`这样的变量名。

有些时候，你会看到以一个下划线开头的实例变量名，比如`_name`，这样的实例变量外部是可以访问的，但是，**按照约定俗成的规定**，当你看到这样的变量时，意思就是，“虽然我可以被访问，但是，_请把我视为私有变量，不要随意访问_”。

双下划线开头的实例变量是不是一定不能从外部访问呢？其实也不是。不能直接访问`__name`是因为 Python 解释器对外把`__name`变量改成了`_Student__name`，所以，仍然可以通过`_Student__name`来访问`__name`变量。

但是不同版本的 Python 解释器可能会把`__name`改成不同的变量名。因此强烈不推荐这种强行访问的做法。

## 继承和多态

在 OOP 程序设计中，当我们定义一个 class 的时候，可以从某个现有的 class 继承，新的 class 称为子类（Subclass），而被继承的 class 称为基类、父类或**超类**（Base class、Super class）。

继承有什么好处？最大的好处是子类获得了父类的全部功能。由于`Animal`实现了`run()`方法，因此，`Dog`和`Cat`作为它的子类，什么事也没干，就自动拥有了`run()`方法。

当子类和父类都存在相同的`run()`方法时，我们说，子类的`run()`覆盖了父类的`run()`，在代码运行的时候，总是会调用子类的`run()`。这样，我们就获得了继承的另一个好处：**多态**。

判断一个变量是否是某个类型可以用`isinstance()`判断：

```python
>>> isinstance(a, list)
True
>>> isinstance(b, Animal)
True
>>> isinstance(c, Dog)
True
```

所以在继承关系中，如果一个实例的数据类型是某个子类，那它的数据类型也可以被看做是父类。但是，反过来就不行：

```python
>>> b = Animal()
>>> isinstance(b, Dog)
False
```

```python
def run_twice(animal):
    animal.run()
    animal.run()
```

新增一个`Animal`的子类，不必对`run_twice()`做任何修改，实际上，任何依赖`Animal`作为参数的函数或者方法都可以不加修改地正常运行，原因就在于多态。

多态的好处就是，当我们需要传入`Dog`、`Cat`、`Tortoise`…… 时，我们只需要接收`Animal`类型就可以了，因为`Dog`、`Cat`、`Tortoise`…… 都是`Animal`类型，然后，按照`Animal`类型进行操作即可。由于`Animal`类型有`run()`方法，因此，传入的任意类型，只要是`Animal`类或者子类，就会自动调用实际类型的`run()`方法，这就是多态的意思：

对于一个变量，我们只需要知道它是`Animal`类型，无需确切地知道它的子类型，就可以放心地调用`run()`方法，而具体调用的`run()`方法是作用在`Animal`、`Dog`、`Cat`还是`Tortoise`对象上，由运行时该对象的确切类型决定，这就是多态真正的威力：调用方只管调用，不管细节，而当我们新增一种`Animal`的子类时，只要确保`run()`方法编写正确，不用管原来的代码是如何调用的。这就是著名的 **“开闭” 原则**：

> 对扩展开放：允许新增`Animal`子类；
>
> 对修改封闭：不需要修改依赖`Animal`类型的`run_twice()`等函数。

继承还可以一级一级地继承下来，就好比从爷爷到爸爸、再到儿子这样的关系。而任何类，最终都可以追溯到根类 object，这些继承关系看上去就像一颗倒着的树。

对于静态语言（例如 Java）来说，如果需要传入`Animal`类型，则传入的对象必须是`Animal`类型或者它的子类，否则，将无法调用`run()`方法。

对于 Python 这样的动态语言来说，则不一定需要传入`Animal`类型。只需要保证传入的对象有一个`run()`方法就可以了：

```python
class Timer(object):
    def run(self):  
          print('Start...')
```

> If it looks like a duck, walks like a duck, and quacks like a duck, it must be a duck!
>
> 如果它看起来像鸭子、游泳像鸭子、叫声像鸭子，那么它可能就是只鸭子。

这就是动态语言的 “**鸭子类型**”，它并不要求严格的继承体系，一个对象只要 “看起来像鸭子，走起路来像鸭子”，那它就可以被看做是鸭子。

Python 的 “file-like object“就是一种鸭子类型。对真正的文件对象，它有一个`read()`方法，返回其内容。但是，许多对象，只要有`read()`方法，都被视为 “file-like object“。许多函数接收的参数就是 “file-like object“，你不一定要传入真正的文件对象，完全可以传入任何实现了`read()`方法的对象。

继承可以把父类的所有功能都直接拿过来，这样就不必重零做起，子类只需要新增自己特有的方法，也可以把父类不适合的方法**覆盖**重写。动态语言的鸭子类型特点决定了继承不像静态语言那样是必须的。

## 获取对象信息

### **type**

```python
class type(object)
class type(name, bases, dict, **kwds)
```

`type()`函数返回对应的 Class 类型或者基本类型。

传入三个参数时，返回一个新的 type 对象。 这在本质上是 [`class`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#class) 语句的一种动态形式，_name_ 字符串即类名并会成为 [`__name__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#definition.\_\_name\_\_) 属性；_bases_ 元组包含基类并会成为 [`__bases__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#class.\_\_bases\_\_) 属性；如果为空则会添加所有类的终极基类 [`object`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=dir#object)。 _dict_ 字典包含类主体的属性和方法定义；它在成为 [`__dict__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#object.\_\_dict\_\_) 属性之前可能会被拷贝或包装。

#### **类型常量**

```python
types.FunctionType
types.BuiltinFunctionType OR types.BuiltinMethodType
# 内置函数(以C语言编写的)例如 len() 或 sys.exit() 以及内置类方法的类型。

types.LambdaType # 用户自定义函数以及由 lambda 表达式所创建函数的类型。
types.GeneratorType # generator 迭代器对象的类型，由生成器函数创建。
```

```python
>>> import types
>>> def fn():...
     pass...

>>> type(fn)==types.FunctionType
True
>>> type(abs)==types.BuiltinFunctionType
True
>>> type(lambda x: x)==types.LambdaType
True
>>> type((x for x in range(10)))==types.GeneratorType
True
```

### **isinstance**

```
isinstance(object, classinfo)
```

主要用于判断自建对象的类型，当然也可以判断基本数据类型。

如果 _object_ 参数是 _classinfo_ 参数的实例，或其（直接、间接或 [virtual](https://docs.python.org/zh-cn/3/glossary.html#term-abstract-base-class) ）子类的实例，则返回 `True`。 如果 _object_ 不是给定类型的对象，则总是返回 `False`。如果 _classinfo_ 是类型对象的元组（或由该类元组递归生成）或多个类型的 [union 类型](https://docs.python.org/zh-cn/3/library/stdtypes.html#types-union)，那么当 _object_ 是其中任一类型的实例时就会返回 `True`。如果 _classinfo_ 不是某个类型或类型元组，将会触发 [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError) 异常。

### **dir： directory**

如果要获得一个对象的所有属性和方法，可以使用`dir()`函数，它返回一个包含字符串的 list，比如，获得一个 str 对象的所有属性和方法：

```python
>>> dir('ABC')
['__add__', '__class__',..., '__subclasshook__', 'capitalize', 'casefold',..., 'zfill']
```

类似`__xxx__`的属性和方法在 Python 中都是有特殊用途的，比如`__len__`方法返回长度。在 Python 中，如果你调用`len()`函数试图获取一个对象的长度，实际上，在`len()`函数内部，它自动去调用该对象的`__len__()`方法。

**反射（reflection）**是指通过字符串映射或修改程序运行时的状态、属性、方法，配合`getattr()`、`setattr()`、`hasattr()`以及`delattr()`，我们可以直接操作一个对象的状态，紧接着，可以测试该对象的属性。

#### **getattr**

```
getattr(object, name[, default])
```

返回对象命名属性的值。_name_ 必须是字符串。如果该字符串是对象的属性之一，则返回该属性的值。例如， `getattr(x, 'foobar')` 等同于 `x.foobar`。如果指定的属性不存在，且提供了 _default_ 值，则返回它，否则触发 [`AttributeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError)。

#### **setattr**

```
setattr(object, name, value)
```

本函数与 [`getattr()`](https://docs.python.org/zh-cn/3/library/functions.html?highlight=getattr#getattr) 相对应。其参数为一个对象、一个字符串和一个任意值。字符串可以为某现有属性的名称，或为新属性。只要对象允许，函数会将值赋给属性。如 `setattr(x, 'foobar', 123)` 等价于 `x.foobar = 123`。

#### **hasattr**

```
hasattr(object, name)
```

该实参是一个对象和一个字符串。如果字符串是对象的属性之一的名称，则返回 `True`，否则返回 `False`。

_（此功能本质上是通过调用 `getattr(object, name)` 看是否有_ [_`AttributeError`_](https://docs.python.org/zh-cn/3/library/exceptions.html#AttributeError) _异常来实现的。）_

#### delattr

```
delattr(object, name)
```

实参是一个对象和一个字符串。该字符串必须是对象的某个属性。如果对象允许，该函数将删除指定的属性。例如 `delattr(x, 'foobar')` 等价于 `del x.foobar` 。

## 实例属性和类属性

可以直接在 class 中定义属性，这种属性是类属性，归`Student`类所有：

```
class Student(object):
    count = 0    
    def __init__(self, name):   
         self.name = name        
         Student.count += 1 # 类属性前面的类名不可省略
```

当我们定义了一个类属性后，这个属性虽然归类所有，但类的所有实例都可以访问到。

在编写程序的时候，千万不要对实例属性和类属性使用相同的名字，因为相同名称的实例属性将屏蔽掉类属性，但是当你删除实例属性后，再使用相同的名称，访问到的将是类属性。

## 类方法和静态方法

### **类方法**

```python
@classmethod
def 类方法名(cls):
    pass
```

* 类方法需要用 **修饰器** `@classmethod` 来标识，告诉解释器这是一个类方法
* 类方法的 **第一个参数** 应该是 `cls`
  * 由 **哪一个类** 调用的方法，方法内的 `cls` 就是 **哪一个类的引用**
  * 这个参数和 **实例方法** 的第一个参数是 `self` 类似
  * **提示** 使用其他名称也可以，不过习惯使用 `cls`

1. 通过 **类名.** 调用 类方法，调用方法时**不需要**传递 `cls` 参数
2. **在类方法内部**
   * 可以通过 `cls.` **访问类的属性**
   * 也可以通过 `cls.` **调用其他的类方法**

### **静态方法：定义在类空间中的函数**

* 在开发时，如果需要在 **类** 中封装一个方法，这个方法：
  * 既 **不需要** 访问 **实例属性** 或者调用 **实例方法**
  * 也 **不需要** 访问 **类属性** 或者调用 **类方法**
* 这个时候，可以把这个方法封装成一个 **静态方法**

```python
@staticmethod
def 静态方法名():    
    pass
```

* **静态方法** 需要用 **修饰器** `@staticmethod` 来标识，**告诉解释器这是一个静态方法**
* 通过 **类名.** 调用 **静态方法**

## 限制实例属性：`__slots__`

为了达到限制的目的，Python 允许在定义 class 的时候，定义一个特殊的`__slots__`变量，来限制该 class 实例能添加的属性：

```
class Student(object):
    __slots__ = ('name', 'age') 
```

使用`__slots__`要注意，`__slots__`定义的属性仅对**当前类**实例起作用，对继承的子类是不起作用的。

除非在子类中也定义`__slots__`，这样，子类实例允许定义的属性就是自身的`__slots__`加上父类的`__slots__`。

## 封装扩展：@property

对于类的方法，装饰器一样起作用。Python内置的`@property`装饰器就是负责把一个方法变成属性调用的：

```python
class Student(object):
    @property    
    def score(self):  
          return self._score
    
    @score.setter
    def score(self, value):  
          if not isinstance(value, int):     
                 raise ValueError('score must be an integer!')    
          if value < 0 or value > 100:     
                 raise ValueError('score must between 0 ~ 100!')
       self._score = value
```

把一个getter方法变成属性，只需要加上`@property`就可以了，此时，`@property`本身又创建了另一个装饰器`@score.setter`，负责把一个setter方法变成属性赋值，于是，我们就拥有了一个可控的属性操作。这样就可以直接通过属性名来访问属性了：

```python
>>> s = Student()
>>> s.set_score(60) # ok!
>>> s.get_score()
60
>>> s.set_score(9999)
Traceback (most recent call last):
  ...
ValueError: score must between 0 ~ 100!
```

还可以定义只读属性，只定义getter方法，不定义setter方法就是一个只读属性。

{% hint style="warning" %}
属性的方法名不要和实例变量重名。例如，以下的代码是错误的：
{% endhint %}

```python
class Student(object):
    # 方法名称和实例变量均为birth:    
    @property
        def birth(self):        
        return self.birth
```

这是因为调用`s.birth`时，首先转换为方法调用，在执行`return self.birth`时，又视为访问`self`的属性，于是又转换为方法调用，造成**无限递归**，最终导致栈溢出报错`RecursionError`。

## 多继承

首先，主要的类层次仍按照哺乳类和鸟类设计：

```python
class Animal(object):
    pass
class Mammal(Animal):
    pass
class Bird(Animal):
    pass
class Dog(Mammal):
    pass
class Bat(Mammal):
    pass
class Parrot(Bird):
    pass
class Ostrich(Bird):
    pass
```

现在，我们要给动物再加上`Runnable`和`Flyable`的功能，只需要先定义好`Runnable`和`Flyable`的类：

```python
class Runnable(object):
    def run(self):
        print('Running...')
        
class Flyable(object):
    def fly(self):
        print('Flying...')
```

对于需要`Runnable`功能的动物，就多继承一个`Runnable`，例如`Dog`：

```python
class Dog(Mammal, Runnable):
    pass
```

对于需要`Flyable`功能的动物，就多继承一个`Flyable`，例如`Bat`：

```python
class Bat(Mammal, Flyable):
    pass
```

通过多重继承，一个子类就可以同时获得多个父类的所有功能。

**Mixin：混入**

在设计类的继承关系时，通常，主线都是单一继承下来的，例如，`Ostrich`继承自`Bird`。但是，如果需要 “混入” 额外的功能，通过多重继承就可以实现，比如，让`Ostrich`除了继承自`Bird`外，再同时继承`Runnable`。这种设计通常称之为 MixIn。

为了更好地看出继承关系，我们把`Runnable`和`Flyable`改为`RunnableMixIn`和`FlyableMixIn`。类似的，你还可以定义出肉食动物`CarnivorousMixIn`和植食动物`HerbivoresMixIn`，让某个动物同时拥有好几个 MixIn：

```python
class Dog(Mammal, RunnableMixIn, CarnivorousMixIn):
    pass
```

MixIn 的目的就是给一个类增加多个功能，这样，在设计类的时候，我们优先考虑通过多重继承来组合多个 MixIn 的功能，而不是设计多层次的复杂的继承关系。

Python 自带的很多库也使用了 MixIn。举个例子，Python 自带了`TCPServer`和`UDPServer`这两类网络服务，而要同时服务多个用户就必须使用多进程或多线程模型，这两种模型由`ForkingMixIn`和`ThreadingMixIn`提供。通过组合，我们就可以创造出合适的服务来。

只允许单继承的语言（如 Java）不能使用 MixIn 的设计。

## 魔术方法：定制类

### **`__str__`**

对象被print()函数调用时，输出对象适宜阅读（非正式）的信息。

```python
>>> class Student(object):
...     def __init__(self, name):
...         self.name = name
...     def __str__(self):
...         return 'Student object (name: %s)' % self.name

>>> print(Student('Michael'))
Student object (name: Michael)
```

### **`__repr__`**

`__str__()`返回用户看到的字符串，而`__repr__()`返回程序开发者看到的字符串，也就是说，`__repr__()`是为调试服务的。

如果一个类定义了 [`__repr__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html?highlight=\_\_str\_\_#object.\_\_repr\_\_) 但未定义 [`__str__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html?highlight=\_\_str\_\_#object.\_\_str\_\_)，则在需要该类的实例的“非正式”字符串表示时也会使用 [`__repr__()`](https://docs.python.org/zh-cn/3/reference/datamodel.html?highlight=\_\_str\_\_#object.\_\_repr\_\_)。

```python
class Student(object):
    def __init__(self, name):        
        self.name = name    
    def __repr__(self):
        return 'Student object (name=%s)' % self.name    
```

### **`__iter__`**

如果一个类想被用于`for ... in`循环，类似list或tuple那样，就必须实现一个`__iter__()`方法，该方法返回一个迭代对象，然后，Python的for循环就会不断调用该迭代对象的`__next__()`方法拿到循环的下一个值，直到遇到`StopIteration`错误时退出循环。

```python
class Fib(object):
    def __init__(self):
        self.a, self.b = 0, 1 # 初始化两个计数器a，b    
    def __iter__(self):
        return self # 实例本身就是迭代对象，故返回自己    
    def __next__(self):
        self.a, self.b = self.b, self.a + self.b # 计算下一个值        
        if self.a > 100000: # 退出循环的条件
            raise StopIteration()
        return self.a # 返回下一个值    
        
if __name__ == '__main__':
    f = Fib()    
    for a in f:
        print(a)
```

### **`__call__`**

该方法的功能类似于在类中重载 **()** 运算符，使得类实例对象可以像调用普通函数那样，以“对象名()”的形式使用。

Python 中，凡是可以将 () 直接应用到自身并执行，都称为**可调用对象**。可调用对象包括自定义的函数、Python 内置函数以及类实例对象。

任何类，只需要定义一个`__call__()`方法，就可以直接对实例进行调用。请看示例：

```python
class Student(object):
    def __init__(self, name):
        self.name = name    
    def __call__(self):
        print('My name is %s.' % self.name)
```

调用方式如下：

```python
>>> s = Student('Michael')
>>> s() 
My name is Michael.
```

`__call__()`还可以定义参数。对实例进行直接调用就好比对一个函数进行调用一样，所以你完全可以把对象看成函数，把函数看成对象，因为这两者之间本来就没啥根本的区别。

如果你把对象看成函数，那么函数本身其实也可以在运行期动态创建出来，因为类的实例都是运行期创建出来的，这么一来，我们就模糊了对象和函数的界限。

那么，怎么判断一个变量是对象还是函数呢？其实，更多的时候，我们需要判断一个对象是否能被调用，能被调用的对象就是一个`Callable`对象。

```python
>>> callable(Student())
True
>>> callable(max)
True
>>> callable([1, 2, 3])
False
>>> callable(None)
False
>>> callable('str')
False
```

通过`callable()`函数，我们就可以判断一个对象是否是 “可调用” 对象。

### **`__getitem__`**

要表现得像 list 那样按照下标取出元素（随机访问），需要实现`__getitem__()`方法。

```python
class Fib(object):
    def __getitem__(self, n):
        a, b = 1, 1
        for x in range(n):
            a, b = b, a + b
        return a
```

事实上，要正确实现一个`__getitem__()`还是有很多工作要做的，比如切片等。

此外，如果把对象看成`dict`，`__getitem__()`的参数也可能是一个可以作 key 的 object，例如`str`。

与之对应的是`__setitem__()`方法，把对象视作 list 或 dict 来对集合赋值。最后，还有一个`__delitem__()`方法，用于删除某个元素。

总之，通过上面的方法，我们自己定义的类表现得和 Python 自带的 list、tuple、dict 没什么区别，这完全归功于动态语言的 “鸭子类型”，不需要强制继承某个接口。

### **`__getattr__`**

Python 还有另一个机制，那就是写一个`__getattr__()`方法，动态返回一个属性。修改如下：

```python
class Student(object):
    def __init__(self):
        self.name = 'Michael'
    def __getattr__(self, attr):
        if attr == 'score':
            return 99
```

当调用不存在的属性时，比如`score`，Python 解释器会试图调用`__getattr__(self, 'score')`来尝试获得属性，这样，我们就有机会返回`score`的值。

返回函数也是完全可以的：

```python
class Student(object):
    def __getattr__(self, attr):
        if attr=='age':
            return lambda: 25
```

注意，只有在没有找到属性的情况下，才调用`__getattr__`，已有的属性，比如`name`，不会在`__getattr__`中查找。

此外，注意到任意调用如`s.abc`都会返回`None`，这是因为我们定义的`__getattr__`默认返回就是`None`。要让 class 只响应特定的几个属性，我们就要按照约定，抛出`AttributeError`的错误：

```python
class Student(object):
    def __getattr__(self, attr):
        if attr=='age':
            return lambda: 25
        raise AttributeError('\'Student\' object has no attribute \'%s\'' % attr)
```

这种完全动态调用的特性有什么实际作用呢？作用就是，可以针对完全动态的情况作调用。

**实例：RESTful API链式调用生成API**

利用完全动态的`__getattr__`，我们可以写出一个链式调用：

```python
class Chain(object):
    def __init__(self, path=''):
        self.__path = path​
    def __getattr__(self, path):
        return Chain('%s/%s' % (self.__path, path)) # 非常巧妙地实现了链式调用​
    def __call__(self, path):
        return Chain('%s/%s' % (self.__path, path)) # 加入__call__是为了方便带参数的构造​
    def __repr__(self):       
        return self.__path​   

​print(Chain().api('login'))
>>>/api/login
```

## 枚举：Enum

枚举是由 [`class`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#class) 句法创建的，这种方式易读、易写。

```python
>>> from enum import Enum
>>> class Color(Enum):
...     RED = 1
...     GREEN = 2
...     BLUE = 3
```

枚举成员具有 _名称_ 和 _值_ (例如 `Color.RED` 的名称为 `RED`，`Color.BLUE` 的值为 `3` 等等)

枚举按定义的顺序进行迭代。枚举成员可哈希，可用于字典和集合：

```python
>>> apples = {}
>>> apples[Color.RED] = 'red delicious'
>>> apples[Color.GREEN] = 'granny smith'
>>> apples == {Color.RED: 'red delicious', Color.GREEN: 'granny smith'}
True
```

{% hint style="info" %}
虽然 Enum 由 [`class`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#class) 语法创建，但 Enum 并不是常规的 Python 类。
{% endhint %}

两个枚举成员的名称不能相同。但是，两个枚举成员可以有相同的值。假设，成员 A 和 B 的值相同（先定义的是 A），则 B 是 A 的别名。

按值查找 A 和 B 的值返回的是 A。按名称查找 B，返回的也是 A：

```python
>>> class Shape(Enum):
...     SQUARE = 2
...     DIAMOND = 1
...     CIRCLE = 3
...     ALIAS_FOR_SQUARE = 2
...
>>> Shape.SQUARE
<Shape.SQUARE: 2>
>>> Shape.ALIAS_FOR_SQUARE
<Shape.SQUARE: 2> # 按别名查找，实际被转化为按原名查找
>>> Shape(2)
<Shape.SQUARE: 2> # 按值查找，返回先定义的SQUARE
```

#### 唯一枚举值：@unique装饰器

`@unique`装饰器可以帮助我们检查保证没有重复值。

```python
>>> from enum import Enum, unique
>>> @unique
... class Mistake(Enum):
...     ONE = 1
...     TWO = 2
...     THREE = 3
...     FOUR = 3
...
Traceback (most recent call last):
...
ValueError: duplicate values found in <enum 'Mistake'>: FOUR -> THREE
```

#### `__members__`

特殊属性 `__members__` 是一个从名称到成员的只读有序映射（字典）。 它包含枚举中定义的所有名称，包括别名:

```python
>>> for name, member in Shape.__members__.items():
...     name, member
...
('SQUARE', <Shape.SQUARE: 2>)
('DIAMOND', <Shape.DIAMOND: 1>)
('CIRCLE', <Shape.CIRCLE: 3>)
('ALIAS_FOR_SQUARE', <Shape.SQUARE: 2>)
```

#### 比较运算

枚举值之间的排序比较 _不被_ 支持。 Enum 成员不属于整数。

`is`和`==`等同，相应地，`is not`和`!=`等同。

**枚举变量与非枚举变量值的比较将总是不相等：**

```python
Color.BLUE == 3     # 错误用法
False
Color.BLUE.value == 3
True
```

## 元类：Metaclass
