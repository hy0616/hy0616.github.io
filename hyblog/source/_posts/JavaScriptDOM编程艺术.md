---
title: JavaScriptDOM编程艺术
date: 2017-01-04 11:01:31
tags: [javaScript、web开发]
categories: javaScript
---

##### JavaScript DOM编程艺术是一本比较基础的书籍，讲解了起源、语法、DOM操作、ajax基础运用、h5等基础，读完之后get到很多基础知识，清除自己的基础漏洞。

<!--more-->

### JavaScript(ECMAscript)
###### 1.DHTML是“Dynamic“HTML(动态HTML)的简称。DHTML并不是一项新的技术，而是描述HTML、CSS、JavaScript技术综合的术语。DHTML背后的含义是:

 * 利用HTML把网页标记为各种元素;
 * 利用CSS设置元素样式和他们的显示位置;
 * 利用JavaScript实时的操控页面和改变样式;

###### 2.五个常用的DOM方法:

 + `document.getElementById("id")`将返回一个对象，该对象对应着文档里的一个特定的元素节点。
 + `document.getElementsByTagName("div")`将返回一个对象数组，对应着文档里的一组特定的元素节点。
 + `document.getElementsByClassName("class")`将返回一个对象数组，对应着文档里的一组特定的元素节点。
 + `object.getAttribute("attribute")` object只能为元素节点。
 + `object.setAttribute("attribute","value")` object只能为元素节点。

###### 3.JavaScript语言里的对象可以分为三种类型：

 * **用户对象**：由程序员自行创建的队形;
 * **内建对象**：内建JavaScript语言里的对象;
 * **宿主对象**：由浏览器提供的对象;

###### 4.一份文档就是一个节点树节点分为不同类型：
 + **元素节点**; nodeType属性值为1。
 + **属性节点**; nodeType属性值为2。
 + **文本节点**; nodeType属性值为3。

###### 5.DOM提供的新属性：

 + childNodes 获取任何元素的所有子元素;
 + nodeType 总共有12种可取值，但只有3种具有实际价值，元素节点nodeType属性值是1、属性节点nodeType属性值是2、文本节点nodeType属性值是3;
 + nodeValue 改变文本节点值;
 + firstChild 获取childNodes第一个子元素;
 + lastChild 获取childNodes最后一个子元素;

###### 6.性能考虑

 + 平稳退化: 确保网页在没有JavaSctipt的情况下也能正常运行;
 + 分离JavaScript: 把网页结构和内容与JavaScript脚本的动作行为分开;(分离JavaScript、渐进渐强、结构样式分离、)
 + 向后兼容性: 确保老版本浏览器不会因为JavaScript脚本而死掉;(对象检测、浏览器嗅探技术)
 + 性能考虑: 确定执行脚本的性能最优;(压缩脚本、合并和放置脚本、尽量少访问DOM、尽量减少标记)

###### 7.window对象的open()方法

JavaScript使用window对象的open()方法来创建新的浏览器窗口这个方法有三个参数`window.open(url,name,features)`,这三个参数都是可选的，第一个参数为新窗口url地址，第二个参数为新窗口名字，第三个参数是一个以逗号分割的字符串，其内容是新窗口的各种属性。示例`window.pen(url,name,"width=300,height=500")`

###### 8.”JavaScript:“ 伪协议

”真“协议用来在因特网上计算机之间传输数据包，如HTTP协议`https://`、FTP协议`ftp://`等，伪协议则是一种非标准化协议。”JavaScript:“伪协议让我们通过一个链接调用JavaScript函数。`onclick="javascript:函数()"`
在HTML文档通过伪协议调用JavaScript代码做法，在较老浏览器或在浏览器禁用JavaScript的情况下会造成链接失败或什么都不做。

###### 9.搜索机器人(searchbot)网络蜘蛛(web Spider)

搜索机器人是一个自动化程序，他们浏览web的目的是把各种网页添加到搜索引擎的数据库里，各大搜索引擎都有类似的程序，目前只有少数机器人能够理解JavaScript代码，所以你的JavaScript代码不能平稳退化他们在搜索引擎上的排名就可能大受损害。

