# 1.流程控制

##条件语句
  &#160; &#160; &#160; &#160;Python用if,elif,else这三个关键字进行条件判断，与java唯一的区别就是用elif取代else if，少打两个字，其它都一样，此外别忘了在if等语句后加：号
如果一个流程控制下不做任何事情，记得写一句pass语句，不然Python会报错。例如：

```
if 0:
     pass #这一句语没有什么意义
```
  &#160; &#160; &#160; &#160;在Python中没有switch语句，你可以使用if..elif..else语句来完成同样的工作。如果你觉得繁琐，可以试试dict实现的方式，下边是一个例子，分别对比了两种实现方式。
  ```
  #-*-coding:utf-8-*-
import sys
def Main():
    #使用if替代
    x='4'
    print "OK"
    if x=='1':
        print 'one'
    elif x=='2':
        print 'two'
    else:
        print 'nothing!'
    #使用dict
    numtrans={
        1:'one',
        2:'two',
        3:'three'
    }
    try:
        print numtrans[x]
    except KeyError:
        print 'nothing!'
if __name__=="__main__":
    Main()

  ```
##循环
  &#160; &#160; &#160; &#160;Python支持两种循环语句while循环和for循环，不支持java中的do-while循环。在Python的while循环和Java基本一致，此处我们着重比较两种语言中的for循环的区别。
  
  &#160; &#160; &#160; &#160;说的简单一点，python中的for语句相当于java中的foreach语句,它用于从集合对象（list/str/tuple等）中遍历数据。例如：
  
```
for I in [1,2,3,4,5]:
print i
for I in range(10):
	print i

```
```
#-*-coding:utf-8-*-
import sys
if __name__=="__main__":
    tuple=(("apple","banana"),("grape","orange"))
    for i in range(50,100+1):
        print i
```

```
#-*-coding:utf-8-*-
import sys
if __name__=="__main__":
    tuple=(("apple","banana"),("grape","orange"))
    for i in range(50,100+1):
        print i
    range(1,5) #代表从1到5(不包含5)
    range(1,5,2) #代表从1到5，间隔2(不包含5)
    range(5) #代表从0到5(不包含5)

```

```
__author__ = 'TenYear'
#-*-coding:utf-8-*-
"""
my fist App
"""
import sys
import urllib
def Main():
    itemlist=[1,2,3,4,5,4]
    for m in itemlist:
        print m
#this is test
if __name__=="__main__":
    Main()

```
