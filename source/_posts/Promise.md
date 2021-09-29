---
title: Promise
date: 2020-09-15 20:13:58
tags:
 - 日常笔记
 - Promise
---

# 1.使用场景

有异步操作的时候，会使用Promise对这个操作进行封装，防止套娃

# 2.基本结构

## 处理形式1

```javascript
      new Promise((resolve, reject) => {
        // 使用setTimeout模拟请求数据的异步操作
        setTimeout(() => {
          // 成功的时候执行resolve
          resolve(data.id);
          // 失败的时候执行reject
          reject(err);
        }, 1000);
      })
        .then((data) => {
          // 这里data就是上面resolve的参数
          // 数据的处理过程
        })
        .catch((err) => {
          // 错误信息展示
        });
```

## 处理形式2

```java
      new Promise((resolve, reject) => {
        // 使用setTimeout模拟请求数据的异步操作
        setTimeout(() => {
          // 成功的时候执行resolve
          resolve(data.id);
          // 失败的时候执行reject
          reject(err);
        }, 1000);
      }).then(
        (data) => {
          // 这里data就是上面resolve的参数
          // 数据的处理过程
        },
        (err) => {
          // 错误信息展示
        }
      );
```

# 3.两种简写

```javascript
      new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve("Jamie");
        }, 1000);
      })
        .then((data) => {
          // 正常写法
          return new Promise((resolve, reject) => {
            setTimeout(() => {
              resolve(data.toLocaleLowerCase());
            }, 1000);
          });
        })
        .then((data) => {
          console.log(data);
          data += " Wang";
          // 初级简写
          return Promise.resolve(data + " Chi");
        })
        .then((data) => {
          console.log(data);
          // 超级简写
          return data + " Jie";
        })
        .then(data => console.log(data));
```

# 4.多异步操作写法

```javascript
      Promise.all([
        new Promise((resolve, reject) => {
          // 异步请求1：
          resolve('res1')
        }),
        new Promise((resolve, reject) => {
          // 异步请求2
          resolve('res2')
        }),
      ]).then((results) => {
        console.log(results);
      })
```



# 重要单词

## sync

synchronization  [ˌsɪŋkrənaɪ'zeɪʃ(ə)n] 同步

## async

asynchronization 异步