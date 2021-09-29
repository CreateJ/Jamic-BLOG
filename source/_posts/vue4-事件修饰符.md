---
title: 'vue4:事件修饰符'
date: 2020-09-12 13:17:58
categories: vue学习
tags:
 - vue
 - 日常笔记
---

事件修饰符可以串联，**@click.stop.prevent='fun'**

## **1.阻止事件冒泡**（.stop）

```html
<!--正常情况下，父盒子的点击事件会被冒泡触发，使用.stop修饰
	之后，就可以阻止事件冒泡-->
<div id="app" @click="handleFather">
  <button @click.stop="handle">click</button>
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {

    },
    methods: {
      handleFather: function (){
        alert('I am father!')
      },
      // 当直接调用函数名作为指令的时候，事件对象会
      // 作为第一个参数传进来，（有参数则为最后一个）
      handle: function (event){
        // 这里也有同样的作用
        // event.stopPropagation();
        alert('I am son!');
      }
    }
  })
</script>
```

## **2.阻止默认行为**（.prevent）

```html
<div id="app">
  <!--被prevent修饰之后，a标签的工作不再是跳转了-->
  <a href="https://www.baidu.com" @click.prevent="handle">百度</a>
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {
    },
    methods: {
      handle: function (event){
        console.log('点击了!');
      }
    }
  })
</script>
```

# 