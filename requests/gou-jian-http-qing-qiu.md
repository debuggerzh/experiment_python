# 构建http请求

**GET:`urlencoded` 格式**

`https://www.baidu.com/s?wd=iphone&rsv_spt=1`

问号后面的部分 `wd=iphone&rsv_spt=1` 就是 url 参数，每个参数之间是用 `&` 隔开的。

上面的例子中 有两个参数 wd 和 rsv\_spt， 他们的值分别为 iphone 和 1 。

使用Requests发送HTTP请求，url里面的参数，通常可以直接写在url里面。

当参数中包含特殊字符时，可以把这些参数放到一个字典里面，然后把字典对象传递给 Requests请求方法的 `params`参数，如下

```python
urlpara = {
    'wd':'iphone&ipad',
    'rsv_spt':'1'
}
​response = requests.get('https://www.baidu.com/s', params=urlpara)
```

**构建请求头**

每个消息头也就是一种 _键值对_的格式存放数据

Requests发送这样的数据，只需要将这些键值对的数据填入一个字典。

然后使用post方法的时候，指定参数 headers 的值为这个字典就可以了，如下

```python
headers = {
    'user-agent': 'my-app/0.0.1',
    'auth-type': 'jwt-token'
}
​r = requests.post("http://httpbin.org/post", headers=headers)
```

**构建请求体**

**XML格式**

```python
payload = 
'''
<?xml version="1.0" encoding="UTF-8"?>
<WorkReport>
    <Overall>良好</Overall>    
    <Progress>30%</Progress>    
    <Problems>暂无</Problems>
</WorkReport>
'''​
r = requests.post("http://httpbin.org/post",                  
            data=payload.encode('utf8')) # data指明请求体数据，utf8编码用于包含中文的数据
```

如果传入的是字符串类型，Requests 会使用缺省编码 `latin-1` 编码为字节串放到http消息体中，发送出去。

**POST：urlencoded 格式**

只需要将这些键值对的数据填入一个字典。

然后使用post方法的时候，指定参数 data 的值为这个字典就可以了，如下

```python
payload = {'key1': 'value1', 'key2': 'value2'}
​r = requests.post("http://httpbin.org/post", data=payload)
```

**JSON格式**

```python
import requests,json

payload = {
    "Overall":"良好",
    "Progress":"30%",
    "Problems":[
        ...
    ]
}
# 可以使用json库的dumps方法
r = requests.post("http://httpbin.org/post", data=json.dumps(payload))
# 也可以将 数据对象 直接 传递给post方法的 json参数
r = requests.post("http://httpbin.org/post", json=payload)
```

\
