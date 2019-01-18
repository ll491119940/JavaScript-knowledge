# JavaScript

## 关于javascript

- JavaScript是基于对象的、事件驱动的脚本程序设计语言

- ` <script  language="javascript"> `用来告诉浏览器这是用JavaScript写的程序

- Ajax的全称是 Asynchronous JavaScript and XML

## 字符串

- 扩展JavaScript中原生的String对象，用prototype添加方法

``` javascript
String.prototype.reverse = function() {
    return this.split("").reverse().join("");
}
```

### chartAt()与charCodeAt() ###

参数：*基于**0的字符位置***

**chartAt()**以单字符字符串的形式返回给定位置的那个字符。而**charCodeAt()**返回的是字符编码。

### concat()(数组中也有该方法) ###

参数：*一个或多个字符串*

将一个会多个字符串拼接起来，当然更常用的是使用 “+” 进行拼接

### substring()与slice()(数组中也有此方法) ###

参数：*指定子字符串的开始位置*，*子字符串到哪里结束*

作用：创建新的子字符串（可以理解为字符串截取）

### substr() ###

参数：*指定子字符串的开始位置*，*返回的子字符串的字符个数*

作用：创建新的子字符串（可以理解为字符串截取）

### repeat()（ES6新增） ###

参数：*数字（表示重复的次数）*

作用：将原字符串重复n次

如果传入负数，则报错，传入小数和`NaN`等同于传入0

```javascript
var stringValue = "hello world"; 
alert(stringValue.slice(3));          //"lo world" 
alert(stringValue.substring(3));      //"lo world" 
alert(stringValue.substr(3));         //"lo world" 
alert(stringValue.slice(3, 7));       //"lo w" 
alert(stringValue.substring(3,7));    //"lo w" 
alert(stringValue.substr(3, 7));      //"lo worl" 
/*repeat()*/
var a = 'he';
var b = a.repeat(3);
console.log(`${a}---${b}`); /		  //"he---hehehe"
```

当给这四个方法传入负值的时候，三个的表现不同：

- slice()会将传入的负值与字符串的长度相加
- substr()会将**第一个**位置的**负值**参数加上字符串长度后转为正数，而**第二个**位置的**负值**将转化为0
- substring()会把所有的负参数转化为0
- repeat()会报错

### indexOf()和lastIndexOf()(数组中也有该方法) ###

参数：*要搜索的子字符串*，*开始搜索的位置（可选）*

搜索给定的子字符串，如果找到则返回位置，否则返回-1

```javascript
var stringValue = "hello world"; 
alert(stringValue.indexOf("o"));             //4 
alert(stringValue.lastIndexOf("o"));         //7
```

这两个方法在搜索到第一个匹配的子字符串后就停止运行，所以如果想找到字符串中所有的
子字符串出现的位置，可以循环调用`indexOf`或`lastIndexOf`。

```javascript
var stringValue = "Lorem ipsum dolor sit amet, consectetur adipisicing elit"; 
var positions = new Array(); 
var pos = stringValue.indexOf("e"); 
 
while(pos > -1){ 
    positions.push(pos); 
    pos = stringValue.indexOf("e", pos + 1); 
} 
     
alert(positions);    //"3,24,32,35,52"
```

### **ES6新增**includes()、startsWith()、endsWith() ###

- includes()：返回布尔值，表示是否找到了参数字符串
- startsWith()：返回布尔值，表示参数字符串是否在源字符串的头部
- endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部

这三个方法的参数与`indexOf()`，`lastIndexOf()`一样

```
var s = 'Hello world';
s.startsWith('world',6);	// true
s.endsWith('Hello',5);		// true
s.includes('Hello',6);		//false
```

**注意：**
使用第2个参数n时，`endsWith`的行为与其他两个方法有所不同。它针对**前面**n个字符，而其他两个方法针对从第n个位置开始直到字符串结束的字符。

###  trim() 去掉空格 ###

ES5中新增`trim()`方法用于去除字符串的左右空格，**该方法会创建一个字符串的副本，不会改变原有的字符串**，此外，Firefox 3.5+、Safari 5+
和 Chrome 8+还支持非标准的 trimLeft()和 trimRight()方法，分别用于删除字符串开头和末尾的
空格。

其实去空格可以使用正则去匹配的去掉，这里写一个去空格函数

```javascript
/*trim	去掉空白
str要处理的字符串		
[type] 	类型：l 去除左边的空白	r去除右边空白	b去掉两边的空白		a去除所有空白*/
function trim (str,type) {
	var type=type||"b";
	if(type=="b"){
		return str.replace(/^\s*|\s*$/g,"");
	}else if(type=="l"){
		return str.replace(/^\s*/g,"");
	}else if(type=="r"){
		return str.replace(/\s*$/g,"");
	}else if(type=="a"){
		return str.replace(/\s*/g,"");
	}
}
```

### 字符串大小写转换 ###

 **toLowerCase()、toLocaleLowerCase()、toUpperCase()和 toLocaleUpperCase() **

### match() ###

参数：*一个正则表达式或RegExp对象*

返回一个数组。在字符串上调用这个方法本质上与调用RegExp的exec()方法相同。

```javascript
var text = "cat, bat, sat, fat";  
var pattern = /.at/; 
 
//与 pattern.exec(text)相同 
var matches = text.match(pattern);         
alert(matches.index);             //0 
alert(matches[0]);                 //"cat" 
alert(pattern.lastIndex);          //0
```

### search() ###

参数：*一个正则表达式或RegExp对象*

返回字符串中第一个匹配项的索引，如果没有找到，则返回-1

```javascript
var text = "cat, bat, sat, fat";  
var pos = text.search(/at/); 
alert(pos);   //1
```

### replace() ###

参数：*一个RegExp对象或者一个字符串（这个字符串不会被转换成正则表达式）*，*一个字符串或一个函数*

利用`replace()`进行替换的时候，如果传入的是字符串，则只会替换第一个子字符串，要想替换所有的子字符串，则需要传入一个正则表达式，而且要指定全局（g）标志

```javascript
var text = 'cat , bat , sat , fat';
var result = text.replace('at','ond');
console.log(result); // =>'cont , bat , sat , fat'

result = text.replace(/at/g,'ond');
console.log(result); //=>'cont , bont , sont , font'
```

