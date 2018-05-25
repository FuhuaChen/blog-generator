---
title: cookie、session、localstorage
date: 2018-05-25 14:52:05
tags:
---
# cookie
cookie是当客户端发起请求时，服务器通过set-cookie响应头设置cookie作为响应的一部分。
客户端得到cookie之后，每次请求相同域名时都会带上服务器设置的cookie，
服务器读取cookie就知道登录用户的信息。
cookie大小一般在4KB左右，
cookie被存在硬盘的文件里，
cookie的有效期可以设置，没设置有效期一般在浏览器关闭后删除，
cookie并不安全，可以被修改。

# session
session一般来说是基于cookie实现的，将sessionID(随机数)通过cookie发给客户端，
客户端访问服务器时，服务器读取sessionID，
通过sessionID我们可以得到对应用户的隐私信息，
session保存在服务器上，服务器有一块内存(哈希表)保存了所有的session。

# localstorage 
localstorage跟HTTP无关，发起请求时不会带上localstorage的值，
只有相同域名的页面才能互相读取localstorage，
每个域名localstorage最大存储量为5MB左右(每个浏览器不一样)，
localstorage永久有效，除非用户清理缓存，
一般用来记录一些没有用的信息，不能记录隐私信息，
常用场景：记录有没有提示过用户。

# sessionstorage
sessionstorage基本和localstorage一样，但是在用户关闭后就会失效

# cache-control
服务器可以设置cache-control的时间，在这段时间内如果请求的相同的url，就不发出请求，直接从缓存读取，
缓存一般都会缓存很久，可以通过更新版本(设置不一样的查询参数)避开缓存。
ETag可以通过对比md5来决定要不要读取响应体，但是还是会发起请求。
