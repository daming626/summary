### json简介

```
JSON(JavaScript Object Notation, JS 对象简谱) 是一种轻量级的数据交换格式。它基于 ECMAScript (欧洲计算机协会制定的js规范)的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。
```

## 二、js中Json对象与Json字符串互转(4种转换方式)

```
**1>jQuery插件支持的转换方式**： 

复制代码代码如下:

$.parseJSON( jsonstr ); //jQuery.parseJSON(jsonstr),可以将json字符串转换成json对象 

2>浏览器支持的转换方式(Firefox，chrome，opera，safari，ie9，ie8)等浏览器： 

复制代码代码如下:

JSON.parse(jsonstr); //可以将json字符串转换成json对象 
JSON.stringify(jsonobj); //可以将json对象转换成json对符串 


注：ie8(兼容模式),ie7和ie6没有JSON对象，推荐采用JSON官方的方式，引入json.js。 

3>Javascript支持的转换方式： 
eval('(' + jsonstr + ')'); //可以将json字符串转换成json对象,注意需要在json字符外包裹一对小括号 
注：ie8(兼容模式),ie7和ie6也可以使用eval()将字符串转为JSON对象，但不推荐这些方式，这种方式不安全eval会执行json串中的表达式。 

4>JSON官方的转换方式： 
http://www.json.org/提供了一个json.js,这样ie8(兼容模式),ie7和ie6就可以支持JSON对象以及其stringify()和parse()方法； 
可以在https://github.com/douglascrockford/JSON-js上获取到这个js，一般现在用json2.js。
```



