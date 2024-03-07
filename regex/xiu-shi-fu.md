# 修饰符

修饰符也称为标记，正则表达式的标记用于指定额外的匹配策略。

标记不写在正则表达式里，标记位于表达式之外，格式如下：

```
/pattern/flags
```

下表列出了正则表达式常用的修饰符：

<table><thead><tr><th width="150">修饰符</th><th>含义</th><th>描述</th></tr></thead><tbody><tr><td>i</td><td>ignore - 不区分大小写</td><td>将匹配设置为不区分大小写，搜索时不区分大小写: A 和 a 没有区别。</td></tr><tr><td>g</td><td>global - 全局匹配</td><td>查找所有的匹配项。否则仅返回最先匹配项。</td></tr><tr><td>m</td><td>multi line - 多行匹配</td><td>将整个字符串分为多行，使边界字符 <strong>^</strong> 和 <strong>$</strong> 匹配每一行的开头和结尾。</td></tr><tr><td>s</td><td>特殊字符圆点 <strong>.</strong> 中包含换行符 （即可表示任何字符）</td><td>默认情况下的圆点 <strong>.</strong> 是匹配除换行符  之外的任何字符，加上 <strong>s</strong> 修饰符之后, <strong>.</strong> 中包含换行符 \n。</td></tr></tbody></table>

**注**：在Python的re模块中，标记通过传入常量参数实现，具体如下：

<table><thead><tr><th width="154">修饰符</th><th>标志常量</th><th>描述</th></tr></thead><tbody><tr><td>i</td><td>re.I(<strong>IGNORECASE</strong>)</td><td></td></tr><tr><td>m</td><td>re.M(<strong>MULTILINE</strong>)</td><td></td></tr><tr><td>s</td><td>re.S(<strong>DOTALL</strong>)</td><td></td></tr><tr><td>x</td><td>re.X(<strong>VERBOSE</strong>)</td><td>这个标记允许你通过分段和添加注释编写更具可读性更友好的正则表达式，空白符号会被忽略。</td></tr></tbody></table>
