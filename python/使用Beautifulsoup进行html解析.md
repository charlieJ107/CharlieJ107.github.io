# 使用Beautifulsoup进行html解析

`beautifulsoup`是一个常用的html解析库, 这篇文章简单记录其使用方法

### beautifulsoup对象

先来看一个例子

```python
from urllib.request import urlopen
from bs4 import BeautifulSoup #注意区分大小写, 使用驼峰命名法
html = urlopen("http://www.pythonscraping.com/pages/page1.html")
bsObj = BeautifulSoup(html.read()) 
print(bsObj.h1)
```

`urlopen`返回一个对象, 这个对象就是url打开后的收到的东西, 使用`read`方法可以读出html的内容

此时将`html.read()`返回的html放进beautifulSoup对象

这个对象的解释如下

```python
class BeautifulSoup(markup="", features=None, builder=None, parse_only=None, from_encoding=None, exclude_encodings=None, element_classes=None)
```

> A data structure representing a parsed HTML or XML document.
>
> Most of the methods you'll call on a BeautifulSoup object are inherited from PageElement or Tag.
>
> Internally, this class defines the basic interface called by the tree builders when converting an HTML/XML document into a data structure. The interface abstracts away the differences between parsers. To write a new tree builder, you'll need to understand these methods as a whole.
>
> These methods will be called by the BeautifulSoup constructor:
>
>   * reset()  
>   * feed(markup)  
> The tree builder may call these methods from its feed() implementation:
>
>   * handle_starttag(name, attrs) # See note about return value  
>   * handle_endtag(name)  
>   * handle_data(data) # Appends to the current data node  
>   * endData(containerClass) # Ends the current data node  
> No matter how complicated the underlying parser is, you should be able to build a tree using 'start tag' events, 'end tag' events, 'data' events, and "done with data" events.
>
> If you encounter an empty-element tag (aka a self-closing tag, like HTML's <br> tag), call handle_starttag and then handle_endtag.****

构造函数传进去的必要参数就是html的文本内容. 据此盲猜`urlopen.read()`返回的也是文本内容

所以创建一个bs4对象的代码

```python
bsObj=bs4.BeautifulSoup(html.read())
```

### 两个重要函数

这两个重要函数分别是`find()`和`findAll()`

```python
findAll(tag, attributes, recursive, text, limit, keywords)
find(tag, attributes, recursive, text, keywords)
#attributes 属性
```

如果`recursive`参数设置为`true`findAll 就会根据你的要求去查找标签参数的所有子标签，以及子 标签的子标签。如果 recursive 设置为 False，findAll 就只查找文档的一级标签。findAll 默认是支持递归查找的（recursive 默认值是 True）；

这两个