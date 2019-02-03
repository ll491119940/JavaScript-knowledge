# HTML5

##  关于html5

###  如果把html5看成一个开放平台，那它的构建模块有哪些？

构建模块至少应该包括以下几个：<nav>、<header>、<section>、<footer>

`<nav>`标签用来将具有导航性质的链接划分在一起，使代码结构在语义化方面更加准确。

`<header>`标签用来定义文档的页眉（介绍信息）

`<section>`标签用来描述文档的结构

`<footer>`标签用来定义section或document的页脚。在典型情况下，该元素会包含创作者的姓名、文档的创作日期以及联系信息。

## html5语法

- `<hgroup>`标签用于对网页或区段（section）的标题进行组合。`<group>`将一组元素声明归在一起，以便将它们作为一个组合并到复杂类型定义中
- `<meter>`标签定义度量衡。仅用于已知最大和最小值的度量
- `<article>`标签定义外部的内容。
- `<aside>`标签定义article以外的内容，aside的内容可用作文章的侧栏
- `<fig caption>`标签定义figure元素的标题
- `<figure>`标签用于对元素进行组合，使用fig caption 元素为元素组添加标题
- `<time>`标签定义日期或时间

###  html标记`<pre>`...`</pre>`表示

`<pre>`是预格式化标记，被包围在pre元素中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体。

###  html5新增内容

html5增添了不少新标签和新属性，能使页面更优化，代码更简洁

1. HTML5引入canvas标签，通过canvas，用户可以动态地生成各种图形图像、图表及动画。canvas标签还能够配合JavaScript利用键盘来控制图形图像
2. 在HTML5中包含Web Forms 2.0，用来描绘如何进行页面表格操作。其中最大的特点就是“表格确认”
3. HTML5中为新元素和现有的元素提供更多的API，旨在改进页面程序开发和增加HTML4所缺乏的特性。比如，一个视频和音频方面的API将与`<audio>` 和 `<video>`元素一起使用，它将提供视频和音频回放功能，而无需依赖第三方程序，比如Flash
4. HTML5中的User Interaction用来描述页面内容交互工作的新方式。它的content editable属性可以让开发者决定，页面哪部分内容允许进行用户更改，这对于wiki类的网站更为有用。
5. HTML的主要任务是描述页面的架构，例如在`<p>...</p>`元素之间的文本内容，HTML将告诉浏览器这些文本是一个段落

###  HTML5新增的属性有哪些？

HTML5新增的属性有auto compelete、min、max、multiple、pattern和step。还有list属性与datalist元素配合使用；datalist元素与autocomplete属性配合使用。multiple属性允许一次上传多个文件；pattern属性用于验证输入字段的模式，其实就是正则表达式。step属性规定输入字段的合法数字间隔，step属性可以与max，min属性配合使用，以创建合法值的范围

为input、button元素增加formaction、formenctype、formmethod、formnovalidate和formtarget属性，用户重载form元素的action、enctype、method、novalidate和target属性。为fieldset元素增加disabled属性，可以把它的子元素设为disabled状态。

为input、button、form增加novalidate属性，可以取消提交时进行的有关检查，表单可以被无条件地提交

###  HTML5中如何使用XHTML的语法吗？

可以，HTML5向下兼容所有存在的HTML语法。

通过不同的头部声明DTD来设置怪异模式和标准模式。标准模式下，HTML4.0提供了三种DOCTYPE（DOCument TYPE，文档类型），XHTML1.0提供了三种类型，它们是transitional（过渡型）、strict（严格型）、frameset（框架型）。XHTML可以理解为HTML+XML，就是用XML的语法来规范HTML。

###  写出几条XHTML规范的内容

1. 所有的标记都必须要有一个相应的结束标记。
2. 所有标签的元素和属性的名字都必须使用小写
3. 所有的XML标记都必须合理嵌套
4. 所有的属性必须用引号“”
5. 所有的<和&特殊符号都要用编码表示

###  HTMl元素的分类及其特点

1. HTML元素分为块级元素和行内元素
   - 块级元素：dl、div、form、h1-h6、p、ul等
   - 行内元素：a、br、input、span、select等

