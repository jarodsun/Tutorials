# 第 5 章 JSP 简单项目

[返回](./README.md)

## tomcat 中运行 jsp

### 第一步：tomcat 下`webapps`目录下创建`test`文件夹

```
mkdir test
```

### 第二步： 创建`index.jsp`文件

```
vim index.jsp
```

### 第三步： 在`index.jsp`文件中，添加代码

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Hello World</title>
</head>
<body>
    <h1>Hello World!</h1>
    <p>This is my first JSP page.</p>
</body>
</html>
```

### 第四步： 在浏览器中，查看结果

`localhost:8080/test/index.jsp`

## 使用 idea 创建 jsp 项目

### 第一步：新建项目

1. 起名字
2. 选语言：Java
3. 选构建系统：Maven

### 第二步： 编辑`pom.xml`

#### 添加打包工具

```
<dependencies>
        <dependency>
            <groupId>jakarta.servlet</groupId>
            <artifactId>jakarta.servlet-api</artifactId>
            <version>5.0.0</version>
            <scope>provided</scope>
        </dependency>
</dependencies>
```

#### 添加`tomcat`部署工具

```
<build>
    <finalName>${project.artifactId}</finalName>
    <plugins>
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
                <url>http://localhost:8090/manager/text</url>
                <server>TomcatServer</server>
                <username>这里配置tomcat中的用户名</username>
                <password>这里是密码</password>
                <path>/这里是部署路径</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```

#### 添加完代码；

从：视图->工具窗口->Maven，打开Maven控制面板

在Maven控制面板中，找到“重新加载所有Maven项目”，点击执行。

#### （选用）如果出现打包结果是：jar文件，需要添加：

```
在`<version>1.0-SNAPSHOT</version>`下面添加

<packaging>war</packaging>
```

### 第三步： 编辑`tomcat-users.xml`文件

添加`manager-script`用户及密码

```
<role rolename="manager-script"/>

<user username="tomcat" password="654321" roles="manager-script"/>
```

### 第四步： 添加`index.jsp`文件，并编辑

文件位置：`srcsrc/main/webapp/index.jsp`

编辑内容：

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Hello World</title>
</head>
<body>
    <h1>Hello World!</h1>
    <p>This is my first JSP page.</p>
</body>
</html>
```

### 第五步： 运行Maven相关命令

打开Maven控制面板。

执行1： 生命周期：clean

执行2： 生命周期：package

执行3： 插件->tomcat7:deploy

等待构建、部署完成。

### 第六步： 查看

浏览器打开：`localhost:8080/myblog`

### 后续： 重新部署

执行1： 插件->tomcat7:undeploy

执行2： 插件->tomcat7:deploy

## 编写程序

### 第一步：建立git仓库

```
初始化仓库
git init
查看仓库状态
git status
设置：
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
git config --global core.editor vim // 设置默认编辑器为vim
添加忽略文件
git add .gitignore
添加提交说明
git commit
查看提交日志
git log
```

### 项目文件结构

```
MyBlogProject/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   ├── com/
│   │   │   │   └── myblog/
│   │   │   │       ├── dao/            # 数据访问对象（Data Access Objects）
│   │   │   │       │   ├── PostDAO.java
│   │   │   │       │   └── UserDAO.java
│   │   │   │       ├── model/          # 模型类
│   │   │   │       │   ├── Post.java
│   │   │   │       │   └── User.java
│   │   │   │       ├── servlet/        # Servlets
│   │   │   │       │   ├── HomeServlet.java
│   │   │   │       │   ├── LoginServlet.java
│   │   │   │       │   ├── LogoutServlet.java
│   │   │   │       │   ├── NewPostServlet.java
│   │   │   │       │   ├── DeletePostServlet.java
│   │   │   │       │   └── EditPostServlet.java
│   │   │   │       └── util/           # 工具类，如数据库连接
│   │   │   │           └── DBConnection.java
│   │   │   └── resources/              # 资源文件，如配置文件
│   │   │       └── database.properties
│   │   └── webapp/                     # Web应用资源
│   │       ├── WEB-INF/
│   │       │   ├── web.xml             # Web应用部署描述符
│   │       │   └── lib/                # 存放Web应用所需的JAR文件
│   │       ├── index.jsp               # 首页
│   │       ├── login.jsp               # 登录页面
│   │       ├── newPost.jsp             # 新建博客帖子页面
│   │       ├── editPost.jsp            # 编辑博客帖子页面
│   │       └── viewPost.jsp            # 查看博客帖子详情页面
└── pom.xml                             # Maven项目对象模型文件
```

