# 第十章 DOM
## 10.1 节点层次
- 文档节点是每个文档的根节点；
- 文档元素是文档的最外层元素， 文档中的其他所有元素都包含在文档元素中，每个文档只能有一个文档元素。
- 在HTML页面中，文档元素始终都是<html>元素。在XML中，没有预定义的元素，所以任何元素都有可能成为文档元素。

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
  