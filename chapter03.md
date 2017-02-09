# 第三章 函数及函数编程

  &#160; &#160; &#160; &#160;在java中没有独立的函数存在，只有类的（动态或静态）方法这一概念，它指的是类中用于执行计算或其它行为的成员。在Python中，你可以使用类似C#的方式定义类的动态或静态成员方法，因为它与java一样支持完全的面向对象编程。你也可以用过程式编程的方式来编写Python程序，这时Python中的函数与类可以没有任何关系，类似C语言定义和使用函数的方式。此外，Python还支持函数式编程，虽然它对函数编程的支持不如LISP等语言那样完备，但适合使用还是可以提高我们工作的效率的。
  
## 函数的定义

  &#160; &#160; &#160; &#160;函数定义是最基本的行为抽象代码，也是软件复用最初级的方式。Python中函数的定义语句由def关键字、函数名、括号、参数及冒号组成。下面是几个简单的函数定义语句：

```

#-*-coding:utf-8-*-
import sys
def Main():
    def F1():
        print "我是F1"
    def F2(x,y):
        a=x+y
        return a
    #定义有多个返回值的函数，用逗号分割不同的返回值，
    #返回结果是一个元组
    def F3(x,y):
        a=x/y
        b=x%y
        return a,b
if __name__=="__main__":
    Main()
```

  &#160; &#160; &#160; &#160;可能你已经注意到了，Python定义函数的时候并没有约束参数的类型，它以最简单的形式支持了泛型编程。你可以输入任意类型的数据作为参数，只要这些类型支持函数内部的操作


## 定义一个交换函数


```
#-*-coding:utf-8-*-
import sys
import random
def compareNum(num1,num2):
    if(num1>num2):
        return 1
    elif(num1==num2):
        return 0
    else:
        return -1
if __name__=="__main__":
    num1=random.randrange(1,9)
    num2=random.randrange(1,9)
    print "num1=",num1
    print "num2=",num2
    print compareNum(num1,num2)
```

## 函数的默认参数与返回值

```
#-*-coding:utf-8-*-
import sys
def arithmetic(x=1,y=1,operator="+"):
    result={
        "+":x+y,
        "-":x-y,
        "*":x*y,
        "/":x/y
    }
    return result.get(operator)
if __name__=="__main__":
    print arithmetic(1,2)
    print arithmetic(1,2,"-")
```


## 返回多个值

**Python支持多个返回值**

```
#coding:utf-8
def testList():
    return "aaa","bbb"
a,b=testList()
print a
print b
```

##locals函数和globals函数介绍

  &#160; &#160; &#160; &#160;Python有两个内置的函数，locals() 和globals()，它们提供了基于字典的访问局部和全局变量的方式。首先，是关于名字空间的一个名词解释。是枯燥，但是很重要，所以要耐心些。Python使用叫做名字空间的东西来记录变量的轨迹。名字空间只是一个字典，它的键字就是变量名，字典的值就是那些变量的值。实际上，名字空间可以象Python的字典一样进行访问，一会我们就会看到。

  &#160; &#160; &#160; &#160;在一个Python程序中的任何一个地方，都存在几个可用的名字空间。每个函数都有着自已的名字空间，叫做局部名字空间，它记录了函数的变量，包括 函数的参数和局部定义的变量。每个模块拥有它自已的名字空间，叫做全局名字空间，它记录了模块的变量，包括函数、类、其它导入的模块、模块级的变量和常量。还有就是内置名字空间，任何模块均可访问它，它存放着内置的函数和异常。

  &#160; &#160; &#160; &#160;当一行代码要使用变量 x 的值时，Python会到所有可用的名字空间去查找变量，按照如下顺序：
  
1. 局部名字空间 - 特指当前函数或类的方法。如果函数定义了一个局部变量 x，Python将使用这个变量，然后停止搜索。

2. 全局名字空间 - 特指当前的模块。如果模块定义了一个名为 x 的变量，函数或类，Python将使用这个变量然后停止搜索。

3. 内置名字空间 - 对每个模块都是全局的。作为最后的尝试，Python将假设 x 是内置函数或变量。如果Python在这些名字空间找不到 x，它将放弃查找并引发一个 NameError 的异常，同时传递 There is no variable named 'x' 这样一条信息,象Python中的许多事情一样，名字空间在运行时直接可以访问。特别地，局部名字空间可以通过内置的 locals 函数来访问。全局（模块级别）名字空间可以通过 globals 函数来访问




