
---
title: Web知识的学习
date: 2019-05-06 12:36:15
tags: web前端
---


# HTML

### 前端三大块

```
1、HTML：页面结构
2、CSS：页面表现：元素大小、颜色、位置、隐藏或显示、部分动画效果
3、JavaScript：页面行为：部分动画效果、页面与用户的交互、页面功能
```

## 基本结构

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>网页标题</title>
</head>
<body>
    网页显示内容
</body>
</html>
```

设置网页编码：<meta charset="utf-8"/>

关键字：<meta name="Keywords" content="关键字" />

描述：  <meta name="Description" content="简介、描述" />

网页标题：<title>本网页标题</title>

导入CSS文件：<link type="text/css" rel="stylesheet" href="**.css"/>

CSS代码：<style type="text/css">嵌入css样式代码</style>

JS文件或代码： <script >。。。</script>

### 标题

```
<h1>这是一级标题</h1>
<h2>这是二级标题</h2>
<h3>这是三级标题</h3>
```

通过 <h1>、<h2>、<h3>、<h4>、<h5>、<h6>,标签可以在网页上定义6种级别的标题

### HTML段落,换行,字符实体



<p> 内容</p>        段落标签

<br/>               换行标签

<hr>                带有行线的换行标签

&nbsp；       空格

```
&lt;      小于号
&gt;      大于号
```

### html块元素

div标签 块元素，表示一块内容，没有具体的语义

<div></div>

### ★行内元素

span标签 行内元素，表示一行中的一小段内容，没有具体的语义。

<span></span>

### 含样式的标签

```
em标签 行内元素，表示语气中的强调词
i标签 行内元素，原本没有语义，w3c强加了语义，表示专业词汇
b标签 行内元素，原本没有语义，w3c强加了语义，表示文档中的关键字或者产品名
strong标签 行内元素，表示非常重要的内容
del 删除线
```

### html图片

```
<img src="images/pic.jpg" alt="产品图片" />
```

<img>标签可以在网页上插入一张图片，它是独立使用的标签，通过“src”属性定义图片的地址，通过“alt”属性定义图片加载失败时显示的文字，以及对搜索引擎和盲人读屏软件的支持。

### html链接   与锚点跳转

链接

```
<a href="#"></a> <!--  # 表示链接到页面顶部   -->
<a href="http://www.itxdl.cn/" title="跳转的it兄弟连网站">兄弟连</a>
<a href="2.html">测试页面2</a>


href（必须） 指的是链接跳转地址
target: 表示链接的打开方式： _blank 新窗口
title属性定义鼠标悬停时弹出的提示文字框

<!-- href属性中的url可以携带参数 ?分割后 携带参数 键=值 多个参数之间用&分割-->
	<a href="./3.html?id=1&name=zhangsan&sex=nan">京东</a>
```

锚点：定义页面内滚动跳转

```
<a href="#mao1">标题一</a>
......
......
<h3 id="mao1">跳转到的标题</h3>
```

## 列表

#### 有序列表

```
<ol>
    <li>列表文字一</li>
    <li>列表文字二</li>
    <li>列表文字三</li>
</ol>
```

#### ★无序列表

```
<ul>
    <li>列表文字一</li>
    <li>列表文字二</li>
    <li>列表文字三</li>
</ul>
去li前面的点: list-style:none
```

#### 定义列表

```
<h3>前端三大块</h3>
<dl>
    <dt>html</dt>
    <dd>负责页面的结构</dd>

    <dt>css</dt>
    <dd>负责页面的表现</dd>

    <dt>javascript</dt>
    <dd>负责页面的行为</dd>

</dl>
```

## 表格

```
<table>
	<tr>
		<th></th>
		........
	</tr>
	<tr>
		<td>内容</td>
		............
	</tr>
</table>

```

#### table常用标签

1、table标签：声明一个表格

2、tr标签：定义表格中的一行

3、td和th标签：定义一行中的一个单元格，td代表普通单元格，th表示表头单元格

#### table常用属性

```
1、border 定义表格的边框

2、cellpadding 定义单元格内内容与边框的距离

3、cellspacing 定义单元格与单元格之间的距离

4、align 设置单元格中内容的水平对齐方式,设置值有：left | center | right

5、valign 设置单元格中内容的垂直对齐方式 top | middle | bottom

6、colspan 设置单元格水平合并

7、rowspan 设置单元格垂直合并
```

## ★html表单:form

```
<form action="http://www..." method="get">
</from>

```

form表单中

 action 表示数据提交的地址url 

 method代表提交数据的方式方法 

get         post 

get提交方式,数据在地址栏 可见,而且数据长度有限制 218k

post提交,地址栏不可见,数据长度 2m

```
 <p>
    <label>姓名：</label><input type="text" name="username" />
 </p>
```

label标签   定义表单控件的文字标注

input 类型为 text 定义了一个单行文本输入框

```
<p>
    <label>密码：</label><input type="password" name="password" />
</p>
```

input类型为password定义了一个密码输入框

```
<p>
    <label>性别：</label>
    <input type="radio" name="gender" value="0" /> 男
    <input type="radio" name="gender" value="1" /> 女
