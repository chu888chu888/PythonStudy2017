# 2.异常与动态表达式

##异常

  &#160; &#160; &#160; &#160;Python和java一样支持异常处理，利用try/except/finally结构，可以很方便的捕获异常，同时可以用raise语句手动抛出异常（上述四个异常处理的关键字分别对就应Java中的try/catch/finally/throw）.通过except，您可以将try标示的语句中出现的错误和异常捕获。

```
#-*-coding:utf-8-*-
import sys
def Main():
    try:
        f=open('chapter0204.py')
        s=f.readline()
        print s
    except IOError,(errno,strerror):
        print "I/O error(%s):%s" %(errno,strerror)
    except ValueError:
        print "Could not convert data to an integer"
    except:
        print "Unexpected error:",sys.exc_info()[0]
        raise
    finally:
        f.close()
if __name__=="__main__":
    Main()

```
最后说明一点，python的try也支持else语句，如果有一些代码要在try没有发生异常的情况下才执行，就可以把它放在else中。

##动态表达式

  &#160; &#160; &#160; &#160;在C#语言中，如果需要在文本框中输入1+2（或更加复杂的数学表达式）后计算它的值，可能会用到表达式解析等。现在我们有了Python，要完成这种任务可以说是非常简单：只要用内置的eval()函数，就可以计算并返回任意有效表达式的值。例如：
```
str=’1+2’
print eval(str)
```
除了eval函数之外，Python还提供了exec语句将字符串str当成有效Python代码来执行，看下面的例子：
```
exec ‘a=100’
print a
```
另外还有execfile函数，它用来执行一个外部的py文件，上一个例子存为exec.py后，运行下边的代码就知道是怎么回事了：

```
execfile(r’c:\exec.py’)
```

最后提醒，默认的eval(),exec,execfile()所运行的代码都位于当前的名字空间中，eval()，exec,和execfile()函数也可以接受一个或两个可选字典参数作为代码执行的全局名字空间和局部名字空间，具体可以参考Python手册。
列表内涵是Python最强有力的语法之一，常用于从集合对象中有选择地获取并计算元素，虽然多数情况下可以使用for/if等语句组合完成同样的任务，但列表内涵书写的代码更加简洁。
```
#-*-coding:utf-8-*-
import sys
def func():
    x=1
    y=2
    m=3
    n=4
    sum=lambda x,y:x+y
    print sum
    sub=lambda m,n:m-n
    print sub
    return sum(x,y)*sub(m,n)
if __name__=="__main__":
    print func()
```

列表内涵的一般形式如下，我们可以把[]内的列表内涵写为一行，也可以写为多行。

**[表达式 for item1 in 序列1 … for itemN in 序列N if 条件表达式]**

上面的表达式分为三部分，最左边是生成每个元素的表达式，然后是for迭代过程，最右边可以设定一个if判断作为过滤条件。
列表内涵的一个著名例子是生成九九乘法表：

**s=[(x,y,x*y) for x in range(1,10) for y in range(1,10) if x>=y]**
