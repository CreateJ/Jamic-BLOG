---
title: vue-cli
date: 2020-09-14 09:07:34
updated: 2020-09-15 08:38:34
categories: vue学习
tags: 
 - vue 
 - 前端学习
 - 日常笔记
---

# 创建项目

```
vue init webpack project
```

创建选项，一般只yes router选项，其他全no

# 启动项目

```
// 编译模式
npm run dev
// 打包模式
npm run build
```

## 注意事项

使用**vue ui**的方式创建项目的话，需要启动**vue ui**的时候给予**命令行工具管理员权限**



# 公共样式书写位置

在**src>assets>css**中创建**base.css**，将公共样式写进去

## 导入方式1

```
//main.js最后一行添加
require('./assets/css/base.css');
```

## 导入方式2

```
@import "./assets/css/base.css";
```



# 给路径起别名

作用：防止路径变化而到导致资源失效

配置方法：在package.json同级目录创建vue.config.js文件，填写以下内容

```javascript
module.exports = {
  configureWebpack: {
    resolve: {
      alias: {
        //配置别名,修改后需要重新编译才能生效
        assets: "@/assets",
        components: "@/components",
        views: "@/views",
      },
    },
  },
};
```

使用方法：

```html
<!--注意html中使用的时候，前面要加 ~ ，js中使用只需要包含 @ 就好了-->
<img src="~@/assets/image/tabbar/home.png" alt="">
```



# bug记录

### 1.多次点击router-link会出现报错

```error
Uncaught (in promise) NavigationDuplicated {_name: "NavigationDuplicated"
```

解决方法：将vue-router版本修改为3.0

```
npm i vue-router@3.0 -S
```

### 2.图片引入**:src**失效

#### 原因：浏览器将相对路径识别为项目目录，故图片无法读取到

```html
<img :src="abc" alt="">
```

```javascript
export default {
data() {
  return {
      // 错误写法
      // abc: "../../assets/image/tabbar/home.png"
      // 正确写法
      abc: require("../../assets/image/tabbar/home.png")
    };
  },
}
```

