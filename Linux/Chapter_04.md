# 第 4 章 Java 开发环境环境搭建

[返回](./README.md)

## JDK

### 下载配置

微软: https://learn.microsoft.com/zh-cn/java/openjdk/download

Adoptium: https://adoptium.net/zh-CN/

第一步：下载

从上面的两个网站中，选择其中一个，找到jdk，21版本的压缩包，进行下载，下载之后，解压。

第二步：配置环境变量：

文件位置：`~/.profile`

```
export JAVA_HOME=/home/ubuntu/downloads/jdk-21.0.2+13
export PATH=$JAVA_HOME/bin:$PATH
```

第三步：编译`~/.profile`

```
source .profile
```

第四步：重启系统

第五步：验证配置结果

```
java -version
```

### apt 安装

安装：

```
sudo apt update

sudo apt install openjdk-21-jdk
```

检查：

```
java -version
```

## Tomcat

### 下载配置

官网： https://tomcat.apache.org/download-10.cgi

第一步：下载，解压

从上面的链接，下载tomcat10，然后解压。

第二步： 运行

```
在tomcat目录下运行

./startup.sh
```

第三步： 检验

用浏览器打开： `localhost:8080`

如何停止？

```
在tomcat目录下运行

./shutdown.sh
```

### apt 安装

第一步：安装：

```
sudo apt update

sudo apt install tomcat9
```

第二步：启动与停用

```
查看状态：
sudo service tomcat9 status

启动：
sudo service tomcat9 start

停用：
sudo service tomcat9 stop
```

第三步： 检查

用浏览器打开： `localhost:8080`

## Docker

官网： https://www.docker.com/

命令大全： https://www.runoob.com/docker/docker-command-manual.html

步骤 1：更新软件包列表

```
sudo apt update
```

步骤 2：安装依赖包

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

步骤 3：添加 Docker 的官方 GPG 密钥

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

步骤 4：设置稳定版仓库

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

步骤 5：安装 Docker Engine

```
sudo apt update
```

然后，安装最新版本的 Docker Engine 和 containerd：

```
sudo apt install docker-ce docker-ce-cli containerd.io
```

步骤 6：验证 Docker 安装

```
sudo systemctl status docker
```

或者，运行一个 Hello World 容器来验证 Docker Daemon 是否正确安装并工作：

```
sudo docker run hello-world
```

步骤 7：非 root 用户运行 Docker（可选）

```
sudo usermod -aG docker $USER
```

## MySql

### docker 安装

第一步:拉取镜像

```
sudo docker pull mysql
```

第二步： 运行容器

```
sudo docker run -d --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=yourpassword mysql
```

### apt 安装

## phpmyadmin

### docker 安装

第一步:拉取镜像

```
sudo docker pull phpmyadmin
```

第二步: 运行容器,连接mysql

```
sudo docker run --name myadmin -d --link your-database-container:db -p 9090:80 phpmyadmin
```

第三步： 检验

用浏览器打开: `localhost:9090`

## IDE

### 下载，运行

官网： https://www.jetbrains.com/zh-cn/idea/download

下载： IntelliJ IDEA Community

解压到指定目录后

```
./bin/idea.sh
```

### 商店安装(snap 加速)

第一种方式

```
$ sudo apt-get install snapd
$ sudo snap install snap-store
$ sudo snap install snap-store-proxy
$ sudo snap install snap-store-proxy-client
```

第二种方式

```
killall snap-store
sudo snap refresh snap-store
```