</p>
name 属性决定是否关联,name一样则所有的都是单选
```

input类型为radio定义了单选框

```
<p>
    <label>爱好：</label>
    <input type="checkbox" name="like" value="sing" /> 唱歌
    <input type="checkbox" name="like" value="run" /> 跑步
    <input type="checkbox" name="like" value="swiming" /> 游泳
</p>
```

input类型为checkbox定义了单选框 

```
<p>
    <label>照片：</label>
    <input type="file" name="person_pic">
</p>
```

input类型为file定义上传照片或文件等资源

如果表单中含有文件上传method提交方式必须为post

 form中必须有enctype属性

enctype="multipart/form-data"

```
 <p>
    <label>籍贯：</label>
    <select name="site">
        <option value="0">北京</option>
        <option value="1">上海</option>
        <option value="2">广州</option>
        <option value="3">深圳</option>
    </select>
 </p>
```

select定义下拉列表选择

```
隐藏域:<input type="hidden" name="id" value="110">
```

```
<input type="submit" value="注册">
<input type="reset" value="重置">
<button>登录</button>
```

input类型为submit定义提交按钮 

input类型为reset定义重置按钮

### type属性

```
text:单行文本框
password:密码输入框
        checkbox:多选框 注意要提供value值
        radio:单选框   注意要提供value值
        file:文件上传选择框
        button:普通按钮 
        submit:提交按钮
        image:图片提交按钮
        reset:重置按钮, 还原到开始\(第一次打开时\)的效果
        hidden:主表单隐藏域,要是和表单一块提交的信息,但是不需要用户修改
```
### 常用属性

name属性:表单项名,用于存储内容值的

value属性:输入的值\(默认指定值\)

size属性:输入框 readonly属性:对输入框只读属性的宽度值

disabled属性:禁用属性

checked属性:对选择框指定默认选项

```
<input  type="submit" value='注册' disabled> 
生成一个不可点击的按钮
```

# CSS

### 基本语法

css的定义方法是：选择器 { 属性:值; 属性:值; 属性:值;}

1、外联式：通过link标签，链接到外部样式表到页面中：

```
<link rel="stylesheet" type="text/css" href="css/main.css">
```

2，嵌入式：通过style标签，在网页上创建嵌入的样式表：

```
<style type="text/css">
    div{ width:100px; height:100px; color:red }
    ......
</style>
```

3、内联式：通过标签的style属性，在标签上直接写样式：

```
<div style="width:100px; height:100px; color:red ">
......
</div>
```

### css颜色

颜色名表示，比如：red 红色，gold 金色

1,    16进制数值表示，比如：#ff0000 表示红色，这种可以简写成 #f00

2,      RGB颜色: 红(R)、绿(G)、蓝(B)三个颜色通道的变化 background-color: rgba(200,100,0);

3,     RGBA颜色: 红(R)、绿(G)、蓝(B)、透明度(A) background-color: rgba(0,0,0,0.5);

### 鼠标手

```
cursor
cursor:pointer     让鼠标在那块变成可点击状态
```

### CSS文本设置

```
color 设置文字的颜色，如： color:red;
font-size 设置文字的大小，如：font-size:12px;
font-family 设置文字的字体，如：font-family:'微软雅黑';
font-style 设置字体是否倾斜，如：font-style:'normal'; 设置不倾斜，font-style:'italic';设置文字倾斜
font-weight 设置文字是否加粗，如：font-weight:bold; 设置加粗 font-weight:normal 设置不加粗
font 同时设置文字的几个属性，写的顺序有兼容问题，建议按照如下顺序写：
      font：是否加粗 字号/行高 字体；如： font:normal 12px/36px '微软雅黑';
line-height 设置文字的行高，如：line-height:24px;
text-decoration 设置文字的下划线，如：text-decoration:none; 将文字下划线去掉
text-indent 设置文字首行缩进，如：text-indent:24px; 设置文字首行缩进24px
text-align 设置文字水平对齐方式，如text-align:center 设置文字水平居中
line-style:none   清除格式 例如：li前面的点
```

### CSS边框属性

```
border:宽度 样式 颜色;
border-color;
border-style; 边框样式：solid实现，dotted点状线，dashed虚线
border-width:
border-left-color;
border-left-style;
border-left-width:
CSS3的样式
border-radius：圆角处理
box-shadow: 设置或检索对象阴影
box-sizing:border-box  元素的大小 在计算时 把边框和内边距计算在内
```

### 背景属性 background

```
background-color: 背景颜色
*background-image: 背景图片
 background:url(图片地址)
*background-repeat：是否重复，如何重复?(平铺)
*background-position：定位
background-attachment： 是否固定背景，
            scroll:默认值。背景图像是随对象内容滚动
            fixed:背景图像固定 