### 第二步： 更改`index.jsp`内容

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page import="java.util.*, com.myblog.model.Post" %>

<!DOCTYPE html>
<html>
<head>
    <title>简单博客首页</title>
    <style>
        body { font-family: Arial, sans-serif; }
        .post { margin-bottom: 20px; }
        .post-title { font-weight: bold; }
        .post-timestamp { font-size: 0.8em; }
        .post-content { margin-top: 5px; }
    </style>
</head>
<body>

<h1>欢迎来到我的博客</h1>

<%
    // 模拟的文章数据，实际开发中应从数据库获取
    List<Post> posts = new ArrayList<>();
    posts.add(new Post(1, "第一篇文章", "这是我的第一篇文章内容...", new Date()));
    posts.add(new Post(2, "第二篇文章", "这是我的第二篇文章内容...", new Date()));

    for(Post post : posts) {
%>
        <div class="post">
            <div class="post-title"><%= post.getTitle() %></div>
            <div class="post-timestamp"><%= post.getTimestamp() %></div>
            <div class="post-content"><%= post.getContent() %></div>
        </div>
<%
    }
%>

</body>
</html>
```

### 第三步： 创建`Post`模型

```
package com.myblog.model;

import java.util.Date;

public class Post {
    private int id;
    private String title;
    private String content;
    private Date timestamp;

    // 构造函数
    public Post(int id, String title, String content, Date timestamp) {
        this.id = id;
        this.title = title;
        this.content = content;
        this.timestamp = timestamp;
    }

    // ID的getter和setter
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    // 标题的getter和setter
    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    // 内容的getter和setter
    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }

    // 时间戳的getter和setter
    public Date getTimestamp() {
        return timestamp;
    }

    public void setTimestamp(Date timestamp) {
        this.timestamp = timestamp;
    }
}

```

### 部署，查看页面

看一下index.jsp页面是否正常显示了

### 第四步： 创建`login.jsp`页面

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<!DOCTYPE html>
<html>
<head>
    <title>登录</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .container {
            width: 300px;
            margin: 0 auto;
            margin-top: 50px;
        }
        form {
            display: flex;
            flex-direction: column;
        }
        input[type="text"], input[type="password"] {
            margin-bottom: 10px;
            height: 30px;
            padding: 0 10px;
        }
        input[type="submit"] {
            cursor: pointer;
            height: 34px;
            background-color: #4CAF50;
            color: white;
            border: none;
        }
        input[type="submit"]:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>登录</h2>
    <!-- 确保action指向LoginServlet的映射地址 -->
    <form action="login" method="post">
        <input type="text" name="username" placeholder="用户名" required>
        <input type="password" name="password" placeholder="密码" required>
        <input type="submit" value="登录">
    </form>
</div>

</body>
</html>
```

### 第五步： 创建`LoginServlet`

