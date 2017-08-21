# 8.virtualenv使用

## 概述

virtualenv 通过创建独立python开发环境来解决依赖、版本以及权限问题。比如一个项目依赖Django1.3。而全局开发环境为Django1.7，版本跨度太大，导致不兼容使项目无法正常运行，使用virtualenv可以解决这些问题。

>virtualenv创建一个拥有自己安装目录的环境, 这个环境不与其他虚拟环境共享库, 能够方便的管理python版本和管理python库



## 1. 安装virtualenv



使用pip安装virtualenv，使用过python的都应该知道pip包管理。

```
$ pip install virtualenv
//或者由于权限问题使用sudo临时提升权限
$ sudo pip install virtualenv
```

## 2.virtual基本使用

现在开始使用virtualenv管理python环境

**windows**
![chapter0004](images\chapter01\chapter0004.png)

> Lib 所有安装的python库都会放在这个目录下

> Scripts 是在当前环境使用的python解析器

## 3. 激活virtualenv
![chapter0004](images\chapter01\chapter0005.png)

## 4. 关闭virtualenv

使用下面命令
```
deactivate.bat
```

## 5. 指定python版本

可以使用-p PYTHON_EXE选项在创建虚拟环境的时候指定python版本

![chapter0004](images\chapter01\chapter0006.png)


##6.生成可打包环境

>某些特殊需求下,可能没有网络, 我们期望直接打包一个ENV, 可以解压后直接使用, 这时候可以使用virtualenv -relocatable指令将ENV修改为可更改位置的ENV


