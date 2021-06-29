衍生过程

Servlet：动态产生网页太麻烦

JSP：<% java代码 %>

JSTL：替代了JSP中的Java代码

### jstl简介

```
JSTL（Java server pages standarded tag library，即JSP标准标签库）是由JCP（Java community Proces）所制定的标准规范，它主要提供给Java Web开发人员一个标准通用的标签库，并由Apache的Jakarta小组来维护。开发人员可以利用这些标签取代JSP页面上的Java代码，从而提高程序的可读性，降低程序的维护难度。
```

### 用例

```html
1、
	request.setAttribute("users",user);

2、
    <%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false" %>
    <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

3、
    <script src="http://cdn.staticfile.org/jquery/3.6.0/jquery.js"></script>

4、
	<c:forEach items="${users.roleList[0].treeList}" var="tree" varStatus="status">
        <c:choose>
            <c:when test="${tree.fatherTreeId eq null}">
                <li class="father">
                    <a href="javascript:void(0)">${tree.title} <img id="img" src="images/jt.png" alt="kk"></a>
                </li>
            </c:when>
            <c:otherwise>
                <ul class="second">
                    <li class="son">
                        <a href="javascript:void(0)">${tree.title}</a>
                    </li>
                </ul>
            </c:otherwise>
        </c:choose>
	</c:forEach>
```

