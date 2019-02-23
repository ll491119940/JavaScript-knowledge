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

```javascript
var arr = [];
var number = 50;
for(var i=1; i <=number; i++) {
    arr.push(i)
}
var result = [];
for(var j = number-1; j >= 0; j--) {
    var rand = Math.ceil(Math.random()*j);
    result.push(arr.splice(rand,1));
}
```



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

```javascript
    // 字面量方式:
    // 这个方法也是我们最常用的，在初始化数组的时候 相当方便
    var a = [3, 11, 8];  // [3,11,8];
    // 构造器:
    // 实际上 new Array === Array,加不加new 一点影响都没有。
    var a = Array(); // [] 
    var a = Array(3); // [,,] 
```

##### ES6 Array.of()  返回由所有参数值组成的数组 #####

定义：返回由所有参数值组成的数组，如果没有参数，就返回一个空数组。

目的：Array.of() 出现的目的是为了解决上述构造器因参数个数不同，导致的行为有差异的问题。

```javascript
    let a = Array.of(3, 11, 8); // [3,11,8]
    let a = Array.of(3); // [3]
```

##### ES6 Arrary.from() 将两类对象转为真正的数组 #####

定义：用于将两类对象转为真正的数组（不改变原对象，返回新的数组）。

参数：

第一个参数(必需):要转化为真正数组的对象。

第二个参数(可选): 类似数组的map方法，对每个元素进行处理，将处理后的值放入返回的数组。

第三个参数(可选): 用来绑定this。

```javascript
    // 1. 对象拥有length属性
    let obj = {0: 'a', 1: 'b', 2:'c', length: 3};
    let arr = Array.from(obj); // ['a','b','c'];
    // 2. 部署了 Iterator接口的数据结构 比如:字符串、Set、NodeList对象
    let arr = Array.from('hello'); // ['h','e','l','l','o']
    let arr = Array.from(new Set(['a','b'])); // ['a','b']
```

------

#### 方法: ####

数组原型提供了非常多的方法，这里分为三类来讲，一类会改变原数组的值，一类是不会改变原数组，以及数组的遍历方法。

**改变原数组的方法(9个): **

```javascript
    let a = [1,2,3];
    ES5:
     a.splice()/ a.sort() / a.pop()/ a.shift()/  a.push()/ a.unshift()/ a.reverse()
    ES6:
    a.copyWithin() / a.fill
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

```javascript
    let a = [1, 2, 3, 4, 5, 6, 7];
    let item = a.splice(0, 3); // [1,2,3]
    console.log(a); // [4,5,6,7]
    // 从数组下标0开始，删除3个元素
    let item = a.splice(-1, 3); // [7]
    // 从最后一个元素开始删除3个元素，因为最后一个元素，所以只删除了7
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

```javascript
    // 字符串排列 看起来很正常
    var a = ["Banana", "Orange", "Apple", "Mango"];
    a.sort(); // ["Apple","Banana","Mango","Orange"]
    // 数字排序的时候 因为转换成Unicode字符串之后，有些数字会比较大会排在后面 这显然不是我们想要的
    var	a = [10, 1, 3, 20,25,8];
    console.log(a.sort()) // [1,10,20,25,3,8];
```

**比较函数的两个参数：**

sort的比较函数有两个默认参数，要在函数中接收这两个参数，这两个参数是数组中两个要比较的元素，通常我们用 a 和 b 接收两个将要比较的元素：

- 若比较函数返回值<0，那么a将排到b的前面;
- 若比较函数返回值=0，那么a 和 b 相对位置不变；
- 若比较函数返回值>0，那么b 排在a 将的前面；

