# Promise介绍与基本使用

## 一、介绍

### 1.理解

#### 1.1 抽象表达

1. Promise是一门新的技术（ES6规范）；

2. Promise是Js中进行**异步编程**的**新解决方案**。

   > 异步编程：
   >
   > - fs文件操作
   >
   >   `require('fs').readFile('./index.html', (err, data)=>{})` 不使用promise，采用回调函数
   >
   > - 数据库操作
   >
   > - AJAX
   >
   >   `$.get('/server',(data)=>{})`
   >
   > - 定时器

#### 1.2 具体表达

1. 从语法来说，Promise是一个构造函数；
2. 从功能来说，Promise对象用来**封装一个异步操作，并可以获取其成功/失败的结果值**。

### 2.意义

1. 指定回调函数的方式更加灵活

   - 旧：必须在启动异步任务前指定；

   - promise：启动异步任务 => 返回promise对象 => 给promise对象绑定回调函数。

2. 支持链式调用，可以解决**回调地狱**的问题

   - 回调地狱：回调函数嵌套调用，外部回调函数异步执行的结果是嵌套的回调执行的条件

     ```js
     var fs = require('fs')
     
     fs.readFile('./src/a.txt', 'utf-8', function(err, data) {
         if (err) {
             throw err
         }
         console.log(data)
         fs.readFile('./src/b.txt', 'utf-8', function(err, data) {
             if (err) {
                 throw err
             }
             console.log(data)
             fs.readFile('./src/c.txt', 'utf-8', function(err, data) {
                 if (err) {
                     throw err
                 }
                 console.log(data)
             })
         })
     })
     
     ```

   - 回调地狱的缺点：不便于阅读、不便于异常处理

### 3.体验

```js
const p = new Promise((resolve, reject) => {
	setTimeout(() => {
		let n = rand(1, 100);
		// 判断
		if (n <= 30) {
			resolve(n);	// 将promise对象的状态设置为成功
            			// 将n作为参数传递给resolve方法
            			// resolve方法将现有对象转为Promise对象 对象的状态是resolved
		}
		else {
			reject(n);	// 将promise对象的状态设置为失败
            			// 将n作为参数传递给reject
                         // rejected方法将现有对象转为Promise对象 对象的状态是rejected
		}
	}, 1000);
});
// 调用then方法
p.then((value) => {
	console.log('恭喜您中奖了，中奖数字为：' + value);
}, (reason) => {
	console.log('再接再厉，您的号码为：' + reason);
})
```

## 二、实践

### 1.fs读取文件

> **fs模块**是nodejs官方提供的、用来**操作文件**的模块。
>
> 它提供了一系列方法和属性，用来满足用户对文件的操作需求。
>
> 导入：`const fs = require('fs');`
>
> 读取：`fs.readFile(path[, options], callback);`
>
> 写入：`fs.writeFile(file, data[, options], callback)`

```js
const fs = require('fs');	// 导入fs模块

// 回调函数形式
fs.readFile('./resource/content.txt'),(err, data) => {
	// 错误 抛出错误
	if (err) throw err;
	console.log(data.toString());
}

// Promise形式
let p = new Promise((resolve, reject) => {
    fs.readFile('./resource/content.txt', (err, data) => {
        // 出错
        if (err) reject(err);
        // 成功
        resolve(data);
    });
});
// 调用then方法
p.then(value => {
    console.log(value.toString());
}, err => {
    console.log(err);
})
```

封装一个函数mineReadFile读取文件内容：

```js
function mineReadFile(path) {
	return new Promise((resolve, reject) => {
		// 读取文件
		require('fs').readFile(path, (err, data) => {
			// 判断
			if (err) {
				reject(err);
			}
			resolve(data);
		})
	})
}

// 调用
mineReadFile('./resource/content.txt').then(value => {
	console.log(value.toString());
}, err => {
	console.log(err);
})
```

### 2.封装AJAX请求

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AJAX请求</title>
</head>

<body>
    <div class="container">
        <button class="btn">发送AJAX</button>
    </div>
    <script>
        const btn = document.querySelector('.btn');
        btn.addEventListener('click', function () {
            // Promise封装
            const p = new Promise((resolve, reject) => {
                // 1. 创建对象
                const xhr = new XMLHttpRequest();
                // 2. 初始化
                xhr.open('GET', 'https://api.apiopen.top/api/sentences');
                // 3. 发送
                xhr.send();
                // 4. 处理响应结果
                xhr.onreadystatechange = function () {
                    if (xhr.readyState === 4) {
                        // 判断响应状态码 2xx
                        if (xhr.status >= 200 && xhr.status < 300) {
                            // 成功
                            resolve(xhr.response);
                        } else {
                            // 失败
                            reject(xhr.status);
                        }
                    }
                }
            });
            // 调用then方法
            p.then(value => {
                console.log(value);
            }, err => {
                console.warn(err);
            })
        })
    </script>
