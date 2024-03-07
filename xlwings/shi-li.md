# 实例

## 基础读写

```python
import xlwings as xw

with xw.App() as app:
    book = app.books.active
    sheet = book.sheets.active
    area = sheet.range('A1', 'C3')
    area.value = 114514
    book.save('kuso.xlsx')
    book.close()
```

## 排序

```python
import xlwings as xw
from xlwings import Range

try:
    book = xw.Book(r'../student.xls')
    sheet = book.sheets[0]
    # 向右下角扩展选区，不能选择标题行
    data_region: Range = sheet.range('A2').expand()
    data_region.api.Sort(Key1=sheet['B1'].api, Order1=1,  # 升序
                         Key2=sheet['C1'].api, Order2=2,  # 降序
                         Orientation=1)  # 按列排序
    book.save('kuso.xlsx')
finally:
    xw.apps.active.kill()

```
