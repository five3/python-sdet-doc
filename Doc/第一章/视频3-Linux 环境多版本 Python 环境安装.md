# Linux 环境多版本Python环境安装

## 背景
`Linux`环境下容易出现多版本Python共存的情况，为了很好的隔离和维护不同版本的环境正常。因此，需要通过一套工具来专门对多版本环境进行管理。

## 多版本工具
`pyenv` 是Python的一个多版本管理工具。它不仅支持 Python 2 和 Python 3 版本的共存，还支持 Python 2.6、Python 2.7、Python 3.5、
Python 3.7 的共存，甚至还支持 CPython 与 PyPy、Jython、IronPython、Anaconda、ActivePython
等发行版的共存。

## 安装
```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv 
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile 
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile 
echo 'eval "$(pyenv init --path)"' >> ~/.bash_profile 
echo 'eval "$(pyenv init -)"' >> ~/.bash_profile 
source ~/.bash_profile
```

更多`Linux`系统安装`pyenv`的详细说明见官网[github](https://github.com/pyenv/pyenv.git)。
如果`github`下载不了的，可以从[这里](https://download.csdn.net/download/five3/85056141)下载zip包

## 使用
### 版本及帮助查看
```bash
pyenv -v
pyenv -h
```

### install命令
`pyenv install` 主要用于安装Python版本。
```bash
pyenv install -l        # 查询可安装的Python版本
pyenv install 3.7.5     # 安装具体的Python版本
```
注意：如果安装过程中出现失败，可能是因为缺少基础依赖库的原因。可通过如下命令来安装所需的依赖库。
```bash
yum install gcc zlib-devel bzip2 bzip2-devel readline-devel openssl openssl-devel -y
```

### version/versions命令
1. `pyenv version` 命令用于查看当前目录所使用的Python版。
1. `pyenv versions` 命令则是查看当前系统中全部已安装的Python版本。其中带`*`的则是当前目录的Python版本

### local/global命令
1. `pyenv local 3.7.5` 设置当前目录使用`3.7.5`版本的Python。
1. `pyenv global 3.7.5` 设置当前系统全局环境默认使用`3.7.5`版本的Python。

### uninstall命令
`pyenv uninstall 3.7.5` 用于卸载已经安装的`3.7.5`版本的Python。