</body>

</html>
```

封装一个函数发送AJAX请求：

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AJAX请求</title>
</head>

<body>
    <div class="container">
        <button class="btn">发送AJAX</button>
    </div>
    <script>
        const btn = document.querySelector('.btn');
        function sendAJAX(method, url) {
            return new Promise((resolve, reject) => {
                // 1. 创建对象
                const xhr = new XMLHttpRequest();
                // 2. 初始化
                xhr.open(method, url);
                // 3. 发送请求
                xhr.send();
                // 4. 处理响应结果
                xhr.onreadystatechange = function () {
                    if (xhr.readyState === 4) {
                        // 判断响应状态码 2xx
                        if (xhr.status >= 200 && xhr.status < 300) {
                            // 成功
                            resolve(xhr.response);
                        } else {
                            // 失败
                            reject(xhr.status);
                        }
                    }
                }
            })
        }
        btn.addEventListener('click', sendAJAX('GET', 'https://api.apiopen.top/api/sentences').then(value => {
            console.log(value);
        }, err => {
            console.warn(err);
        }));
    </script>
</body>

</html>
```

### 3.util.promisify方法进行promise风格转化

#### 3.1 util.promisify(original)

- original <function>
- 返回：<function>

传入一个遵循常见的**错误优先的回调风格的函数**（即以`(err, value) => ...`回调作为最后一个参数），并**返回一个promise的版本**。

```js
const util = require('util');	// 传入util模块
const fs = require('fs');	// 传入fs模块

// 返回一个新的
const mineReadFile = util.promisify(fs.readFile);
mineReadFile('./resource/content.txt').then((value) => {
	// 使用value
    console.log(value.toString());
})
```

## 三、promise实例对象属性

### 1.promise的状态

指promise实例对象中的一个属性：**PromiseState**

![image-20220505140417704](https://gitee.com/v876774538/my-img/raw/master/image-20220505140417704.png)

- pending：未决定的（初始）
- resolved / fullfilled：成功
- rejected：失败

> 1. pending变为resolved
> 2. pending变为rejected
>
> 只有这2种，且**一个promise对象只能改变一次**。
>
> 无论变为成功还是失败，都会有一个结果数据。
>
> 成功的结果数据一般称为value，失败的结果数据一般称为reason。

### 2.promise对象的值

指实例对象中的另一个属性：**PromiseResult**

保存着异步任务 **成功/失败** 的结果。

## 四、promise的基本流程

![image-20220505141427655](https://gitee.com/v876774538/my-img/raw/master/image-20220505141427655.png)

# Promise API

## 一、Promise构造函数

```js
Promise(excutor){}
```

- executor函数：执行器函数`(resolve, reject) => {}`
- resolve函数：内部定义**成功**时调用的函数，`value => {}`
- reject函数：内部定义**失败**时调用的函数，`reason => {}`

说明：executor会在Promise内部**立即同步调用**，异步操作在执行器中执行。

## 二、Promise API 

### 1.Promise.prototype.then()

Promise实例具有then方法。它的作用是**为Promise实例添加状态改变时的回调函数**。

then方法有两个参数，第一个是成功状态下的回调函数（onResolved），第二个（可选）是失败状态下的回调函数（onRejected）。

### 2.Promise.prototype.catch()

Promise的catch()方法用于指定**发生错误时的回调函数**。如果异步操作抛出错误，状态就会变为rejected，就会调用catch方法指定的回调函数处理错误。另外，then方法指定的回调函数如果运行中抛出错误也会被catch方法捕获。

> 注:虽然then方法的第二个参数也可以定义失败的回调函数，但是建议总是使用catch方法，因为catch还可以捕获到前面then方法执行中的错误。

### 3.Promise.prototype.finally()

finally方法用于指定**不管Promise对象最后状态如何，都会执行的操作**。避免了同样的语句需要在then()和catch()中各写一次。

```js
promise
.then(result => {···})
.catch(error => {···})
.finally(() => {···});
```

finally方法的回调函数不接受任何参数，所以我们没办法知道前面promise的状态。

### 4.Promise.all()

Promise.all方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。Promise.all方法接受一个数组作为参数，p1、p2、p3都是 Promise 实例.

```js
let p1 = new Promise((resolve, reject) => {
    resolve('OK');
})
let p2 = Promise.resolve('Success');
let p3 = Promise.resolve('Oh Yeah');

const result = Promise.all([p1, p2, p3]);

console.log(result);
```

p的状态由p1、p2、p3决定，分成两种情况。

（1）只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。

（2）只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。

> 注意，如果作为参数的 Promise 实例，自己定义了catch方法，那么它一旦被rejected，并不会触发Promise.all()的catch方法。

### 5.Promise.race()

```js
const p = Promise.race([p1, p2, p3]);
```

Promise.race方法同样是将多个 Promise 实例包装成一个新的 Promise 实例。**只要有一个实例率先改变状态，p的状态就跟着改变。**那个率先改变的 Promise 实例的返回值，就传递给p的回调函数。

### 6.Promise.resolve()

Promise.resolve()方法将现有对象转为Promise对象，实例的状态为resolved。

```js
Promise.resolve('foo')
// 等价于
new Promise(resolve => resolve('foo'))`
```

### 7.Promise.reject()

Promise.reject(reason)方法也会返回一个新的 Promise 实例，该实例的状态为rejected。

```js
const p = Promise.reject('出错了');
// 等同于
const p = new Promise((resolve, reject) => reject('出错了'))
```

> 注意，Promise.reject()方法的参数，会原封不动地作为reject的理由，变成后续方法的参数。这一点与Promise.resolve方法不一致。

### 8.Promise.allSettled()

在ES6中推出的Promise实例中，有一个方法叫allSettled()。通过Promise.allSettled()方法可以接收一个数组，并且在数组里面的所有实例都执行完，通过then方法或catch方法对数组里面的实例进行遍历与操作。

```js
// 声明两个Promise对象
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('商品数据 -1')
    }, 1000)
})

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('商品数据 -2')
    }, 1000)
})

