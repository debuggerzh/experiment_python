# logging

### 预备知识 <a href="#yu-bei-zhi-shi" id="yu-bei-zhi-shi"></a>

### 什么是日志 <a href="#shi-mo-shi-ri-zhi" id="shi-mo-shi-ri-zhi"></a>

日志是一种可以追踪某些软件运行时所发生事件的方法。软件开发人员可以向他们的代码中调用日志记录相关的方法来表明发生了某些事情。一个事件可以用一个可包含可选变量数据的消息来描述。此外，事件也有重要性的概念，这个重要性也可以被称为严重性级别（level）。

### 日志的等级 <a href="#ri-zhi-de-deng-ji" id="ri-zhi-de-deng-ji"></a>

| 级别        | 何时使用                                       |
| --------- | ------------------------------------------ |
| DEBUG     | 详细信息，典型地调试问题时会感兴趣。 详细的debug信息。             |
| INFO      | 证明事情按预期工作。 关键事件。                           |
| WARNING   | 表明发生了一些意外，或者不久的将来会发生问题（如‘磁盘满了’）。软件还是在正常工作。 |
| ERROR     | 由于更严重的问题，软件已不能执行一些功能了。 一般错误消息。             |
| CRITICAL  | 严重错误，表明软件已不能继续运行了。                         |
| NOTICE    | 不是错误，但是可能需要处理。普通但是重要的事件。                   |
| ALERT     | 需要立即修复，例如系统数据库损坏。                          |
| EMERGENCY | 紧急情况，系统不可用（例如系统崩溃），一般会通知所有用户。              |

> java的`log4j`,`log4php`等第三方库也能较好的提供日志操作功能，有机会可以试着了解了解

### logging的日志等级 <a href="#logging-de-ri-zhi-deng-ji" id="logging-de-ri-zhi-deng-ji"></a>

<table><thead><tr><th>日志等级（level）</th><th>描述</th><th data-type="number"></th></tr></thead><tbody><tr><td>DEBUG</td><td>最详细的日志信息，典型应用场景是 问题诊断</td><td>10</td></tr><tr><td>INFO</td><td>信息详细程度仅次于DEBUG，通常只记录关键节点信息，用于确认一切都是按照我们预期的那样进行工作</td><td>20</td></tr><tr><td>WARNING</td><td>当某些不期望的事情发生时记录的信息（如，磁盘可用空间较低），但是此时应用程序还是正常运行的</td><td>30</td></tr><tr><td>ERROR</td><td>由于一个更严重的问题导致某些功能不能正常运行时记录的信息</td><td>40</td></tr><tr><td>CRITICAL</td><td>当发生严重错误，导致应用程序不能继续运行时记录的信息</td><td>50</td></tr></tbody></table>

* 该列表中的日志等级是从上到下依次增高，日志内容依次减少，即DEBUG可以显示所有日志，CRITICAL只能显示自己。例子如下：

```python
import logging

logging.debug("debug_msg")
logging.info("info_msg")
logging.warning("warning_msg")
logging.error("error_msg")
logging.critical("critical_msg")
```

输出结果

```
WARNING:root:warning_msg
ERROR:root:error_msg
CRITICAL:root:critical_msg
```

说明根记录器默认的日志级别为WARNING

### logging的使用方法 <a href="#logging-de-shi-yong-fang-fa" id="logging-de-shi-yong-fang-fa"></a>

### 常用函数 <a href="#chang-yong-han-shu" id="chang-yong-han-shu"></a>

| 函数                                        | 说明                     |
| ----------------------------------------- | ---------------------- |
| logging.debug(msg, \*args, \*\*kwargs)    | 创建一条严重级别为DEBUG的日志记录    |
| logging.info(msg, \*args, \*\*kwargs)     | 创建一条严重级别为INFO的日志记录     |
| logging.warning(msg, \*args, \*\*kwargs)  | 创建一条严重级别为WARNING的日志记录  |
| logging.error(msg, \*args, \*\*kwargs)    | 创建一条严重级别为ERROR的日志记录    |
| logging.critical(msg, \*args, \*\*kwargs) | 创建一条严重级别为CRITICAL的日志记录 |
| logging.log(level, \*args, \*\*kwargs)    | 创建一条严重级别为level的日志记录    |
| logging.basicConfig(\*\*kwargs)           | 对root logger进行一次性配置    |

