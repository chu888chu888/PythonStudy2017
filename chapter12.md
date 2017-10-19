# 第十一章 Django

##安装Django
在安装pip工具的python之后，可以直接通过pip install 命令安装django:

```
#pip install django
```
该命令将自动下载Django安装包并安装。安装完成后可以进入Python,通过如下命令验证是否安装成功：

```
#python
>>> import django
>>> print django.VERSION
```

##创建第一个Django Hello World

在进行Django开发之前需要先用django-admin建立Django项目，语法如下：

```
#django-admin startproject djangodemo
```

该命令在当前目录中建立了一个子目录djangodemo,并在其中生成了Django开发默认文件，djangodemo的目录内容如下：

![](images/chapter12/00001.png)

默认生成的几个文件都非常重要，在今后的开发中一直使用或者维护他们：

1. manage.py 是Django用于管理本项目的命令行工具，之后进行站点运行、数据库自动生成、静态文件收集等都要通过该文件完成
2. settings.py Django的项目配置文件。默认时，在其中定义了本项目引用的Django组件、Django项目名等。在之后的开发中，还需在其中配置数据库参数、导入的其他python包信息.
3. urls.py 维护项目的URL路由映射，即定义客户端访问的URL由哪一个Python模块解析并提供反馈。在默认情况下，其中只定义了/admin即管理员站点的解析器
4. wsgi.py定义WSGI的接口信息，用于与其他web接口信息

### 建立应用
我们需要在项目中建立Django应用每个Django项目可以包含多个Django应用。建立应用的语法如下：

```
#python manage.py startapp app
```

命令完成后会在项目中建立如下目录及文件结构：

![](images/chapter12/00002.png)


### 基本视图与路由

1. 首先在app/views.py中建立一个路由相应函数
  该代码定义了一个函数welcome()，简单的返回一条被HttpResponse封装的Welcome信息
```
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

from django.shortcuts import render

# Create your views here.

from django.http import HttpResponse

def welcome(request):
    return HttpResponse("<h1>欢迎使用django</h1>")

```

2. 接下来，要通过URL映射将用户的HTTP访问与该函数绑定起来

```
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'', views.welcome)
]
```
在其中的第一行引入了django.conf.urls中的url()函数，Django中所有路由映射由该函数生成。
第二行引入djangodemo/app/views.py模块。之后定义了关键变量urlpatterns.该变量是一个列表，保存所有由url函数生成的路由映射。


3. 在项目URL文件djangodemo/urls.py的urlpatterns中增加一项，声明对应app中的urls.py文件的引用，代码如下：

```
from django.conf.urls import url
from django.contrib import admin
from django.conf.urls import include
urlpatterns = [
    url(r'^app/', include('app.urls')),
    url(r'^admin/', admin.site.urls),
]
```
首先通过import语句引入django.conf.urls.include()函数，之后在urlpatterns列表中增加一个路径app/,将其转换到app.urls,这样，通过include函数就将两个urlpatterns连接起来了。

### 运行
通过以上配置和编码过程，我们可以开发启动项目了。

```
#cd djangodemo
#python manage.py runserver 0.0.0.0:8001

```

###urlretrieve方法的使用

**urllib.urlretrieve(url[, filename[, reporthook[, data]]])：**

filename指定保存到本地的路径（若未指定该，urllib生成一个临时文件保存数据）
reporthook回调函数，当连接上服务器、以及相应的数据块传输完毕的时候会触发该回调

###data指post到服务器的数据

**urllib.urlretrieve(url[,filename[,reporthook[,date]]]) **

此函数将远程的数据下载到本地，其中参数url是URL字符串，filename指定数据保存到本地的路径；reporthook(block,size,total)是一个回调函数当链接上服务器，以及相应的数据传送完毕时会触发该函数（即每下载一块(block)就调用一次回调函数），我们可以用该函数来显示当前数据下载的进度，也可以用来限速，date是指post到服务器的数据；该方法返回一个包含两个元素的元组(filename, headers)，filename表示保存到本地的路径，header表示服务器的响应头。