2. 块级元素和行内元素的特点：
   - 块级元素的特点：总是在新行上开始；高度、行高及外边距和内边距可以控制；宽度默认是它的容器的100%；可以容纳内联元素和其他块元素。
   - 行内元素特点：和其他元素都在一行上；高和外边距不可变；宽度就是它的文字和图片的宽度，不可改变；内联元素只能容纳文本或者其他内联元素。



##  HTML结构

###  请用HTML5标签写一个符合语义化的页面，页面有导航栏、页眉、页脚、文字内容以及图片内容。

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Page title</title>
    </head>
    <body>
        <header>
            <h1>Page title</h1>
        </header>
        <nav><!--Navigation--></nav>
        <section id="intro">
            <!-- Introduction -->
        </section>
        <section>
            <!-- Main content area -->
        </section>
        <aside>
            <!-- Sidebar -->
        </aside>
        <footer>
            <!-- Footer -->
        </footer>
    </body>
</html>
   
```

## HTML布局

###  实现布局，side左边宽度固定，main右边宽度自适应

```html
<div class="main">
    <div class="content">
        主栏1内容区内容区内容区内容区内容区内容区内容区
    </div>
    <div class="side">
        内容区内容区内容区内容区内容区内容区内容区
    </div>
</div>
```

```css
.main{
    float: right;
    width:100%;
    margin-left:-220px;
}
.content {
    margin-left:220px;
}
.side{
    float: left;
    width:200px;
}
```

###  实现布局，两列和左边宽度自适应，右边宽度固定为200px

```html
<div style="width:90%;margin:0 auto">
    <div style="width:200px;float:right;">
        这是右侧的内容
    </div>
    <div style="margin-right:210px;">
        这是左侧的内容，宽度自适应
    </div>
</div>
```

##  HTML音频与视频

###  请用代码`<video>`标签的使用方法

方法一：`<video src="test.mp4">您的浏览器不支持video标签</video>`

方法二：`<video><source src="test.3gp">您的浏览器不支持video标签</video>`

###  如何在HTML5页面中嵌入音频？

HTML5包含嵌入音频文件的标准方式，支持的格式包括MP3、wav和ogg

```html
<audio controls>
    <source src="1.mp3" type="audio/mpeg" />
</audio>
```

###  HTML5有哪些不同类型的存储？

HTML5支持本地存储，速度快而且安全，在之前版本中是通过Cookie实现的。

有两种不同的对象可用来存储数据

- localStorage，适用于长期存储数据，浏览器关闭后数据不丢失；
- sessionStorage，存储的数据在浏览器关闭之后自动删除。

###  HTML5应用程序缓存为应用带来什么优势？

应用程序缓存为应用带来三个优势。

离线浏览——用户可在应用离线时使用它们；

速度——已缓存资源加载得更快

减少服务器负载——浏览器将只从服务器下载更新过或更改过的资源



##  上传

###  请写出可以实现上传且只能上传图片的标签

HTML自带一个上传文件控件：

`<input type="file" name="uploadFile" />`

再给input标签添加一个accept=“image/*”的属性就只能上传图片了

###  请写一段JavaScript代码，实现input type=“file”文件上传实例的代码

```html
<html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <meta http-equiv="Content-Type" content="text/html;charset=utf-8" />
        <style type="text/css">
            ._box {
                position:relative;
                width:119px;
                height:37px;
                background-color:#53AD3F;
                background-image:url(images/bg.png);
                background-repeat:no-repeat;
                background-position:0 0;
                background-attachment: scroll;
                line-height:37px;
                text-align:center;
                color:white;
                cursor:pointer;
                overflow:hidden;
                z-index:1;
            }
            ._box input {
                position:absolute;
                width:119px;
                height:40px;
                line-height:40px;
                font-size:23px;
                opacity:0;
                filter: "alpha(opacity=0)";
                filter: alpha(opacity=0);
                -moz-opacity:0;
                left:-5px;
                top:-2px;
                cursor:pointer;
                z-index:2;
            }
        </style>
        <title>js实现input file 文件上传</title>
    </head>
    <body>
        <form id="form1" runat="server" method="post" enctype="multipart/form-data">
            <div>
                <div class="_box">
                    <input type="file" name="_f" id="_f" />
                    选择图片
                </div>
            </div>
    </body>
