# References

{% embed url="https://docs.xlwings.org/zh_CN/latest/api.html#python-api" %}

## Apps

```python
class xlwings.main.Apps(impl)
```

所有app对象的集合。

#### 属性

```python
property count
```

返回app的总数，即xlwings创建的仍在内存的Excel进程的总数。

## App

```python
class xlwings.App(visible=None, spec=None, add_book=True, impl=None)
```

打开一个Excel进程，应当始终使用上下文管理器。

#### 属性

```python
property pid
```

返回app的PID。

```python
property display_alerts
```

缺省值为 True。通过设置为 False 可以关闭正在运行的代码的报警信息；如果报警信息是需要响应的，Excel 会选择默认的响应方式。

```python
property screen_updating
```

关掉屏幕刷新 (设置为 `False` ) 来加速脚本运行。虽然看不到脚本的运行情况，但是会让它运行更快。

```python
property books
```

当前打开的所有工作簿对象的集合。

#### 用法

```python
import xlwings as xw

with xw.App(visible=True, add_book=False) as app:
    print(app.books)
```

## Books

```python
class xlwings.main.Books(impl)
```

工作簿对象的集合。

#### 属性

```python
property active
```

返回活动工作簿。

```python
add()
```

创建一个新的工作簿。新工作簿变成活动工作簿。返回一个工作簿对象。

## Book

{% code overflow="wrap" %}
```python
class xlwings.Book(fullname=None, update_links=None, read_only=None, format=None, password=None, write_res_password=None, ignore_read_only_recommended=None, origin=None, delimiter=None, editable=None, notify=None, converter=None, add_to_mru=None, local=None, corrupt_load=None, impl=None)
```
{% endcode %}

一个 book 对象是 books 集合中的一个成员。

#### 方法

```python
activate(steal_focus=False)
```

把一个工作簿置于激活态，steal\_focus为True时会置顶Excel并且把焦点从 Python 切换到 Excel。

```python
save(path=None)
```

保存工作簿。如果提供了路径，就类似于 Excel 中的另存为。如果文件事先没有被保存过，又没有提供保存路径，会以当前的文件名保存在当前的工作目录中。同名文件会在没有提示的情况下被直接覆盖。

```renpy
close()
```

放弃保存，直接关闭工作簿。

#### 属性

```python
property sheets
```

返回工作簿中所有工作表的集合。

|                    |  xw.Book                           | xw.books                                 |
| ------------------ | ---------------------------------- | ---------------------------------------- |
| New book           | `xw.Book()`                        | `xw.books.add()`                         |
| Unsaved book       | `xw.Book('Book1')`                 | `xw.books['Book1']`                      |
| Book by (full)name | `xw.Book(r'C:/path/to/file.xlsx')` | `xw.books.open(r'C:/path/to/file.xlsx')` |

两种方式的区别：

方式1是**创建一个新的App**,并在新App中新建一个Book;

方式2是在当前App下新建一个Book

## Sheets

```python
class xlwings.main.Sheets(impl)
```

