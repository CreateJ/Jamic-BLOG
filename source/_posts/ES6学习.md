---
title: ES6学习
date: 2020-09-12 17:23:05
categories: Javascript学习
tags:
 - javascript
 - ES6
---

# let 与 const 关键字

let能享有块级作用域的特点，一个变量在同一个作用域中无法被let声明2次

const声明的变量一旦创建就必须初始化，且后续无法修改

tips： const声明的复杂对象，只能保证指向的地址不变，地址所存储内容无法保证不被修改

## 三个高级js数组函数

```javascript
// filter： 过滤
new_arr = old_arr.filter(fun(n){
	// 逻辑 return true 时，将n加入new_arr,否则不加入
})
// map： 计算
new_arr = old_arr.map(fun(n){
	// return 计算结果，将计算结果push到new_arr中
})
// reduce: 汇总
res = old_arr.reduce(fun(preValue,n){
	// return preValue和n的计算逻辑，例如preValue+n,计算数组中数字的总和
},0)//这里0为preValue的默认值
```

# 08-函数扩展

## 02-Array.from()

### 01-主要作用

将对象转换成数组

可以将所有拥有Iterator（遍历器）接口的数据结构转换成数组

### 02-第二个参数

传入一个方法，用于将处理后的数据放入返回的数组，类似于map函数

```javascript
Array.from({ length: 2 }, () => 'jack')
// ['jack', 'jack']
```

## 03-Array.of()

### 01-主要作用

将一组值转换为数组

```javascript
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
```

与Array方法的区别，没有参数，一个参数，大于等于两个参数的结果不同，需要额外记忆

```javascript
Array() // []
Array(3) // [, , ,]
Array(3, 11, 8) // [3, 11, 8]
```

## 04-copyWithin()

### 01-主要作用

在数组内部，将数组的某些位置的成员，替换为另一个位置的一个或者一组的成员

第一个参数代表目标位置，第二个参数代表替换的内容，第三个参数代表到第几个结束

```javascript
Array.prototype.copyWithin(target, start = 0, end = this.length)
```

```javascript
// 将3号位复制到0号位
[1, 2, 3, 4, 5].copyWithin(0, 3, 4)
```

## 05-find和findIndex

### 01-find()的使用方法

find用于找到数组中符合规范的某个成员，并返回该成员

该方法的参数是一个回调函数

```javascript
[1, 4, -5, 10].find((n) => n < 0)
// -5
```

该回调函数的可传入的三个参数分别是，当前值，当前位置和原数组

```javascript
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
```

### 02-findIndex（）的使用方法

findIndex用于找到数组的某个成员，并返回该成员的下标

使用方法与find一致，区别只有返回值不同

### 03-find和findIndex方法的第二个参数

第二个参数用于绑定回调函数的this对象

```javascript
function f(v){
  return v > this.age;
}
let person = {name: 'John', age: 20};
[10, 12, 26, 15].find(f, person);    // 26
```

### 04-可以发现NaN

indexOf方法无法识别数组中的NaN成员

## 06-fill()数组填充方法

### 01-主要作用

给一个给定的数组填充数据

```javascript
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]
```

### 02-第二、三个参数

用于指定填充的开始和结束的位置

## 07-entries(),keys()和values()遍历器对象生成方法

### 01-主要作用

遍历器对象包括，数组，字符串，类数组对象等

```javascript
for (let index of ['a', 'b'].keys()) {
  console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
  console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```

### 02-手动遍历

```javascript
let letter = ['a', 'b', 'c'];
let entries = letter.entries();
console.log(entries.next().value); // [0, 'a']
console.log(entries.next().value); // [1, 'b']
console.log(entries.next().value); // [2, 'c']
```

## 08-includes

### 01-主要作用

判断数组内是否包含与参数相同的成员，返回值为布尔值

区别于indexOf，可以正确判断NaN

### 02-第二个参数

用于指定起始位置

## 09-flat()，flatMap()数组拉平方法

### 01-flat()主要作用

将套娃数组拉平，参数代表要拉平几层

如果无论多少都要拉平，使用参数**Infinity**

### 02-flatMap()主要作用

将套娃数组拉平一层并使用传入的参数（方法），将数组转换成新数组返回

### 03-区别

flatMap()只能展开一层数组

# 09-数组的扩展

# 10-对象的扩展

## 01-Object.is

### 01-主要作用

用于严格比较两个值是否相等

### 02-与严格相等符号（===）比较

```javascript
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

## 02-Object.assign()

### 01-主要作用

用于将对象进行合并（可枚举属性）

```javascript
const target = { a: 1, b: 1 };

const source1 = { b: 2, c: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

### 02-注意事项

1.如果有同名属性，后面的会覆盖前面的

2.只有一个参数，则返回该参数本身

3.参数不是对象，则会转为对象然后返回

4.本拷贝为浅拷贝

5.可以处理数组，但是会把数组视为对象

### 03-常见应用场景

1.为对象添加属性

```javascript
class Point {
  constructor(x, y) {
    Object.assign(this, {x, y});
  }
}
```

2.为对象添加方法

```javascript
Object.assign(SomeClass.prototype, {
  someMethod(arg1, arg2) {
    ···
  },
  anotherMethod() {
    ···
  }
});

// 等同于下面的写法
SomeClass.prototype.someMethod = function (arg1, arg2) {
  ···
};
SomeClass.prototype.anotherMethod = function () {
  ···
};
```

3.克隆对象

4.合并多个对象

5.为对象设置默认值

```javascript
const DEFAULTS = {
  logLevel: 0,
  outputFormat: 'html'
};

function processContent(options) {
  options = Object.assign({}, DEFAULTS, options);
  console.log(options);
  // ...
}
```

默认值为DEFAULT对象，一旦options中有对应的同名属性，就会替代

