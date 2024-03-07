# 🥳 文件与IO

## _print_

### **语法**

`print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)`

### **参数**

* `objects` – 表示可以一次输出多个对象。输出多个对象时，需要用 , 分隔。
* `sep` – 用来间隔多个对象，默认值是一个空格。
* `end` – 用来设定以什么结尾。默认值是换行符 \n，我们可以换成其他字符串。
* `file`– 要写入的文件对象。
* `flush` – 输出是否被缓存通常决定于 file，但如果 flush 关键字参数为 True，流会被强制刷新。

## _input_

```
input([prompt])
```

Python3.x 中 input() 函数将所有输入默认为_**字符串**_处理，返回为 string 类型。

需要输入多个参数时，一般搭配split()函数使用。

参数说明：

* prompt: 提示信息

## _StringIO_模块

字符流。很多时候，数据读写不一定是文件，也可以在内存中读写。

StringIO 顾名思义就是在内存中读写 str。

要把 str 写入 StringIO，我们需要先创建一个 StringIO，然后，像文件一样写入即可：

```python
>>> from io import StringIO
>>> f = StringIO()
>>> f.write('hello')
5
>>> print(f.getvalue())
'hello'
```

要读取 StringIO，可以用一个 str 初始化 StringIO，然后像读文件一样读取。

## _BytesIO_模块

StringIO 操作的只能是 str，如果要操作二进制数据，就需要使用 BytesIO。

BytesIO 实现了在内存中读写 bytes。

```python
>>> from io import BytesIO
>>> f = BytesIO()
>>> f.write('中文'.encode('utf-8'))
6
>>> print(f.getvalue())
b'\xe4\xb8\xad\xe6\x96\x87'
```

## 打开文件——_**open**_

### **语法**

{% code overflow="wrap" %}
```python
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
```
{% endcode %}

### **参数值**

<table data-header-hidden><thead><tr><th width="150"></th><th width="508.2857142857143"></th></tr></thead><tbody><tr><td>参数</td><td>描述</td></tr><tr><td><em>file</em></td><td>文件的路径或名称。</td></tr><tr><td><em>mode</em></td><td><p>字符串，定义您要在哪种模式下打开文件：</p><p> "r" - 读取 - 默认值。打开文件进行读取，如果文件不存在，则发生错误。 </p><p>"a" - 追加 - 打开文件进行追加，如果不存在则创建文件。</p><p>"w" - 写入 - 打开文件进行写入，如果不存在则创建文件。 </p><p>"x" - 创建 - 创建指定的文件，如果文件存在则返回错误。 </p><p><strong>另外</strong>，您可以指定文件应以二进制还是文本模式处理：</p><p> "t" - 文本 - 默认值。文字模式。 </p><p>"b" - 二进制 - 二进制模式（例如图像）。</p></td></tr><tr><td>errors</td><td>"ignore"表示忽略编码错误</td></tr></tbody></table>

如果文件不存在，`open()`函数就会抛出一个`IOError`的错误。

### **返回值**

返回文件对象。

## 写文件——_**write**_

**write()** 方法用于向文件中写入指定字符串。

在文件关闭前或缓冲区刷新前，字符串内容存储在缓冲区中，这时你在文件中是看不到写入的内容的。

如果文件打开模式带 b，则写入文件内容时，str (参数)要用 encode 方法转为 bytes 形式，否则报错：

TypeError: a bytes-like object is required, not 'str'。

同样适用with语句。

### **语法**

write() 方法语法如下：

```
fileObject.write( str )
```

### **参数**

* **str** -- 要写入文件的字符串。

### **返回值**

返回的是写入的字符长度。

## 读取文件

### **read**

#### **概述**

**read()** 方法用于从文件读取指定的字符数（文本模式 **t**）或字节数（二进制模式 **b**），如果未给定参数 **size** 或 **size** 为负数则读取文件所有内容。

#### **语法**

read() 方法语法如下：

```
fileObject.read([size]); 
```

#### **参数**

* **size** -- 从文件中读取的字符数（文本模式）或字节数（二进制模式），默认为 **-1**，表示读取整个文件。

#### **返回值**

返回从字符串中读取的字节数或字符数。（str或bytes）

### **readline**

**readline()** 方法用于从文件读取整行，包括 "\n" 字符。如果指定了一个非负数的参数，则返回指定大小的字节数，包括 "\n" 字符。

#### **语法**

readline() 方法语法如下：

