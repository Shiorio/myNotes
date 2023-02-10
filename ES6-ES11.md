# ES6-ES11

## 一、ES6简介

### 1.什么是ES6

ES的全称是ECMAScript，它是由ECMA国际标准化组织制定的一项**脚本语言的标准化规范**。

可以简单理解为：ECMAScript是JavaScript的语言规范，JavaScript是ECMAScript的实现和扩展。

| 年份      | 版本   |
| --------- | ------ |
| 2015年6月 | ES2015 |
| 2016年6月 | ES2016 |
| 2017年6月 | ES2017 |
| 2018年6月 | ES2018 |
| ...       | ...    |

ES6实际上是一个泛指，泛指ES2015及后续的版本。

### 2.为什么使用ES6

> 每一次标准的诞生都意味着语言的完善，功能的加强。JavaScript语言本身也有一些令人不满意的地方。

- 变量提升特性增加了程序运行时的不可预测性；
- 语法过于松散，实现相同的功能，不同的人可能会写出不同的代码。

## 二、ES6新增语法

### 1.let

ES6中新增的用于声明**变量**的关键字。

let的声明变量**只在所处的块级作用域有效**。

> 块作用域：Js中包含全局作用域、函数作用域，没有块作用域的概念。在ES6中，新增了块作用域。**块作用域由{}包括**，if和for语句中的{}也属于块作用域。

```js
if (true) {
	let a = 10;
}
console.log(a);	// a is not defined
```

#### 1.1 特点

- 具有块级作用域，能够防止循环变量变成全局变量；

  ```js
  // 使用var声明循环变量
  for(var i = 0; i < 2; i++) {
  
  }
  console.log(i);	// 2	// for循环定义的迭代变量会渗透出去，也就是渗透到循环体外部
  ```

- 不存在变量提升；

  > 变量提升：在当前上下文中（全局/私有/块级），js代码自上而下执行之前，浏览器会提前处理一些事情（可以理解为词法解析的一个环节，词法解析一定发生在代码执行之前）。
  >
  > 变量提升会把上下文中的所有带var/function关键字进行提前声明或者定义。

  **var的变量提升**

  ```js
  // 代码执行之前，全局上下文中的变量会提升
  // var a; 默认是undefined
  console.log(a); // 输出undefined
  var a = 12; // 执行到这才会给 a赋值 12（不需要声明a了，变量提升阶段完成了，完成的事情不会重新处理）
  a = 13; // 全局变量 a=13
  console.log(a); // 13
  ```

  **function的变量提升**

  ```js
  /*
  全局上下文中的变量提升
  fn = 函数   这个阶段函数的声明和赋值都做了，所以 调用fn()可以在函数代码之前调用
  */
  fn();
  function fn() {
    var a = 12;
    console.log("ok");
  }
  ```

  ```js
  fn(); // 会报错  TypeError: fn is not a function，因为用var 声明的变量只会声明fn但是不会赋值
  var fn = function () {
    var a = 12;
    console.log("ok");
  };
  ```

  ```js
  var fn = function fb() {
    // 原本匿名函数给具名化以后，但是在外部依然是不能方位的，在当前上下文中是不会创建这个名字，但是在函数内部我们是可以调用这个函数名，因为：在函数执行时，在形成私有上下文中，会把这个具名化的名字作为私有上下文中的变量来处理
    var a = 12;
    console.log("ok");
    fb(); // 递归调用
  };
  fb(); // 会报错Uncaught ReferenceError: fb is not defined
  fn();
  ```

  **let和const不存在有变量提升**

  ```js
  console.log(a); // 会报错Uncaught ReferenceError: a is not defined
  let a = 1;
  ```

- 暂时性死区；

  > 如果区块中存在let和const命令，这个区块对这些命令声明的变量就形成封闭的作用域。在声明之前使用这些变量，就会报错，这就是暂时性死区。
  >
  > 解释：当程序的控制流程在新的作用域进行实例化时，在此作用域中用let/const声明的变量会先在作用域中被创建出来，但因此时还未进行词法绑定（对声明语句进行求值运算），所以不能被访问（访问就会抛出错误）。

  ```js
  var tmp = 123;
  if (true) {
  	tmp = 'abc';
      console.log(tmp);
  	let tmp;	// 形成封闭的作用域
  }
  ```

#### 1.2 经典面试题

