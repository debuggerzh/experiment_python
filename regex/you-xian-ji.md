# 优先级

正则表达式从左到右进行计算，并遵循优先级顺序，这与算术表达式非常类似。

相同优先级的从左到右进行运算，不同优先级的运算先高后低。下表从最高到最低说明了各种正则表达式运算符的优先级顺序：

<table><thead><tr><th width="220.7020164301718">运算符</th><th>描述</th></tr></thead><tbody><tr><td>\</td><td>转义符</td></tr><tr><td>(), (?:), (?=), []</td><td>圆括号和方括号</td></tr><tr><td>*, +, ?, {n}, {n,}, {n,m}</td><td>限定符</td></tr><tr><td>^, $, \b,\B,任何字符</td><td>定位点和序列（即：位置和顺序）</td></tr><tr><td>|</td><td><p>替换，"或"操作 </p><p></p></td></tr></tbody></table>

**特别注意**：由于字符具有高于替换运算符的优先级，使得"m|food"匹配"m"或"food"。若要匹配"mood"或"food"，请使用括号创建子表达式，从而产生"(m|f)ood"。