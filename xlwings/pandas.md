---
layout: editorial
---

# pandas

## 向Excel输出的封装类

```python
class pandas.ExcelWriter(path, engine=None, date_format=None, datetime_format=None, mode='w', storage_options=None, if_sheet_exists=None, engine_kwargs=None, **kwargs)
```

其中path可以是`.xls`或`.xlsx`路径或**typing.BinaryIO**（一个IO泛型）。

engine指定具体使用的库。

```python
df = pd.DataFrame([["ABC", "XYZ"]], columns=["Foo", "Bar"])  
with pd.ExcelWriter("path_to_file.xlsx") as writer:
    df.to_excel(writer)  
```

## 读取Excel文件

```python
pandas.read_excel(io, sheet_name=0, header=0, names=None, index_col=None, usecols=None, squeeze=None, dtype=None, engine=None, converters=None, true_values=None, false_values=None, skiprows=None, nrows=None, na_values=None, keep_default_na=True, na_filter=True, verbose=False, parse_dates=False, date_parser=None, thousands=None, decimal='.', comment=None, skipfooter=0, convert_float=None, mangle_dupe_cols=True, storage_options=None)
```

其中io可以为字符串所描述的本地或网络路径、路径类对象、文件类对象。

sheet\_name指定打开的工作表，默认值0表示第一张工作表（不包括图表），列表参数指定要打开的多张工作表，None则表示打开所有工作表。

index\_col指定将成为索引的列，第一列索引为0。数字列表参数将指定多索引，默认值None表示新增索引列，第一行索引为0。

header指定表头，默认值0表示指定第一行为表头。指定None则使用0，1，2……为表头。

### 返回值

返回DataFrame或DataFrame列表。

```python
pd.read_excel(open('tmp.xlsx', 'rb'),
              sheet_name='Sheet3')  

   Unnamed: 0      Name  Value
0           0   string1      1
1           1   string2      2
2           2  #Comment      3
```

## 导出数据帧

```python
DataFrame.to_excel(excel_writer, sheet_name='Sheet1', na_rep='', float_format=None, columns=None, header=True, index=True, index_label=None, startrow=0, startcol=0, engine=None, merge_cells=True, encoding=None, inf_rep='inf', verbose=True, freeze_panes=None, storage_options=None)
```

其中excel\_writer可以是路径类对象、文件类对象或**ExcelWriter**对象。

sheet\_name为**字符串**，默认为'Sheet1'。

## 排序

### `DataFrame.sort_values`

```python
DataFrame.sort_values(by, axis=0, ascending=True, inplace=False, kind='quicksort', na_position='last', ignore_index=False, key=None)
```

其中by指定参与排序的关键字，可以是单个字符串或者字符串列表（多排序）。

ascending和by参数相对应，指定递增、递减。

na\_position决定非数字单元格的位置。

key指定对关键字进行处理的函数。

#### 返回值

inplace参数默认取False时，函数返回一个已排序的DataFrame对象，否则原地排序，返回None。

```python
df = pd.DataFrame({
    'col1': ['A', 'A', 'B', np.nan, 'D', 'C'],
    'col2': [2, 1, 9, 8, 7, 4],
    'col3': [0, 1, 9, 4, 2, 3],
    'col4': ['a', 'B', 'c', 'D', 'e', 'F']
})
df

  col1  col2  col3 col4
0    A     2     0    a
1    A     1     1    B
2    B     9     9    c
3  NaN     8     4    D
4    D     7     2    e
5    C     4     3    F

df.sort_values(by=['col1', 'col2'])
  col1  col2  col3 col4
1    A     1     1    B
0    A     2     0    a
2    B     9     9    c
5    C     4     3    F
4    D     7     2    e
3  NaN     8     4    D
```

### `DataFrame.sort_index`

```python
DataFrame.sort_index(axis=0, level=None, ascending=True, inplace=False, kind='quicksort', na_position='last', sort_remaining=True, ignore_index=False, key=None)
```

将某一行或某一列作为索引对数据进行排序。

其中axis为默认值0表示对数据行排序，为1表示对数据列排序。

该函数可以用`sort_values`的等价形式代替。
