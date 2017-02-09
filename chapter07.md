# 第七章 文件IO


##基本文件功能演示

```
#-*-coding:utf-8-*-
import sys
import re
if __name__=="__main__":
    #创建文件
    context='''hello world
    hello china '''
    f=file('hello.txt','w')
    f.write(context)
    f.close()
```
    
```
#-*-coding:utf-8-*-
import sys
import re
if __name__=="__main__":
    #读取文件
    f=open("hello.txt")
    while True:
        line=f.readline()
        if line:
            print line
        else:
            break
    f.close()
```

```
#-*-coding:utf-8-*-
import sys
import re
if __name__=="__main__":
    #使用readlnes()读取多个文件
    f=file("hello.txt")
    lines=f.readlines()
    print lines
    for line in lines:
        print line
```

```
#-*-coding:utf-8-*-
import sys
import re
if __name__=="__main__":
    #一次性读取
    f=open("hello.txt")
    context=f.read()
    print context
```


```
#-*-coding:utf-8-*-
import sys
import re
if __name__=="__main__":
    f=open("hello.txt")
    context=f.read(5)
    print context #读取前5个字节的数据
    print f.tell()#显示当前的位置
    context=f.read(5)
    print context
    print f.tell()
    f.close()
```


##文件的写入

```
#-*-coding:utf-8-*-
import sys
import re
if __name__=="__main__":
    #使用writelines()写文件
    f=file("hello.txt","w+")
    li=["hello chu888\n","hello li\n"]
    f.writelines(li)
    f.close()
```

```
#-*-coding:utf-8-*-
import sys
import re
if __name__=="__main__":
    #使用writelines()写文件
    f=file("hello.txt","w+")
    li=["hello chu888楚\n","hello li\n"]
    f.writelines(li)
    f.close()
    #追加文件内容
    f=file("hello.txt","a+")
    new_context="goodbye"
    f.write(new_context)
    f.close()
```


##文件的删除与复制

```
#-*-coding:utf-8-*-
import sys
import re
import os
if __name__=="__main__":
    file("hello.txt","w")
    if os.path.exists("hello.txt"):
        os.remove("hello.txt")
```

file类没有提供文件拷贝的功能，但是我们可以使用read()、write()方法模拟实现文件的拷贝，但是最好的方法是引入shutil模块

```
#-*-coding:utf-8-*-
import sys
import re
import os
import shutil
if __name__=="__main__":
    shutil.copyfile("a.txt","hello2.txt")
    shutil.move("a.txt","../")
    shutil.move("hello2.txt","aaa.txt")
```

##文件与目录的重命名

os模块的函数rename()可以对文件或目录进行重命名
演示文件重命名的操作。如果当前目录存在名为hello.txt的文件，则重命名为hi.txt;如果存在hi.txt的文件则重命名为hello.txt

```
#-*-coding:utf-8-*-
import sys
import os
if __name__=="__main__":
    li=os.listdir(".")#判断当前目录
    print li
    if "hello.txt" in li:
        os.rename("hello.txt","hi.txt")
    elif "hi.txt" in li:
        os.rename("hi.txt","hello.txt")
```

把后缀名为”html”的文件修改为”htm”后缀的文件

```
#-*-coding:utf-8-*-
import sys
import os
if __name__=="__main__":
    files=os.listdir(".")
    for filename in files:
        #查找文件名中.所在的位置并把它给pos
        pos=filename.find(".")
        #print pos
        #得到.后面的内容
        if filename[pos+1:]=="html":
            print filename
            newname=filename[:pos+1]+"htm"
            print newname
            os.rename(filename,newname)
```

```
#-*-coding:utf-8-*-
import sys
import os
if __name__=="__main__":
    files=os.listdir(".")
    for filename in files:
        li=os.path.splitext(filename)
        if li[1]==".html":
            newname=li[0]+".htm"
            os.rename(filename,newname)
```

##文件内容的查找和替换

从文件中查找字符串hello，并统计hello出现的次数

```
#-*-coding:utf-8-*-
import sys
import os
import re
if __name__=="__main__":
    fl=file("aaa.txt","r")
    count=0
    for s in fl.readlines():
        li=re.findall("hello",s)
        if len(li)>0:
            count=count+li.count("hello")
    print "查找到"+str(count)+"个hello"
    fl.close()
```

把hello.txt中的字符串hello全部替换为hi，并把结果保存在文件hello2.txt中

```
#-*-coding:utf-8-*-
import sys
import os
import re
if __name__=="__main__":
    f1=file("aaa.txt","r")
    f2=file("bbb.txt","w")
    for s in f1.readlines():
        f2.write(s.replace("hello","hi"))
    f1.close()
    f2.close()
```
    
##文件的比较

Python提供了模块difflib用于实现对序列、文件的比较。如果要比较两个文件，列出两个文件的异同，可以使用difflib模块的SequenceMatcher类实现。其中的方法get_opcodes()可以返回两个序列的比较结果。调用方法get_opcodes()之前，需要生成1个SequenceMatcher对象。


##控制台输入

raw_input控制台输入

```
#-*-coding:utf-8-*-
import os
myname = raw_input("please enter you name:")
print myname
```

getpass.getpass方法

```
#-*-coding:utf-8-*-
import os
import getpass
myname = raw_input("please enter you name:")
print myname
#输入密码安全
pwd = getpass.getpass('password: ')
print pwd
```