```
from __future__ import unicode_literals
import urllib
import re
def  callback_f(downloaded_size, block_size, romote_total_size): 
  per = 100.0 * downloaded_size * block_size / romote_total_size 
  if per > 100: 
    per = 100  
  print"%.2f%%"% per 
def getHtml(url):
    page=urllib.urlopen(url)
    html=page.read()
    page.close()
    return html
def getImg(html):
    imgre=re.compile(r"""<img\s.*?\s?src\s*=\s*['|"]?([^\s'"]+).*?>""",re.I)
    imglist=imgre.findall(html)
    i=0
    for imgurl in imglist:
        if not imgurl.find("http://"):
            urllib.urlretrieve(imgurl,"img/%d.jpg"%(i),callback_f)
            i+=1
            print imgurl
ht=getHtml(r"http://www.cnbeta.com/articles/234303.htm")
getImg(ht)
```



###url编码

1. urllib.quote(str[，safe]) 对字符串进行编码，而参数safe指定不需要编码的字符；
2. urllib.unquote(str) 对字符串进行解码；
3. urllib.quote_plus(str[,safe]) 和quote类似,只是把参数str中的空格转化成“+” 而quote是把
  空格转化成“%20”
4. urllib.unquote_plus(str) 对字符串进行解码；
5. urllib.urlencode(query[,dosep]) 参数query可以是两个元素的元组也可以是一个字,将其转成url；
6. urllib.url2pathname(path) 将url路径转化成本地路径；
7. urllib.pathname2url 将本地路径转化成url路径；

```
#coding:utf-8
import urllib
date="whoiam=i am student+i like python"
#对字符串编码
date1=urllib.quote(date)
print date1
#对字符串编码
print urllib.unquote(date1)
print urllib.unquote_plus(date1)
#将参数试点转成url
date5=urllib.urlencode({"name":"python","love":"python"})
print date5
```


###使用httplib抓取

httplib.HTTPConnection ( host [ , port [ ,strict [ , timeout ]]] )
host表示服务器主机
port为端口号，默认值为80
strict的 默认值为false， 表示在无法解析服务器返回的状态行时(status line) （比较典型的状态行如： HTTP/1.0 200 OK ），是否抛BadStatusLine 异常
可选参数timeout 表示超时时间。

HTTPConnection提供的方法：
- HTTPConnection.request ( method , url [ ,body [ , headers ]] )
  调用request 方法会向服务器发送一次请求
  method 表示请求的方法，常用有方法有get 和post ；
  url 表示请求的资源的url ；
  body 表示提交到服务器的数据，必须是字符串（如果method是”post”，则可以把body 理解为html 表单中的数据）；
  headers 表示请求的http 头。

- HTTPConnection.getresponse ()
  获取Http 响应。返回的对象是HTTPResponse 的实例，关于HTTPResponse 在下面会讲解。

- HTTPConnection.connect ()
  连接到Http 服务器。

- HTTPConnection.close ()
  关闭与服务器的连接。

- HTTPConnection.set_debuglevel ( level )
  设置高度的级别。参数level 的默认值为0 ，表示不输出任何调试信息。

httplib.HTTPResponse
-HTTPResponse表示服务器对客户端请求的响应。往往通过调用HTTPConnection.getresponse()来创建，它有如下方法和属性：
-HTTPResponse.read([amt])
获取响应的消息体。如果请求的是一个普通的网页，那么该方法返回的是页面的html。可选参数amt表示从响应流中读取指定字节的数据。
-HTTPResponse.getheader(name[, default])
获取响应头。Name表示头域(header field)名，可选参数default在头域名不存在的情况下作为默认值返回。

-HTTPResponse.getheaders()
以列表的形式返回所有的头信息。

-HTTPResponse.msg
获取所有的响应头信息。

-HTTPResponse.version
获取服务器所使用的http协议版本。11表示http/1.1；10表示http/1.0。

-HTTPResponse.status
获取响应的状态码。如：200表示请求成功。

-HTTPResponse.reason
返回服务器处理请求的结果说明。一般为”OK”

