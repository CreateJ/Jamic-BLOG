---
title: 'vue1:基础知识'
date: 2020-09-12 13:14:25
categories: vue学习
tags:
 - vue
 - 日常笔记
---

## 1.MVVM

View：Dom树，可视化的部分

View-Model：即我们所用的Vue，分为两部分，分别为DomLinsteners和DataBindings

1. DomLinstener: View->Model
2. DataBindings: Model->View

Model：js代码中自己定义的部分，或者网络上传来的数据

## 2.语法糖

语法糖（Syntactic sugar），也译为糖衣语法，是由英国计算机科学家彼得·约翰·兰达（Peter J. Landin）发明的一个术语，指计算机语言中添加的某种语法，这种语法对语言的功能并没有影响，但是更方便程序员使用。通常来说使用语法糖能够增加程序的可读性，从而减少程序代码出错的机会。



### Vue中的语法糖

### 已知语法糖

```javascript
v-on:click=''
@click=''
```

```javascript
v-bind:src=''
:src=''
```

## 3.Vue的生命周期

 可以理解为，vue是封装好的，创建的过程中，他会有很多步骤，当你定义了类似于**create**的生命周期函数之后，他会在做完一些我们看不见的操作之后，将这个**function**作为回调函数调用，在源码中是以**callHook(vm,fn())**的形式

具体流程

```
beforeCreate(){}
created(){}
beforeMount(){}
mounted(){}
```

![Vue 实例生命周期](vue1-基础知识/lifecycle.png)