该方法并不改变调用它的字符串本身，只是返回一个新的替换后的字符串。

**当第二个参数为函数时**函数的返回值作为替换字符串。与第二个参数是字符串一样，如果第一个参数是正则表达式，并且全局匹配，则这个函数的方法将被多次调用，每次匹配都会被调用。

该函数的参数：

- match：匹配的子串
- p1,p2…：假如`replace()`方法的第一个参数是RegExp对象，则代表第n个括号匹配的字符串。
- offset：匹配到的子字符串在原字符串中的偏移量。（比如，如果原字符串是“abcd”，匹配到的子字符串时“bc”，那么这个参数是1）
- 被匹配的原字符串

```javascript
function replacer(match , p1 , p2 , p3 , offset , string){
	// p1 is nondigits, p2 digits, and p3 non-alphanumerics
    console.log(`${match}
				 ${p1}
				 ${p2}
				 ${p3}
				 ${offset}
				 ${string}`); 
	/* => abc12345#$*%
         abc
         12345
         #$*%
         0
         abc12345#$*%"	*/		 
    console.log([p1, p2, p3].join(' - ')); // => "abc - 12345 - #$*%"
    return [p1, p2, p3].join(' - ');
}
var newString = 'abc12345#$*%'.replace(/([^\d]*)(\d*)([^\w]*)/, replacer); // =>"abc - 12345 - #$*%"
```

### split() ###

参数：*用于分隔字符串的分隔符*，*数字（可选，用于指定数组的大小）*

作用：基于指定的分隔符将一个字符串分割成多个子字符串，并将结果放在一个**数组**中，分隔符可以是字符串，也可以是RegExp对象

```javascript
var color = 'red,blue,yellow,black';
var color1 = color.split(',');		// =>['red','blue','yellow','black']
var color2 = color.split(',',2);	// =>['red','blue']
var color3 = color.split(/[^\,]+/); // =>["", ",", ",", ",", ""]
```

最后一个调用`split`的时候，出现了前后的两个空白，是因为通过正则表达式指定的分隔符出现在了字符串的开头和结尾。

### localeCompare() ###

这个方法用于比较两个字符串，并返回下列值中的一个：

- 如果字符串在字母表中应该排在字符串参数之前，则返回负数（大多情况下为-1）
- 如果相等，则返回0
- 如果排在字符串参数之前，则返回正数（大多数情况下为1）

### fromCharCode() ###

String构造函数的一个静态方法

参数：*一个或多个字符串编码*

作用：将接收到的一个或多个字符串编码**转换**成一个字符串，这个方法与实例方法`charCodeAt()`执行**相反**的操作。

```javascript
/*fromCharCode*/
String.fromCharCode(104,101,108,108,111);	// =>hello
/*charCodeAt*/
let s = 'hello';
for(let i=0;i<s.length;i++){
  console.log(`${s[i]}----${s[i].charCodeAt()}`);
}
/*
"h----104"
"e----101"
"l----108"
"l----108"
"o----111"
*/
```

最后写一个字符串与数组方法应用的一个例子，熟悉它们方法的话很简单，不熟悉就会觉得有点儿乱。

```javascript
let s = 'hello';
let news = s.split('').reverse().join('');
console.log(news); // => "olleh"
```

## 变量 ##

###  有var和没有var的区别

在函数内部，有var声明的是局部变量，没有var的是全局变量。

函数定义有两种方式，一种是函数定义表达式，一种是函数声明语句。

函数声明语句“被提前”到外部脚本或外部函数作用域的顶部。

而以表达式方式定义的函数在函数定义之前无法调用

###  undefined变量和undeclared变量

undefined是JavaScript语言类型，而undeclared是一种JavaScript语法错误

##  数据类型 ##

###  JavaScript中的数据类型

####  原始数据类型

- Undefined类型 只有一个值，就是undefined
- Null类型 只有一个值，null
- Boolean类型 非0即真，0可以看成false
- Number类型 非数字NaN（Not a Number）是一个特殊的值
- String类型 赋值时双引号和单引号都一样
#### 复合数据类型 ####

- function函数类型

- object对象类型

- array数组类型

##  window的属性和方法

- alter中换行使用\n
- 通过改变DIV的innerHTML属性值动态改变页面内容
- document.write是在页面里写内容，会覆盖页面内容；innerHTML是DOM元素对象的一个属性，用于设置内容
- innerHTML设置或获取位于对象起始和结束标签内的HTML；outerHTML设置或获取对象及其内容的HTML形式
- 刷新页面的方法：`location.reload([bForceGet])`，`location.replace(URL)`
## 元素

###  JavaScript中获取元素的方式

- `document.getElementById()`用来获得名为ID值的元素
- `document.myform.xxx`按照层次结构来获取
- `document.getElementsByName()`用于获得所有名字相同的元素
- ` document.getElemntsByTagName("标签名"); ` 根据标签名获取该标签标示的节点对象数组

###  创建、查找、删除DOM节点

- 创建DOM节点 ` var odiv = document.createElement('div');` 
- 查找DOM节点` getElementById();` 
- 删除DOM节点` document.body.removeChild(oP)` 
- 添加DOM节点` od.appendChild(doiv);`

##  表达式

- null == undefined

###  “==” 和 “===” 的区别

- “==”直接比较两个变量的值，在对不同类型比较时会做出相应的类型转换
- “===”比较两个变量的值和类型

### JS中Number()、parseInt()和parseFloat()的区别 ###

**三者的作用：** 
Number(): 可以用于任何数据类型转换成数值； 
parseInt()、parseFloat(): 专门用于把字符串转换成数值

#### Number( ): ####

（1）如果是Boolean值，true和false将分别转换为1和0。 
（2）如果是数字值，只是简单的传入和返回。 
（3）如果是null值，返回0。 
（4）如果是undefined,返回NaN。 
（5）如果是字符串，遵循下列规则： 
如果字符串截去开头和结尾的空白字符后，不是纯数字字符串，那么最终返回结果为NaN。 

如果是字符串中只包含数字（包括前面带正号或负号的情况），则将其转换为十进制数值，即“1”变成1，“123”会变成123，而“011”会变成11（前导的零被忽略了）； 

