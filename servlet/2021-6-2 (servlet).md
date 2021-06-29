### servlet简介

```
	Servlet（Server Applet）是Java Servlet的简称，称为小服务程序或服务连接器，用Java编写的服务器端程序，具有独立于平台和协议的特性，主要功能在于交互式地浏览和生成数据，生成动态Web内容。
	
	狭义的Servlet是指Java语言实现的一个接口，广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。Servlet运行于支持Java的应用服务器中。从原理上讲，Servlet可以响应任何类型的请求，但绝大多数情况下Servlet只用来扩展基于HTTP协议的Web服务器。
	
	最早支持Servlet标准的是JavaSoft的Java Web Server，此后，一些其它的基于Java的Web服务器开始支持标准的Servlet。
```

### servlet-mapping(文件web.xml)

```xml
servlet-mapping 即servlet映射

<servlet>
    <servlet-name>Servlet</servlet-name>
    <servlet-class>edu.guet.servlet.LoginServlet</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>Servlet</servlet-name>
    <url-pattern>*.do</url-pattern><!--后缀形式-->
</servlet-mapping>
<servlet-mapping>
    <servlet-name>Servlet</servlet-name>
    <url-pattern>/LoginServlet</url-pattern><!--路径形式-->
</servlet-mapping>

此处相同的Servlet为桥梁
edu.guet.servlet.LoginServlet为后端
<url-pattern>为前端访问的地址，主要分为两种形式，后缀形式和路径形式，前端通过此地址访问到后端
    
通过servlet-mapping(映射)将前后端连接起来
```

### 创建一个类来处理前后端数据的交互

```java
public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        
        }
    }
}

doget和dopost区别：
    
    1、生成方式
get方式有四种：1）直接在URL地址栏中输入URL。2）网页中的超链接。3）form中method为get。4）form中method为空时，默认是get提交。
post只知道有一种：form中method属性为post。

2、数据传送方式
get方式：表单数据存放在URL地址后面。所有get方式提交时HTTP中没有消息体。
post方式：表单数据存放在HTTP协议的消息体中以实体的方式传送到服务器。

3、服务器获取数据方式
GET方式：服务器采用request.QueryString来获取变量的值。
POST方式：服务器采用request.Form来获取数据。

4、传送的数据量
GET方式：数据量长度有限制，一般不超过2kb。因为是参数传递，且在地址栏中，故数据量有限制。
POST方式：适合大规模的数据传送。因为是以实体的方式传送的。

5、安全性
GET方式：安全性差。因为是直接将数据显示在地址栏中，浏览器有缓冲，可记录用户信息。所以安全性低。
POST方式：安全性高。因为post方式提交数据时是采用的HTTP post机制，是将表单中的字段与值放置在HTTP HEADER内一起传送到ACTION所指的URL中，用户是看不见的。

6、在用户刷新时
GET方式：不会有任何提示、
POST方式：会弹出提示框，问用户是否重新提交

get是从服务器上获取数据，post是向服务器传送数据。
get是把参数数据队列加到提交表单的ACTION属性所指的URL中，值和表单内各个字段一一对应，在URL中可以看到。post是通过HTTP post机制，将表单内各个字段与其内容放置在HTML HEADER内一起传送到ACTION属性所指的URL地址。用户看不到这个过程。
对于get方式，服务器端用Request.QueryString获取变量的值，对于post方式，服务器端用Request.Form获取提交的数据。
get传送的数据量较小，不能大于2KB。post传送的数据量较大，一般被默认为不受限制。但理论上，IIS4中最大量为80KB，IIS5中为100KB。
get安全性非常低，post安全性较高。但是执行效率却比Post方法好。 建议： 1、get方式的安全性较Post方式要差些，包含机密信息的话，建议用Post数据提交方式；2、在做数据查询时，建议用Get方式；而在做数据添加、修改或删除时，建议用Post方式；
Servlet的doGet/doPost 是在 javax.servlet.http.HttpServlet 中实现的
doGet：处理GET请求
doPost：处理POST请求
当发出客户端请求的时候，调用service方法并传递一个请求和响应对象。Servlet首先判断该请求是GET操作还是POST 操作。然后它调用下面的一个方法：doGet 或 doPost。如果请求是GET就调用doGet方法，如果请求是POST就调用doPost方法。doGet和doPost都接受请求(HttpServletRequest)和响应(HttpServletResponse)。

```