</html>
  //用一个不透明度为0的<input type="file" />盖在让用户可见的标签上，让用户单击
```

用width height line-height font-size来控制`<input type="file" />`右侧浏览器按钮的大小。用left top（right、bottom）来控制右侧浏览器按钮的位置，可以设置为负值。用z-index来设置它们的覆盖层关系。Form必须有enctype=“multipart/form-data”标记才能上传文件。

##  文本

###  写出中英文强制转换的代码，以及文字超长显示的代码。

1. word-break：break-all；只对英文起作用，以字母作为换行依据。
2. word-wrap：break-word；只对英文起作用，以单词作为换行依据。
3. white-space：pre-wrap；只对中文起作用，强制换行。
4. white-space：nowrap；强制不换行，都起作用。
5. white-space：nowrap；over-flow：hidden；text-overflow：elipsis；不换行，超出部分隐藏且以省略号形式出现。

###  如下代码：`<div>这是div中的内容</div>`，如何得到div元素中文本的内容？如何清空div元素中的文本？

$("div").text();获取中间的文本，不包括HTML标签

$("div").html();获取中间的所有内容、

$("div").empty();清空div元素中的文本。

###  font-size：62.5%，解释一下如此设计字体大小的原因。

在网页设计中我们经常看见`body{font-size:62.5%}`这样的设置，这主要是为了方便em与px相互转换，em的初始值为1em=16px，显然这样的话，1.2em=19.2px，可是我们在设置时很少看见19.2px这样表示的大小，也就是在用px表示大小时数值是不带小数位的。当设置了`body{font-size:62.5%}`时，则1em = 16px*62.5% = 10px，1.2em=12px，这样会使页面更精确。

###  如下代码：

```html
<div id="mydiv">
    <h2>
        通过Ajax改变文本
    </h2>
</div>
<button id="b01" type="button">
    改变文本
</button>
```

（1）使用$(select).load(url)把HTML文本内容改为XX.txt内容。

（2）使用$.ajax(option)把HTMl文本内容改为XX.txt内容

1. ```javascript
   $(document).ready(function（) {
       $("#b01").click(function() {
           $("#mydiv").load("/jQuery/xx.txt");
       })
   }）
   ```

2. ```javascript
   $.ajax({
       type:"POST",
       url:"xx.txt",
       success: function(msg) {
           $("#id").txt(msg);
       }
   })
   ```



##  模式

###  什么是DOCTYPE？如何触发严格模式与混杂模式，这两种模式有什么区别？

DOCTYPE（是 DOCument TYPE 的简写，即文档类型）是一组机器可读的规则，它们指示(X)HTML文档中允许有什么，不允许有什么。DOCTYPE正是用来告诉浏览器使用哪种DTD，一般放在(X)HTML文档开头表示声明，用以告诉其他人这个文档的类型风格。

触发：根据不同的DTD触发，如果没有声明，那么默认为混杂模式。

区别：严格模式是浏览器根据Web标准去解析页面，是一种要求严格的DTD，不允许使用任何表现层的语法， 如`<br/>`，混杂模式则是一种向后兼容的分析方法。

##  HTML5页面

###  如何触发页面 reflow，repaint？

**什么是 repaint 和 reflow？**

一个页面由两部分组成：
DOM：描述该页面的结构
render：描述 DOM 节点 (nodes) 在页面上如何呈现

当 DOM 元素的属性发生变化 (如 color) 时， 浏览器会通知 render 重新描绘相应的元素，此过程称为 repaint。

如果该次变化涉及元素布局 (如 width)， 浏览器则抛弃原有属性，重新计算并把结果传递给 render 以重新描绘页面元素， 此过程称为 reflow。

这两个过程是很耗费浏览器性能的，从 IE 系列和 Chrome 渲染页面速度上的差距即可看出渲染引擎计算对应值和呈现并不一定高效， 而每次对元素的操作都会发生 repaints 或 reflow，因此编写 DOM 交互时如果不注意就会导致页面性能低下。

页面渲染的过程如下:

1.解析HTML代码并生成一个 DOM 树。

2.解析CSS文件，顺序为：浏览器默认样式->自定义样式->页面内的样式。

3.生成一个渲染树（render tree）。这个渲染树和DOM树的不同之处在于，它是受样式影响的。它不包括那些不可见的节点。

4.当渲染树生成之后，浏览器就会在屏幕上“画”出所有渲染树中的节点。

**什么情况下会触发浏览器的repaint/reflow?**

除了页面在首次加载时必然要经历该过程之外，还有以下行为会触发这个行为：

1. DOM元素的添加、修改（内容）、删除( Reflow + Repaint)
2. 仅修改DOM元素的字体颜色（只有Repaint，因为不需要调整布局）
3. 应用新的样式或者修改任何影响元素外观的属性
4. Resize浏览器窗口、滚动页面
5. 读取元素的某些属性（offsetLeft、offsetTop、offsetHeight、offsetWidth、 scrollTop/Left/Width/Height、clientTop/Left/Width/Height、 getComputedStyle()、currentStyle(in IE))

###   如何将一个表单中的值同时提交到两个页面？

```javascript
<script>
    function send_2page_f(formname,page1,target1,page2,target2) {
    with(eval("document." + formname)) {
        action=page1;
        target=target1;
        submit();
        action=page2;
        target=target2;
        submit();
    }
}
</script>
<form name="form">
    <input type="button"
	onclick='send_2page_f("form","01.asp","01","02.asp","02")' value="提交">
