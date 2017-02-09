# 2.基本数据类型

##1 第一个程序的解析
**“一切数据是对象，一切命名是引用”**

  &#160; &#160; &#160; &#160;如果你能理解这句话，说明对Python的变量与数据类型已经有了不错的认识，与Java不同，Python在使用变量之前无须定义它的类型，试着运行下面的例子：
```
#-*-coding:utf-8-*-
"""
我的第一个应用程序
"""
import sys
def Main():
    sys.stdout.write("开始程序")
    i=1
    print i
#下面的语句看起来比较奇怪，一会儿我们会解析它
if __name__=="__main__":
    Main()
```


从上边我们可以看到，变量i在使用前并不需要定义，但是必须声明以及初始化该变量。试着运行下面的例子：
```
i=1
print i+j
```

  &#160; &#160; &#160; &#160;上面的代码会产生一个异常：”NameError:name ‘j’ is not defined”，Python提示变量j没有定义。这点和BASIC等弱类型的语言不一样。另一方面，Python与java有一个很大的差异就是在程序运行过程中，同一变量名可以（在不同阶段）代表不同类型的数据，看看下面的例子：

```
#-*-coding:utf-8-*-
"""
我的第一个应用程序
"""
import sys
def Main():
    sys.stdout.write("开始程序\n")
    i=1
    print i,type(i),id(i)
    i=1000000000
    print i,type(i),id(i)
    i=1.1
    print i,type(i),id(i)
#下面的语句看起来比较奇怪，一会儿我们会解析它
if __name__=="__main__":
    Main()
```

  &#160; &#160; &#160; &#160;变量i的类型在程序执行过程中分别经历了int long float的变化，这和静态类型语言如C语言有很大不同。静态语言只要有一个变量获取了一个数据类型，它就会一直是这个类型，变量名代表的是用来存放数据的内存位置。而Python中使用的变量名只是各种数据及对象的引用，用id()获取的才是存放数据的内存位置，我们输入的1、1000000000、1.1三个数据均会保存在id()所指示的这些内存位置中，直到垃圾回收把它们拉走，这是动态语言的典型特征，它确定一个变量的类型是在给它赋值的时候。

**另一方面，Python又是强类型的，试着运行下边的例子：**

```
#-*-coding:utf-8-*-
"""
我的第一个应用程序
"""
import sys
def Main():
    sys.stdout.write("开始程序\n")
    i=10
    j='虎虎'
    print i+j
if __name__=="__main__":
    Main()
```

**这个程序会出错，产生一个异常”TypeError:unsupported operand type(s) for +:’int’ and ‘str’”。一个正确的写法是：**

```
#-*-coding:utf-8-*-
"""
我的第一个应用程序
"""
import sys
def Main():
    sys.stdout.write("开始程序\n")
    i=10
    j='虎虎'
    print str(i)+j
#下面的语句看起来比较奇怪，一会儿我们会解析它
if __name__=="__main__":
    Main()
```

  &#160; &#160; &#160; &#160;所以，我们说Python即是一种动态类型语言，同时也是一种强类型的语言，这点是和java不同的地方，对于Python的这种变量的声明、定义、使用方式。Java程序员可能要花一段时间去适应，不过相信你会很快喜欢上它，因为它让事情变的更加简单（而且不会不安全）。
我们再小试牛刀一下，比如我们想看看根目录下面有什么数据与目录的话：
```
#-*-coding:utf-8-*-
import sys
import os
def main():
    sys.stdout.write("查看根目录下的目录\n")
    print os.listdir("/")
if __name__=="__main__":
    main()
```

##2 变量的命名规范

  &#160; &#160; &#160; &#160;Python与java的变量（函数、类等其他标识符）的命名规范基本一样，同样对大小敏感。不一样的地方是Python中以下划线开始或者结束的标识符通常有特殊的意义。例如以一个下划线开始的标识符如_foo不能用from module import *语句导入。前名均有两个下划线的标识符，如__init__被特殊方法保留。前边有两个下划线的标识符，如__bar，被用来实现类私有属性，这个将在“类和面对对象编程”中再说。最后，Python的关键字不能作为标识符，不过Python的关键字比java要少得多，可以google一下，这里就列出了。

  &#160; &#160; &#160; &#160;Python没有常量，如果你非要定义常量，可以引用const模块,Python程序中一切数据都是对象，包括自定义对象及基本数据类型，这一点和C#一样，它们都是完全面向对象的语言，所以我想C#程序员很容易理解Python的一切数据都是对象这个口号。
Python不区分值类型和引用类型，你可以把所有的类型都理解为引用类型（当然，它们的实现方式不是一样的，这里只是一个类比）。

  &#160; &#160; &#160; &#160;Python内建的数据类型有20多种，其中有些不常用到的，有些即将合并。本文将主要介绍空类型、布尔类型、整型、浮点型和字符串、元组、列表、集合、字典等9种Python内置的数据类型。