全部工作表对象 [`sheet`](https://docs.xlwings.org/zh\_CN/latest/api.html#xlwings.Sheet) 的集合。

由于Sheets的父类实现了`__getitem__`方法，因此可以将工作表名作为key，来取得对应的工作表：

<pre class="language-python"><code class="lang-python">>>> import xlwings as xw
>>> wb = xw.Book()
<strong>>>> wb.sheets['Sheet1']
</strong>&#x3C;Sheet [Book1]Sheet1>
</code></pre>

#### 方法

```python
add(name=None, before=None, after=None)
```

before参数和after参数用来决定新工作表的位置。

不指定位置时，默认在最前插入（同Excel逻辑）。

#### 属性

```python
property active
```

返回活动的工作表 (Sheet)。

## Sheet

```python
class xlwings.Sheet(sheet=None, impl=None)
```

一个 sheet 对象是 sheets 集合中的一员。

通过在工作表对象上使用索引和切片标注，提供了引用区域对象的一种快捷方式。例如：

```python
sheet = xw.Book().sheets['Sheet1']
sheet['A1']
<Range [Book1]Sheet1!$A$1>
sheet['A1:B5']
<Range [Book1]Sheet1!$A$1:$B$5>
sheet[0, 1]
<Range [Book1]Sheet1!$B$1>
sheet[:10, :10]
<Range [Book1]Sheet1!$A$1:$J$10>
```

#### 属性

```python
property cells
```

返回一个代表工作表上所有单元格的区域对象 (不仅仅是那些正在使用中的单元格)。

#### 方法

```python
range(cell1, cell2=None)
```

从活动工作簿的活动工作表中返回一个区域对象, 参见 [`Range()`](https://docs.xlwings.org/zh\_CN/latest/api.html#xlwings.Range) 。

<pre class="language-python" data-line-numbers><code class="lang-python"><strong># 选择整行
</strong><strong>sheet[0, :]
</strong>&#x3C;Range [工作簿1]Sheet1!$1:$1>
sheet.range('1:1')
&#x3C;Range [工作簿1]Sheet1!$1:$1>
# 选择整列
sheet[:,0]
&#x3C;Range [工作簿1]Sheet1!$A:$A>
sheet.range('a:a')
&#x3C;Range [工作簿1]Sheet1!$A:$A>
</code></pre>

```
clear()
```

重新格式化工作表，清除所有内容及格式。

```
clear_contents()
```

清除工作表的所有内容但是保留原有格式。

```
delete()
```

```
autofit(axis：string=None)
```

在整个工作表中对行、列或者两者同时根据内容进行自适应。

对参数axis：

* 要做行自适应，用 `rows` 或 `r`
* 要做列自适应，用 `columns` 或 `c`
* 同时做行和列的自适应，不需要参数。

```
select()
```

选中工作表。

## Range

{% code overflow="wrap" %}
```python
class xlwings.Range(cell1=None, cell2=None, **options)

# cell1 (str or tuple or Range) – 区域左上角的名字，可以是 A1 表示法、坐标元组、名字或者是 xw.Range 对象。
也可用区域操作符号 (例如 ‘A1:B2’ ) 来表示。

# cell2 (str or tuple or Range, default None) – 区域右下角角的名字，可以是 A1 表示法、坐标元组、名字或者是 xw.Range 对象。
```
{% endcode %}

返回一个区域对象，可以代表一个单元格，也可以是一个区域。（单元格也是特殊的区域）

```python
xw.Range('A1')
xw.Range('A1:C3')
xw.Range((1,1))
xw.Range((1,1), (3,3))
xw.Range('NamedRange')
xw.Range(xw.Range('A1'), xw.Range('B2'))
```

区域对象支持索引和切片。例如：

```python
rng = xw.Book().sheets[0].range('A1:D5')
rng[0, 0]
 <Range [Workbook1]Sheet1!$A$1>
rng[1]  # 等价于rng[0, 1]
 <Range [Workbook1]Sheet1!$B$1>
# 行省略时，默认为第一行
rng[:, 3:]
<Range [Workbook1]Sheet1!$D$1:$D$5>
rng[1:3, 1:3]
<Range [Workbook1]Sheet1!$B$2:$C$3>
```

### 方法

```python
offset(row_offset=0, column_offset=0)
```

返回一个由当前range经过平移得到的新range。

Excel正向：👉和👇。参数为负数代表负向平移。

```python
expand(mode='table')
```

根据要求的模式扩展选区，不管左上角是否为空。

类似于Excel中快捷键`Ctrl+Shift+↓/→`键的效果。

参数mode可以取 `'down'` , `'right'` ,`'table'` (=down + right)。

{% code lineNumbers="true" %}
```python
>>> import xlwings as xw
>>> wb = xw.Book()
>>> xw.Range('A1').value = [[None, 1], [2, 3]]
>>> xw.Range('A1').expand().address
$A$1:$B$2
>>> xw.Range('A1').expand('right').address
$A$1:$B$1
>>> xw.Range('A1').expand('down').address
'$A$1:$A$2'
```
{% endcode %}

```python
resize(row_size=None, column_size=None)
```

```
clear()
```

```
clear_contents()
```

```python
delete(shift=None)
```

删除一个单元格或者一个区域的单元格。shift可以取`left` or `up`；

如果省略shift，Excel 将根据区域的形状决定。

```python
options(convert=None, **options)
```

允许用户设定转换器和相关的选项。转换器定义了 Excel 的区域及其值在读写过程中如何转换。如果没有明确指定转换器，会使用基转换器 (base converter)。

**关键字参数：**

* **transpose** (_Boolean, default False_) – 是否转置

### 属性

```python
property api
```

返回正在使用的引擎的原生对象 ( `pywin32` 或 `appscript` 对象)。

使用api的方法调用，本质上是VBA函数调用。

#### 绘制边框

![](<../.gitbook/assets/image (9).png>)

![LineStyle，即边框线型的取值](<../.gitbook/assets/image (4).png>)

```python
# Borders(9) 底部边框，LineStyle = 1 直线。
b3.api.Borders(9).LineStyle = 1
b3.api.Borders(9).Weight = 3                # 设置边框粗细。
```

#### 合并/取消合并单元格

<pre class="language-python"><code class="lang-python"><strong>sht.range('C8:D8').api.merge()      # 合并区域 C8：D8
</strong>sht.range('C8:D8').api.unmerge()    # 拆分单元格。
</code></pre>

#### 单元格格式

```python
b3.api.HorizontalAlignment = -4108    
# -4108 水平居中。 -4131 靠左，-4152 靠右。
b3.api.VerticalAlignment = -4130      
# -4108 垂直居中（默认）。 -4160 靠上，-4107 靠下， -4130 自动换行对齐。

b3.api.NumberFormat = "0.00"          # 设置单元格的数字格式。
```

#### 使用颜色索引

![](<../.gitbook/assets/image (12).png>)

```python
a1 = sheet['a1']
a1.value = 123
a1.font.size = 24
a1.font.api.ColorIndex = 38
```

![](<../.gitbook/assets/image (6).png>)

```python
property value
```

取得/设定给定区域的值。

#### 按行填充

```python
sheet.range('A1').value = [1, 2, 3, 4, 5]
```

![](<../.gitbook/assets/image (5).png>)

#### 按列填充

```python
sht.range('A1').options(transpose=True).value = [1, 2, 3]
sht.range('A1').value = [[1], [2], [3]]
```

![](<../.gitbook/assets/image (10).png>)

#### 按表格填充

```python
sht.range('A1').value = [[1,2], [3,4]]
```

![](<../.gitbook/assets/image (14).png>)

```python
property current_region
```

此属性返回一个范围对象，该对象表示由（但不包括）**空白行**、**空白列**或工作表**边缘**的任何组合所限定的范围。它对应于 Windows 上的 `Ctrl + Shift + *`快捷键。

![](../.gitbook/assets/current\_region.png)

## Font

```python
class xlwings.main.Font(impl)
```

字体对象可以作为Range或Shape对象的属性访问。

```python
mysheet['A1'].font

mysheet.shapes[0].font
```

#### 属性

```python
property bold
property color
sheet['A1'].font.color = (255, 0, 0)  # or '#ff0000'

property italic
property name    # 以Fonts中安装的字体名称为准
property size    # 设置字号（float）
```
