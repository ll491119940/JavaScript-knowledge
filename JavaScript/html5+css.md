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

###  分别使用2个、3个、5个div画出一个大的红十字

用div创建一个矩形





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