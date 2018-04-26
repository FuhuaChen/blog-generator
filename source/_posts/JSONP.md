---
title: JSONP
date: 2018-04-26 13:30:10
tags:
---
# 什么是JSONP
由于受同源策略的限制，有时候浏览网站会带来很大的不方便，而JSONP就是服务器和客户端跨源通信的常用方法。
它的基本思想是，网页通过创建并添加一个`script`标签，src指向服务器，同时传查询参数`?callback=xxx`,
服务器根据查询参数，将数据放在指定的回调函数传回来(`xxx.call(undefined,'你要的数据')`)这样的响应，浏览器接收到响应就会执行`xxx.call(undefined,'你要的数据')`，从而获得想要的数据，这就是JSONP:
```
button.addEventlistener('click',(e)=>{
    let script = document.createElement('script')
    let functionName = 'jQuery' + parseInt(Math.random()*100000,10)
    window[functionName] = function(){
        amount.innerText = amount.innerText - 0 - 1
    }
    script.src = '/pay?callback=' + functionName
    document.body.appendChild(script)
    script.onload = function(e){
        e.currentTarget.remove()
        delete window[functionName]
    } 
})
```
用jQuery实现JSONP:
```
 $.ajax({
 url: "http://jack.com:8002/pay",
 dataType: "jsonp",
 success: function( response ) {
     if(response === 'success'){
     amount.innerText = amount.innerText - 1
     }
 }
 })
```
