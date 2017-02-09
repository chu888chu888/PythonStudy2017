# 3.基础数据类型列表

  &#160; &#160; &#160; &#160;Python中列表（list）类似于java中的ArrayList,用于顺序存储结构。列表用符号[]表示，中间的元素可以是任何类型（包括列表本身，以实现多维数组），元素之间用逗号分隔。取值或赋值的时候可以像C数组一样，按位置索引：
```
#-*-coding:utf-8-*-
import sys
def Main():
    array=[1,2,3]
    print array[0]
    #输出1
    array[0]='a'
    print array
    #输出['a',2,3]
    L=[123,'spam',1.23]
    #输出大小
    print len(L)
    print L[0]
    print L[:-1]#不包含最后一个
    print L+[4,5,6]#重新拼接一个新的列表
if __name__=="__main__":
    Main()
```

  &#160; &#160; &#160; &#160;从上边的代码中你可能发现一个有趣的事情：在Python的列表中可以混合使用不同类型的数据，像[‘a’,2,3]这样，不过我不建议你这样做，我觉着没有什么好处。

  &#160; &#160; &#160; &#160;另外还可以看到，列表是可变的序列，也就是说我们可以在“原地”改变列表上某个位置所存储的对象的值。

  &#160; &#160; &#160; &#160;Python中的list支持多数的操作，同时list也支持“切片”这样的操作。切片指的是抽取序列的一部分，其形式为：list[start:end:step].其抽取规则是：从start开始，每次加上step，直到end为止。默认的step为1;当start没有给出时，默认从list的第一个元素开始;当end=-1时表示list的最后一个元素，依次类推。一些简单的例子见下边代码：

```

#-*-coding:utf-8-*-
import sys
def Main():
    test=['never',1,2,'yes',1,'no','maybe']
    print test[0:3]#包括test[0],不包括test[3]
    print test[0:6:2]#包括test[0],不包括test[6],而且步长为2
    print test[:-1]#包括开始，不包括最后一个
    print test[-3:]#抽取最后3个
if __name__=="__main__":
    Main()
```

  &#160; &#160; &#160; &#160;字符串、列表、元组都支持切片操作，这个很方便，应该学会熟练使用它。最后，list是Python中最基础的数据结构，你可以把它当作链表、堆栈或队列来使用，效率还不错。Python中没有固定长度数组，如果你确实很在意性能，可以改入array模块来创建一个C风格的数组，它的效率很高，这里就不详细介绍了。

**我们还可以对其进行排序与反转**

```
#-*-coding:utf-8-*-
import sys
def Main():
    array=[5,2,3,1,8]
    array.sort()
    for s in array:
        print s
    array.reverse()
    for s in array:
        print s
if __name__=="__main__":
    Main()
```
  &#160; &#160; &#160; &#160;Python核心数据类型的一个优秀的特性就是它们支持任意的嵌套。能够以任意的组合对其进行嵌套。这种特性的一个直接应用就是实现矩阵，或者Python中的多维数组。一个嵌套列表的殂表能够完成这个基本的操作。

```
#-*-coding:utf-8-*-
import sys
def Main():
    M=[[1,2,3],
       [4,5,6],
       [7,8,9]]
    print M[0]
    print M[1]
    print M[2]
if __name__=="__main__":
    Main()
```

  &#160; &#160; &#160; &#160;处理序列的操作和列表的方法中，Python还包括了一个更高级的操作，称作列表解析表达式，从而提供了一种处理像矩阵这样结构的强大工具。列如，假设我们需要从列举的矩阵中提取出第二列。因为矩阵是按照行进行存储的，所以可以通过简单的索引即可获得行，使用列表解析可以同样简单地获得列。

```
#-*-coding:utf-8-*-
import sys
def Main():
    M=[[1,2,3],
       [4,5,6],
       [7,8,9]]
    
    col2=[row[1] for row in M]
    print col2
    col3=[row[1]+1 for row in M]
    print col3
    colfilter=[row[1] for row in M if row[1]%2==0]
    print colfilter
if __name__=="__main__":
    Main()
```

###常用方法

* len(list)长度
* del list 删除对象

列表对象支持的方法：

* append(x) 尾部追加 单个对象x，使用多个对象会引起异常。
* count(x) 返回对象x在list中出现的次数
* extend(L) 将列表L中的项添加到表中
* index(x) 返回匹配对象x第一个表项的索引，无匹配时产生异常
* insert(i,x) 在索引‘i’的元素钱插入对象x
* pop(x) 删除列表中索引x的表项，并返回同该表项的值，无参数删除最后
* remove(x) 删除表匹配对象x的第一个元素，无匹配时异常
* reverse() 颠倒列表元素的顺序
* sort() 对列表排序

此外可简单使用+实现列表连接：

```[3,4] + [[1,2],5,6] --> [3,4,[1,2],5,6]```

删除列表中的重复项：M = list(set(L))，python的set和其他语言类似, 是一个无序不重复元素集