*background-size: 背景大小，如 background-size:100px 140px;
```

### 元素溢出 overflow

**overflow的设置项：**
1、visible 默认值。内容不会被修剪，会呈现在元素框之外。
2、hidden 内容会被修剪，并且其余内容是不可见的，此属性还有清除浮动、清除margin-top塌陷的功能。
3、scroll 内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。
4、auto 如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。
5、inherit 规定应该从父元素继承 overflow 属性的值。

### CSS内边距

```
padding： 检索或设置对象四边的内部边距,如padding:10px; padding:5px 10px;
padding-top： 检索或设置对象顶边的内部边距
padding-right： 检索或设置对象右边的内部边距
padding-bottom：检索或设置对象下边的内部边距
padding-left： 检索或设置对象左边的内部边距
```

### CSS外边距

```
margin： 检索或设置对象四边的外延边距,如 margin:10px; margin:5px auto;
margin-top： 检索或设置对象顶边的外延边距
margin-right： 检索或设置对象右边的外延边距
margin-bottom： 检索或设置对象下边的外延边距
margin-left： 检索或设置对象左边的外延边距
设置元素水平居中： margin:x auto
注意,margin 外边距 在垂直方向会合并,水平方向不会合并
```

## 盒子

### 设置边距

```
border-top-color:red;    /* 设置顶部边框颜色为红色 */  
border-top-width:10px;   /* 设置顶部边框粗细为10px */   
border-top-style:solid;  /* 设置顶部边框的线性为实线，常用的有：solid(实线)  
dashed(虚线)  dotted(点线); */

上面三句可以简写成一句：
border-top:10px solid red;
```

### 设置内间距padding

```
padding-top：20px;     /* 设置顶部内间距20px */ 
padding-left:30px;     /* 设置左边内间距30px */ 
padding-right:40px;    /* 设置右边内间距40px */ 
padding-bottom:50px;   /* 设置底部内间距50px */

上面的设置可以简写如下：
padding：20px 40px 50px 30px; /* 四个值按照顺时针方向，分别设置的是 上 右 下 左  四个方向的内边距值。 */


padding：20px 40px 50px; /* 设置顶部内边距为20px，左右内边距为40px，底部内边距为50px */ 

padding：20px 40px; /* 设置上下内边距为20px，左右内边距为40px*/ 

padding：20px; /* 设置四边内边距为20px */
```

### ★margin-top 塌陷

```
在两个盒子嵌套时候，内部的盒子设置的margin-top会加到外边的盒子上，导致内部的盒子margin-top设置失败，解决方法如下：
1、外部盒子设置一个边框
2、外部盒子设置 overflow:hidden
3、使用伪元素类：
              .clearfix:before{
                  content: '';
                  display:table;
              }
