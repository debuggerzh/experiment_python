# 检查http响应

**检查状态码**

直接 通过 reponse对象的 `status_code` 属性获取

**检查响应头**

直接 通过 reponse对象的 `headers` 属性获取。

response.headers 对象的类型 是 继承自 Dict 字典 类型的一个 类，我们也可以像操作字典一样操作它。

**检查响应体**

直接通过response对象 的 `text` 属性即可获取。

```python
import requests

response = requests.get('http://mirrors.sohu.com/')
response.encoding='utf8' # 指定编码格式为utf-8
print(response.text)
```

如果我们要直接获取消息体中的字节串内容，可以使用 `content` 属性。

`response.content.decode('utf8')`可以把消息体中的字节串内容解码为utf-8格式。

为了 方便处理 响应消息中`json` 格式的数据 ，我们通常应该把 json 格式的字符串 转化为 python 中的数据对象。

```python
import requests, json
response = requests.post("http://httpbin.org/post", data={1:1, 2:2})
# 可以直接使用 json库里面的 loads 函数， 把 json 格式的字符串 转化为 数据对象
obj = json.loads(response.content.decode('utf8'))
# 更方便的方法，可以使用 Response对象的 json方法
obj = response.json()
```

\