```
历史：
WEB-INF中存放classes、lib、web.xml等
```

### 前后端数据交互

```
前端到后端：
后端通过doget，dopost拿到前端的访问数据
方法：
1、在表单中提交数据,后端通过request.getParameter("名称")拿到前端的值，名称为name属性的属性值
2、地址栏？第一个参数名称=第一个参数&第二个参数名称=第二个参数.....，后端通过request.getParameter("地址栏参数名称")拿到前端的值

后端到前端：
后端大数据发送到前端，拿到数据后，加入xxx作用域、例如request、session、application
```

### session的生命周期

```
session的生命周期
session的生命周期包括三个阶段：创建、活动、销毁
创建：
当客户端第一次访问某个jsp或者servlet的时候，服务器会为当前会话创建一个SessionId，每次客户端向服务器发送请求时，都会将此sessionId携带过去，服务端会对此sessionId进行校验。
活动：
某次会话当中通过超链接打开的新页面属于同义词会话。
只要当前页面没有全部关闭，重新打开新的浏览器窗口访问同一项目资源时属于同一次会话。

本次会话的所有页面都关闭后再重新访问某个Jsp或者Servlet将会创建新的会话。

注意事项：注意原有会话还存在，只是这个旧的SessionID任然存在服务端，只不过再也没有客户端会携带它然后交予服务端校验。
销毁：
Session的销毁只有三种方式：
1.调用了session.invalidate()方法
2.session过期（超时）
3.服务器重新启动

Tomcat默认session超时时间为30分钟。
```



### 请求转发和重定向的区别

```
一、请求转发和重定向
请求转发：
request.getRequestDispatcher(URL地址).forward(request, response)

处理流程：

客户端发送请求，Servlet做出业务逻辑处理。
Servlet调用forword()方法，服务器Servlet把目标资源返回给客户端浏览器。

请求转发
2）重定向：
response.sendRedirect(URL地址)

处理流程：

客户端发送请求，Servlet做出业务逻辑处理。
Servlet调用response.sendReadirect()方法，把要访问的目标资源作为response响应头信息发给客户端浏览器。
客户端浏览器重新访问服务器资源xxx.jsp，服务器再次对客户端浏览器做出响应。

重定向
以上两种情况，你都需要考虑Servlet处理完后，数据如何在jsp页面上呈现。图例是请求、响应的流程，没有标明数据如何处理、展现。

二、转发和重定向的路径问题
1）使用相对路径在重定向和转发中没有区别
2）重定向和请求转发使用绝对路径时，根/路径代表了不同含义
重定向response.sendRedirect("xxx")是服务器向客户端发送一个请求头信息，由客户端再请求一次服务器。/指的Tomcat的根目录,写绝对路径应该写成"/当前Web程序根名称/资源名" 。如"/WebModule/login.jsp","/bbs/servlet/LoginServlet"
转发是在服务器内部进行的，写绝对路径/开头指的是当前的Web应用程序。绝对路径写法就是"/login.jsp"或"/servlet/LoginServlet"。

总结：以上要注意是区分是从服务器外的请求，还在是内部转发，从服务器外的请求，从Tomcat根写起(就是要包括当前Web的根)；是服务器内部的转发，很简单了，因为在当前服务器内，/写起指的就是当前Web的根目录。

三、转发和重定向的区别
request.getRequestDispatcher()是容器中控制权的转向，在客户端浏览器地址栏中不会显示出转向后的地址；服务器内部转发，整个过程处于同一个请求当中。
response.sendRedirect()则是完全的跳转，浏览器将会得到跳转的地址，并重新发送请求链接。这样，从浏览器的地址栏中可以看到跳转后的链接地址。不在同一个请求。重定向，实际上客户端会向服务器端发送两个请求。
所以转发中数据的存取可以用request作用域：request.setAttribute(), request.getAttribute()，重定向是取不到request中的数据的。只能用session。

forward()更加高效，在可以满足需要时，尽量使用RequestDispatcher.forward()方法。（思考一下为什么？）

RequestDispatcher是通过调用HttpServletRequest对象的getRequestDispatcher()方法得到的，是属于请求对象的方法。
sendRedirect()是HttpServletResponse对象的方法，即响应对象的方法，既然调用了响应对象的方法，那就表明整个请求过程已经结束了，服务器开始向客户端返回执行的结果。

重定向可以跨域访问，而转发是在web服务器内部进行的，不能跨域访问。
```



