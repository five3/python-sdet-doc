# Python2 与 Python3 的主要区别

## 前述
对于刚开始准备学习Python的朋友来说，可以先忽略本小节内容。直接学习Python3版本的语法即可，避免给自己的造成扰乱。
等到后期对于Python3已经熟练掌握之后，再回过头来了解下与Python2的区别也不为晚。

对于已经学习过Python2，目前正准备向Python3转换的朋友来说，还是需要先了解下它们之间的一些区别，避免编码过程中出现意外困扰。

## 默认编码
默认编码的改变是Python3的一个核心升级点，如果说其它的升级点只影响局部功能的话；那么默认编码的变更则是影响全局的，涉及到的是底层的变更，对上层的影响面也更广。

Python2 代码文件默认是`ASCII`编码；Python3 代码文件默认是`UTF-8`编码。
```python
s = '中国'
```
同样的编码文件内容由于涉及到中文。在`Python2`中就会执行报错，而`Python3`中则执行正常。
> 因为 ASCII 编码不能正常对中文进行编解码，而 UTF-8 编码则可以。当然 Python2 中可以通过显式指定代码文件的编码类型来解决中文编解码问题。

`Python2`解释器中默认字符串类型为`bytes`(通过特定编码方式编码后得到的有序字节内容)；`Python3`解释器中默认字符串类型为`Unicode`（一种各编码方式互相转换时过渡的中间态编码）。
```python
type('中国')
```
同样是字符串类型，在`Python2`代表的是经过编码后的`bytes`类型；而`Python3`中则是`Unicode`类型。

## print函数
Python2 中`print`是语句；Python3 中`print()`是函数。
```python
# Python2
print 'hello Python'
# Python 3
print('hello Python')
```

## True/False
`Python2`中`True`和`False`并不是保留字而是全局变量，因此我们甚至可以在编程时改变其值。当然这就会非常的危险。

`Python3`中自然就解决了这个隐患，`True`和`False`正式被作为保留字，且其值也不再可以被更改。

## nonlocal
`Python3`中引入的新的保留字，其作用与`global`保留字有类型的作用。
所不同的是`global`是引入全局的变量来替代局部变量；`nonlocal`则引入全局与局部之间的变量来替代局部变量。
```python
# global demo
j = 1
def foo():
    j = 2
    def bar():
        global j
        j += 1
    bar()
    print(j)    # 2
    
foo()
```
```python
# nonlocal demo
j = 1
def foo():
    j = 2
    def bar():
        nonlocal j
        j += 1
    bar()
    print(j)    # 3
    
foo()
```

## 异常捕获
异常捕获的差异仅仅体现在语法上的变化。由原来的
```python
# Python2
try:
    1 / 0
except Exception, e:
    pass
```
改为
```python
# Python3
try:
    1 / 0
except Exception as e:
    pass
```

## 除法运算符
`Python`中有2种除法运算符。
1. /：普通除法
1. //：地板除，即取整除法，不保留小数部分

`Python3`中的改变只针对普通除法。把普通除法与地板除的功能分的非常明确。
```python
# Python2
3 / 2       # 1
3 / 2.0     # 1.5
```
`Python3`中普通除法不再具备地板除的能力。
```python
# Python3
3 / 2       # 1.5
3 / 2.0     # 1.5
```

## range函数
`Python3`中`range`函数等同于`Python2`中的`xrange`。而`Python2`中存在的`xrange`则直接在`Python3`中被移除掉。

## input函数
`Python3`中`input`函数等同于`Python2`中的`raw_input`。而`Python2`中存在的`raw_input`则直接在`Python3`中被移除掉。

## file函数
`Python2`中存在的`file`在`Python3`中被移除掉，仅保留`open`函数用于文件的读写操作。

## <>运算服务 
`Python2`中存在的`<>`在`Python3`中被移除掉，仅保留`!=`用于操作数之间的不等于比较。

## ``表达式
`Python2`中存在的``在`Python3`中被移除掉，仅保留`repr`函数用于显示字符串的源信息。

## long类型
`Python2`中存在的`long`在`Python3`中被移除掉，仅保留`int`代表int、long类型。

## double类型
`Python2`中存在的`double`在`Python3`中被移除掉，仅保留`float`代表float、double类型。