</form>
```

##  Canvas

getContext() 方法返回一个用于在画布上绘图的环境。

Graphics是java绘图的核心类，它可以支持两种绘图方式：一种是基本的绘图，如画线、矩形、圆等；另一种是画图像，主要用于动画制作。

Canvas API(画布)用于在网页实时生成图像，并且可以操作图像内容，基本上它是一个可以用JavaScript操作的位图（bitmap）

Canvas对象表示一个HTML画布元素`<canvas>`。它没有自己的行为，但是定义了一个API支持脚本化客户端绘图操作。你可以直接在该对象上指定宽度和高度，但是，其大多数功能都可以通过CanvasRenderingContext2D对象获得。这是通过Canvas对象的getContext()方法并且把直接量字符串“2d”作为唯一的参数传递给它而获得的。

###  写出Canvas中画圆的代码，直径为150px，边框宽度为5px。

```html
<!DOCTYPE html>
<html>
    <body>
        <canvas id="myCanvas" width="200" height="200" style="border:2px solid blue">您的浏览器不支持</canvas>
    </body>
    <script type="text/javascript">
        var c=document.getElementById("myCanvas");
        var cxt=c.getContext("2d");
        cxt.fillStyle="#FF0000";
        cxt.beginPath();
        cxt.arc(100,100,75,0,Math.PI*2,true);
        cxt.closePath();
        cxt.fill();
    </script>
