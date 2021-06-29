### javascript简介

```
JavaScript，与Java没有任何关系，为了蹭Java的热度
vbscript：微软的
操作DOM，操作网页中的元素
document object model
高级：ES6、原型、函数与闭包（函数作为参数传递）

JavaScript用于控制html
例如
JavaScript 能够改变 HTML 内容
JavaScript 能够改变 HTML 属性
JavaScript 能够改变 HTML 样式 (CSS)
JavaScript 能够隐藏 HTML 元素
JavaScript 能够显示 HTML 元素

调用方法
1、在html中<script></script>
2、建立 名称.js文件，然后在html中调用<script src="名称.js"></script>

对象
内置对象：Array String Date Number
宿主对象：宿主是指浏览器
自定义对象
```

### 用法

```html
JavaScript是一个弱类型语言
variable：变量英文单词
js中变量都用var进行声明，甚至变量不需要声明？！

阻止超链接的默认行为 <a href="javascript:void(0)" ></a>

var a=3;
console.log(typeof a)//打印a的数据类型
typeof是一个运算符

==：等于,要求值一样为true
===：严格等于，要求值和类型一样为true
例：
<script>
    var a=2
    var b=2
    var c='abc'
    var d="abc"
    var e="2"
    console.log(typeof a)	//输出：number
    console.log(typeof b) 	//输出：number
    console.log(typeof c)	//输出：string
    console.log(typeof d)	//输出：string
    console.log(typeof e)	//输出：string
    console.log(a==b)	//输出：true
    console.log(a===b)	//输出：true
    console.log(c==d)	//输出：true
    console.log(c===d)	//输出：true
    console.log(a==e)	//输出：true
    console.log(a===e)	//输出：false
    
    var f=new Array(1,2,3)
    var g=[1,2,3]
    console.log(typeof f)	//输出：object
    console.log(typeof g)	//输出：object
    console.log(f instanceof Array)	//输出：true
    console.log(g instanceof Array)	//输出：true
    
    var h=new Object()
    h.setId=111
    h.setName="大明"
    for(prop in h){	//输出：setId setName
        console.log(prop)
    }
    console.log(h.setId)	//输出：111
    console.log(h.setName)	//输出：大明
    delete h.setId
    for(prop in h){	//输出：setName
        console.log(prop)
    }
</script>


```

### 函数

```javascript
function f1(){
	console.log("aaa")
	console.log(arguments[0])
	console.log(arguments[1])
	console.log(arguments[2])
	return 3
}

function f2(id,name,address){//不需要数据类型
	console.log(id)
	console.log(name)
	console.log(address)
}

var a=f1()	//第一次调用f1
console.log(a)
f1(5,6,7)	//第二次调用f1，没有形参也是传参数

f2(123,"大明","桂电")

输出：
aaa
undefined
undefined
undefined
3
aaa
5
6
7
123
大明
桂电

```

### 对象

```javascript
var stu=new Object()

stu.stuId=1111
stu.stuName='陈立鹏'
stu.address="桂林电子科技大学"

//输出一个对象的属性
for(prop in stu){
	console.log(prop)
}
//输出对象的属性值
//两种方式
//1.对象.属性名
//2.对象[属性名]
for(prop in stu){
	console.log("属性值："+stu[prop]);
}
console.log("拼字符串输出属性值："+stu['stu'+'Id']);


var book={
	"bookId":11111,
	'bookName':'Java网络编程',
	'bookPublisher':'电子工业出版社',
}
console.log(typeof book);
for(prop in book){
	console.log(prop);
}

var student={
	'stuId':1111,
	'stuName':'陈立鹏',
	'course':{
		'courseId':22222,
		'courseName':'Java网络',
		'courseScore':3
	}
}
console.log('--------------------------');
console.log(typeof student.course);//判断course是一个什么类型？

输出：
stuId
stuName
address
属性值：1111
属性值：陈立鹏
属性值：桂林电子科技大学
拼字符串输出属性值：1111
object
bookId
bookName
bookPublisher
--------------------------
object

```

### 事件

```
常用的HTML事件
1、onblur：浏览器可以监听失去焦点事件，可以针对这个事件进行处理，通常是某个事件触发调用javascript的函数（自定义函数） 
2、onchange：当对象或选中区的内容改变时触发。
3、onclick：在用户用鼠标左键单击对象时触发。
4、onkeydown：当用户按下键盘按键时触发。
5、onkeyup：当用户释放键盘按键时触发。
6、onload：在浏览器完成对象的装载后立即触发。
7、onmousedown：当用户用任何鼠标按钮单击对象时触发。
8、onmousemove：当用户将鼠标划过对象时触发。
9、onmouseout：当用户将鼠标指针移出对象边界时触发。
10、onmouseover：当用户将鼠标指针移动到对象内时触发。
11、onmouseenter：当用户将鼠标指针移动到对象内时触发。
12、onmouseleave：当用户将鼠标指针移出对象边界时触发。
```

### 事件处理

```html
1、在元素节点中 onclick="test()"声明
调用：
<script>
    window.onload=function(){	//先加载全部代码
		function test(){}
    }
</script>

2、不声明，直接
<script>
    window.onload = aaa	//先加载全部代码
    function aaa(){
    	通过id拿到某个对象a (document.getElementById("id名称"))
    	a.onclick=function(){}
    }
</script>

var interval = setInterval(f1,3000)
clearInterval(interval)/*此处放入变量，而不是setInterval(f1,3000)*/
```

