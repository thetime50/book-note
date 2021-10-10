# 第1章 什么是JavaScript
本章内容  
❑ JavaScript历史回顾  
❑ JavaScript是什么  
❑ JavaScript与ECMAScript的关系  
❑ JavaScript的不同版本  

1995年，JavaScript问世。代替Perl等服务器端语言处理输入验证  
网景公司在Navigator浏览器中加入JavaScript验证输入有效，避免后端验证耗时

## 1.1 简短的历史回顾

- 1955年 工程师 Brendan Eich，在浏览器 NetscapeNavigator 2 中开发Mocha脚本(后改名LiveScripe)
- 在 NetscapeNavigator 3 中发布 JavaScript1.1
    - 1996 年 8 月 13 日 微软发布 [IE3](https://en.wikipedia.org/wiki/Internet_Explorer_3) 包含 JScript 冲击网景
- 1997年,JavaScript 1.1作为提案被提交给欧洲计算机制造商协会（Ecma）
    - 第39技术委员会（TC39）承担了“标准化一门通用、跨平台、厂商中立的脚本语言的语法和语义”的任务（参见TC39-ECMAScript）
    - 定义ECMA-262标准，也就是ECMAScript（发音为“ek-ma-script”）脚本语言标准。
- 1998年，国际标准化组织（ISO）和国际电工委员会（IEC）也将ECMAScript采纳为标准（ISO/IEC-16262）
    - 各家浏览器按照标准来实现

## 1.2 JavaScript实现

js实现的构成
- JavaScript  
    ❑ 核心（ECMAScript）  
    ❑ 文档对象模型（DOM）  
    ❑ 浏览器对象模型（BOM）

## 1.2.1 ECMAScript

ECMAScript，即ECMA-262定义的语言，不包含输入和输出之类的方法。  
**宿主环境**提供ECMAScript的基准实现和与环境自身交互必需的扩展（比如DOM）。包括
- Web浏览器
- Node.js
- 即将被淘汰的Adobe Flash


ECMASript定义了  
❑ 语法  
❑ 类型  
❑ 语句  
❑ 关键字  
❑ 保留字  
❑ 操作符  
❑ 全局对象  

### 1. ECMAScript版本
ECMAScript不同的版本以“edition”表示(即ECMA-262版本)  
最近的是2019年6月的第10版 [*12th Edition – ECMAScript 2021*](https://en.wikipedia.org/wiki/ECMAScript#12th_Edition_–_ECMAScript_2021)  

**ECMA-262 第一版**
1. 以网景的JavaScript 1.1为基础
2. 删除了所有浏览器特定的代码
3. ECMA-262要求支持Unicode标准
4. 对象要与平台无关 特别是Date (也是JavaScript 1.1和JavaScript 1.2不符合ECMA-262第1版要求的原因。)

**ECMA-262第2版**
1. 编校 以满足ISO/IEC-16262要求

**ECMA-262第3版**
1. * 字符串处理
2. * 错误定义
3. * 数值输出
4. * 正则表达式
5. 新的控制语句??
6. * try/catch异常处理的支持
7. 让标准国际化的少量修改

**ECMA-262第4版** 彻底修订  
第3版基础上完全定义了一门新语言
1. 强类型变量
2. 新语句和数据结构
3. 真正的类和经典的继承
4. 操作数据的新手段

***ECMAScript 3.1***提案  
进行较少的改进 第4版跳跃太大了，ECMA-262第4版在正式发布之前被放弃  
ECMAScript 3.1变成了ECMA-262的第5版

**ECMA-262的第5版** 2009/12/03  
2011/06 修订
1. 厘清第3版存在的歧义
2. 原生的解析和序列化JSON数据的JSON对象
3. 继承和高级属性定义的方法
4. 严格模式 增强ECMAScript引擎解释和执行代码能力

**ECMA-262第6版** ES6、ES2015或ES Harmony（和谐版）
1. 类
2. 模块
3. 迭代器
4. 生成器
5. 箭头函数
6. 期约
7. 反射
8. 代理
9. 众多新的数据类型。

**ECMA-262第7版** 也称为ES7或ES2016
1. 少量语法层面的增强
    - 如Array.prototype.includes和指数操作符

**ECMA-262第8版** 也称为ES8、ES2017，完成于2017年6月
1. 异步函数（async/await）
2. [SharedArrayBuffer][SharedArrayBuffer]: 通用的、固定长度的原始二进制数据缓冲区，类似于该ArrayBuffer对象
3. [Atomics API][Atomics-API]: 该Atomics对象提供原子操作作为静态方法。它们与SharedArrayBuffer和ArrayBuffer对象一起使用。
4. Object.values()/Object.entries()/Object. getOwnPropertyDescriptors()
    1. Object.values()
    2. [Object.entries()][entries]: 给定对象的[key, value]可枚举对象
    3. Object. getOwnPropertyDescriptors():给定对象的所有属性描述符
5. 字符串填充方法  
    [String.prototype.padStart()][padStart]  
    [String.prototype.padEnd()][padEnd]  
6. 明确支持对象字面量最后的逗号

[SharedArrayBuffer]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer
[Atomics-API]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics
[entries]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries
[padStart]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/padStart  
[padEnd]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/padEnd

**ECMA-262第9版** 也称为ES9、ES2018，发布于2018年6月
1. 异步迭代
2. 剩余和扩展属性
3. 一组新的正则表达式特性
4. Promise finally()
5. 模板字面量修订

**ECMA-262第10版** 也称为ES10、ES2019，发布于2019年6月
1. [Array.prototype.flat()/flatMap()、][[flat]]: 指定深度递归展开多维数组
2. [String.prototype.trimStart()/trimEnd()]: 方法从字符串的开头/结束删除空格。trimLeft()/trimRight() 是此方法的别名
3. [Object.fromEntries()][fromEntries]: 方法把键值对列表转换为一个对象
4. Symbol.prototype.description: 它会返回 Symbol 对象的可选描述的字符串
5. 明确定义了Function.prototype.toString()的返回值
6. 固定了Array.prototype.sort()的顺序
7. 解决与JSON字符串兼容的问题
8. 定义catch子句的可选绑定

[flat]:https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat
[trimStart]:https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/trimStart
[fromEntries]:https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries

### 2. ECMAScript 符合性

❑ 支持ECMA-262中描述的所有“类型、值、对象、属性、函数，以及程序语法与语义”；  
❑ 支持Unicode字符标准。  
此外，符合性实现还可以满足下列要求。  
❑ 增加ECMA-262中未提及的“额外的类型、值、对象、属性和函数”。ECMA-262所说的这些额外内容主要指规范中未给出的新对象或对象的新属性。  
❑ 支持ECMA-262中没有定义的“程序和正则表达式语法”（意思是允许修改和扩展内置的正则表达式特性）。  

### 3. 浏览器对ECMAScript的支持

2008年，五大浏览器（IE、Firefox、Safari、Chrome和Opera）全部兼容ECMA-262第3版。IE8率先实现ECMA-262第5版，并在IE9中完整支持。Firefox 4很快也做到了。下表列出了主要的浏览器版本对ECMAScript的支持情况。

## 1.2.2 DOM

### 1. DOM规范的制定
在IE4和Netscape Navigator 4支持不同形式的动态HTML（DHTML）的情况下，开发者首先可以做到不刷新页面而修改页面外观和内容。  
万维网联盟（W3C, World Wide Web Consortium）开始了制定DOM标准的进程。


### 2. DOM级别
1998年10月，DOM Level 1成为W3C的推荐标准
  - DOM Core 映射XML文档
  - DOM HTML 扩展 加了特定于HTML的对象和方法

DOM Level 2新增模块

❑ DOM视图：描述追踪文档不同视图（如应用CSS样式前后的文档）的接口。  
❑ DOM事件：描述事件及事件处理的接口。  
❑ DOM样式：描述处理元素CSS样式的接口。  
❑ DOM遍历和范围：描述遍历和操作DOM树的接口。  
❑ DOM Level 1中的DOM Core被扩展以包含对XML命名空间的支持。

DOM Level 3
  增加以统一的方式加载和保存文档的方法（包含在一个叫DOM Load and Save的新模块中）
  验证文档的方法（DOM Validation）
  DOM Core扩展了所有XML 1.0的特性，包括XML Infoset、XPath和XML Base。

目前，W3C不再按照Level来维护DOM了，而是作为DOM Living Standard来维护，其快照称为DOM4。  
DOM4新增的内容包括替代Mutation Events的Mutation Observers

// 没有一个标准叫“DOM Level 0” Level 0可以看作IE4和Netscape Navigator 4中最初支持的DHTML。

### 3. 其他DOM

除了DOM Core和DOM HTML接口之外其他语言的DOM标准

❑ 可伸缩矢量图（SVG, Scalable Vector Graphics）
❑ 数学标记语言（MathML, Mathematical Markup Language）
❑ 同步多媒体集成语言（SMIL, Synchronized Multimedia IntegrationLanguage）

### 4. Web浏览器对DOM的支持情况
DOM标准在Web浏览器实现它之前就已经作为标准发布了。  
IE在第5版中尝试支持DOM，但直到5.5版才开始真正支持，该版本实现了DOM Level 1的大部分。  
之后版本仅修复了一些问题没有实现新特性  

DOM标准在Web浏览器实现它之前就已经作为标准发布了。IE在第5版中尝试支持DOM，但直到5.5版才开始真正支持，该版本实现了DOM Level 1的大部分。

## 1.2.3 BOM
IE3和Netscape Navigator 3提供了浏览器对象模型（BOM）API，用于支持访问和操作浏览器的窗口  
HTML5规范正式规范的形式涵盖了尽可能多的BOM特性。

❑ 弹出新浏览器窗口的能力；
❑ 移动、缩放和关闭浏览器窗口的能力；
❑ navigator对象，提供关于浏览器的详尽信息；
❑ location对象，提供浏览器加载页面的详尽信息；
❑ screen对象，提供关于用户屏幕分辨率的详尽信息；
❑ performance对象，提供浏览器内存占用、导航行为和时间统计的详尽信息；
❑ 对cookie的支持；
❑ 其他自定义对象，如XMLHttpRequest和IE的ActiveXObject。


## 1.3 JavaScript版本
Netscape/Mozilla(firefox)一直沿用JavaScript的版本编号  

Netscape Navigator 2 - JavaScript 1.0
Firefox 4 - JavaScript 1.8.5

## 1.4 小结
JavaScript保护
❑ ECMAScript：由ECMA-262定义并提供核心功能。
❑ 文档对象模型（DOM）：提供与网页内容交互的方法和接口。
❑ 浏览器对象模型（BOM）：提供与浏览器交互的方法和接口。

五大Web浏览器（IE、Firefox、Chrome、Safari和Opera）基本支持 ES5  
ES6（ECMAScript 6）和ES7（ECMAScript 7）的支持度也在不断提升。