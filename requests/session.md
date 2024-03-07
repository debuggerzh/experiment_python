# Session

![](https://i.loli.net/2021/09/24/ZRzvEjXwu3BoSls.png)

从上图可以看出， 服务端是通过 HTTP的响应头 `Set-Cookie` 把产生的 sessionid 告诉客户端的。

客户端的后续请求，是通过 HTTP的请求头 `Cookie` 告诉服务端它所持有的sessionid的。

HTTP 协议规定了， 网站服务端放HTTP响应中 消息头 `Set-Cookie` 里面的数据， 叫做 cookie 数据， 浏览器客户端 必须保存下来。

而且后续访问该网站，必须在 HTTP的请求头 `Cookie` 中携带保存的所有cookie数据。

requests库给我们提供一个 `Session` 类 ，通过这个类，无需我们操心， requests库自动帮我们保存服务端返回的 cookie数据， HTTP请求自动 在消息头中放入 cookie 数据。

```python
import requests

# 打印HTTP响应消息的函数
def printResponse(response):
    print('\n\n-------- HTTP response * begin -------')
    print(response.status_code)

    for k, v in response.headers.items():
        print(f'{k}: {v}')

    print('')

    print(response.content.decode('utf8'))
    print('-------- HTTP response * end -------\n\n')


# 创建 Session 对象
s = requests.Session()

# 通过 Session 对象 发送请求
response = s.post("http://127.0.0.1/api/mgr/signin",
       data={
           'username': 'byhy',
           'password': '88888888'
       })

printResponse(response)

# 通过 Session 对象 发送请求
response = s.get("http://127.0.0.1/api/mgr/customers",
      params={
          'action'    :  'list_customer',
          'pagesize'  :  10,
          'pagenum'   :  1,
          'keywords'  :  '',
      })

printResponse(response)
```
