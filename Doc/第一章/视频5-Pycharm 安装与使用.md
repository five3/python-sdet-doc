# Pycharm 安装与使用

## 下载地址
```bash
# Windows 版本下载页
https://www.jetbrains.com/pycharm/download/#section=windows
# 社区版安装包下载地址
https://www.jetbrains.com/pycharm/download/download-thanks.html?platform=windows&code=PCC
```

## 安装
1. 双击`exe`文件
1. 选择安装目录

## 配置Python解释器
1. `File` -> `Settings` -> `Project Interpreter`
1. 选择安装的`Python`解释器位置
1. 点击`OK`

## 创建项目
1. `File` -> `New Project…` -> `Pure Python`
1. `Location` 处设置项目路径
1. 点击`Create`

## 新建文件
1. `New` -> `Python File`
1. 输入文件名
1. 点击`OK`

## 运行与调试
第一条运行代码
```python
print("Hello Python")
```
调试代码
```python
n = 10
count = 0
for i in range(1, n+1): 
 count += i 
 print(count)
```
