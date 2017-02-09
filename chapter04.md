# 第四章 类及对象

  &#160; &#160; &#160; &#160;如果你熟悉java或者c#,那么对类和面向对象应该不会陌生。Python与c#一样，能够很好的支持面向对象的编程模式。
  
###类的定义

  &#160; &#160; &#160; &#160;与C#一样，Python使用class关键字定义一个类。一个最简单的类定义语句如下：
  ```
  Class A:
	Pass
  ```
  &#160; &#160; &#160; &#160;它等价于java中的class A{}.当然以上语句没有任何实际意义，它只是告诉我们什么是定义一个类所必需要的。即class关键字，类名和冒号，pass关键字只用来占位，相当于用来占位，相当于java中花括号的作用。
  
  &#160; &#160; &#160; &#160;类是定义对象格式的模板，而对象则是类的实例，通过类创建对象的过程称为类的实例化。在java中，需要使用new关键字实例化一个类，例如
```
A a=new A();
```

  &#160; &#160; &#160; &#160;在上条语句，java完成了两件事，首先声明一个类型为A的变量a,然后用new运算符创建一个类型为A的对象，并将该对象的引用赋值给变量a,而在python中没有new 关键字，同时它是一个动态语言，不需要事先指定变量的类型，只需要：
```
a=A()
```

即创建一个类型为A的对象，看起来好像是将类当作一个函数调用，返回值是新创建的对象。

###为类添加数据

  &#160; &#160; &#160; &#160;通常我们利用类来定义各种新的数据类型，其中即包含数据内容，也包含对数据内容的操作。Python类的数据添加方法与C#有一些不同，因为Python是一种动态语言，变量在使用之前不需要定 义，所以你可以不在类定义中添加成员变量，而是在运行时动态地添加它们，例如：

```
#-*-coding:utf-8-*-
import sys
def Main():
    class A:pass
    a=A()
    a.x=1
    print a.x
if __name__=="__main__":
    Main()
    
```
```
#-*-coding:utf-8-*-
import sys
def Main():
    class A:pass
    a=A()
    a.x=1
    print a.x
if __name__=="__main__":
    Main()
```

    
###构造函数
  &#160; &#160; &#160; &#160;Python的类提供了类似C#构造函数的东西：__init__(注意是前后是两个下划线)，类在实例化时会首先调用这个函数，我们可以通过重写__init__函数，完成变量的初始化等工作。与C#不同的地方是，Python不支持无参数的初始化函数，你至少需要为初始化函数指定一个参数，即对象实例本身(self).下面是一段简单的代码。在该代码中，我们重写了函数__init__，定义并初始化一个类的成员变量X：
  
```
#-*-coding:utf-8-*-
import sys
def Main():
    class A:
        def __init__(self):
            self.x=1
    a=A()
    print a.x
if __name__=="__main__":
    Main()
```
```
#-*-coding:utf-8-*-
import sys
class Student:
    def __init__(self,name,age):
        self.__name=name
        self.__age=age
    def getName(self):
        format="my name is %s my age is %d"%(self.__name,self.__age)
        print format
    def __del__(self):
        print "del"
if __name__=="__main__":
    student=Student("chu",35)
    student.getName()
```


###类的访问修饰符

  &#160; &#160; &#160; &#160;以前我们在使用C#或都java这一类语言时，经常使用public private之类的访问修饰符，但是在python中就大大的不一样了。请看以下二段代码的比较。

```
namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            A a = new A();
            Console.WriteLine(A.y);
            Console.WriteLine(a.x);
        }
    }
    class A
    {
        public static int y = 2;
        public int x;
        private int z;
        public A()
        {
            x = 1;
            z = 1;
        }
    }
}
```

```
#-*-coding:utf-8-*-
import sys
class A:
    #定义静态成员变量
    y=2
    def __init__(self):
        #定义公共的成员变量
        self.x=1
        #定义私有的成员变量
        self.__z=1
if __name__=="__main__":
    a=A()
    #打印公共的成员变量
    print a.x
    #打印静态成员变量
    print A.y
    #打印私有成员变量出错
    #print a.__z
```


    
###为类添加方法
  &#160; &#160; &#160; &#160;方法是对类数据内容的操作，在Python中，定义类的方法与定义一个普通的函数在语法上基本上相同，c#程序员需要注意的是，在类中定义的常规方法的第一个参数总是该类的实例，即self，同时注意在方法中引用类的另一个方法必须使用类名加方法名的形式，下面是一个定义类的方法的简单的例子。
  
