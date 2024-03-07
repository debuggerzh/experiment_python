---
description: Lexical analysis
---

# 🤣 词法分析

## 注释

### 单行注释

Python中单行注释以 **#** 开头。

### 多行注释

多行注释用三个单引号 **'''** 或者三个双引号 **"""** 将注释括起来。

## 行内拼接

### 显式拼接

可用反斜杠（`\`）拼接行：

```python
if 1900 < year < 2100 and 1 <= month <= 12:
    return 1
# 等价于
if 1900 < year < 2100 \ 
    and 1 <= month <= 12:
    return 1
```

### 隐式拼接

圆括号、方括号、花括号内的表达式可以分成多个行，不必使用反斜杠。例如：

```python
month_names = ['Januari', 'Februari', 'Maart',      # These are the
               'April',   'Mei',      'Juni',       # Dutch names
               'Juli',    'Augustus', 'September',  # for the months
               'Oktober', 'November', 'December']   # of the year
```

### 字符串拼接

以空白符分隔的多个相邻字符串或字节串字面值，可用不同引号标注，等同于合并操作。因此，`"hello" 'world'` 等价于 `"helloworld"`。此功能不需要反斜杠，即可将长字符串分为多个物理行，还可以为不同部分的字符串添加注释，例如：

```python
re.compile("[A-Za-z_]"       # letter or underscore
           "[A-Za-z0-9_]*"   # letter, digit or underscore
          )
```
