---
layout: post
title: javascript 获取屏幕/页面的宽度和高度的方法
categories: [js]
author: chenghaojie
excerpt: "js 获取宽高"
---


* content
{:toc}


>网页可见区域宽： document.body.clientWidth

>网页可见区域高： document.body.clientHeight

>网页可见区域宽： document.body.offsetWidth (包括边线的宽)

>网页可见区域高： document.body.offsetHeight (包括边线的高)

>网页正文全文宽： document.body.scrollWidth

>网页正文全文高： document.body.scrollHeight

>网页被卷去的高： document.body.scrollTop

>网页被卷去的左： document.body.scrollLeft

>网页正文部分上： window.screenTop

>网页正文部分左： window.screenLeft

>屏幕分辨率的高： window.screen.height

>屏幕分辨率的宽： window.screen.width

>屏幕可用工作区高度： window.screen.availHeight

>屏幕可用工作区宽度： window.screen.availWidth

举个例子：

    var cliWidth=document.documentElement.clientWidth||document.body.clientWidth;
    
这样兼容IE，另外如果你想获得一个div的大小，可以用div.offsetWidth,div.offsetHeight取得宽高。