```
#-*-coding:utf-8-*-
import sys
class A:
    def prt(self):
        print "my name is A"
    def reprt(self):
        A.prt(self)
if __name__=="__main__":
    a=A()
    a.prt()
    a.reprt()
```
    
不能定义一个不操作实例的方法

```
#-*-coding:utf-8-*-
import sys
class Student:
    __name=""
    def __init__(self,name):
        self.__name=name
    def getName(self):
        return self.__name
if __name__=="__main__":
    student=Student("chu")
    print student.getName()
```

###静态方法

  &#160; &#160; &#160; &#160;Python与C#一样支持静态方法。在C#中需要使用关键字static声明一个静态方法，而在Python中是通过静态方法修饰符@staticmethod来实现的，下面是例子：
  
  ```
  #-*-coding:utf-8-*-
import sys
class A:
    def prt(self):
        print "my name is A"
    def reprt(self):
        A.prt(self)
    @staticmethod
    def prt2():
        print "我是静态方法"
if __name__=="__main__":
    a=A()
    a.prt()
    a.reprt()
    A.prt2()
  ```

如你所见，静态方法可以直接被类调用，它没有常规方法那样的特殊行为（默认第一行参数是self等 ），你完全可以将静态方法当成一个用属性引用方式调用的普通函数。

###单继承

Python用类名后加扩号的方式实现继承，下面是一个简单的示例：

```
#-*-coding:utf-8-*-
import sys
class A:
    x=1
class B(A):
    y=2
if __name__=="__main__":
    print B.x
    print B.y

```

一个复杂的实例

```
#-*-coding:utf-8-*-
import sys
class SchoolMember:
    '''Represents any school member.'''
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print'(Initialized SchoolMember: %s)'% self.name

    def tell(self):
        '''Tell my details.'''
        print'Name:"%s" Age:"%s"'% (self.name, self.age),

class Teacher(SchoolMember):
    '''Represents a teacher.'''
    def __init__(self, name, age, salary):
        SchoolMember.__init__(self, name, age)
        self.salary = salary
        print'(Initialized Teacher: %s)'% self.name

    def tell(self):
        SchoolMember.tell(self)
        print'Salary: "%d"'% self.salary

class Student(SchoolMember):
    '''Represents a student.'''
    def __init__(self, name, age, marks):
        SchoolMember.__init__(self, name, age)
        self.marks = marks
        print'(Initialized Student: %s)'% self.name

    def tell(self):
        SchoolMember.tell(self)
        print'Marks: "%d"'% self.marks


if __name__=="__main__":
    t = Teacher('Mrs. Shrividya',40,30000)
    s = Student('Swaroop',22,75)
```
    
###传值与传引用

1. python不允许程序员选择采用传值还是传引用。Python参数传递采用的肯定是“传对象引用”的方式。实际上，这种方式相当于传值和传引用的一种综合。如果函数收到的是一个可变对象（比如字典或者列表）的引用，就能修改对象的原始值——相当于通过“传引用”来传递对象。如果函数收到的是一个不可变对象（比如数字、字符或者元组）的引用，就不能直接修改原始对象——相当于通过“传值'来传递对象。
2. 当人们复制列表或字典时，就复制了对象列表的引用同，如果改变引用的值，则修改了原始的参数。
3. 为了简化内存管理，Python通过引用计数机制实现自动垃圾回收功能，Python中的每个对象都有一个引用计数，用来计数该对象在不同场所分别被引用了多少次。每当引用一次Python对象，相应的引用计数就增1，每当消毁一次Python对象，则相应的引用就减1，只有当引用计数为零时，才真正从内存中删除Python对象。

```
#-*-coding:utf-8-*-
def add_list(p):
    p=p+[1]
def add_list2(p2):
    p2+=[1]
tmpList=[1,2,3,4]
add_list(tmpList)
print tmpList
#结果[1,2,3,4]
add_list2(tmpList)
print tmpList
#结果[1,2,3,4,1]
```
  &#160; &#160; &#160; &#160;这主要是由于“=”操作符会新建一个新的变量保存赋值结果，然后再把引用名指向“=”左边，即修改了原来的p引用，使p成为指向新赋值变量的引用。而+=不会，直接修改了原来p引用的内容，事实上+=和=在python内部使用了不同的实现函数。
  