在这里，我们将前4种称为“简单数据类型”，将后5种称为“高级数据类型”，实际上Python语言本身没有这种叫法，这样分类是我自已设定的，主要是为了和java的相关知识对照方便，希望不要误导大家。

### 空类型

  &#160; &#160; &#160; &#160;空类型(None)表示该值是一个空对象，比如没有明确定义返回值的函数就是返回None。空类型没有任何属性，经常被用做函数中可选参数的默认值。None的布尔值为假。

### 布尔类型

  &#160; &#160; &#160; &#160;Python中用True和False来定义真假，你可以直接用a=True或a=False来定义一个布尔型变量，但在Python2.6里,True/False以及None却都不是关键字，在Python3.0里它们已经是关键字了，这个有点乱， 我们可以不用管它，直接使用就OK了。
  
  &#160; &#160; &#160; &#160;注意和java不同的是，Python中True和False的首字母要大写。最后一点，在java中布尔类型和其他类型之间不存在标准的转换。但是在Python中，None、任何数值类型中的0、空字符串’’,空元组（），空列表[]，空字典{}都被当作False，其他对象均为True，这点和C++差不多，要提起注意，请思考一下，下面的Python代码会输出什么？

```

#-*-coding:utf-8-*-
"""
我的第一个应用程序
"""
import sys
def Main():
    sys.stdout.write("开始程序\n")
    if 0:
        print 'True'
    else:
        print 'False'
if __name__=="__main__":
    Main()
```
**结果是:False**


### 数值类型
Python拥有四种数值类型：整型、长整型、浮点类型以及复数类型。

* 整数类型（int）
    
    用来表示从-2147483648到2147483647之间的任意整数（在某些电脑系统上这个范围可能会更大，但绝不会比这个更小）;

* 长整型(long)

    长整型（long）可以表示任意范围的整数，实际上我们把Python的long和int理解为同一种类型就可以了，因为当一个整数超过int的范围后，Python会自动将其升级为长整型。

* 双精度浮点(float)

    Python中只有64位双精度浮点数float，与java中的double类型相同(注意在Python中浮点数类型名字是float而不是double)，Python不支持32位单精度的浮点数。

* 复数(complex)

    除了整数和实数，Python还提供了一种特殊类型复数(complex)。复数使用一对浮点数表示，复数z的实部和虚部分分别用z.real和z.imag访问。在数值运算中，整数与浮点数运算的结果是浮点数，这就是所谓的“提升规则”，也就是“小”类型会被提升为“大”类型参与计算。这一点和java是一样的，提升的顺序依次为：int long float complex作为数值类型的最后一个问题，java程序员需要注意的是,Python没有内建的decimal类型，但可以导入decimal模块用来完成与货币相关的计算。

    Python中序列是由非负整数索引的对象的有序集合，它包括字符串、Unicode字符串，列表、元组、xrange对象以及缓冲区对象。


#### 字符串类型

  &#160; &#160; &#160; &#160;Python拥有两种字符串类型：标准字符串(str)是单字节字符序列，Unicode字符串(unicode)是双字节字符序列。在Python中定义一个标准字符串(str)可以使用单引号、双引号、三引号，这使得Python输入文本比java更方便。比如当Str的内容中包含双引号时，就可以用单引号定义，反之亦然。当字符中有换行符等特殊字符时，可以直接使用三引号定义。这样就方便了很多不用去记那些乱七八糟的转义字符。当然Python也支持转义字符，且含义与java基本一样。
下面是一个例子来说明这一点

```
#-*-coding:utf-8-*-
"""
字符串例子
"""
import sys
def Main():
    sys.stdout.write("开始程序\n")
    str1='i am "python"\n'
    str2="i am 'Python' \r"
    str3="""
               i'm "Python",
               <a href="http://www.sina.com.cn"></a>
         """
    #你可以把html之类的东西都直接弄进来而不需要处理
    print str1,str2,str3
if __name__=="__main__":
    Main()
```
在Python中定义一个Unicode字符串，需要在引号前面加上一个字符u,例如

```
#-*-coding:utf-8-*-
import sys
def Main():
    print u"我是派森"
if __name__=="__main__":
    Main()
```

同时注意，当使用UTF-8编码时，非unicode字符中一个汉字的长度是3，而使用gb2312时是2，见下边代码：

```
#-*-coding:utf-8-*-
'''
test
'''
import sys
def Main():
    print u"我是派森"
    unicode =u'我'
    str='我'
    print len(unicode),len(str)
    #输出的 1 3
if __name__=="__main__":
    Main()
```

#### 全局变量

不加入global关键字的话，如果你是在函数内部定义的变量的话，在外部是无法获取的。

```
#coding:utf-8
def testList():
    global list
    list=[]
    list.append("test1")
    list.append("test2")
    print list
testList()
print list
```
