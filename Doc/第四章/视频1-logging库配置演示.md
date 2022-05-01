# logging库配置演示

## logging模块
logging 模块主要包含以下几个基础类：
1. Logger——对外提供日志记录 API 的类。 
1. Handler——处理日志记录请求的类，并记录到指定终端上。
1. Filter——用于过滤日志的输出内容。
1. Formatter——指定日志输出的具体格式。

## 简单使用
```python
import logging

# 获取默认的logger
logger = logging.getLogger()
# 设置日志等级， 默认为logging.WARNING
logger.setLevel(logging.ERROR)
# 进行相关类型的日志记录
logger.critical("critical")
logger.error("error")
logger.warning("warning")
logger.info("info")
logger.debug("debug")
```

## logging配置
logging 模块支持的 4 种配置方式分别如下：
1. 通过 logging.basicConfig 函数设置。
1. 通过 logging.config.fileConfig 函数设置。
1. 通过 logging.config.dictConfig 函数设置。
1. 通过 logging 的 API 设置。
