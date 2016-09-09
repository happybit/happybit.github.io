---
layout: post
title: "Select Box Experience I"
date: 2016-09-07 20:25
comments: true
categories: Web
---

前段时间做了个简单的页面应用，其中用到了[Vue.js](http://vuejs.org/)去实现几种不同的select box，一些要点记录如下。

<!--more-->

Vue.js是一款轻量级的MVVM前端框架，使用Vue，一定程度就是忍受不了jQuery。但作为初学者，在前人用Bootstrap搭的网站上新增页面，本身已依赖大量jQuery的插件/组件，一时也无法全盘推翻。而Vue本身也并不像React，如选择它，就只能从一而终，且彻底抛弃其他框架。Vue可以和jQuery混搭使用，如不想重构，也可以work。后面有些功能，也不知道如何用Vue写，最后采用jQuery也能奏效。

实现一个简单的单选框，HTML原生的方式如下([jsfiddle](https://jsfiddle.net/slownoise/dbbzgds9/))：

~~~html
<select class="select2">
  <option value="1">Ongoing</option>
  <option value="2">Released</option>
  <option value="3">Delay</option>
  <option value="4">Hold</option>
</select>
~~~

如果用Vue([jsfiddle](https://jsfiddle.net/slownoise/ajtc1v4w/))：

~~~javascript
var allStatus = [
    {id: 1, text: "Ongoing"},
    {id: 2, text: "Released"},
    {id: 3, text: "Delay"},
    {id: 4, text: "Hold"}
];

var editPlanApp = new Vue({
    el: '#editPlanApp',
    data: {
        allStatus: allStatus,
        status: 1
    }
});
~~~

HTML这样写：

~~~html
<div id="editPlanApp">
  <select v-model="status" class="form-control">
    <option v-for="status in allStatus" v-bind:value="status.id">
      {{ status.text }}
  </select>
</div>
~~~

你会发现使用Vue之后，代码量还增加了。Don't worry，接下来我们对比一下如何获取已选项的value。

使用jQuery的方式:

~~~javascript
console.log($('.select2').select2("val"));
~~~

使用Vue的方式：

~~~javascript
console.log(editPlanApp.status);
~~~

而通过程序更新所选项的话，jQuery的方式时，找到页面元素，设置选项，接着trigger更新页面：

~~~javascript
$(".select2").select2('data',{id:1,text:"Ongoing"}).trigger('change');
~~~

Vue的话，直接赋值，即可自动更新页面元素：

~~~javascript
editPlanApp.status=1;
~~~

是不是更简洁清爽了？一旦页面涉及到交互和计算，用MVVM的优势就展现出来了。