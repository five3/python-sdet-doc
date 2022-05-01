# Python 中如何间接定义常量

## 什么是常量
常量一旦被定义就无法再修改的符号。这样做的意义在于防止其他人修改一些关键参数和配置。

## 常量特点
1. 有且只能被赋值一次
1. 定义时即被赋值

## 通过类模拟常量特点
1. 通过类变量来模拟常量
1. 捕获类变量的设置操作，`通过__setattr__`魔法属性。
1. 控制类变量只能被赋值一次

## 代码
代码文件名称`Constant.py`
```python
import sys

class Constant:
    # 自定义异常处理
    class ConstValueError(PermissionError):
        pass
    class ConstCaseError(PermissionError):
        pass
        
    # 类属性设置事件处理
    def __setattr__(self, name, value):
        if name in self.__dict__:
            raise self.ConstValueError("不能修改常量 {0} 的值 ".format(name))
            
        if not name.isupper():
            raise self.ConstCaseError("常量名称 {0} 必须大写".format(name))
            
        self.__dict__[name] = value

sys.modules[__name__] = Constant()
```

支持多线程的单例版本。
```python
import sys
from threading import RLock

single_lock = RLock()

def Singleton(cls):
    instance = {}
    def _singleton_wrapper(*args, **kargs):
        with single_lock:
            if cls not in instance:
                instance[cls] = cls(*args, **kargs)
        return instance[cls]
        
    return _singleton_wrapper

@Singleton
class Constant:
    # 自定义异常处理
    class ConstValueError(PermissionError):
        pass
    class ConstCaseError(PermissionError):
        pass
        
    # 类属性设置事件处理
    def __setattr__(self, name, value):
        if name in self.__dict__:
            raise self.ConstValueError("不能修改常量 {0} 的值 ".format(name))
            
        if not name.isupper():
            raise self.ConstCaseError("常量名称 {0} 必须大写".format(name))
            
        self.__dict__[name] = value

sys.modules[__name__] = Constant()
```

## 使用
```python
import Constant

Constant.MAX_VALUE = 100
print(Constant.MAX_VALUE)
```
