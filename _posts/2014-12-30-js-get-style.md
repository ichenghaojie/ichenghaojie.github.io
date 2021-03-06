---
layout: post
title: 一个有用的css的函数，以及获取样式的方法
categories: [js]
author: chenghaojie
excerpt: "js 获取css"
---


* content
{:toc}


这是个很有用的css函数

    function css(obj, attr, value)
    {
        switch (arguments.length)
        {
        case 2:
            if(typeof arguments[1] == "object")
            { //二个参数, 如果第二个参数是对象, 批量设置属性
               for (var i in attr)obj.style[i] = attr[i]
            }
            else
            { //二个参数, 如果第二个参数是字符串, 读取属性值
               return obj.currentStyle ? obj.currentStyle[attr] : getComputedStyle(obj, null)[attr]
            }
            break;
        case 3:
            //三个参数, 单一设置属性
            obj.style[attr] = value;
            break;
        default:
            alert("参数错误！");
        }
    }
    
读取 css 属性值，这里注意，css 属性值，有包括真实计算值和行内样式值两部分。<br/>
这里关键点在于定义了一个 css 函数，这个 css 函数很有用的啊。<br/>
它可以灵活接收多种参数形式并且可以接收两个参数。<br/>
第一个参数一定是一个对象的引用，如果只有两个参数，那么判断第二个参数，如果第二个参数为 字符串，那么返回 该元素的该属性值。<br/>
如果第二个参数是一个 键值对 表 object ，那么批量设置键值对表里面的属性和值。 <br/>
如果包涵三个参数，直接设置css 样式。<br/>
注意，这里所有的属性的获取或者设置，都是用的 style[attr] 这种方法，这里面的 attr 要用“驼峰样式”来书写，不能用别的写法，毕竟这是 javascript 属性。<br/>
注意，这里用到了 typeof 这个运算符，来计算 待测目标的性质。<br/>
还有，这里的 currentStyle 和 getComputedStyle()，主要是为了兼容不同浏览器，后面的是火狐下用的。<br/>
多记录下，用js的style属性可以获得html标签的样式，但是不能获取非行间样式,而关于行间样式在IE下可以用currentStyle，而在火狐下面我们需要用到getComputedStyle。<br/>
举个例子：

    function getStyle(obj, attr)
    {
        if(obj.currentStyle)
        {
           return obj.currentStyle[attr];
        }
        else
        {
           return getComputedStyle(obj,false)[attr];
        }
    }
    window.onload=function()
    {
        var oDiv=document.getElementById('div1');
        alert(getStyle(oDiv,'width'));
    }
    
而关于行间样式：

上面的 style='color:red; 叫做 “行间样式”。

非行间样式指的是你的html元素的样式不是直接写在元素里的，而是通过样式表等方式给html元素添加样式的，就叫做 ‘非行间样式’