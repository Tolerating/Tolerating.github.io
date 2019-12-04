---
title: vue.js2.0学习(一)——基础
date: 2019/12/02 21:20:25
tags:
- vue2.0
categories:
- 前端开发
comments: false
---



vue.js是一套构建用户界面的渐进式框架。
`Vue`只关注视图层，采用自底向上增量开发的设计。
`Vue` 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件。

<!-- more -->

# `Vue`语法格式
## 基本格式：
```vue
var vm = new Vue({
//选项
})
```

实例:

     <div id="vue_det">
    		<h1>site : {{site}}</h1>
    		<h1>url : {{url}}</h1>
    		<h1>{{details()}}</h1>
    	</div>
    	<script type="text/javascript">
    		var vm = new Vue({
    			el: '#vue_det',
    			data: {
    				site: "菜鸟教程",
    				url: "www.runoob.com",
    				alexa: "10000",
    			},
    			methods: {
    				details: function() {
    					return  this.site + " - 学的不仅是技术，更是梦想！";
    				}
    			}
    		})
    	</script>

1.	`el(element)`参数是`DOM`元素中的`id`。
2.	`data`用于定义属性(也可以是实例外部方法(函数)的返回值),`v-model`双向绑定时,`data`中的属性若为空的话可以用双引号[""],会根据绑定的数据类型自动转换类型。
3.	`methods`用于定义函数,通过`return`来返回函数值。

## 设置属性

    var data = { site: "菜鸟教程", url: "www.runoob.com", alexa: 10000}
    var vm = new Vue({
        el: '#vue_det',
        data: data
    })

```javascript
// 它们引用相同的对象！
document.write(vm.site === data.site) // true

// 设置属性也会影响到原始数据
vm.site = "Runoob"
document.write(data.site + "<br>") // Runoob

// ……反之亦然
data.alexa = 1234
document.write(vm.alexa) // 1234
```



`vue`实例还提供了一些有用的实例属性与方法.它们都有前缀$.以便与用户定义的属性区分开来

例如:

    //我们的数据对象
    var data = { site: "菜鸟教程", url: "www.runoob.com", alexa: 10000}
    var vm = new Vue({
        el: '#vue_det',
        data: data
    })
     
    document.write(vm.$data === data) // true
    document.write("<br>") // true
    document.write(vm.$el === document.getElementById('vue_det')) // true


# Vue.js模板语法
## 插值

 - 文本


```vue
<p id="app">{{message}}</p>
var vm = new Vue({
	el:#app,
	data:{
		message:"hello world!"
	}
})
```

   




 		使用这种方法可能会出现闪烁问题,即页面中的DOM和数据还没有加载完成,页面上会显示出大括号
	解决:

```css
[v-cloak] {
  display:none;
}
```

在使用了双大括号语法的标签里使用v-cloak



扩展: v-text
文本插值,其等同于Mustache语法


```
<p v-text="msg"></p>
<!--和下面的一样-->
<p><{{msg}}/p>
```


​	
 2.  使用` v-once `指令,可以一次性的插值,当数据改变时,插值处的内容不会更新


 - Html

使用v-html指令用于输出html代码

	 <div id="app">
	    <div v-html="message"></div>
	</div>
	<script>
	    new Vue({
	        el: '#app',
	        data: {
	        	message: '<h1>菜鸟教程</h1>'
	        }
	    })
	</script>


 - 属性

   HTML属性中的值应使用v-bind指令(双大括号不能作用在HTML特性上)

   `<button v-bind:disabled="isButtonDisabled">Button</button>`	

   在布尔特性的情况下,它们的存在即暗示为true,  如果 `isButtonDisabled` 的值为 null , 
   `underfined `或 false,则disable的特性不会被包含在渲染出来的`<button>`元素中
   (即不加载这个特性)

 - 使用JavaScript表达式

   vue.js支持JavaScript表达式(每个绑定都只能包含单个表达式)

   JS表达式: 是由运算元和运算符(可选)构成，并产生运算结果的语法结构。

```html
<div>数学运算:{{x+y}}</div>
<div>三目运算符:{{ok?"yes":"no"}}</div>
<div>方法的调用{{msg.split(""),reverse().join()}}</div>
```

 - 指令

指令是带有 v-前缀的特殊属性
	指令用于在表达式的值改变时,将某些行为应用到DOM上

例如 v-if v-bind  v-text......

 - 参数

参数在指令后以冒号指明.
	例如 `v-bind:href = "url"`

这里的`href`是参数,告知 `v-bind `指令该元素的`href`属性与表达式url的值绑定

参数除了是HTML元素的属性,也可以是监听的事件名,如`:click`事件



 - 修饰符

   修饰符是以半角句号 `.` 指明的特殊后缀,用于指出一个指令应该以特殊方式绑定

   例如: `<form v-on:submit.prevent="onSubmit">...</form>`
    		`.prevent` 修饰符告诉 v-on 指令对于触发的事件调用`event.preventDefault()`

 - 用户输入

		使用 v-model 指令来实现双向数据绑定

实例:	  

   

     <div id="app">
        	<p>{{ message }}</p>
        	<input v-model="message">
        </div>
        <script>
         new Vue({
         	el: '#app',
            data: {
              message: 'Runoob!'
            }
          })
        </script>

按钮的事件可以使用 `v-on` 监听事件     例如:` v-on:click = "click"`

