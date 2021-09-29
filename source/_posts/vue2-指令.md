---
title: 'vue2:指令'
date: 2020-09-12 13:16:02
categories: vue学习
tags:
 - vue
 - 日常笔记
---

## 1.v-for

自动遍历渲染相对应的数组内容

```html
<div id="app">
  <div :key="item.id" v-for="(item,index) in fruit">{{item.name}}</div>
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {
      fruit: [{
        name: 'apple',
        id: 1,
      },{
        name: 'banana',
        id: 2,
      },{
        name: 'pear',
        id: 3,
      }]
    },
    methods: {
    }
  })
</script>
```

**tips**：注意这里记得使用**v-bind：key='id'**或者**：key='id'**来提高vue渲染器的性能，但是对于实际开发没有任何影响

## 2.v-once

被修饰的**html**标签中的**mustache**语法不会再因为变量内容修改而被修改，优点是可以提高网页性能

```html
   <div id="app">
  <div>{{message}}</div>
  <div v-once>{{message}}</div>
  <!--  v-once的作用是让被修饰的标签的mustache语法
  不会因为对象内容被修改而修改-->
  <button v-on:click="click">修改</button>
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {
      message: '修改前是阴天',
    },
    methods: {
      click: function () {
        this.message = '修改后是晴天';
      },
    }
  })
</script>
```

## 3.v-text和v-html

**v-text**跟原生js的**ele.innerText()**有类似的意思

**v-html**和原生js的**ele.innerHTML()**有类似的意思

```html
<div id="app">
  <div>{{message}}你好帅！</div>
  <div v-text="message">你好帅！</div>
  <!--v-text不够灵活-->
  <div v-html="url"></div>
  <a href=""></a>
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {
      message: '你好二蛋！',
      url: '<a href="#">你好二蛋！</a>'
    },
    methods: {

    }
  })
</script>
```

## 4.v-pre

让被修饰的标签中的**mustache**语法失效，从而直接显示双大括号

```html
<div id="app">
  <div>{{message}}</div>
  <div v-pre>{{message}}</div>
  <!--v-pre = prevent：作用是让mustache语法失效-->
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {
      message: 123,
    },
    methods: {

    }
  })
</script>
```

## 5.v-choak（解决闪动问题）

**更推荐使用v-text语法**

vue解析之前，div中有一个属性v-cloak

vue解析之后，div中的v-cloak属性被删除

```html
<!--css部分-->
<style>
    [v-cloak] {
      display: none;
    }
  </style>

<!--html部分-->
<div id="app">
  <h2 v-cloak>{{message}}</h2>
</div>

<!--js部分-->
<script>
  setTimeout(function () {
    let app = new Vue({
      el: '#app',
      data: {
        message: '你好二蛋！',
      },
      methods: {

      }
    })
  },2000)
</script>
```

## 6.v-show

**决定元素是否显示出来**

```html
<div id="app">
  <div class="pink box"></div>
  <div class="lightBlue box" v-show="isShow"></div>
  <button @click="showHandle">显示/隐藏</button>
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {
      isShow: true,
    },
    methods: {
      showHandle: function (){
        this.isShow = !this.isShow;
      }
    }
  })
</script>
```

## 7.v-if & v-else-if & v-else

```html
<div id="app">
  <div v-if="msg>90">优秀</div>
  <div v-else-if="msg<=90&&msg>80">良好</div>
  <div v-else-if="msg<=80&&msg>70">及格</div>
  <div v-else="msg<=70">不及格</div>
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {
      msg: 88,
    },
    methods: {}
  })
</script>
```

**补充**：**v-if**可以和**v-for**一起使用

```HTML
<div id="app">
  <div v-if='item === 22' v-for="(item,key,index) in obj">{{(index + 1) + '---' + key + ': ' + item }}</div>
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {
      obj: {
        name: 'Jamie',
        gender: 'male',
        age: 22
      }
    },
    methods: {}
  })
</script>
```

结果只显示

```
3---age: 22
```