```
fileObject.readline(size); 
```

#### **参数**

* **size** -- 从文件中读取的字节数。

#### **返回值**

返回从字符串中读取的字节。

### **readlines**

**readlines()** 方法用于读取所有行(直到结束符 EOF)并返回列表，该列表可以由 Python 的 for... in ... 结构进行处理。 如果碰到结束符 EOF 则返回空字符串。

请注意使用 `for line in file: ...` 就足够对文件对象进行迭代了，可以不必调用 `file.readlines()`。

## 关闭文件——_**close**_

### **概述**

**close()** 方法用于关闭一个已打开的文件。关闭后的文件不能再进行读写操作， 否则会触发 _ValueError_ 错误。 close() 方法允许调用多次。

当 file 对象，被引用到操作另外一个文件时，Python 会自动关闭之前的 file 对象。 使用 close() 方法关闭文件是一个好的习惯。

### **语法**

close() 方法语法如下：

```
fileObject.close();
```

## 补：_with_关键字

Python 中的 **with** 语句用于异常处理，封装了 **try…except…finally** 编码范式，提高了易用性。

**with** 语句使代码更清晰、更具可读性， 它简化了文件流等公共资源的管理。

由于文件读写时都有可能产生`IOError`，一旦出错，后面的`f.close()`就不会调用，因此在处理文件对象时使用 with 关键字是一种很好的做法。

```
with open('/path/to/file', 'r') as f:
    print(f.read())
```

## file-like Object

像`open()`函数返回的这种有个`read()`方法的对象，在 Python 中统称为 file-like Object（类文件对象，可读对象）。除了 file 外，还可以是内存的字节流，网络流，自定义流等等。file-like Object 不要求从特定类继承，只要写个`read()`方法就行。

`StringIO`就是在内存中创建的 file-like Object，常用作临时缓冲。

## 操作文件和目录——_os_模块

操作文件和目录的函数一部分放在`os`模块中，一部分放在`os.path`模块中。

这些合并、拆分路径的函数并不要求目录和文件要真实存在，它们只对字符串进行操作。

### **环境变量**

在操作系统中定义的环境变量，全部保存在`os.environ : dict`这个变量中，可以直接查看。

### os.getcwd

返回表示当前工作目录(Current Working Directory)的字符串。

### **os.listdir——ls**

os.listdir() 方法用于返回指定的文件夹包含的文件或文件夹的名字的列表。这个列表以字母顺序。 它不包括 **.** 和 **..** 即使它在文件夹中。

只支持在 Unix, Windows 下使用。

#### **语法**

**listdir()**方法语法格式如下：

```
os.listdir(path='.')
```

#### **参数**

* **path** -- 需要列出的目录路径，默认为当前目录

#### **返回值**

返回指定路径下的文件和文件夹**列表**。

### **os.rename**

os.rename() 方法用于命名文件或目录，从 src 到 dst,如果dst是一个存在的目录, 将抛出OSError。

**语法**

**rename()**方法语法格式如下：

```
os.rename(src, dst)
```

**参数**

* **src** -- 要修改的目录名
* **dst** -- 修改后的目录名

### **os.remove**

os.remove() 方法用于删除指定路径的文件。如果指定的路径是一个目录，将抛出OSError。

**语法**

**remove()**方法语法格式如下：

```
os.remove(path)
```

**参数**

* **path** -- 要移除的文件路径

### **os.mkdir**

os.mkdir() 方法用于以数字权限模式创建目录。默认的模式为 0777 (八进制)。

如果目录有多级，则创建最后一级，如果最后一级目录的上级目录有不存在的，则会抛出一个 OSError。

**语法**

**mkdir()**方法语法格式如下：

```
os.mkdir(path[, mode])
```

**参数**

* **path** -- 要创建的目录，可以是相对或者绝对路径。
* **mode** -- 要为目录设置的权限数字模式

### **os.rmdir**

os.rmdir() 方法用于删除指定路径的目录。仅当这文件夹是_**空的**_才可以, 否则, 抛出OSError。

**语法**

**rmdir()**方法语法格式如下：

```
os.rmdir(path)
```

**参数**

* **path** -- 要删除的目录路径

### **os.path.abspath**

`os.path.abspath(path)`

返回路径 _path_ 的绝对路径。

### **os.path.join**

`os.path.join(path, *paths)`

