# 原型链

```css
每个实例对象（object）都有一个私有属性（称之为 __proto__ ）指向它的构造函数的原型对象（prototype）。该原型对象也有一个自己的原型对象（__proto__），层层向上直到一个对象的原型对象为null。根据定义，null没有原型，并作为这个原型链中的最后一个环节。
```

# Some和forEach的区别

### forEach

- 遍历数组，数组中的每一项元素都调用一遍回调函数；
- 遍历整个数组，无法中途停止（即使有return也不会终止），所以效率低
- 返回值是undefined，不能链式调用；
- 不会改变原数组；

### some

- 遍历数组，查找是否存在满足条件的元素，如果有就停止循环
- 会根据回调函数的返回值确定是否停止循环；回调函数返回true就停止，否则继续循环；迭代效率更高；
- 返回值为布尔类型

# 函数内this的指向

这些this的指向，是当我们调用函数的时候确定的。调用方式的不同决定了this的指向不同，一般指向我们的调用者。

- 普通函数（this指向window）
- 构造函数调用（this指向实例对象 原型对象里面的方法也指向实例对象）
- 对象方法调用（this指向该方法所属对象）
- 事件绑定方法（this指向绑定事件对象）
- 定时器函数（this指向window）
- 立即执行函数（this指向window）

# 改变函数内部this指向

常用的有三种方法：call()、apply()、bind()

```css
call 第一个可以调用函数 第二个可以改变函数内的this指向
call 的主要作用可以实现继承
```

```css
apply 也是调用函数 第二个可以改变函数内部的this指向
apply 但是他的参数必须是数组（伪数组）
apply 的主要应用 比如：利用apply借助于数学内置对象求最大值
```

```css
bind 不会调用函数。但是能改变原来函数内部this指向。
bind 返回的是原函数改变this之后产生的新函数。
bind 的作用：如果有的函数我们不需要立即调用，但是又想改变函数内部this的指向，这时候就可以用bind。
```

## **call()、apply()、bind()总结：**

**相同点：**都可以改变函数内部this指向

**区别点：**

1. call和apply会调用函数，并且改变函数内部this指向。
2. call和apply传递的参数不一样，call传递参数aru1,aru2形式。apply必须传递的是数组。
3. bind不会调用函数，可以改变this指向

**主要应用场景：**

1. call经常做继承
2. apply经常跟数组有关系，比如借助数学对象实现最大值最小值
3. bind不调用函数，但是还想改变this指向。比如改变定时器内部的this指向

# 高阶函数

**定义：**
高阶函数是对其他函数进行操作的函数，它接受函数作为参数或将函数作为返回值输出。

# 闭包

**闭包的定义：（也是一个函数）**
闭包(closure)指有权访问另一个函数作用域中变量的函数。 简单理解，一个作用域可以访问另外一个函数内部的局部变量。

**闭包的作用：**
延伸了变量的作用范围。

# 递归

**递归的定义：**
如果一个函数在内部可以调用其本身，那么这个函数就是递归函数。

**简单理解：**函数内部自己调用自己，这个函数就是递归函数。

**递归函数的作用和循环效果一样**

由于递归很容易发生“栈溢出”错误(stack overflow)，所以必须要加退出条件return。

# 浅拷贝和深拷贝

1.浅拷贝只是拷贝一层，更深层次对象级别的只拷贝引用. 2.深拷贝拷贝多层，每一层级别的数据都会拷贝 3.ES6中有浅拷贝的语法糖：Object.assign(target,...sources) es6新增方法可以浅拷贝
**target：拷贝给谁？sources 拷贝的对象**

# ES6

## let

1.变量不能重复声明 2.块级作用域 3.不存在变量提升 4.不影响作用域链

## const

1.一定要赋初始值 2.一般常量使用大写（潜规则） 3.常量的值不能修改 4.不存在变量提升 5.块级作用域 6.对于数组和对象的元素修改，不算对常量做修改，不会报错