</html>
```

##  媒体查询

###  `<meta name="viewport" content="width=device-width, minimum-scale=1.0, maximum-scale=10 "/>` 解释这个标签行的作用

网页手机Wap2.0网页的head里加入这条元标签，在iPhone的浏览器中，页面将以原始大小显示，并不允许缩放。

width ——viewport的宽度；

height ——viewport的高度；

initial-scale ——初始的缩放比例；

minimum-scale ——允许用户缩放到的最小比例；

maximum-scale —— 允许用户缩放到的最大比例；

user-scalable ——用户是否可以手动缩放。

###  写出media type的几种使用方法。

方法一:`<link href= "style.css" media="screen print" ...`

方法二：`< ? Xml-stylesheet media="screen" href="style.css"...`

方法三：`@import url("style.css") screen;`

方法四：`<style media="screen"> @import url("style.css") </style> `

方法五：`media screen{ Selector {rules} }`

##  媒体调用标签

###  请写出可以调用手机照相机的标签

```html
<input type="file" accept"audio/*;capture=microphone"/>
```

###  标签代码调用大全

关键描述调用标签：

```html
<meta name="keywords" content="{dede:field name='keywords'/}">
<meta name="description" content="{dede:field name='description' function='html2text(@me)'/}">
模板路径调用标签：{dede:field name='templeturl'/}
网站标题调用标签：{dede:global name='cfg_webname'/}
栏目导航调用标签：<a href="/">首页</a>
{dede:channel type='top' row='8' currentstyle="<li class='thisclass'><a href='~typelink~'>~typename~</a></li>"}
<li><a href='[field:typelink/]' target="_blank">[field:typename/]</a></li>
{/dede:channel}
指定栏目调用标签：{dede:one-type typeid='ID'}[field:typename/]{/dede:onetype}
频道栏目调用标签：{dede:channel type='self'} <li><a href='[field:typelink/]'>[field:type-name]</a></li>{/dede:channel}
友情链接调用标签：{dede:flink row='24' linktype=2/}
网站版权调用标签：{dede:global name='cfg_powerby'/}
网站备案调用标签：{dede:global name='cfg_beian'/}
当前栏目名称调用标签：{dede:field name='typename'/}
当前位置调用标签：{dede:field name='position'/}
列表文章调用标签：{dede:list pagesize='8'}{/dede:list}
栏目链接调用标签：[field:typelink function='str_replace("a", "a class=ulink ", @me)'/]
作者链接调用标签：[field：writer /]
列表单击调用标签：[field:click /]
列表评论调用标签：[field:post-num /]
查阅全文调用标签：<a href="[field:arcurl/]">查阅全文...</a>
```







#  CSS3

##  关于CSS3

###  谈一下CSS Reset

CSS Reset，我们可以把它叫做css重设，也有人叫css复位、默认css、css重置等。css重设就是由于各种浏览器解释css样式的初始值有所不同，导致设计师在没有定义某个css属性时，不同的浏览器会按照自己的默认值来为没有定义的样式赋值，所以我们要先定义好一些css样式，来让所有浏览器都按照同样的规则解释css，这样就能避免发生以下问题：

1. 标题部分采用的是line-height来实现标题中文字的间距，由于中英文有别，一般我们在实际项目中h2的大小设为14px，高度设为30px。而bootstrap或normalize.css面对的都是英文字体，所以我们默认设置的字体比中文的大，而且间距也比较大。
2. 根据我们常用的需求给ul添加两个class样式，一个为has-style，顾名思义就是拥有列表样式，因为我们在一开始重置了没有样式，但是偶尔我们又确实需要前面的那个小圆点，所以就用这个class来还原；另一个inline-style，即li浮动，一般和clearfix结合使用以清除浮动。
3. 对于normalize.css不支持的IE6，我们添加了class用以支持。

###  请解释浏览器是如何根据css3选择器选择对应元素的？

IE-CSS3.js下载页面的每一个样式文件并解析它的CSS3伪选择器。如果一个选择器被找到，他就会替换为同名的CSS class。比如： div：nth-child（2）将会变成div._IEcss-nth-child-2.接着，Robert Nyman的DOMAssistant用于寻找匹配元素CSS3选择器的DOM节点，然后将相应的CSS类添加给它。最终，元素的样式表会被新的版本替代实现用CSS3选择器对相应元素添加对应的样式。

###  排App时是怎么切图的？

排版时切图可使用的软件很多，以下说一款PS切图。打开photoshop，左边工具栏有个小刀形状的工具，叫“切片工具”，用小刀按照想要的样子在图片上切割，做好之后，点“文件-存储为Web所用格式”，选择路径后单击“确定”按钮，之后再所选路径下有一个新的文件夹和一个HTML文件，文件夹里是切好的图片

##  css3新增内容

###  至少说出5个css3新增内容

1. css3圆角表格，对应属性：`border-redius`
2. 以往对网页上的文字加特效只能用filter属性，但是在css3
3. 中专门制定了一个加文字特效的属性，而且不止加阴影这种效果。对应属性：`fonteffect`
4. 丰富了对链接下划线的样式，有波浪线、点线、虚线等，可以对下划线的颜色和位置进行任意改变，对应属性：`text-underline-style; text-underline-color; text-underline-mode; text-underline-position`
5. 在文字下画几个点或打个圈以示重点，css3中加入了这项功能。对应属性：`font-emphasize-style; font-emphasize-position`
6. `Font-face`可以用来加载字体样式，而且它还能够加载服务器端的字体文件，显示客户端没有安装的字体

##  定位相关

###  关于元素的定位有哪些？其中对z-index样式的理解及z-index对不同浏览器默认的样式是什么？

position属性规定元素的定位类型，position属性有几个取值定义：statis、relative、absolute

- static：默认值。如果没有指定position属性，支持position属性的HTML对象都默认为static，可以这么理解，把HTML页面看作一个文档流，源代码中各个标签的先后位置就是它们所对应的对象的呈现次序，所有取值为static的对象都按照所编写的HTML标签的顺序依次呈现。
- relative：相对定位。这个属性值保持对象所在文档流中的位置，也就是说，它具有和static相同的呈现方式，它同样占有在文档流中的固定位置，后面的对象不会侵占或者覆盖；与static属性值不同是，它设置了relative的对象，可以通过top、left、right、bottom属性设定新的显示位置，这4个属性的取值是相对于文档流的前一个对象的，你可以自由设置这4个属性，偏移到新的位置而不对文档流中的其他对象产生任何影响，原来的页面呈现仍然会我行我素。
- absolute：绝对定位。和relative不同的是，这个属性值会将当前对象拖出文档流，后面的对象会占有原来的位置，也就是说，当前对象的呈现是独立显示的，但是它的位置在指定top、left、right、bottom任一属性之前仍是有继承性的，这时的4个属性的取值是相对于浏览器的，和文档流无关。属性值为absolute对象的z-index属性可以设置层叠显示的次序，它是直接有效的；而属性值为relative对象的z-index属性在设置时要小心，把当前对象的z-index设置为-1是不行的，必须设置为0以上，如果我们想让别的对象挡住它，只有将其他对象也设置position为relative，并将z-index属性取一个比它大的值即可。

z-index属性的默认值是0

元素可拥有负的z-index属性值，如z-index：-1

z-index属性无继承性

z-index属性在JavaScript中使用语法：object.style.zIndex="1"

几乎所有的主流浏览器都支持z-index属性

z-index在IE和Firefox下的默认值不同，在IE下z-index默认值为0；在Firefox下其默认值为auto

##  弹性盒布局

引入弹性盒布局模型的目的是提供一种更加有效的方式来对一个容器中的条目进行排列、对齐和分配空白空间。即便容器中条目的尺寸未知或是动态变化的，弹性盒布局模型也能正常工作。在该布局模型中，容器会根据布局的需要，调整其中包含的条目尺寸和顺序来最好地填充所有可用的空间。当容器的尺寸由于屏幕大小或窗口尺寸发生变化时，其中包含的条目也会被动态的调整。比如，当容器尺寸变大时，其中包含的条目会拉伸以占满多余的空白空间；当容器尺寸变小时，条目会缩小以防止超出容器的范围。弹性盒布局是与方向无关的。在传统的布局方式中，block布局是把块在垂直方向从上到下依次排列的；而inline布局则是在水平方向来排列的。弹性盒模型并没有这样内在的方向限制，可以由开发人员自由操作。

###  了解弹性盒模型属性

box-orient：设置或检索弹性盒模型对象的子元素的排列方式。

box-pack：设置或检索弹性盒模型对象的子元素的左右对齐方式。

box-align：设置或检索弹性盒模型对象的子元素的上下对齐方式。

box-flex：设置或检索弹性盒模型对象的子元素如何分配其剩余元素。

box-flex-group：设置或检索弹性盒模型对象的子元素的所属组。

box-ordinal-group：设置或检索弹性盒模型对象的子元素的显示顺序。

box-direction：设置或检索弹性盒模型对象的子元素的排列顺序是否反转。

box-lines：设置或检索弹性盒模型对象的子元素是否可以显示换行。

##  代码优化

###  请简化这段CSS代码

```css
abc {
    padding-left:50px;
    padding-top:10px;
    padding-bottom:5px;
    padding-right:15px;
}
```

padding属性的书写格式总共有以下几种。

1. padding：10px的意思是上下左右值全是10px。
2. padding：5px 10px的意思是上下为5px，左右为10px。
3. padding：1px 2px 3px 4px的意思是：上为1px，右为2px，下为3px，左为4px。
4. padding：5px 10px 7px的意思是：上为5px，左右为10px，下为7px。
5. padding后面4个值定义的顺序分别为：上、右、下、左，而padding-top或padding-bottom这种写法，只是单方面的定义了一个方向的值，这样写会增加CSS代码的长度，增加CSS样式的代码量，拖慢页面的加载速度。

###  请列出CSS代码的7个优化准则

1. 使用简单
2. 避免使用hack
3. 使用留白
4. 移除多余的结构和重设
5. 让CSS保证日后的维护
6. 记录工作（标记向导和样式表向导）
7. 压缩使用

##  边框背景

###  CSS3如何实现圆角、阴影效果？

第一种方法是添加背景图片，CSS3可以允许一个元素有多个背景图像，这样给一个元素添加4个1/4圆的背景图像分别位于四个角就可以实现圆角效果了

```css
.box {
    background-img:url(/img/top-left.gif), url(/img/top-right.gif), url(/img/bottom-left.gif), url(/img/bottom-right.gif);
    background-repeat:no-repeat,no-repeat,no-repeat,no-repeat;
    //定义4幅图分别显示在4个角上
    background-position: top left, top right, bottom left, bottom right;
}
```

第二种方法，直接用CSS实现，不需要使用图片。

```css
.box {
    -moz-border-radius: 1em;
    -webkit-border-radius: 1em;
    border-radius: 1em;
}
```

CSS3的box-shadow属性可以直接实现阴影效果。

```css
img {
    -webkit-box-shadow:3px 3px 6px #666;
    -moz-box-shadow:3px 3px 6px #666;
    box-shadow:3px 3px 6px #666;
}
```

这个属性的4个参数是：垂直偏移、水平偏移、投影的宽度（模糊程度）、颜色

###  box-sizing属性有哪些，各代表什么含义？

box-sizing属性允许以特定的方式定义匹配某个区域的特定元素。

content-box：padding 和 border不被包含在定义的width和height之内。对象的实际宽度等于设置的width、border、padding以及margin之和，即（Element width = width + border + padding + margin），此属性表现为标准模式下的盒模型。

border-box：padding和border被包含在定义的width和height之内，对象的实际宽度就等于设置的width值，即使定义有border和padding也不会改变对象的实际宽度，即（Element width = width），此属性表现为怪异模式下的盒模型。

##  多列布局

CSS3中新出现的多列布局（multi-column）是传统HTML页面中块状布局模式的有力扩充。这种新语法能够让Web开发人员轻松地让文本呈现多列显示。

###  宽度自适应三栏的布局方式有哪些？

1. 绝对定位法 左右两栏采用绝对定位，分别固定于页面的左右两侧，中间的主题栏用左右margin值撑开距离，于是实现了三栏的自适应布局。

2. 自身浮动法 此方法代码最简单，应用了标签浮动跟随的特性。左栏左浮动，右栏右浮动，主体之间放后面，就实现了自适应

   

###  写出三列布局的CSS，HTMl如下，要求不改变HTML结构，用CSS分别实现，按照ABC排列、按照BAC排列、按照CBA排列。其中AB为定宽，尽量让B自适应宽度，不能使用CSS hack

```html
<div id="A"></div>
<div id="B"></div>
<div id="C"></div>
```

CSS三列布局走出HTML布局阴影，两端固定宽度，中间自适应结构

```html
<div class="wrap">
    <div class="main">
        <div id="A"></div>
    </div>
    <div id="B"></div>
	<div id="C"></div>
</div>
//CSS代码
.wrap {
	width:500px;
	border: 1px solid;
	overflow:hidden;
}
.main {
	float:left;
	width:100%;
}
#A {
	height: 50px;
	margin: 0 150px;
	background-color:#f60;
}
#B {
	float:left;
	width:150px;
	height: 50px;
	margin-left: -100%;
	background-color:#6f0;
}
#C {
	float:left;
	width:150px;
	height: 50px;
	margin-left: -150px;
	background-color:#06f;
}
```

## 响应式布局

###  谈谈你对响应式布局的看法？

响应式布局有缺点，也有优点。

优点：面对不同分辨率设备，灵活性强，能够快捷地解决多设备显示适应问题。

缺点：兼容各种设备时所需工作量大、效率低下、代码累赘，会隐藏无用的元素，加载时间延长，其实这是一种折衷性质的设计解决方案，由于多方面因素影响而达不到最佳效果，在一定程度上改变了网站原有的布局结构，会出现用户混淆的情况。