let p = Promise.allSettled([p1, p2]).then((res) => {
    console.log(res)
})
```

返回一个**包含resolve内容的数组**：

![image-20230202112644046](https://gitee.com/v876774538/my-img/raw/master/image-20230202112644046.png)

- resolve返回：`{ status: 'fulfilled', value: 'xxx' }`

- reject返回：`{ reason: 'xxx', status: 'rejected'}`

  ![image-20230202113454754](https://gitee.com/v876774538/my-img/raw/master/image-20230202113454754.png)

  > 注意，都在then中返回。

  ![image-20230202113542027](https://gitee.com/v876774538/my-img/raw/master/image-20230202113542027.png)

**allSettled()和all()的区别：**

- 返回的数据不同：all()直接返回一个包裹resolve内容的数组，而allSettled()则返回包裹对象的数组；
- 如果其中一个Promise对象报错，all()将无法继续执行，catch可以捕获到错误的内容，无法获取其他成功的数据；而allSettled()不管有没有报错，都会执行到最后，把所有的Promise实例数据都放入数组中返回。

## 三、Promise关键问题

### 1.如何修改对象状态

#### 1.1 resolve函数

pending=>resolved

```js
let p = new Promise((resolve, reject) => {
	// 1. resolve 函数
	resolve('ok');	// pending => fulfilled(resolved)
})
```

#### 1.2 reject函数

pending=>rejected

```js
let p = new Promise((resolve, reject) => {
	// 2. reject 函数
	resolve('error');	// pending => rejected
})
```

#### 1.3 throw抛出错误

pending=>rejected

```js
let p = new Promise((resolve, reject) => {
	throw 'error';
})
```

### 2.一个promise能否指定多个回调？

```js
let p = new Promise((resolve, reject) => {
	resolve('OK');
})
// 1
p.then(value => {
	console.log(1);
})
// 2
p. then(value => {
	console.log(2);
})
```

![image-20220505160327039](https://gitee.com/v876774538/my-img/raw/master/image-20220505160327039.png)

**当promise改变为对应状态时会调用**。

### 3.promise.then()返回的新promise的结果状态由什么决定？

1. 简单表达：**由then()指定的回调函数的执行结果决定**。

2. 详细表达：

   - 如果抛出异常，新promise状态变为rejected，reason为抛出的异常；

     ```js
     let p = new Promise((resolve, reject) => {
     	resolve('ok');
     })
     // 执行then方法
     let result = p.then(value => {
     	// 抛出错误
     	throw '出了问题'
     }, reason => {
         console.log(111);
         console.warn(reason);
     })
     console.log(result);
     ```

     ![image-20220505162603093](https://gitee.com/v876774538/my-img/raw/master/image-20220505162603093.png)

   - 如果返回的是非promise的任意值，新promise状态变为resolved，value为返回的值；

     ```js
     let p = new Promise((resolve, reject) => {
     	resolve('ok');
     })
     // 执行then方法
     let result = p.then(value => {
     	// 返回结果是非promise对象
     	return value;
     }, reason => {
         console.warn(reason);
     })
     console.log(result);
     ```

     ![image-20220505162953274](https://gitee.com/v876774538/my-img/raw/master/image-20220505162953274.png)

   - 如果返回的是另一个新的promise，此promise的结果就会成为新promise的结果。

     ```js
     let p = new Promise((resolve, reject) => {
         resolve('ok');
     })
     // 执行then方法
     let result = p.then(value => {
         return new Promise((resolve, reject) => {
             resolve('success');
         })
     }, reason => {
         console.warn(reason);
     })
     console.log(result);
     ```

     ![image-20220505163145091](https://gitee.com/v876774538/my-img/raw/master/image-20220505163145091.png)

### 4.promise串联多个操作任务

promise的then()返回的是一个新的promise，可以写成then()的链式调用。

通过**then的链式调用**串联多个同步/异步任务。

```js
let p = new Promise((resolve, reject) => {
	setTimeout(() => {
		resolve('OK');
	}, 1000);
});
p.then(value => {
	return new Promise((resolve, reject) => {
		resolve('success');
	});
}).then(value => {
	console.log(value);	// success
}).then(value => {
	console.log(value);	// undefined // 上一个then没有返回值
})
```

### 5.promise异常穿透

当**使用promise的then链式调用时，可以在最后指定失败的回调**。

前面任何操作出了异常，都会传到最后失败的回调中处理。

```js
let p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('OK');
    }, 1000);
});
p.then(value => {
    return new Promise((resolve, reject) => {
        // resolve('success');
        reject('error');
    });
}).then(value => {
    console.log(value); 
}).then(value => {
    console.log(value); 
}).catch(reason => {
    console.log(111);
    console.warn(reason);
})
```

![image-20220505165059504](https://gitee.com/v876774538/my-img/raw/master/image-20220505165059504.png)

### 6.中断promise链

当使用promise的then链式调用时，在中间中断，不再调用后面的回调函数：**在回调函数中返回一个pending状态的promise对象**。

```js
let p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('OK');
    }, 1000);
});
p.then(value => {
    return new Promise((resolve, reject) => {
        resolve('success');
        // reject('error');
    });
}).then(value => {
    console.log(value); // success
    // 返回一个pending状态的promise对象
    return new Promise(() => {});
}).then(value => {
    console.log(value); // undefined
}).catch(reason => {
    console.log(111);
    console.warn(reason);
})
```

![image-20220505165502377](https://gitee.com/v876774538/my-img/raw/master/image-20220505165502377.png)

# async与await

## 一、async函数

1. 函数的返回值为promise对象
   - return的只要不是promise对象，那么返回的就是成功的promise对象；
   - async函数返回的是error，那么返回的是失败的Promise；
   - async函数返回的是promise对象，则根据这个对象的状态来决定Promise的状态

```js
// 1. 返回值是一个非promise类型的数据
async function main() {
	return 521;
}
```

**返回值为promise对象**

![image-20230130142153937](https://gitee.com/v876774538/my-img/raw/master/image-20230130142153937.png)

```js
// 2. 返回的是一个promise对象
async function main() {
	return new Promise((resolve, reject) => {
		resolve('OK');
	});
}
```

```js
// 3. 抛出异常
async function main() {
	throw 'oh no'
}
```

```js
let result = main();
console.log(result);
```

## 二、await表达式

1. await右侧的表达式一般为promise对象，也可以是其他值
2. 若表达式为promise对象，await返回的是promise成功的值
3. 若表达式是其他值，直接将此值作为await的返回值

```js
// 1. 右侧为promise的情况（成功）
async function main() {
	let p = new Promise((resolve, reject) => {
		resolve('OK');
	})
	let res = await p;
    console.log(res)
}
```

```js
// 2. 右侧为promise的情况（失败）
async function main() {
	let p = new Promise((resolve, reject) => {
		reject('ERROR');
	})
    // 通过try...catch捕获
    try {
        let res2 = await p;
    }
    catch(err) {
        console.log(err)
    }
}
```

```js
// 3. 右侧为其他值
async function main() {
	let res3 = await 20;
	console.log(res3);
}
```

```js
main();
```

## 三、注意

1. await必须写在async函数中，但async函数中可以没有await
2. 若await的promise失败了，就会抛出异常，需要通过try...catch捕获

## 四、async与await结合实践

```js
const fs = require('fs');	// 在js文件中导入文件系统模块
const util = require('util');	// 传入util模块
const mineReadFile = util.promisify(fs.readFile);

