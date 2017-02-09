# 5.基本数据类型元组

  &#160; &#160; &#160; &#160;元组与列表非常相似，它用()而不是[]括起来的序列。元组比列表的速度更快，但元组是一个不可变的序列，也就是与str一样，无法在原位改变它的值。除此之外，其他属性与列表基本一致。

  &#160; &#160; &#160; &#160;元组是Python中内置的一种数据结构。元组由不同的元素组成，每个元素可以存储不同类型的数据，如字符串、数字甚至元组。元组是写保护的！即元组创建后不能再做任何修改操作，元组通常代表一行数据，而元组中的元素代表不同的数据项。

**元组的创建**

```
#-*-coding:utf-8-*-
import sys
if __name__=="__main__":
    tuple_name=("apple","banana","grape","orange")
    print tuple_name[0]
```

**分片输出**

```
#-*-coding:utf-8-*-
import sys
if __name__=="__main__":
    tuple_name=("apple","banana","grape","orange")
    print tuple_name[1]
    #支持分片输出
    print tuple_name[-1]
    print tuple_name[-2]
    print tuple_name[1:3]
    #我还可以在元组中包含自已
    print '-----------------'
    tuple=(('t1','t2'),('t3','t4'))
    print tuple[0][0]
    print tuple[1][0]
```

**实现解包的功能**
```
#-*-coding:utf-8-*-
import sys
if __name__=="__main__":
    tuple_name=("apple","banana","grape","orange")
    a,b,c,d=tuple_name
    print a,b,c,d
```

元组定义的方法与列表类似，不过在定义只包含一个元素的元组时，注意在后边加一个逗号，请体会以下几句的差异：

```
#-*-coding:utf-8-*-
import sys
def Main():
    test=[0]               #列表可以这样定义
    print type(test)      #输出<type 'list'>
    test=[0,]              #也可以这样定义
    print type(test)      #输出<type 'list'>
    test=(0,)              #元组可以这样定义
    print type(test)      #输出<type 'tuple'>
    test=(0)               #但不能这样定义，Python会认为它是一个括号表达式
    print type(test)      #输出<type 'int'>
    test=0,                #也可以省略括号，但要注意与C的逗号表达式不同
    print type(test)   #输出<type 'tuple'>
    #还可以简单的交换数据
    a=1
    b=2
    a,b=b,a
    print a,b
if __name__=="__main__":
    Main()
```
##总结
  &#160; &#160; &#160; &#160;以上这类语句在Python中被广泛应用于变量交换、函数传值等应用，因此Python的解析器在不断对其进行优化，现在已经具备了相当高的效率。所以以上代码在Python2.5以后的版本中，比tmp=a;a=b;b=tmp这种常规语句更快。
  
* Python是一种动态的强类型语言，在使用变量之前无须定义其类型，但是必须声明和初始化
* “一切命名是引用”，Python中变量名是对象的引用，同一变量名可以在程序运行的不同阶段代表不同类型的数据
* “一切数据都是对象”，Python的所有数据类型都是对象，相较java具有一致的使用方法
* 把问题想得更简单一点，Python的数值类型可以说只有两种：整形和浮点
* 多使用list/tuple/set/dict这几种很pythonic的数据类型，它们分别用[]/()/([])/{}定义