```
package com.myblog.servlet;

import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import jakarta.servlet.http.HttpSession;
import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

@WebServlet(name = "LoginServlet", urlPatterns = {"/login"})
public class LoginServlet extends HttpServlet {

    @Override
    public void init() throws ServletException {
        super.init();
        // 这里可以初始化数据库连接信息，例如加载JDBC驱动
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            throw new ServletException(e);
        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String username = request.getParameter("username");
        String password = request.getParameter("password"); // 实际应用中应使用哈希密码

        // 数据库连接字符串，根据实际情况修改
        String dbURL = "jdbc:mysql://172.17.0.2:3306/myblogdb";
        String dbUser = "root";
        String dbPassword = "123456";

        try (Connection connection = DriverManager.getConnection(dbURL, dbUser, dbPassword);
             PreparedStatement statement = connection.prepareStatement("SELECT * FROM users WHERE username = ? AND password = ?")) {

            statement.setString(1, username);
            statement.setString(2, password);

            ResultSet resultSet = statement.executeQuery();

            if (resultSet.next()) {
                // 登录成功
                HttpSession session = request.getSession();
                session.setAttribute("username", username);
                response.sendRedirect("newPost.jsp"); // 修改为你的主页
            } else {
                // 登录失败
                request.setAttribute("errorMessage", "无效的用户名或密码");
                request.getRequestDispatcher("/login.jsp").forward(request, response);
            }
        } catch (SQLException e) {
            e.printStackTrace();
            throw new ServletException("数据库连接失败");
        }
    }
}
```

### 第六步： 在`pom.xml`中，添加新的插件

```
<dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.33</version>
</dependency>
```

然后，Maven面板中，重新加载所有项目。

### 第七步： 添加`web.xml`文件

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!-- Servlet配置 -->

    <servlet>
        <servlet-name>LoginServlet</servlet-name>
        <servlet-class>com.myblog.servlet.LoginServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>LoginServlet</servlet-name>
        <url-pattern>/login</url-pattern>
    </servlet-mapping>

    <!-- 更多Servlet和Servlet映射 -->

    <!-- 欢迎文件列表 -->
    <welcome-file-list>
        <welcome-file>/</welcome-file>
    </welcome-file-list>

    <!-- 会话配置 -->
    <session-config>
        <session-timeout>30</session-timeout> <!-- 以分钟为单位 -->
    </session-config>
</web-app>
```

### 第八步： 创建 数据库

使用phpmyadmin创建数据库

```
// 创建数据库：
CREATE DATABASE myblogdb;

// 创建user表
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

// 创建post表
CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    author_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (author_id) REFERENCES users(id)
);

// 切换到user表，添加一条记录
INSERT INTO users (username, password) VALUES ('admin', 'password');
```

### 部署，测试

测试成功后，别忘了用git提交一下代码。

### 第九步： 创建`newPost.jsp`页面

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<!DOCTYPE html>
<html>
<head>
    <title>发布新帖子</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .container {
            width: 400px;
            margin: 0 auto;
            margin-top: 50px;
        }
        form {
            display: flex;
            flex-direction: column;
        }
        input[type="text"], textarea {
            margin-bottom: 10px;
            padding: 8px;
        }
        input[type="submit"] {
            cursor: pointer;
            padding: 10px;
            background-color: #4CAF50;
            color: white;
            border: none;
        }
        input[type="submit"]:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>发布新帖子</h2>
    <form action="newPost" method="post">
        <input type="text" name="title" placeholder="标题" required>
        <textarea name="content" placeholder="内容" rows="10" required></textarea>
        <input type="submit" value="发布">
    </form>
</div>

</body>
</html>
```

### 第十步： 创建`NewPostServlet`

```
package com.myblog.servlet;

import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

@WebServlet(name = "NewPostServlet", urlPatterns = {"/newPost"})
public class NewPostServlet extends HttpServlet {

    @Override
    public void init() throws ServletException {
        super.init();
        // 这里可以初始化数据库连接信息，例如加载JDBC驱动
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            throw new ServletException(e);
        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String title = request.getParameter("title");
        String content = request.getParameter("content");

        // 数据库连接字符串，根据实际情况修改
        String dbURL = "jdbc:mysql://172.17.0.2:3306/myblogdb";
        String dbUser = "root";
        String dbPassword = "123456";

        String sql = "INSERT INTO posts (title, content) VALUES (?, ?)";

        try (Connection connection = DriverManager.getConnection(dbURL, dbUser, dbPassword);
             PreparedStatement statement = connection.prepareStatement(sql)) {

            statement.setString(1, title);
            statement.setString(2, content);

            int result = statement.executeUpdate();

            if (result > 0) {
                // 发布成功，重定向到博客首页或帖子列表页面
                response.sendRedirect("./"); // 根据你的页面结构调整重定向目标
            } else {
                // 发布失败，可以设置一个错误消息并重定向回发布页面
                response.sendRedirect("newPost.jsp"); // 使用实际的错误处理逻辑
            }
        } catch (SQLException e) {
            e.printStackTrace();
            throw new ServletException("保存帖子到数据库时发生错误");
        }
    }
}
```

