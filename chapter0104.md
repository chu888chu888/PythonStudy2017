# 4.基本数据类型字典

## 概述

  &#160; &#160; &#160; &#160;用过java中的字典的人对Hashtable应该不会陌生，Python里的哈希表就是字典(dict)了。与set类似，字典是一种无序存储结构，它包括关键字（key）和关键字对应的值(value)。java程序员需要了解的就是,在Python中dict是一种内置的数据类型，定义方式为：

```
#当有多个键值时，用逗号进行分割。
dictionary={key:value}
```
  &#160; &#160; &#160; &#160;字典里的关键字为不可变类型，如字符串、整数、只包含不可变对象的元组，列表等不能作为关键字。字典中一个键只能与一个值关联，对于同一个键，后添加的值会覆盖之前的值。学过数据结构的人对字典的散列查找效率应该都有认识，所以我建议在可能的情况下尽量多用字典，其它的就不多写了。

```
#-*-coding:utf-8-*-
import sys

if __name__=="__main__":
    dict={"a":"apple","b":"banana","g":"grape","o":"orange"}
    print dict
    print dict["a"]
    dict2={1:"apple",2:"banana",3:"grape",4:"orange"}
    print dict2
    print dict2[1]
```

```
#-*-coding:utf-8-*-
import sys

if __name__=="__main__":
    #字典的添加、删除、修改操作
    dict={"a":"apple","b":"banana","g":"grape","o":"orange"}
    dict["w"]="watermelon"
    print dict
    del(dict["a"])
    print dict
    print dict.pop("b")
    #dict.clear()
    #print dict
    #字典的遍历
    for k in dict:
        print "dict[%s]="%k,dict[k]
```

```
#-*-coding:utf-8-*-
import sys

if __name__=="__main__":
    #字典的keys()与values()方法
    dict={"a":"apple","b":"banana","g":"grape","o":"orange"}
    #输出key的列表
    print dict.keys()
    #输出values的列表
    print dict.values()
    
```


```
#-*-coding:utf-8-*-
import sys
def Main():
    D={'food':'spam','quantity':4,'color':'pink'}
    print D['food']
    D['quantity']+=1
    print D
    #另外一种定义字典的方法
    D={}
    D['name']='Bob'
    D['job']='dev'
    D['age']=40
    print D
    #使用键值,进行排序
    D={'a':1,'b':2,'c':3}
    print D
    Ks=D.keys()
    print Ks
    Ks.sort()
    print Ks
    for key in Ks:
        print key,'=>',D[key]
    for key in sorted(D):
        print key,'=>',D[key]
    #迭代与优化
    squares=[x ** 2 for x in [1,2,3,4,5]]
    print squares
    #与以下代码是等效的
    squares=[]
    for x in [1,2,3,4,5]:
        squares.append(x**2)


if __name__=="__main__":
    Main()
```


在访问的时候，如果这个键值不存在的话，如果我们没有做任何判断的话，会出现错误，这个时候我们可以用以下代码来进行判断。
```
#-*-coding:utf-8-*-
import sys
def Main():
    D={'food':'spam','quantity':4,'color':'pink'}
    #测试不存在的键值
    if not D.has_key('f'):
        print '不存在这个键值'
    else:
        print D['f']

if __name__=="__main__":
    Main()
```


### 常用方法

* has_keys(x) 若字典中有x返回true
* keys() 返回键的列表
* values() 返回值的列表
* dict.items() 返回tuples的列表。每个tuple有字典的dict的键和相应的值组成
* clear() 删除词典的所有条目
* copy() 返回字典的高层结构的拷贝，但不复制嵌入结构，而复制那些结构的引用。
* update(x) 用字典x中的键/值对更新字典的内容。
* get(x[,y]) 返回键x。若未找到返回None
