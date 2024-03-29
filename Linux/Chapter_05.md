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