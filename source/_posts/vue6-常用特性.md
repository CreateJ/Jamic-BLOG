---
title: 'vue6:常用特性'
date: 2020-09-12 13:19:40
categories: vue学习
tags:
 - vue
 - 日常笔记
---

## 1.表单操作

```html
<div id="app">
  <form action="http://itcast.cn">
    <div>
      <span>姓名：</span>
      <span>
          <input type="text" v-model='uname'>
        </span>
    </div>
    <div>
      <span>性别：</span>
      <span>
          <input type="radio" id="male" value="1" v-model='gender'>
          <label for="male">男</label>
          <input type="radio" id="female" value="2" v-model='gender'>
          <label for="female">女</label>
        </span>
    </div>
    <div>
      <span>爱好：</span>
      <input type="checkbox" id="ball" value="1" v-model='hobby'>
      <label for="ball">篮球</label>
      <input type="checkbox" id="sing" value="2" v-model='hobby'>
      <label for="sing">唱歌</label>
      <input type="checkbox" id="code" value="3" v-model='hobby'>
      <label for="code">写代码</label>
    </div>
    <div>
      <span>职业：</span>
      <select v-model='occupation' >
        <option value="0">请选择职业...</option>
        <option value="1">教师</option>
        <option value="2">软件工程师</option>
        <option value="3">律师</option>
      </select>
    </div>
    <div>
      <span>个人简介：</span>
      <textarea v-model='desc'></textarea>
    </div>
    <div>
      <!--注意要使用js的方式来提交-->
      <input type="submit" value="提交" @click.prevent='handle'>
    </div>
  </form>
</div>
</body>
<script>
  let app = new Vue({
    el: '#app',
    data: {
      uname: 'Jamie',
      gender: 1,
      hobby: ['1','2'],
      occupation: 1,
      desc: 'Jamie is a softwareEngineer!',
    },
    method:{
    }
  })
</script>
```

# 