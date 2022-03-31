# Python 虚拟环境安装

## 背景
多版本环境是指在一台电脑上安装多个版本的Python环境；
虚拟环境则是指在一个`Python`环境中创建多个相对独立的软件执行环境。

这些独立的虚拟环境共享一个`Python`的基础环境，即`Python`的解释器环境；
但却拥有不同的`三方库`依赖环境，其主要解决不同项目间三方库冲突的问题。

## 安装
```bash
pip install pipenv
pipenv –-version
```

## 创建虚拟环境
```bash
# 创建一个空的虚拟环境
pipenv install
# 当前虚拟环境下安装requests库
pipenv install requests
# 安装指定依赖文件中的三方库
pipenv install -r /path/to/requirements.txt
# 安装setpu.py源码库
pipenv install -e .
```
注意：安装前需要配置下虚拟环境目录下的`Pipfile`文件中url字段，更新为国内三方库的源

## 使用
交互式虚拟环境
```bash
pipenv shell
python /path/to/script.py
```
一次性虚拟环境
```bash
pipenv run python /path/to/script.py
```

## 卸载三方库
```bash
# 删除requests库
pipenv uninstall requests
# 删除所有已安装的三方库
pipenv uninstall –all
```

## 三方库迁移备份
```bash
pipenv lock -r
```
该命令会生成一个名为`requirements.txt`的依赖库文件中，该文件包含了当前虚拟环境中的所有三方库的版本信息。
