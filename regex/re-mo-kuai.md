# re模块

Python 提供`re`模块，包含所有正则表达式的功能。由于 Python 的字符串本身也用`\`转义，所以强烈建议使用原义字符串，即在字符串前加字母**r**。

## 编译（compile）

当我们在 Python 中使用正则表达式时，re 模块内部会干两件事情：

1. 编译正则表达式，如果正则表达式的字符串本身不合法，会报错；
2. 用编译后的正则表达式去匹配字符串。

如果一个正则表达式要重复使用几千次，出于效率的考虑，我们可以_预编译_该正则表达式，接下来重复使用时就不需要编译这个步骤了，直接匹配。重要的应用程序大多会在使用前先编译正则表达式。

```python
re.compile(pattern, flags=0)
```

将正则表达式的样式编译为一个 [正则表达式对象](https://docs.python.org/zh-cn/3/library/re.html?highlight=match#re-objects) ，可以通过这个对象的方法 [`match()`](https://docs.python.org/zh-cn/3/library/re.html?highlight=match#re.Pattern.match), [`search()`](https://docs.python.org/zh-cn/3/library/re.html?highlight=match#re.Pattern.search)进行匹配。

这个表达式的行为可以通过指定 _标记_ 的值来改变。值可以是以下任意变量，可以通过位的OR操作来结合（ `|` 操作符）。

```python
prog = re.compile(pattern)
result = prog.match(string)
```

等价于

```python
result = re.match(pattern, string)
```

## re.search

```python
re.search(pattern, string, flags=0)
```

扫描**整个** _字符串_ 找到匹配样式的第一个位置，并返回一个相应的 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html?highlight=match#match-objects)。如果没有匹配，就返回一个 `None`。

## re.match

```python
re.match(pattern, string, flags=0)
```

如果 _string_ **开头**的零个或多个字符与正则表达式 _pattern_ 匹配，则返回相应的 [MatchObject](https://cainiaojiaocheng.com/Python/docs/2.7/library/re#re.MatchObject) 实例。 如果字符串与模式不匹配，则返回 `None`。

## search() vs. match()

Python 提供了两种不同的操作：

基于 [`re.match()`](https://docs.python.org/zh-cn/3/library/re.html?highlight=match#re.match) 检查字符串开头，或者 [`re.search()`](https://docs.python.org/zh-cn/3/library/re.html?highlight=match#re.search) 检查字符串的任意位置。

```python
>>> re.match("c", "abcdef")    # No match

>>> re.search("c", "abcdef")   # Match
<re.Match object; span=(2, 3), match='c'>
```

## Match对象

匹配对象总是有一个布尔值 `True`。如果没有匹配的话 [`match()`](https://docs.python.org/zh-cn/3/library/re.html?highlight=match#re.Pattern.match) 和 [`search()`](https://docs.python.org/zh-cn/3/library/re.html?highlight=match#re.Pattern.search) 返回 `None` ，所以你可以简单的用 `if` 语句来判断是否匹配。

```python
match = re.search(pattern, string)
if match:
    process(match)
```

## re.split

```python
re.split(pattern, string, maxsplit=0, flags=0)
```

用 _pattern_ 分开 _string_ 。 如果 _pattern_ 中包含括号，那么所有的分割模式也会包含在列表里。

如果 _maxsplit_ 非零， 最多进行 _maxsplit_ 次分隔， 剩下的字符全部返回到列表的最后一个元素。

如果分割模式匹配到字符串的开始，那么结果将会以一个空字符串开始。结尾类似。

```python
>>> re.split(r'\W+', 'Words, words, words.')
['Words', 'words', 'words', '']

>>> re.split(r'(\W+)', 'Words, words, words.')
['Words', ', ', 'words', ', ', 'words', '.', '']

>>> re.split(r'\W+', 'Words, words, words.', 1)
['Words', 'words, words.']

>>> re.split('[a-f]+', '0a3B9', flags=re.IGNORECASE)
['0', '3', '9']

>>> re.split(r'(\W+)', '...words, words...')
['', '...', 'words', ', ', 'words', '...', '']
```
