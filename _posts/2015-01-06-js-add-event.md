---
layout: post
title: 事件的绑定与解绑
categories: [js]
author: chenghaojie
excerpt: "js 事件绑定"
---


* content
{:toc}


事件处理函数的绑定和解绑，这里凡是要处理事件解绑和绑定的，都要单独创建 一个 EventUtil 对象，通过他的 addHandler removeHandler 来绑定和解绑函数。<br/>

>addHandler 方法，他分别视情况使用DOM0级方法、DOM2级方法或IE方法来添加事件。<br/>
这个方法属于一个名字叫EventUtil的对象，可以使用这个对象来处理浏览器间的差异。<br/>
addHandler() 方法接受3个参数：要操作的元素、时间名称和事件处理程序函数。<br/>

>与addHandler()方法对应的方法是removeHandler()，它也接受相同参数。<br/>
这个方法是移除之前添加的事件处理程序-------无论该事件处理程序是采取什么方式添加到元素中的。<br/>
如果其他方法无效，默认采用DOM0级方法。<br/>
方法中首先检查DOM2级，方法，如果存在DOM2级方法存在，则使用该方法：传入事件类型、事件处理程序、和第三个参数false（表示冒泡阶段）。如果存在的是IE的方法，则采取第二种方案。<br/>
这里的关键点在于这里面要做一些 hack. IE 浏览器要解绑函数的时候， 需要 在事件名前面加 'on' ，为了在IE8及更早版本中运行。<br/>

    var EventUtil = {
        /**//*
        此方法用来给特定对象添加事件，oElement是指定对象,sEvent是事件类型，如click、keydown等， fnHandler是事件回调函数
        /**/
        addHandler: function (oElement, sEvent, fnHandler) {
          oElement.addEventListener ? oElement.addEventListener(sEvent, fnHandler, false) : oElement.attachEvent("on" + sEvent, fnHandler)
        },
        /*
        此方法用来移除特定对象的特定事件，oElement是指定对象,sEvent是事件类型，如click、keydown等，fnHandler是事件回调函数
        /* */
        removeHandler: function (oElement, sEvent, fnHandler) {
          oElement.removeEventListener ? oElement.removeEventListener(sEvent, fnHandler, false) : oElement.detachEvent("on" + sEvent, fnHandler)//removeEventListener在firefox情况下使用，detachEvent在IE下使用
        },
        addLoadHandler: function (fnHandler) {
          this.addHandler(window, "load", fnHandler)
        }
        };
        EventUtil.addLoadHandler(function () {
            var aBtn = document.getElementsByTagName("input");

            //为第一个按钮添加绑定事件
            EventUtil.addHandler(aBtn[1], "click", function () {
            EventUtil.addHandler(aBtn[0], "click", fnHandler);
            aBtn[0].value = "我可以点击了";
        });

        //解除第一个按钮的绑定事件
        EventUtil.addHandler(aBtn[2], "click", function () {
            EventUtil.removeHandler(aBtn[0], "click", fnHandler);
            aBtn[0].value = "毫无用处的按钮";
        });

        //事件处理函数
        function fnHandler ()
        {
          alert("事件绑定成功！")
        }
    })