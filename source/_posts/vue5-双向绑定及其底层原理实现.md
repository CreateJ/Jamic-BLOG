---
title: 'vue5:双向绑定及其底层原理实现'
date: 2020-09-12 13:19:03
categories: vue学习
tags:
 - vue
 - 日常笔记
---

这里，**@input**的作用是**DomLinsteners**，**:value**的作用是**DataBindings**

```html
<div id="app">
  <!--这里三行的作用等价-->
  <input type="text" v-model="msg"><br>
  <input type="text" v-bind:value="msg" v-on:input="handle"><br>
  <input type="text" :value="msg" @input="msg=$event.target.value"><br>
  <div>{{msg}}</div>
</div>
<script src="../../js/vue.js"></script>
<script>
  let app = new Vue({
    el: '#app',
    data: {
      msg: '',
    },
    methods: {
      handle: function (event){
        //使用最新的输入域中的内容来更新msg的内容
        this.msg = event.target.value;
      }
    }
  })
</script>
```

# 