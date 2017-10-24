---
title: 一个简易的server
date: 2017-10-23 10:27:19
tags:
---

# Node.js 服务器
## 接收请求
我们的脚本只需要一个文件就可以搞定
  1.`cd ~/Desktop; mkdir node-demo; cd node-demo`//新建一个安全的目录
  2.`touch server.js`
  3.编辑 server.js
  4.运行`node server`或者`node server.js`，看到报错
  5.根据报错提示调整你的命令
  6.成功之后，这个 server 会保持运行，无法退出
    *如果你想「中断」这个 server，按`Ctrl + C`即可（C 就是 Cancel 的意思）
    *中断后你才能输入其他命令
    *建议把这个 server 放在那里别动，新开一个 Bash 窗口，完成下面的教程

好了服务器完成。只不过
  1.这个服务器目前只有一个功能，那就是打印出路径和查询字符串
  2.还缺少一个重要的功能，那就是发出 HTTP 响应

目前我们先只做一个功能玩玩。

接下来你要发起一个请求到这个服务器。这听起来有点怪异，「我向自己发起请求」，目前是的，因为你买不起服务器啊。

在新的 Bash 窗口运行`curl http://localhost:你的指定的端口/xxx`或者`curl http://127.0.0.1:你指定的端口/xxx`。

你会马上发现 server 打印出了路径
  1.这说明我们的 server 收到了我们用 curl 发出的请求
  2.由于 server 迟迟没有发出响应，所以 curl 就一直等在那里，无法退出（用 Ctrl + C 中断这个傻 curl）

---
## 发出响应
接下来我们让我们 server 发出响应
  1.编辑 server.js
  2.在中间我标注的区域添加两行代码
    `response.write('Hi')`
    `response.end()`
  3.中断之前的 server，重新运行`node server 8888`
  4.`curl http://127.0.0.1:8888/xxx`，结果如下：
    `hi%`
  这个 % 不是我们的内容，% 表示结尾。如果你看 % 不爽，就把 `Hi` 换成 `Hi\n`。
  5.好了，响应添加成功
  6.使用`curl -s -v -- "http://localhost:8888/xxx"` 可以查看完整的请求和响应

---
## 根据请求返回不同的响应
  1.用户请求 / 时，返回 html 内容
  2.该 html 内容里面由一个 css link 和一个 script
  3.css link 会请求 /style.css，返回 css 内容
  4.script 会请求 /main.js，返回 js 内容
  5.请求 / /style.css /main.js 以外的路径，则一律返回 404 状态码
[完整内容参考我的server](https://github.com/FuhuaChen/script-demo/blob/master/server.js)