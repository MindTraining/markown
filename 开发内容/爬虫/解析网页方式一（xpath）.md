# 网页的解析（xpath）

（对整个html比较熟的时候使用）

## xpath的解释

> **XPath**即为[XML](https://link.zhihu.com/?target=https%3A//zh.wikipedia.org/wiki/XML)路径语言（XML Path Language），它是一种用来确定XML文档中某部分位置的语言。
> XPath基于XML的树状结构，提供在数据结构树中找寻节点的能力。起初XPath的提出的初衷是将其作为一个通用的、介于[XPointer](https://link.zhihu.com/?target=https%3A//zh.wikipedia.org/w/index.php%3Ftitle%3DXPointer%26action%3Dedit%26redlink%3D1)与[XSL](https://link.zhihu.com/?target=https%3A//zh.wikipedia.org/wiki/XSL)间的语法模型。但是XPath很快的被开发者采用来当作小型[查询语言](https://link.zhihu.com/?target=https%3A//zh.wikipedia.org/wiki/%E6%9F%A5%E8%A9%A2%E8%AA%9E%E8%A8%80)。



## XPath的基本使用

要使用xpath需要下载lxml

```python
from lxml import etree
# 定义一个函数，给他一个html，返回xml结构
def getxpath(html):
    return etree.HTML(html)
# 下面是我们实战的第一个html
sample1 = """<html>
  <head>
    <title>My page</title>
  </head>
  <body>
    <h2>Welcome to my <a href="#" src="x">page</a></h2>
    <p>This is the first paragraph.</p>
    <!-- this is the end -->
  </body>
</html>
"""
# 获取xml结构
s1 = getxpath(sample1)

# 获取标题(两种方法都可以)
#有同学在评论区指出我这边相对路径和绝对路径有问题，我搜索了下
#发现定义如下图
s1.xpath('//title/text()')
s1.xpath('/html/head/title/text()')
```

相对路径是相对于整个文件的位置 ，使用相对路径一定要加//



## 总结及注意事项

- 获取文本内容用 text()

- 获取注释用 comment()

- 获取其它任何属性用@xx，如

- - @href                                         ` href 标签的 href 属性用于指定超链接目标的 URL`
  - @src                                           ` src 属性规定在框架中显示的文档的 URL。`
  - @value                                       `value 属性规定在表单被提交时被发送到服务器的值。`

```python
sample2 = """
<html>
  <body>
    <ul>
      <li>Quote 1</li>
      <li>Quote 2 with <a href="...">link</a></li>
      <li>Quote 3 with <a href="...">another link</a></li>
      <li><h2>Quote 4 title</h2> ...</li>
    </ul>
  </body>
</html>
"""
s2 = getxpath(sample2)
```

![preview](https://pic1.zhimg.com/v2-2cc49f0ee328e4ea66e40bd775db851c_r.jpg)

## 总结及注意事项

- 上面的li 可以更换为任何标签，如 p、div
- **位置默认以1开始的**
- 最后一个用 **li[last()]** 不能用 **li[-1]**
- **这个一般在抓取网页的下一页，最后一页会用到**

## 总结及注意事项

- 根据html的属性或者文本直接定位到当前标签

- 文本是 text()='xxx'

- 其它属性是@xx='xxx'

- 这个是我们用到最多的，如抓取知乎的xsrf(见下图)

- - 我们只要用如下代码就可以了//input[@name="_xsrf"]/@value

![img](https://pic4.zhimg.com/80/v2-0b39f4300006926adcdfe113a4fedd6f_720w.jpg)

```python
sample4 = u"""
<html>
  <head>
    <title>My page</title>
  </head>
  <body>
    <h2>Welcome to my <a href="#" src="x">page</a></h2>
    <p>This is the first paragraph.</p>
    <p class="test">
    编程语言<a href="#">python</a>
    <img src="#" alt="test"/>javascript
    <a href="#"><strong>C#</strong>JAVA</a>
    </p>
    <p class="content-a">a</p>
    <p class="content-b">b</p>
    <p class="content-c">c</p>
    <p class="content-d">d</p>
    <p class="econtent-e">e</p>
    <p class="heh">f</p>
    <!-- this is the end -->
  </body>
</html>
"""
s4 = etree.HTML(sample4)
```

![img](https://pic2.zhimg.com/80/v2-0b0bfc85cf04adefd1a05cf01721a8c9_720w.jpg)

## 总结及注意事项

- 想要获取某个标签下所有的文本（包括子标签下的文本），使用string

- - 如 <p>123<a>来获取我啊</a></p>，这边如果想要得到的文本为"123来获取我啊"，则需要使用string



- starts-with 匹配字符串前面相等
- contains 匹配任何位置相等
- 当然其中的(@class,"content")也可以根据需要改成(text(),"content")或者其它属性(@src,"content")

  