```
#!/usr/bin/python
# -*- coding:utf-8 -*-


def use_httplib():
    import httplib
    conn = httplib.HTTPConnection("www.baidu.com")
    i_headers = {"User-Agent":
                 "Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.9.1) Gecko/20090624 Firefox/3.5",
                 "Accept": "text/plain"}
    conn.request("GET", "/", headers=i_headers)
    r1 = conn.getresponse()
    print"version:", r1.version
    print "------------------------"
    print"reason:", r1.reason
    print "------------------------"
    print"status:", r1.status
    print "------------------------"
    print"msg:", r1.msg
    print "------------------------"
    print"headers:", r1.getheaders()
    print "------------------------"
    data = r1.read()
    print data.decode("utf-8")
    print "------------------------"
    print "data length:%s"%len(data)
    conn.close()

if __name__ == "__main__":
    use_httplib()
```

##最简单的爬虫

网络爬虫是一个自动提取网页的程序，它为搜索引擎从万维网上下载网页，是搜索引擎的重要组成。python的urllib\urllib2等模块很容易实现这一功能，下面的例子实现的是对baidu首页的下载。具体代码如下：

```
import urllib2
page=urllib2.urlopen("http://www.baidu.com")
print page.read().decode('utf-8')
```

###用GET方法提交数据
提交表单的GET方法是把表单数据编码至URL。在给出请示的页面后，加上问号，接着是表单的元素。
如在百度中搜索“马伊琍”得到url为：

**http://www.baidu.com/s?wd=%E9%A9%AC%E4%BC%8A%E7%90%8D&pn=100&rn=20&ie=utf-8&usm=4&rsv_page=1**

其中？后面为表单元素。wd=%E9%A9%AC%E4%BC%8A%E7%90%8D表示搜索的词是“马伊琍”，pn表示从第100条信息所在页开始显示（感觉是这样，我试了几次，当写100时，从其所在页显示，但如果写10，就是从第1页显示），rn=20表示每页显示20条，ie=utf-8表示编码格式，usm=4没明白是什么意思，换了1、2、3试了下，没发现什么变化，rsv_page=1表示第几页。如果要下载以上页面比较简单的方法是直接用上面的网址进行提取。如代码：

```
#coding:utf-8
import urllib2
keyword=urllib2.quote('马伊琍')
page=urllib2.urlopen("http://www.baidu.com/s?wd="+keyword+"&pn=100&rn=20&ie=utf-8&usm=4&rsv_page=1")
print page.read()
```

##Html的解析
在python中能够进行html和xhtml的库有很多，如HTMLParser、sgmllib、htmllib、BeautifulSoup、mxTidy、uTidylib等，这里介绍一下HTMLParser、BeautifulSoup等模块。

###BeautifulSoup进行解析

一段最简单的程序

```
#coding:utf-8
import urllib2
from BeautifulSoup import BeautifulSoup

page = urllib2.urlopen('http://www.baidu.com');

soup = BeautifulSoup(page)
#打印页面的编码
print soup.originalEncoding
#打印规范化的html
print soup.prettify().decode('utf-8')

```
```
#抓取网页图片并下载
#coding:utf-8
import urllib2
import urllib
import uuid
from BeautifulSoup import BeautifulSoup
def  callback_f(downloaded_size, block_size, romote_total_size):
  per = 100.0 * downloaded_size * block_size / romote_total_size
  if per > 100:
    per = 100
  print"%.2f%%"% per


page = urllib2.urlopen('http://dianying.fm/');
soup = BeautifulSoup(page)
#打印页面的编码
print soup.originalEncoding
#打印规范化的html
print soup.prettify().decode('utf-8')
#打印title
titleTag=soup.html.head.title
print titleTag.string
#提取图片在本地目录
links=soup.findAll('img')
for i in links:
    if str(i['src'])!='':
        print str(i).decode('utf-8')
        #print i['src']
        urllib.urlretrieve(str(i['src']),"img/%s.jpg"%(uuid.uuid1()),callback_f)

```

###使用PyQuery来进行XML与Html的解析

在写PyQuery之前我一直都是使用BeautifulSoup来进行XML与Html的操作的，偶然的一个机会让我见到了PyQuery之后，真是非常喜爱，原因很简单PyQuery采用CSS选择器的方法来进行DOM元素操作，Jquery的技能可以有效继承过来。

PyQuery允许你使用jquery的方法来查询xml与html文件，它的API结构非常的接近jquery。PyQuery在内部使用lxml来操作xml与html所以速度是有保障的。

这是一个开源的项目，现在托管在Github上，大家可以自行查询到。

####快速入门