```python
exception(msg, *args, **kwargs)
```

在此记录器上记录 `ERROR` 级别的消息。参数解释同 [`debug()`](https://docs.python.org/zh-cn/3/library/logging.html#logging.debug)。异常信息将添加到日志消息中。仅应从异常处理程序中调用此方法。msg参数接受一个`Exception`类型的对象。

> 不推荐使用basicConfig对日志等级进行自我创作，因为会影响代码的移植性，代码在别人那里容易起冲突

### 使用方法 <a href="#shi-yong-fang-fa" id="shi-yong-fang-fa"></a>

日志输出方法

```python
logging.basicConfig(level=logging.DEBUG)#将日志的输出级别调节为debug
logging.basicConfig(filename='demo.log',level=logging.DEBUG)#将日志的输出到demo.log文件中
logging.basicConfig(filename='demo.log',filemote='w',level=logging.DEBUG)#先清空再写入，也可以设置为继续写
```

常用的输出（字符串格式化输出）[\[3\]](broken-reference)

```python
logging.debug("姓名 %s, 年龄%d",name,age)
logging.debug("姓名 %s, 年龄%d",% (name,age))
logging.debug("姓名 {}, 年龄{}".format(name,age))
logging.debug(f"姓名{name}, 年龄{age}")
```

#### basicConfig

通过使用默认的 [`Formatter`](https://docs.python.org/zh-cn/3/library/logging.html#logging.Formatter) 创建一个 [`StreamHandler`](https://docs.python.org/zh-cn/3/library/logging.handlers.html#logging.StreamHandler) 并将其加入根日志记录器来为日志记录系统执行基本配置。 如果没有为根日志记录器定义处理器则 [`debug()`](https://docs.python.org/zh-cn/3/library/logging.html#logging.debug), [`info()`](https://docs.python.org/zh-cn/3/library/logging.html#logging.info), [`warning()`](https://docs.python.org/zh-cn/3/library/logging.html#logging.warning), [`error()`](https://docs.python.org/zh-cn/3/library/logging.html#logging.error) 和 [`critical()`](https://docs.python.org/zh-cn/3/library/logging.html#logging.critical) 等函数将自动调用 [`basicConfig()`](https://docs.python.org/zh-cn/3/library/logging.html#logging.basicConfig)。

如果根日志记录器已配置了处理器则此函数将不执行任何操作，除非关键字参数 _force_ 被设为 `True`。

```python
>>> logging.basicConfig(format="{asctime} {name}:{levelname}:{message}", 
    style="{", force=True)
>>> logging.debug('ggg')
2022-08-21 10:27:53,671 root:DEBUG:ggg
```

### logger的高级应用 <a href="#logger-de-gao-ji-ying-yong" id="logger-de-gao-ji-ying-yong"></a>

### 相关组件 <a href="#xiang-guan-zu-jian" id="xiang-guan-zu-jian"></a>

![](<.gitbook/assets/image (13).png>)

| 名称         | 作用                       |
| ---------- | ------------------------ |
| Loggers    | 记录器，提供应用程序代码直接使用的接口      |
| Handlers   | 处理器，将记录器产生的日志分发至目的地      |
| Filters    | 过滤器，提供更好的粒度控制，决定哪些日志会被输出 |
| Formatters | 格式化器，设置日志内容的组成结构和消息字段    |

#### Handlers <a href="#handlers" id="handlers"></a>

它们将日志分发到不同的目的地。可以是文件、标准输出、邮件、或者通过 socke、htt等协议发送到任何地方\
setFormatter():设置当前Handler对象使用的消息格式

* Streamhandler\
  标准输出stout分发器

```
sh = logging.StreamHandler(stream=None)
```

* Filehandler\
  将日志保存到磁盘文件的处理器

```
fh = logging.FileHandler(filename,mode='a',encoding=None,delay=False)
```

* BaseRotatingHandler
* Rotating Filehandler\
  滚动的多日志输出，按照时间or其他方式去生成多个日志
* TimedRotatingfilehandler

以下的使用较少

* Sockethandler
* Dataaramhandler
* Smtphandler
* Sysloghandler
* Nteventloghandler
* Httphandler
* WatchedFilehandler
* Qutelehandler
* Nullhandler

#### Filters <a href="#formatters-ge-shi" id="formatters-ge-shi"></a>

`Filters` 可被 `Handlers` 和 `Loggers` 用来实现比按层级提供更复杂的过滤操作。 基本过滤器类只允许低于日志记录器层级结构中低于特定层级的事件。 例如，一个用 'A.B' 初始化的过滤器将允许 'A.B', 'A.B.C', 'A.B.C.D', 'A.B.D' 等日志记录器所记录的事件。 但 'A.BB', 'B.A.B' 等则不允许。 如果用空字符串初始化，则所有事件都会通过。

#### Formatters格式 <a href="#formatters-ge-shi" id="formatters-ge-shi"></a>

| 属性          | 格式              | 描述                                         |
| ----------- | --------------- | ------------------------------------------ |
| asctime     | %(asctime)s     | 日志产生的时间，默认格式为msecs2003-07-0816:49:45,896   |
| msecs       | %(msecs)d       | 日志生成时间的亳秒部分                                |
| created     | %(created)f     | time.tme)生成的日志创建时间戳                        |
| message     | %(message)s     | 具体的日志信息                                    |
| filename    | %(filename)s    | 生成日志的程序名                                   |
| name        | %(name)s        | 日志调用者                                      |
| funcname    | %( funcname)s   | 调用日志的函数名                                   |
| levelname   | %(levelname)s   | 日志级別( DEBUG,INFO, WARNING, 'ERRORCRITICAL) |
| levene      | %( leveling)s   | 日志级别对应的数值                                  |
| lineno      | %(lineno)d      | 日志所针对的代码行号（如果可用的话）                         |
| module      | %( module)s     | 生成日志的模块名                                   |
| pathname    | %( pathname)s   | 生成日志的文件的完整路径                               |
| process     | %( (process)d   | 生成日志的进程D（如果可用）                             |
| processname | (processname)s  | 进程名（如果可用）                                  |
| thread      | %(thread)d      | 生成日志的线程D（如果可用）                             |
| threadname  | %( threadname)s | 线程名（如果可用)                                  |

### 举例 <a href="#ju-li" id="ju-li"></a>

```
#记录器
logger = logging.getLogger('cn.cccb.applog')
logger.setLevel(logging.DEBUG)
#必须设置为两个handler中级别更低的

#处理器handler
consoleHandler = logging.StreamHandler()
consoleHandler.setLevel(logging.DEBUG)

#没有给handler指定日志级别，将使用logger的级别
fileHandler = logging.FileHandler(filename='addDemo.log')
consoleHandler.setLevel(logging.INFO)

#formatter格式
formatter = logging.Formatter("%(asctime)s|%(levelname)8s|%(filename)10s%lineno)s|%(message)s")
#里面的8，10实现了占位对齐

#给处理器设置格式
consoleHandler.setFormatter(formatter)
fileHandler.setFormatter(formatter)

#记录器要设置处理器
logger.addHandler(consoleHandler)
logger.addHandler(fileHandler)

#定义一个过滤器
# flt = logging.Filter("cn.cccb")


#关联过滤器
# logger.addFilter(flt)
fileHandler.addFilter(flt)

#打印日志的代码
#logging.debug()#不能使用这个了！！！会使用WARNING的版本，不会用之前的记录器
logger.debug("姓名 %s, 年龄%d",name,age)
logger.debug("姓名 %s, 年龄%d",% (name,age))
logger.debug("姓名 {}, 年龄{}"。format(name,age))
logger.debug(f"姓名{name}, 年龄{age}")
```

### 大型工程的配置文件（推荐！！！） <a href="#da-xing-gong-cheng-de-pei-zhi-wen-jian-tui-jian" id="da-xing-gong-cheng-de-pei-zhi-wen-jian-tui-jian"></a>

> 使用字典可以进行过渡，不过需要找时间再去了解吧\~

```
#./logging.conf

#记录器：提供应用程序代码直接使用的接口
#设置记录器名称，root必须存在！！！
[loggers]
keys=root,applog

#处理器，将记录器产生的日志发送至目的地
#设置处理器类型
[handlers]
keys=fileHandler,consoleHandler

#格式化器，设置日志内容的组成结构和消息字段
#设置格式化器的种类
[formatters]
keys=simpleFormatter

#设置记录器root的级别与种类
[logger_root]
level=DEBUG
handlers=consoleHandler

#设置记录器applog的级别与种类
[logger_applog]
level=DEBUG 
handlers=fileHandler,consoleHandler
#起个对外的名字
qualname=applog
#继承关系
propagate=0

#设置
[handler_consoleHandler]
class=StreamHandler
args=(sys.stdout,)
level=DEBUG
formatter=simpleFormatter

[handler_fileHandler]
class=handlers.TimedRotatingFileHandler
#在午夜1点（3600s）开启下一个log文件，第四个参数0表示保留历史文件
args=('applog.log','midnight',3600,0)
level=DEBUG
formatter=simpleFormatter

[formatter_simpleFormatter]
format=%(asctime)s|%(levelname)8s|%(filename)s[:%(lineno)d]|%(message)s
#设置时间输出格式
datefmt=%Y-%m-%d %H:%M:%S
```

```
import logging
import logging.config

logging.config.fileConfig('logging.conf')
#使用字典就能从任意格式文件进行配置，字典是一种接口格式
# logging.config.dictConfig({"loggers":"root,applog"})

rootLogger = logging.getLogger('applog')
rootLogger.debug("This is root Logger, debug")

logger = logging.getLogger('cn.cccb.applog')
logger.debug("This is applog, debug")

try:
    int(a)
except Exception as e:
    logger.exception(e)
```

#### 我的使用方式 <a href="#wo-de-shi-yong-fang-shi" id="wo-de-shi-yong-fang-shi"></a>

1. 前面的`logger.conf`
2. 写一个`get_logging.py`

```
import logging
import logging.config

def getLogging(confName = "applog"):
    logging.config.fileConfig("logging.conf")
    return logging.getLogger(confName)
```

引用

```
from get_logging import getLogging

logger = getLogging()
```

输出

```
>>> 2021-04-26 11:23:05|   DEBUG|try.py[:21]|This is root Logger, debug
>>> 2021-04-26 11:23:05|   DEBUG|try.py[:24]|This is applog, debug
>>> 2021-04-26 11:23:05|   ERROR|try.py[:29]|name 'a' is not defined
Traceback (most recent call last):
  File "/home/kangshuaibo/code/shapan/calibration/try.py", line 27, in <module>
    int(a)
NameError: name 'a' is not defined
```

### 一些个性化 <a href="#yi-xie-ge-xing-hua" id="yi-xie-ge-xing-hua"></a>

### 设置打印颜色 <a href="#she-zhi-da-yin-yan-se" id="she-zhi-da-yin-yan-se"></a>

```
print('\x1b[36m{}\x1b[0m'.format('This is debug Logger'))
print('\x1b[1;31m{}\x1b[0m'.format('This is warn Logger'))
print('\x1b[1;4;31m{}\x1b[0m'.format('This is error Logger'))
print('\x1b[35m{}\x1b[0m'.format('This is omitted Logger'))
print('\x1b[32m{}\x1b[0m'.format('This is normal Logger'))
```

![效果](<.gitbook/assets/image (11).png>)

1. [核心参考](https://www.jianshu.com/p/a6c20c264b97) [↩︎](broken-reference)
2. [b站视频](https://www.bilibili.com/video/BV1sK4y1x7e1?from=search\&seid=9616106534784167987) [↩︎](broken-reference)
3. [字符串格式化输出](https://www.cnblogs.com/kangshuaibo/p/14668941.html) [↩︎](broken-reference)
4. [冷知识集锦-linux相关-linux终端控制符](https://www.cnblogs.com/kangshuaibo/p/14668941.html) [↩︎](broken-reference)