###### 10.共享onload

假设两个函数都在页面加载时执行，如果逐一绑定到onload事件上它们当中只有最后一个才被执行
`window.onload=函数1();window.onload=函数2();`

**解决方法**

1.创建匿名函数来包容要被执行的函数，然后把匿名函数绑定到onload事件上
`window.onload=function(){函数1();函数2();}`

2.弹性最佳解决方案，创建通用函数

 + 把现有的onload事件处理函数的值存入变量oldonload;
 + 如果事件上没有绑定任何函数，把新的函数添加给事件;
 + 如果事件绑定了一些函数，就把新函数追加到现有函数末尾;


    function addloadEvent (fun){
        var oldonload = window.onload;
        if(typeof window.onload != 'function'){
        	window.onload = fun;
        }else{
        	oldonload();
        	fun();
        }
    }

###### 11.DOM Core 和 HTML DOM

###### 12.动态创建标记

传统方法:

 + document对象的write方法可以方便快捷的把字符串插到文档里去。
 `document.write("<p>This is write</p>")` 但是它违背的行为与表现分离的原则。
 + innerHTML属性可以读、写给定元素里HTML内容，当插入大段HTML内容，innerHTML属性更适用。


    window.onload = function(){
         var testdiv = document.getElementById("div");
         testdiv.innerHTML = "<p>This is innerHTML</p>";
    }

DOM方法:

 + **createElement()**方法完成创建新的元素`document.createElement("p")`，但是不属于任何一棵DOM节点树的组成部分，这种情况称为**节点碎片**。
 + **createTextNode()**方法为新创建的元素创建文本节点` document.createTextNode("Hellow World")`。
 + **appendChild()**方法插入文档节点树`parent.appendChild(child)`。
 + **inserBefore()**方法把一个新的元素插入到现有元素。
 + **nextSibling()**属性，目标元素的下一个兄弟元素即目标元素的nextSinling属性


    //插入为目标元素的子元素
    window.onload = function(){
        var child = document.createElement("p");
        var parent = document.getElementById('textdiv');
        parent.appendChild(child);
        var txt = document.createTextNode("Hello world");
        child.appendChild(txt);
    }

    //使用inserBefore方法插入为目标元素的兄弟元素前边
    window.onload = function(){
    var textp = document.createElement("p");
        var textdiv= document.getElementById('textdiv');
        var parent = textdiv.parentNode;
        parent.inserBefore(textdiv,textp);
        var txt = document.createTextNode("Hello world");
        child.appendChild(txt);
    }

    //自己编写inserAfter
    //newElement 新元素; targetelement 目标元素
    function inserAfter (newElement,targetElement){
        var parent = targetElement,patentNode;
        if(parent.lastChild == targetElement)
        parent.appendChild(newElement);
        }else{
        parent.inserBefore(newElement,targetElement.nextSibling);
    }

###### 13.Ajax

Ajax主要优势就是对页面的请求以异步方式发送到服务器。
Ajax技术的核心就是XMLHttpRequest对象。

###### 14.三位一体的网页

 +  结构层 由HTML或XHTML之类的标记语言负责创建;
 +  表现层 由CSS负责完成，描述页面应该如何呈现;
 +  行为层 JavaScript和DOM的主宰领域;

###### 15.用css和js做table斑马线效果

CSS:
== :nth-child(n) 选择器匹配属于其父元素的第 N 个子元素，不论元素的类型。==
== n 可以是数字、关键词或公式。==
== Odd 和 even 是可用于匹配下标是奇数或偶数的子元素的关键词（第一个子元素的下标是 1）。==
`tr:nth-child(old) {background-color:#ffc}`
`tr:nth-child(even) {background-color:#fff}`
js:

    function table (){
        if(documen.getElementsByTagName)return false;
        var tables = document.getElementsByTagName("table");
        var odd,rows;
        for(var i=0; i>tables.length;i++){
            odd = false;
            rows = tables[i].getElementByTagName("tr");
            for(var j=0;j<rows;j++){
                if(odd){
                    rows[j].style.background = #ffc;
                    odd = false;
                }else{
                	odd = true;
                }
            }
        }
    }