// 回调函数的方式
fs.readFile('./resource/1.html', (err, data1) => {
	if (err) {
		throw err;	// 文件读取失败
	}
	fs.readFile('./resource/2.html', (err, data2) => {
		if (err) {
			throw err;
		}
		fs.readFile('./resource/3.html', (err, data3) => {
			if (err) {
				throw err;
			}
			console.log(data1 + data2 + data3)
		})
	})
})

// async与await
async function main() {
    try {
        let data1 = await mineReadFile('./resource/1.html');
    	let data2 = await mineReadFile('./resource/2.html');
    	let data3 = await mineReadFile('./resource/3.html');
    	console.log(data1 + data2 + data3)
    }
	catch(e) {
        console.log(e)
    }
}
```

## 五、async与await结合发送AJAX请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button id="btn">点击获取</button>
    <script>
        function sendAJAX(method, url) {
            return new Promise((resolve, reject) => {
                // 1. 创建对象
                const xhr = new XMLHttpRequest();
                // 2. 初始化
                xhr.open(method, url);
                // 3. 发送请求
                xhr.send();
                // 4. 处理响应结果
                xhr.onreadystatechange = function () {
                    if (xhr.readyState === 4) {
                        // 判断响应状态码 2xx
                        if (xhr.status >= 200 && xhr.status < 300) {
                            // 成功
                            resolve(xhr.response);
                        } else {
                            // 失败
                            reject(xhr.status);
                        }
                    }
                }
            })
        }

        // 段子接口地址 https://api.apiopen.top/getJoke
        let btn = document.querySelector('#btn')
        btn.addEventListener('click', async function() {
            // 获取段子信息
            let msg = await sendAJAX('get', 'https://api.apiopen.top/getJoke')
            console.log(msg)
        })
    </script>
</body>
</html>
```

