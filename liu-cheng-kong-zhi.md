# 😆 流程控制

## 条件控制语句

```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:    
    statement_block_3
```

Python 中用 **elif** 代替了 **else if**，所以if语句的关键字为：**if – elif – else**。

条件控制语句可以嵌套使用。

{% hint style="info" %}
1. 每个条件后面要使用冒号 **:** ，表示接下来是满足条件后要执行的语句块。
2. 使用缩进来划分语句块，相同缩进数的语句在一起组成一个语句块。
3. 在Python中**没有**switch – case语句。
{% endhint %}

## 循环语句

循环语句**可以有 else 子句**，它在穷尽列表(如for循环)或条件变为 false (如while循环)导致循环终止时被执行，**但循环被 break 终止时不执行**。

### **while循环**

```python
while <expr>:
    <statement(s)>
else:
    <additional_statement(s)>
```

同样需要注意冒号和缩进。另外，在 Python 中没有 `do..while` 循环。

expr 条件语句为 true 则执行 statement(s) 语句块，如果为 false，则执行`else`子句additional\_statement(s)，并退出循环。

### **for循环**

Python for 循环可以遍历任何可迭代对象，如一个列表或者一个字符串。

当所有项被耗尽时 (这会在序列为空或迭代器引发 [`StopIteration`](https://docs.python.org/zh-cn/3/library/exceptions.html#StopIteration) 异常时立刻发生)，`else` 子句的子句体如果存在将会被执行，并终止循环。

```python
for <variable> in <sequence>:
    <statements>
else:    
    <statements>
```

## **特殊语句**

### **pass**

Python pass是空语句，是为了保持程序结构的完整性。

pass 不做任何事情，一般用做占位语句。

### **break**

**break** 语句可以跳出 for 和 while 的循环体。如果你从 for 或 while 循环中终止，任何对应的循环 else 块将不执行。

### **continue**

**continue** 语句被用来告诉 Python 跳过当前循环块中的剩余语句，然后继续进行下一轮循环。
