# 第八章 BOM

## 8.1 window 对象
- BOM的核心对象是window，它表示浏览器的一个实例。在浏览器中，window对象有双重角色，它既是通过JavaScript访问浏览器窗口的一个接口，又是ECMAScript规定的Global对象

### 8.1.1 全局作用域
- 全局作用域声明的变量、函数都会成为window对象的属性和方法
- 全局变量无法通过delete删除，window的属性可以，这是由于全局变量的[Configurable]属性为false
- 访问未声明的全局变量会抛出错误，但是通过属性查询的时候则返回undefined

### 8.1.2 窗口关系及框架
- window.top() 指向最高层(最外层)的框架，也就是浏览器窗口
- window.parent() 指向当前框架的直接上层框架

### 8.1.3 窗口位置
- IE Safari Opera Chorme: 
  - window.screenLeft、 window.screenTop
- Firefox
  - window.screenX、 window.screenY
- 兼容写法
  - `var leftPos = (typeof(window.screenLeft == 'number')?window.screenLeft:window.screenX)`
- 被禁用的
  - moveTo(), moveBy()

### 8.1.4 窗口大小
- viewport
  - document.documentElement.clientWidth
  - document.documentElement.clientHeight
  - 被禁用的
    - resizeTo(), resizeBy()

### 8.1.5 导航和打开窗口
- 其他打开窗口的方法
  - \<a href=url\>
  - window.location/window.location.href = url
  - location.assign(url)
- window.open(URL, name, features, replace)
  - URL: 要加载的URL
  - name: 窗口目标
    - a.target
    - _self, _parent, _top, _blank
  - features: 弹出窗口的特性(height, width, top, left)
  - replace: 表示新页面是否取代浏览器历史记录中当前加载页面的布尔值

### 8.1.6 间歇调用和超时调用
- 间歇调用：setInterval()
- 超时调用：setTimeout()

### 8.1.6 系统对话框
- alter()
- confirm()
- prompt()
  - 2argument: 要显示给用户的文本提示, 文本输入域的默认值（可以是一个空字符串）

## 8.2 location 对象
- location即是window对象，也是document对象，window.location和document.location引用的是同一个对象
- location.href: 完整的URL
- location.host: 服务器名称和端口号(如果有)
- location.hash: URL中的hash值(#号后)
- location.search: URL查询的字符串(?号后)
- location.host.name: 不含端口号的服务器名称(域名)
- location.pathname: URL中的目录和文件名
- location.port: 端口号
- location.protocol: 协议名

### 8.2.1 位置操作
- location.assign() 调用location.href/window.location也是调用这个方法
- location.href/window.location\
- location.replace(): 不会在历史记录中出现原来页面的记录，所以无法退回(后退处于禁用状态)
- location.reload(): 
  - location.reload() 重新加载(可能从缓存中加载)
  - location.reload(true) 重新加载(强制从服务器中加载)

## 8.3 navigator 对象
- 识别客户端浏览器的事实标准

## 8.4 screen 对象

## 8.5 history 对象
- history对象保存着客户的历史记录
- history.go(n) 接受两种参数，字符串或整数值，当历史记录中不包含字符串，那么这个方法什么也不做
- history.length: 保存着历史记录的数量
