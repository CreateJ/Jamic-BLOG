---
title: 'vue7:组件'
date: 2020-09-12 13:20:25
categories: vue学习
tags:
 - vue
 - 日常笔记
---

优先级：局部组件大于全局组件

重点： 所有组件都继承了vue的原型

## 1.局部组件

```html
    <div id="app">
      <cpm :key="index" v-for="(item,index) in id" :id="index"></cpm>
    </div>
    <script>
      // 局部组件
      const cpmc = Vue.extend({
            props: ["id"],
            data: function () {
              return {};
            },
            template: `
              <div>
                <h2>这个是组件{{id+1}}号</h2>
                <p>红红火火恍恍惚惚</p>
              </div>
              `,
          }
      );

      let vue = new Vue({
        el: "#app",
        data: {
          message: 1,
          id: [{ id: 0 }, { id: 1 }, { id: 3 }, { id: 4 }, { id: 5 }],
        },
        methods: {},
        components: {
          'cpm': cpmc,
        },
      });
    </script>
```



## 2.全局组件

```html
    <div id="app">
      <comp></comp>
    </div>
    <script src="../../js/vue.js"></script>
    <script>

      //全局组件
      Vue.component('comp',{
        data: function(){
          return {
            items: [1,2,3,4,5],
          }
        },
        template: `
          <div>
            <h2 :key="index" v-for="(item,index) in items">{{index+1}}</h2>
          </div>
        `
      })
      const app = new Vue({
        el: '#app',
        data: {
          message: ''
        }
      })
    </script>
```

## 3.组件模板的分离

1.使用script的方式引入，type选择text/x-template

```html
	<div id="app">
      <cpn></cpn>
    </div>
    <!-- 下面全局组件会找到id为cpn的script标签，
  将里面的内容作为模板渲染到整个dom中 -->
    <script type="text/x-template" id="cpn">
      <h2>这个是写在script里面的模板</h2>
    </script>
    <script src="../../js/vue.js"></script>
    <script>
      Vue.component("cpn", {
        template: "#cpn",
      });
      const app = new Vue({
        el: "#app",
        data: {
          message: "",
        },
      });
    </script>
```

2.使用template的方式引入，注意id为组件注册的id

```html
	<div id="app">
      <cpn></cpn>
    </div>
    <!-- 下面全局组件会找到id为cpn的template标签，
  将里面的内容作为模板渲染到整个dom中 -->
    <template id="cpn">
      <h2>这个是写在template标签里面的模板</h2>
    </template>
    <script src="../../js/vue.js"></script>
    <script>
      Vue.component("cpn", {
        template: "#cpn",
      });
      const app = new Vue({
        el: "#app",
        data: {
          message: "",
        },
      });
    </script>
```

## 4.参数使用问题

在组件中，参数data对应的是一个函数，数据存放在函数return的对象中。

```javascript
			data: function () {
              return {//数据，};
            },
```

5.相同组件多次引用，之间数据不互通

## 6.父子传参

### 1.数组类型

```
props: ['parm1','parm2']
```

### 2.对象类型

```javascript
props: {
	'parm1': Array,//这里对象对用的参数用于限制传参进来的参数数据类型
	'parm2': {
		type: String,
		default: 'default_num' //默认值，如果没有传参进来，就使用默认值
	}
}
```

### 3.驼峰命名注意点

参数如果是用驼峰命名法的话，注意在使用的时候要使用'-'连接两个单词

```javascript
<cpm :c-name="parm1" :c-movies="parm2">

props: ['cName','cMovies']
```



## 7.子父传参

```html
    <!-- 子组件模板内容 -->
    <template id="tags">
      <div>
        <!-- 设置子组件的点击事件 -->
        <button :key="item.id" v-for="item in tags_list" @click="btnClick(item)">{{item.name}}</button>
      </div>
    </template>


    <div id="app">
      <!-- 引用模板，注册监听事件，与子组件的点击事件中传回的第一个参数同名，接收默认自带子组件传递过来的数据，这里cpnClick括号内不写，下方监听函数也可以直接使用item参数 -->
      <tags @item-click="cpmClick"></tags>
    </div>
    <script src="../../js/vue.js"></script>
    <script>
      Vue.component("tags", {
        template: "#tags",
        data: function () {
          return {
            tags_list: [
              { id: "aaa", name: "热门推荐" },
              { id: "bbb", name: "男生上衣" },
              { id: "ccc", name: "男生裤子" },
              { id: "ddd", name: "女生上衣" },
              { id: "eee", name: "女生裤子" },
            ],
          };
        },
        methods: {
          btnClick: function(item){
            // 设置子组件的点击事件，传回的数据名称以及数据
            this.$emit('item-click',item);
          }
        }
      });
      const app = new Vue({
        el: "#app",
        data: {
          message: "",
        },
        methods: {
          cpmClick: function(item){
            console.log('触发了父组件的点击事件,收到了'+item.name+'按钮传来的参数');
          }
        }
      });
    </script>
```

```
		@click="btnClick(item)"
		
		btnClick: function(item){
			// 将参数传递给父组件
            this.$emit('item-click',item);
          }
          
		@item-click="cpmClick"
		
		cpmClick: function(item){
            // 处理逻辑
          }
```

tips：传参只能使用‘-’命名法，否则失效

## 8.所有的组件都继承vue原型（学习vue-cli之后补充）

在main.js文件添加

```javascript
Vue.prototype.name = 'Jamie'
```

之后在所有组件中，只要使用

```javascript
console.log('this.name');
```

即可打印出来

```
Jamie
```

原理就是先修改了vue的原型之后，所有继承于vue的组件对象中都拥有这个原型属性