### 第十一步： 更新`web.xml`

增加了，对`NewPostServlet`和`FetchPostsServlet`的映射

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!-- Servlet配置 -->
    <servlet>
        <servlet-name>FetchPostsServlet</servlet-name>
        <servlet-class>com.myblog.servlet.FetchPostsServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>FetchPostsServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>LoginServlet</servlet-name>
        <servlet-class>com.myblog.servlet.LoginServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>LoginServlet</servlet-name>
        <url-pattern>/login</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>NewPostServlet</servlet-name>
        <servlet-class>com.myblog.servlet.NewPostServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>NewPostServlet</servlet-name>
        <url-pattern>/newPost</url-pattern>
    </servlet-mapping>

    <!-- 更多Servlet和Servlet映射 -->

    <!-- 欢迎文件列表 -->
    <welcome-file-list>
        <welcome-file>/</welcome-file>
    </welcome-file-list>

    <!-- 会话配置 -->
    <session-config>
        <session-timeout>30</session-timeout> <!-- 以分钟为单位 -->
    </session-config>

</web-app>
```

### 倒数第二步： 创建`FetchPostsServlet`

```
package com.myblog.servlet;

import com.myblog.model.Post;
import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;

@WebServlet(name = "FetchPostsServlet", urlPatterns = {"/"})
public class FetchPostsServlet extends HttpServlet {

    @Override
    public void init() throws ServletException {
        super.init();
        // 这里可以初始化数据库连接信息，例如加载JDBC驱动
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            throw new ServletException(e);
        }
    }

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 数据库连接字符串，根据实际情况修改
        String dbURL = "jdbc:mysql://172.17.0.2:3306/myblogdb";
        String dbUser = "root";
        String dbPassword = "123456";
        String sql = "SELECT * FROM posts ORDER BY created_at DESC";

        List<Post> posts = new ArrayList<>();

        try (Connection connection = DriverManager.getConnection(dbURL, dbUser, dbPassword);
             PreparedStatement statement = connection.prepareStatement(sql);
             ResultSet resultSet = statement.executeQuery()) {

            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String title = resultSet.getString("title");
                String content = resultSet.getString("content");
                Timestamp timestamp = resultSet.getTimestamp("created_at");

                Post post = new Post(id, title, content, new java.util.Date(timestamp.getTime()));
                posts.add(post);
            }

            request.setAttribute("posts", posts);
            request.getRequestDispatcher("/index.jsp").forward(request, response);

        } catch (SQLException e) {
            e.printStackTrace();
            throw new ServletException("获取帖子列表时发生数据库错误");
        }
    }
}
```

### 最后一步： 更新`index.jsp`

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page import="java.util.List, com.myblog.model.Post" %>
<%@ page import="com.myblog.servlet.FetchPostsServlet" %>
<!DOCTYPE html>
<html>
<head>
    <title>简单博客首页</title>
    <style>
        /* 你的CSS样式 */
    </style>
</head>
<body>

<h1>欢迎来到我的博客</h1>

<%

    List<Post> posts = (List<Post>) request.getAttribute("posts");
    if (posts == null || posts.isEmpty()) {
%>
        <p>没有找到帖子。</p>

<%
    } else {
        for (Post post : posts) {
%>
            <div class="post">
                <div class="post-title"><h3>标题：<%= post.getTitle() %></h3></div>
                <div class="post-timestamp">发布时间：<%= new java.text.SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss").format(post.getTimestamp()) %></div>
                <div class="post-content">内容：<%= post.getContent() %></div>
                <br />
            </div>
<%
        }
    }
%>


</body>
</html>
```

### 不断地部署、测试，直到成功。