你可以使用PyQuery封装类从一个字符串、一个lxml文档或者是一个文件还或者是一个url地址，反正来源地址可以非常丰富。

```
#coding:utf-8
from pyquery import PyQuery as pq
from lxml import etree
import urllib
d = pq("<html></html>")
d = pq(etree.fromstring("<html></html>"))
d = pq(url='http://google.com/')
# d = pq(url='http://google.com/', opener=lambda url, **kw: urllib.urlopen(url).read())
#path_to_html_file='c:\\test.html'
#d = pq(filename=path_to_html_file)
```

```
#coding:utf-8
from pyquery import PyQuery as pq
from lxml import etree
import urllib
d = pq("<html></html>")
d = pq(etree.fromstring("<html></html>"))
d = pq(url='http://2.myrestful.sinaapp.com/')
# d = pq(url='http://google.com/', opener=lambda url, **kw: urllib.urlopen(url).read())
#path_to_html_file='c:\\test.html'
#d = pq(filename=path_to_html_file)
print d("#downloads")
print '-----------'
p=d("#downloads")
#打印html
print p.html()
#打印text
print p.text()
2.	元素操作
#coding:utf-8
from pyquery import PyQuery as pq
from lxml import etree
import urllib
p=pq('<p id="hello" class="hello"></p>')
print p.attr("id")
p.attr("id","plop")
print p.attr("id")
p.css("font-size","15px")
print p.attr("style")

#coding:utf-8
from pyquery import PyQuery as pq
from lxml import etree
import urllib

htmlsource=pq(url='http://www.baidu.com')
f=file('out.html','w')
f.write(htmlsource.html().encode('utf-8'))
f.close()
3.	其他操作
# coding:utf-8
from pyquery import PyQuery as pq
from lxml import etree
import urllib
p=pq("<head><title>hello</title></head>")
p('head').html()#返回<title>hello</title>
p('head').text()#返回hello

d=pq('<div><p>test 1</p><p>test 2</p></div>')
d('p')#返回[<p>,<p>]
print d('p')#返回<p>test 1</p><p>test 2</p>
print d('p').html()#返回test 1

print d('p').eq(1).html() #返回test 2
#filter() ——根据类名、id名得到指定元素
d=pq("<div><p id='1'>test 1</p><p class='2'>test 2</p></div>")
d('p').filter('#1') #返回[<p#1>]
d('p').filter('.2') #返回[<p.2>]
#find() ——查找嵌套元素
d=pq("<div><p id='1'>test 1</p><p class='2'>test 2</p></div>")
d('div').find('p')#返回[<p#1>, <p.2>]
d('div').find('p').eq(0)#返回[<p#1>]
#直接查找ID或者类名
d=pq("<div><p id='1'>test 1</p><p class='2'>test 2</p></div>")
d('#1').html()#返回test 1
d('.2').html()#返回test 2
#获取属性与修改属性
d=pq("<p id='my_id'><a href='http://hello.com'>hello</a></p>")
d('a').attr('href')#返回http://hello.com
d('p').attr('id')#返回my_id
d('a').attr('href', 'http://baidu.com')
#addClass(value) ——为元素添加类
d=pq('<div></div>')
d.addClass('my_class')#返回[<div.my_class>]
#hasClass(name) #返回判断元素是否包含给定的类
d=pq("<div class='my_class'></div>")
d.hasClass('my_class')#返回True
#children(selector=None) ——获取子元素
d=pq("<span><p id='1'>hello</p><p id='2'>world</p></span>")
d.children()#返回[<p#1>, <p#2>]
d.children('#2')#返回[<p#2>]
#parents(selector=None)——获取父元素
d=pq("<span><p id='1'>hello</p><p id='2'>world</p></span>")
d('p').parents()#返回[<span>]
d('#1').parents('span')#返回[<span>]
d('#1').parents('p')#返回[]
#nextAll(selector=None) ——返回后面全部的元素块
d=pq("<p id='1'>hello</p><p id='2'>world</p><img scr='' />")
d('p:first').nextAll()#返回[<p#2>, <img>]
d('p:last').nextAll()#返回[<img>]
#not_(selector) ——返回不匹配选择器的元素
d=pq("<p id='1'>test 1</p><p id='2'>test 2</p>")
d('p').not_('#2')#返回[<p#1>]


```