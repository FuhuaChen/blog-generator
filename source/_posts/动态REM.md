---
title: 动态REM
date: 2017-12-28 22:29:53
tags:
---

# 动态REM

1. 什么是REM：这个单位代表根元素的`font-size`(默认为16px)的大小

2. REM和EM的区别：REM指根元素的`font-size`，EM指自身元素的`font-size`

3. 手机端方案的特点：所有的手机显示的界面都是一样的，只是大小不同。由于REM代表html的`font-size`，我们可以间接用REM表示viewport width（设备宽度），
然后用JS动态调整REM

4. 用JS动态调整REM：我们可以用`document.write()`写入样式，同样需要写一个meta来阻止页面的缩放：
```
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
<script>
    var pageWidth = window.innerWidth
    document.write('<style>html{font-size' + pageWidth/10 + 'px;}</style>')
</script>
```
此时`1REM==html{font-size}==pageWidth/10`也就是设备宽度的十分之一

5. REM可以和其他单位同时使用：
```
font-size:16px;
border:1px soild red;
width:5rem; 
```

6. 在SCSS里使用PX2REM：
首先安装SASS
* npm config set registry https://registry.npm.taobao.org/
* touch ~/.bashrc
* echo 'export SASS_BINARY_SIZE="https://npm.taobao.org/mirrors/node-sass"'>>~/.bashrc
* source ~/.bashrc
* npm i -g node-sass

* makdir ~/Docktop/scss-demo
* cd ~/Docktop/scss-demo
* mkdir scss css
* touch scss/style.scss
* start scss/style.scss

* node-sass -wr scss -o css

编辑scss文件自动得到css文件：
在scss文件里添加：
```
@function px($px){
    @return $px/designWidth*10 + rem;
}

$designWidth: 640; //这里的640指设计稿的宽度，需要根据设计稿的宽度填写

.child{
    width: px(320); //这里的px()指上面的function
    height: px(160);
    margin: px(40) px(40);
    border: 1px soild red;
    float: left;
    font-size: 1em
}
```
即可实现px自动变为rem
