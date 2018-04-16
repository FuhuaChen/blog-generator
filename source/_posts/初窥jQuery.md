---
title: 初窥jQuery
date: 2018-04-16 13:23:13
tags:
---
jQuery作为目前最受欢迎的javascript库，想必大家都不陌生，据统计，已经超过70%的网站直接或间接的使用了jQuery，所以学习jQuery是很有必要的。
我们知道jQuery其实是一个函数库，既然是函数，那我们能不能自己实现一个类似jQuery的功能呢？答案自然是肯定的。所以我们今天通过自己封装一个最简单的函数来了解一下jQuery的原理与思想。

# 给元素加上一个class
首先，在页面上有5个`div`标签，我们需要给这5个`div`都加上一个名字为`red`的class，那么我们会这样做：
```
var allDiv = document.querySelectorAll('div')
allDiv[0].classList.add('red')
allDiv[1].classList.add('red')
allDiv[2].classList.add('red')
allDiv[3].classList.add('red')
allDiv[4].classList.add('red')
```
这样我们就实现了我们的需求，但是我们发现这个代码有很大的问题，没有效率且都是重复的代码，所以我们很容易就想到了循环：
```
var allDiv = document.querySelectorAll('div')
for(var i=0;i<allDiv.length;i++){
    allDiv[i].calssList.add('red')
}
```
现在代码就简洁了许多，然后我们就想，既然能给`div`添加class，我们能不能给其他元素添加class呢？
```
function addClass(node){
    var allNodes = document.querySelectorAll(node)
    for(var i=0;i<allNode.length;i++){
        allNodes[i].calssList.add('red')
    }
}
```
当然，我们又发现新问题了，其他的元素我们想加的是其他的class，并不是所有的都添加`red`：
```
function addClass(node，classes){
    var allNodes = document.querySelectorAll(node)
    for(var i=0;i<allNode.length;i++){
        allNodes[i].calssList.add(classes)
    }
}
```
只要把class当做参数传进去就行啦。

# 设置元素的textContent
还是那5个`div`现在我们希望把`div`的textContent全部变为hello：
```
function setText(node){
    var allNodes = document.querySelectorAll(node)
    for(var i=0;i<allNodes;i++){
        allNodes[i].textContent = 'hello'
    }
}
```
还是那个问题，我们希望每次设置不同的内容：
```
function setText(node,text){
    var allNodes = document.querySelectorAll(node)
    for(var i=0;i<allNodes;i++){
        allNodes[i].textContent = text
    }
}
```
现在我们就可以使用这两个函数批量添加class和设置textContent了,但是很显然这跟jQuery一点关系都没有，我们知道jQuery是我们给它一个元素，它会封装这个元素并返回一些私有的属性，并不是直接使用这些函数，所以我们需要进一步封装：
```
window.jQuery = function(node){
    return{
        addClass:function(classes){
            var allNodes = document.querySelectorAll(node)
            for(var i=0;i<allNodes.length;i++){
                allNodes[i].classList.add(classes)
            }
        },
        setText:function setText(text){
            var allNodes = document.querySelectorAll(node)
            for(var i=0;i<allNodes.length;i++){
                allNodes[i].textContent = text
            }
        }
    }
}
```
现在我们把两个函数作为对象的属性返回出去，我们发现现在已经非常接近jQuery了：
```
window.$ = jQuery
```
现在我们就可以使用这个功能简单的jQuery了
```
var $div = $('div')
$div.addClass('red')
$div.setText('hello')
```
这样我们就实现了和原来一样的效果，当然jQuery的功能更加强大和复杂，但是都是同样通过操作DOM实现的，只不过jQuery帮我们做了这些复杂的工作，让遍历和操作、事件处理、动画和Ajax各种复杂操作变得简单高效。