如果字符串中包含有效的浮点格式，如“1.1”，则将其转换为对应的浮点数值（同样也会忽略前导零）； 

如果字符串中包含有效的十六进制格式，例如”0xf”，则将其他转换为相同大小的十进制整数值； 

如果字符串是空的（不包含任何字符），则将其转换为0； 

如果字符串中包含除上述格式之外的字符，则将其他转换成NaN. 

（6）如果是对象，则调用对象的valueOf()方法，然后依照前面的规则转换返回的值。如果转换的结果是NaN，则调用的对象的toString()方法，然后再次依照前面的规则转换返回的字符串值。

#### parseInt( )： ####

` parseInt(string, radix);`

parseInt()函数可以将字符串转换成一个整数，与Number()函数相比，parseInt()函数不仅可以解析纯数字字符串，也可以解析以数字开头的部分数字字符串(非数字部分字符串在转换过程中会被去除)。 
（1）如果第一个字符不是数字字符或者负号，parseInt()就会返回NaN; 也就是说，用parseInt()转换空字符串会返回NaN。 

（2）如果第一个字符是数字字符，parseInt()会继续解析第二个字符，直到解析完所有后续字符或者遇到了一个非数字字符。 

（3）如果字符串以”0x”开头且后跟数字字符，就会将其当作一个十六进制整数。 

（4）如果字符串以”0”开头且后跟数字字符，就会将其当作一个八进制整数。 

（5）parseInt()函数增加了第二参数用于指定转换时使用的基数（即多少进制）。 

#### parseFloat( ): ####

与parseInt()一样，parseFloat()也可以解析以数字开头的部分数字字符串(非数字部分字符串在转换过程中会被去除)。与parseInt()不同的是，parseFloat()可以将字符串转换成浮点数；但同时，parseFloat()只接受一个参数，且仅能处理10进制字符串。 
（1）字符串中的第一个小数点是有效的，而第二个小数点就是无效的了，因此它后面的字符串将被忽略。 

（2）如果字符串包含的是一个可解析为整数的数（没有小数点，或者小数点后面都是零），parseFloat()会返回整数。

###  统计1-400亿之间的自然数中含有多少个1？



##  Math对象

###  请用JavaScript实现获取5个0~99之间不相同的随机数

- ` Math.random();` 结果为0~1之间的一个随机数
- ` Math.ceil(num);`参数num为一个数值，函数结果为num的向上取整
- ` Math.floor(num);` 参数num为一个数值，函数结果为num的整数部分
- ` Math.round(num);` 参数num为一个数值，函数结果为num四舍五入后的整数 ` Math.round(-11.5)=-11`
- ` document.write(Math.floor(Math.random()*10+1))`

###  求两个数的最大公约数

```javascript
function f (num1, num2) {
    for(var i = Math.min(num1,num2); i > 0; i--) {
        if(num1 % i == 0 && num2 % i == 0)
            return i;
    }
}
```

###  获取一个1~50的随机不重复数组



##  数组

###  属性和方法

####  属性

#####  Array.length #####

**`length`** 是`Array`的实例属性。返回或设置一个数组中的元素个数。该值是一个无符号 32-bit 整数，并且总是大于数组最高项的下标。

#####  Array.prototype #####

**Array.prototype**  属性表示 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array) 构造函数的原型，并允许您向所有Array对象添加新的属性

鲜为人知的事实：`Array.prototype` 本身也是一个 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)。

```js
Array.isArray(Array.prototype); 
// true
```

#### 创建一个数组: ####

```
    // 字面量方式:
    // 这个方法也是我们最常用的，在初始化数组的时候 相当方便
    var a = [3, 11, 8];  // [3,11,8];
    // 构造器:
    // 实际上 new Array === Array,加不加new 一点影响都没有。
    var a = Array(); // [] 
    var a = Array(3); // [,,] 
    var a = Array(3,11,8); // [ 3,11,8 ]
复制代码
```

##### ES6 Array.of()  返回由所有参数值组成的数组 #####

定义：返回由所有参数值组成的数组，如果没有参数，就返回一个空数组。

目的：Array.of() 出现的目的是为了解决上述构造器因参数个数不同，导致的行为有差异的问题。

```
    let a = Array.of(3, 11, 8); // [3,11,8]
    let a = Array.of(3); // [3]
复制代码
```

##### ES6 Arrary.from() 将两类对象转为真正的数组 #####

定义：用于将两类对象转为真正的数组（不改变原对象，返回新的数组）。

参数：

第一个参数(必需):要转化为真正数组的对象。

第二个参数(可选): 类似数组的map方法，对每个元素进行处理，将处理后的值放入返回的数组。

第三个参数(可选): 用来绑定this。

```
    // 1. 对象拥有length属性
    let obj = {0: 'a', 1: 'b', 2:'c', length: 3};
    let arr = Array.from(obj); // ['a','b','c'];
    // 2. 部署了 Iterator接口的数据结构 比如:字符串、Set、NodeList对象
    let arr = Array.from('hello'); // ['h','e','l','l','o']
    let arr = Array.from(new Set(['a','b'])); // ['a','b']
复制代码
```

------

#### 方法: ####

数组原型提供了非常多的方法，这里分为三类来讲，一类会改变原数组的值，一类是不会改变原数组，以及数组的遍历方法。

**改变原数组的方法(9个): **

```
    let a = [1,2,3];
    ES5:
     a.splice()/ a.sort() / a.pop()/ a.shift()/  a.push()/ a.unshift()/ a.reverse()
    ES6:
    a.copyWithin() / a.fill
复制代码
```

对于这些能够改变原数组的方法，要注意避免在循环遍历中改变原数组的选项，比如: 改变数组的长度，导致遍历的长度出现问题。

##### splice() 添加/删除数组元素 #####

定义： splice() 方法**向/从数组中添加/删除**项目，然后返回被删除的项目

语法： `array.splice(index,howmany,item1,.....,itemX)`

参数:

1. index：必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
2. howmany：可选。要删除的项目数量。如果设置为 0，则不会删除项目。
3. item1, ..., itemX： 可选。向数组添加的新项目。

返回值: 如果有元素被删除,返回包含被删除项目的新数组。

eg1:删除元素

