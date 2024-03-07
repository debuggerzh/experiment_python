# 😎 异常处理

`SyntaxError`：语法错误

执行时检测到的错误称为 _异常_，异常并不一定导致严重的后果。

如果错误没有被捕获，它就会一直往上抛，最后被Python解释器捕获，打印一个错误信息，然后程序退出。

```python
while True:
     try:
          x = int(input("Please enter a number: "))
          break     
     except ValueError:         
          print("Oops!  That was no valid number.  Try again...")
```

## 异常处理语句

[`try`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#try) 语句的工作原理如下：

* 首先，执行 _try 子句_ （[`try`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#try) 和 [`except`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#except) 关键字之间的（多行）语句）。
* 如果没有触发异常，则跳过 _except 子句_，[`try`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#try) 语句执行完毕。
* 如果在执行 [`try`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#try) 子句时发生了异常，则跳过该子句中剩下的部分。 如果异常的类型与 [`except`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#except) 关键字后指定的异常相匹配，则会执行 _except 子句_，然后跳到 try/except 代码块之后继续执行。
* 如果发生的异常与 _except 子句_ 中指定的异常不匹配，则它会被传递到外部的 [`try`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#try) 语句中；如果没有找到处理程序，则它是一个 _未处理异常_ 且执行将终止并输出错误消息。

可以有多个 _except 子句_ 来为不同的异常指定处理程序， 但至多一个处理程序会被执行。 处理程序只处理对应的 _try 子句_ 中发生的异常，而不处理同一 `try` 语句内其他处理程序中的异常。 _except 子句_ 可以用带圆括号的元组来指定多个异常，例如:

```
except (RuntimeError, TypeError, NameError):
    pass
```

except子句中的类和异常类相同或者是其父类时，它们相兼容。

```python
class B(Exception):    pass​
class C(B):    pass​
class D(C):    pass​

for cls in [B, C, D]:
    try:        
        raise cls()    
    except D:        print("D")    
    except C:        print("C")    
    except B:        print("B") 
# B C D
```

{% hint style="info" %}
如果颠倒 _except 子句_ 的顺序（把 `except B` 放在最前），则会输出 `B, B, B` ，即三次均触发了第一个匹配的 _except 子句_。
{% endhint %}

可以选择让最后一个 except 子句省略异常名称，但在此之后异常值必须从 `sys.exc_info()[1]` 获取。

### else子句

[`try`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#try) ... [`except`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#except) 语句具有可选的 _else 子句_，该子句如果存在，它必须放在所有 _except 子句_ 之后。它适用于 _try 子句_ **没有引发异常但又必须要执行**的代码。

发生的异常可能具有关联值，即异常 _参数_ 。是否需要参数，以及参数的类型取决于异常的类型。

_except 子句_ 可以在异常名称后面指定一个变量。 这个变量会绑定到一个异常实例并将参数存储在 `instance.args` 中。 为了方便起见，该异常实例定义了 `__str__()` 以便能直接打印参数而无需引用 `.args`。 也可以在引发异常之前先实例化一个异常并根据需要向其添加任何属性。

```python
>>> try:
...     raise Exception('spam', 'eggs')
... except Exception as inst:
...     print(type(inst))    # the exception instance
...     print(inst.args)     # arguments stored in .args
...     print(inst)          # __str__ allows args to be printed directly

<class 'Exception'>
('spam', 'eggs')
('spam', 'eggs')
```

异常处理程序不仅会处理在 _try 子句_ 中发生的异常，还会处理在 _try 子句_ 中调用（包括间接调用）的函数。

```python
>>> def this_fails():
...     x = 1/0
...
>>> try:
...     this_fails()
... except ZeroDivisionError as err:
...     print('Handling run-time error:', err)
...
Handling run-time error: division by zero
```

### 主动触发异常：raise语句

[`raise`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#raise) 语句支持强制触发指定的异常。例如：

```python
>>> raise NameError('HiThere')
Traceback (most recent call last):  
File "<stdin>", line 1, in <module>
NameError: HiThere
```

[`raise`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#raise) 唯一的参数就是要触发的异常。这个参数必须是异常实例或异常类（派生自 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) 类）。如果传递的是异常类，将通过调用没有参数的构造函数来隐式实例化。

如果只想判断是否触发了异常，但并不打算处理该异常，则可以使用更简单的 [`raise`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#raise) 语句重新触发异常。

```python
try:        
        raise NameError('HiThere')    
except NameError:        
        print('An exception flew by!')        
        raise   

An exception flew by!
Traceback (most recent call last):  File "<stdin>", line 2, in <module>
NameError: HiThere
```

### 异常链

[`raise`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#raise) 语句支持可选的 [`from`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#raise) 子句，该子句用于启用链式异常。

进行异常转换时，这种方式很有用。

```python
>>> def func():
...     raise ConnectionError

>>> try:
...     func()
... except ConnectionError as exc:
...     raise RuntimeError('Failed to open database') from exc

Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
  File "<stdin>", line 2, in func
ConnectionError

​The above exception was the direct cause of the following exception:

​Traceback (most recent call last):
  File "<stdin>", line 4, in <module>
RuntimeError: Failed to open database
```

异常链会在 [`except`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#except) 或 [`finally`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#finally) 子句内部引发异常时自动生成。 这可以通过使用 `from None` 这样的写法来禁用。

所有异常都继承自 [`BaseException`](https://docs.python.org/zh-cn/3/library/exceptions.html#BaseException)，因此它可被用作通配符。 但这种用法要非常谨慎小心，因为它很容易掩盖真正的编程错误！因此不论是以直接还是间接的方式，异常都应从 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception) 类派生。

```python
class InputError(Exception):    
    '''当输出有误时，抛出此异常'''    #自定义异常类型的初始化    
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

### 最后的清理操作：finally

[`try`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#try) 语句还有一个可选子句，用于定义在所有情况下都必须要执行的清理操作。例如：

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

如果存在 [`finally`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#finally) 子句，则 `finally` 子句是 [`try`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#try) 语句结束前执行的最后一项任务。不论 `try` 语句是否触发异常，都会执行 `finally` 子句。以下内容介绍了几种比较复杂的触发异常情景：

* 如果执行 `try` 子句期间触发了某个异常，则某个 [`except`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#except) 子句应处理该异常。如果该异常没有 `except` 子句处理，在 `finally` 子句执行后会被重新触发。
* `except` 或 `else` 子句执行期间也会触发异常。 同样，该异常会在 `finally` 子句执行之后被重新触发。
* 如果 `finally` 子句中包含 [`break`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#break)、[`continue`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#continue) 或 [`return`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#return) 等语句，异常将不会被重新引发。
* 如果执行 `try` 语句时遇到 [`break`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#break),、[`continue`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#continue) 或 [`return`](https://docs.python.org/zh-cn/3/reference/simple\_stmts.html#return) 语句，则 `finally` 子句在执行 `break`、`continue` 或 `return` 语句之前执行。
* 如果 `finally` 子句中包含 `return` 语句，则返回值来自 `finally` 子句的某个 `return` 语句的返回值，而不是来自 `try` 子句的 `return` 语句的返回值。

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
  File "<stdin>", line 3, in divideTypeError: unsupported operand type(s) for /: 'str' and 'str'
```

如上所示，任何情况下都会执行 [`finally`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#finally) 子句。[`except`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#except) 子句无法处理两个字符串相除触发的 [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError)，因此该异常会在 `finally` 子句执行后被重新触发。

在实际应用程序中，[`finally`](https://docs.python.org/zh-cn/3/reference/compound\_stmts.html#finally) 子句对于释放外部资源（例如文件或者网络连接）非常有用，无论是否成功使用资源。