1. 结果：2 2

   ![image-20220420110711292](https://gitee.com/v876774538/my-img/raw/master/image-20220420110711292.png)

2. 结果：0 1

   ![image-20220420110906251](https://gitee.com/v876774538/my-img/raw/master/image-20220420110906251.png)

### 2.const

ES6中新增的用于声明**常量**的关键字，常量指的就是值（内存地址）不能变化的值。

#### 2.1 特点

- 具有块级作用域；

  ```js
  if (true) {
  	const a = 10;
  }
  console.log(a);	// a is not defined
  ```

- **声明常量时必须赋初始值**；

  ```js
  const PI;	// Missing initializer in const declaration
  ```

- 常量赋值后，值（内存地址）不可修改

  ```js
  // 基本数据类型 值不可更改
  const PI = 3.14;
  PI = 100;	// Assignment to constant variable
  ```

  ```js
  const ary = [100, 200];
  ary[0] = 'a';
  ary[1] = 'b';
  console.log(ary);	// ['a', 'b']	// 复杂数据类型 由于并没有修改其内存地址 因此其数据结构内部的值可以进行修改
  ary = ['a', 'b'];	// Assignment to consstant variable
  ```

#### 2.2 let、const、var的区别

| var          | let            | const          |
| ------------ | -------------- | -------------- |
| 函数级作用域 | 块级作用域     | 块级作用域     |
| 变量提升     | 不存在变量提升 | 不存在变量提升 |
| 值可更改     | 值可更改       | 值不可更改     |

在我们编写程序的过程中，若存储的数据不需要变化，尽量使用const关键字。

**const优先，let次之。**

### 3.解构赋值

ES6中**允许从数组中提取值，按照对应位置，对变量赋值**。对象也可以实现解构。

ES6中对变量的赋值遵循一个规则，只要左右两边的模式相同，就可以进行合法赋值。

#### 3.1 数组解构

```js
// [a, b, c]此处的[]是解构的意思
let [a, b, c] = [1, 2, 3];
console.log(a);	// a
console.log(b);	// b
console.log(c);	// c
```

```js
let [a, [b], d] = [1, [2, 3], 4];
console.log(a);	// 1
console.log(b);	// 2
console.log(c);	// 4
```

若解构不成功（没有对应的值），变量的值为undefined。

```js
let [foo] = [];
console.log(foo);	// undefined
let [bar, foo] = [1];
console.log(bar);	// 1
console.log(foo);	// undefined
```

#### 3.2 对象解构

```js
let person = {
	name: 'zhangsan',
	age: 20
};
let {name, age} = person;
console.log(name);	// 'zhangsan'
console.log(age);	// 20
```

```js
let {name: myName, age: myAge} = person;	// 别名 myName myAge
console.log(myName);	// 'zhangsan'
console.log(myAge);	// 20
```

### 4.箭头函数

ES6新增的定义函数的方式。

```js
( 形参 ) => {
	// 函数体
}

const fn = () => {}
```

若函数体中只有一句代码，且代码的执行结果就是返回值，可以省略大括号。

```js
function sum(num1, num2) {
	return num1 + num2;
}

// 箭头函数
const sum = (num1, num2) => num1 + num2;
```

若形参只有一个，可以省略外侧小括号。

```js
function fn (v) {
	return v;
}

// 箭头函数
const fn = v => {
	alert(v);
}
```

箭头函数不绑定this关键字，箭头函数中的this，指向的是**函数定义位置的上下文this**。

箭头函数中的this引用的是**距离最近的作用域中的this**，从this的所在处向外层层寻找，直到有this的定义。

```js
// 按下按钮300ms后禁用按钮

var btn = document.querySelector('.btn');
btn.onclick = function() {
    this.disabled = true;
    setTimeout(function() {
        // 如果没有特殊指向，setInterval和setTimeout的回调函数中this的指向都是window，因为js的定时器方法是定义在window下的
        this.disabled = false;  // this指向的是window
    })

    // 赋值变量解决
    var that = this;
    setTimeout(function() {
        that.disabled = false;  // this指向的是调用者btn
    })

    // 利用bind解决
    setTimeout(function() {
        this.disabled = false;  // this指向的是调用者btn
    }.bind(this), 300);

    // 箭头函数
    setTimeout(() => {
        this.disabled = false;   // this指向的是调用者btn
    }, 300);

}
```

### 5.rest参数（剩余/多余参数）

剩余参数语法允许我们将一个**不定数量的参数**表示为一个**数组**。

```js
function sum(first, ...args) {
	console.log(first);	// 10
	console.log(args);	// [20, 30]
}
sum(10, 20, 30);
```

```js
const sum = (...args) => {
	let total = 0;
	args.forEach(item => total += item);
	return total;
}
sum(10, 20);	// 30
sum(10, 20, 30);	// 60
```

**剩余参数配合解构使用**

```js
let students = ['wangwu', 'zhangsan', 'lisi'];
let [s1, ...s2] = students;
console.log(s1);	// 'wangwu'
console.log(s2);	// ['zhangsan', 'lisi']
```

### 6.函数参数的默认值设置

```js
// 1. 形参初始值 具有默认值的参数 一般位置靠后（潜规则）
function add(a, b, c=10) {
	return a + b + c;
}
let result = add(1, 2);
console.log(result);
```

```js
function connect(options) {
	let host = options.host
	let username = options.userName
	...
}
// 2. 与解构赋值结合
function connect({ host="127.0.0.1", username, password, port});

let query = {
	host: 'localhost',
	username:'root',
	password: 'root',
	port: 8800
}
// 调用
connect(query)
```

### 7.Symbol

#### 7.1 Symbol介绍

> ES6引入了一种新的原始数据类型Symbol，**表示独一无二的值**。它是JavaScript语言的第七种数据类型（null， undefined, number, string, boolean, object, symbol）。

1. 创建Symbol

   ```js
   const a = Symbol();
   
   const b = new Symbol();	// 报错！Symbol是原始数据类型！
   ```

   使用Symbol()创建一个Symbol类型的值并赋值给a变量后，我们就得到了一个**在内存中独一无二的值**。

   现在除了通过变量a，任何人在任何作用域都无法重新创建出这个值。

   ```js
   const a = Symbol();
   const b = Symbol();
   console.log(a === b);	// false
   ```

   尽管a和b都是通过Symbol()创建出来的，但他们在内存中却是：

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191130113820517.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxNjk0Mjkx,size_16,color_FFFFFF,t_70)

   如果借助变量a给c赋值（地址）：

   ```js
   const c = a;
   console.log(c === a);	// true
   ```

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191130134842266.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxNjk0Mjkx,size_16,color_FFFFFF,t_70)

#### 7.2 Symbol的作用

**Symbol标记一块内存，不能与其他数据类型进行运算**。Symbol存在的主要目的就是作为对象属性的唯一标识符，**防止命名冲突**。

```js
//文件A.js
var a = {
	name: "夕山雨",
    getName(){
        return this.name;
    }
}
exports default a;

//文件B.js
var a = require("A.js");
a.getName = function(){
    return "xxx";
}

```

由于getName这个键本质上只是个字符串，而无论在哪个模块或作用域内，都可以直接引用到“getName”这个字符串，因此字符串类型的属性很容易被意外覆盖。

但是如果a中的属性是使用Symbol类型的变量作为键，那么它就无法被篡改：

```js
//模块A.js
var s = Symbol();
var a = {
	name: "夕山雨",
	//s是个变量，因此需要用中括号包裹起来
    [s]: function(){  
        return this.name;
    }
}
exports default a;

//模块B.js
var a = require("A.js");
var s = Symbol();

a[s] = function(){
    ...  //它不会对A模块中的[s]属性造成任何影响，因为两个模块的[s]不是同一个属性
}

```

#### 7.3 语法规范