```
    let a = [1, 2, 3, 4, 5, 6, 7];
    let item = a.splice(0, 3); // [1,2,3]
    console.log(a); // [4,5,6,7]
    // 从数组下标0开始，删除3个元素
    let item = a.splice(-1, 3); // [7]
    // 从最后一个元素开始删除3个元素，因为最后一个元素，所以只删除了7
复制代码
```

eg2: 删除并添加

```
     let a = [1, 2, 3, 4, 5, 6, 7];
    let item = a.splice(0,3,'添加'); // [1,2,3]
    console.log(a); // ['添加',4,5,6,7]
    // 从数组下标0开始，删除3个元素，并添加元素'添加'
     let b = [1, 2, 3, 4, 5, 6, 7];
    let item = b.splice(-2,3,'添加1','添加2'); // [6,7]
    console.log(b); // [1,2,3,4,5,'添加1','添加2']
    // 从数组最后第二个元素开始，删除3个元素，并添加两个元素'添加1'、'添加2'
复制代码
```

eg3: 不删除只添加:

```
    let a = [1, 2, 3, 4, 5, 6, 7];
    let item = a.splice(0,0,'添加1','添加2'); // [] 没有删除元素，返回空数组
    console.log(a); // ['添加1','添加2',1,2,3,4,5,6,7]
    let b = [1, 2, 3, 4, 5, 6, 7];
    let item = b.splice(-1,0,'添加1','添加2'); // [] 没有删除元素，返回空数组
    console.log(b); // [1,2,3,4,5,6,'添加1','添加2',7] 在最后一个元素的前面添加两个元素
复制代码
```

从上述三个栗子可以得出:

1. 数组如果元素不够，会删除到最后一个元素为止
2. 操作的元素，包括开始的那个元素
3. 可以添加很多个元素
4. 添加是在开始的元素前面添加的

##### sort() 数组排序 #####

定义: sort()方法对数组元素进行排序，并返回这个数组。

参数可选: 规定排序顺序的比较函数。

默认情况下sort()方法没有传比较函数的话，默认按字母升序，如果不是元素不是字符串的话，会调用`toString()`方法将元素转化为字符串的Unicode(万国码)位点，然后再比较字符。

```
    // 字符串排列 看起来很正常
    var a = ["Banana", "Orange", "Apple", "Mango"];
    a.sort(); // ["Apple","Banana","Mango","Orange"]
    // 数字排序的时候 因为转换成Unicode字符串之后，有些数字会比较大会排在后面 这显然不是我们想要的
    var	a = [10, 1, 3, 20,25,8];
    console.log(a.sort()) // [1,10,20,25,3,8];
复制代码
```

**比较函数的两个参数：**

sort的比较函数有两个默认参数，要在函数中接收这两个参数，这两个参数是数组中两个要比较的元素，通常我们用 a 和 b 接收两个将要比较的元素：

- 若比较函数返回值<0，那么a将排到b的前面;
- 若比较函数返回值=0，那么a 和 b 相对位置不变；
- 若比较函数返回值>0，那么b 排在a 将的前面；

