---
description: 生成器的核心
---

# 😝 迭代器

迭代是Python最强大的功能之一，是访问集合元素的一种方式。迭代器是一个可以记住遍历的位置的对象。

迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。（拱卒）

迭代器有两个基本的方法：**iter()** 和 **next()**。

## 创建迭代器

可迭代对象指能够逐一返回其成员项的对象。 可迭代对象的例子包括所有序列类型 (例如 `list`, `str` 和 `tuple`) 以及某些非序列类型例如 `dict`, 文件对象 以及定义了 **iter**() 方法或是实现了序列语义的 **getitem**() 方法的任意自定义类对象。

字符串，列表或元组对象都可用于创建迭代器。

```python
iter(iterable)
next(iterator)
​>>> list = [1,2,3,4]
>>> it = iter(list)    # 创建迭代器对象
>>> print (next(it))   # 输出迭代器的下一个元素
1
>>> print (next(it))
2
```

把一个类作为一个迭代器使用需要在类中实现两个方法 `__iter__()` 与 `__next__()` 。

`__iter__()` 方法返回`self`， 这个迭代器对象实现了 `__next__()` 方法并通过 `StopIteration异常` 标识迭代的完成。

`__next__()` 方法（Python 2 里是 next()）会返回下一个迭代器对象。

```python
class MyNumbers:
    def __iter__(self):        
        self.a = 1        
        return self​    
    def __next__(self): 
        self.a += 1        
        return self.a   
 
myclass = MyNumbers()
myiter = iter(myclass)

print(next(myiter))
```

## StopIteration

`StopIteration`异常用于标识迭代的完成，防止出现无限循环的情况，在 \_\_next\_\_() 方法中我们可以设置在完成指定循环次数后触发 `StopIteration`异常来结束迭代。

## 遍历

可以使用`for`语句遍历迭代器。
