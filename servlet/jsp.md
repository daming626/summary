### jsp

```
JSP是动态网页技术，出现在Servlet技术之后的,JSP技术是为了解决Servlet的开发效率低下,不方便开发人员开发,其本质还是Servlet
```

### 语法

```
用<%@ page session="false"%> 指不能在本页使用session。也就是在本页面禁用session。
request.getSession(false)是指如果存在session就返回session，如果不存在就返回一个null值；
request.getSession(true)是指如果存在session就返回session，如果不存在就创建一个新的session。
```

### jsp有哪些内置对象？作用分别是什么？

```
1.HttpServletRequet类的Request对象：代表请求对象，主要用于接受客户端通过HTTP协议连接传输服务器端的数据。

2.HttpSevletResponse类的Response对象：代表响应对象，主要用于向客户端发送数据。

3.JspWriter类的out对象：主要用于向客户端输出数据，out的基类是jspWriter

4.HttpSession类的session对象：主要用来分别保存每个月的信息与请求关联的会话；会话状态的维持是web应用开发者必须面对的问题。

5.ServletContext类的application对象：主要用于保存用户信息，代码片段的运行环境；它是一个共享的内置对象，即一个容器中的多个用户共享一个application

，故其保存的信息被所有用户所共享。

6.PageContext类的PageContext对象：管理网页属性，为jsp页面包装页面的上下文，管理对属于jsp的特殊可见部分中已经命名对象的访问，它的创建和初始化都是由容器来完成的。

7.ServletConfig类的Config对象：代码片段配置对象，标识Servlet的配置。

8.Object类的Page对象，处理jsp页面，是object类的一个实例，指的是jsp实现类的实例

9.Exception对象：处理jsp文件执行时发生的错误和异常，只有在错误页面里才使用，前提是在页面指令里要有isErrorPage=true
```



