---
title: JSP 语法
date: 2017/11/08
categories:
- javaee
tags:
- javaee
- jsp
---

本小节将会简单地介绍一下JSP开发中的基础语法。

------

## 脚本

脚本程序可以包含任意量的Java语句、变量、方法或表达式，只要它们在脚本语言中是有效的。

脚本程序的语法格式：

```jsp
<% 代码片段 %>
```

或者，您也可以编写与其等价的XML语句，就像下面这样：

```jsp
<jsp:scriptlet>
   代码片段
</jsp:scriptlet>
```

任何文本、HTML标签、JSP元素必须写在脚本程序的外面。

下面给出一个示例，同时也是本教程的第一个JSP示例：

```jsp
<html>
<head><title>Hello World</title></head>
<body>
Hello World!<br/>
<%
out.println("Your IP address is " + request.getRemoteAddr());
%>
</body>
</html>
```

**注意：**请确保Apache Tomcat已经安装在C:\apache-tomcat-7.0.2目录下并且运行环境已经正确设置。

将以上代码保存在hello.jsp中，然后将它放置在 C:\apache-tomcat-7.0.2\webapps\ROOT目录下，打开浏览器并在地址栏中输入http://localhost:8080/hello.jsp。运行后得到以下结果：

![img](http://www.runoob.com/wp-content/uploads/2014/01/jsp_hello_world.jpg)

### 中文编码问题

如果我们要在页面正常显示中文，我们需要在 JSP 文件头部添加以下代码：<>

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
```

接下来我们将以上程序修改为：

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
Hello World!<br/>
<%
out.println("你的 IP 地址 " + request.getRemoteAddr());
%>
</body>
</html>
```

这样中文就可以正常显示了。

## JSP声明

一个声明语句可以声明一个或多个变量、方法，供后面的Java代码使用。在JSP文件中，您必须先声明这些变量和方法然后才能使用它们。

JSP声明的语法格式：

```jsp
<%! declaration; [ declaration; ]+ ... %>
```

或者，您也可以编写与其等价的XML语句，就像下面这样：

```jsp
<jsp:declaration>
   代码片段
</jsp:declaration>
```

程序示例：

```jsp
<%! int i = 0; %> 
<%! int a, b, c; %> 
<%! Circle a = new Circle(2.0); %> 
```

## JSP表达式

一个JSP表达式中包含的脚本语言表达式，先被转化成String，然后插入到表达式出现的地方。

由于表达式的值会被转化成String，所以您可以在一个文本行中使用表达式而不用去管它是否是HTML标签。

表达式元素中可以包含任何符合Java语言规范的表达式，但是不能使用分号来结束表达式。

JSP表达式的语法格式：

```
<%= 表达式 %>
```

同样，您也可以编写与之等价的XML语句：

```
<jsp:expression>
   表达式
</jsp:expression>
```

程序示例：

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
<p>
   今天的日期是: <%= (new java.util.Date()).toLocaleString()%>
</p>
</body> 
</html> 
```

运行后得到以下结果：

```
今天的日期是: 2016-6-25 13:40:07
```

------

## JSP注释

JSP注释主要有两个作用：为代码作注释以及将某段代码注释掉。

JSP注释的语法格式：

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>JSP注释示例</title>
</head>
<body>
<%-- 该部分注释在网页中不会被显示--%> 
<p>
   今天的日期是: <%= (new java.util.Date()).toLocaleString()%>
</p>
</body> 
</html> 
```

运行后得到以下结果：

```
今天的日期是: 2016-6-25 13:41:26
```

不同情况下使用注释的语法规则：

| **语法**       | 描述                           |
| ------------ | ---------------------------- |
| <%-- 注释 --%> | JSP注释，注释内容不会被发送至浏览器甚至不会被编译   |
| <!-- 注释 -->  | HTML注释，通过浏览器查看网页源代码时可以看见注释内容 |
| <\%          | 代表静态 <%常量                    |
| %\>          | 代表静态 %> 常量                   |
| \'           | 在属性中使用的单引号                   |
| \"           | 在属性中使用的双引号                   |

## 控制语句

JSP提供对Java语言的全面支持。您可以在JSP程序中使用Java API甚至建立Java代码块，包括判断语句和循环语句等等。

### if…else语句

`If…else`块，请看下面这个例子：

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8"%>
<%! int day = 1; %>
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>02.JSP语法 - if...else示例</title>
</head>
<body>
<h3>IF...ELSE 实例</h3>
<% if (day == 1 | day == 7) { %>
<p>今天是周末</p>
<% } else { %>
<p>今天不是周末</p>
<% } %>
</body>
</html>
```

运行后得到以下结果：

```
IF...ELSE 实例
今天不是周末
```

### switch…case语句

现在来看看switch…case块，与if…else块有很大的不同，它使用out.println()，并且整个都装在脚本程序的标签中，就像下面这样：

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8"%>
<%! int day = 3; %>
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>02.JSP语法 - switch...case示例</title>
</head>
<body>
<h3>Sswitch...case示例</h3>
<%
  switch(day) {
    case 0:
      out.println("星期天");
      break;
    case 1:
      out.println("星期一");
      break;
    case 2:
      out.println("星期二");
      break;
    case 3:
      out.println("星期三");
      break;
    case 4:
      out.println("星期四");
      break;
    case 5:
      out.println("星期五");
      break;
    default:
      out.println("星期六");
  }
%>
</body>
</html>
```

浏览器访问，运行后得出以下结果：

```
SWITCH...CASE 实例

星期三
```

### 循环语句

在JSP程序中可以使用Java的三个基本循环类型：for，while，和 do…while。

让我们来看看for循环的例子，以下输出的不同字体大小的"菜鸟教程"：

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%! int fontSize; %> 
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
<h3>For 循环实例</h3>
<%for ( fontSize = 1; fontSize <= 3; fontSize++){ %>
   <font color="green" size="<%= fontSize %>">
    菜鸟教程
   </font><br />
<%}%>
</body> 
</html> 
```

运行后得到以下结果：

![img](http://www.runoob.com/wp-content/uploads/2014/01/7B4B85CF-FE4B-43CB-AAFF-F8594AD4342C.jpg)

将上例改用while循环来写：

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%! int fontSize; %> 
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
<h3>While 循环实例</h3>
<%while ( fontSize <= 3){ %>
   <font color="green" size="<%= fontSize %>">
    菜鸟教程
   </font><br />
<%fontSize++;%>
<%}%>
</body> 
</html> 
```

浏览器访问，输出结果为（fontSize 初始化为0，所以多输出了一行）：

![img](http://www.runoob.com/wp-content/uploads/2014/01/4F744CC9-E484-45BA-AF18-27AFCF4AD45C.jpg)

JSP运算符

JSP支持所有Java逻辑和算术运算符。

下表罗列出了JSP常见运算符，优先级从高到底：

| **类别** | **操作符**                            | **结合性** |
| ------ | ---------------------------------- | ------- |
| 后缀     | () [] . (点运算符)                     | 左到右     |
| 一元     | ++ - - ! ~                         | 右到左     |
| 可乘性    | * / %                              | 左到右     |
| 可加性    | + -                                | 左到右     |
| 移位     | >> >>> <<                          | 左到右     |
| 关系     | > >= < <=                          | 左到右     |
| 相等/不等  | == !=                              | 左到右     |
| 位与     | &                                  | 左到右     |
| 位异或    | ^                                  | 左到右     |
| 位或     | \|                                 | 左到右     |
| 逻辑与    | &&                                 | 左到右     |
| 逻辑或    | \|\|                               | 左到右     |
| 条件判断   | ?:                                 | 右到左     |
| 赋值     | = += -= *= /= %= >>= <<= &= ^= \|= | 右到左     |
| 逗号     | ,                                  | 左到右     |

------

## JSP 字面量

JSP语言定义了以下几个字面量：

- 布尔值(boolean)：true 和 false;
- 整型(int)：与 Java 中的一样;
- 浮点型(float)：与 Java 中的一样;
- 字符串(string)：以单引号或双引号开始和结束;
- Null：null。
