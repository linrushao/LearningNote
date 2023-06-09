# Java程序员的10道XML面试题

1. 包括web开发人员的Java面试在内的各种面试中，XML面试题在各种编程工作的面试中很常见。XML是一种成熟的技术，经常作为从一个平台到其他平台传输数据的标准。XML面试问题包括用于转换XML文件的XSLT技术，XPATH，XQuery等各种XML技术和XML基础知识，比如DTD或者Schema。
2. 本文将看到10道常见的XML面试问答题。这些问题大部分在Java面试中会问到，同时在C，C++，Scala或其他语言的编程面试中同样很有用处。XML并不依赖于其他编程语言，同SQL一样是编程人员所需要的技能之一，因此在任何技术工作面试之前准备一些XML问题是很有意义的。
3. XML面试问答

> 下面是我列出的关于XML技术经常会问到的面试题。这些问题并不很难但涵盖了XML技术的一些重要领域，比如DTD，XMLSchema，XSLT转换，XPATH检索，XML绑定，XML解析器以及XML的基本知识，比如命名空间，校验，属性，元素等。

## 问题1：XML是什么？

答：XML即可扩展标记语言（ExtensibleMarkuplanguage），你可以根据自己的需要扩展XML。XML中可以轻松定义==<books>==,==<orders>==等自定义标签，而在HTML等其他标记语言中必须使用预定义的标签，比如==**<p>**==，而不能使用用户定义的标签。使用DTD和XMLSchema标准化XML结构。XML主要用于从一个系统到另一系统的数据传输，比如企业级应用的客户端与服务端。

## 问题2：DTD与XMLSchema有什么区别？

答：DTD与XMLSchema有以下区别：DTD不使用XML编写而XMLSchema本身就是xml文件，这意味着XML解析器等已有的XML工具可以用来处理XMLSchema。而且XMLSchema是设计于DTD之后的，它提供了更多的类型来映射xml文件不同的数据类型。DTD即文档类型描述(DocumentTypedefinition)是定义XML文件结构的传统方式。

## 问题3：XPath是什么？

答：XPath是用于从XML文档检索元素的XML技术。XML文档是结构化的，因此XPath可以从XML文件定位和检索元素、属性或值。从数据检索方面来说，XPath与SQL很相似，但是它有自己的语法和规则。了解更多查看怎样使用XPath从XML文档中检索数据。

## 问题4：XSLT是什么?

答：XSLT也是常用的XML技术，用于将一个XML文件转换为另一种XML，HTML或者其他的格式。XSLT为转换XML文件详细定义了自己的语法，函数和操作符。通常由XSLT引擎完2成转换，XSLT引擎读取XSLT语法编写的XML样式表或者XSL文件的指令。XSLT大量使用递归来执行转换。一个常见XSLT使用就是将XML文件中的数据作为HTML页面显示。XSLT也可以很方便地把一种XML文件转换为另一种XML文档。

## 问题5：什么是XML元素和属性

答：最好举个例子来解释。下面是简单的XML片断。

```xml
<Orders>
    <Order id="123">
        <Symbol>6758.T</Symbol>
        <Price>2300</Price>
    </Order>
</Orders>
```

例子中id是元素的一个属性，其他元素都没有属性。

## 问题6：什么是格式良好的XML

答：这个问题经常在电话面试中出现。一个格式良好的XML意味着该XML文档语法上是正确的，比如它有一个根元素，所有的开放标签合适地闭合，属性值必须加引号等等。如果一个XML不是格式良好的，那么它可能不能被各种XML解析器正确地处理和解析。

## 问题7：XML命名空间是什么？它为什么很重要？

答：XML命名空间与Java的package类似，用来避免不同来源名称相同的标签发生冲突。XML命名空间在XML文档顶部使用xmlns属性定义，语法为xmlns:prefix=’URI’。prefix与XML文档中实际标签一起使用。下面例子为XML命名空间的使用。

```xml
<root xmlns:inst="http://instruments.com/inst">
    <inst:phone>
		<inst:number>837363223</inst:number>
    </inst:phone>
</root>
```

## 问题8：DOM和SAX解析器有什么区别

答：这又是一道常见面试题，不仅出现在XML面试题中，在Java面试中也会问到。DOM和SAX解析器的主要区别在于它们解析XML文档的方式。使用DOM解析时，XML文档以树形结构的形式加载到内存中，而SAX是事件驱动的解析器。这个问题更详细的回答查看DOM和SAX解析器之间的区别。

## 问题9：XMLCDATA是什么

答：这道题很简单也很重要，但很多编程人员对它的了解并不深。CDATA是指字符数据，它有特殊的指令被XML解析器解析。XML解析器解析XML文档中所有的文本，比如==<name>This is name of person </name>==，标签的值也会被解析，因为标签值也可能包含XML标签，比如==<name><FirstName>First Name</FirstName></name>==。CDATA部分不会被XML解析器解析。CDATA部分以==<![CDATA[开始，以]==结束。

## 问题10：Java的XML数据绑定是什么

答：Java的XML绑定指从XML文件中创建类和对象，使用Java编程语言修改XML文档。XML绑定的JavaAPI，JAXB提供了绑定XML文档和Java对象的便利方式。另一个可选的XML绑定方法是使用开源库，比如XMLBeans。Java中XML绑定的一个最大的优势就是利用Java编程能力创建和修改XML文档。以上的XML面试问答题收集自很多编程人员，但它们对于使用XML技术的每个人都是有用的。由于XML具有平台独立的特性，XPath，XSLT，XQuery等XML技术越来越重要，XML广泛用于跨平台数据传输。尽管XML有冗余和文档体积大等缺点，但它在web服务以及带宽、速率作为次要考虑因素的系统间数据传输起很大作用。