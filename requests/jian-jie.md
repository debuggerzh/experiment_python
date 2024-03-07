# 简介

Requests 库 是用来发送HTTP请求，接收HTTP响应的一个Python库，经常被用来 爬取 网站信息。 用它发起HTTP请求到网站，从HTTP响应消息中提取信息，也经常被用来做 网络服务系统的Web API 接口测试。

[中文文档点我](https://cn.python-requests.org/zh\_CN/latest/)

```python
import requests​
response = requests.get('http://mirrors.sohu.com/')
print(response.text)
```

**安装**

`pip install requests`
