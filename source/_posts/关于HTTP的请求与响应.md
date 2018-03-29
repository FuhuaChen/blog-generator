---
title: 关于HTTP的请求与响应
date: 2018-03-23 18:26:02
tags:
---
# 超文本传输协议
HTTP(HyperText Transfer Protocol)超文本传输协议是一种用于分布式，协作式和超媒体信息系统的应用层协议，是万维网的数据通信的基础。

HTTP是一个客户端终端（用户）和服务器端（网站）请求和应答的标准。通过使用网页浏览器，命令行或其他工具，客户端发起一个HTTP请求创建到服务器指定端口
（默认为80端口）的TCP连接。HTTP服务器在那个端口监听客户端的请求。一旦收到请求，服务器会向客户端返回一个状态和内容。

# 请求
请求一般包括4部分，但第4部分可以为空：
1. 第一部分为请求行，格式为：
动词 路径 协议/版本
```
GET / HTTP/1.1
```
2. 第二部分为请求头，格式为：
key1:value1
key2:value2
...
```
Host: www.baidu.com
content-Type: application/x-www-from-urlenconded
```
3. 第三部分为空行，固定为一个回车
4. 第四部分为消息体，表示要上传的数据

所以一个请求就由上面四部分组成，而HTTP/1.1协议中一共定义了八种请求方法，GET和POST是最常用的请求方法。

## GET请求
```
GET / HTTP/1.1
Host: www.baidu.com
User-Agent: curl/7.55.0

```

## POST请求
```
POST / HTTP/1.1
Host: www.baidu.com
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 10

name=12345
```

除了GET和POST方法外还有：HEAD、PUT、DELETE、OPTIONS、CONNECT、PATCH等方法。

# 响应
响应也分为4部分，第4部分可以很长：
1. 第一部分为状态行，格式为：
```
协议/版本号 状态吗 状态解释
```
```
HTTP/1.1 200 OK
```
2. 第二部分为响应头，格式和请求第二部分一样：
```
key1: value1
key2: value2
...
```
```
content-type: text/html //这里的content-type标注了第四部分的格式
content=length: 2345 
```
3. 第三部分和请求一样为空行，必须要有
4. 第四部分为响应正文，格式为第二部分的content-type所指定的格式
```
<html>
<head>
<meta http-equive="content-type" content="text/html;charset=utf-8">
...
</head>
</html>
```

# HTTP状态码
所有状态码的第一个数字代表响应的状态，一共有五种状态：
1xx:消息——表示请求被接受，需要继续处理。
2xx:成功——代表请求已成功被服务器接受、理解、并接受。
3xx:重定向--代表需要客户端采取进一步的操作才能完成请求。
4xx:客户端错误--代表客户端错误，无法实现请求。
5xx:服务器错误--表示服务器无法完成有效的请求。

## 常见状态码
```
200 OK //请求已成功
204 Created //创建成功
301 Moved Permanently //被请求的资源已永久移动到新位置
302 Found //表示临时等不到响应
403 Forbidden //服务器已经理解请求，但是拒绝执行它
404 Not Found //请求失败，找不到资源
500 Intnal Server Error //通用错误消息，服务器发生不可预期的错误
503 Service Unavailable //服务器目前无法处理请求，一段时间后可能会恢复
```

# 在chrome上查看请求与响应
1. 打开Network
2. 地址栏输入网址
3. 选中对应的请求/响应
4. 在Headers里面点击Request Headers，然后点击view source,就能看到对应的请求的前三部分。
5. 如果请求有第四部分，在FormData或Payload里面可以看到。
6. 在Headers里面点击Response Headers,然后点击view source,就能看到对应的响应的前两部分。
7. 查看Response或Preview，就可以看到响应的第四部分。