对于sort()方法更深层级的内部实现以及处理机制可以看一下这篇文章[深入了解javascript的sort方法](https://juejin.im/entry/59f7f3346fb9a04514635552)

**sort排序常见用法**：

1. 数组元素为数字的升序、降序:

   ```
    var array =  [10, 1, 3, 4,20,4,25,8];
    // 升序 a-b < 0   a将排到b的前面，按照a的大小来排序的 
    // 比如被减数a是10，减数是20  10-20 < 0   被减数a(10)在减数b(20)前面   
    array.sort(function(a,b){
      return a-b;
    });
    console.log(array); // [1,3,4,4,8,10,20,25];
    // 降序 被减数和减数调换了  20-10>0 被减数b(20)在减数a(10)的前面
    array.sort(function(a,b){
      return b-a;
    });
    console.log(array); // [25,20,10,8,4,4,3,1];
   复制代码
   ```

2. 数组多条件排序

   ```
    var array = [{id:10,age:2},{id:5,age:4},{id:6,age:10},{id:9,age:6},{id:2,age:8},{id:10,age:9}];
        array.sort(function(a,b){
            if(a.id === b.id){// 如果id的值相等，按照age的值降序
                return b.age - a.age
            }else{ // 如果id的值不相等，按照id的值升序
                return a.id - b.id
            }
        })
     // [{"id":2,"age":8},{"id":5,"age":4},{"id":6,"age":10},{"id":9,"age":6},{"id":10,"age":9},{"id":10,"age":2}] 
   复制代码
   ```

3. 自定义比较函数，天空才是你的极限

类似的：**运用好返回值，我们可以写出任意符合自己需求的比较函数**

```
    var array = [{name:'Koro1'},{name:'Koro1'},{name:'OB'},{name:'Koro1'},{name:'OB'},{name:'OB'}];
    array.sort(function(a,b){
        if(a.name === 'Koro1'){// 如果name是'Koro1' 返回-1 ，-1<0 a排在b的前面
            return -1
        }else{ // 如果不是的话，a排在b的后面
          return 1
        }
    })
    // [{"name":"Koro1"},{"name":"Koro1"},{"name":"Koro1"},{"name":"OB"},{"name":"OB"},{"name":"OB"}] 
复制代码
```

##### pop() 删除一个数组中的最后的一个元素 #####

定义: pop() 方法删除一个数组中的最后的一个元素，并且返回这个元素。

参数: 无。

```
    let  a =  [1,2,3];
    let item = a.pop();  // 3
    console.log(a); // [1,2]
复制代码
```

##### shift() 删除数组的第一个元素 #####

定义: shift()方法删除数组的第一个元素，并返回这个元素。

参数: 无。

```
    let  a =  [1,2,3];
    let item = a.shift();  // 1
    console.log(a); // [2,3]
复制代码
```

##### push() 向数组的末尾添加元素 #####

定义：push() 方法可向数组的末尾添加一个或多个元素，并返回新的长度。

参数:  item1, item2, ..., itemX ,要添加到数组末尾的元素

```
    let  a =  [1,2,3];
    let item = a.push('末尾');  // 4
    console.log(a); // [1,2,3,'末尾']
复制代码
```

##### unshift() #####

定义：unshift() 方法可向数组的开头添加一个或更多元素，并返回新的长度。

参数:  item1, item2, ..., itemX ,要添加到数组开头的元素

```
    let  a =  [1,2,3];
    let item = a.unshift('开头');  // 4
    console.log(a); // ['开头',1,2,3]
复制代码
```

##### reverse() 颠倒数组中元素的顺序 #####

定义: reverse() 方法用于颠倒数组中元素的顺序。

参数: 无

```
    let  a =  [1,2,3];
    a.reverse();  
    console.log(a); // [3,2,1]
复制代码
```

##### ES6: copyWithin() 指定位置的成员复制到其他位置 #####

定义: 在当前数组内部，将指定位置的成员复制到其他位置,并返回这个数组。

语法:

```
    array.copyWithin(target, start = 0, end = this.length)
复制代码
```

参数:

三个参数都是数值，如果不是，会自动转为数值.

1. target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
2. start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示倒数。
3. end（可选）：到该位置前停止读取数据，默认等于数组长度。使用负数可从数组结尾处规定位置。

浏览器兼容(MDN): chrome 45,Edge 12,Firefox32,Opera 32,Safari 9, IE 不支持

eg:

```
        // -2相当于3号位，-1相当于4号位
        [1, 2, 3, 4, 5].copyWithin(0, -2, -1)
        // [4, 2, 3, 4, 5]
        var a=['OB1','Koro1','OB2','Koro2','OB3','Koro3','OB4','Koro4','OB5','Koro5']
        // 2位置开始被替换,3位置开始读取要替换的 5位置前面停止替换
        a.copyWithin(2,3,5)
        // ["OB1","Koro1","Koro2","OB3","OB3","Koro3","OB4","Koro4","OB5","Koro5"] 
复制代码
```

从上述栗子:

1. 第一个参数是开始被替换的元素位置
2. 要替换数据的位置范围:从第二个参数是开始读取的元素，在第三个参数前面一个元素停止读取
3. 数组的长度不会改变
4. **读了几个元素就从开始被替换的地方替换几个元素**

##### ES6: fill() 填充数组 #####

定义:  使用给定值，填充一个数组。

参数:

第一个元素(必须): 要填充数组的值

第二个元素(可选): 填充的开始位置,默认值为0

第三个元素(可选)：填充的结束位置，默认是为`this.length`

[MDN浏览器兼容](https://link.juejin.im?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray%2Ffill%23%25E6%25B5%258F%25E8%25A7%2588%25E5%2599%25A8%25E5%2585%25BC%25E5%25AE%25B9%25E6%2580%25A7)

```
    ['a', 'b', 'c'].fill(7)
    // [7, 7, 7]
    ['a', 'b', 'c'].fill(7, 1, 2)
    // ['a', 7, 'c']
复制代码
```

------

**不改变原数组的方法(8个):**

```
    ES5：
    slice、join、toLocateString、toStrigin、cancat、indexOf、lastIndexOf、
    ES7：
    includes
复制代码
```

##### slice() 浅拷贝数组的元素 #####

定义： 方法返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象，且原数组不会被修改。

**注意**：字符串也有一个slice() 方法是用来提取字符串的，不要弄混了。

语法:

```
    array.slice(begin, end);
复制代码
```

参数:

begin(可选): 索引数值,接受负值，从该索引处开始提取原数组中的元素,默认值为0。

end(可选):索引数值(不包括),接受负值，在该索引处前结束提取原数组元素，默认值为数组末尾(包括最后一个元素)。

```
    let a= ['hello','world'];
    let b=a.slice(0,1); // ['hello']
    a[0]='改变原数组';
    console.log(a,b); // ['改变原数组','world'] ['hello']
    b[0]='改变拷贝的数组';
     console.log(a,b); // ['改变原数组','world'] ['改变拷贝的数组']
复制代码
```

如上：新数组是浅拷贝的，**元素是简单数据类型，改变之后不会互相干扰**。

如果是**复杂数据类型(对象,数组)的话，改变其中一个，另外一个也会改变**。

```
    let a= [{name:'OBKoro1'}];
    let b=a.slice();
    console.log(b,a); // [{"name":"OBKoro1"}]  [{"name":"OBKoro1"}]
    // a[0].name='改变原数组';
    // console.log(b,a); // [{"name":"改变原数组"}] [{"name":"改变原数组"}]
    // b[0].name='改变拷贝数组',b[0].koro='改变拷贝数组';
    //  [{"name":"改变拷贝数组","koro":"改变拷贝数组"}] [{"name":"改变拷贝数组","koro":"改变拷贝数组"}]
复制代码
```

原因在定义上面说过了的：slice()是浅拷贝，对于复杂的数据类型浅拷贝，拷贝的只是指向原数组的指针，所以无论改变原数组，还是浅拷贝的数组，都是改变原数组的数据。

##### join()  数组转字符串 #####

定义:  join() 方法用于把数组中的所有元素通过指定的分隔符进行分隔放入一个字符串，返回生成的字符串。

语法:

```
    array.join(str)
复制代码
```

参数:

str(可选): 指定要使用的分隔符，默认使用逗号作为分隔符。

```
    let a= ['hello','world'];
    let str=a.join(); // 'hello,world'
    let str2=a.join('+'); // 'hello+world'
复制代码
```

使用join方法或者下文说到的toString方法时，当数组中的元素也是数组或者是对象时会出现什么情况？

```
    let a= [['OBKoro1','23'],'test'];
    let str1=a.join(); // OBKoro1,23,test
    let b= [{name:'OBKoro1',age:'23'},'test'];
    let str2 = b.join(); // [object Object],test
    // 对象转字符串推荐JSON.stringify(obj);
复制代码
```

所以，`join()/toString()`方法在数组元素是数组的时候，会将里面的数组也调用`join()/toString()`,如果是对象的话，对象会被转为`[object Object]`字符串。

##### toLocaleString() 数组转字符串 #####

定义: 返回一个表示数组元素的字符串。该字符串由数组中的每个元素的 toLocaleString() 返回值经调用 join() 方法连接（由逗号隔开）组成。

语法:

```
    array.toLocaleString()
复制代码
```

参数：无。

```
    let a=[{name:'OBKoro1'},23,'abcd',new Date()];
    let str=a.toLocaleString(); // [object Object],23,abcd,2018/5/28 下午1:52:20 
复制代码
```

如上述栗子：调用数组的`toLocaleString`方法，数组中的每个元素都会调用自身的`toLocaleString`方法，对象调用对象的`toLocaleString`,Date调用Date的`toLocaleString`。

##### toString() 数组转字符串 不推荐 #####

定义: toString() 方法可把数组转换为由逗号链接起来的字符串。

语法:

```
    array.toString()
复制代码
```

参数: 无。

该方法的效果和join方法一样，都是用于数组转字符串的，但是与join方法相比没有优势，也不能自定义字符串的分隔符，因此不推荐使用。

**值得注意的是**：当数组和字符串操作的时候，js 会调用这个方法将数组自动转换成字符串

```
   let b= [ 'toString','演示'].toString(); // toString,演示
   let a= ['调用toString','连接在我后面']+'啦啦啦'; // 调用toString,连接在我后面啦啦啦
复制代码
```

##### cancat #####

定义： 方法用于合并两个或多个数组，返回一个新数组。

语法：

```
    var newArr =oldArray.concat(arrayX,arrayX,......,arrayX)
复制代码
```

参数：

arrayX（必须）：该参数可以是具体的值，也可以是数组对象。可以是任意多个。

eg1:

```
    let a = [1, 2, 3];
    let b = [4, 5, 6];
    //连接两个数组
    let newVal=a.concat(b); // [1,2,3,4,5,6]
    // 连接三个数组
    let c = [7, 8, 9]
    let newVal2 = a.concat(b, c); // [1,2,3,4,5,6,7,8,9]
    // 添加元素
    let newVal3 = a.concat('添加元素',b, c,'再加一个'); 
    // [1,2,3,"添加元素",4,5,6,7,8,9,"再加一个"]
   // 合并嵌套数组  会浅拷贝嵌套数组
   let d = [1,2 ];
   let f = [3,[4]];
   let newVal4 = d.concat(f); // [1,2,3,[4]]
复制代码
```

**ES6扩展运算符...合并数组**：

因为ES6的语法更简洁易懂，所以现在合并数组我大部分采用`...`来处理，`...`运算符可以实现`cancat`的每个栗子，且更简洁和具有高度自定义数组元素位置的效果。

```
    let a = [2, 3, 4, 5]
    let b = [ 4,...a, 4, 4]
    console.log(a,b); //  [2, 3, 4, 5] [4,2,3,4,5,4,4]
复制代码
```

更多关于扩展符的详细内容移步阮一峰大神的[ECMAScript 6 入门](https://link.juejin.im?target=http%3A%2F%2Fes6.ruanyifeng.com%2F%23docs%2Farray%23%25E6%2589%25A9%25E5%25B1%2595%25E8%25BF%2590%25E7%25AE%2597%25E7%25AC%25A6)

##### indexOf() 查找数组是否存在某个元素，返回下标 #####

定义: 返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

语法:

```
    array.indexOf(searchElement,fromIndex)
复制代码
```

参数:

searchElement(必须):被查找的元素

fromIndex(可选):开始查找的位置(不能大于等于数组的长度，返回-1)，接受负值，默认值为0。

严格相等的搜索:

数组的indexOf搜索跟字符串的indexOf不一样,数组的indexOf使用严格相等`===`搜索元素，即**数组元素要完全匹配**才能搜索成功。

**注意**：indexOf()不能识别`NaN`

eg:

```
    let a=['啦啦',2,4,24,NaN]
    console.log(a.indexOf('啦'));  // -1 
    console.log(a.indexOf('NaN'));  // -1 
    console.log(a.indexOf('啦啦')); // 0
复制代码
```

使用场景：

1. [数组去重](https://juejin.im/post/5aad40e4f265da237f1e12ed#heading-10)
2. 根据获取的数组下标执行操作，改变数组中的值等。
3. 判断是否存在，执行操作。

##### lastIndexOf() 查找指定元素在数组中的最后一个位置 #####

定义:  方法返回指定元素,在数组中的最后一个的索引，如果不存在则返回 -1。（从数组后面往前查找）

语法:

```
    arr.lastIndexOf(searchElement,fromIndex)
复制代码
```

参数:

searchElement(必须): 被查找的元素

fromIndex(可选): 逆向查找开始位置，默认值数组的长度-1，即查找整个数组。

关于fromIndex有三个规则:

1. 正值。如果该值大于或等于数组的长度，则整个数组会被查找。

2. 负值。将其视为从数组末尾向前的偏移。(比如-2，从数组最后第二个元素开始往前查找)

3. 负值。其绝对值大于数组长度，则方法返回 -1，即数组不会被查找。

   ```
    let a=['OB',4,'Koro1',1,2,'Koro1',3,4,5,'Koro1']; // 数组长度为10
    // let b=a.lastIndexOf('Koro1',4); // 从下标4开始往前找 返回下标2
    // let b=a.lastIndexOf('Koro1',100); //  大于或数组的长度 查找整个数组 返回9
    // let b=a.lastIndexOf('Koro1',-11); // -1 数组不会被查找
    let b=a.lastIndexOf('Koro1',-9); // 从第二个元素4往前查找，没有找到 返回-1
   复制代码
   ```

##### ES7 includes() 查找数组是否包含某个元素 返回布尔 #####

定义： 返回一个布尔值，表示某个数组是否包含给定的值

语法：

```
    array.includes(searchElement,fromIndex=0)
复制代码
```

参数：

searchElement(必须):被查找的元素

fromIndex(可选):默认值为0，参数表示搜索的起始位置，接受负值。正值超过数组长度，数组不会被搜索，返回false。负值绝对值超过长数组度，重置从0开始搜索。

**includes方法是为了弥补indexOf方法的缺陷而出现的:**

1. indexOf方法不能识别`NaN`
2. indexOf方法检查是否包含某个值不够语义化，需要判断是否不等于`-1`，表达不够直观

eg:

```
    let a=['OB','Koro1',1,NaN];
    // let b=a.includes(NaN); // true 识别NaN
    // let b=a.includes('Koro1',100); // false 超过数组长度 不搜索
    // let b=a.includes('Koro1',-3);  // true 从倒数第三个元素开始搜索 
    // let b=a.includes('Koro1',-100);  // true 负值绝对值超过数组长度，搜索整个数组
复制代码
```

兼容性(MDN): chrome47, Firefox 43,Edge 14,Opera 34, Safari 9,IE 未实现。

------

**遍历方法(12个): **

js中遍历数组并不会改变原始数组的方法总共有12个:

```
    ES5：
    forEach、every 、some、 filter、map、reduce、reduceRight、
    ES6：
    find、findIndex、keys、values、entries
复制代码
```

##### 关于遍历： #####

- 关于遍历的效率，可以看一下这篇[详解JS遍历](https://link.juejin.im?target=http%3A%2F%2Flouiszhai.github.io%2F2015%2F12%2F18%2Ftraverse%2F%23%25E6%25B5%258B%25E8%25AF%2595%25E5%2590%2584%25E6%2596%25B9%25E6%25B3%2595%25E6%2595%2588%25E7%258E%2587)
- 尽量不要在遍历的时候，修改后面要遍历的值
- 尽量不要在遍历的时候修改数组的长度（删除/添加）

##### forEach #####

定义: 按升序为数组中含有效值的每一项执行一次回调函数。

语法：

```
    array.forEach(function(currentValue, index, arr), thisValue)
复制代码
```

参数:

function(必须): 数组中每个元素需要调用的函数。

```
    // 回调函数的参数
    1. currentValue(必须),数组当前元素的值
    2. index(可选), 当前元素的索引值
    3. arr(可选),数组对象本身
复制代码
```

thisValue(可选):  当执行回调函数时this绑定对象的值，默认值为`undefined`

**关于forEach()你要知道**：

- 无法中途退出循环，只能用`return`退出本次回调，进行下一次回调。
- 它总是返回 undefined值,即使你return了一个值。

##### 下面类似语法同样适用这些规则 #####

```
    1. 对于空数组是不会执行回调函数的
    2. 对于已在迭代过程中删除的元素，或者空元素会跳过回调函数
    3. 遍历次数再第一次循环前就会确定，再添加到数组中的元素不会被遍历。
    4. 如果已经存在的值被改变，则传递给 callback 的值是遍历到他们那一刻的值。
复制代码
```

eg:

```
    let a = [1, 2, ,3]; // 最后第二个元素是空的，不会遍历(undefined、null会遍历)
    let obj = { name: 'OBKoro1' };
    let result = a.forEach(function (value, index, array) { 
      a[3] = '改变元素';
      a.push('添加到尾端，不会被遍历')
      console.log(value, 'forEach传递的第一个参数'); // 分别打印 1 ,2 ,改变元素
      console.log(this.name); // OBKoro1 打印三次 this绑定在obj对象上
      // break; // break会报错
      return value; // return只能结束本次回调 会执行下次回调
      console.log('不会执行，因为return 会执行下一次循环回调')
    }, obj);
    console.log(result); // 即使return了一个值,也还是返回undefined
    // 回调函数也接受接头函数写法
复制代码
```

##### every 检测数组所有元素是否都符合判断条件 #####

定义: 方法用于检测数组所有元素是否都符合函数定义的条件

语法：

```
    array.every(function(currentValue, index, arr), thisValue)
复制代码
```

参数:(这几个方法的参数，语法都类似)

function(必须): 数组中每个元素需要调用的函数。

```
    // 回调函数的参数
    1. currentValue(必须),数组当前元素的值
    2. index(可选), 当前元素的索引值
    3. arr(可选),数组对象本身
复制代码
```

thisValue(可选):  当执行回调函数时this绑定对象的值，默认值为`undefined`

方法返回值规则:

1. 如果数组中检测到**有一个元素不满足，则整个表达式返回 false**，且剩余的元素不会再进行检测。
2. 如果所有元素**都满足条件，则返回 true**。=

eg:

```
    function isBigEnough(element, index, array) { 
      return element >= 10; // 判断数组中的所有元素是否都大于10
    }
    let result = [12, 5, 8, 130, 44].every(isBigEnough);   // false
    let result = [12, 54, 18, 130, 44].every(isBigEnough); // true
    // 接受箭头函数写法 
    [12, 5, 8, 130, 44].every(x => x >= 10); // false
    [12, 54, 18, 130, 44].every(x => x >= 10); // true
复制代码
```

##### some 数组中的是否有满足判断条件的元素 #####

定义：数组中的是否有满足判断条件的元素

语法：

```
    array.some(function(currentValue, index, arr), thisValue)
复制代码
```

参数:(这几个方法的参数，语法都类似)

function(必须): 数组中每个元素需要调用的函数。

```
    // 回调函数的参数
    1. currentValue(必须),数组当前元素的值
    2. index(可选), 当前元素的索引值
    3. arr(可选),数组对象本身
复制代码
```

thisValue(可选):  当执行回调函数时this绑定对象的值，默认值为`undefined`

方法返回值规则：

1. 如果**有一个元素满足条件，则表达式返回true**, 剩余的元素不会再执行检测。

2. 如果**没有满足条件的元素，则返回false**。

   ```
    function isBigEnough(element, index, array) {
      return (element >= 10); //数组中是否有一个元素大于 10
    }
    let result = [2, 5, 8, 1, 4].some(isBigEnough); // false
    let result = [12, 5, 8, 1, 4].some(isBigEnough); // true
   复制代码
   ```

##### filter 过滤原始数组，返回新数组 #####

定义: 返回一个新数组, 其包含通过所提供函数实现的测试的所有元素。

语法：

```
    let new_array = arr.filter(function(currentValue, index, arr), thisArg)
复制代码
```

参数:(这几个方法的参数，语法都类似)

function(必须): 数组中每个元素需要调用的函数。

```
    // 回调函数的参数
    1. currentValue(必须),数组当前元素的值
    2. index(可选), 当前元素的索引值
    3. arr(可选),数组对象本身
复制代码
```

thisValue(可选):  当执行回调函数时this绑定对象的值，默认值为`undefined`

eg:

```javascript
     let a = [32, 33, 16, 40];
    let result = a.filter(function (value, index, array) {
      return value >= 18; // 返回a数组中所有大于18的元素
    });
    console.log(result,a);// [32,33,40] [32,33,16,40]
复制代码
```

##### map 对数组中的每个元素进行处理，返回新的数组 #####

定义：创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

语法：

```javascript
    let new_array = arr.map(function(currentValue, index, arr), thisArg)
复制代码
```

参数:(这几个方法的参数，语法都类似)

function(必须): 数组中每个元素需要调用的函数。

```javascript
    // 回调函数的参数
    1. currentValue(必须),数组当前元素的值
    2. index(可选), 当前元素的索引值
    3. arr(可选),数组对象本身
复制代码
```

thisValue(可选):  当执行回调函数时this绑定对象的值，默认值为`undefined`

eg:

```javascript
let a = ['1','2','3','4'];
let result = a.map(function (value, index, array) {
  return value + '新数组的新元素'
});
console.log(result, a); 
// ["1新数组的新元素","2新数组的新元素","3新数组的新元素","4新数组的新元素"] ["1","2","3","4"]
复制代码
```

##### reduce 为数组提供累加器，合并为一个值 #####

定义：reduce() 方法对累加器和数组中的每个元素（从左到右）应用一个函数，最终合并为一个值。

语法：

```javascript
    array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
复制代码
```

参数：

function(必须): 数组中每个元素需要调用的函数。

```javascript
    // 回调函数的参数
    1. total(必须)，初始值, 或者上一次调用回调返回的值
    2. currentValue(必须),数组当前元素的值
    3. index(可选), 当前元素的索引值
    4. arr(可选),数组对象本身
复制代码
```

initialValue(可选): 指定第一次回调 的第一个参数。

回调第一次执行时:

- 如果 initialValue 在调用 reduce 时被提供，那么第一个 total 将等于 initialValue，此时 currentValue 等于数组中的第一个值；
- 如果 initialValue 未被提供，那么 total 等于数组中的第一个值，currentValue 等于数组中的第二个值。此时如果数组为空，那么将抛出 TypeError。
- 如果数组仅有一个元素，并且没有提供 initialValue，或提供了 initialValue 但数组为空，那么回调不会被执行，数组的唯一值将被返回。

eg:

```javascript
    // 数组求和 
    let sum = [0, 1, 2, 3].reduce(function (a, b) {
      return a + b;
    }, 0);
    // 6
    // 将二维数组转化为一维 将数组元素展开
    let flattened = [[0, 1], [2, 3], [4, 5]].reduce(
      (a, b) => a.concat(b),
      []
    );
     // [0, 1, 2, 3, 4, 5]
复制代码
```

##### reduceRight  从右至左累加 #####

这个方法除了与reduce执行方向相反外，其他完全与其一致，请参考上述 reduce 方法介绍。

##### ES6：find()& findIndex() 根据条件找到数组成员 #####

find()定义：用于找出第一个符合条件的数组成员，并返回该成员，如果没有符合条件的成员，则返回undefined。

findIndex()定义：返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1。

这两个方法

语法：

```javascript
    let new_array = arr.find(function(currentValue, index, arr), thisArg)
     let new_array = arr.findIndex(function(currentValue, index, arr), thisArg)
复制代码
```

参数:(这几个方法的参数，语法都类似)

function(必须): 数组中每个元素需要调用的函数。

```javascript
    // 回调函数的参数
    1. currentValue(必须),数组当前元素的值
    2. index(可选), 当前元素的索引值
    3. arr(可选),数组对象本身
复制代码
```

thisValue(可选):  当执行回调函数时this绑定对象的值，默认值为`undefined`

这两个方法都可以识别`NaN`,弥补了`indexOf`的不足.

eg:

```javascript
        // find
        let a = [1, 4, -5, 10].find((n) => n < 0); // 返回元素-5
        let b = [1, 4, -5, 10,NaN].find((n) => Object.is(NaN, n));  // 返回元素NaN
        // findIndex
        let a = [1, 4, -5, 10].findIndex((n) => n < 0); // 返回索引2
        let b = [1, 4, -5, 10,NaN].findIndex((n) => Object.is(NaN, n));  // 返回索引4
复制代码
```

浏览器兼容(MDN):Chrome 45,Firefox 25,Opera 32, Safari 8, Edge yes,

##### ES6 keys()&values()&entries() 遍历键名、遍历键值、遍历键名+键值 #####

定义：三个方法都返回一个新的 Array Iterator 对象，对象根据方法不同包含不同的值。

语法：

```
    array.keys()
    array.values()
    array.entries()
复制代码
```

参数：无。

遍历栗子(摘自[ECMAScript 6 入门](https://link.juejin.im?target=http%3A%2F%2Fes6.ruanyifeng.com%2F%23docs%2Farray%23%25E6%2595%25B0%25E7%25BB%2584%25E5%25AE%259E%25E4%25BE%258B%25E7%259A%2584-entries%25EF%25BC%258Ckeys-%25E5%2592%258C-values))：

```javascript
    for (let index of ['a', 'b'].keys()) {
      console.log(index);
    }
    // 0
    // 1
    
    for (let elem of ['a', 'b'].values()) {
      console.log(elem);
    }
    // 'a'
    // 'b'
    
    for (let [index, elem] of ['a', 'b'].entries()) {
      console.log(index, elem);
    }
    // 0 "a"
    // 1 "b"
复制代码
```

在`for..of`中如果遍历中途要退出，可以使用`break`退出循环。

如果不使用`for...of`循环，可以手动调用遍历器对象的next方法，进行遍历:

```javascript
    let letter = ['a', 'b', 'c'];
    let entries = letter.entries();
    console.log(entries.next().value); // [0, 'a']
    console.log(entries.next().value); // [1, 'b']
    console.log(entries.next().value); // [2, 'c']
复制代码
```

entries()浏览器兼容性(MDN):Chrome 38, Firefox 28,Opera 25,Safari 7.1

keys()浏览器兼容性(MDN):Chrome 38, Firefox 28,Opera 25,Safari 8,

**注意**:目前只有Safari 9支持,，其他浏览器未实现，babel转码器也还未实现

------

作者：OBKoro1

链接：https://juejin.im/post/5b0903b26fb9a07a9d70c7e0

------

###  找到在第一个数组array1中出现，而在第二个数组array2中没有出现的数字

``` javascript
function findNullof
```



