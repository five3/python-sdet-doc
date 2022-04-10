# Python 运算符重载实例说明

## 什么是运算符重载
1. 运算符重载可以被看作是多态的一种形式
1. 通过给对象添加特定运算符重载的方法而实现
1. 支持运算符重载的对象可以支持特定运算符的计算表达式

## 举例
运算符：+、-、*
```python
1 + 1 = 2
'1' + '1' = '11'
[1] + [1] = [1, 1]

1 * 4 = 4
'1' * 4 = '****'
[1] * 4 = [1, 1, 1, 1]
```

## 自己实现运算符重载
```python
class MyCls:
    def __init__(self, data=0):
        if isinstance(data, int):
            self.data = data
        elif isinstance(data, str) and data.isdecimal():
            self.data = int(data)
        else:
            raise ValueError("初始化值必须给数字")
            
    def __add__(self, other):
        if isinstance(other, MyCls):
            return MyCls(self.data + other.data)
        elif isinstance(other, int):
            return MyCls(self.data + other)
            
    def __str__(self):
        return str(self.data)
```

## 使用
```python
from foo import MyCls

m = MyCls(1)
print(m)        # 1
print(m + 2)    # 1 + 2 = 3

n = MyCls(10)
print(n)        # 10
print(m + n)    # 1 + 10 = 11
print(n + m)    # 10 + 1 = 11
```