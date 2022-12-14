# MyWebServer
基于Cpp11实现的高性能Web服务器。
## 特性
- 利用Epoll与线程池实现Reactor高并发模型
- 利用状态机与正则实现HTTP请求报文解析，可同时处理GET与POST请求
- 用vector容器封装char，实现了一个可自动扩容的缓冲区
- 基于epoll_wait实现定时功能，关闭超时的非活动连接，并用小根堆作为容器管理定时器
- 利用单例模式实现了一个简单的线程池，减少了线程创建与销毁的开销
- 利用单例模式实现连接MySQL的数据库连接池，减少数据库连接建立与关闭的开销，实现了用户注册登录功能
- 利用单例模式与阻塞队列实现异步日志系统，记录服务器运行状态
- 能够处理前端发送的multi/form-data类型的post请求，实现了文件上传功能
## 环境要求
- Linux
- C++11
- MySQL 5.7.31
## 目录树
```
.
├── bin
│   └── Simpleserver 可执行文件
├── build
│   └── Makefile
├── code             源代码
│   ├── buffer       自动扩容的缓冲区
│   ├── config       配置文件
│   ├── http         HTTP请求解析、响应
│   ├── lock         锁函数封装
│   ├── log          基于阻塞队列的异步日志模块
│   ├── main.cpp     主函数
│   ├── server       基于epoll的服务器
│   ├── sqlconnpool  数据库连接池
│   ├── threadpool   线程池
│   └── timer        小根堆管理的定时器
├── log              日志目录
├── files            文件上传目录
├── CMakeLists
├── build.sh
├── README.md
└── resources        静态资源
```
## 项目启动
将项目克隆到本地
```
git clone https://github.com/Pekingplx/MyWebServer.git
```

## 服务器测试环境
-Ubuntu版本   16.04
-MySQL版本    5.7.29

## 浏览器测试环境
-Windows、Linux均可
-Chrome
-FireFox

配置数据库

```
//创建数据库
create database mydb;
//创建user表
USE webdb;
CREATE TABLE user(
    username char(50) NULL,
    passwd char(50) NULL
)ENGINE=InnoDB;
//添加数据
INSERT INTO user(username, passwd) VALUES('username', 'password');

//mydb是数据库名，user是表名，需要在main函数中传入
```
然后运行脚本编译
```
sh build.sh
```
浏览器访问
```
192.168.0.1:9000
#9000是在main函数中传入的服务器监听端口
```

## 致谢
Linux高性能服务器编程，游双著

[markparticle/WebServer](https://github.com/markparticle/WebServer)

[Sakura1221/SimpleWebServer](https://github.com/Sakura1221/SimpleWebServer) 