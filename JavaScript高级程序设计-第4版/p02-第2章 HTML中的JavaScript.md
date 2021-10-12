# 第2章 HTML中的JavaScript

❑ 使用&lt;script&gt;元素
❑ 行内脚本与外部脚本的比较
❑ 文档模式对JavaScript有什么影响
❑ 确保JavaScript不可用时的用户体验

## 2.1 &lt;script&gt;元素

由网景在Netscape Navigator 2中实现的

&lt;script&gt;元素有下列8个属性。
❑ async：可选。表示应该立即开始下载脚本，但**不能阻止其他页面动作**，比如下载资源或等待其他脚本加载。只对外部脚本文件有效。  
❑ charset：可选。使用src属性指定的代码字符集。这个属性很少使用，因为大多数浏览器不在乎它的值。  
❑ crossorigin：可选。配置相关请求的CORS（跨源资源共享）设置。默认不使用CORS。crossorigin="anonymous"配置文件请求不必设置凭据标志。crossorigin="use-credentials"设置凭据标志，意味着出站请求会包含凭据。  
❑ defer：可选。表示脚本可以延迟到**文档完全被解析和显示之后再执行**。只对外部脚本文件有效。在IE7及更早的版本中，对行内脚本也可以指定这个属性。  
❑ integrity：可选。允许比对接收到的资源和指定的加密签名以验证子资源完整性（SRI, SubresourceIntegrity）。如果接收到的资源的签名与这个属性指定的签名不匹配，则页面会报错，脚本不会执行。这个属性可以用于确保内容分发网络（CDN, Content DeliveryNetwork）不会提供恶意内容。  
❑ language：废弃。最初用于表示代码块中的脚本语言（如"JavaScript"、"JavaScript 1.2"或"VBScript"）。大多数浏览器都会忽略这个属性，不应该再使用它。  
❑ src：可选。表示包含要执行的代码的外部文件。  
❑ type：可选。代替language，表示代码块中脚本语言的内容类型（也称MIME类型）。按照惯例，这个值始终都是"text/javascript"，尽管"text/javascript"和"text/ecmascript"都已经废弃了。JavaScript文件的MIME类型通常是"application/x-javascript"，不过给type属性这个值有可能导致脚本被忽略。在非IE的浏览器中有效的其他值还有"application/javascript"和"application/ecmascript"。如果这个值是module，则代码会被当成ES6模块，而且只有这时候代码中才能出现import和export关键字。


没有配置async 或者 defer &lt;script&gt;元素中的代码被计算完成之前，页面的其余内容不会被加载，也不会被显示
```html
<!-- 行内 被解释为函数定义保存到解释器环境中 -->
<script>
    function fn(){}
</script>
<!-- 外部文件中的JavaScript -->
<script src="xxx.js" ></script>
<!-- XHTML文档中，可以忽略结束标签 但是在HTML文件中是无效的 -->
<script src="xxx.js" />
```

可以不使用.js扩展名（如TypeScript，或React的JSX），但是服务器要返回正确的[MIME类型](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

1. 向src属性指定的路径发送一个GET请求，不受浏览器同源策略限制(jsonx原理)，但返回并被执行的JavaScript则受限制。当然，这个请求仍然受父页面HTTP/HTTPS协议的限制。

### 2.1.1 标签位置

最早所有&lt;script&gt;元素都被放在页面的&lt;head&gt;标签内，但是会阻塞页面渲染  
现代Web应用程序通常将所有JavaScript引用放在&lt;body&gt;元素中的页面内容后面

### 2.1.2 推迟执行脚本
defer的属性 脚本会被延迟到整个页面都解析完毕后再运行  
HTML5规范要求脚本应该按照它们出现的顺序执行  
会在DOMContentLoaded事件之前执行 （请参考第17章）

defer属性的支持是从IE4、Firefox 3.5、Safari 5和Chrome7开始的。  
XHTML文档，指定defer属性时应该写成defer="defer"。


### 2.1.3 异步执行脚本

async属性 不阻塞异步下载，下载后立即执行，不保证执行顺序  
异步脚本不应该在加载期间修改DOM(或者有副作用的操作 会相互影响)

XHTML文档，指定async属性时应该写成async="async"

### 2.1.4 动态加载脚本

通过向DOM中动态添加script元素同样可以加载指定的脚本  
把HTMLElement元素添加到DOM且执行到这段代码之前不会发送请求  
默认情况下，动态插入的&lt;script&gt;元素是以异步方式加载的  
但是不是所有浏览器都支持异步加载，为了统一行为最好一致设置async为false  
```js
let script = document.createElement('script')
script.src = 'xxx.js'
script.async = false
document.head.appendChild(script)
```

- 动态加载对浏览器不是可见的，会影响在资源获取队列中的优先级
- 可能会影响性能
- 使用&lt;link ref="preload"&gt;&lt;/link &gt; 让浏览器预加载资源 [Link types: preload](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/preload)
```html
<link rel="stylesheet" href="xxx.js">
```

### 2.1.5 XHTML中的变化

XHTML是将HTML作为XML的应用重新包装的结果  
(就像html中的ts 一个xml定义文件 更倾向于xml语法 更严格的html)  
XHTML中使用JavaScript必须指定type属性且值为text/javascript  
XHTML虽然已经退出历史舞台

```html
<script type="test/javascript"> 
function compare(a,b){
    if(a < b){
        return true
    }
    return false
}
</script>
```
html解析script元素时会使用特殊规则，xhtml中则是按xml的语法来解析
上面的代码在xhtml中 (&lt;) 会被解析为标签开始，并且 (&lt;) 后面不能是空格  
解决 1. 需要把 (&lt;) 替换为HTML 字符实体 (&amp;lt;)
解决 2. 把代码放在CDATA块中,并且用注释来支持\[支持html语法的浏览器]

```xhtml
<script type="test/javascript"> 
// <![CDATA[
function compare(a,b){
    if(a < b){
        return true
    }
    return false
}
// ]]>
</script>
```

可以设置script元素 EMEI 类型 type="application/xhtml+xml"指定为XHTML,不是所有浏览器都支持

### 2.1.6 废弃的语法

早期的type属性使用一个MIME类型字符没有跨浏览器标准化，这会导致不支持的MIME类型的script标签被跳过  
所以最好不指定type属性

对于早期不支持script标签的浏览器(Mosaic)会直接把里面的内容显示在页面上，所以会有下面这种写法  
但是在xhtml模式下，这样的脚本又会被忽略

```html
<script><!--
    function fn(){}
//--></script>
```

## 2.2 行内代码与外部文件