## 六、promise与async的区别

1. 执行async函数返回的都是Promise对象；
2. Promise.then成功的情况下对应async中的await；
3. Promise.catch异常的情况下对应async中的try catch；
4. async/await更符合同步语义，使得异步代码更像是同步代码；
5. async/await是基于promise实现的；
6. async/await是生成器函数的语法糖，拥有内置执行器，不需要额外调用，直接回自动调用并返回一个promise对象。

# Axios的理解和使用

## 一、Json-server

### 1.安装

全局安装json-server

```
npm install -g json-server
```

查看版本号

```
npm json-server -v
```

### 2.创建db.json

```json
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```

### 3.启动

终端-cmd

```
json-server --watch db.json
```

![image-20220422171022712](https://gitee.com/v876774538/my-img/raw/master/image-20220422171022712.png)

## 二、axios介绍与页面配置

### 1.特点

1. 基于 xhr + promise 的异步 ajax 请求库；
2. 浏览器端/node 端都可以使用；
3. 支持请求／响应拦截器；
4. 支持请求取消；
5. 请求/响应数据转换；
6. 批量发送多个请求。

### 2.安装

1. 使用npm：

   ```
   npm install axios
   ```

2. 使用CDN:

   ```js
   <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.26.1/axios.js"></script>
   ```

## 三、基本使用

### 1.通用方法

1. `axios(config)`: `通用/最本质`的发任意类型请求的方式。

   > 基本框架：给 axios() 函数传入一个配置对象，该对象中包含 method、url、data 等配置项，具体配置规则可以参考其GitHub官网的文档描述。
   >
   > axios 是基于Promise的， axios() 函数的返回值就是一个Promise类型的对象，所以可以直接在 axios() 函数后跟上 then() 函数来处理请求结果。

   - 增：POST
   - 删：DELETE
   - 改：PUT
   - 查：GET

2. `axios(url[, config])`: 可以只指定 url 发 get 请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>axios基本使用</title>
    <script src="https://cdn.bootcdn.net/ajax/libs/axios/0.26.1/axios.js"></script>
</head>
<body>
    <div class="container">
        <h2>基本使用</h2>
        <button>发送GET请求</button>
        <button>发送POST请求</button>
        <button>发送PUT请求</button>
        <button>发送DELETE请求</button>
    </div>
    <script>
        const btns = document.querySelectorAll('button');

        // 获取数据（查）
        btns[0].onclick = function() {
            // 发送AJAX请求
            axios({
                // 请求类型
                method: 'GET',
                // URL
                url: 'http://localhost:3000/posts'
            }).then(response => {
                console.log(response);
            })
        }
        // 追加新数据（增）
        btns[1].onclick = function() {
            // 发送AJAX请求
            axios({
                // 请求类型
                method: 'POST',
                // URL
                url: 'http://localhost:3000/posts',
                // 设置请求体
                data: {
                    title: '下班倒计时！',
                    author: '张三'
                }
            }).then(response => {
                console.log(response);
            })
        }
        // 更新数据（改）
        btns[2].onclick = function() {
            // 发送AJAX请求
            axios({
                // 请求类型
                method: 'PUT',
                // URL
                url: 'http://localhost:3000/posts/1',
                // 设置请求体
                data: {
                    title: '更新更新更新',
                    author: '张三'
                }
            }).then(response => {
                console.log(response);
            })
        }
        // 删除数据（删）
        btns[3].onclick = function() {
            // 发送AJAX请求
            axios({
                // 请求类型
                method: 'DELETE',
                // URL
                url: 'http://localhost:3000/posts/1',
            }).then(response => {
                console.log(response);
            })
        }
    </script>
</body>
</html>
```

### 2.使用对象上的方法发送请求

1. `axios.request(config)`: 等同于axios(config)
2. `axios.get(url[, config])`: 发get请求
3. `axios.delete(url[, config])`: 发delete请求
4. `axios.post(url[, data, config])`: 发post请求
5. `axios.put(url[, data, config])`: 发put请求

```js
//发送 GET 请求
axios.request({
  // 设置请求方法（请求行信息）
  method:'GET',
  // 设置请求的目标url（请求行信息）
  url: 'http://localhost:3000/comments'
}).then(response => {
  console.log(response);
})

//发送 POST 请求
axios.post(
  // 设置请求的目标url（请求行信息）
  'http://localhost:3000/comments',
  // 要带给服务端的数据
  {
    "body": "喜大普奔",
    "postId": 2
  }).then(response => {
  console.log(response);
})

......

```

### 3.axios请求响应结果结构

```json
// {data: Array(1), status: 200, statusText: "OK", headers: {…}, config: {…}, …}
data: [{…}]
status: 200
statusText: "OK"
headers: {cache-control: "no-cache", 
          content-length: "68", 
          content-type: "application/json; charset=utf-8", 
          expires: "-1", pragma: "no-cache"
          }
config: {url: "http://localhost:3000/comments", 
  		method: "get", 
    	headers: {…},
        data: undefined,
      	transformRequest: Array(1), 
        transformResponse: Array(1), 
        …}
request: XMLHttpRequest {
  		readyState: 4, 
        timeout: 0, 
        withCredentials: false, 
        upload: XMLHttpRequestUpload, 
        onreadystatechange: ƒ, 
        …}
```

![image-20220422180344972](https://gitee.com/v876774538/my-img/raw/master/image-20220422180344972.png)

1. `data`：服务端返回的具体，也就是**响应体**。它是一个数组，里面根据客户端发送的请求会保存若干个对象，本来应该是json格式的字符串，但是axios自动将其转换为了相应的对象类型以便我们处理数据。
2. `status`：响应状态码，而statusText是对应的响应状态字符串。
3. `headers` 响应头。
4. `config`：我们所发送的请求的相关配置，包括请求行、请求头和请求体等信息。
5. `request`：axios根据我们所发送的请求所生成的XMLHttpRequest实例对象（其实axios底层也是对原生 XMLHttpRequest 的封装）。

### 4.axios配置对象详细说明

上面我们提到了`config`这个参数`config`是一个配置对象，该对象中包含许多配置项，我们可以通过设置这些配置项的值来发送我们想要的请求。

1. `url`：【字符串】设置我们想要请求的**目标资源的地址**；
2. `method`：【字符串】设置**请求方法**，默认为GET；
3. `baseURL`:【字符串】设置资源的**基础路径**，一般与url配合使用。比如，我们想要向`http://localhost:3000/comments`这个地址发送请求，我们就可以事先设置baseURL为`http://localhost:3000`，然后发送请求时设置url为`/comments`；
4. `headers`：【对象】设置**请求头**信息；
5. `data`：【对象/字符串】设置**请求体**，即我们想要向服务端发送的数据；
6. `params`：【对象】设置跟在url后的**参数**。如，我们设置params:{a:100, b:200}，那么在发送请求时，Axios将自动在url参数后面添加`?a=100&b=200`；
7. `timeout`：【整数（单位：毫秒）】设置**超时时间**。若超过这个时间还未收到响应，则取消这个请求。默认为0，不考虑超时；
8. `responseType`：【字符串】设置响应体的格式。默认为json，即默认收到的响应体内容转换为json格式，然后客户端将自动对该结果进行转换。可选项有`arraybuffer`，`document`，`json`，`text`，`stream`；
9. `responseEncoding`：设置响应体的编码格式，默认为uft8；
10. `withCredentials`：【布尔值】在跨域请求时设置是否携带cookie信息，true表示携带，默认为false；
11. `maxContentLength`和`maxBodyLength`：【整数（单位：字节）】maxContentLength用于设置HTTP响应体的最大尺寸；maxBodyLength用于设置HTTP请求体的最大尺寸。注意，这两个配置只能在Node.js环境下使用；
12. `proxy`：【对象】设置**代理**，一般用于服务器（Node.js）；
13. `cancelToken`：指定某个cancel token用于取消某个请求；
14. `adapter`：【函数】用于指定发送请求时的适配器（xhrAdapter或httpAdapter）；
15. `decompress`：【布尔值】设置是否对响应结果进行解压。默认为true。注意，该配置仅能在Node.js环境下使用；
16. `xsrfCookieName`和`xsrfHeaderName`：【字符串】一种安全设置，保证请求来自我们自己的客户端。需要和服务器的相关设置配合，可以有效地避免跨站攻击；
17. `validateStatus`：【函数】设置判断当前请求的响应是否有效（**是否成功**）的规则。传入响应状态码status作为参数，返回一个布尔值。默认规则为：**return status >= 200 && status < 300**；
18. `transformRequest`：【数组】允许我们将请求的数据进行一番处理，再将处理后的结果发送给服务端。它是一个数组，数组中的元素是函数类型的，我们可以将请求的数据data和请求头headers作为参数传入，并最后返回一个处理过的data；
19. `transformResponse`：【数组】允许我们将来自服务器的响应数据进行一番处理，再将处理后的结果传递给后续的then()或catch()函数。它也是一个数组，数组中的元素也是函数类型的。我们可以将得到的响应数据data作为参数传入并最后返回一个处理过的data；
20. `onUploadProgress`和`onDownloadProgress`：【函数】分别设置上传和下载的回调。

### 5.axios默认配置

我们可以通过 `axios.defaults.xxx` 的方式设置一些可能会重复用到的配置项来让某个配置项拥有某个默认值，这样在后续使用该配置项时就可以省去重复配置的操作。

其中，xxx可以是上面提到的config中的任意一个配置项。

```js
// 默认配置
axios.defaults.method = 'GET';	// 设置默认的请求类型为 GET
axios.defaults.baseURL = 'http://localhost:3000';	// 设置默认的基础 URL
axios.defaults.timeout = 3000;	// 设置默认的超时时间
......
```

### 6.axios创建实例对象

我们可以通过`axios.create(config)`函数创建一个拥有指定配置的新axios对象（假设对象名为 miniAxios）。

这个 miniAxios 的功能和原本的 axios 的功能几乎一样，唯一不同的地方就在于这个新axios对象没有取消请求和批量发请求的方法。miniAxios 是函数类型的，其返回结果也是一个 Promise 类型的对象。我们可以像之前使用原本的axios 时那样通过传入 config 配置对象来发送指定的AJAX请求：`miniAxios(config)`，也可以通过`miniAxios.xxx()`的方式发送请求。

```js
const miniAxios = axios.create({
  baseURL: 'https://api.apiopen.top',
  timeout: 2000
});

const anotherAxios = axios.create({
  baseURL: 'https://www.other.com',
  timeout: 3000
});
// miniAxios 与 axios 对象的功能几乎是一样的
miniAxios({
  method: 'GET',
  url: '/getJoke',
}).then(response => {
  console.log(response);
});
// 下面这段代码和上面那段是等效的
miniAxios.get('/getJoke').then(response => {
  console.log(response.data)
})
```

应用场景：当我们需要向两台不同域名的服务器发送请求时，如果用原本的 axios ，我们只能设置默认配置时只能针对其中一个服务器，而如果通过 axios.create(config) 函数创建一个拥有指定配置的新 axios 对象，我们就可以针对不同域名的服务器设置相应的默认配置，比如上面的 miniAxios 和 anotherAxios。

### 7.axios拦截器（Interceptors）

#### 7.1 请求拦截器 axios.interceptors.request

![image-20220424104837981](https://gitee.com/v876774538/my-img/raw/master/image-20220424104837981.png)

请求拦截器是在AJAX请求被发送之前对该请求先做层层处理后再发送给服务端。

```js
// 设置请求拦截器
axios.interceptors.request.use(function(config) {
	// 在发送请求之前做些什么
    ...
	return config;
}), function(error) {
	// 对错误请求做些什么
    ...
	return Promise.reject(error);
}
```

我们可以通过多次像上面那样调用 `use()` 函数来为请求添加多个请求拦截器。

其中，`config` 参数就是我们想要发送的AJAX的配置对象，其中有我们上面提到的各种配置项可供我们设置。

#### 7.2 响应拦截器 axios.interceptors.response

![image-20220424104918151](https://gitee.com/v876774538/my-img/raw/master/image-20220424104918151.png)

响应拦截器则是把从服务端返回的响应结果进行层层处理后再交给客户端。

```js
// 设置响应拦截器
axios.interceptors.response.use(function(response) {
	// 响应成功做什么
	...
	return response.data;
}, function(error) {
    // 响应失败做什么
	...
	return Promise.reject(error);
})
```

#### 7.3 案例

```js
/**
*  添加请求拦截器
*/
axios.interceptors.request.use(function (config) {
// 在发送请求之前做些什么
const tokenStr = localStorage.getItem('token');
// 若本地有token 给它加上请求头
if (tokenStr) {
  config.headers.Authorization = 'Bearer ' + localStorage.getItem('token');
}
//如果不是get提交。那么就要加锁，防止表单提交
return config
}, function (error) {
// 对请求错误做些什么
return Promise.reject(error)
})

/**
* 添加响应拦截器
*/
axios.interceptors.response.use(res => {
return res.data
}, function (error) {
console.log(error.response)
if (error.response != undefined && ((error.response.data.code === 'B0301') || (error.response.data.code === 'A0307'))) {
  localStorage.removeItem('accessToken')
  localStorage.removeItem('token')
  localStorage.removeItem('grade')
  localStorage.removeItem('payContent')
  localStorage.removeItem('balance')
  _val.$bus.$emit('loginBus')
  localStorage.setItem('cacheAddress',window.location.href) //前往登录时，缓存地址
  switch (error.response.data.code) {
    case 'B0301':
      _val.$Modal.confirm({
        title:'当前登录会话过期，请重新登录',
        content:'是否前往登录',
        onOk() {
          router.push({
            path: '/Login'
          })
        }
      });
      break;
    case 'A0307':
      _val.$Modal.confirm({
        title:'请登录后再查看',
        content:'是否前往登录',
        onOk() {
          router.push({
            path: '/Login'
          })
        }
      });
      break;
  }
  return;
}
if (error.response) {
  if (error.response.status == 500) {
    // _val.$Message.info("【" + error.response.status + "】请求出错了" + JSON.stringify(error.response.data.message));
    var str = JSON.stringify(error.response.data.message);
    _val.$Message.error(str.substring(1, str.length-1));
  } else {
    _val.$Message.error("【" + error.response.status + "】请求出错了" + JSON.stringify(error.response.data));
  }
} else {
  _val.$Message.error("请求出错了：" + error.message)
}
return Promise.reject(error)
})
```

### 8.axios取消请求

在通过 `axios` 发送请求时，我们可以通过此前提到的 `config` 中的 `cancelToken` 配置项与一个全局变量的配合来完成取消某个请求的操作。

```js
// 获取按钮
const btns = document.querySelectorAll('button');
2. 声明全局变量
let cancel = null;
// 发送请求
btns[0].onclick = function() {
    // 检测上一次请求是否已经完成
    // 防抖
    if (cancel != null) {	// 上一次请求还没结束
        // 取消上一次请求
        cancel();
    }
	axios({
		method:'GET',
		url:'http://localhost:3000/posts',
		// 1. 添加配置对象的属性
		cancelToken: new axios.CancelToken(function(c) {
			// 3. 将c的值赋值给cancel
			cancel = c;
		})
	}).then(response => {
        console.log(response);
        // cancel重置 初始化
        cancel = null;
    })
}
// 取消请求
btns[1].onclick = function() {
	cancel();
}
```

## 四、Vue的axios封装

### 1.安装

```
npm install axios
```

### 2.请求封装

**require.js**

```js
import axios from 'axios'
import qs from 'qs'
import baseUrl from './env.js'
import router from '../router'

const install = function (Vue) {
  const _val = new Vue()
  // axios.defaults.withCredentials = true
  /**
   *  添加请求拦截器
   */
  axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    ...
    return config
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error)
  })

  /**
   * 添加响应拦截器
   */
  axios.interceptors.response.use(res => {
    ...
    return res.data
  }, function (error) {
    ...
    return Promise.reject(error)
  })

  let service = function (method, url, data) {
    let option = {
      method: method ? method : 'POST',
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
        // 'Content-Type': 'multipart/form-data',
      },
      data: qs.stringify(data),
      // data: data,
      url: baseUrl + url,
      timeout: 60000
    }
    return axios(option)
  }
  //请求参数为json（Array(),[]）
  let service1 = function (method, url, data) {
    let option = {
      method: method,
      headers: {
        // 'Content-Type': 'application/x-www-form-urlencoded',
        'Content-Type': 'application/json',
      },
      dataType: 'json',
      data: data,
      // data: data,
      url: baseUrl + url,
      // timeout: 60000
      timeout: 1800000
    }
    return axios(option)
  }
  let service2 = function (method, url, data) {
    let option = {
      method: method ? method : 'POST',
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
        // 'Content-Type': 'multipart/form-data',
      },
      params: (data),
      // data: data,
      url: baseUrl + url,
      timeout: 60000
    }
    return axios(option)
  }

  //下载文档
  let exportService = function (method, url, data) {
    let option = {
      method: method ? method : 'POST',
      responseType: 'blob',
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
        // 'Content-Type': 'application/json',
      },
      dataType: 'json',
      data: qs.stringify(data),
      // data: data,
      url: baseUrl + url,
      timeout: 15000
    }
    return axios(option)
  }

  // 在vue全局中使用axios
  Vue.prototype.$http = service
  Vue.prototype.$http1 = service1
  Vue.prototype.$http2 = service2
  Vue.prototype.$exportService = exportService
}
export default install
```

### 3.api的统一管理

**api.js**

```js
const APIURL = {
  //登录模块
  register:'/userInfo/register',// 注册
  loginApi:'/loginApi',// 登录-密码
  loginCodeApi:'/loginCodeApi',// 登录-验证码
  getCode:'/verificationCode/getCode',// 获取短信验证码
  forgetPwd:'/userInfo/forgetPwd',// 忘记密码
  getCurrentLoginUserInfo:'/userInfo/getCurrentLoginUserInfo',// 用户信息
  ...
}
export default APIURL
```

### 4.环境切换

**env.js**

```js
const host = window.location.host
let baseUrl = ''

if (host === 'localhost:8900') {
  baseUrl = '/api'  //测试
} else {
  // baseUrl = 'http://192.168.0.154:9501/appApi'  //本地  
  // baseUrl = 'http://47.111.73.151:9501/appApi'  // 服务器
  baseUrl = 'http://ys.syy333.com/appApi'  // 测试
  // baseUrl = 'https://www.93114.com/appApi'  //生产
}
export default baseUrl
```