```

### 块元素,内联元素,内联块元素

### 解决内联元素间隙的方法

1、去掉内联元素之间的换行
2、将内联元素的父级设置font-size为0，内联元素自身再设置font-size

### display属性

display属性是用来设置元素的类型及隐藏的，常用的属性有：
1、none 元素隐藏且不占位置
2、block 元素以块元素显示
3、inline 元素以内联元素显示
4、inline-block 元素以内联块元素显示

### 浮点

float:left     左浮动

float:right     右浮动

### ★清除浮动

```
方法1：
.clearfix:after,.clearfix:before{ content: "";display: table;}
.clearfix:after{ clear:both;}
.clearfix{zoom:1;}
浮动的父级添加：
<div class="con2 clearfix">
方法2：
父级上增加属性overflow：hidden
.con2{... overflow:hidden}
```

## ★定位

```
relative：相对定位,不脱离文档流,相对于自己本身的位置进行定位,
absolute：绝对定位,脱离文档流,位置相对于已定位的父级,
	 如果没有父级,或父级没有定位,那么相对于文档的00点 (body)
 可以通过 z-index 属性定义层叠(先后),参数值越大,越先
 在style里面定义			
 .z1{z-index:1;background:#000;}
fixed：固定定位,脱离文档流,位置相对于浏览器窗口 进行定义
```
# javascrip

```
1, 在html页面中任意位置 书写 script标签,在标签内写js代码
2. 在元素 (标签) 内书写事件属性  来触发js代码的执行
3, 注意 ,在 包含src属性的script标签内不能在书写js代码
js 是运行在浏览器端的脚本语言,属于解释性语言.
```

```
锦定义变量时，用var关键字，不然严格模式会报错。
console。log(a) 在控制台打印值
alert()  弹框内容
typeof()函数   检测当前变量的数据类型
例    console.log(a,typeof(a))

```

### 使用场景

```
1, 注意 ,在 包含src属性的script标签内不能在书写js代码 
<script type="text/javascript" src="./1.js"></script>

2. 在元素 (标签) 内书写事件属性  来触发js代码的执行 -->
	<div onclick="alert('点我干啥?')" style="width: 200px;height: 200px;background: #369;"></div>
	<a href="javascript:alert('点你咋滴')">点一下试试</a>
	<a href="javascript:void(0)" onclick="alert('试试就试试')">再点一下试试</a>
!! void(0) 下面提示不显示值
	
3在html页面中任意位置 书写 script标签,在标签内写js代码 -->
	<script type="text/javascript">
		// alert('哎呦,不错哦');
	</script>
```

```
1、行间事件（主要用于事件）
<input type="button" name="" onclick="alert('ok！');">
2、页面script标签嵌入

<script type="text/javascript">
	var a = '你好！';
    alert(a);
</script>

3、外部引入

<script type="text/javascript" src="js/index.js"></script>
javascript语句与注释

1、一条javascript语句应该以“;”结尾

<script type="text/javascript">
var a = 123;
var b = 'str';
function fn(){
    alert(a);
};
fn();
</script>

2、javascript注释

<script type="text/javascript">
// 单行注释
var a = 123;
/*  
    多行注释
    1、...
    2、...
*/
var b = 'str';
</script>
```

### 常用方法

```
console.log(a) 			在控制台进行输出
alert(a)				弹出一个窗口
document.write(a)		向文档中输出一个文档流
如果遇到有-的单词，去掉-，后面的首字母大写，比如 fontSize.
document.write(a)		在页面进行输出。
标签对象.innerHTML="内容"；//在标签对象内放置指定内容
onclick                  单击事件
onsubmit				提交事件
docunment.getElementsByTagName  
	获取元素(比如 input,div)里的状态
document.getElementById
	获取id所属的状态
for (var i in window){
		document.write(i+'======'+window[i]+'<br>')	};
查看js的所有属性和方法，window是浏览器最大的对象。

var res = rr.constructor;    console.log(res);
查看当前对象的构造函数（当前这个对象和函数的上一层）
```

### 数据类型转换

```
typeof函数获取一个变量的类型：

* boolean - 如果变量是 Boolean 类型的
* number - 如果变量是 Number 类型的 (整数、浮点数)
* string - 如果变量是 String 类型的 （采用""、 ''）
* object - 如果变量是一种引用类型或 Null 类型的 
        如：new Array()/ new String()...
* function -- 函数类型
* undefined - 如果变量是 Undefined 类型的

数值类型 Number
	NaN  任何值与NaN进行比较,都是false,除了!=
	检测一个变量是否为NaN,只能使用isNaN()
字串类型 string
	var = 'a'
对象类型 object
	var a =new Object()
	数组类型  (表现类型为对象0bject)
		var a = new Array()    （数组）
		var a = [1,2,3,4]
	空（表现类型也为对象）
	var a = null
未定义 undefined
	var a  (直接定义不给值)
	
```

```
使用：Number（）、parseInt() 和parseFloat（） 做类型转换
  Number()强转一个数值(包含整数和浮点数)。
      整形和浮点型都可以，如果是纯数字，转数字，包含非数字时，转			NaN，可以转布尔
  *parseInt()强转整数，
      只能转整型 如果字符转中首字母是非数字，转为NaN
  *parseFloat（）强转浮点数 （最好用）
      整形和浮点都可以，如果字符串中首字母是非数字，转为NaN
      
函数isNaN()检测参数是否不是一个数字。
   isNaN()  is not a number
  		
ECMAScript 中可用的 3 种强制类型转换如下：

    Boolean(value) - 把给定的值转换成 Boolean 型；
		为假的情况：
   !!!     false,0,NaN,null,undefined,0.0,‘’。
   
    Number(value) - 把给定的值转换成数字（可以是整数或浮点数）；

    String(value) - 把给定的值转换成字符串；
```

### 运算符

```
++ 自加1    --自减
+ 后面是字符串进行连接，数字则进行相加
	（必须注意优先级，如果前面为字符串连接，后面也都为连接）
```

```
算 字 赋 比 逻 位 它

算术运算符
 + - * / ++ --
 
字符串连接
 +
 
赋值运算
 =    +=   -=   %=
 
比较运算符
 <  >    >=    <=    ==    ===   !=   !==
 === 值和类型都要相同    == 值相同
 
逻辑运算符
 && （与）   ||（或）  !
 
位运算
 ^    &    |   <<   >>
 
其它运算符
 ?   :    三元运算符
 
delete：用于删除对象中属性的   如：delete o.name; //删除o对象中的name属性
void：   void 运算符对任何值返回 undefined。没有返回值的函数真正返回的都是 undefined。
var iNum1=1, iNum2=2, iNum3=3;// 逗号运算符 用逗号运算符可以在
```

### 流程控制

```
if 判断值一样就可以

### else if中间必须有空格
if(判断){
  执行
}else if{
  执行
}else{
  执行
}
```

```
switch 的判断 ===  值和类型都一样

var a = 6;
swith(a){
  case 1:
  case 2:
  case 2:
  case 4:
  case 5:
  	alert{'工作日'};
  	break;
  case 6:
  case 7:
  	alert{'休息日'}；
  	break;       !!!!（如果这个祛除，default也会默认出现。）
  default:
  	alert{'火星人你好'}；
  	break;
}
```

### 循环

```
for循环

  for(var i=0;i<len;i++){
      ......
  }
  
while循环

  var i=0;
  while(i<8){
      ......
      i++;
  }
  
for-in 语句
for-in 语句是严格的迭代语句，用于枚举对象的属性。

  var a = [10,20,30,40,50];
  //迭代的是数组的下标。
  for(i in a){
     document.write(a[i]);
  }
  //输出： 1020304050
  
  ！！！简短写法
  for(car i =1;i<=10,i++){
			if(i == 7){
				continue;
			}
			if(i == 8){
				break;
			}
		}
```

### 元素获取

```
可以使用内置对象document上的getElementById方法来获取页面上设置了id属性的元素，获取到的是一个html对象，然后将它赋值给一个变量，比如：

<script type="text/javascript">
    var oDiv = document.getElementById('div1');
</script>

....

<div id="div1">这是一个div元素</div>
上面的语句，如果把javascript写在元素的上面，就会出错，因为页面上从上往下加载执行的，javascript去页面上获取元素div1的时候，元素div1还没有加载，解决方法有两种：

第一种方法：将javascript放到页面最下边
....
<div id="div1">这是一个div元素</div>
....
<script type="text/javascript">
    var oDiv = document.getElementById('div1');
</script>
</body>

第二种方法：将javascript语句放到window.onload触发的函数里面,获取元素的语句会在页面加载完后才执行，就不会出错了。
<script type="text/javascript">
    window.onload = function(){
        var oDiv = document.getElementById('div1');
    }
</script>
....

<div id="div1">这是一个div元素</div>
样式操作

标签对象.style.css属性名="值" //改变标签对象的样式。
示例：id.style.color="red";

注意：属性名相当于变量名,所以css属性名中含有双拼词的(font-size)的减号要去掉，将后面的首字母大写。fontSize

文本操作
标签对象.innerHTML="内容"；//在标签对象内放置指定内容
表单中值的操作
标签对象.value； //获取标签对象的value值
标签对象.value=”值“；//设置标签对象的value值
```

### 定时器

```
单次定时
setTimeout(要执行的代码，时间)  时间以毫秒算
clearTimeout 关闭只执行一次的定时器
```

```
多次计时
setInterval  反复执行的定时器
 clearInterval 关闭反复执行的定时器
 
 ！！一般都是用单次是来结束多次计时
```

```
做一个小动画图片流畅切换
<img src="./img/p1.png" alt="" id="tp">
	<script type="text/javascript">
	var tp = document.getElementById('tp');
	var i = 1;
	setInterval(function(){
		i++;
		if(i > 5){
			i = 1;
		}
		tp.src = './img/p'+i+'.png';
	},50)
	
	</script>
```

```
三种写法
1   var init = setTimeout(function(){
		alert('2');
	},2000);
	
function love(){
	console.log('22');
	}
	
2  setTimeout('love()',2000);
3  setTimeout(love,2000);
```

### 函数

```
*第一种是使用function语句定义函数
function abc(){
    alert('abc');
}

*第二种是在表达式中定义函数
var 函数名 = function(参数1，参数2，…\){
	alert('abc')；
};

！！！在使用函数时,如果没有传递参数,形参的默认值就是undefined

第三种是使用Function()构造函数来定义函数（不常用）
var 函数名 = new Function\(“参数1”，”参数2”，”参数3”……”函数体”\);
如：
var 函数名 = new Function\(”x”,”y”,”var z=x+y;return z;”\);
arguments 对象

在函数代码中，使用特殊对象 arguments，开发者无需明确指出参数名，就能访问它们。
例如，在函数 sayHi() 中，第一个参数是 message。用 arguments[0] 
也可以访问这个值，即第一个参数的值（第一个参数位于位置 0，
第二个参数位于位置 1，依此类推）。
关于变量和参数问题：

函数外面定义的变量是全局变量，函数内可以直接使用。
在函数内部没有使用var定义的=变量则为全局变量，
*在函数内使用var关键字定义的变量是局部变量，即出了函数外边无法获取。
js函数定义的参数没有默认值（目前只有最新的火狐浏览器支持）
```
### 优先级

```
如果有变量和函数通用一个变量名，函数会在执行时，优先加载。
函数会在执行时,优先加载,如果在代码中还有变量的定义和函数名一样,那么变量会覆盖函数
	！！！注意,函数名和变量名千万不要冲突
     //	var love = 222;

	function love(){
		alert('111');
	}

	love();
	// alert(love); (打印出来时一个函数)
```
### 对象

```
var obj = new Object();
	定义对象属性
    1，	obj.name = "张三";
		obj.sex = "女";
		obj.age = "18";
    2，  obj['age'] = 18;  
         var a = 'age';
		 obj[a] = 22;
		 
		alert(obj['age'])
	定义对象的方法
	1，	obj.sing = function(){
	 		alert('二营长')
	 	}
    2， 	var a = 'dance';
		obj[a] = function(){
	 		alert('你他娘的意大利炮呢');
		};
	  
	 	  obj.dance();
```

```
json
1,  var 对象名 = {属性名1：属性值，属性名2：属性值2，…….}
   var rr = {
		 	name:'玲玲',sex:'女',
			dance:function(){
	 						alert(this.name);
			}
		 };

2,  function person(a,sex,age){
	 	this.name = a;
	 	this.info =function(){
	 		alert(this.name);
	 	}
		
	 }
	 var a = new person('翠兰')
	 var b = new person('三炮')
 	 a.info()
```

### 数组

数组就是一组数据的集合，javascript中，数组里面的数据可以是不同类型的。

```
定义数组的方法

//对象的实例创建
var aList = new Array(1,2,3);

//直接量创建
var aList2 = [1,2,3,'asd'];
操作数组中数据的方法
1、获取数组的长度：aList.length;

var aList = [1,2,3,4];
alert(aList.length); // 弹出4
2、用下标操作数组的某个数据：aList[0];

var aList = [1,2,3,4];
alert(aList[0]); // 弹出1
3、push() 和 pop() 从数组最后增加成员或删除成员

var aList = [1,2,3,4];
aList.push(5);
alert(aList); //弹出1,2,3,4,5
aList.pop();
alert(aList); // 弹出1,2,3,4
4、unshift()和 shift() 从数组前面增加成员或删除成员

var aList = [1,2,3,4];
aList.unshift(5);
alert(aList); //弹出5,1,2,3,4
aList.shift();
alert(aList); // 弹出1,2,3,4
5、splice() 在数组中增加或删除成员

var aList = [1,2,3,4];
aList.splice(2,1,7,8,9); //从第2个元素开始，删除1个元素，然后在此位置增加'7,8,9'三个元素
alert(aList); //弹出 1,2,7,8,9,4
多维数组
多维数组指的是数组的成员也是数组的数组。

var aList = [[1,2,3],['a','b','c']];

alert(aList[0][1]); //弹出2;
```
### 正则

```
var str = 'aaaa1q?i+cn1312w4o_#ilovem4$2enshaizi ';
//转义字符
	var reg = /w/;
	var reg = /\w/; //单个字母数字下划线
	var reg = /\W/; //单个非字母数字下划线
	var reg = /\d/; //单个数字  
	var reg = /\D/; //单个非数字
	var reg = /\s/; //单个空白字符
	var reg = /\S/; //单个非空白字符
//元字符串
	var reg = /./; //除了换行外的任意字符
	var reg = /1*/; //匹配0次或多次(看第一个字符)
	var reg = /q+/; //匹配至少一次或多次
	var reg = /i+?/; //拒绝贪婪模式
	var reg = /a{3}/; //指定匹配次数
	var reg = /a{1,5}/; //指定匹配1-3次
	var reg = /[a-z,A-Z,_,0-9]+/;//指定字符范围
	var reg = /i(lo(v)e)m/;//子组
	var reg = /cn|com|net/;//或
//开头和结尾
	var reg = /^\w+\d$/; //开头除了特殊字符结尾数字
	var reg = /^\w{10,20}\d$/;
	//开头除了特殊数字匹配10-20次数字结尾
	var reg = /^\d+[a-z]+$/;//数字开头字母结尾
	var reg = /^\w+@\w{2,10}\.(cn|com)$/;//匹配邮箱
// 方法
	var res1 = reg.test(str);//返回布尔类型
	var res2 = reg.exec(str);
	//按照规则探索,有则以数组形式返回,无则返回null
	console.log(res1);
	console.log(res2);
```
### return作用

```
在函数中如果不写 return 或者只写return 没有返回指定值时 默认返回值 undefined;
在函数中写了return 代表当前函数要立即结束,并将结果返回

return flase 1 阻止事件冒泡  2 阻止元素的行为
```
## JQuery

### 选择器

```
$('li') //选择所有的li元素
$('#myId') //选择id为myId的网页元素
$('.myClass') // 选择class为myClass的元素
$('input[name=username]') 
// 选择name属性等于username的input元素
$('#ul1 li span') 
//空格层级获取选择id为为ul1元素下的所有li下的span元素
$('#id,.class');//逗号并列获取

对选择集进行修饰过滤(类似CSS伪类)

$('#ul1 li:first') //选择id为ul1元素下的第一个li
$('#ul1 li:odd') //选择id为ul1元素下的li的奇数行
$('#ul1 li:eq(2)') //选择id为ul1元素下的第3个li

对选择集进行函数过滤

$('div').has('p'); // 选择包含p元素的div元素
$('div').not('.myClass'); //选择class不等于myClass的div元素
$('div').filter('.myClass'); //选择class等于myClass的div元素
$('div').first(); //选择第1个div元素
$('div').eq(5); //选择第6个div元素

选择集转移

$('div').prev('p'); //选择div元素前面的第一个p元素
$('div').next('p'); //选择div元素后面的第一个p元素
$('div').children(); //选择div的所有子元素
$('div').siblings(); //选择div的同级元素
$('div').parent(); //选择div的父元素
$('#abc').parents(); //选择id为abc的所有的先辈元素
$('div').find('.myClass'); //选择div内的class等于myClass的元素
```

### 样式操作和获取操作

```
// 给当前的楼号加样式 其他移除
	$(this).addClass('cur').siblings().removeClass('cur')

// 获取div的样式
$("div").css("width");

//设置div的样式
$("div").css("width","30px");
 设置样式,多个样式
 $('.as').css({border:'2px solid red',background:'#666'});
```

```
//通过标签名获取元素 document.getElementsByTagName()
	//$('li').css('border','2px solid #f39');

//通过标签中的属性获取元素 []
	//$('li[name=y]').css('border','2px solid #f39');
	//$('img[width="100%"]').css('border','2px solid #f39');
	//$('img[name=logo]').css('border','2px solid #f39');

//空格 层级关系获取元素
	//$('#images li').css('border','2px solid #f39');
//逗号 并列获取
	//$('.w,#img').css('border','2px solid #f39');
//选择id为menu元素下的第一个li
	//$('#menu li:first').css('border','2px solid #f39');
/选择id为section元素下的li的奇数行
	// $('#section li:odd').css('border','2px solid #f39');
	// $('#section li:even').css('border','2px solid #f63');
//选择id为section元素下的第3个li 下标从0开始
	// $('#section li:eq(1)').css('border','2px solid #f63');
//id为section 前面第一个div元素
	//$('#footer').prev('p').css('color','#f39');
//id为section 后面第一个div元素
	//$('#section').next('p').css('color','#f63');
//选择images的所有子元素
	//$('#images').children().css('border','2px solid #f63');
//选择id为acc的同级元素
	//$('#acc').siblings().css('border','2px solid #f39');
//选择id为acc的父级元素
	//$('#acc').parent().css('border','2px solid #f63');
//选择id为acc的所有的先辈元素
	//$('#acc').parents().css('border','2px solid #f39');
//选择id为acc的先辈元素中 id为all的元素
	//$('#acc').parents('#all').css('border','2px solid #f63');
//选择id为images下的id为acc元素
	var c = $('#images').find('#acc');
	console.log(c)
```

### 类名操作

```
操作样式类名

$("#div1").addClass("divClass2") //为id为div1的对象追加样式divClass2
$("#div1").removeClass("divClass")  //移除id为div1的对象的class名为divClass的样式
$("#div1").removeClass("divClass divClass2") //移除多个样式
$("#div1").toggleClass("anotherClass") //重复切换anotherClass样式
```

### 文本操作

```
$('#as').html('<span style="color:red">11</span>')
	可以执行的样式操作
$('#as').text('<span style="color:blue">22</span>')
	取出或添加文本内容
var r = $('#as').html();
var b = $('#as').text();
```

### 属性操作

```
属性操作

1、attr() 取出或设置某个属性的值
// 取出图片的地址
var $src = $('#img1').attr('src');
$("input[name='sex'][value='{{user.sex}}']").attr("checked", true);
选择框尾name时sex,值为当前选项的添加默认选项

// 设置图片的地址和alt属性
$('#img1').attr({ src: "test.jpg", alt: "Test Image" });

//也可以用户设置class属性
$('#abc').attr('class','all')

//也可以自定义 属性
$('#abc').attr('love','iloveyou')

2、removeattr()删除属性
$('#abc').removeattr('class')
$('#abc').removeattr('love')
3 toggleClass()
如果存在,则移除,如果不存在.则添加
$('#as').toggleClass('myclass');
```
### 获取尺寸操作

```
1 获取元素距离文档偏移量
	//var innero = $('.inner').offset();
	var innerTo = $('.inner').offset().top
	
2  获取当前元素相对于父级元素的偏移量 
	//var innerp = $('.inner').position();
	
3  获取文档滚动的距离  
	 var wt = $(window).scrollTop();
	 
4  快速获取元素的宽高
	// var w = $('.inner').width();
	// var h = $('.inner').height();

5   设置元素的宽高
	// var w = $('.inner').width(200);
	// var h = $('.inner').height(100);

6   获取可视区域的宽高 
	// var ww = $(window).width();
	// var wh = $(window).height();

7    获取整个文档的宽高
	var dw = $(document).width();
	var dh = $(document).height();
```

### 事件

```
方法绑定
1 click
2 bind  方法绑定			bind('dblclick',function(){
3 live   动态方法绑定			live('click',function(){
4 trigger   自动触发    		$('#move').trigger('click');
5  解除事件绑定
	$('#move').die('click')   解除动态绑定
	 $('#move').unbind()

单击事件 click
双击事件 dblclick			鼠标抬起 mouseup
鼠标按下 mousedown			鼠标右键 oncontextmenu
					window.oncontextmenu = function(){
							alert(2);}
鼠标移入 mouseover			鼠标移出  mouseout
鼠标移动查看位置:
	$('.move').mousemove(function(e){
		// 鼠标相对于浏览器的窗口 
		var x = e.clientX;
		var y = e.clientY;

		// 鼠标相对于文档的窗口
		// var x = e.pageX;
		// var y = e.pageY;
		console.log(x,y)
	})
	
键盘按下 keydown       键盘抬起  keyup
//获取按键信息    function里一般传入参数 e 
var k = e.keyCode;

获取焦点事件 focus        丧失焦点事件  blur
改变值之后的事件 change

文档滚动事件,当文档发动滚动时触发的事件
	$(window).scroll(InitScroll);
网页加载事件   window.onload = function(){}
```

### 节点操作

```
创建节点
var $div = $('<div>');

在元素内部尾部添加   append
在元素内部头部添加	prepend
在元素外部头部添加	before
在元素外部尾部添加	after
删除				 remove
清空				 empty
克隆				 clone
弹出一个询问框,带有取消和确定按钮,返回布尔类型
var res = confirm('您确定要删除这个元素码?');
```
### 效果

```
!所有的效果后面都可以加时间.

$('#move').show(2000); //显示
$('#move').slideDown();//滑动显示
$('#move').fadeIn();//渐变

$('#move').hide(2000);//隐藏
$('#move').slideUp;//滑动隐藏
$('#move').fadeOut();//渐变

$('#move').toggle(2000);//隐藏和显示切换
$('#move').slideToggle(2000);//滑动隐藏和显示切换
$('#move').fadeToggle(2000);//渐变隐藏和显示切换

自定义动画
$('#move').animate({
	width:'300px',height:'400px',
	top:'100px',left:'100px',
	borderRadius:'50%'
},3000)

$('#move').stop();		暂停动画效果
		
// 延时执行自定义动画  (delay 延时多长时间 )
$('#move').delay(1000).animate({
	width:'300px',height:'400px',
	top:'100px',left:'100px',
	borderRadius:'50%',
		},4000)
		

	// 绑定文档滚动事件
	$(window).scroll(function(){
		// 获取整个文档的高度
		var dH = $(document).height();
		// 获取可视区域的高度
		var cH = $(window).height;
		// 获取文档的滚动距离
		var dT = $(window).scrollTop();
		// 判断 是否触底
		if(dT == dH-cH){
			requestGoods();
		}
	})
```
### json

```
json是 JavaScript Object Notation 的首字母缩写，单词的意思是javascript对象表示法，这里说的json指的是类似于javascript对象的一种数据格式，目前这种数据格式比较流行，逐渐替换掉了传统的xml数据格式。

javascript对象字面量：
var tom = {
    name:'tom',
    age:18
}

json格式的数据：
{
    "name":'tom',
    "age":18
}

与json对象不同的是，json数据格式的属性名称需要用双引号引起来，用单引号或者不用引号会导致读取数据错误。

json的另外一个数据格式是数组，和javascript中的数组字面量相同。
['tom',18,'programmer']
```

### ajax   异步和同步

```
AJAX 是与服务器交换数据并更新部分网页的艺术，在不重新加载整个页面的情况下。
通过 HTTP 请求加载远程数据

jQuery 底层对 AJAX 实现进行了封装.使得我们在进行ajax操作时,不必像原生js中那么复杂
$.get, $.post, $.ajax() 返回其创建的 XMLHttpRequest 对象。多数情况下我们不需要去操作返回的对象

/发送ajax请求 1.url  2.可选 发送get请求时携带的参数  ,3,可选 回调函数,请求完之后做什么事  4,可选,返回的数据类型 json
$.get(url,{携带的参数},function(data){},'json');

$.post(url,{携带的参数},function(data){},'json');

$.ajax({
  url:'/cgi-bin/1.py',   当前请求的url地址
  type:'post',			当前请求的方式 get post
  data:{name:'fei'},	 请求时携带的参数
  dataType:'json',		 返回的数据类型
  success:function(data){	 请求成功后执行的代码
    alert('请求成功')
  },
  error:function(){			请求失败后执行的代码
  alert('请求错误')
  },
  timeout:2000,     毫秒		设置当前请求的超时时间,必须异步
  async:false   ture异步, flase 同步
})
```

```
ajax异步 同步

//设置ajax的全局配置  async:false 设置当前请求为同步
$.ajaxSetup({
    async:false
})

关于ajax中 异步 和 同步 
ajax默认就是异步请求,
async (默认: true) 默认设置下，所有请求均为异步请求。
如果需要发送同步请求，请将此选项设置为 false。
同步请求,就发ajax请求发出去后必须等待ajax的结果返回后才能继续往下执行
一般情况下都使用异步操作就可以,除非有特殊情况,必须等ajax的结果回来后才能做处理的,就用同步
```

```
注意
1.ajax是无刷新请求服务器,所以我们在浏览器中是感觉不到,也看不到ajax的具体请求和执行情况的.,
    因此我们需要借助浏览器的调试工具 (F12打开) 进行查看

2.ajax的请求是基础HTTP协议的,就要求你当前打开这个带有ajax的html时必须使用http协议

3.ajax要求同源策略
    http://127.0.0.1:8000/cgi-bin/1.py
    即: 协议(http https)  域名或IP 以及端口(80 443 8000 8080 ...)都必须一致

4.关于返回的数据类型 在get() post() ajax() 都可以设置返回的数据类型 'json'
    如果要求返回json格式数据,那么就必须返回json,如果不正确,
    在get和post方法将拿不到data中返回的数据,在ajax方法中则会进去error方法

5.在python中返回json格式数据,
    引入 json模块
    json.dumps(数据)  使用json_dumps方法进行json格式的编码转换

6.在使用ajax方法时.会创建一个对象 XMLHttpRequest
    那么在ajax的方法中使用的 $(this) 就代表 ajax的对象

    $(this) 永远代表一个对象,没有指明对象时 代表的时window对象,
    在它有对象时 代表的就是当前的这个对象
```
### ajax注意

```
在ajax使用$(this)时,一定要用变量接受
var uid=$(this).parents('tr').find('td:first').text()
		var btn = $(this)
```
### Bootstrap

```
head格式(注意:js需要改名)
<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link href="./public/css/bootstrap.min.css" rel="stylesheet">
    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="./public/js/jquery-1.12.4.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="./public/js/bootstrap.min.js"></script>
```
# 商城统计

```
	window.onload=function(){
    var x = document.getElementsByName('xiaoji'); ##小计的name
    var num = 0;
    for (var i = x.length - 1; i >= 0; i--) {
        console.log($(x[i]).text());
        num = num +  parseInt($(x[i]).text());
    };
    console.log(num);
    $('.zj').html(num);
}
```
    