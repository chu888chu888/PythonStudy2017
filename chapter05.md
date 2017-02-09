# 第五章 模块与包


  &#160; &#160; &#160; &#160;Python的脚本都是用扩展名为py的文本文件保存的，一个脚本可以单独运行，也可以导入另一个脚本中运行。当脚本被导入运行时，我们将其称为模块（module）。模块是Python组织代码的基本方式。
  
  &#160; &#160; &#160; &#160;Python的程序是由包（package）、模块（module）和函数组成.包是由一系列模块组成的集合。模块是处理某一类问题的函数和类的集合。
  
  &#160; &#160; &#160; &#160;包就是一个完成特定任务的工具箱，Python提供了许多有用的工具包，如字符串处理、图形用户接口、WEB接口、图形图像处理等。使用这些工具包，可以提高程序员的开发效率、减少编程的复杂度、达到代码重用的效果。这些自带的工具包和模块安装在Python的安装目录下的Lib子目录中。

  &#160; &#160; &#160; &#160;例如，Lib目录中的xml 文件夹就是一个包，这个包用于完成XML的应用开发。Xml包中有几个子包：dom、sax、etree和parser。文件__init__.py（注意是两个下滑线）是xml包的注册文件，如果没有该文件，Python将不能识别xml包。在系统字典中定义了xml包。
  
  &#160; &#160; &#160; &#160;包必须至少含有一个__init__.py文件，该文件的内容可以为空。__init__.py用于表示当前文件夹是一个包。
  
###对于模块的理解
  &#160; &#160; &#160; &#160;用简单的说法来说，每一个以扩展名为.py结尾的Python源代码都是一个模块。其他的文件可以通过导入一个模块读取这个模块的内容。导入从本质上来讲，就是载入另一个文件，并能够读取那个文件的内容。一个模块的内容通过这样的的属性能够被外部世界使用。
  
**比如我们举一个简单的例子，首先建立一个python文件define.py**
```
#-*-coding:utf-8-*-
myvar="这是一个测试"
```
**很简单的代码就二行，我们定义了一个变量myvar.现在我们通过另一个python文件来导入它。**

```
#-*-coding:utf-8-*-
import sys
import define
def Main():
    print define.myvar
    print dir(define)
    print define.__file__
if __name__=="__main__":
    Main()
```

```
import define #这一行语句的意义在于导入define.py这个模块

print define.myvar#这一行的意义在于打印myvar这个变量

print dir(define)#这一行的意义在于输出所有可以使用的变量
```


  &#160; &#160; &#160; &#160;输出结果，不言而喻。但是在默认情况下，只是在每次会话的第一次运行。在第一次导入之后，其他的导入都不会再工作。
  
  &#160; &#160; &#160; &#160;但是如果真的想要python在同一次会话中再次运行文件（不停止和重新启动会话），需要调用内置的reload函数。
  
###模块的显要特性：属性

  &#160; &#160; &#160; &#160;导入和重载提供了一种自然的程序启动的选择，因为导入操作将会在最后一步执行文件。从更宏观的角度来看，模块扮演了一个工具库的角色。我们可以直接使用from define import myvar这条语句来实现。
  
```
#-*-coding:utf-8-*-
import sys
from define import myvar
def Main():
    print myvar
if __name__=="__main__":
    Main()
```

###模块创建过程的例子

  &#160; &#160; &#160; &#160;模板把一组相关的函数或代码组织到一个文件中。一个文件即是一个模板。模块由代码、函数或类组成。例如，创建一个名为myModule.py的文件，即定义了一个名为myModule的模块。在该模块中定义一个函数func()和一个类MyClass。MyClass类中定义一个方法myFunc().
  
```
#-*-coding:utf-8-*-
import sys
def func():
    print "myModule.func()"
class MyClass:
    def myFunc(self):
        print "myModule.MyClass.myFunc()"
```
        
然后在myModule.py所在目录下创建一个名为call_myModule.py文件，在该文件中调用myModule模块的函数和类：

```
#-*-coding:utf-8-*-
import sys
import random
import myModule
if __name__=="__main__":
    myModule.func()
    myClass=myModule.MyClass()
    myClass.myFunc()
```

当python寻入一个模块时，python首先查找当前路径，然后查找lib目录、site-packages目录(python/lib/site-packages)和环境变量PYTHONPATH设置的目录。

###模块的导入
在使用一个模块中的函数或类之前，首先要导入该模块。

```
import myModule
```

还可以使用from …import..语句将模块导入。
```
from module_name import *
from module_name import function_name
```

**实现例子**

```
#-*-coding:utf-8-*-
import sys
def func():
    print "myModule.func()"
class MyClass:
    def myFunc(self):
        print "myModule.MyClass.myFunc()"

#-*-coding:utf-8-*-
import sys
import random
from myModule import func
if __name__=="__main__":
    func()
```

###模块的属性
模块中有许多内置的属性，用于完成特定的任务，如__name__ __doc___。每个模块都有一个名称。

```
#-*-coding:utf-8-*-
import sys
if __name__=="__main__":
    print __name__
    print __doc__
    print __file__
    print __package__
```
