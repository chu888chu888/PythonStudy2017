# 第十章 virtualenv的使用

##概念
VirtualEnv可以方便的解决不同项目中对类库的依赖问题。这通常是通过以下方式实现的：首先将常用的类库安装在系统环境中；然后为每个项目安装独立的类库环境。这样子可以保证每个项目都运行在独立的类库环境中.

* 1、首先在系统中安装virtualenv：
  ![](/images/chapter10/0001.png)
* 2、构造项目目录，为项目安装虚拟环境：
  ![](/images/chapter10/0001.png)
* 3、启动虚拟环境，安装所需类库：
  ![](/images/chapter10/0001.png)
* 4、在虚拟环境中可以进行运行脚本等操作：
  ![](/images/chapter10/0001.png)
* 5、离开虚拟环境，使用deactivate命令：
  ![](/images/chapter10/0001.png)
* 6、在系统环境中，我们并没有安装flask类库，可以对比在系统环境中和虚拟环境中的脚本运行效果：
  ![](/images/chapter10/0001.png)
* 7、总结：
  ![](/images/chapter10/0001.png)

