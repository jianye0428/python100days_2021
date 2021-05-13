- [日志](#日志)
- [模块化组件使用](#模块化组件使用)

# 日志

日志是一种可以追踪某些软件运行时所发生事件的方法。软件开发人员可以向他们的代码中调用日志记录相关的方法来表明发生了某些事情。一个事件可以用一个可包含可选变量数据的消息来描述。此外，事件也有重要性的概念，这个重要性也可以被称为严重性级（level）。

```py
import logging

LOG_FORMAT = "%(asctime)s - %(levelname)s - %(message)s" #设置输出格式

logging.basicConfig(level = logging.WARNING, format=LOG_FORMAT)

logging.debug("This is a debug log!")
logging.info("This is a info log!")
logging.warning("This is a warning log")
logging.error("This is a error log")
logging.critical("This is a critical log")
```

Logging 中几种级别：**DEBUG < INFO < WARNING < ERROR < CRITICAL**

|%(asctime)s|日志事件发生的事件|
|-----|-----|
|%(levelname)s|该日志记录的日志级别|
|%(message)s|日志记录的文本内容|
|%(name)s|所使用的日志器名称，默认是‘root’|
|%(pathname)s|调用日志记录函数的文件的全部路径|
|%(filename)s|调用日志记录函数的文件|
|%(funcName)s|调用日志记录函数的函数名|
|%(lineno)d|调用日志记录函数的代码所在的行号|

logging模块是python内置的标准模块，主要用于输出运行日志，可以设置输出日志的等级、日志保存路径、日志文件和回滚等； 可以说，logging模块主要由4部分组成：

- Logger 记录器，提供了应用程序代码能直接使用的接口
- Handler 处理器，将记录器产生的日志记录发送至合适的目的地，或者说将Logger产生的日志传到指定位置
- Filters 过滤器，对输出的日志进行过滤，它可以决定输出哪些日志记录
- Formatter 格式化器，控制日志输出的格式，指明了最终输出中日志记录的布局

|组件|说明|
|----|----|
|Loggers(日志记录器)|提供程序直接使用的借口|
|Handlers(日志处理器)|将记录的日志发送到指定的位置|
|Filters(日志过滤器)|用于过滤特定的日志记录|
|Formatters(日志格式器)|用于控制日志信息的输出格式|


# 模块化组件使用

- 创建一个logger（日志处理器）对象
- 定义handler(日志处理器)，决定把日志发到哪里


- 设置日志级别（level）和输出格式Formatters（日志格式器）
- 把handler添加到对应的logger中去