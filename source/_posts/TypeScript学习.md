# TypeScript学习

## 1.基础

### 1.注解

1. 声明变量类型

   ```typescript
   let a : number
   ```

   

2. 声明函数的入参和出参类型

   ```typescript
   const fun1 = (arg1: number, arg2: number): number => {
     return arg1 + arg2
   }
   ```

### 2.类型

#### 1.字面量

```typescript
let a : 10
// 联合类型
let sex : "male" | "female"
sex = "male"
sex = "female"
```

#### 2.any（不建议使用 ）

关闭ts的类型检测

可以被赋值给所有类型的变量，也可以被所有类型的变量赋值

```typescript
let b;
b = 1
b = '1'
b = true
```

#### 3.unknown

```typescript
let a : 10 // any

let c : unknown
c = 1
c = '1'
c = true

// any与unknown的区别
let d : string
// any类型可以赋值给其他变量
d = b 
// unknown类型不可以赋值给其他变量
// d = c 
d = c as boolean
```

#### 4.void

用于空返回类型

```typescript
const fun2 = (arg: number): void => {
  console.log(`输入结果是${arg}`)
}
fun2(200)
```

#### 5.never(无法理解)

不能是任何值，用于报错返回

```typescript
const fun3 = (): never => {
  // throw new Error('抛出一个错误')
}
fun3()
```

#### 6.object

1. 指定变量类型为对象

   ```typescript
   let O1 : object
   let O2 : {name: string}
   ```

2. 