智能地拼接一个或多个路径部分。 返回值是 _path_ 和 _\*paths_ 的所有成员的拼接，其中每个非空部分后面都紧跟一个目录分隔符，最后一个部分除外，这意味着如果最后一个部分为空，则结果将以分隔符结尾。 如果某个部分为绝对路径，则之前的所有部分会被丢弃并从绝对路径部分开始继续拼接。

### **os.path.split**

`os.path.split(path)`

同样的道理，要拆分路径时，也不要直接去拆字符串，而要通过`os.path.split()`函数。

该函数将路径 _path_ 拆分为一对，即 `(head, tail)`，其中，_tail_ 是路径的最后一部分，而 _head_ 里是除最后部分外的所有内容。_tail_ 部分不会包含斜杠，如果 _path_ 以斜杠结尾，则 _tail_ 将为空。

如果 _path_ 中没有斜杠，_head_ 将为空。

如果 _path_ 为空，则 _head_ 和 _tail_ 均为空。

_head_ 末尾的斜杠会被去掉，除非它是根目录（即它仅包含一个或多个斜杠）。

在所有情况下，`join(head, tail)` 指向的位置都与 _path_ 相同（但字符串可能不同）。

### **os.path.splitext**

`os.path.splitext(path)`

主要用法是分割扩展名。

将路径名称 _path_ 拆分为 `(root, ext)` 对使得 `root + ext == path`，并且扩展名 _ext_ 为空或以句点打头并最多只包含一个句点。如果路径 path 不包含扩展名，则 _ext_ 将为 `''`:

```
>>> splitext('bar')('bar', '')
```

如果路径 path 包含扩展名，则 _ext_ 将被设为该扩展名，包括打头的句点。 请注意在其之前的句点将被忽略。

### **os.path.isdir**

```
os.path.isdir(path)
```

如果 _path_ 是 [`现有的`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.exists) 目录，则返回 `True`。本方法会跟踪符号链接，因此，对于同一路径，[`islink()`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.islink) 和 [`isdir()`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.isdir) 都可能为 `True`。

### **os.path.isfile**

```
os.path.isfile(path)
```

如果 _path_ 是 [`现有的`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.exists) 常规文件，则返回 `True`。本方法会跟踪符号链接，因此，对于同一路径，[`islink()`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.islink) 和 [`isfile()`](https://docs.python.org/zh-cn/3/library/os.path.html?highlight=abspath#os.path.isfile) 都可能为 `True`。

## _shutil_（**shell utility**）模块

作为os模块的有力补充，shutil 模块提供了一系列对文件和文件集合的高阶操作，特别是提供了一些支持文件拷贝和删除的函数。

### **shutil.copyfile**

`shutil.copyfile(src, dst, *, follow_symlinks=True)`

将名为 _src_ 的文件的内容（不包括元数据）拷贝到名为 _dst_ 的文件并以尽可能高效的方式返回 _dst_。 _src_ 和 _dst_ 均为路径类对象或以字符串形式给出的路径名。

### **shutil.copytree**

```
shutil.copytree(src, dst, symlinks=False, ignore=None, copy_function=copy2, ignore_dangling_symlinks=False, dirs_exist_ok=False)
```

将以 _src_ 为根起点的整个目录树拷贝到名为 _dst_ 的目录并返回目标目录。 _dirs\_exist\_ok_ 指明是否要在 _dst_ 或任何丢失的父目录已存在的情况下引发异常。

目录的权限和时间会通过 [`copystat()`](https://docs.python.org/zh-cn/3/library/shutil.html?highlight=shutil#shutil.copystat) 来拷贝，单个文件则会使用 [`copy2()`](https://docs.python.org/zh-cn/3/library/shutil.html?highlight=shutil#shutil.copy2) 来拷贝。

### **shutil.rmtree**

```
shutil.rmtree(path, ignore_errors=False, onerror=None)
```

删除一个完整的目录树；_path_ 必须指向一个目录（但不能是一个目录的符号链接）。 如果 _ignore\_errors_ 为真值，删除失败导致的错误将被忽略；如果为假值或是省略，此类错误将通过调用由 _onerror_ 所指定的处理程序来处理，或者如果此参数被省略则将引发一个异常。

### **shutil.move**

```
shutil.move(src, dst, copy_function=copy2)
```

递归地将一个文件或目录 (_src_) 移至另一位置 (_dst_) 并返回目标位置。

如果目标是已存在的目录，则 _src_ 会被移至该目录下。