# 结构赋值

**定义：**
ES6允许按照一定模式从数组和对象中提取值，对变量进行赋值，这种被称为解构赋值。

# 模板字符串

1.变量拼接用${变量名}

# 箭头函数

**与其他声明方式对比，箭头函数具有的特点：**

1. this是静态的，this始终指向函数声明时所在作用于下的this的值
2. 不管使用call()、apply()、bind()都不会改变this指向
3. 不能作为构造实例化对象
4. 不能使用 arguments 变量
5. 箭头函数的简写
   (1) 省略小括号，当形参有且只有一个的时候
   (2) 省略花括号，当代码体只有一条语句的时候，return语句必须省略，而且语句的执行结果就是返回值
6. 箭头函数**适合**与this无关的回调，定时器，数组的方法回调
7. 箭头函数**不适合**与this有关的回调，事件回调，对象的方法

# rest参数

1. ES6引入rest参数，用于获取函数的实参，用来代替arguments.
2. rest生成的是数组，arguments生成的是对象.
3. rest参数必须放到参数最后.

# Symbol

**定义：**
ES6引入了一种新的原始数据类型Symbol，表示独一无二的值.

**特点：**

1. Symbol的值是唯一的，用来解决命名冲突的问题
2. Symbol的值不要与其他数据进行运算
3. Symbol定义的对象属性不能使用for...in进行遍历，但是可以使用Reflect.ownKeys来获取对象的所有健名

# 迭代器

**定义：**
迭代器(Iterator)是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作。

1. ES6创建了一种新的遍历命令for...of循环，Iterator接口主要提供for...of消费
2. 原生具备iterator接口的数据（可用for of遍历）
    1. Array
    2. Arguments
    3. Set
    4. Map
    5. String
    6. TypedArray
    7. NodeList
3. 工作原理
    1. 创建第一个指针对象，指向当前数据结构的起始位置
    2. 第一次调用对象的next方法，指针自动指向数据结构的第一个成员
    3. 接下来不断调用next方法，指针一直往后移动，直到指向最后一个成员
    4. 每调用next方法返回一个包含value和done属性的对象
       **注：需要自定义遍历数据的时候，要想到迭代器。**

# 面向对象

## 什么是面向对象

```css
面向对象不是新的东西，它只是过程式代码的一种高度封装，目的在于提高代码的开发效率和可维 护性。
```

**面向对象编程** —— Object Oriented Programming，简称 OOP ，是一种编程开发思想。 它将真实世界各种复杂的关系，抽象为一个个对象，然后由对象之间的分工与合作，完成对真实世界的模拟。

在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工，可以完成接受信息、处理数据、发出信息等任务。
因此，面向对象编程具有灵活、代码可复用、高度模块化等特点，容易维护和开发，比起由一系列函数或指令组成的传统的过程式编程（procedural programming），更适合多人合作的大型软件项目。

# 生成器

**定义：**
生成器函数是ES6提供的异步解决方案，语法行为与传统函数完全不同

# Promise

**前引**
Promise是ES6引入的异步编程的新解决方案。语法上Promise是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果。

1. Promise有三个状态
    1. 初始化、成功、失败

## 使用Promise封装读取文件的操作函数

```javascript
// 使用 Promise 封装，对异步任务进行封装
const promise = new Promise(function (resolve, reject) {
  fs.readFile('./resources/七律长征.md', (err, data) => {
    // 如果失败，让promise状态变为false
    if (err) reject(err);
    // 如果成功输出buffer
    reject(data.toString());
  });
});

// value 处理成功的情况下
promise.then(function (value) {
  console.log(value);
// reason 处理失败的情况下
}, function (reason) {
  console.log(reason);
})
```

