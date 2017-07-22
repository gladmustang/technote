 
# 扩展jQuery对象时如何扩展成员变量具体怎么实现

作者： 字体：[<a>增加</a> <a>减小</a>] 类型：转载 时间：2014-04-25[ 我要评论](http://www.jb51.net/article/49383.htm#comments)

 这篇文章主要介绍了扩展jQuery对象时如何扩展成员变量,需要的朋友可以参考下

 先看一段代码： 

 <a id="copybut18806" class="copybut"></a><u>复制代码</u>代码如下:
```
jQuery.fn.extend( 
{ 
myOwnMember: 3, 
getMyOwnMember: function () { return this.myOwnMember; }, 
setMyOwnMember: function (v) { this.myOwnMember = v; return this.myOwnMember; } 
} 
); 

$("body").myOwnMember; //3 
$("body").getMyOwnMember(); //3 
$("body").setMyOwnMember(4); //4 
$("body").getMyOwnMember(); //3 
```
这段代码给jQuery对象扩展了一个成员myOwnMember，两个函数getMyOwnMember，setMyOwnMember分别用于返回和设置myOwnMember的值。但是我们看到setMyOwnMember并没有起作用，我们再次getMyOwnMember时，返回的还是初始的值。这是为什么呢？原因在于$("body")每次都会创建一个新对象，所以每次$("body")里面的myOwnMember都是初始值。如果我们将代码改成： 

 <a id="copybut10520" class="copybut"></a><u>复制代码</u>代码如下:
```
jQuery.fn.extend( 
{ 
myOwnMember: 3, 
getMyOwnMember: function () { return this.myOwnMember; }, 
setMyOwnMember: function (v) { this.myOwnMember = v; return this.myOwnMember; } 
} 
); 

var body = $("body"); 
body.myOwnMember; //3 
body.getMyOwnMember(); //3 
body.setMyOwnMember(4); //4 
body.getMyOwnMember(); //4 
```
这就是我们想要的效果了，这是因为$("body")只创建了一次，后面都是通过body变量进行的引用。但是这种方法在实际使用过程中还是存在问题，因为我不可能在全局范围内都能够引用到body变量，很多时候还是通过$("body")来获取dom节点，这样的话我们又怎么保存一个jQuery对象扩展变量的值呢？解决方法是我们不要把变量保存在jQuery对象上，而是保存在dom节点上，无论在一个dom节点上创建多少个jQuery对象，都是指向同一个dom节点的。所以我们将代码改成如下： 

 <a id="copybut88493" class="copybut"></a><u>复制代码</u>代码如下:
```
jQuery.fn.extend( 
{ 
getMyOwnMember: function () { return this[0].myOwnMember; }, 
setMyOwnMember: function (v) { this[0].myOwnMember = v; return this[0].myOwnMember; } 
} 
); 

$("body").getMyOwnMember(); //undefined 
$("body").setMyOwnMember(4); //4 
$("body").getMyOwnMember(); //4 
```
如对本文有疑问，请提交到交流社区，广大热心网友会为你解答！！ [点击进入社](http://shequ.jb51.net/)