对于sort()方法更深层级的内部实现以及处理机制可以看一下这篇文章[深入了解javascript的sort方法](https://juejin.im/entry/59f7f3346fb9a04514635552)

**sort排序常见用法**：

1. 数组元素为数字的升序、降序:

   ```javascript
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
   ```

2. 数组多条件排序

   ```javascript
    var array = [{id:10,age:2},{id:5,age:4},{id:6,age:10},{id:9,age:6},{id:2,age:8},{id:10,age:9}];
        array.sort(function(a,b){
            if(a.id === b.id){// 如果id的值相等，按照age的值降序
                return b.age - a.age
            }else{ // 如果id的值不相等，按照id的值升序
                return a.id - b.id
            }
        })
     // [{"id":2,"age":8},{"id":5,"age":4},{"id":6,"age":10},{"id":9,"age":6},{"id":10,"age":9},{"id":10,"age":2}] 
   ```

3. 自定义比较函数，天空才是你的极限

类似的：**运用好返回值，我们可以写出任意符合自己需求的比较函数**

```javascript
    var array = [{name:'Koro1'},{name:'Koro1'},{name:'OB'},{name:'Koro1'},{name:'OB'},{name:'OB'}];
    array.sort(function(a,b){
        if(a.name === 'Koro1'){// 如果name是'Koro1' 返回-1 ，-1<0 a排在b的前面
            return -1
        }else{ // 如果不是的话，a排在b的后面
          return 1
        }
    })
    // [{"name":"Koro1"},{"name":"Koro1"},{"name":"Koro1"},{"name":"OB"},{"name":"OB"},{"name":"OB"}] 
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

```javascript
        // -2相当于3号位，-1相当于4号位
        [1, 2, 3, 4, 5].copyWithin(0, -2, -1)
        // [4, 2, 3, 4, 5]
        var a=['OB1','Koro1','OB2','Koro2','OB3','Koro3','OB4','Koro4','OB5','Koro5']
        // 2位置开始被替换,3位置开始读取要替换的 5位置前面停止替换
        a.copyWithin(2,3,5)
        // ["OB1","Koro1","Koro2","OB3","OB3","Koro3","OB4","Koro4","OB5","Koro5"] 
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

```javascript
    ['a', 'b', 'c'].fill(7)
    // [7, 7, 7]
    ['a', 'b', 'c'].fill(7, 1, 2)
    // ['a', 7, 'c']
```

------

**不改变原数组的方法(8个):**

```javascript
    ES5：
    slice、join、toLocateString、toString、cancat、indexOf、lastIndexOf、
    ES7：
    includes
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

```javascript
    let a= ['hello','world'];
    let b=a.slice(0,1); // ['hello']
    a[0]='改变原数组';
    console.log(a,b); // ['改变原数组','world'] ['hello']
    b[0]='改变拷贝的数组';
     console.log(a,b); // ['改变原数组','world'] ['改变拷贝的数组']
```

如上：新数组是浅拷贝的，**元素是简单数据类型，改变之后不会互相干扰**。

如果是**复杂数据类型(对象,数组)的话，改变其中一个，另外一个也会改变**。

```javascript
    let a= [{name:'OBKoro1'}];
    let b=a.slice();
    console.log(b,a); // [{"name":"OBKoro1"}]  [{"name":"OBKoro1"}]
    // a[0].name='改变原数组';
    // console.log(b,a); // [{"name":"改变原数组"}] [{"name":"改变原数组"}]
    // b[0].name='改变拷贝数组',b[0].koro='改变拷贝数组';
    //  [{"name":"改变拷贝数组","koro":"改变拷贝数组"}] [{"name":"改变拷贝数组","koro":"改变拷贝数组"}]
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

```javascript
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
```

**ES6扩展运算符...合并数组**：

因为ES6的语法更简洁易懂，所以现在合并数组我大部分采用`...`来处理，`...`运算符可以实现`cancat`的每个栗子，且更简洁和具有高度自定义数组元素位置的效果。

```javascript
    let a = [2, 3, 4, 5]
    let b = [ 4,...a, 4, 4]
    console.log(a,b); //  [2, 3, 4, 5] [4,2,3,4,5,4,4]
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
function findNullofNum(arr1, arr2) {
    var str = arr2.join("");
    var result = [];
    for(var i = 0, x = 0; i < arr1.length;i++) {
        if(str.indexOf(arr1[i]) == -1) {
            result[x] = arr1[i];
        }
        x++;
    }
    return result;
}
```

###  编写函数，用于过滤一个数组内重复的元素，并用这些元素重构一个新数组，新数组内也不能有重复元素



###  给定一个数组实现字符串反转

```javascript
var arr = new Array();
function myreverse(arr) {
    for(var i = 0; i < arr.length/2; i++) {
        var temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i -1] = temp;
    }
}
```

###  将数组["a","b"] 和 ["c","d"] 合并，并且删除第二个元素



###  请给Array本地对象增加一个原型方法，它的用途是删除数组中重复的条目，并将数组返回。

```javascript
Array.prototype.delrepeat = function() {
    var arr = this;
    var _arr = new Array();
    for(var i in arr) {
        if(i == 'delrepeat') continue;
        if(_arr.length == 0)
            _arr.push(arr[i]);
        for(var j=0;j < _arr.length;j++) {
            if(arr[i] == _arr[j]) {
                break;
            }
            if(j > _arr.length - 2)
                _arr.push(arr[i]);
        }
    }
    return _arr;
}
```

##  函数

### JavaScript中如何规避多人开发函数重名问题

- 命名空间，根据不同开发人员开发的功能在函数前加前缀
- 立即执行函数模式（即时对象初始化），避免污染全局环境

###  分别描述JavaScript中 prototype、constructor、this、argument的含义

-  **prototype** prototype的行为类似于C++中的静态域，用prototype来对构造函数创建共用的存储空间,prototype就相当于是一个公共的存储空间,所有实例化对象所引用的都是一个地方的内容,不需要再重新开辟空间去存储函数或者变量。这种共享是只读的，在任何一个实例中只能够用自己的同名属性覆盖这个属性，而不能够改变它。


```javascript
    // 给Object原型中添加一个函数
    Object.prototype.newStr = function(str){
        console.log(str);
    };
    // 给Object原型中添加一个函数
    Object.prototype.texts = "自定义的新变量<br>";
    var obj1 = new Object();
    var obj2 = new Object();
    console.log(obj1.texts === obj2.texts); //true
```
- **constructor** 构造函数，在对象创建或者实例化时

###  typeof、instanceof

- JavaScript里的typeof有6种：object、function、string、boolean、number、undefined
- typeof 返回一个字符串，用于说明元算数的类型
- instanceof判断一个变量是否是某个对象（类）的实例，返回值是布尔类型

##  this

###  简述JavaScript中对this的理解，并举例说明

this代表函数运行时，自动生成的一个内部对象，只能在函数内部使用。比如

```javascript
function test() {
    this.x = 1;
}
```

随着函数使用场合的不同，this的值会发生变化。但是有一个总的原则，那就是this指的是调用函数的那个对象。

下面分四种情况，详细讨论this的用法：

####  纯粹的函数调用 ####

这是函数的最通常用法，属于全局性调用，因此this就代表全局对象Global

```javascript
function test() {
    this.x = 1;
    alert(this.x);
}
//为了证明this就是全局对象,这里对代码做一下改变
var x = 1;
function test() {
    alert(this.x);
}
test();//1
```

####  作为对象方法的调用 ####

函数还可以作为某个对象的方法调用，这时this就指这个上级对象

```javascript
function test() {
    alter(this.x);
}
var o = {};
o.x = 1;
o.m = test;
o.m();//1
```

####  作为构造函数调用 ####

所谓构造函数，就是通过这个函数生成一个新对象（object）。这时，this就指这个新对象。

```javascript
function test() {
    this.x = 1;
}
var o = new test();
alert(o.x);//1
//为了表明这时的this不是全局对象，这里对代码做一些改变
var x=2;
function test() {
    this.x =1;
}
var o = new test();
alert(x);//2
//结果为2，表明全局变量x的值根本没变化
```

####  apply调用 ####

apply() 是函数对象的一个方法，它的作用是改变函数的调用对象，它的第一个参数就表示改变后的调用这个函数的对象。因此，this指的就是第一个参数。

```javascript
var x = 0;
function test() {
    alter(this.x);
}
var o = {};
o.x = 1;
o.m = test;
o.m.apply();//0
```

当apply（）的参数为空时，默认调用全局对象。因此，这时的运行结果为0，证明this指的是全局对象。如果把最后一行代码修改为`o.m.apply(o);//1` ，运行结果就变成了1，证明了这时this代表的是对象o。

##  事件

- onChange 事件是在客户端改变输入控件的值
- onClick 事件处理程序可用在用户单击按钮时执行函数
- onKeyDown 事件会在按下键盘时触发
- onKeyPress 事件会在敲击键盘时触发，就是按下并抬起同一个按键
- window.onresize 事件会在浏览器的窗口大小被改变时触发
- mouseover 不论鼠标指针穿过被选元素或其子元素，都会触发mouseover事件
- mouseenter 只有在鼠标指针穿过被选元素时，才会触发mouseenter事件
- mouseout  不论鼠标指针离开被选元素还是任何子元素，都会触发mouseout事件
- mouseleave 只有在鼠标指针离开被选元素时，才会触发mouseleave事件

###  写一段JavaScript，实现监听页面上所有a标签的click事件

```javascript
//原生的写法
document.getElementsByTagName('a').onclick = function() {}
//用jQuery的写法
$('a').click(function() {});
```

###  请写一个通用的事件监听器函数 ####

``` javascript
/*绑定事件与取消绑定*/
var handleHash = {}
var bind = (function() {
    if(window.addEventListener) {
        return function(el, type, fn, capture) {
            el.addEventListener(type, function() {
                fn();
                handleHash[type] = handleHash[type] || [];
                handleHash[type].push(arguments.callee);
            },capture);
        }else if (window.attachEvent) {
            return function(el, type, fn, capture) {
                el.attachEvent("on"+type, function() {
                	fn();
                    handleHash[type] = handleHash[type] || [];
                	handleHash[type].push(arguments.callee);
                });
                    
            };
        };
})();
    var unbind = (function() {
        if(window.addEventListener) {
            return function(el, type) {
                if(handleHash[type]){
                    var i = 0, len= handleHash[type].length;
                    for(i; i <len; i++) {
                        el.removeEventListener(type, handleHash[type][i]);
                    }
                };
            };
        }else if(window.attachEvent) {
            return function(el,type) {
                if(handleHash[type]) {
                    var i = 0,len = handleHash[type].length;
                    for(i; i< len; i++) {
                        el.detachEvent("on"+type, handleHash[type][i]);
                    }
                };
            };
        }
    })();
```

handleHash 用作哈希表缓存事件function，handleHash[‘事件名称’]是一个数组，用来添加多个事件监听的方法，当需要移除哪个事件时，遍历handleHash[‘事件名称’]的数组，然后移除。

###  简述JavaScript的事件模型 ###

####  原始事件模型

- 基本事件处理。
- 事件类型 分为“输入事件（如 onclick）” 和 “语义事件（如onsubmit）”

####  标准事件模型

DOM2对其做了标准化

1. 先由document向目标对象传播，称之为捕捉阶段。
2. 目标对象的事件处理程序运行
3. 从目标对象向document冒泡

####  IE事件模型

1. 传播过程只起泡，不捕捉。起泡中断的方法：window.event.cancelBulle = true
2. event对象不是事件处理程序的函数参数，而是window的全局变量
3. 事件注册函数attachEvent() 和反注册函数detachEvent()

####  Netscape事件模型

就是只捕捉不冒泡

###  简述addEventListener和attachEvent的作用，两者是否有区别？ ###

####  支持的浏览器

- addEventListener 在支持DOM2的浏览器中使用，如Firefox、Chrome等
- attachEvent 为IE所用

####  处理程序执行阶段

- addEventListener的第三个参数为true时，在捕获阶段执行；为false时，在冒泡阶段执行
- attachEvent均在冒泡阶段执行

#### 作用域 ####

- addEventListener 的作用域为元素作用域，this为element引用
- addEvent的作用域为全局作用域，this为window引用

####  事件处理程序执行顺序

- addEventListener：执行顺序和添加顺序一致
- attachEvent：执行顺序与添加顺序相反

### document.load 和document.ready有何区别？

页面加载完成有两种事件，一是ready，表示文档结构已经加载完成（不包含图片等非文字媒体文件）；

二是onload，表示页面包含图片等文件在内的所有元素都加载完成

###  JavaScript的事件绑定的方法，并举例说明

在JavaScript中，有三种常用的绑定事件的方法：

1. 在DOM元素中直接绑定；

``` javascript
<input  onclick="alert('谢谢支持')"  type="button"  value="点击我，弹出警告框" />

<input  onclick="myAlert()"  type="button"  value="点击我，弹出警告框" />
<script type="text/javascript">
function myAlert(){
    alert("谢谢支持");
}
</script>
```

2. 在JavaScript代码中绑定；
```javascript
<input  id="demo"  type="button"  value="点击我，显示 type 属性" />
<script type="text/javascript">
document.getElementById("demo").onclick=function(){
    alert(this.getAttribute("type"));  //  this 指当前发生事件的HTML元素，这里是<div>标签
}
</script>
```

3. 绑定事件监听函数。

```javascript
function addEvent(obj,type,handle){
    try{  // Chrome、FireFox、Opera、Safari、IE9.0及其以上版本
        obj.addEventListener(type,handle,false);
    }catch(e){
        try{  // IE8.0及其以下版本
            obj.attachEvent('on' + type,handle);
        }catch(e){  // 早期浏览器
            obj['on' + type] = handle;
        }
    }

```

##  表单、文本框

###  如何获取下拉框中选中项的内容？ ###

```javascript
<select id="test" name="">
    <option value="1">text1</option>
	<option value="2">text2</option>
</select>
//js原生的方法
var myselect = document.getElementById("test");
var index = myselect.selectIndex //selectIndex代表的是你所选中项的index
value = myselect.options[index].value;//拿到选中项options的value
myselect.options[index].text //拿到选中项options的text

//jQuery方法
var options = $("#test options:selected")
alert(options.val())//拿到选中项的值
alert(options.text())//拿到选中项的文本
```

###  table标签中border、cellpadding，以及td标签中colspan、rowspan分别起什么作业？

- border：边界
- cellpadding：边距
- colspan：跨列数
- rowspan：跨行数

###  在Form表单中get与post方式提交的区别

1. get是从服务器上获取数据，post是向服务器传送数据。
2. get是把参数数据队列加到提交表单的action属性所指的URL中，值和表单内各个字段一一对应，在URL中可以看到。post是通过HTTP post机制，将表单内各个字段与其内容放置在HTML HEADER内一起传送到action属性所指的URL地址。用户看不到这个过程。
3. get传送的数据量较小，不能大于2KB。post传送的数据量较大，一般默认为不受限制。但理论上，IIS4中最大值为80KB，IIS5中最大值为100KB。
4. get安全性非常低，post安全性较高
5. get限制Form表单的数据集的值必须为ASCII字符，不是ASCII字符时要转换为ASCII字符，也就是“%XX”(其中XX为该符号以16进制数表示的ASCII或ISO Latin-1值)这种；而post支持整个ISO10646字符集。

###  写一个简单的Form表单，当光标离开表单时把表单的值发送给后台

``` javascript
<script type="text/javascript"> 
    $("#o_form").blur(function() {
    var vals = $(this).val();
    $.Ajax({
        url: "./index.php",
        type: "post",
        data:{$val: vals},
        success : function(data) {
            alert(data);
        }
    })
})
</script>
```

###  创建一个文本框，让其宽度为120像素，高度为20像素，对齐方法为居中对齐，写出该代码

```javascript
<textarea name="" id="" cols="30" rows="10"
style="width:120px;
hight:20px;
text-align: center;"></textarea>
```

##  对称数

###  一个数字倒着读时，和原数字相同，我们将这个数字称之为对称数，例如（1,121,88,8998），在不考虑性能的情况下，请找出1~10000之间的对称数，要求用JavaScript实现。

```javascript
<script>
    for(var i = 1; i <= 10000; i++) {
        var str_i = i.toString(), I = str_i.length;//将数字转化为字符串，获取字符串的长度
        var arr_i = str_i.split("");//将字符串转化为数组
        var rev_arr = [];//命名一个空数组
        for(var j = 0; j < I; j++) {
            rev_arr.unshift(arr_i[j]);
        }
        var rev_str = rev_arr.join("");
        if(str_i == rev_str) {//将原来的数字与反转后的数字作比较
            document.write(str_i + "<br>");//如果是相等的，就是对称数，并返回
        }
    }
</script>
```

##  排序

###  请根据每个元素的i属性，有小到大排序如下数组。

``` javascript
var ar=[{i:5,v:1},{i:2,v:4},{i:3,v:2},{i:1,v:5},{i:4,v:3}];

ar.sort(function(a,b) {
    return a.i - b.i;
})
//对于一个数组，sort()默认按字符编码排序：

```

###  JavaScript数组排序方法sort()的使用，重点介绍sort()参数的使用及其内部机制

- sort方法用于对数组的元素进行排序
- 语法：` arrayObject.sort(sortby)`
- 参数：sortby 可选，规定排序顺序，必须是函数
- 返回值：对数组的引用，数组在源数组上进行排序，不生成副本
- 说明：

1. 如果调用该方法时没有实用参数，将按字母顺序对数组中的元素进行排序，说得更精确点，是按照字符编码的顺序进行排序。
2. 如果想按照其他标准进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个，用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数：a和b，其返回值如下：
   - 若a小于b，在排序后的数组中a应该出现在b之前，返回一个小于0的值
   - 若a等于b，则返回0
   - 若a大于b，则返回一个大于0的值。

```javascript
<script type="text/javascript">

function sortNumber(a,b)
{
return a - b
}

var arr = new Array(6)
arr[0] = "10"
arr[1] = "5"
arr[2] = "40"
arr[3] = "25"
arr[4] = "1000"
arr[5] = "1"

document.write(arr + "<br />")
document.write(arr.sort(sortNumber))

</script>
```

输出：

```javascript
10,5,40,25,1000,1
1,5,10,25,40,1000
```

这里可以看出，如果安装升序排列，那么方法为：

```javascript
function sortNumber(a,b)
{
return a - b
}
```

如果是按照降序排列则为：

```javascript
function sortNumber(a,b)
{
return b - a
}
```

##  call、apply

###  call和apply的区别

ECMAScript 规范给所有函数都定义了 call 与 apply 两个方法，它们的应用非常广泛，它们的作用也是一模一样，只是传参的形式有区别而已。

**apply( ) **

apply 方法传入两个参数：一个是作为函数上下文的对象，另外一个是作为函数参数所组成的数组。

```javascript
var obj = {
    name : 'linxin'
}

function func(firstName, lastName){
    console.log(firstName + ' ' + this.name + ' ' + lastName);
}

func.apply(obj, ['A', 'B']);    // A linxin B
```

可以看到，obj 是作为函数上下文的对象，函数 func 中 this 指向了 obj 这个对象。参数 A 和 B 是放在数组中传入 func 函数，分别对应 func 参数的列表元素。

apply的好处是可以直接将当前函数的arguments对象作为apply的第二个参数传入。

**call()**

call 方法第一个参数也是作为函数上下文的对象，但是后面传入的是一个参数列表，而不是单个数组。

```javascript
var obj = {
    name: 'linxin'
}

function func(firstName, lastName) {
    console.log(firstName + ' ' + this.name + ' ' + lastName);
}

func.call(obj, 'C', 'D');       // C linxin D
```

对比 apply 我们可以看到区别，C 和 D 是作为单独的参数传给 func 函数，而不是放到数组中。

对于什么时候该用什么方法，其实不用纠结。如果你的参数本来就存在一个数组中，那自然就用 apply，如果参数比较散乱相互之间没什么关联，就用 call。

###  apply 和 call 的用法

**1.改变 this 指向**

```javascript
var obj = {
    name: 'linxin'
}

function func() {
    console.log(this.name);
}

func.call(obj);       // linxin
```

我们知道，call 方法的第一个参数是作为函数上下文的对象，这里把 obj 作为参数传给了 func，此时函数里的 this 便指向了 obj 对象。此处 func 函数里其实相当于

```java
function func() {
    console.log(obj.name);
}
```

**2.借用别的对象的方法**

先看例子

```javascript
var Person1  = function () {
    this.name = 'linxin';
}
var Person2 = function () {
    this.getname = function () {
        console.log(this.name);
    }
    Person1.call(this);
}
var person = new Person2();
person.getname();       // linxin
```

从上面我们看到，Person2 实例化出来的对象 person 通过 getname 方法拿到了 Person1 中的 name。因为在 Person2 中，Person1.call(this) 的作用就是使用 Person1 对象代替 this 对象，那么 Person2 就有了 Person1 中的所有属性和方法了，相当于 Person2 继承了 Person1 的属性和方法。

**3.调用函数**

apply、call 方法都会使函数立即执行，因此它们也可以用来调用函数。

```
function func() {
    console.log('linxin');
}
func.call();            // linxin
```

###  call的作用是什么？它的参数是如何传递的？

call方法在msdn中的解释为，调用一个对象的一个方法，以另一个对象替换当前对象。

JavaScript中，call的语法为：call(thisObj, arg1, ... , argn)

参数thisObj：可选项，将被用作为当前对象的对象

参数arg1, ... , ：可选项，将被传递方法参数列表

## 继承和多态

### 请用代码说明JavaScript如何实现继承和多态

1. 继承

   - 原型继承法
```javascript
function parentClass() {
    var x = "I'm a parentClass field";
    function method1() {
        alert(x);
        alert("I'm a parentClass  method!");
    }
    this.x = "I'm a parentClass object field!";
    this.method1 = function() {
        alert(x);
        alert(this.x);
        method1();
    }
}
parentClass.prototype.method = function() {
    alert("I'm a parentClass prototype method!");
    parentClass.staticMethod = function() {
        alert("I'm a parentClass static method!");
    }
}
```
   - 调用继承法

```javascript

```

###  多态

```javascript
//重载
function add() {
    var sum = 0;
    for(var i = 0; i < arguments.length; i++) {
        sum += arguments[i];
    }
    return sum;
}
//覆盖
function parentClass() {
    this.method = function() {
        alert("parentClass method");
    }
}
function subClass() {
    this.method = function() {
        alert("subClass method");
    }
}
subClass.prototype = new parentClass();
subClass.prototype.constructor = subClass;
var o = new subClass();
o.method();
```

###  JavaScript实现一个类A，包含私有属性、公有属性、私有方法和公有方法

``` javascript
function A() {
    this.name = "world";//公有属性
    var message = "No Message!";//私有属性
    this.sayHello = function() {
        //公有方法（可访问所有权限的方法和属性）
    }
    function getMessage(){
        //私有方法（只能访问私有的方法和属性）
        alert(message);
    }
}
class1.staticMethod = function() {
    //定义该类的一个静态方法
    alert("staticMethod()");
}
```

JavaScript中所有的function都可以当作一个类来使用，从上述的例子可以看出，可以new一个类，也可以直接当作function调用。

##  charAt()、indexOf()

charAt() 语法：strObj.charAt(index) 返回指定索引位置处的字符

indexOf() 语法：strObj.indexOf(subString[,startIndex]) 返回String对象内第一次出现子字符串的字符位置

###  如何把一个字符串里的所有单词的第一个字符转换为大写？

```javascript
var words = string.split(" ");
for(var i = 0; i < words.length; i++) {
    words[i] = words[i].charAt(0).toUpperCase() + words[i].slice(1);
}
return words.join(" ");
```



##  substr、substring

JavaScript中substr和substring的区别是什么？

- stringvar.substr(start[,length])返回一个从指定位置开始的指定长度的子字符串。如果length为0或负数，将返回一个空字符串。如果没有指定该参数，则子字符串将延续到stringvar的最后
- strVariable.subtring(start,end)返回位于String对象中指定位置的子字符串。返回一个包含从开始到最后（不包含end）的子字符串。

###  用JavaScript取www.qdjhu.com/public/images/test.jpg 字符串test.jpg 的扩展名

```javascript
url = www.qdjhu.com/public/images/test.jpg;
m = url.lastIndexOf(".");
fileName = url.substr(m+1)
```

##  iframe

iframe 元素也就是文档中的文档，或者好像浮动的框架（frame）。通过iframe对象所在页面的对象模型，用户可以访问iframe对象的属性，但不能访问其内容。

##  Ajax

###  Ajax是什么？它的全称是什么？

Ajax的全称是  “ Asynchronous JavaScript and XML ” （异步JavaScript和XML），它是一种创建交互式网页应用的网页开发技术

###  简述Ajax中JavaScript脚本缓存问题，如何解决？

修改JavaScript内容，调试时并不能显示新写的代码的结果，是因为JavaScript为了加速页面执行，当前页面会使用缓存来保持当前调用的相同链接。

解决方法：为了开发时调试方便，可以在链接地址的后面增加一个随机函数

###  Ajax应用和传统Web应用有什么不同？

在传统的JavaScript编程中，如果想得到服务器端数据库或文件上的信息，或者发送客户端信息到服务器，需要建立一个HTML form，然后get或者post数据到服务器端。用户需要单击“submit”按钮来发送或者接收数据信息，然后等待服务器响应请求，页面重新加载。因为服务器每次都会返回一个新的页面，所以传统的web应用有可能很慢，而且交互不太好。使用Ajax技术，就可以使JavaScript通过XMLHttpRequest对象直接与服务器进行交互。通过HTTPRequest，一个Web页面可以发送一个请求到Web服务器，并且接收Web服务器返回的信息，展示给用户的还是同一个页面，用户感觉页面刷新了，但是看不到JavaScript后台进行的发送请求和接收响应。

###  Ajax有哪些优点和缺点

优点：

- 最大的优点是页面无刷新，用户的体验非常好
- 使用异步方式与服务器通信，具有更加迅速的响应能力
- 可以把以前一些服务器负担的工作转嫁到客户端，利用客户端闲置的能力来处理，减轻服务器和带宽的负担，节约空间和宽带租用成本。并且减轻服务器的负担，Ajax的原则是“按需取数据”，可以最大程度的减少冗余请求和响应对服务器造成的负担
- 基于标准化的并被广泛支持的技术，不需要下载插件或者小程序

缺点：

- Ajax不支持浏览器返回按钮
- 安全问题，Ajax暴露了与服务器交互的细节
- 对搜索引擎的支持比较弱
- 破坏了程序的异常机制
- 不容易调试

###  Ajax跨域的解决办法？

1. Web代理的方式。 即用户访问A网站时所产生的对B网站的跨域访问请求均提交到A网站的指定页面，由该页面代替用户页面完成交互，从而返回合适的结果。此方案可以解决现阶段所能够想到的多数跨域访问问题，但要求A网站提供Web代理的支持，因此A网站与B网站之间必须是紧密协作的，且每次交互过程，A网站的服务器负担增加，无法代用户保存session状态
2. on-Demand方式。 MYMSN的门户就是用的这种方式，不过MYMSN中不涉及跨域访问问题。动态控制script标记的生成，通过修改script标记的src属性完成对跨域页面的调用。此方案存在的缺陷是，script的src属性完成该调用时，采取的是get方式，如果请求时传递的字符串过大，程序可能会无法正常运行。不过此方案非常适合聚合类门户使用
3. iframe方式。采用iframe这种方式的确可以，但由于父窗口与子窗口之间不能交互（跨域访问的情况下，这种交互被拒绝），因此无法完成对父窗口效果的影响。
4. 用户本地转储方式
5. 结合前几种方式，在访问A网站时，先请求B网站完成数据处理，再根据返回的标识来获得所需的结果。这种方法的缺点也很明显，即B网站的负载增大了。其优点在于，对session实现了保持，同时A网站与B网站页面间的交互能力增强了

###  XMLHttpRequest对象

使用XMLHttpRequest (XHR)对象可以与服务器交互。您可以从URL获取数据，而无需让整个的页面刷新。这使得Web页面可以只更新页面的局部，而不影响用户的操作。XMLHttpRequest在 [Ajax](https://developer.mozilla.org/en-US/docs/AJAX) 编程中被大量使用。

**常用属性**
此接口继承了 XMLHttpRequestEventTarget 和 EventTarget 的属性

 [`XMLHttpRequest.onreadystatechange`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/onreadystatechange) 

当readyState属性发生变化时调用的[`EventHandler`](https://developer.mozilla.org/zh-CN/docs/Web/API/EventHandler)。

[`XMLHttpRequest.readyState`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState) 

返回 一个unsigned short 即无符号短整型，请求的状态码。

 [`XMLHttpRequest.response`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/response) 

返回[`ArrayBuffer`](https://developer.mozilla.org/zh-CN/docs/Web/API/ArrayBuffer)、[`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)、[`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document)、[`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)}，具体是哪种类型取决于[`XMLHttpRequest.responseType`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/responseType)的值。其中包含响应体body。

 [`XMLHttpRequest.responseText`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/responseText) 

返回一个[`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)}，该[`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)}包含对请求的响应，如果请求未成功或尚未发送，则返回null。

**常用方法**

 [`XMLHttpRequest.open()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/open) 

初始化一个请求。该方法只能JavaScript代码中使用，若要在native code中初始化请求，请使用openRequest()。

 [`XMLHttpRequest.send()`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/send) 

发送请求。如果请求是异步的（默认），那么该方法将在请求发送后立即返回。

###  JavaScript如何得到HTTP的请求头信息和返回的头信息？

getResponseHeader从响应头信息中获取指定的http头信息。

语法：strValue =  oXMLHttpRequest.getResponseHeader(bstrHeader);

getAllResponseHeaders()获取响应的所有HTTP头信息

语法：strValue = oXMLHttpRequest.getAllResponseHeaders();

##  闭包

###  什么是闭包？

闭包就是能够读取其他函数内部变量的函数

- 闭包外层是一个函数
- 闭包内部都有函数
- 闭包会return内部函数
- 闭包返回的函数内部不能有return
- 执行闭包后，闭包内部变量会存在，而闭包内部函数的内部变量不会存在。

**作用和原理：**

因为闭包只有在被调用时才执行操作，所以它可以被用来定义控制结构。

多个函数可以使用一个相同的环境，这使得他们可以通过改变那个环境相互交流。

闭包可以用来实现对象系统。

**使用的场景：**

- 采用函数引用方式的setTimeout调用
- 将函数关联到对象的实例方法
- 封装相关的功能集

###  闭包有什么特性？对页面有什么影响？

**闭包特性：**

- 作为函数变量的一个引用。当函数返回时，其处于激活状态
- 闭包就是当一个函数返回时，并没有释放资源的栈区

**闭包对页面的影响：**

通过使用闭包，我们可以做很多事情。比如模拟面向对象的代码风格；更优雅、更简洁的表达出代码；在某些方面提升代码的执行效率。

###  闭包的好处和坏处？

闭包的好处：

- 逻辑连续，当闭包作为另一个函数调用参数时，避免脱离当前逻辑而单独编写额外逻辑
- 方便调用上下文的局部变量
- 加强封装性，是第二点的延伸，可以达到对变量的保护作用

闭包的坏处：

- 闭包有一个非常严重的问题，即浪费内存，浪费内存不仅仅因为它常驻内存，更重要的是，对闭包的使用不当会造成无效内存的产生。

###  请写出一个闭包的简单实例

```javascript
function a() {
    var i = 0;
    function b() {
        alert(++i);
    }
    return b;
}
var c = a();
c();
//这是一个标准的闭包。在函数a中，定义了函数b，a又return了b的值。
```

##  video

###  请使用JavaScript创建video标签，并创建播放、暂停方法

```javascript
function playPause() {
    var myVideo = document.getElementsByTagName('video')[0];
    if(myVideo.paused)
        myVideo.play();
    else
        myVideo.pause();
}

function makeBig() {
    var myVideo = document.getElementsByTagName('video')[0];
    myVideo.height = (myVideo.videoHeight*2);
}
function makeNormal() {
    var myVideo = document.getElementsByTagName('video')[0];
    myVideo.height = (myVideo.videoHeight);
}
```

## URL

###  获取当前url，并将url的参数遍历数组打印出来，并在3秒自动返回前一个页面

```javascript
function getUrlPars() {
    var url = location.search;
    var theRequest = new Object();
    if(url.indexOf("?") != -1) {
        var str=url.substr(1);
        strs = str.split("&");
        for(var i = 0; i < strs.length; i++) {
            var sTemp = strs[i].split("=");
            theRequest[sTemp[0]]=(sTemp[1]);
        }
    }
    return theRequest;
}
var myRequest = getUrlPars();
```

##  正则表达式

###  请写一个方法，验证用户输入是否为数字

```javascript
function validate() {
    var reg = new RegExp("^[0-9]*$");
    var obj = document.getElementById("name");
    if(!reg.test(obj.value)){
        alert("请输入数字！");
    }
    if(!/^[0-9]*$/.test(obj.value)){
        alert("请输入数字！")；
    }
}
```

###  用正则表达式怎样去掉重复的字符串，而只保留其中的一个？

```javascript
var str = "aaadcccdddd";
str = str.replace(/(.)\1+/g,'$1');
```

###  用正则表达式判断手机、邮箱、电话、中文

```javascript
//手机
/^13[0-9]{1}[0-9]{8} | ^15[9]{1}[0-9]{8}/
//邮箱
/^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$/
//电话
/((\(\d{3}\)|\d{3}-)|(\(\d{4}\)\d{4}-))?(\d{8}|\d{7})/
//中文
/^[\u4e00-\u9fa5]{0,}$/
```

## JSON

###  请解释一下JSON是如何进行跨域的？

json可以跨域，但是必须有jsoncallback这个参数约定

###  请实现一个JSON.stringify()方法，能够对标准的JSON序列化

JSON对象有两个方法：stringify() 和pares()。

###  什么事JSON

JSON是一种基于文本的数据交换方式，或者叫做数据描述格式，你是否该选用他首先肯定要关注它所拥有的优点。

**JSON的优点：**

1、基于纯文本，跨平台传递极其简单；

2、Javascript原生支持，后台语言几乎全部支持；

3、轻量级数据格式，占用字符数量极少，特别适合互联网传递；

4、可读性较强，虽然比不上XML那么一目了然，但在合理的依次缩进之后还是很容易识别的；

5、容易编写和解析，当然前提是你要知道数据结构；

JSON的缺点当然也有，但在作者看来实在是无关紧要的东西，所以不再单独说明。

**JSON的格式或者叫规则：**

JSON能够以非常简单的方式来描述数据结构，XML能做的它都能做，因此在跨平台方面两者完全不分伯仲。

1、JSON只有两种数据类型描述符，大括号{}和方括号[]，其余英文冒号:是映射符，英文逗号,是分隔符，英文双引号""是定义符。

2、大括号{}用来描述一组“不同类型的无序键值对集合”（每个键值对可以理解为OOP的属性描述），方括号[]用来描述一组“相同类型的有序数据集合”（可对应OOP的数组）。

3、上述两种集合中若有多个子项，则通过英文逗号,进行分隔。

4、键值对以英文冒号:进行分隔，并且建议键名都加上英文双引号""，以便于不同语言的解析。

5、JSON内部常用数据类型无非就是字符串、数字、布尔、日期、null 这么几个，字符串必须用双引号引起来，其余的都不用，日期类型比较特殊，这里就不展开讲述了，只是建议如果客户端没有按日期排序功能需求的话，那么把日期时间直接作为字符串传递就好，可以省去很多麻烦。

###  jsonp的实现机制是什么？

jsonp全称是JSON with Padding，是为了解决跨域请求资源而产生的解决方案。



##  事件流

###  描述一下事件冒泡，介绍事件委托（事件代理）的实现方法，以及它的原理和优点。

1. 事件冒泡。在一个对象上触发某类事件，如果该对象定义了此事件的处理程序，那么此事件就会调用这个处理程序；如果没有定义此事件处理程序或者事件返回true，那么这个事件会向这个对象的父级对象传播，从里到外，直至它被处理，或者它到达了对象层次的顶层，即document对象
2. 事件委托的实现方法。通俗地讲，onclick、onmouseover、onmouseout等就是事件。而委托，就是让别人来做，这个事件本来是加在某些元素上的，然而你却加到别人身上来做，以完成这个事件。也就是：利用冒泡的原理，把事件加到父级上，触发执行效果。
3. 事件委托的原理。事件委托，其实从名字上就很好理解，就是自己的事交给别人去做，即将事件委托给别人。
4. 事件委托的优点。利用比如有很多li元素，我们想为每一个元素注册一个单击事件，是一项海量的工作，如果利用冒泡原理，将事件委托给父级元素。

###  解释JavaScript事件冒泡机制

事件：在浏览器客户端应用平台，基本上都是以事件驱动的，即某个事件发生，然后做出相应的动作。浏览器的事件表示的是某些事情发生的信号。

冒泡：例如，气泡从水底开始往上升，由深到浅，升到最上面。在上升的过程中，气泡会经过不同深度层次的水。这个气泡就相当于这里的事件，而水则相当于整个DOM树；事件从DOM树的底层一层一层往上传递，直至传递到DOM的根节点。

###  分别写出普通与绑定的阻止默认事件

普通： return false；

绑定： preventDefault()；

###  event.preventDefault 的作用是什么？与event.stopPropagation 有什么区别？

event.preventDefault() 用法：该方法将通知Web浏览器不要执行与事件关联的默认动作。例如，如果type属性是submit，在事件传播的任意阶段可以调用任意的事件句柄，通过调用该方法，可以阻止提交表单。注意，如果event对象的cancelable属性是false，那么久没有默认动作，或者不能阻止默认动作。无论哪种情况，调用该方法都没有作用。

event.stopPropagation() 用法：该方法将停止事件的传播，阻止它被分派到其他document节点。在事件传播的任何阶段都可以调用它。注意，虽然该方法不能阻止同一个document节点上的其他事件句柄被调用，但是它可以阻止把事件分派到其他节点。

###  如何阻止冒泡事件和默认事件

阻止冒泡事件发生需要调用以下函数：

```javascript
function stopBubble(e) {
    if(e && e.stopPropagation) {
        e.stopPropagation();
    }
    else {
        window.event.cancelBubble = true;
    }
}
```

阻止默认事件发生需要调用以下函数：

```javascript
function stopDefault(e) {
    if(e && e.preventDefault) {
        e.preventDefault();
    }
    else {
        window.event.returnValue = false;
    }
    return false;
}
```

## 错误处理与调试

### JavaScript程序中异常捕获的方法有哪些？

使用Try...catch...来异常捕获

使用onerror事件异常捕获，这种捕获方式是比较古老的一种方式，目前一些主流的浏览器暂不支持这种捕获方式

##  Cookie

HTTP Cookie（也叫Web Cookie或浏览器Cookie）是服务器发送到用户浏览器并保存在本地的一小块数据，它会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上。通常，它用于告知服务端两个请求是否来自同一浏览器，如保持用户的登录状态。Cookie使基于[无状态](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview#HTTP_is_stateless_but_not_sessionless)的HTTP协议记录稳定的状态信息成为了可能。

Cookie主要用于以下三个方面：

- 会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）
- 个性化设置（如用户自定义设置、主题等）
- 浏览器行为跟踪（如跟踪分析用户行为等）

Cookie曾一度用于客户端数据的存储，因当时并没有其它合适的存储办法而作为唯一的存储手段，但现在随着现代浏览器开始支持各种各样的存储方式，Cookie渐渐被淘汰。由于服务器指定Cookie后，浏览器的每次请求都会携带Cookie数据，会带来额外的性能开销（尤其是在移动环境下）。




