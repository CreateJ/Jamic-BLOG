---
title: vue-router
date: 2020-09-10 08:00:00
updated: 2020-09-12 22:19:57
categories: vue学习
tags: 
 - vue 
 - 前端学习
 - 日常笔记
---

## 1.router--index.js文件各配置作用

**mode**：默认为**hash**模式，不方便使用**history.pushState**

**linkActiveClass**：用于将渲染出来的**html**文件中的**router-link-active|Class**替换成**active**，便于代码维护

```js
import Vue from 'vue'
import Router from 'vue-router'
//这里注意要将使用到的组件导入进来
//普通导入方法
//import Home from '@/components/Home'
//懒加载写法
const Home = () => import('../components/Home.vue')

//所有的插件都需要使用vue.use(插件名)导入
Vue.use(Router)

export default new Router({
  mode: 'history',
  linkActiveClass: 'active',
  routes: [ 
    {
      // 根目录写在最前面
      path: '',
      redirect: '/home', //重定向
    },{
      path: '/home',
      // 这个是为了同个页面不同个组件区分时使用
      // eg: <router-view name="Hello"/>
      name: 'Home',
      component: Home,
    },
  ]
})
```

## 2.router跳转方式

### 1.html中

```javascript
<router-link to="/home" tag="button" replace>首页</router-link>
<router-link to="/about" tag="button" replace>关于</router-link>
```

1. to指向要跳转的页面
2. tag表示要渲染成的标签类型
3. replace表示是否可以前进后退

### 2.js中

```javascript
this.$router.push('/home');
this.$router.replace('/home');
```

#### **push()**和**replace()**的区别

**push**可以通过浏览器左上方的前进后退记录，原理跟栈差不多

**replace**不行

## 3.动态路由

### 1.添加

```html
<router-link :to="'/user/'+userId" tag="button" replace>用户</router-link>
```

```javascript
data: function(){
    return {
      userId: 'Jamie'
    }
  },
}
```

这里to属性需要使用冒号修饰，保证可以使用data中的属性

### 2.子组件获取路由参数

使用**this.$route.params.userId**获取

## 3.router和route的区别

**router**是指整个对象

**route**是指当前活跃的路由对象

## 4.路由懒加载写法

1.结合**vue**异步组件和**Webpack**的代码分析（过于复杂，不推荐）

2.AMD写法

```javascript
const Home = resolve => require(['../components/Home.vue'],resolve);
```

3.ES6写法(推荐)

```javascript
const Home = () => import('../components/Home.vue');
```

## 5.路由传参

### 1.使用query方式传参(复杂对象)

父组件中

```html
<router-link :to="{path:'/profile',query:{name: 'Jamie',age:'22',height:'1.70'}}" tag="button" replace>档案</router-link>
```

子组件中

```html
<template>
  <div id="profile">
    <h2>这里是档案</h2>
    <h2>姓名：{{$route.query.name}}</h2>
    <h2>年龄：{{$route.query.age}}</h2>
    <h2>身高：{{$route.query.height}}</h2>
  </div>
</template>
```

### 2.使用params方式传参(简单参数)

父组件中

```
<router-link :to="''/user/'+userId" tag="button" replace>用户</router-link>
```

子组件中d

```
this.$route.params.userId
```

## 6.守卫导航

### 使用方法： 

在**/router->index.js**中，覆盖了**router**组件的**beforeEach**生命周期函数

```javascript
router.beforeEach((to, from, next) => {
  // 原理：
  // 当路由切换的时候，自动调用beforeEach中的内容，对网页进行修改的过程

  // 这个功能是为了实现切换路由的时候，标签的名字自动更改
  // 这里meta是元数据（描述数据的数据）的意思，需要在route定义的时候添加一个meta对象才能读取到
  // 将title放在里面方便读取 eg：meta: { title: "首页" }，meta与name等属性同级
  document.title = to.meta.title;
  next();
})
```

## 7.路由使用实例1

切换到兄弟组件时，保存当前组件中子组件的选中状态，下次返回该组件的时候访问该子组件

```javascript
export default{
  data() {
    return {
      path: '/home/news'
    };
  },
  created() {
    console.log('create + ' + this.path);
    this.$router.push(this.path)
  },
  activated(){
    console.log('activated + '+ this.$route.path);
    this.$router.push(this.path);
  },
  beforeRouteLeave(to,form,next){
    console.log('before route leave + ' + this.$route.path);
    this.path = this.$route.path;
    next()
  },
  deactivated(){
    // 激活时间太晚，route已经更新成另一个组件了，不适用
  },
}
```



# bug合集

## 1.使用click方式跳转同个路由的时候路由器控制台会爆红

### 原因：

阻止多余的同名路由跳转，节省浏览器资源

### 解决方法：

跳转路由的时候，多加一层判定，判断原路由与目标路由是否相同，若不同则切换路由

```javascript
if(this.$route.path != nextPath){
	this.$router.replace(nextPath);
}
```



## 无法理解的部分

关于router源码部分在[视频](https://www.bilibili.com/video/BV17j411f74d?p=113)第113集