1. 基本语法

   Symbol函数可以接收一个字符串作为参数，表示对Symbol实例的描述，主要是为了在控制台显示，或转为字符串时使用，比较容易区分。

   ```js
   var s1 = Symbol('Symbol1')
   var s2 = Symbol('Symbol2')
   ```

   注意:

   ```js
   var s1 = Symbol('Symbol')
   var s2 = Symbol('Symbol')
   console.log(s1 === s2)	// false
   ```

   在对象中使用：

   ```js
   let info1 = {
   	name: '婷婷',
   	age: 24,
   	job: '公司前台',
   	[Symbol('description')]: '平时喜欢做做瑜伽，人家有男朋友，你别指望了'
   }
   let info2 = {
   	name: '婷婷',
   	age: 24,
   	job: '公司前台',
   	[Symbol('description')]: '小姑娘挺好的，挺热情的……'
   }
   
   let target = {}
   Object.assign(target, info1, info2)
   console.log(target)
   ```

   ![image-20230130175300567](https://gitee.com/v876774538/my-img/raw/master/image-20230130175300567.png)

2. 属性的遍历

   以Symbol类型的变量作为对象属性时，该属性不会出现在`for … in`、`for … of`循环中，也不会被`Object.keys()`、`Object.getOwnPropertyNames()`、`JSON.stringify()`返回。

   但该属性并不是私有属性，它可以被专门的`Object.getOwnPropertySymbols()`方法遍历出来。该方法返回一个数组，包含了当前对象的所有用作属性名的Symbol值：

   ```js
   var s1 = Symbol('a');
   var s2 = Symbol('b');
   
   var a = {
       name: "夕山雨",
       [s1]: 24,
       [s2]: function(){}
   }
   
   var s = Object.getOwnPropertySymbols(a); //[Symbol(a), Symbol(b)]
   a[s[0]] = 24; //返回的数组元素不是字符串，而是实际的Symbol值，
                  //因此可以通过它引用到对象的该属性
   
   ```

   另外，ES6新增的`Reflect.ownKeys()`方法可以遍历出所有的常规键名和Symbol键名。语法为:

   ```js
   Reflect.ownKeys(a); //["name", Symbol(a), Symbol(b)]
   ```

3. Symbol.for(), Symbol.keyFor()

   使用`Symbol.for()`方法可以**创建相同Symbol**。

   通过该方法生成的Symbol会根据描述符进行**全局注册**，之后再次通过Symbol.for()传入相同描述符时，就可以得到相同的Symbol值。

   ```js
   var s1 = Symbol.for('symbol');  //向全局注册了以"symbol"为描述符的Symbol
   //由于描述符"symbol"已被注册到全局，因此这里创建的Symbol与上面是同一个
   var s2 = Symbol.for('symbol');  
   
   console.log(s1 === s2);	// true
   ```

   得到全局注册的Symbol的描述符，使用`Symbol.keyFor()`：

   ```js
   Symbol.keyFor(s1);	// "symbol"
   ```

#### 7.4 内置的Symbol值

> 上面讲到的Symbol的用法都是自定义的Symbol，在ES6中还定义了11个内置的Symbol，用于指向语言内部使用的方法。

1. Symbol.hasInstance

   当使用instanceof运算符判断某个对象是否为某个构造函数的实例时，就是在调用该构造函数上的静态方法[Symbol.hasInstance]，它时js引擎预先定义好的。

   ```js
   [] instanceof Array;  //true
   
   //浏览器实际上是在调用下面的方法
   Array[Symbol.hasInstance]([]);
   ```

2. Symbol.isConcatSpreadable

   该属性决定了当前对象作为concat的参数时是否可以展开。

   ```js
   var obj = {age: 24};
   [1].concat(obj); //[1, {age: 24}]
   ```

   通常情况下，obj被传入concat后会直接作为一个元素添加到数组中。

   可以通过将obj的**Symbol.isConcatSpreadable属性设置为true**，obj会在执行concat时尝试展开，**如果该对象无法展开，obj不会被拼接到数组中去。**所谓的**可展开**，指的是obj是否**为数组或类数组结构**。如果obj是数组，显然是可展开的，如果它有length属性，并且有"0"，"1"这样的属性键，那么它就是类数组，也是可以展开的：

   ```js
   //设置了该对象需要展开，但它无法展开，因此最终结果为[]
   var obj = {age: 24, [Symbol.isConcatSpreadable]: true};
   [].concat(obj); // []
   
   // 这是一个类数组对象，它是可展开的
   var obj = {
     length: 2, 
     "0": 24, 
     "1": 25, 
     name: "夕山雨",
     [Symbol.isConcatSpreadable]: true
   };
   // name属性被丢弃了，因为它无法被obj[index]的方式引用到
   [].concat(obj); //[24, 25]
   
   ```

3. Symbol.species

   该属性用于在继承的时候指定一个类的类别。如：

   ```js
   class T1 extends Promise {
   }
   
   class T2 extends Promise {
     static get [Symbol.species]() {
       return Promise;
     }
   }
   
   new T1() instanceof T1 // true
   new T2() instanceof T2 // false
   
   ```

   对于T1，由它构造出的实例默认都是T1的实例。而在T2中我们为该类定义了[Symbol.species]方法，它始终返回Promise，因此由T2构造出的实例都不再被认为是T2的实例，而是Promise的实例。

   该方法允许我们在定义衍生对象时，人为指定由它构造出的实例的构造函数。

4. Symbol.match/replace/search/split

   这四个方法允许我们以对象的方式自定义String的match、replace、search、split方法。

   - match

     以match为例，我们通常这样调用它：

     ```js
     var s = "hello";
     s.match(RegExp);  //匹配一个正则表达式
     ```

     假如我们需要为当前的字符串s**定制一个自己的match方法**，但是又不希望修改String原型上的match方法。Symbol.match就为我们提供了这种能力。

     **如果传入的对象具有[Symbol.match]方法，那么js引擎就会修改match方法默认的行为，去调用定义的[Symbol.match]方法。**如：

     ```js
     var a = {
         [Symbol.match](){
             return true;
         }
     }
     
     "hello".match(a);  //true
     // 等同于
     a[Symbol.match]("hello");  //true
     ```

   - replace

     ```js
     const x = {};
     x[Symbol.replace] = (...s) => console.log(s);
     
     'Hello'.replace(x, 'World') // ["Hello", "World"]
     ```

     由于replace的第一个参数有[Symbol.replace]方法，因此js引擎会调用这个方法，并把调用者‘Hello’和第二个参数‘World’作为参数传递给该方法。这样，上面的写法就等同于：

     ```js
     x[Symbol.replace]("Hello", "world");
     ```

   - search

     ```js
     var a = {
         [Symbol.match](){
             return true;
         }
     }
     
     "hello".search(a);  //true
     ```

   - split

     ```js
     var a = {
         sep: ",",
         [Symbol.match](t){
             return t.split(this.sep);
         }
     }
     
     "hello,world".split(a);  //["hello", "world"]
     ```

5. Symbol.iterator

   定义一个对象的**遍历器**（迭代器）方法。

   > 迭代器(Interator)是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署了Iterator接口，就可以进行遍历操作。

   1. ES6创造了一种新的遍历命令`for...of`循环，Iterator接口主要供for...of消费。

      `for...in` 和 `for...of`的区别：

      - 循环数组

        ```js
        const arr = [1,2,3,4]
         
        // for ... in
        for (const key in arr){
            console.log(key) // 输出 0,1,2,3	// for in 输出下标
        }
         
        // for ... of
        for (const key of arr){
            console.log(key) // 输出 1,2,3,4	// for of输出数组每一项的值
        }
        ```

      - 循环对象

        ```js
        const object = {
        	name: 'sjy',
        	age: 24,
        }
        
        // for ... in
        for (const key in obj) {
        	console.log(key)	// 输出 name, age	// for in 输出键名
        }
        
        // for ... of
        for (const key of obj) {
        	console.log(key)	// 报错！for of不能遍历对象
        }
        ```

      - 数组对象

        ```js
        const list = [
        	{
        		name: 'sjy',
        		age: 24
        	},
        	{
        		name: 'zs',
        		age: 23
        	}
        ]
        for (const val of list) {
        	console.log(val)
        	for (const key in val) {
        		console.log(key)
        	}
        }
        ```

        ![image-20230131110427655](https://gitee.com/v876774538/my-img/raw/master/image-20230131110427655.png)

      > 总结：**for in 适合遍历对象，for of 适合遍历数组**。二者都可以使用**break中断遍历**，而forEach不可以！

   2. 工作原理：

      - 创建一个**指针对象**，**指向当前数据结构的起始位置**；
      - 第一次调用对象的next方法，指针自动指向数据结构的第一个成员；
      - 接下来不断调用next方法，指针一直向后移动，直到指向最后一个成员；
      - 每次调用next方法返回一个**包含value和done属性的对象**。

   3. 自定义遍历数据

   **凡是具有[Symbol.iterator]方法的对象都是可遍历的**，可以使用`for … of`循环依次输出对象的每个属性。**数组和类数组，以及ES6新增的Map、Set等都原生部署了该方法，因此它们都可遍历。**如：

   ```js
   for(var item of [1,2,3]){
     console.log(item); //依次输出1，2，3
   }
   ```

   任何一个数组都具备这个原生的遍历器方法，但普通对象默认不具有该遍历器方法，无法使用循环遍历出对象所有的属性值。我们可以手动为该对象定义遍历器方法：

   ```js
   var a = {
       name: "夕山雨",
       age: 24,
       [Symbol.iterator]: function* (){
           yield this.name;
           yield this.age;
       }	// ES6的Generator函数（生成器函数，详见 8），它定义该遍历器先输出name属性，再输出age属性。
   }
   
   for(var item of a){
     console.log(item);  //依次输出："夕山雨"  24
   }
   ```

   ```js
   const banji = {
   	name: '终极一班',
   	stus: [
   		'xiaoming',
   		'xiaohong',
   		'xiaozhang',
   	],
   	[Symbol.iterator]() {
   		// 索引变量
   		let index = 0;
   		let _this = this;
   		return {
   			// 重写next方法
   			next: function() {
   				if (index < _this.stus.length) {
   					const result = { value: _this.stus[i], done: false}
   					index++
                         // 返回结果
                     	  return result
                     }
                     else {
                         return { value: undefined, done: true }
                     }
   			}
   		}
   	}
   }
   
   for(var item of banji {
     console.log(item);  //依次输出："xiaoming", "xiaohong", "xiaozhang"
   }
   ```

6. Symbol.toPrimitive

   定义了一个对象如何被**转化为一个基本数据类型**。

   通常对象是不能直接与基本数据类型的变量进行运算的，但是如果你为它定义了[Symbol.toPrimitive]方法，它就可以按照你所指定的规则转化为基本数据类型。它接收一个字符串，表示需要转换成的数据类型：

   ```js
   let obj = {
     [Symbol.toPrimitive](hint) {
       switch (hint) {
         case 'number':
           return 123;
         case 'string':
           return 'str';
         case 'default':
           return 'default';
         default:
           throw new Error();
        }
      }
   };	// 如果对象需要转化为数字，就返回123；如果需要转化为字符串，就转化为'str'；如果没有指定要转化的类型，那就返回字符串'Default'。
   
   2 * obj // 246
   3 + obj // '3default'
   obj == 'default' // true
   // 由于乘法运算*只能对数值操作，因此js引擎会调用[Symbol.toPrimitive]并传入"number"，将obj转化为数字。而加法既可以对数值生效，也可以对字符串生效，因此js引擎传入了"default"。该方法默认只接受number、string和default这三个值。
   String(obj) // 'str'
   ```

7. Symbol.toStringTag

   自定义**对象的toString()方法**。

   通常对象的toString方法会返回一个类似[object Object]的字符串，表示该对象的类型，如：

   ```js
   var a = {};
   
   a.toString();  // "[object Object]"
   ```

   修改对象的Symbol.toStringTag方法：

   ```js
   a[Symbol.toStringTag] = function(){
     return "xxx";
   }
   a.toString(); //"[object xxx]"
   ```

   定义的返回值覆盖了之前的字符串中的后半部分"Object"，因此该方法可以用于**定制对象的toString()的返回值**。

8. Symbol.unscopables

   该方法用于with语句。它指定在使用with语句时，哪些属性不属于with环境。

   ```js
   let author = {
       name: "夕山雨",
       age: 24,
       stature: "179",
       weight: 65
   }
   
   let name = "张三";
   let age = "28";
   
   with(author){
     console.log(name);  //“夕山雨”
     console.log(age);   //24
     console.log(stature);  //"179"
     console.log(weight);   //65
   }	// 临时扩展作用域链
   ```

   默认情况下，对于with语句内引用的变量，**js引擎会优先去with的作用对象上查找对应的属性**，如果找不到，才认为是外部变量。但是你可以**人为指定哪些属性不应该去作用对象上查找**，如：

   ```js
   var author = {
       name: "夕山雨",
       age: 24,
       stature: "179",
       weight: 65,
       get [Symbol.unscopables](){
         return { name: true, age: true }	// 指定name和age不在作用对象上查找
       }
   }
   
   var name = "张三";
   var age = "28";
   var stature = "153";
   var weight = 80;
   
   with(author){
     console.log(name);  // "张三"
     console.log(age);   // 28
     console.log(stature);  // "179"
     console.log(weight);   // 65
   }
   ```

### 8.生成器(Generator)

> 生成器函数是ES6提供的一种**异步编程解决方案**，语法行为与传统函数完全不同。

- 我们可以理解它是一个状态机，里面封装了多个内部状态；
- 执行Generator函数会返回一个**遍历器对象(Iterator)**，返回的遍历器对象可以依次遍历这个Generator函数的成员和状态；
- 写法上与普通函数不同的是：在声明关键字后面需要加上星号(*)，在函数内部可以使用**yield表达式**（yield关键字用来暂停和回富一个生成器函数）。

1. 生成与调用

   ```js
   function* helloWorld() {
   	yield 'hello'
   	yield 'world'
   	return 'ending'
   }
   
   let hello = helloWorld()
   hello.next() // {value: 'hello', done: false}
   hello.next() // {value: 'world', done: false}
   hello.next() // {value: 'ending', done: false}
   hello.next() // {value: undefined, done: true}
   ```

   ```js
   for(let v of helloWorld()) {
       console.log(v)
   }
   ```

   ![image-20230131135326424](https://gitee.com/v876774538/my-img/raw/master/image-20230131135326424.png)

   每当遇到yield，遍历器就会停止并且返回yield后面的对象信息，直到遇到return或者没有return时就返回undefined来结束遍历。这里yield起到一个暂停的作用。

2. 函数参数

   ```js
   function* helloWorld(arg) {
       console.log(arg)
       let one = yield 'hello'
       console.log(1, one)
       let two = yield 'world'
       console.log(2, two)
       return 'ending'
   }
   
   // 执行获取迭代器对象
   let iterator = helloWorld('AAA');
   console.log(iterator.next())
   // next方法传入实参
   console.log(iterator.next('BBB'))   // 传入参数
                                       // next传入参数将作为上一个yeild语句的返回结果
   console.log(iterator.next())
   ```

   ![image-20230131141538444](https://gitee.com/v876774538/my-img/raw/master/image-20230131141538444.png)

3. 实例1

   ```js
   // 1s后输出 111 再2s后输出 222 再3s后输出 333
   // setTimeout(() => {
   //     console.log(111)
   //     setTimeout(() => {
   //         console.log(222)
   //         setTimeout(() => {
   //             console.log(333)
   //         }, 3000)
   //     }, 2000)
   // }, 1000)    // 回调地狱
   
   function one() {
       setTimeout(() => {
           console.log(111)
           iterator.next()
       }, 1000)
   }
   
   function two() {
       setTimeout(() => {
           console.log(222)
           iterator.next()
       }, 2000)
   }
   
   function three() {
       setTimeout(() => {
           console.log(333)
           iterator.next()
       }, 3000)
   }
   
   function* gen() {
       yield one()
       yield two()
       yield three()
   }
   
   let iterator = gen()
   iterator.next()
   ```

4. 实例2

   ```js
   // 模拟获取 用户数据 订单数据 商品数据
   function getUsers() {
       setTimeout(() => {
           let data = '用户数据'
           iterator.next(data)
       }, 1000)
   }
   function getOrders() {
       setTimeout(() => {
           let data = '订单数据'
           iterator.next(data)
       }, 1000)
   }
   function getGoods() {
       setTimeout(() => {
           let data = '商品数据'
           iterator.next(data)
       }, 1000)
   }
   function *gen() {
       let users = yield getUsers()
       console.log(users)
       let orders = yield getOrders()
       console.log(orders)
       let goods = yield getGoods()
       console.log(goods)
   }
   let iterator = gen()
   iterator.next()
   ```

   ![image-20230131145514835](https://gitee.com/v876774538/my-img/raw/master/image-20230131145514835.png)

### 9.Promise

Promise是ES6引入的异步变成新解决方案。语法上Promise是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果。

详见`Promise+Axios.md`文件。

## 三、ES6的内置对象扩展

### 1.Array的扩展方法

#### 1.1 扩展运算符（展开语法）

扩展运算符可以将数组或对象转为以**逗号分隔**的**参数序列**。

```js
let ary = [1, 2, 3];
...ary;	// 1, 2, 3
console.log(...ary);	// 1 2 3	// 逗号在log中被作为分隔符省略了
console.log(1, 2, 3);	// 1 2 3
```

扩展运算符可以应用于**合并数组**。

```js
// 方法1
let ary1 = [1, 2, 3];
let ary2 = [3, 4, 5];
let ary3 = [...ary1, ...ary2];

// 方法2
ary1.push(...ary2);	// 直接追加给ary1
```

应用：**将类数组或可遍历对象（伪数组）转换为真正的数组**。

```js
let oDivs = document.getElementsByTagName('div');
console.log(oDivs);
oDivs = [...oDivs];
console.log(oDivs);
```

![image-20220420144740968](https://gitee.com/v876774538/my-img/raw/master/image-20220420144740968.png)

#### 1.2 构造函数方法：Array.from()

Array.from()方法从类似数组或可迭代对象创建一个新的（浅拷贝）的数组实例。

```js
Array.from(arrayLike, mapFn, thisArg);
```

- arrayLike：必选，想要转换成数组的伪数组对象或可迭代对象；
- mapFn：可选，若指定了该参数，新数组中的每个元素都会执行该函数；
- thisArg：可选，执行回调函数mapFn时this对象；
- 可迭代对象包括ES6新增的数据结构Set和Map。

```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};
let arr = Array.from(arrayLike);
console.log(arr);   // ['a', 'b', 'c']
console.log(arr[0]);    // a
console.log(typeof arr[0]);    // string
```

![image-20220420150321117](https://gitee.com/v876774538/my-img/raw/master/image-20220420150321117.png)

mapFn，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。

```js
let arrayLike = {
	'0': 1,
	'1': 2,
	'lenght': 2
}
let newAry = Array.from(aryLike, item => item * 2);	// [2, 4]
```

#### 1.3 实例方法：find()

用于**找出第一个符合条件的数组成员**，若有，则**返回符合条件的元素**，若无，则返回undefined。

```js
let ary = [{
	id: 1,
	name: '张三',
}, {
	id: 2,
	name: '李四',
}
];
let target = ary.find((item, index) => item.id == 2);
console.log(target);
```

![image-20220420151906914](https://gitee.com/v876774538/my-img/raw/master/image-20220420151906914.png)

和some()的区别：some()方法用于检测数组中的元素**是否存在**满足指定条件的元素，**返回布尔值**。

#### 1.4 实例方法：findIndex()

用于找出**第一个符合条件的数组成员的位置**，若未找到则返回-1。

```js
let ary = [1, 5, 10, 15];
let index = ary.findIndex((value, index) => value > 9);
console.log(index);	// 2
```

和indexOf的区别：

- indexOf：查找值作为第一个参数，采用===比较，更多的是用于**查找基本类型**，如果是对象类型，则是判断是否是同一个对象的引用；

  ```js
  const sisters = ['a', 'b', 'c', 'd', 'e'];
  console.log(sisters.indexOf('b'));
  // 1
  
  let sisters = [{a: 1}, {b: 2}];
  console.log(sisters.indexOf({b: 2}));
  // -1
  
  const an = {b: 2}
  sisters = [{a: 1}, an];
  console.log(sisters.indexOf(an));
  // 1
  ```

- findIndex：比较函数作为第一个参数，多用于**非基本类型（如，对象）的数组索引查找**，或查找条件较为复杂的情况。

#### 1.5 实例方法：includes()

表示某个数组是否包含给定的值，返回布尔值。

```js
[1, 2, 3].includes(2);	// true
[1, 2, 3].includes(4);	// false
```

#### 1.6 Array.prototype.flat()和flatMap()

1. flat()

   用于将嵌套的数组“拉平”（降维）。该方法返回一个新数组，对原数据没有影响。

   ```js
   // flat() 将多维数组转化为低维数组（降维）
   const arr = [1, 2, 3, 4, [5, 6, [7, 8, 9]]]
   console.log(arr.flat())
   console.log(arr.flat().flat())
   ```

   ![image-20230201180315905](https://gitee.com/v876774538/my-img/raw/master/image-20230201180315905.png)

   flat()默认只会拉平一层，如果想要拉平更多层嵌套，可以向flat()方法传递一个参数（整数），表示需要拉平的层数（默认为1）。

   ```js
   const arr = [1, 2, 3, 4, [5, 6, [7, 8, 9]]]
   console.log(arr.flat(2))
   ```

   如果不论有多少层嵌套，都要转为一维数组，可以用`Infinity`（无穷）关键字作为参数：

   ```js
   const arr = [1, 2, 3, 4, [5, 6, [7, 8, 9]]]
   console.log(arr.flat(Infinity))
   ```

   注意：若原数组存在空位，flat()方法会跳过空位

   ```js
   [1, 2, , 4, 5].flat()
   // [1, 2, 4, 5]
   ```

2. flatMap()

   flatMap()方法对原数组的每个成员执行一个函数，相当于执行Array.prototype.map(),然后对返回值组成的数组执行flat()方法。该方法返回一个新数组，不改变原数组。

   ```js
   const arr = [2, 3, 4]
   const result = arr.flatMap(item => [item, item * 2])
   // 相当于 先map()后flat()
   // const result = arr.map(item => [item, item * 2]).flat()
   console.log(result)
   ```

   - 增加元素

     ```js
     // 增加元素
     const msgArr = ["it's Sunny in", "California"];
     
     const newArr = msgArr.flatMap(i => i.split(' '))
     console.log(newArr); //   ["it's", "Sunny", "in", "California"]
     ```

   - 删除元素

     ```js
     // 删除元素
     const arr = [1, 2, 3, 4]
     
     const newArr = arr.flatMap(x => x % 2 === 0 ? [x]: [])
     console.log(newArr); // [2, 4]
     ```

   - 修改元素

     ```js
     // 修改元素
     const arr = [1, 2, 3, 4]
     
     const newArr = arr.flatMap(x => [x * 2])
     console.log(newArr); // [2, 4, 6, 8]
     ```

   实例：例如我们现在有一个选择公司的Select下拉组件，但是后端接口返回的公司列表里面的每一项的字段和我们Select下拉组件需要的字段格式不一样，而且我们还有一个特殊的要求，就是已授权的公司我们才允许在Select下拉组件中选择。这时候我们就想办法遍历公司列表，然后先**把未授权的公司过滤掉，然后再把每一项转换成Select下拉组件所需要的数据格式。**

   - 后端接口返回的数据：

     ```js
     /**
      * 后端接口返回的公司列表数据：
      * 	Id: 公司的唯一ID
      *  Name: 公司名称
      * 	Authorized: 是否已经授权： 1:已授权，2：未授权
      * 
      */
     
     const studioList = [{
             Authorized: "2",
             CompanyType: "1",
             Id: "3729",
             Name: "阿我打完的",
             ServiceProviderId: "6",
             TenantId: "1",
         },
         {
             Authorized: "1",
             CompanyType: "1",
             Id: "3134",
             Name: "纳税统计-启用时间202101无期初",
             ServiceProviderId: "6",
             TenantId: "1",
         },
         {
             Authorized: "1",
             CompanyType: "1",
             Id: "427",
             Name: "美丽人生工作室",
             ServiceProviderId: "6",
             TenantId: "1",
         },
         {
             Authorized: "1",
             CompanyType: "1",
             Id: "410",
             Name: "凭证测试专用2",
             ServiceProviderId: "6",
             TenantId: "1",
         }
     ]
     ```

   - 需要的数据结构：

     ```js
     [
         {
             text: '公司名称',
             value: '公司ID'
         }
     ]
     ```

   - filter() map()的方式：

     ```js
     const filterList = studioList.filter((item) => item.Authorized === '1').map((item) => {
         return {
             text: item.Name,
             value: item.Id
         }
     })
     // filter过滤掉未授权 map修改
     ```

   - flatMap()的方式：

     ```js
     const filterList = studioList.flatMap((item) => {
         return item.Authorized === '1' ? [{
             text: item.Name,
             value: item.Id
         }] : []
     })
     console.log(filterList)
     // flat() 展开时将会跳过空项
     ```

     

   

### 2.String的扩展方法

#### 2.1 模板字符串

ES6中新增的创建字符串的方式，使用反引号``定义。

在模板字符串中，可以**解析变量**。

```js
let name = 'zhangsan';

// 传统写法
// let sayHello = 'hello,' + name + '!';

// 模板字符串写法
let sayHello = `hello, ${name}!`;

console.log(sayHello);	// hello,zhangsan!
```

在模板字符串中，可以**换行**（**包裹html标签**）。

```js
let result = {
	name: 'zhangsan',
	age: 20,
	sex: '男'
}
let html = `
<div>
	<span>${result.name}</span>
	<span>${result.age}</span>
	<span>${result.sex}</span>
</div>
`
```

在模板字符串中，可以**调用函数**。

```js
const sayHello = function() {
	return 'hello!!!'
};
let greet = `${sayHello}`;
console.log(greet);
```

#### 2.2 实例方法：startsWith()和endsWith()

- startsWith()：表示参数字符串是否在原字符串的头部，返回布尔值；
- endsWith()：表示参数字符串是否在原字符串的尾部，返回布尔值。

```js
let str = 'Hello World!';
str.startsWith('Hello');	// true
str.endsWith('!');	// true
```

#### 2.3 实例方法：repeat()

repeat方法表示**将原字符串重复n次**，返回一个新字符串。

```js
'x'.repeat(3);	// 'xxx'
'hello'.repeat(2);	// 'hellohello'
```

### 3.Set数据结构

> ES6提供的新的数据结构Set（集合）。**类似于数组**，但**成员的值都是唯一的**，**没有重复的值**。

Set本身是一个构造函数，用来生成Set数据结构。

```js
const s = new Set();
```

Set函数可以接受一个数组作为参数，用来初始化。

```js
const set = new Set([1, 2, 3, 4, 4]);
console.log(set);
```

![image-20220420163247613](https://gitee.com/v876774538/my-img/raw/master/image-20220420163247613.png)

**实例方法**

- `add(value)`：添加某个值，返回Set结构本身；
- `delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功；
- `has(value)`：返回一个布尔值，表示该值是否为Set的成员；
- `clear()`：清除所有成员，没有返回值。

```js
const s = new Set();
s.add(1).add(2).add(3);	// 想set结构中添加值
s.delete(2);	// 删除set结构中的2值
s.has(1);	// 表示set结构中是否存在有1这个值，返回布尔值
s.clear();	// 清除set结构中的所有值
```

**遍历**

Set结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。

```js
s.forEach(value => console.log(value));
```

Set实现了iterator接口，所以可以使用**扩展运算符**和**for...of**进行遍历。

```js
const set = new Set(['张三', '李四', '王五', '赵六'])
// for of
for(let item of set) {
    console.log(item)
}
// 扩展运算符
console.log(...set)
```

![image-20230131160755147](https://gitee.com/v876774538/my-img/raw/master/image-20230131160755147.png)

**实践：**

```js
let arr1 = [1, 2, 2, 3, 4, 4]
let arr2 = [1, 3, 3, 5]
// 去重
let set = new Set(arr1)
console.log('去重前', arr1)
console.log('去重后', [...set])

// 交集
let intersection = [...new Set(arr1)].filter((item) => {
    return new Set(arr2).has(item)
})
console.log('交集', [...intersection])

// 并集
let union = [...new Set([...arr1, ...arr2])]
console.log('并集', union)

// 差集
let difference = [...new Set(arr1)].filter((item) => {
    return !(new Set(arr2).has(item))
})
console.log('差集', difference)
```

![image-20230131164544945](https://gitee.com/v876774538/my-img/raw/master/image-20230131164544945.png)

### 4.Map数据结构

> ES6提供了Map数据结构。
>
> 类似于对象，也是键值对的集合。但是键的范围不限于字符串，各种类型的值（包括对象）都可以被当作键。
>
> Map也实现了iterator接口，可以使用扩展运算符和for...of进行遍历。

声明Map：

```js
let m = new Map();
```

**实例方法**

- `set(key, value)`：添加一个新元素，返回当前Map；
- `get(key)`：返回键名对象的键值；
- `has(key)`：检测Map中是否包含某个元素，返回boolean值；
- `clear`：清空集合，返回undefined。

```js
// 声明map
let m = new Map();

// 添加元素
m.set('name', '张三')
m.set('age', 24)
m.set('change', function() {
    console.log('改变')
})
let key = {
    school: 'ATGUIGU'
}
m.set(key, ['北京', '上海', '深圳'])
console.log(m)

// 删除元素
m.delete('age')
console.log(m)

// 获取元素
console.log(m.get('name'))

// 检测
console.log(m.has('name'))

// 遍历
for (let v of m) {
    console.log(v)
}

// 清空
m.clear()
console.log(m)
```

![image-20230131172540026](https://gitee.com/v876774538/my-img/raw/master/image-20230131172540026.png)

### 5.数值拓展

1. `Number.isFinite()`

   用于检测一个数值**是否有限**。

   ```js
   let a = 1
   let r = Number.isFinite(a)     // 将a添加到Number中     如果a不是数字，直接返回false
   console.log(r);	// true
   ```

2. `Number.isNaN()`

   检测**是否为非数值型**。

   ```js
   let a = 1
   let r = Number.isNaN(a)
   console.log(r);	// false
   ```

3. `Number.parseInt()`

   可解析一个字符串，并**返回一个整数**。

   ```js
   let a = '1.2'
   let r = Number.parseInt(a)
   console.log(r);	// 1
   ```

4. `Number.parseFloat()`

   可解析一个字符串，并**返回一个浮点数**。

   ```js
   let a = '1.2'
   let r = Number.parseFloat(a)
   console.log(r); // 1.2
   ```

5. `Number.isInteger()`

   判断一个数值**是否为整数**。

   ```js
   let a = 1
   let r = Number.isInteger(a)
   console.log(r);	// true
   ```

6. `Math.trunc()`

   将小数部分抹掉（**取整**）。

   ```js
   let a = 1.2
   let r = Math.trunc(a)
   console.log(r)	// 1
   ```

7. `Math.sign()`

   判断一个数是正数、负数、还是零。

   ```js
   let a = -1.2
   let r = Math.sign(a)
   console.log(r)  // -1
                   // 正数 1 负数 -1 零 0
   ```

8. `Number.EPSILON`

   ES6在Number对象上，新增一个**极小的常量**Number.EPSILON，是JavaScript表示的最小精度。根据规格，它表示1与大于1的最小浮点数之间的差。EPSILON属性的值接近于2.2204460492503130808472633361816E-16。

   ```js
   function equal(a, b) {
       if (Math.abs(a - b) < Number.EPSILON) {
           return true
       } else {
           return false
       }
   }
   
   console.log(0.1 + 0.2, 0.1 + 0.2 === 0.3)	// 0.30000000000000004 false
   console.log(equal(0.1 + 0.2, 0.3))	// true
   ```

9. 二进制和八进制

   `ES6`提供了`二进制`和`八进制`数值的新的写法，分别用前缀`0b（或0B）和0o（或0O）`表示，第一个字符是`数字零`。

   ```js
   let b = 0b1010;
   let o = 0o777;
   console.log('二进制', b)
   console.log('八进制', o)
   ```

   ![image-20230131175454312](https://gitee.com/v876774538/my-img/raw/master/image-20230131175454312.png)

### 6.Object静态方法扩展

1. `Object.is()`

   判断两个值是否完全相等。

   ```js
   let a = 120
   let b = 120
   console.log(Object.is(a, b))	// true
   console.log(Object.is(NaN, NaN))	// true
   console.log(NaN, Nan)	// false
   ```

2. `Object.assign()`

   合并对象。

   ```js
   let queryParams = {
   	name: '',
   	type: 1,
   }
   let pagination = {
   	current: 1,
   	pageSize: 10
   }
   let query = Object.assign(queryParams, pagination)
   console.log('queryParams', queryParams)
   console.log('pagination', pagination)
   console.log('query', query)
   ```

   ![image-20230201093316428](https://gitee.com/v876774538/my-img/raw/master/image-20230201093316428.png)

   ```js
   let queryParams1 = {
   	name: '张三',
   	age: 23,
   	sex: '男'
   }
   let queryParams2 = {
   	name: '李四',
   	age: 24,
   }
   let query = Object.assign(queryParams1, queryParams2)
   console.log('queryParams1', queryParams1)
   console.log('queryParams2', queryParams2)
   console.log('query', query)
   ```

   ![image-20230201094528390](https://gitee.com/v876774538/my-img/raw/master/image-20230201094528390.png)

   ```js
   let queryParams = {
       name: '',
       type: 1,
   }
   let pagination = {
       current: 1,
       pageSize: 10
   }
   let query = {...queryParams, ...pagination}	// 扩展运算符
   console.log('queryParams', queryParams)
   console.log('pagination', pagination)
   console.log('query', query)
   ```

   ![image-20230201094118495](https://gitee.com/v876774538/my-img/raw/master/image-20230201094118495.png)

3. `Object.setPrototypeOf() Object.getPrototypeOf()`

   设置/获取原型对象。

   ```js
   let school = {
       name: '尚硅谷'
   }
   let cities = {
       xiaoqu: ['北京', '上海', '深圳']
   }
   Object.setPrototypeOf(school, cities)
   console.log(school)
   console.log(Object.getPrototypeOf(school))
   ```

   ![image-20230201094909752](https://gitee.com/v876774538/my-img/raw/master/image-20230201094909752.png)

4. `Object.keys()`

   返回对象所有属性组成的数组（键）。t

   ```js
   let queryParams = {
       name: '',
       type: 1,
       createTimeStart: '2023-02-01',
       createTimeEnd: '2023-02-02'
   }
   console.log(Object.keys(queryParams))
   ```

   ![image-20230201095450183](https://gitee.com/v876774538/my-img/raw/master/image-20230201095450183.png)

5. `Object.values()`

   返回对象所有属性值组成的数组（值）。

   ```js
   let queryParams = {
       name: '',
       type: 1,
       createTimeStart: '2023-02-01',
       createTimeEnd: '2023-02-02'
   }
   console.log(Object.values(queryParams))
   ```

   ![image-20230201095545070](https://gitee.com/v876774538/my-img/raw/master/image-20230201095545070.png)

6. `Object.entries()`

   返回该对象组成的键值对。

   ```js
   let queryParams = {
       name: '',
       type: 1,
       createTimeStart: '2023-02-01',
       createTimeEnd: '2023-02-02'
   }
   console.log(Object.entries(queryParams))
   ```

   ![image-20230201095818104](https://gitee.com/v876774538/my-img/raw/master/image-20230201095818104.png)

7. `Object.fromEntries()`

   将键值对转化为对应的对象。

   ```js
   let keyValues = [
       ['name', 'tom'],
       ['age', 12, ],
       ['gender', '男']
   ]
   console.log(Object.fromEntries(keyValues))
   ```

   ![image-20230201100439906](https://gitee.com/v876774538/my-img/raw/master/image-20230201100439906.png)


## 四、模块化

### 1.ES6模块化(ES module)

1. 好处

   - 防止命名冲突；
   - 代码复用；
   - 高维护性。

2. 模块化规范产品

   ES6之前的模块化规范有：

   1. CommonJS	=>	NodeJS、Browserify
   2. AMD		 =>	requireJS
   3. CMD		 =>	seaJS

   这些由社区提出的模块化标准，还是存在一定的差异性和局限性，并不是浏览器与服务器通用的模块化标准。比如：

   > - AMD和CMD适用于浏览器的Javascript模块化；
   > - CommonJS适用于服务器端的Javascript模块化。
   >   - 导出：`module.exports = 导出的内容`
   >   - 导入：`require('模块')`

3. 为什么要学习ES6模块化规范

   ES6模块化规范是浏览器端与服务器端通用的模块化开发规范。它的出现极大地降低了前端开发者的模块化学习成本，开发者不需再额外学习AMD、CMD或CommonJS等的模块化规范。

   > ES6模块化规范中定义：
   >
   > - 每个js文件都是一个独立的模块；
   > - 导入其他模块成员使用`import`关键字；
   > - 向外共享模块成员使用`export`关键字。

4. 在nodejs中使用ES6模块化

   node.js中默认支持CommonJS模块化规范，若想基于node.js使用ES6模块化语法，可以按照如下两个步骤进行配置：

   > 1. 确保安装了`v13.0.0`或更高版本的node.js
   > 2. 在package.json的根节点中添加`"type": "module"`节点
   >    - type默认为"commonjs"，表示项目代码只能使用CommonJS语法（module.exports导出，require导入）
   >    - type配置为"module"后，表示项目代码只能使用ES6模块化语法

### 2.ES6模块化语法

#### 1.1 默认导出（统一暴露）与默认导入

```js
// 默认导出
export default 默认导出的成员

// 默认导入
import 接收名称 from '模块路径'
```

- 导出

  ```js
  const a = 10
  const b = 20
  const fn = () => {
  	console.log('这是一个函数')
  }
  
  // 默认导出
  export default {
  	a,
  	b,
  	fn
  }
  // 注意：每个模块中，只允许出现唯一一次export default
  ```

- 导入

  ```js
  // 默认导入时的接收名称可以是任意名称，只要是合法的成员名称即可
  import result from './xxx.js'
  
  // 使用
  console.log(result)
  ```

  ![image-20230201104534138](https://gitee.com/v876774538/my-img/raw/master/image-20230201104534138.png)

  > 本地`html`文件中的`script`标签引入[ES6](https://so.csdn.net/so/search?q=ES6&spm=1001.2101.3001.7020)的模块，直接在浏览器中打开该`html`文件，报错：`Uncaught SyntaxError: Cannot use import statement outside a module`
  >
  > 解决方法：https://blog.csdn.net/cc18868876837/article/details/113915176

#### 1.2 按需导出（分别暴露）与按需导入

```js
// 按需导出
export ...

// 按需导入
import { 按需导入的名称 } from '模块标识符'	// 解构赋值形式
```

- 导出

  ```js
  export function sayHello() {
      console.log('hello')
  }
  
  export const c = 30
  // 每个模块中可以有多次按需导出
  ```

- 导入

  ```js
  import { sayHello } from './result.js'
  import { c as d } from './result.js'	// 按需导入的成员名称必须和按需导出的名称保持一致
  									 // 可以使用 as 关键字进行重命名
  
  sayHello()
  console.log(d)
  ```

  ```js
  // 将所有内容全部导入
  import * as obj from ''
  console.log(obj)
  ```

  ![image-20230201111736614](https://gitee.com/v876774538/my-img/raw/master/image-20230201111736614.png)

#### 1.3 直接导入并执行模块中的代码

如果只是想单纯地执行某个模块中的代码，并不需要得到模块中向外共享的成员，可以直接导入并执行模块代码：

```js
import '模块路径'
```

```js
// 父js文件 module.js
console.log('朝辞白帝彩云间')
import './result.js'
```

```js
// 子js文件 result.js
console.log('千里江陵一日还')
```

![image-20230201112208858](https://gitee.com/v876774538/my-img/raw/master/image-20230201112208858.png)

导入内置模块和第三方模块：

```js
// 内置模块 支持默认导入
import fs from 'fs'

// 内置模块 支持按需导入
import { readFile, writeFile } from 'fs'

// 第三方模块
import dayjs from 'dayjs'
```

## 五、可选链操作符

### 1.概述

可选链操作符（`?.`）允许读取位于连接对象链深处的属性的值而不必明确验证链中的每个引用是否有效。

```js
// 原先引用一个存在嵌套结构的对象obj
let nestedProp = obj.first && obj.first.second	// 需要验证之间的引用
```

`?.`操作符的功能类似于`.`链式操作符。不同之处在于，在**引用为空(null或undefined)的情况下不会引起错误**，该表达式**短路的返回值为undefined**。

当尝试访问可能不存在的对象属性时，可选链操作符将会使表达更简明：

```js
const myInfo = {
	name: 'sjy',
	age: 24,
}
console.log(myInfo?.name)	// sjy
console.log(myInfo.school?.name)	// undefined
```

### 2.语法

```js
obj?.prop	// 对象
obj?.[expr]
arr?.[index]	// 数组
func?.(args)	// 函数
```

**可选链与函数调用：**

当尝试调用一个可能不存在的方法时也可以使用可选链。比如，当使用一个API方法可能不可用（实现版本问题/用户设备不支持等）时。函数调用时若方法不存在，可选链可以使表达式自动返回undefined而不是抛出异常。

```js
let result = someInterface.customMethod?.()
```

> 注意: 如果 someInterface 自身是 null 或者 undefined ，异常 TypeError 仍会被抛出 someInterface is null 如果你希望允许 someInterface 也为 null 或者 undefined ，那么你需要像这样写 `someInterface?.customMethod?.()`

**处理可选的回调函数或者事件处理器：**

```js
//  ES2019的写法
function doSomething(onContent, onError) {
  try {
    // ... do something with the data
  }
  catch (err) {
    if (onError) { // 校验onError是否真的存在
      onError(err.message);
    }
  }
}
```

```js
// 使用可选链进行函数调用
function doSomething(onContent, onError) {
  try {
   // ... do something with the data
  }
  catch (err) {
    onError?.(err.message); // 如果onError是undefined也不会有异常
  }
}
```

**可选链访问数组元素：**

```js
let arrayItem = arr?.[42];
```

> 注意：可选链不能用于赋值！！！

```js
let object = {};
object?.property = 1; // Uncaught SyntaxError: Invalid left-hand side in assignment
```

## 六、动态import

**import.html**

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>动态import</title>
    </head>
    <body>
        <script type="module" src="./js/import.js"></script>
        <button id="btn">获取元素</button>
    </body>
</html>
```

**import.js**

```js
// 获取元素
const btn = document.getElementById('btn')

btn.onclick = function () {
    // 动态引入
    import('./hello.js').then((module) => {
        module.hello()
    })
}
```

**hello.js**

```js
export function hello () {
    console.log('hello')
}
```

![image-20230202152310210](https://gitee.com/v876774538/my-img/raw/master/image-20230202152310210.png)

## 七、BigInt类型

### 1.概述

在js中，存在7种原始值，分别是：`boolean、null、undefined、number、string、symbol、bigint`。

```js
console.log(999999999999999);  //=>10000000000000000
// js中number类型只能安全的表示-9007199254740991(-(2^53-1))和
// 9007199254740991（(2^53-1)） 任何超出此范围的整数值都可能失去精度。
```

BigInt是一种新的数据类型，用于当整数值大于Number数据类型支持范围时使用。这种数据类型允许我们安全地对大整数执行算数操作，比如表示**高分辨率的时间戳**，使用**大整数id**等等而无需使用库。

### 2.使用

1. 在整数末尾追加n

   ```js
   console.log( 9007199254740995n );    // → 9007199254740995n	
   console.log( 9007199254740995 );     // → 9007199254740996
   ```

2. 调用BigInt()构造函数

   ```js
   BigInt("9007199254740995");    // → 9007199254740995n
   ```

3. 其他

   ```js
   10n + 20n;    // → 30n	
   10n - 20n;    // → -10n	
   +10n;         // → 报错 TypeError: Cannot convert a BigInt value to a number	
   -10n;         // → -10n	
   10n * 20n;    // → 200n	
   20n / 10n;    // → 2n	
   23n % 10n;    // → 3n	
   10n ** 3n;    // → 1000n	
   9007199254740992 === 9007199254740993;    // → true 居然是true!
   10 + 10n;	  // → TypeError: Cannot mix BigInt and other types 
   ```

   > 注意：
   >
   > - BigInt不支持一元加号运算符；
   > - 不允许在BigInt和Number之间进行混合操作。

## 八、绝对全局对象globalThis

`globalthis` 始终指向全局对象，如果需要对全局对象进行操作，直接调用 `globalthis`。

```js
console.log(globalThis)
```

![image-20230202160157455](https://gitee.com/v876774538/my-img/raw/master/image-20230202160157455.png)