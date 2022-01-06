---
title: 创建python虚拟环境
date: 2019-12-05 17:15:10
tags:
- python
- Django
copyright: true
categories: python
mathjax: true
---

## 虚拟环境

### 为什么需要虚拟环境

我们通过pip install XXX的方式安装第三方包，这样所有的包安装到系统的python环境中，但是这样就有一个问题，当我电脑上的Django版本和我需要迁移过来的django项目版本不一致时，就会出现问题，但是如果我电脑上同时拥有这两个版本的django，就解决这个问题了。如何让两个版本的django同时存在呢，这就需要用到虚拟环境了。

<!-- more -->

### virtualenv

#### 安装virtualenv

virtualenv是用来创建虚拟环境的软件工具，可以通过pip或者pip3来安装（如果安装了两个版本的python环境，用pip3来安装工具到python3）

```
pip install virtualenv
pip3 install virtualenv
```

#### 创建虚拟环境

在需要创建虚拟环境的路径下，通过以下命令创建虚拟环境，如果电脑同时存在两个版本的python，想指定特定的版本作为虚拟环境的解释器的话，可以通过`-p`参数来指定具体的python解释器：

```
virtualenv [-p C:\python36\python.exe] [virutalenv name]
```

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%88%9B%E5%BB%BApython%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83/%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83.png)

执行命令之后会在相应的路径下生成一个虚拟环境的文件夹abc-env

#### 进入和退出虚拟环境

创建好虚拟环境之后，可以进入虚拟环境中，需要注意的是，windows和linux进入虚拟环境的方式不同，本篇是在window上进行操作的。

windows进入虚拟环境：进入到虚拟环境abc-env的Scripts文件夹中，然后执行`activate`

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%88%9B%E5%BB%BApython%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83/%E8%BF%9B%E5%85%A5%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83.png)

然后可以在这个虚拟环境下安装我们的python包，例如安装1.10版本的Django，当我们迁移不同版本django项目时，创建虚拟环境十分有用。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%88%9B%E5%BB%BApython%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83/%E5%AE%89%E8%A3%85django.png)

当我们需要退出虚拟环境时，直接执行命令`deactivate`。

### virtualenvwrapper

virtualenvwrapper这个软件包可以让我们更方便简单的管理虚拟环境，不再需要像virtualenv那也需要跑到某个目录下来创建虚拟环境，并且激活的时候也要到相应的scripts目录下激活。

#### 安装virtualenvwrapper

安装vitualenvwrapper时会自动安装virtualenv，所以可以直接安装virtualenvwrapper，在windows操作系统下安装：

```
pip install virtualenvwrapper-win
pip3 install virtualenvwrapper-win
```

#### 创建虚拟环境

```
mkvirtualenv my_env
```

用这种方法创建虚拟环境不用像之前那样指定文件夹下创建，它会在在你当前用户下创建一个env的文件夹，然后将这个虚拟环境安装到这个目录下，如果你的电脑安装了python2和python3，并且两个版本都安装了virtualenvwrapper，那么将会使用环境变量中第一个出现的python版本作为虚拟环境的python解释器。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%88%9B%E5%BB%BApython%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83/%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%832.png)

如图，即使我在F盘中直接创建虚拟环境，也只会在我的用户名文件夹下生成一个Envs文件夹用来存放虚拟环境，并在创建完成后自动进入该虚拟环境中。

#### 操作虚拟环境

1. 进入虚拟环境

```
workon my_env
```

2. 退出当前虚拟环境

```
deactivate
```

和virtualenv退出虚拟环境的命令相同

3. 删除某个虚拟环境

```
rmvirtualenv my_env
```

其实也就是删除Envs文件夹下相应的虚拟环境文件夹

4. 列出虚拟环境

```
lsvirtualenv
```

5. 进入虚拟环境所在的目录

```
cdvirtualenv
```

#### 修改virtualenv的默认路径

因为虚拟环境默认时安装到C盘的，而如果安装多个虚拟环境，会占用C盘大量的空间，是不明智的，所以，可以更改virtualenv的默认路径。

在【我的电脑】->【右键】->【属性】->【高级系统设置】-> 【环境变量】->【系统变量】中添加一个参数WORKON_HOME，将这个参数的值设置为你需要的路径。这里我在E盘创建了Envs文件夹，所以参数值为`E:\Envs\`：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%88%9B%E5%BB%BApython%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83/%E4%BF%AE%E6%94%B9%E9%BB%98%E8%AE%A4%E8%B7%AF%E5%BE%84.png)

修改完环境变量后，新建虚拟环境，发现虚拟环境的默认路径已经修改为指定的默认路径：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%88%9B%E5%BB%BApython%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83/%E6%88%90%E5%8A%9F%E4%BF%AE%E6%94%B9%E9%BB%98%E8%AE%A4%E8%B7%AF%E5%BE%84.png)

#### 创建虚拟环境时指定python版本

在使用`mkvirtualenvs`的时候，可以指定`--python`的参数来指定具体的python路径：

```
mkvirtualenv --python==C:\python36\python.exe my_env
```

### pycharm中创建虚拟环境

如果利用pycharm创建django项目，可以在创建的同时创建虚拟环境。

选择【File】->【New project】->【Django】:

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%88%9B%E5%BB%BApython%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83/pycharm%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83.png)

其中虚拟环境的路径，会根据你的项目路径改变，自动放在项目文件夹的venv文件夹下，当然也可以自己选择存放虚拟环境的路径。虚拟环境的解释器也可以根据本地存在的python解释器来选择。这种方式比较方便，但是创建项目的时候就会比较慢了。

