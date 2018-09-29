### JS

#####用call方法将伪数组转化为数组

```js
 <script>
        var noRealArr = document.getElementsByTagName("*");
        noRealArr =  Array.prototype.slice.call(noRealArr);
        console.log(noRealArr)
    </script>

//(27) [html, head, meta, title, script, script, link, link, body, div.self_container, div.self_head, div.logo, i.fa.fa-music, span, div.music_search, input, i.fa.fa-search, div.person_info, img, div.person_name, span, i.fa.fa-caret-down, div.self_setting, i.fa.fa-cog, div.hidden_person_info, div.triangle-up, script]
```

##### - 函数声明和函数表达式的区别



- 函数声明

```js
// 函数声明
    function funDeclaration(type){
        return type==="Declaration";
    }
```

- 函数表达式

```js
 // 函数表达式
    var funExpression = function(type){
        return type==="Expression";
    }

```

Javascript 中函数声明和函数表达式是存在区别的，函数声明在JS解析时进行函数提升，因此在同一个作用域内，不管函数声明在哪里定义，该函数都可以进行调用。而函数表达式的值是在JS运行时确定，并且在表达式赋值完成后，该函数才能调用。这个微小的区别，可能会导致JS代码出现意想不到的bug,让你陷入莫名的陷阱中。

##### - 面试题

​	[call  bind  apply](https://segmentfault.com/a/1190000000375138?page=1)



##### - e.target == e.currentTarget`处理冒泡



##### - bind` `call` `applay`的区别

​	[区别](http://www.cnblogs.com/coco1s/p/4833199.html)

##### 关于js`childNodes`的坑

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
</head>
<body><p id="demo">请点击按钮来获得 body 元素子节点的节点类型。</p>
<button onclick="myFunction()">试一下</button>
<script>
    function myFunction()
    {
        var txt="";
        var c=document.body.childNodes;
        for (i=0; i<c.length; i++)
        {
            txt=txt + c[i].nodeType + "<br>";
        };
        var x=document.getElementById("demo");
        x.innerHTML=txt;
    }
</script>

<p><b>注释：</b>元素中的空格被视作文本，而文本被视作文本节点。</p>

</body>
</html>


```

![1](C:\Users\Administrator\Desktop\1.png)

- 其中text节点是来自于换行,即`p`和`button`之间换行导致的,将换行也当做文本节点来解析了



##### 当批量添加多个HTML对象的时候,这样能够优化性能

- [文档碎片详解](https://www.cnblogs.com/aaronjs/p/3510768.html)


- 在动态添加非常多的dom元素到页面的时候经常用到方法createDocumentFragment，起到了性能优化作用。

```js
var ul = document.getElementsByTagName("ul")[0]; // assuming it exists
var docfrag = document.createDocumentFragment();  //创建fragment
var browserList = ["Internet Explorer", "Mozilla Firefox", "Safari", "Chrome", "Opera"];

browserList.forEach(function(e) {
  var li = document.createElement("li");
  li.textContent = e;
  docfrag.appendChild(li);
});

ul.appendChild(docfrag);  //一次性加入ul中
// a list with well-known web browsers
```

- 若不使用createDocumentFragment，可以如下实现，但是问题是在数组项有成千上万个时，在循环中每次一个去添加DOM元素，给性能带来压力，最好的做法是使用createDocumentFragment先创建文档片段，然后在循环外一次性批量添加完成。

```js
var ul = document.getElementsByTagName("ul")[0];
    var browserList = ["Internet Explorer", "Mozilla Firefox", "Safari", "Chrome", "Opera"];
    browserList.forEach(function (e) {
        var li = document.createElement("li");
        li.textContent = e;
        ul.appendChild(li);
    });
```

```javascript
 //不建议的做法
    var browserList = ["Internet Explorer", "Mozilla Firefox", "Safari", "Chrome", "Opera"];
    $.each(browserList, function (index,value) {
        $('<li>').text(value).appendTo($('ul').eq(0));
    })

    //好的做法NO1
    var browserList = ["Internet Explorer", "Mozilla Firefox", "Safari", "Chrome", "Opera"];
    var myHTML = '';
    $.each(browserList, function (index, value) {
        myHTML += '<li>' + value + '</li>';
    })
    $('ul').eq(0).html(myHTML);

    //好的作法NO2
    var frag = document.createDocumentFragment();
    var browserList = ["Internet Explorer", "Mozilla Firefox", "Safari", "Chrome", "Opera"];
    $.each(browserList, function (index, value) {
        var li = document.createElement("li");
        li.textContent = value;
        frag.appendChild(li);
    })
    $('ul').eq(0).append($(frag));
```





### jquery源码

##### - 源码分析网址

- [源码浅析2--奇技淫巧](http://www.cnblogs.com/coco1s/p/5303041.html)
- [jquery-1.6.1源码分析系列](http://www.cnblogs.com/nuysoft/archive/2011/11/14/2248023.html)
- [jquery源码分析笔记](http://www.cnblogs.com/fjzhou/category/301373.html)
- [jquery-1.9.1源码分析系列完毕目录整理](http://www.cnblogs.com/chuaWeb/p/jQuery-1-9-1-catalog.html)
- [jquery中的正则详解](https://book.2cto.com/201401/39480.html)


### 浏览器兼容问题

- [IE兼容性问题汇总](http://www.cnblogs.com/chuaWeb/p/5210689.html)