## 使用Promise封装AJAX请求
```javascript
const p = new Promise((resolve, reject) => {
    // 1.创建HTTP请求
    const xhr = new XMLHttpRequest();

    // 2.初始化
    xhr.open("GET", "https://api.apiopen.top/getJoke");

    // 3.发送请求
    xhr.send();

    // 4.绑定事件，处理响应结果
    xhr.onreadystatechange = function () {
      // 对状态state进行判断
      if (xhr.readyState === 4) {
        // 判断响应状态码 200-299都为成功
        if (xhr.status >= 200 && xhr.status < 300) {
          // 表示成功
          resolve(xhr.response);
        } else {
          // 如果失败
          reject(xhr.status);
        }
      }
    }
  });

  // 指定回调
  p.then(function (value) {
    console.log(value);
  },function (reason) {
    console.error(reason);
  });
```

# Set方法
**实践：**

**（1）数组去重**

```javascript
let arr = [1, 2, 3, 4, 5, 4, 3, 2, 1];
// 去重的结果，声明一个新Set方法
let result = [...new Set(arr)];
console.log(result);
```

**（2）交集**

```javascript
let arr = [1, 2, 3, 4, 5, 4, 3, 2, 1];
let arr2 = [4, 5, 6, 4, 3, 4, 5, 6, 5];

// 第一步：去重，为了维持效率以及不必要的操作，要将数组去重之后再进行操作。
let result = [...new Set(arr)].filter(value => {
  // 去重arr2
  let s2 = new Set();
  if (s2.has(value)) {
    return true;
  } else {
    return false;
  }
});
console.log(result);

// 简化
let result = [...new Set(arr)].filter(value => new Set(arr2).has(value));
console.log(result);
```

**（3）并集**

```javascript
let union = [...new Set([...arr, ...arr2])];
console.log(union);
```

**（3）差集**
let diff = [...new Set(arr)].filter(value => !(new Set(arr2).has(value)));
console.log(diff);

# Map方法
定义：
ES6提供了Map数据结构。它类似于对象，也是键值对的集合。但是“键”的范围不限于字符串。各类型的值（包括对象）都可以当作键。Map也实现了iterator接口，所以可以使用【扩展运算符】和【for...of...】进行遍历。

# Class类

## ES5 通过构造函数实例化对象

```javascript
  // 手机
  function Phone(brand, price) {
    this.brand = brand;
    this.price = price;
  }

  // 添加方法
  Phone.prototype.view = function () {
    console.log('我可以看电影😀');
  }

  // 实例化对象
  let Apple = new Phone('iPhone13 Pro Max 远峰蓝', '8999');
  Apple.view();
  console.log(Apple);
```

## ES6 实例化对象
```javascript
class Phone {
    // 构造方法 名称不可修改，必须是constructor
    constructor(brand, price) {
      this.brand = brand;
      this.price = price;
    }

    // 方法必须使用该方法，不能使用 ES5 的对象完整形式
    call() {
      console.log('我可以打电话🍉');
    }
  }

  // 实例化对象
  let onePlus = new Phone('一加', 3499);
  console.log(onePlus);
```

# ES7 新特性

## Array.prototype.includes
Includes 方法检测数组中是否包含某个元素，返回布尔类型值。

## **
表示数字的几次方，例如2 ** 10 = 1024

# ES8 新特性

## async 和 await
async和await两种语法结合可以让异步代码像同步代码一样。

## async 函数
1. async函数的返回值为promise对象
2. promise对象的结果由async函数执行的返回值决定

## await 表达式
1. await必须写在async函数中
2. await右侧的表达式一般为promise对象
3. await返回的是promise成功的值
4. await的promise失败了，就会抛出异常，需要通过try...catch捕获处理

## Object.values和Object.entries
1. Object.values()方法返回一个给定对象的所有可枚举属性值的数组
2. Object.entries()方法返回一个给定对象自身可遍历属性[key,value]的数组

## Object.getOwnPropertyDescriptors
该方法返回指定对象所有自身属性的描述对象
