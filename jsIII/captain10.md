# 第十章 DOM
## 10.1 节点层次
- 文档节点是每个文档的根节点；
- 文档元素是文档的最外层元素， 文档中的其他所有元素都包含在文档元素中，每个文档只能有一个文档元素。
- 在HTML页面中，文档元素始终都是\<html\>元素。在XML中，没有预定义的元素，所以任何元素都有可能成为文档元素。

### 10.1.1 Node类型
- 每个节点都有一个nodeType属性，一共有12种(nodeType)
* Node.ELEMENT_NODE(1)  元素节点
* Node.ATTRIBUTE_NODE(2)  属性节点
* Node.TEXT_NODE(3)  文本节点
* Node.COMMENT_NODE(8)  注释节点
* Node.DOCUMENT_NODE(9)  文档节点
#### 1 nodeName和nodeValue
- 属性的名称(nodeName)和属性的值(nodeValue)
#### 2 节点的关系
- parentNode, 
- childNodes(nodeList动态的), firstChild, lastChild
- previousSibling, nextSibling
- 每个节点都有一个childNodes属性，其中保存着一个NodeList对象，NodeList是一个类数组
  - 访问方式：通过方括号访问(childNodes[0]) 或 通过item()方法访问(childNodes.item(0))
  - nodeList有一个length属性，保存子节点数
  - 与argument一样是一个类数组，可以通过Array.prototype.slice.call(someNode.childNode, 0)方法转换为数组
- hasChildNodes()检测是否有子节点
- ownerDocument属性指向整个文档的文档节点(根节点)
#### 3 操作方法 <a name='操作方法'></a>
- appendChild()
  - 如果传入的节点已经是文档中的一部分了，将会把该节点从原来位置转移到新位置
- insertBefore()
  - 2argument: 要插入的节点， 做为参照的节点
  - 如果参照节点是null，则与appendChild()执行相同的操作
- replaceChild()
  - 2argument: 要插入的节点， 要替换的节点
- removeChild()
#### 4 其他方法
- 所有类型节点都具有的 
1. cloneNode()
  - argument: 是否进行深复制的布尔值
  - 参数为true: 复制节点及整个子节点树；参数为false： 只复制节点本身
  - 复制后要通过<a href="#操作方法">操作方法</a>添加到文档树才能显示
2. normalize()
- 查找空文本节点删除，查找相邻文本节点合并

### 10.1.2 Document类型
- `document.constructor = f HTMLDocument {}`<br>document对象是HTMLDocument的一个实例，表示整个HTML页面
- nodeType: 9
- nodeName: '#document'
- nodeValue, parentNode, ownerDocument的值为null
#### 1 文档的子节点
- document.documentElement: 始终指向页面的\<html\>元素
- document.childNodes
- document.body
- document.head
- document.doctype 取得对于\<!DOCTYPE\>的引用(浏览器的支持不一致，用处有限)
#### 2 文档信息
- document.title  包含文本标题
- document.URL  包含页面的完整URL
- document.domain  包含页面域名
- document.referrer  包含链接到当前页面的URL，没有来源则返回空字符串
#### 3 查找元素
- getElementById()
  - 严格匹配，包括大小写
  - 不存在则返回null
  - 存在多个相同的id则返回第一个
- getElementsByTagName()
  - 返回一个nodeList。在HTML中返回的是一个HTMLCollection对象，是一个动态的集合
  - 访问方式：通过方括号访问(childNodes[0]) 或 通过item()方法访问(childNodes.item(0))
  - length
- getElementsByName()
#### 4 特殊集合
- document.anchors: 包含文档中所有带name特性的\<a\>元素
- document.form: 等于document.getElementsByTagName('form')
- document.images: 等于document.getElementsByTagName('img')
- document.links: 包含文档中所有带href特性的\<a\>元素
#### 5 文档写入
- write()、writeln()、open()、close()

### 10.1.3 Element类型
- nodeType: 1
- nodeName: 元素的标签名
- nodeValue: null
- 访问标签名可通过nodeName属性或tagName属性
#### 1 HTML元素
- 五个基本属性: id title lang dir className(calss是保留字，所以使用className)
#### 2 取得属性
- getAttribute()
  - 访问class： .className 或 getAttribute('class')  --属性访问和方法访问
  - 此方法中，括号内的特性(属性)的名称不区分大小写
  - 也可以取得自定义属性，在H5中自定义特性(属性)应该加上data-前缀
  - getAttribute('style')返回字符串；.style返回的是对象
#### 3 设置特性
- setAttribute()
  - 2argument: 要设置的特性名， 要设置的特性值
  - 如果特性已存在，则替换现有值
  - 通过此方法可以操作HTML特性和自定义特性，通过此方法设置的特性名会被统一转换为小写形式
- removeAttribute()
#### 4 创建元素
- document.createElement()
  - 该方法在HTML中不区分大小写，在XML中区分
  - 设置完成后需要通过<a href="#操作方法">操作方法</a>添加到文档树才能显示
#### 5 元素子节点
- elememt.childNodes

### 10.1.4 Text类型
- nodeType: 3
- nodeName: '#text'
- nodeValue: 节点所包含的文本
- 操作文本节点的方法
  - appendData(text)
  - deleteData(offset, count): 从offset指定的位置开始删除count个字符
  - insertData(offset, count)： 从offset指定的位置开始插入count个字符
  - replaceData(offset, count, text)
  - splitText(offset): 从 offset 指定的位置将当前文本节点分成两个文本节点
  - substringData(offset, count)：提取从offset指定的位置开始到offset+count为止处的字符串
- nodeValue可以修改文本节点
#### 1 创建文本节点
- document.createTextNode()
- normalize()<br>
  `var element = document.createElement("div");` <br>
  `element.className = "message"; `<br>
  `var textNode = document.createTextNode("Hello world!"); `<br>
  `element.appendChild(textNode); `<br>
  `var anotherTextNode = document.createTextNode("Yippee!"); `<br>
  `element.appendChild(anotherTextNode); `<br>
  `document.body.appendChild(element); `<br>
  `alert(element.childNodes.length); //2 `<br>
  `element.normalize(); `<br>
  `alert(element.childNodes.length); //1 `<br>
  `alert(element.firstChild.nodeValue); // "Hello world!Yippee!" `

