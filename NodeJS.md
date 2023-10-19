# NodeJS

## 一、命令行窗口

1. 开始菜单（Win + R） --> 运行 --> CMD --> 回车

2. 常用指令：

   - dir：列出当前目录下的所有文件；
   - cd 目录名：进入到指定目录

3. 目录：

   - .：当前目录
   - ..： 表示上一级目录

4. 环境变量（Windows系统中变量）：

   ![image-20230202164615721](https://gitee.com/v876774538/my-img/raw/master/image-20230202164615721.png)

   > 当我们在命令行窗口打开一个文件，或调用一个程序时，系统会首先在当前目录下寻找文件程序，找到了就直接打开，否则会依次到环境变量path路径中寻找。
   >
   > 因此我们可以将一些经常需要访问的程序和文件的路径添加到path中，以便在任意位置访问这些文件和程序。

## 二、进程和线程

1. 进程

   > 进程负责为程序的运行提供必备的环境。
   >
   > 进程相当于工厂中的车间。

   ![image-20230202165617042](https://gitee.com/v876774538/my-img/raw/master/image-20230202165617042.png)

2. 线程

   > 线程是计算机中的最小的计算单位，线程负责**执行进程中的程序**。
   >
   > 线程就相当于工厂中的工人。

3. 单线程

   JS是单线程的。

4. 多线程

## 三、Node.js简介

### 1.概述

> Node.js是一个能在**服务器端**运行JavaScript的开放源代码、跨平台**JavaScript运行环境**。

Node采用Google开发的V8引擎运行js代码，使用**事件驱动**、**非阻塞**和**异步I/O模型**等技术提高性能，可优化应用程序的传输量和规模。

Node大部分基本模块都采用JavaScript编写。在Node出现之前，Js通常作为**客户端程序设计语言**使用，以js写出的程序常在用户的浏览器上运行。（前端）

> 传统的服务器都是多线程的，即每进来一个请求，就创建一个线程去处理请求；而Node服务器是单线程的，但是在后台拥有一个I/O线程池。

### 2.用途

- Web服务API，比如REST
- 实时多人游戏
- 后端的Web服务，例如跨域、服务端的请求
- 基于Web的应用
- 多客户端的通信，如即时通信

### 3.node执行js文件

进入目录：

```
node xxx.js
```

## 四、Node.js模块化

### 1.module简介

Node.js遵循的是**CommonJS模块规范**：

- 导出模块：`exports 导出模块` / `module.exports 导出模块 `

  ```js
  // exports
  // 暴露属性
  exports.x = 100
  exports.y = 200
  
  // 暴露方法
  exports.fn = function() {
      console.log('1111')
  }	// exports只能通过使用.的形式来向外暴露内部变量
  
  // module.exports
  // 写法1
  var x = 100
  var y = 200
  module.exports.x = x
  module.exports.y = y
  
  // 写法2
  module.exports = {
      x,
      y
  }
  
  console.log(module.exports == exports)	// true 实际上指向的是同一个对象
  ```

- 导入模块：`require("模块标识")`

  ```js
  require('./hello.js')
  ```

  接收require返回值：

  ```js
  var md = require('./hello.js')
  // 使用require()引入模块后，该函数会返回一个对象，代表引入的模块
  ```

  我们可以通过`md.变量`访问另一个文件向外暴露的对象。

  > **模块的基本分类：**
  >
  > - 核心模块：由node引擎提供的模块
  > - 文件模块：由用户自己创建的模块
  >
  > 核心模块的模块标识就是模块的名字（如，fs），文件模块的标识是文件的路径（绝对/相对路径）。

**举例：**

```js
var x = 5;
var addX = function(value) {
	return value + x;
};
module.exports.x = x;
module.exports.addX = addX;
```

通过`module.exports`对象，定义对外接口，输出变量`x`和函数`addX`。`module.exports`对象是可以被其他文件导入的，它其实就是文件内部与外部通信的桥梁。

`require`方法用于在其他文件加载这个接口：

```js
var example = require('./example.js');
console.log(example.x); // 5
console.log(example.addX(1)); // 6
```

**CommonJS模块特点：**

- 所有代码都运行在模块作用域，**不会污染全局作用域**。
- 模块可以多次加载，但是只会在`第一次加载时运行一次`，然后运行`结果就被缓存`了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须`清除缓存`。
- 模块加载的顺序，按照其在代码中出现的顺序。

### 2.module对象

每个模块内部，都有一个module对象，代表**当前模块**。包含以下属性：

- `module.id` 模块的识别符，通常是带有绝对路径的模块文件名；
- `module.filename` 模块的文件名，带有绝对路径；
- `module.loaded` 返回一个布尔值，表示模块是否已经完成加载；
- `module.parent` 返回一个对象，表示调用该模块的模块；
- `module.children` 返回一个数组，表示该模块要用到的其他模块。

下面是一个示例文件，最后一行输出module变量。

### 3.global对象

node中没有window，但拥有一个**全局对象global**，作用就和网页中的window类似。

- 在全局中创建的变量都会作为global的属性保存；
- 在全局中创建的函数都会作为global的方法保存。

```js
var a = 10
b = 100
console.log(global.a)	// undefined
console.log(global.b)	// 100
```

## 五、package 包

### 1.包简介

CommonJS的包规范允许我们将一组相关的模块组合到一起，形成一组完整的工具。CommonJS的包规范由**包结构**和**包描述文件**两个部分组成：

- 包结构：用于组织包中的各种文件；
- 包描述文件：描述包的相关信息，以供外部读取分析

#### 1.1 包结构

包实际上就是一个压缩文件，解压以后还原为目录。符合规范的目录，应该包含如下文件：

- `package.json` 描述文件（**必须**）
- `bin` 可执行二进制文件
- `lib` （library）js代码
- `doc` 文档
- `test` 单元测试

#### 1.2 包描述文件

包描述文件（`package.json`）用于表达非代码相关的信息，它是一个JSON格式的文件，位于包的根目录下，是包的重要组成部分。

| 字段                         | 说明                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| name                         | 项目/模块名称。<br>长度必须小于等于214个字符，不能以"."(点)或者"_"(下划线)开头，不能包含大写字母。 |
| version                      | 项目版本。                                                   |
| description                  | 项目描述。字符串。方便人们使用`npm search`找到这个包。       |
| keywords                     | 项目关键字。字符串数组。方便人们使用`npm search`找到这个包。 |
| private                      | 是否私有。设置为true时，npm拒绝发布。                        |
| license                      | 软件授权条款。                                               |
| bugs                         | bug提交地址。                                                |
| author                       | 包作者。                                                     |
| contributors                 | 项目其他贡献者。                                             |
| repository                   | 项目仓库地址.                                                |
| homepage                     | 项目包的官网URL                                              |
| repository                   | 项目仓库地址。                                               |
| dependencies/devDependencies | 生产/开发环境依赖包列表，通过`npm install`命令，它们将被安装在`node_module`目录下。 |
| main                         | 字段制定了程序的主入口文件。                                 |
| bin                          | 内部命令对应的可执行文件的路径。                             |
| scripts                      | 执行npm脚本命令简写。                                        |
| ...                          | ...                                                          |

### 2.npm 包管理器

`NPM(Node Package Manager/Node包管理器)`。对于Node而言，NPM帮助其完成了**第三方模块的发布、安装和依赖**等。借助NPM，Node与第三方模块之间形成了一个很好的生态系统。

#### 2.1 npm命令

- `npm -v` 查看版本
- `npm` 帮助说明
- `npm search 包名` 搜索模块包
- `npm install 包名` 在当前目录安装包
- `npm install 包名 -g` 全局模式安装包
- `npm install 包名 --save` 安装并添加到描述文件的依赖(dependencies)中记录下来
- `npm remove 包名` 删除包

### 3.cnpm 配置

阿里定制的cnpm命令行工具代替默认的npm，安装：

```
npm install -g cnpm --registry=http://registry.npmmirror.com
```

检查是否安装成功：

```
cnpm -v
```

### 4.node搜索包流程

通过npm下载的包都会放到`node_modules`文件夹中，通过npm下载的第三方包，直接通过包名引入即可。

node在使用模块名字来引入模块时，会首先在当前目录的`node_modules`中寻找是否含有该模块，如果有则使用，反之进入上一级目录的`node_modules`中寻找，以此类推，直到找到为止……若找到磁盘根部仍未找到，则报错。

## 六、Buffer缓冲区

> node.js Buffer（缓冲）中文文档地址：https://www.nodeapp.cn/buffer.html

### 1.Buffer的用处

JavaScript语言没有二进制数据类型，但在处理像TCP流或文件流时，必须使用到二进制数据。因此在Node.js中，定义了一个Buffer类，该类用来创建一个**专门存放二进制数据的缓冲区**。

### 2.Buffer与字符编码

Node.js目前支持的字符编码包括：

| 编码格式   | 支持                                                         |
| ---------- | ------------------------------------------------------------ |
| **ascii**  | 仅支持 7 位 ASCII 数据。如果设置去掉高位的话，这种编码是非常快的。 |
| **utf8**   | 多字节编码的 Unicode 字符。许多网页和其他文档格式都使用 UTF-8 。 |
| utf16le    | 2 或 4 个字节，小字节序编码的 Unicode 字符。支持代理对（U+10000 至 U+10FFFF）。 |
| ucs2       | utf16le 的别名。                                             |
| **base64** | Base64 编码。                                                |
| latin1     | 一种把 Buffer 编码成一字节编码的字符串的方式。               |
| binary     | latin1 的别名。                                              |
| hex        | 将每个字节编码为两个十六进制字符。                           |

### 3.创建Buffer类

1. `Buffer.from(string[, encoding])`

   - string <string>：需要编码的字符串
   - encoding <string>：字符编码方式，默认utf-8

   ```js
   let buff=Buffer.from("a","ascii");
   console.log(buff);	// <Buffer 61>
   				   // buffer中存储的都是二进制数据，但是在计算机显示时以16进制显示
   console.log(buff.length)	// 1	// 占用内存的大小 byte（字节）
   console.log(buff.toString());	// a
   ```

2. `Buffer.alloc(size[, fill[, encoding]])`

   - size <integer>：新建的Buffer的期望长度；
   - fill <string> | <Buffer> | <integer>：用来预填充新建的Buffer的值，默认为0（默认初始值）；
   - encoding <string>：若fill为字符串，则该值为它的字符编码方式

   分配一个大小为`size`字节的新建的`Buffer`。若`fill`为`undefined`，则该`Buffer`会以`0`填充。

   ```js
   const buf = Buffer.alloc(5);
   console.log(buf);	// <Buffer 00 00 00 00 00>
   
   // 通过索引来操作buf中的元素
   buf[0] = 88;
   buf[1] = 255;
   buf[2] = 0xaa;
   console.log(buf);	// <Buffer 58 ff aa 00 00 00 00 00 00 00>
   buf[5] = 11;
   console.log(buf);	// <Buffer 58 ff aa 00 00 00 00 00 00 00>
   				   // 超出范围
   				   // alloc在内存中申请了5个连续的内存空间，Buffer的大小一旦确定，就不能再修改
   				   // Buffer实际上是对底层内存的直接操作
   buf[3] = 556;
   console.log(buf)	// <Buffer 58 ff aa 2c 00 00 00 00 00 00>
   				   // 超出数值范围！（八进制00-ff 二进制00000000-ffffffff 十进制0-255）
   				   // 1000101100 → 取后八位00101100
   ```

   > 注意：如果size的大小大于`buffer.constans.MAX_LENGTH`**`(2^31)-1` (~2GB)**或小于0，会抛出`RangeError`错误。如果size为0，则创建一个长度为0的Buffer。

3. `Buffer.allocUnsafe(size)`

   - size <integer>：新建的Buffer的期望长度

   以这种方式创建的 `Buffer` 实例的底层内存是**未初始化**的（不清空数据）。 新创建的 `Buffer` 的内容是未知的，且**可能包含敏感数据**。 可以使用 [`buf.fill(0)`](https://www.nodeapp.cn/buffer.html#buffer_buf_fill_value_offset_end_encoding) 初始化 `Buffer` 实例为0。

   ```js
   const buf = Buffer.allocUnsafe(10);
   
   // 输出: (内容可能不同): <Buffer a0 8b 28 3f 01 00 00 00 50 32>
   console.log(buf);
   
   buf.fill(0);
   
   // 输出: <Buffer 00 00 00 00 00 00 00 00 00 00>
   console.log(buf);
   ```

## 七、文件系统

### 1.概述

在Node中，与文件系统的交互是非常重要的，**服务器的本质就是将本地的文件发送给远程的客户端**。

Node通过fs模块来和文件系统进行交互。该模块提供了一些标准文件访问API来实现**对文件的IO操作**。

fs是Node的核心模块，使用时通过`const fs = require('fs')`进行导入。

### 2.同步和异步

- 同步：同步文件系统会**阻塞**程序的执行，除非操作完毕，否则不会向下执行代码（**顺序执行**）；
- 异步：异步文件系统**不会阻塞**程序的执行，而是在操作完成时，通过回调函数将结果返回。

### 3.文件写入

#### 3.1 同步文件写入

1. 打开文件`fs.openSync(path, flags[, mode])`

   - path <string> | <buffer> | <URL>：文件的路径

   - flags <string> | <number>：打开文件要做的操作类型

     | 操作类型 | 说明                                                         |
     | -------- | ------------------------------------------------------------ |
     | **r**    | **读取模式**，**若文件不存在则发生异常**                     |
     | r+       | 读写模式，若文件不存在则发生异常                             |
     | rs+      | 同步读写模式，命令操作系统绕过本地文件系统缓存（跳过潜在的旧本地缓存） |
     | **w**    | **写入模式**，**若文件不存在将自动创建一个新文件**           |
     | wx       | 类似'w'，但如果文件路径存在，则文件写入失败                  |
     | w+       | 读写模式，若文件不存在则创建                                 |
     | wx+      | 类似'w+'，但如果文件路径存在，则读写文件失败                 |
     | **a**    | **追加模式**，**若文件不存在将自动创建一个新文件**           |
     | ax       | 类似于a，但如果文件路径存在，则追加失败                      |
     | a+       | 以读取和追加模式打开文件，若文件不存在，将自动创建一个新文件 |
     | ax+      | 类似于'a+'，但如果文件路径存在，则失败                       |

   - mode <integer>：设置文件的操作权限，默认0o666

   返回值：该方法会返回一个文件的描述符的**数字**作为结果，我们可以通过该描述符来对文件进行各种操作。

2. 向文件写入内容`fs.writeSync(fd, string[, position[, encoding]])`

   - fd <integer>：文件的描述符，需要传递要写入的文件的描述符
   - string <string>：要写入的内容
   - position <integer>：写入的起始位置
   - encoding <string>：写入内容的编码，默认utf-8

   返回值：返回写入的字节数。

3. 保存并关闭文件`fs.closeSync(fd)`

   - fd <integer>：文件的描述符

   返回值：undefined。

```js
var fs = require("fs")

// 打开文件
var fd = fs.openSync('./hello.txt', 'w')
// 向文件写入内容
var length = fs.writeSync(fd, "距离下班还有两小时二十分钟...")
var end = fs.closeSync(fd)
```

![image-20230203154157001](https://gitee.com/v876774538/my-img/raw/master/image-20230203154157001.png)

#### 3.2 异步文件写入

1. 打开文件`fs.open(path, flags[, mode], callback)`
   - path <string> | <Buffer> | <URL>：文件路径
   - flags <string> | <number>：打开文件要做的操作类型
   - mode <integer>：操作权限，默认0o666
   - callback <Function>：回调函数
     - err <Error>：错误对象（第一个参数是err，nodeJs**错误优先思想**），**正确时返回null**
     - fd <integer>：文件描述符
2. 向文件写入内容`fs.write(fd, string[, position[, encoding]], callback)`
   - fd <integer>：文件的描述符，需要传递要写入的文件的描述符
   - string <string>：要写入的内容
   - position <integer>：写入的起始位置
   - encoding <string>：写入内容的编码，默认utf-8
   - callback <Function>：回调函数
     - err <Error>：错误对象
     - written <integer>
     - string <string>
3. 保存并关闭文件`fs.close(fd, callback)`
   - fd <integer>：文件描述符
   - callback <Function>：回调函数
     - err <Error>：错误对象

```js
fs.open('./hello.txt', 'w', (err, fd) => {
    if (!err) {
        fs.write(fd, '距离下班只剩两个小时了！', (err, written, string) => {
            if (!err) {
                console.log(written, string)
            }
            else {
                console.log(err)
            }
            // 关闭
            fs.close(fd, (err) => {
                if (!err) {
                    console.log('文件关闭')
                }
                else {
                    console.log(err)
                }
            })
        })
    }
    else {
        console.log(err)
    }
})
```

![image-20230203160846014](https://gitee.com/v876774538/my-img/raw/master/image-20230203160846014.png)

#### 3.3 简单文件写入

1. 异步写入

   `fs.writeFile(file, data[, options], callback)`

   - file <string> | <Buffer> | <URL> | <integer>：文件名或文件描述符
   - data <string> | <Buffer> | <Uint8Array>：要写入的数据
   - options <Object> | <string>：选项，可以对写入进行一些设置
     - encoding <string> | <null>：编码方式，默认utf-8
     - mode <integer>：操作权限
     - flag <string>：操作类型，**默认为'w'**
     - callback <Function>：回调函数
       - err <Error>：错误对象

   ```js
   const fs = require('fs')
   fs.writeFile('./hello.txt', '一小时三十分钟……', (err) => {
       if (!err) {
           console.log('写入成功~')
       }
       else {
           console.log(err)
       }
   })
   ```

2. 同步写入

   `fs.writeFileSync(file, data[, options])`

   - file <string> | <Buffer> | <URL> | <integer>：文件名或文件描述符
   - data <string> | <Buffer> | <Uint8Array>：要写入的数据
   - options <Object> | <string>：选项，可以对写入进行一些设置
     - encoding <string> | <null>：编码方式，默认utf-8
     - mode <integer>：操作权限
     - flag <string>：操作类型，**默认为'w'**

#### 3.4 流式文件写入

> 同步、异步、简单文件的写入都不适合大文件的写入：性能较差，一次性将内容准备好并进行写入容易导致内存溢出的问题。

1. 创建可写流

   `fs.createWriteStream(path[, options])`

   - path <string> | <Buffer> | <URL>：文件路径

   - options <string> | <Object>：可配置的参数

     - flags <string>
     - encoding <string>
     - fd <integer>
     - mode <integer>
     - autoClose <boolean>
     - start <integer>

     ```js
     const default = {
     	flags: 'w',
     	encoding: 'utf8',
     	fd: null,
     	mode: 0o666,
     	autoClose: true
     }
     ```

   返回值：返回一个新建的`WriteStream`对象。

   ```js
   const fs = require('fs')
   var ws = fs.createWriteStream('./hello.txt')
   ```

2. 通过ws向文件输入内容

   ```js
   ws.write('花间一壶酒，')
   ws.write('独酌无相亲。')
   ws.write('举杯邀明月，')
   ws.write('月既不解饮，')
   ws.write('影徒随我身。')
   ws.write('暂伴月将影，')
   ws.write('行乐须及春。')
   ws.write('我歌月徘徊，')
   ws.write('我舞影零乱。')
   ws.write('醒时相交欢，')
   ws.write('醉后各分散。')
   ws.write('永结无情游，')
   ws.write('相期邈云汉。')	// 分多次写入
   ```

   ![image-20230203171705401](https://gitee.com/v876774538/my-img/raw/master/image-20230203171705401.png)

3. 通过监听流的open和close事件来监听流的打开和关闭

   ```js
   ws.once('open', function () {
       console.log('流打开了')
   })
   ws.once('close', function () {
       console.log('流关闭了')
   })
   ```

### 4.文件读取

#### 4.1 同步文件读取

`fs.readSync(fd, buffer, offset, length, position)`

- fd <integer>：文件描述符，由open函数返回
- buffer <Buffer> | <Uint8Array>：缓冲区，存放从二进制文件读取的内容（Uint8Array 八位无符号整型数组）
- offset <integer>：偏移量，写入缓冲区的位置
- length <integer>
- position <integer>

#### 4.2 异步文件读取

`fs.read(fd, buffer, offset, length, position, callback)`

- fd <integer>：文件描述符，由open函数返回
- buffer <Buffer>：缓冲区，存放从二进制文件读取的内容
- offset <integer>：偏移量，写入缓冲区的位置
- length <integer>：读取的字节数
- position <integer>：表示从文件的某个位置读，默认从当前位置开始
- callback <Function>：回调函数
  - err <Error>
  - byteRead <integer>
  - buffer <Buffer>

#### 4.3 简单文件读取

1. 异步读取

   `fs.readFile(path[, options], callback)`

   - path <string> | <Buffer> | <URL> | <integer>：文件名或文件描述符
   - options <Object> | <string>
     - encoding <string> | <null>：默认为null
     - flag <string>：默认为'r'
   - callback <Function>
     - err <Error>:错误对象
     - data <string> | <Buffer>：读取数据

   ```js
   const fs = require('fs')
   fs.writeFile('./hello.txt', (err, data) => {
   	if (!err) {
   		console.log(data)
   	}
   })
   ```

2. 同步读取

   `fs.readFileSync(path[, options])`

   - path <string> | <Buffer> | <URL> | <integer>：文件名或文件描述符
   - options <Object> | <string>
     - encoding <string> | <null>：默认为null
     - flag <string>：默认为'r'

   > 如果指定了 `encoding` 选项，则该函数返回一个字符串，否则返回一个 buffer。

#### 4.4 流式文件读取

1. 创建一个可读流
   `fs.createReadStream(path[, options])`

   - path <string> | <Buffer> | <URL>

   - options <string> | <Object>

     - flag <string>
     - encoding <string>
     - fd <integer>
     - mode <integer>
     - autoClose <boolean>
     - start <integer>
     - end <integer>
     - highWaterMark <integer>

     ```js
     const defaults = {
     	flags: 'r',
     	encoding: null,
     	fd: null,
     	mode: 0o666,
     	autoClose: true,
     	highWaterMark: 64 * 1024
     }
     ```

   返回值：返回一个新建的`ReadStream`对象。

   ```js
   const fs = require('fs')
   var rs = fs.createReadStream('./hello.txt')
   
   // 监听流的打开和关闭
   rs.once('open', function() {
       console.log('可读流打开了')
   })
   rs.once('close', function() {
       console.log('可读流关闭了')
   })
   ```

2. 通过rs读取文件内容

   如果要读取一个可读流中的数据，必须要为可读流绑定一个data事件。data事件绑定完毕，它会自动开始读取数据。

   ```js
   rs.on('data', function(data) {
   	console.log(data)
   })
   ```

3. 将可读流读取到的数据直接输入到可写流中

   ```js
   const fs = require('fs')
   var rs = fs.createReadStream('./hello.txt')
   var fs = fs.createWriteStream('./hello1.txt')
   
   // 监听流的打开和关闭
   rs.once('open', function() {
       console.log('可读流打开了')
   })
   rs.once('close', function() {
       console.log('可读流关闭了')
   })
   ws.once('open', function() {
       console.log('可写流打开了')
   })
   ws.once('close', function() {
       console.log('可写流关闭了')
   })
   
   // 水管 将可读流读取到的数据直接输入到可写流中
   rs.pipe(ws);
   ```

### 5.fs模块其他方法

#### 5.1 验证路径是否存在

1. `fs.existsSync(path)`

   - path <string> | <Buffer> | <URL>

   若路径存在，则返回**true**，否则返回**false**。

#### 5.2 获取文件状态

1. `fs.stat(path, callback)`

   - path <string> | <Buffer> | <URL>
   - callback <Function>
     - err <Error>
     - stats <fs.Stats>

   获取文件的状态。它会给我们返回一个**对象**，这个对象保存了当前对象状态的相关信息。

   ```js
   Stats {
     dev: 2114,
     ino: 48064969,
     mode: 33188,
     nlink: 1,
     uid: 85,
     gid: 100,
     rdev: 0,
     size: 527,
     blksize: 4096,
     blocks: 8,
     atimeMs: 1318289051000.1,
     mtimeMs: 1318289051000.1,
     ctimeMs: 1318289051000.1,
     birthtimeMs: 1318289051000.1,
     atime: Mon, 10 Oct 2011 23:24:11 GMT,
     mtime: Mon, 10 Oct 2011 23:24:11 GMT,
     ctime: Mon, 10 Oct 2011 23:24:11 GMT,
     birthtime: Mon, 10 Oct 2011 23:24:11 GMT
   }
   ```

   **方法**：

   - stats.isFile() 是否是一个文件
   - stats.isDirectory() 是否是一个文件夹（目录）

   ```js
   fs.stat('a.mp3', (err, stat) => {
   	if (!err) {
   		console.log(stat)
   	}
   })
   ```

2. `fs.statSync(path)`

   - path <string> | <Buffer> | <URL>

#### 5.3 删除文件

1. `fs.unlink(path, callback)`

   - path <string> | <Buffer> | <URL>
   - callback <Function>
     - err <Error>：完成回调只有一个可能的异常参数

2. `fs.unlinkSync(path)`

   - path <string> | <Buffer> | <URL>

   返回值：`undefined`。

#### 5.4 列出文件

1. `fs.readdir(path[, options], callback)`
   - path <string> | <Buffer> | <URL>
   - options <string> | <Object>
     - encoding <string>：默认'utf8'
   - callback <Function>
     - err <Error>
     - files <string[]> | <Buffer[]>：目录中不包括'.'和'..'文件名的数组。每一个元素就是一个文件夹或一个文件的名字
2. `fs.readdirSync(path[, options])`
   - path <string> | <Buffer> | <URL>
   - options <string> | <Object>
     - encoding <string>：默认'utf8'

#### 5.5 截断文件

1. `fs.truncate(path, len, callback)`

   - path <string> | <Buffer> | <URL>
   - len <integer>：长度（字节），默认0
   - callback <Function>
     - err <Error>

   截断文件，将文件截断为指定的大小。

2. `fs.truncateSync(path, len)`

   - path <string> | <Buffer> | <URL>
   - len <integer>：默认0

#### 5.6 建立目录

1. `fs.mkdir(path[, mode], callback)`

   - path <string> | <Buffer> | <URL>
   - mode <integer>：默认0o777
   - callback <Function>
     - err <Error>

2. `fs.mkdirSync(path[, mode])`

   - path <string> | <Buffer> | <URL>
   - mode <integer>：默认0o777

   同步创建目录，返回`undefined`。

#### 5.7 删除目录

1. `fs.rmdir(path, callback)`

   - path <string> | <Buffer> | <URL>

   - callback <Function>

     - err <Error>

     > 注意：用于删除一个目录，如果在文件上使用fs.rmdir()，在windows平台将会导致`ENOENT`错误，在POSIX平台将会导致`ENOTDIR`错误。

2. `fs.rmdirSync(path)`

   - path <string> | <Buffer> | <URL>

#### 5.8 文件重命名

1. `fs.rename(oldPath, newPath, callback)`

   - oldPath <string> | <Buffer> | <URL>
   - newPath <string> | <Buffer> | <URL>
   - callback <Function>
     - err <Error>

   既可以对文件进行重命名，也可以间接实现对文件剪切（移动）的功能。

   ```js
   fs.rename('笔记.txt', 'C:\\Users\\sjy\\Desktop\\笔记.txt', (err) => {
   	if (!err) {
   		console.log('修改成功')
   	}
   })
   ```

2. `fs.renameSync(oldPath, newPath)`

   - oldPath <string> | <Buffer> | <URL>
   - newPath <string> | <Buffer> | <URL>

#### 5.9 监听文件的修改

1. `fs.watchFile(filename[, options], listener)`

   - filename <string> | <Buffer> | <URL>：要监视的文件的名字
   - options <Object>
     - persistent <boolean>：默认，true
     - interval <integer>：监听时间间隔（ms）。默认，5007
   - listener <Function>：回调函数，当文件发生变化时执行
     - current <fs.Stats>：当前状态对象
     - previous <fs.Stats>：以前状态对象

   监视`filename`的变化。回调`listener`会在每次访问文件时被调用。

   ```js
   fs.watchFile('message.txt', (curr, prev) => {
   	console.log('修改前文件大小', prev.size)
   	console.log('修改后文件大小', curr.size)
   })
   ```


### 6.练习-考试成绩整理

1. 导入需要的fs文件系统模块

   ```js
   const fs = require('fs')
   ```

2. 使用`fs.readFile()`方法，读取素材目录下的`成绩.txt`文件

3. 判断文件是否读取失败

   ```js
   fs.readFile('../素材/成绩.txt', 'utf-8', function(err, dataStr) {
   	// 文件读取失败
       if (err) {
           return console.log('读取文件失败！' + err.message)
       }
       // 文件读取成功
       console.log('读取文件成功！' + dataStr)
   })
   ```

   ![image-20230801155318435](C:\Users\pc01\AppData\Roaming\Typora\typora-user-images\image-20230801155318435.png)

4. 文件读取成功后，处理成绩数据

5. 将处理完成的成绩数据，调用`fs.writeFile()`方法，写入到新文件`成绩-ok.txt`中

   ```js
   fs.readFile('../素材/成绩.txt', 'utf-8', function(err, dataStr) {
   	// 文件读取失败
       if (err) {
           return console.log('读取文件失败！' + err.message)
       }
       // 文件读取成功
       console.log('读取文件成功！' + dataStr)
       
       // 处理成绩数据
       const arrOld = dataStr.split(' ')
       const arrNew = []
       arrOld.forEach((item) => {
           arrNew.push(item.replace('=', '：'))
       })
       const newStr = arrNew.join('\r\n')
       
       // 写入新文件
       fs.writeFile('./files/成绩-ok.txt', newStr, function(err) {
           if (err) {
               return console.log('成绩写入失败！' + err.message)
           }
           console.log('成绩写入成功！')
       })
   })
   ```

### 7.路径动态拼接

在使用fs模块操作文件时，如果提供的操作路径是以`./`或`../`开头的**相对路径**时，很容易出现路径动态拼接错误的问题：

因为代码在运行的时候，会**以执行node命令时所处的目录，动态拼接出被操作文件的完整路径**。

![image-20230801162635303](https://gitee.com/v876774538/my-img/raw/master/image-20230801162635303.png)

```js
const fs = require('fs')

// 出现路径拼接错误的问题，是因为提供了./或../开头的相对路径
fs.readFile('./files/1.txt', 'utf-8', function(err, dataStr) {
	if (err) {
		return console.log('读取文件失败！' + err.message)
	}
	console.log('读取文件成功！ ' + dataStr)
})
```

1. 解决方案1：提供绝对路径

   ```js
   // 单个\表示转义
   fs.readFile('C:\\Users\\escood\\Desktop\\Node.js基础\\day1\\code\\files\\1.txt', 'utf-8', function(err, dataStr) {
   	if (err) {
   		return console.log('读取文件失败！' + err.message)
   	}
   	console.log('读取文件成功！ ' + dataStr)
   })
   ```

   移植性非常差，不利于维护。

2. 解决方案2：`__dirname` 表示当前文件所处的目录

   ```js
   const fs = require('fs')
   
   fs.readFile(__dirname + '/files/1.txt', 'utf-8', function(err, dataStr) {
   	if (err) {
   		return console.log('读取文件失败！' + err.message)
   	}
   	console.log('读取文件成功！ ' + dataStr)
   })
   ```

## 八、path路径模块

### 1.概述

> **path模块**是Node.js官方提供的用来**处理路径**的模块，它提供了一系列的方法和属性，用来满足用户对路径处理的需求。

例如：

- `path.join()`方法，用来将多个路径片段拼接成一个完整的路径字符串
- `path.basename()`用来从路径字符串中，将文件名解析出来

在javascript代码中，使用path模块来处理路径，需要使用如下方法导入它：

```js
const path = require('path')
```

### 2.路径拼接

1. `path.join()`语法格式

   使用`path.join()`方法，可以把多个路径片段拼接为完整的路径字符串，语法格式如下：

   ```js
   path.join([...paths])
   ```

   - ...paths<string> 路径片段的序列
   - 返回值：<string>

2. 示例

   ```js
   const fs = require('fs')
   const path = require('path')
   
   fs.readFile(path.join(__dirname, '/files/1.txt'), 'utf-8', function(err, dataStr) {
   	if (err) {
   		return console.log('读取文件失败！' + err.message)
   	}
   	console.log('读取文件成功！ ' + dataStr)
   })
   ```

   ```js
   const path = require('path')
   
   // 注意： ../会抵消前面的路径
   const pathStr = path.join('/a', '/b/c', '../', './d', 'e')
   console.log(pathStr)	// \a\b\d\e
   
   const pathStr = path.join('/a', '/b/c', '../../', './d', 'e')
   console.log(pathStr)	// \a\d\e
   ```

### 3.获取路径中的文件名

1. `path.basename()`的语法格式

   使用`path.basename()`方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下：

   ```js
   path.basename(path[, ext])
   ```

   - path<string> 表示一个路径的字符串
   - ext<string> 可选参数，表示文件的扩展名
   - 返回值：<string> 表示路径中的最后一部分

2. 示例

   ```js
   const fpath = '/a/b/c/index.html'
   
   var fullName = path.basename(fpath)
   console.log(fullName)	// index.html
   
   var nameWithoutExt = path.basename(fpath, '.html')
   console.log(nameWithoutExt)	// index
   ```

### 4.获取路径中的文件扩展名

1. `path.extname()`的语法格式

   使用`path.extname()`方法，可以获取路径中的扩展名的部分，语法格式如下：

   ```js
   path.extname(path)
   ```

   - path<string> 必选参数，表示一个路径的字符串
   - 返回值<string> 返回得到的扩展名字符串

2. 示例

   ```js
   const fpath = '/a/b/c/index.html'
   
   const fext = path.extname(path)
   console.log(fext)	// .html
   ```

## 九、http模块

### 1.概述

> 回顾：什么是**客户端**？什么是**服务器**？
>
> 在网络节点中，**负责消费资源**的电脑，叫做**客户端**；**负责对外提供网络资源**的电脑，叫做**服务器**。

> `http模块`是Node.js官方提供的、用来创建Web服务器的模块。
>
> 通过http模块提供的`http.createServer()`方法，就能方便地把一台普通的电脑，变成一台Web服务器，对外提供Web资源服务。

如果要使用http模块来创建Web服务器，我们首先需要导入它：

```js
const http = require('http')
```

### 2.作用

服务器和普通电脑的区别在于：服务器上安装了Web服务器软件，例如：IIS、Apache等。通过安装这些服务器软件，就能把一台普通的电脑变成一台Web服务器。

在Node.js中，我们不需要使用这些第三方Web服务器软件，而是基于Node.js提供的http模块，通过几行简单的代码，就能轻松地手写一个而服务器软件，对外提供Web服务。

### 3.服务器相关的概念

#### 3.1 IP地址

IP地址是互联网上每台计算机的唯一地址。

IP地址的格式：通常用“点分十进制”表示成(`a.b.c.d`)的形式，其中，a b c d都是0~255之间的十进制整数：如，192.168.1.1。

注意：

- 互联网中每台Web服务器，都有自己的IP地址：例如可以在Windows终端中运行`ping www.baidu.com`命令，查看百度服务器的IP地址；
- 在开发期间，自己的电脑即时一台服务器，也是一个客户端。为了方便测试，可以在自己的浏览器中输入`127.0.0.1`（localhost，本机回送地址）这个IP地址，就能把自己的电脑当做服务器进行访问了。

#### 3.2 域名和域名服务器

1. 域名

   尽管IP地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，**不直观**也**不便于记忆**，于是人们又发明了另一套**字符型的地址方案**，即所谓的**域名(Domain Name)地址**。

2. 域名服务器

   IP地址和域名存在对应的关系，这份**对应关系**存放在一种叫做**域名服务器(DNS, Domain name server)**的电脑中。使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，域名服务器就是提供IP地址和域名之间转换服务的服务器。

#### 3.3 端口号

计算机中的端口号，就好比现实生活中的门牌号。

在一台电脑中，可以运行成百上千个Web服务，每个Web服务都对应一个**唯一**的端口号。

![image-20230801175705601](https://gitee.com/v876774538/my-img/raw/master/image-20230801175705601.png)



注：在实际应用中，URL中的**80端口可以被省略**。

### 4.创建最基本的Web服务器

1. 导入http模块

   ```js
   const http = require('http')
   ```

2. 创建web服务器实例

   调用`http.createServer()`方法，快速创建一个web服务器实例

   ```js
   const server = http.createServer()
   ```

3. 为服务器实例绑定`request`事件，**监听客户端请求**

   调用服务器实例的`.on()`方法，为服务器绑定一个request事件

   ```js
   server.on('request', (req, res) => {
   	// 只要有客户端来请求服务器，就会触发request事件，从而调用这个事件处理函数
   	console.log('Someone visit our web server')
   })
   ```

4. 启动服务器

   调用服务器实例的`.listen()`方法，即可启动当前的Web服务器实例

   ```js
   server.listen(80, () => {
   	console.log('http server running at http://127.0.0.1:80')
   })
   ```

   ![image-20230802152649495](https://gitee.com/v876774538/my-img/raw/master/image-20230802152649495.png)

5. `req`请求对象

   只要服务器接收到了客户端的请求，就会调用通过`.on()`为服务器绑定的**request事件处理函数**。

   如果想在事件处理函数中，**访问与`客户端`相关的数据或属性**，可以使用如下方法：

   ```js
   server.on('request', (req, res) => {
   	// req是请求对象，它包含了与客户端相关的数据和属性，例如：
   	// req.url 是客户端请求的url地址
   	// req.method 是客户端的method请求类型
   	const str = `Your request url is ${req.url}, and request method is ${req.method}``
   	console.log(str)
   })
   ```

6. `res`响应对象

   在服务器的request事件处理函数中，如果想**访问与`服务器`相关的数据或属性**，可以使用如下方法：

   ```js 
   server.on('request', (req, res) => {
   	// res是响应对象，它包含了与服务器相关的数据和属性，例如：
   	// 要发送到客户端的字符串
   	const str = `Your request url is ${req.url}, and request method is ${req.method}`
   	// res.end()方法
   	// 想客户端发送指定的内容，并结束这次请求的处理过程
       res.end(str)
   })
   ```

7. 解决中文乱码的问题

   在调用`.end()`方法向客户端发送中文内容的时候，会出现乱码的问题，需要手动**设置内容的编码格式**：

   ```js
   server.on('request', (req, res) => {
   	// 发送的内容包含中文
   	const str = `您请求的url地址为${req.url}，请求的method类型为${req.method}`
       // 设置响应头
       res.setHeader('Content-Type', 'text/html; charset=utf-8')
       res.end(str)
   })
   ```

### 5.根据不同的url响应不同的html内容（动态响应内容）

1. 获取请求的url地址

2. 设置默认的响应内容为`404 not found`

3. 判断用户请求的是否为`/`或`/index.html`首页

4. 设置Content-Type响应头，防止中文乱码

5. 使用`res.end()`把内容响应给客户端

   ```js
   server.on('request', (req, res) => {
   	const url = req.url	// 1.获取请求的url地址
   	let content = '<h1>404 not found!</h1>'	// 2.设置默认响应内容为404 not found
   	if (url == '/' || url == '/index.html') {
   		content = '<h1>首页</h1>'
   	}
   	else if (url == '/about.html') {
   		content = '<h1>关于页面</h1>'
   	}
   	res.setHeader('Content-Type', 'text/html; charset=utf-8')
   	res.end(content)
   })
   ```

### 6.实现一个html资源的web服务器

#### 6.1 核心思路

把文件的实际存放路径，作为每个资源的请求url地址。

![image-20230802172602488](https://gitee.com/v876774538/my-img/raw/master/image-20230802172602488.png)

#### 6.2 实现步骤

1. 导入需要的模块

   ```js
   const http = require('http')	// http模块
   const fs = require('fs')		// 文件系统
   const path = require('path')	// path模块
   ```

2. 创建基本的web服务器

   ```js
   // 创建web服务器
   const server = http.createServer()
   
   // 监听web服务器的request事件
   server.on('request', (req, res) => {
   	...
   })
   
   // 启动服务器
   server.listen(80, () => {
   	console.log('server listen at http://127.0.0.1')
   })
   ```

3. **将资源请求的url地址映射为文件的存放路径**

   ```js
   server.on('request', (req, res) => {
       // 获取到客户端请求的url
       const url = req.url
   
       // 把请求的url地址，映射为本地文件的存放路径
       const fpath = path.join(__dirname, url)
   })
   ```

4. 读取文件内容，并响应给客户端

   ```js
   server.on('request', (req, res) => {
       ...
       
       // 根据映射过来的文件路径读取文件
       fs.readFile(fpath, 'utf8', (err, dataStr) => {
           // 读取文件失败，向客户端响应固定的错误消息
           if (err) {
               return res.end('404 not fount')
           }
           // 读取文件成功，向客户端响应读取成功的内容
           res.end(dataStr)
       })
   })
   ```

5. 优化资源的请求路径

   ```js
   server.on('request', (req, res) => {
       // 获取到客户端请求的url
       const url = req.url
   
       // 把请求的url地址，映射为本地文件的存放路径
       let fpath = ''
       if (url == '/') {
           // 手动指定文件存放路径
           fpath = path.join(__dirname, './clock/index.html')
       } else {
           // 动态拼接文件路径
           fpath = path.join(__dirname, './clock', url)
       }
       
   })
   ```

6. 全部代码

   ```js
   const http = require('http')	// http模块
   const fs = require('fs')		// 文件系统
   const path = require('path')	// path模块
   
   // 创建web服务器
   const server = http.createServer()
   
   // 监听web服务器的request事件
   server.on('request', (req, res) => {
   	// 获取到客户端请求的url
       const url = req.url
   
       // 把请求的url地址，映射为本地文件的存放路径
       let fpath = ''
       if (url == '/') {
           // 手动指定文件存放路径
           fpath = path.join(__dirname, './clock/index.html')
       } else {
           // 动态拼接文件路径
           fpath = path.join(__dirname, './clock', url)
       }
       
       // 根据映射过来的文件路径读取文件
       fs.readFile(fpath, 'utf8', (err, dataStr) => {
           // 读取文件失败，向客户端响应固定的错误消息
           if (err) {
               return res.end('404 not fount')
           }
           // 读取文件成功，向客户端响应读取成功的内容
           res.end(dataStr)
       })
   })
   
   // 启动服务器
   server.listen(80, () => {
   	console.log('server listen at http://127.0.0.1')
   })
   ```

## 十、模块化

### 1.模块化的基本概念

#### 1.1 概述

> **模块化**是指解决一个复杂问题，**自顶向下逐层地把系统划分成若干模块**的过程。对于整个系统来说，模块是**可组合、分解和更换的单元**。

1. 生活中的模块化

   ![image-20230816140403797](https://gitee.com/v876774538/my-img/raw/master/image-20230816140403797.png)

2. 编程领域中的模块化

   编程领域中的模块化，就是**遵守固定的规则**，把一个大文件拆成**独立并且互相依赖**的多个小模块。

   模块化的好处：

   - 提高了代码的**复用性**；
   - 提高了代码的**可维护性**；
   - 可以实现**按需加载**

#### 1.2 模块化规范

> 模块化规范就是对代码进行模块化拆分和组合时，需要遵守的规则。

模块化规范的好处：

- 降低了沟通的成本，极大方便了各个模块之间的相互调用。

### 2.Node.js模块化

#### 2.1 Node.js中模块的分类

Node.js中根据模块的来源不同，将模块分为了3大类，分别是：

- **内置模块**：由nodejs官方提供的，如fs、path、http等；
- **自定义模块**：用户创建的每个.js文件，都是自定义模块；
- **第三方模块**：由第三方开发的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要下载

#### 2.2 加载模块

使用强大的`require()`方法，加载所需的模块进行使用：

```js
// 加载内置模块
const fs = require('fs')

// 加载用户自定义模块
const custom = require('./custom.js')	// js后缀名可省略

// 加载第三方模块
const moment = require('moment')
```

注意：使用`require()`方法加载其他模块时，会执行被加载模块中的代码

#### 2.3 模块作用域

和函数作用域类似，**在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问**，这种模块级别的访问限制，叫做**模块作用域**。

```js
// custom.js

const username = '张三'
function sayHello() {
	console.log('大家好，我是' + username)
}
```

```js
// test.js

const custom = require('./custom.js')

console.log(custom.username)	// undefined
```

1. 模块作用域的好处

   - 防止全局变量污染的问题

     ![image-20230816142136791](https://gitee.com/v876774538/my-img/raw/master/image-20230816142136791.png)

2. 向外共享模块作用域中的成员

   - `module`对象

     ```js
     console.log(module)
     ```

     在每个.js自定义模块中都有一个module对象，它里面存储了和当前模块有关的信息，打印如下：

     ![image-20230816142731892](https://gitee.com/v876774538/my-img/raw/master/image-20230816142731892.png)

   - `module.exports`对象

     在自定义模块中，可以使用`module.exports`**对象**，将模块内的成员共享出去，供外界使用。

     外界用`require()`方法导入自定义模块时，得到的就是`module.exports`所指向的对象。

     ```js
     // custom.js
     
     module.exports.username = '张三'
     module.exports.sayHello = function() {
     	console.log('大家好，我是' + this.username)
     }
     
     module.exports = {
         username: '张三',
         sayHello() {
             console.log('大家好，我是' + this.username)
         }
     }
     ```

     ```js
     // test.js
     
     const custom = require('./custom.js')
     
     custom.sayHello()
     ```

   - `exports`对象

     由于`module.exports`单词拼写较为复杂，为了简化向外共享成员的代码，Node提供了`exports`对象。默认情况下，**`exports`与`module.exports`指向的是同一个对象**。

     最终共享的结果，还是以`module.exports`指向的对象为准。

     ```js
     // custom.js
     
     exports.username = '张三'
     exports.sayHello = function() {
     	console.log('大家好，我是' + this.username)
     }
     ```

   - `exports`和`module.exports`的使用误区

     使用`require()`方法导入模块时，导入的结果永远**以`module.exports`指向的对象为准**：

     ```js
     // custom.js
     
     module.exports = {
         gender: '男',
         age: 22
     }
     exports.username = '张三'
     
     console.log(module)
     ```

     ```js
     // test.js
     
     const custom = require('./custom.js')
     ```

     ![image-20230816145430351](https://gitee.com/v876774538/my-img/raw/master/image-20230816145430351.png)

     ![image-20230816151056675](https://gitee.com/v876774538/my-img/raw/master/image-20230816151056675.png)

     ```js
     // custom.js
     
     module.exports.username = '张三'
     exports = {
     	gender: '男',
     	age: 22
     }
     ```

     ![image-20230816151549751](https://gitee.com/v876774538/my-img/raw/master/image-20230816151549751.png)

     ![image-20230816151755009](https://gitee.com/v876774538/my-img/raw/master/image-20230816151755009.png)

     ```js
     // custom.js
     
     exports.username = '张三'
     module.exports.gender = '男'
     ```

     ![image-20230816150301055](https://gitee.com/v876774538/my-img/raw/master/image-20230816150301055.png)

     ![image-20230816150439206](https://gitee.com/v876774538/my-img/raw/master/image-20230816150439206.png)

     ```js
     // custom.js
     
     exports = {
         username: '张三'
     }
     module.exports = exports
     module.exports.gender = '男'
     module.exports.age = 22
     ```

     ![image-20230816152155480](https://gitee.com/v876774538/my-img/raw/master/image-20230816152155480.png)

     ![image-20230816152439946](https://gitee.com/v876774538/my-img/raw/master/image-20230816152439946.png)

     建议不要在一个模块中同时使用`exports`和`module,exports`

#### 2.4 Node.js模块化规范

Node.js遵循了CommonJS模块化规范：

- 每个模块内部，`module`变量代表当前模块；
- `module`变量是一个对象，它的`exports`属性，是对外的接口；
- **加载某个模块，其实是加载模块的`module.exports`属性**。

### 3.npm与包

#### 3.1 概述

Node.js 中的第三方模块又叫做包。

**第三方模块和包指的是同一个概念**，只不过叫法不同。

1. 包的来源

   不同于Node.js中的内置模块与自定义模块，包是由第三方个人或团队开发的，免费且开源。

2. 为什么需要包

   Node.js的内置模块仅提供了一些底层API，导致在基于内置模块进行项目开发时效率很低。

   包是基于内置模块封装而来的，提供了更高级、方便的API，极大地提高了开发效率。包和内置模块之间的关系，类似于jQuery和浏览器内置API之间的关系。

#### 3.2 npm

全球最大的包共享平台 https://www.npmjs.com/，我们可以从这个网站上**搜索**到需要的包；

另外`npm, Inc.`公司提供了一个地址为https://registry.npmjs.org/的服务器，来对外共享所有的包，我们可以从这个服务器上**下载**自己所需要的包。

1. 下载包

   使用包管理工具（`Node Package Manager`，简称npm包管理工具，Node.js自带），从https://registry.npmjs.org/服务器把所需要的包下载到本地使用。

   我们可以在终端执行`npm -v`命令，来查看电脑上安装的npm包管理工具的版本号。

2. npm体验：格式化时间的两种做法

   - 格式化时间的传统做法：

     1）创建格式化时间的自定义模块

     `dateFormat.js`

     2）定义格式化时间的方法

     3）创建补零函数

     4）从自定义模块中导出格式化时间的函数

     ```js
     // dateFormat.js
     // 创建格式化时间函数
     function dateFormat(dtStr) {
     	const dt = new Date()
         const y = dt.getFullYear()
         const m = padZero(dt.getMonth() + 1)
         const d = padZero(dt.getDate())
         
         const hh = padZero(dt.getHours())
         const mm = padZero(dt.getMinutes())
         const ss = padZero(dt.getSeconds())
         
         return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
     }
     
     // 创建补0函数
     function padZero(n) {
     	return n > 9 ? n : '0'+ n;
     }
     
     // 导出格式化时间函数
     module.exports = {
     	dateFormat
     }
     ```

     5）导入格式化时间的自定义模块

     ```js
     // 导入自定义格式化时间模块
     const TIME = require('./dateFormate')
     const dt = new Date()
     // 调用格式化时间函数
     const newDT = TIME.dateFormat(dt)
     console.log(newDT)
     ```

   - `moment`包

     1）使用npm包管理工具，在项目中安装格式化时间包`moment`

     2）使用`require()`导入格式化时间的包

     3）参考`moment`的官方API文档对时间进行格式化https://momentjs.com/docs/#/use-it/

     ```js
     const moment = require('moment')
     
     // moment() 获取当前时间
     // format() 对时间进行格式化
     const dt = moment().format('YYYY-MM-DD HH:mm:ss')
     
     console.log(dt)
     ```

3. 项目中安装包

   ```shell
   npm install 包的完整名称
   ```

   简写：

   ```shell
   npm i 包的完整名称
   ```

4. 初次装包后多了哪些文件

   - `node_modules`文件夹：存放所有已安装到项目中的包。`require()`导入第三方包时，就是从这个目录中查找并加载包；

   - `package-lock.json`配置文件：记录`node_modules`目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等。

     ![image-20231016150234312](https://gitee.com/v876774538/my-img/raw/master/image-20231016150234312.png)

     注意：二者由npm包管理工具自动维护，不要手动修改。

5. 安装指定版本的包

   默认情况下，使用`npm install`命令安装包会自动安装最新版本的包。

   如果需要安装指定版本的包，可以在包名之后，通过`@`符号指定具体版本：

   ```shell
   npm i moment@2.22.2
   ```

6. 包的语义化版本规范

   包的版本号是以**“点分十进制”**的形式进行定义的。总共有三维数字，例如`2.24.0`。

   - 第1位数字：代表`大版本`；

   - 第2位数字：代表`功能版本`；

   - 第3位数字：代表`Bug修复版本`。

   > 版本号提升规则：只要前面的版本号增长，后面的版本号就**归零**。

7. 包管理配置文件`package.json`

   npm规定，在`项目根目录`中，必须提供一个叫做`package.json`的包管理配置文件，用来记录与项目有关的一些配置信息。例如：

   - 项目的名称、版本号、描述；
   - 项目中使用的包；
   - 声明哪些包仅在`开发期间`使用，哪些包在`开发`和`部署`时都需要使用。

   **多人协作问题：**

   ![image-20231016153101714](https://gitee.com/v876774538/my-img/raw/master/image-20231016153101714.png)

   在共享代码时剔除`node_modules`目录（将`node_modules`文件添加到`.gitignore`git忽略文件中），**根据`package.json`配置文件记录的安装包使用`npm install`或`npm i`一次性安装所有的依赖包**，从而方便团队成员之间共享项目源代码。

   **快速创建`package.json`文件：**

   ```shell
   npm init -y
   ```

   注意：

   - 上述命令只能在英文目录下成功运行。项目文件夹名称一定要使用英文命名，且不能出现空格；
   - 运行`npm install`命令安装包时，npm包管理工具会自动把包的名称及版本号记录到`package.json`中。

   **`dependencies`节点：** 专门用来记录我们使用`npm install`命令安装了那些包。

   ![image-20231016154017546](https://gitee.com/v876774538/my-img/raw/master/image-20231016154017546.png)

   **`devDependencies`节点：** 如果某些包**只在项目开发阶段使用**，则建议把这些包记录到`devDependencies`节点中。

   ```shell
   npm i 包名 -D
   
   // 完整形式
   npm install 包名 --save-dev
   ```

8. 卸载项目中的包

   ```shell
   npm uninstall 包名
   ```

   注意：`npm uninstall`命令执行成功后，会将卸载的包自动从`package.json`的`dependencies`中移除掉。

9. 解决下包速度慢的问题：

   - 淘宝npm镜像服务器

     ![image-20231016155248274](https://gitee.com/v876774538/my-img/raw/master/image-20231016155248274.png)

     淘宝在国内搭建了一个服务器，专门把国外官方服务器上的包同步到国内服务器，然后在国内提供下包的服务，从而极大地提高了下包的速度。

     扩展：**镜像(Mirroring)** 是一种文件存储形式，一个磁盘上的数据在另一个磁盘上存在一个完全相同的副本，即为镜像。

   - 切换npm的下包镜像源

     下包的镜像源，指下包的服务器地址。

     ```shell
     # 查看当前的下包镜像源
     npm config get registry
     
     # 将下包的镜像源切换为淘宝镜像源
     npm config set registry=https://registry.npm.taobao.org/
     # 检查镜像源是否下载成功
     npm config get registry
     ```

   - nrm（非必须）

     `nrm`工具提供了终端命令，可以快速查看和切换下包的镜像源。

     ```shell
     # 通过npm包管理器将nrm安装为全局可用的工具
     npm i nrm -g
     # 查看所有可用的镜像源
     nrm ls
     # 将下包的镜像源切换为taobao镜像
     nrm use taobao
     ```

#### 3.3 包的分类

1. 项目包：被安装到项目的`node_module`目录的包，都属于项目包

   - 开发依赖包（记录在`devDependencies`节点，仅在开发期间使用）
   - 核心依赖包（记录在`dependencies`节点，在开发及上线之后都会使用）

   ```shell
   npm i 包名 -D	# 开发依赖包
   npm i 包名	# 核心依赖包
   ```

2. 全局包：在执行`npm install`命令时，如果提供了`-g`参数，则会把包安装为`全局包`

   全局包默认会被安装到`C:\Users\用户目录\AppData\Roaming\npm\node_modules`目录下。

   ![image-20231016161522003](https://gitee.com/v876774538/my-img/raw/master/image-20231016161522003.png)

   ```shell
   npm i 包名 -g			# 全局安装
   npm uninstall 包名 -g	 # 卸载全局包
   ```

3. i5ting_toc：一个可以把`md`文档转为`html`页面的小工具，使用步骤如下

   ```shell
   # 安装
   npm install -g i5ting_toc
   # 调用
   i5ting_toc -f 要转换的md文件路径 -o
   ```

   ![image-20231016164049750](https://gitee.com/v876774538/my-img/raw/master/image-20231016164049750.png)

#### 3.4 规范的包结构

1. 包必须以`单独的目录`存在

   ![image-20231016164249132](https://gitee.com/v876774538/my-img/raw/master/image-20231016164249132.png)

2. 包的顶级目录下必须包含`package.json`这个包管理配置文件

   ![image-20231016164354812](https://gitee.com/v876774538/my-img/raw/master/image-20231016164354812.png)

3. `package.json`中必须包含`name`，`version`，`main`三个属性，分别代表包的名字、版本号、包的入口

#### 3.5 开发属于自己的包

1. 需要实现的功能

   - 格式化日期
   - 转义HTML中的特殊字符
   - 还原HTML中的特殊字符

2. 初始化包的基础结构

   - 新建`itheima-tools`文件夹，作为**包的根目录**

   - 在`itheima-tools`文件夹中，新建以下文件：

     - `package.json`包管理配置文件
     - `index.js`包的入口文件
     - `src目录`将不同功能进行模块化拆分，放到src目录下
     - `README.md`包的说明文档

     ![image-20231016172732963](https://gitee.com/v876774538/my-img/raw/master/image-20231016172732963.png)

3. 初始化`package.json`

   ```json
   {
   	"name": "itheima-tools",
       "version": "1.0.0",
       "main": "index.js",
       "description": "提供了格式化时间、HTML Escape的功能",
       "keywords": ["itheima", "dateFormat", "escape"],
       "license": "ISC"
   }
   ```

   - name：包名

   - version：包的版本

   - main：指定包的入口文件路径

   - desciption：包的剪短的描述信息

     ![image-20231016170520010](https://gitee.com/v876774538/my-img/raw/master/image-20231016170520010.png)

   - keywords：数组，每一项都是字符串，搜索关键字

   - license：许可协议，https://www.jianshu.com/p/86251523e898

     ![image-20231016170740409](https://gitee.com/v876774538/my-img/raw/master/image-20231016170740409.png)

4. 在`src/dateFormat.js`中定义格式化时间的方法

   ```js
   // 创建格式化时间函数
   function dateFormat(dtStr) {
   	const dt = new Date()
       const y = dt.getFullYear()
       const m = padZero(dt.getMonth() + 1)
       const d = padZero(dt.getDate())
       
       const hh = padZero(dt.getHours())
       const mm = padZero(dt.getMinutes())
       const ss = padZero(dt.getSeconds())
       
       return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
   }
   
   // 创建补0函数
   function padZero(n) {
   	return n > 9 ? n : '0'+ n;
   }
   
   // 导出格式化时间函数
   module.exports = {
   	dateFormat
   }
   ```

5. 在`src/htmlEscape.js`中定义转义及还原HTML的方法

   ```js
   // 定义转义HTML字符串函数
   function htmlEscape(htmlStr) {
       return htmlStr.replace(/<|>|"|&/g, (match) => {
           switch(match) {
               case '<':
                   return '&lt;'
               case '>':
                   return '&gt;'
               case '"':
                   return '&quot;'
               case '&':
                   return '&amp;'
           }
       })
   }
   
   // 定义还原HTML字符串函数
   function htmlUnEscape(htmlStr) {
       return htmlStr.replace(/&lt;|&gt;|&quot;|&amp;/g, (match) => {
           switch(match) {
               case '&lt;':
                   return '<'
               case '&gt;':
                   return '>'
               case '&quot;':
                   return '"'
               case '&amp;':
                   return '&'
           }
       })
   }
   
   module.exports = {
       htmlEscape,
       htmlUnEscape
   }
   ```

6. `index.js`引入

   ```js
   const date = require('./src/dateFormat')
   const escape = require('./src/htmlEscape')
   
   // 向外暴露需要的成员
   // ...展开运算符
   module.exports = {
       ...date,
       ...escape
   }
   ```

7. 编写包的说明文档`README.md`

   将包的使用说明，以markdown的格式写出来，方便用户参考。

   ```markdown
   ## 安装
   npm install itheima-tools
   
   ## 导入
   const itheima = require('itheima-tools')
   
   ## 格式化时间
   const dtStr = itheima.dateFormat(new Date())
   console.log(dtStr)
   
   ## 转义HTML
   const htmlStr = '<h1 title="abc">这是h1标签<span>123&nbsp;</span></h1>'
   const str = itheima.htmlEscape(htmlStr)
   console.log(str)
   
   ## 还原HTML
   const str2 = itheima.htmlUnEscape(str)
   console.log(str2)
   
   ## 开源协议
   ISC
   ```

8. 发布包

   - 注册npm账号https://www.npmjs.com/

   - 登录

     ```shell
     npm login
     ```

     注意：在运行`npm login`之前，**必须把下包的服务器地址切换为npm的官方服务器！**

   - 发布包

     切换到包的根目录，运行`npm publish`命令，即可将包发布到npm上（注意：`包名不能雷同`）。

     ```shell
     npm publish
     ```

     ![image-20231016175446360](https://gitee.com/v876774538/my-img/raw/master/image-20231016175446360.png)

   - 删除包

     运行`npm unpublish 包名 --force`，即可从npm删除已发布的包。

     ```shell
     npm unpublish 包名 --force
     ```

     注意：

     - 只能删除`72小时内`发布的包
     - 通过该命令删除的包，在`24小时内`不允许重复发布
     - 发布包时要慎重，尽量不往npm上发布无意义的包

### 4.模块的加载机制

#### 4.1 优先从缓存中加载

**模块在第一次加载后会被缓存**。

这也就意味着多次调用`require()`并不会导致模块代码被重复执行。

不论是内置模块、用户自定义模块还是第三方模块，它们都会优先从缓存中加载，从而**提高模块的加载效率**。

#### 4.2 内置模块的加载机制

内置模块是由Node.js官方提供的模块，**内置模块的加载优先级最高**。

例如，`require('fs')`始终返回内置的fs模块，即使在`node_modules`目录下有名字相同的其他fs包。

#### 4.3 自定义模块的加载机制

使用`require()`加载自定义模块时，必须指定以`./`或`../`开头的**路径标识符**。在加载自定义模块时，如果没有指定，NodeJs会把它当做`内置模块`或`第三方模块`进行加载。

注意：在使用`require()`导入自定义模块时，如果省略了文件的扩展名，则Node.js会按顺序分别尝试加载以下的文件：

1. 按照`确切的文件名`进行加载
2. 补全`.js`扩展名进行加载
3. 补全`.json`扩展名进行加载
4. 补全`.node`扩展名进行加载
5. 加载失败，终端报错

#### 4.4 第三方模块的加载机制

如果传递给`require()`的模块标识符不是一个内置模块，也没有以`./`或`../`开头，则Node.js会从当前模块的父目录开始，尝试**从`/node_modules`文件夹中加载第三方模块**。

如果没有找到对应的第三方模块，则移动到上一层父目录中，进行加载，直到文件系统的根目录。

![image-20231017103954937](https://gitee.com/v876774538/my-img/raw/master/image-20231017103954937.png)

#### 4.5 目录作为模块

当目录作为模块标识符，传递给`require()`进行加载的时候，有三种加载方式：

1. 在被加载的目录下查找一个叫做`package.json`的文件，并寻找`main`属性，作为`require()`加载的入口
2. 若目录中**没有**`package.json`文件，或`main`**入口不存在/无法解析**，则Node.js会视图加载目录下的`index.js`文件
3. 若以上两步均失败，Node.js会在终端打印错误信息，报告模块缺失：`Error: Cannot find module 'xxx'`

## 十一、Express

### 1.初识Express

#### 1.1 Express简介

1. 概述

   > 官方概念：Express是基于Node.js平台，快速、开放、极简的**Web开发框架**。

   Express的作用和Node.js内置的http模块类似，是专门**用来创建Web服务器**的。**本质上就是npm上的第三方包，提供了快速创建Web服务器的方法**（Express是基于内置的http模块进一步封装而来的）。

   Express中文官网：http://www.expressjs.com.cn/

2. 作用

   - `Web网站服务器`：专门对外提供Web网页资源的服务器；
   - `API接口服务器`：专门对外提供API接口的服务器

#### 1.2 使用

1. 安装

   在项目所处的目录中，运行如下终端命令：

   ```shell
   npm install express --save
   ```

2. 创建基本的web服务器

   ```js
   // 1.导入express
   const express = require('express')
   // 2.创建web服务器
   const app = express()
   // 3.调用app.listen(端口号, 启动成功后的回调函数) 启动服务器
   app.listen('80', () => {
   	console.log('express server running at http://127.0.0.1')
   })
   ```

3. 监听`GET请求`

   通过`get()`方法，可以监听客户端的GET请求。具体语法格式如下：

   ```js
   app.get('请求URL', function(req, res) {
   	// 处理函数
   })
   ```

   - 参数1：客户端请求的URL地址
   - 参数2：请求对应的处理函数
     - req：请求对象，包含与请求相关的属性与方法；
     - res：响应对象，包含与响应相关的属性与方法

4. 监听`POST请求`

   通过`post()`方法，可以监听客户端的POST请求。具体语法格式如下：

   ```js
   app.post('请求URL', function(req, res) {
   	// 处理函数
   })
   ```

   - 参数1：客户端请求的URL地址
   - 参数2：请求对应的处理函数
     - req：请求对象，包含与请求相关的属性与方法；
     - res：响应对象，包含与响应相关的属性与方法

5. 把内容`响应`给客户端

   通过调用`res.send()`方法，可以把处理好的内容，发送给客户端：

   ```js
   app.get('/user', (req, res) => {
   	// 调用Express提供的res.send()方法，向客户端响应一个JSON对象
   	res.send({
   		name: 'zs',
   		age: 20,
   		gender: '男'
   	})
   })
   
   app.post('/user', (req, res) => {
       // 向客户端发送文本内容
       res.send('请求成功')
   })
   ```

6. 获取URL中携带的查询参数

   通过`req.query`对象，可以访问到客户端通过`查询字符串`的形式，发送到服务器的参数：

   ```js
   app.get('/', (req, res) => {
   	// req.query 默认是一个空对象
   	// 客户端使用 ?name=zs&age=20 这种url携带字符串的形式，发送到服务器的参数，可以通过req.query对象访问到，如：
   	// req.query.name req.query.age
   	console.log(req.query)
   })
   ```

7. 获取URL中的动态参数

   通过`req.params`对象，可以访问到URL中通过`:`匹配到的动态参数：

   ```js
   // URL地址中，可以通过:参数名的形式，匹配动态参数值
   app.get('/user/:id/:name', (req, res) => {
   	// req.params 默认是一个空对象
   	// 里面存放通过:动态匹配到的参数值
   	console.log(req.params)
       res.send(req.params)
   })
   ```

   ![image-20231017135912998](https://gitee.com/v876774538/my-img/raw/master/image-20231017135912998.png)

#### 1.3 托管静态资源

1. `express.static()`

   通过`express.static()`创建一个**静态资源服务器**。例如，通过如下代码就可以将public目录下的图片、CSS文件、JavaScript文件对外开放访问：

   ```js
   // 指定静态资源目录
   app.use(express.static('public'))
   ```

   现在，我们就可以访问public目录中的所有文件了：

   http://localhost:3000/images/bg.jpg

   http://localhost:3000/css/style.css

   http://localhost:3000/js/login.js

   Express**在指定的静态目录中查找文件**，并对外提供资源的访问路径。因此，存放静态文件的目录名(public)并不会出现在URL中。

   ```js
   const express = require('express')
   cosnt app = express()
   
   // 调用express.static()快速地对外提供静态资源
   app.use(express.static(path.join(__dirname, '../public')))
   
   app.listen(80, () => {
   	console.log('express server running at http://127.0.0.1')
   })
   ```

2. 托管多个静态资源目录

   希望脱光多个静态资源目录，多次调用`express.static()`函数即可：

   ```js
   app.use(express.static('public'))
   app.use(express.static('files'))
   ```

   访问静态资源文件时，`express.static()`会**根据目录的添加顺序查找所需的文件**。

3. 挂载路径前缀

   ```js
   app.use('/public', express.static('public'))
   ```

   现在，我们就可以通过带有`/public`前缀的地址来访问public目录中的文件了：

   http://localhost:3000/public/images/bg.jpg

   http://localhost:3000/public/css/style.css

   http://localhost:3000/public/js/login.js

#### 1.4 nodemon

1. 概述

   在编写调试Node.js项目的时候，若修改了项目的代码，需要频繁地手动close再重新启动，非常繁琐。

   因此我们可以使用`nodemon`(https://www.npmjs.com/package/nodemon)工具，它能够**监听项目文件的变动**，当代码被修改后，**自动帮我们重启项目**。

2. 安装

   在终端中，运行如下命令，将nodemon安装为全局可用的工具：

   ```shell
   npm install -g nodemon
   ```

3. 使用

   在基于Node.js编写网站应用的时候，传统方式是运行`node app.js`命令，来启动项目。

   现在，我们可以将`node`命令替换为`nodemon`命令，使用`nodemon app.js`来启动项目。

### 2.Express路由

#### 2.1 概述

1. 路由

   在Express中，路由指的是**客户端的请求**与**服务器处理函数**之间的**映射关系**。

   Express中的路由分为3部分组成，分别是`请求的类型`、`请求的URL地址`、`处理函数`。格式如下：

   ```js
   app.METHOD(PATH, HANDLER)
   ```

   ```js
   app.get('/', function(req, res) {
   	res.send('Hello World!')
   })
   
   app.post('/', function(req, res) {
   	res.send('Got a POST request')
   })
   ```

2. 路由的匹配过程

   每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成果之后，才会调用对应的处理函数。

   在匹配时，会按照路由的**先后顺序**进行匹配，如果`请求类型`和`请求的URL`同时匹配成功，则Express会将这次请求，转交给对应的function函数进行处理。

   ![image-20231017145522979](https://gitee.com/v876774538/my-img/raw/master/image-20231017145522979.png)

#### 2.2 使用

1. 最简单的用法

   在Express中使用路由最简单的方式，就是把路由挂载到app（服务器实例）上，实例代码如下：

   ```js
   const express = require('express')
   const app = express()
   
   // 挂载路由
   app.get('/', function(req, res) {
   	res.send('Hello World!')
   })
   app.post('/', function(req, res) {
   	res.send('Got a POST request')
   })
   
   // 启动Web服务器
   app.listen(80, () => {
   	console.log('Server running at http://127.0.0.1')
   })
   ```

2. 模块化路由

   为了方便对路由进行**模块化管理**，Express不建议将路由直接挂载到app上，而是**将路由抽离为单独的模块**。

   步骤：

   - 创建路由模块对应的`.js`文件
   - 调用`express.Router()`函数创建路由对象
   - 向路由对象上挂载具体的路由
   - 使用`module.exports`向外共享路由对象
   - 使用`app.use()`函数注册路由模块

   ```js
   // /router/user.js
   // 创建路由模块
   
   // 导入express
   var express = require('express')
   // 创建路由对象
   var router = express.Router()
   
   // 挂载具体的路由
   // 挂载获取用户列表的路由
   router.get('/user/list', function(req, res) {
       res.send('Get user list.')
   })
   // 挂载添加用户的路由
   router.post('/user/add', function(req, res) {
       res.send('Add new user.')
   })
   
   module.exports = router	// 向外导出路由对象
   ```

   ```js
   // app.js
   const express = require('express')
   const app = express()
   
   // 导入路由模块
   const userRouter = require('./router/user.js')
   
   // 使用app.use()注册路由模块
   app.use(userRouter)
   
   app.listen(80, () => {
       console.log('http://127.0.0.1')
   })
   ```

   注意：`app.use()`函数的作用，就是来注册全局中间件。

3. 为路由模块添加前缀

   类似于托管静态资源时，为静态资源统一挂载访问前缀一样，路由模块添加前缀的方式也非常简单：

   ```js
   app.use('/api', userRouter)
   ```

### 3.Express中间件

#### 3.1 概述

1. 中间件

   中间件(Middleware)，特指**业务流程的中间处理环节**。

2. 中间件的`调用流程`

   当一个请求到达Express服务器之后，可以**连续调用多个中间件**，从而对这次请求进行**预处理**。

   ![image-20231017155144725](https://gitee.com/v876774538/my-img/raw/master/image-20231017155144725.png)

3. 中间件的`格式`

   Express中间件，本质上就是一个`function处理函数`，格式如下：

   ![image-20231017155333572](https://gitee.com/v876774538/my-img/raw/master/image-20231017155333572.png)

   中间件的形参列表中，**必须包含`next`参数**；路由处理函数中只包含`req`和`res`。

4. next函数的作用

   `next`函数是实现多个中间件连续调用的关键，它表示把流转关系**转交**给下一个中间件或路由。

   ![image-20231017160236332](https://gitee.com/v876774538/my-img/raw/master/image-20231017160236332.png)

#### 3.2 使用

1. 定义中间件函数

   ```js
   // 常量 mw 所指向的，就是一个中间件函数
   const mw = function(req, res, next) {
   	console.log('这是一个简单的中间件函数')
   	next()
   }
   ```

2. `全局生效`的中间件

   客户端发起的**任何请求**，到达服务器之后，**都会触发**的中间件，叫做**全局生效的中间件**。

   > 类似于`路由守卫`/`请求拦截器`。

   通过调用`app.use(中间件函数)`，即可注册一个全局生效的中间件（**全局中间件**），实例代码如下：

   ```js
   const express = require('express')
   const app = express()	// 实例化
   
   // 定义一个最简单的中间件函数
   // 常量 mw 所指向的，就是一个中间件函数
   const mw = function(req, res, next) {
   	console.log('这是一个简单的中间件函数')
   	next()
   }
   
   // 全局生效的中间件
   app.use(mw)
   
   app.get('/', (req, res) => {
       res.send('Home page.')
   })
   
   app.get('/user', (req, res) => {
       res.send('User page.')
   })
   
   app.listen(80, () => {
       console.log('http://127.0.0.1')
   })
   ```

   定义全局中间件的**简化形式**：

   ```js
   app.use(function (req, res, next) {
   	console.log('这是一个简单的中间件函数')
   	next()
   })
   ```

3. 中间件的作用

   多个中间件和路由之间，**共享同一份`req`和`res`**。

   基于这样的特性，我们可以在**上游**的中间件中，**统一**为req或res对象**添加自定义的属性或方法**，供**下游**的中间件或路由进行使用。

   ```js
   const express = require('express')
   const app = express()	// 实例化
   
   app.use(function (req, res, next) {
   	// 获取请求到达服务器的时间
   	const time = Date.now()
   	req.startTime = time	// 为req对象挂载自定义属性 把时间共享给后面的所有路由
   	next()
   })
   
   app.get('/', (req, res) => {
       res.send('Home page.' + req.startTime)
   })
   
   app.get('/user', (req, res) => {
       res.send('User page.' + req.startTime)
   })
   
   app.listen(80, () => {
       console.log('http://127.0.0.1')
   })
   ```

4. 定义多个全局中间件

   可以使用`app.use()`连续定义多个全局中间件。

   客户端请求到达服务器之后，会**按照中间件定义的先后顺序**依次进行调用，示例代码如下：

   ```js
   const express = require('express')
   const app = express()	// 实例化
   
   // 第一个全局中间件
   app.use(function (req, res, next) {
   	console.log('第1个全局中间件')
   	next()
   })
   
   // 第二个全局中间件
   app.use(function (req, res, next) {
   	console.log('第2个全局中间件')
   	next()
   })
   
   app.get('/', (req, res) => {
       res.send('Home page.')
   })
   
   app.get('/user', (req, res) => {
       res.send('User page.')
   })
   
   app.listen(80, () => {
       console.log('http://127.0.0.1')
   })
   ```

5. `局部生效`的中间件

   不使用`app.use()`定义的中间件，称作局部生效的中间件（局部中间件），示例代码如下：

   ```js
   const mw1 = function(req, res, next) {
   	console.log('这是中间件函数')
   	next()
   }
   
   // mw1 仅在当前路由中生效
   app.get('/', mw1, function(req, res) {
   	res.send('Home page')
   })
   
   app.get('/user', (req, res) => {
       res.send('User page.')
   })
   ```

6. 定义多个局部中间件

   可以在路由中，通过如下两种**等价**的方式，**使用多个局部中间件**：

   ```js
   app.get('/', mw1, mw2, (req, res) => {
   	res.send('Home page.')
   })
   // 或
   app.get('/', [mw1, mw2], (req, res) => {
   	res.send('Home page.')
   })
   ```

7. 中间件使用注意事项

   - 一定要**在路由之前注册中间件**；
   - 客户端发送过来的请求，可以连续调用多个中间件进行处理；
   - 执行完中间件业务代码之后，**不要忘记调用`next()`函数**；
   - 为了防止代码逻辑的混乱，在调用`next()`之后，不要再书写额外的代码；
   - 连续调用多个中间件时，**多个中间件之间，共享`req`和`res`对象**；

#### 3.3 中间件的分类

为了方便大家理解和记忆中间件的使用，Express官方把常见的中间件用法，分成了5大类，分别是：

1. `应用级别`的中间件

   通过`app.use()`或`app.get()`或`app.post()`绑定到app实例上的中间件，都叫做应用级别的中间件。

2. `路由级别`的中间件

   绑定到`express.Router()`实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不过应用级别中间件是绑定到app实例上的，而**路由级别中间件是绑定到router实例上**：

   ```js
   var express = require('express')
   var app = express()
   var router = express.Router()
   
   // 路由级别的中间件
   router.use(function(req, res, next) {
       console.log('Time:', Date.now())
       next()
   })
   
   app.use('/', router)
   ```

3. `错误级别`的中间件

   用于捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

   格式：错误级别中间件的function处理函数中，必须有4个形参，分别是(`err`, req, res, next)

   ```js
   // 路由在前 错误级别中间件在后
   app.get('/', function(req, res) {
   	throw new Error('服务器发生错误')	// 抛出自定义错误
   	res.send('Home page.')
   })
   
   // 错误级别中间件
   app.use(function(err, req, res, next)) {
   	console.log('发生错误' + err.message)
   	res.send('Error!' + err.message)
   }
   ```

   注意：错误级别的中间件，**必须注册在所有路由之后**！

4. `Express`内置的中间件

   自4.16.0版本开始，Express内置了3个常用的中间件，极大地提高了Express项目的开发效率和体验：

   - `express.static`快速托管静态资源的内置中间件，可以托管如HTML文件、图片、CSS样式等（无兼容性要求）
   - `express.json`解析JSON格式的请求体数据（有兼容性要求，仅在4.16.0+版本可用）
   - `express.urlencoded`解析URL-encoded格式的请求体数据（有兼容性，仅在4.16.0+版本中可用）

   ```js
   // 配置解析 application/json 格式数据的内置中间件
   app.use(express.json())
   
   // 配置解析 application/x-www-form-urlencoded 格式数据的内置中间件
   app.use(express.urlencoded({ extended: false }))
   ```

   ```js
   const express = require('express')
   const app = express()	// 实例化
   
   // 除了错误级别的中间件，其他中间件必须在路由之前进行配置
   app.use(express.json())	// 中间件解析之后 将数据挂载到req.body
   
   app.use(express.urlencoded({ extended: false }))
   
   app.post('/user', (req, res) => {
   	// 在服务器，可以使用req.body这个属性来接收客户端发送过来的请求体数据（JSON格式/url-encoded格式）
   	// 默认情况下，如果不配置解析表单数据的中间件，则req.body默认=undefined
   	console.log(req.body)
       res.send('ok.')
   })
   
   app.post('/book', (req, res) => {
       console.log(req.body)
       res.send('ok.')
   })
   
   app.listen(80, () => {
       console.log('http://127.0.0.1')
   })
   ```

5. `第三方`的中间件

   非Express官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率。

   例如，在express@4.16.0版本之前，人们经常使用`body-parser`这个第三方中间件来解析请求体数据：

   - 运行`npm install body-parser`安装中间件
   - 使用`require`导入中间件
   - 调用`app.use()`注册并使用中间件

   ```js
   const express = require('express')
   const app = express()	// 实例化
   
   const parser = require('body-parser')
   app.use(parser.urlencoded({ extended: false }))
   
   app.post('/user', (req, res) => {
   	console.log(req.body)
       res.send('ok.')
   })
   
   app.listen(80, () => {
       console.log('http://127.0.0.1')
   })
   ```

#### 3.4 自定义中间件

需求描述：

手动模拟一个类似于express.urlencoded这样的中间件，来**解析POST提交到服务器的表单数据**。

实现步骤：

1. 定义中间件

   ```js
   app.use(function(req, res, next) {
   	// 中间件业务逻辑
   	...
   })
   ```

2. 监听req的`data`事件

   获取客户端发送到服务器的数据。

   如果数据量较大，无法一次性发送完毕，则客户端会**将数据切割后分批发送到服务器**。所以data时间可能会触发多次，每次触发data事件时，**获取到数据只是完整数据的一部分，需要手动对接收到的数据进行拼接**。

   ```js
   // 定义变量 存储客户端发送过来的请求体数据
   let str = ''
   // 监听req对象的data事件
   req.on('data', (chunk) => {
   	// 拼接请求体数据 隐式转换为字符串
   	str += chunk
   })
   ```

3. 监听req的`end`事件

   当请求体数据接收完毕之后，会自动触发req的end事件。

   因此我们可以在req的end事件中，**拿到并处理完整的请求体数据**。

   ```js
   req.on('end', () => {
   	// 打印完整的请求体数据
   	console.log(str)
       // 解析数据
       ...
   })
   ```

4. 使用`querystring`模块解析请求体数据

   Node.js内置了一个`querystring`模块，专门**用来处理查询字符串**。通过模块提供的`parse()`函数，可以轻松把查询字符串解析为对象的格式。示例代码如下：

   ```js
   // 导入处理querystring的Node.js内置模块
   const qs = require('querystring')
   
   // 调用qs.parse()方法，把查询字符串解析为对象
   const body = qs.parse(str)
   ```

5. 将解析出来的数据对象挂载到`req.body`

   ```js
   const express = require('express')
   const app = express()	// 实例化
   
   // 解析表单数据全局中间件
   app.use(function(req, res, next) {
   	// 定义变量 存储客户端发送过来的请求体数据
       let str = ''
       // 监听req对象的data事件
       req.on('data', (chunk) => {
           // 拼接请求体数据 隐式转换为字符串
           str += chunk
       })
       // 监听req对象的end事件
       req.on('end', () => {
           // 打印完整的请求体数据
           console.log(str)
           // 解析数据
           const body = qs.parse(str)
           console.log(body)
           req.body = body
           
           next()	// 调用next()函数 执行后续的业务逻辑
       })
   })
   
   app.post('/user', (req, res) => {
       // 共享req
   	console.log(req.body)
       res.send(req.body)
   })
   
   app.listen(80, () => {
       console.log('http://127.0.0.1')
   })
   ```

6. 将自定义中间件封装为模块

   ```js
   // custom-body-parser.js
   const qs = require('querystring')
   function bodyParser(req, res, next) {
       // 定义变量 存储客户端发送过来的请求体数据
       let str = ''
       // 监听req对象的data事件
       req.on('data', (chunk) => {
           // 拼接请求体数据 隐式转换为字符串
           str += chunk
       })
       // 监听req对象的end事件
       req.on('end', () => {
           // 打印完整的请求体数据
           console.log(str)
           // 解析数据
           const body = qs.parse(str)
           console.log(body)
           req.body = body
           
           next()	// 调用next()函数 执行后续的业务逻辑
       })
   }
   
   module.exports = bodyParser
   ```

   ```js
   // index.js
   const express = require('express')
   const app = express()	// 实例化
   
   // 导入自定义中间件模块
   const myBodyParser = require('custom-body-parser')
   // 注册自定义中间件模块
   app.use(myBodyParser)
   
   app.post('/user', (req, res) => {
       // 共享req
   	console.log(req.body)
       res.send(req.body)
   })
   
   app.listen(80, () => {
       console.log('http://127.0.0.1')
   })
   ```

### 4.使用Express写接口

#### 4.1 搭建基本的服务器

```js
// app.js
// 导入express模块
const express = require('express')
// 创建express服务器实例
const app = express()

// 调用app.listen方法，指定端口号并启动Web服务
app.listen(80, () => {
	console.log('Express server running at http://127.0.0.1')
})
```

#### 4.2 创建API路由模块

```js
// apiRouter.js 路由模块
const express = require('express')
const apiRouter = express.Router()

// 挂载对应的路由
...

module.exports = apiRouter
```

```js
// app.js
...

// 导入注册路由模块
const apiRouter = require('./apiRouter.js')
app.use('/api', apiRouter)

...
```

#### 4.3 编写GET接口

```js
apiRouter.get('/get', (req, res) => {
	// 获取到客户端通过查询字符串发送到服务器的数据
	const query = req.query
	// 调用send()方法把数据响应给客户端
	res.send({
		status: 0,	// 0 成功 1 失败
		msg: 'GET请求成功！',	// 状态描述
		data: query,	// 响应给客户端的具体数据
	})
})
```

#### 4.4 编写POST接口

```js
apiRouter.post('/post', (req, res) => {
	// 获取客户端通过请求体发送到服务器的URL-encoded数据
	const body = req.body
	// 调用send()方法把数据响应给客户端
	res.send({
		status: 0,	// 0 成功 1 失败
		msg: 'POST请求成功！',	// 状态描述
		data: body,	// 响应给客户端的具体数据
	})
})
```

注意：若要获取`URL-encoded`格式的请求数据，必须配置中间件`app.use(express.urlencoded({ extended: false }))`

#### 4.5 CORS跨域资源共享

1. 接口`跨域问题`

   ```html
   <button id="btnGET">GET</button>
   <button id="btnPOST">POST</button>
   ```

   ```html
   <script>
   	$(function() {
           // 1.测试GET接口
           $('#btnGET').on('click', function() {
               $.ajax({
                   type: 'GET',
                   url: 'http://127.0.0.1/api/get',
                   data: {
                       name: 'zs',
                       age: 20
                   },
                   success: function(res) {
                       console.log(res)
                   }
               })
           })
           // 2.测试POST接口
           $('#btnPOST').on('click', function() {
               $.ajax({
                   type: 'POST',
                   url: 'http://127.0.0.1/api/post',
                   data: {
                       bookname: '水浒传',
                       author: '施耐庵'
                   },
                   success: function(res) {
                       console.log(res)
                   }
               })
           })
       })
   </script>
   ```

   ![image-20231018140532514](https://gitee.com/v876774538/my-img/raw/master/image-20231018140532514.png)

2. 解决跨域问题的方案

   - `CORS`（推荐）
   - `JSONP`（有缺陷，只支持GET）

3. 使用`CORS`中间件解决跨域问题

   CORS是Express的一个第三方中间件。通过安装和配置CORS中间件，可以很方便地解决跨域问题。

   - 运行`npm install cors`安装中间件
   - 使用`const cors = require('cors')`导入中间件
   - **在路由之前**，调用`app.use(cors())`配置中间件

4. 什么是CORS

   CORS(Cross-Origin Resource Sharing, 跨域资源共享)，是由一系列`HTTP响应头`通组成的，这些HTTP响应头**决定了浏览器是否阻止前端JS代码跨域获取资源**。

   **浏览器**的**同源安全策略**默认会**阻止网页跨域获取资源**，但如果接口服务器配置了CORS相关的HTTP响应头，就可以**解除浏览器端的跨域访问限制**。

   ![image-20231018141706410](https://gitee.com/v876774538/my-img/raw/master/image-20231018141706410.png)

5. CORS注意事项

   - CORS主要在`服务器端`进行配置。客户端浏览器无需做任何额外的配置即可请求开启了CORS的接口；
   - CORS在浏览器中有兼容性要求。只支持XMLHttpRequest Level2的浏览器（例如：IE10+、Chrome4+、FireFox3.5+）

6. CORS响应头

   - `Access-Control-Allow-Origin`

     响应头部可以携带一个`Access-Control-Allow-Origin`字段，其语法如下：

     ```http
     Access-Control-Allow-Origin: <origin> | *
     ```

     其中，origin参数的值指定了**允许访问该资源的外域URL**。

     例如，指定允许来自http://itcast.cn的请求：

     ```js
     res.setHeader('Access-Control-Allow-Origin', 'http://itcast.cn')
     ```

     `*`通配符，表示允许来自任何域的请求：

     ```js
     res.setHeader('Access-Control-Allow-Origin', '*')
     ```

   - `Access-Control-Allow-Header`

     默认情况下，CORS仅支持**客户端向服务器**发送如下的9个请求头：

     > `Accept`、`Accept-Language`、`Content-Language`、`DPR`、`Downlink`、`Save-Data`、`Viewport-Width`、`Width`、`Content-Type`（值仅限于text/plain、multipart/form-data、application/x-www-form-urlencoded三者之一）

     如果客户端向服务器发送了额外的请求头信息，则需要在服务器端通过`Access-Control-Allow-Header`**对额外的请求头进行声明**，否则请求将会失败！

     ```js
     // 多个请求头之间用英文逗号分隔
     res.setHeader('Access-Control-Allow-Headers', 'Content-Type, X-Custom-Header')
     ```

   - `Access-Control-Allow-Methods`

     默认情况下，**CORS仅支持客户端发起`GET`、`POST`、`HEAD`请求**。

     如果客户端希望通过`PUT`、`DELETE`等方式请求服务器资源，需要在服务器端通过`Access-Control-Allow-Methods`来**指明实际请求所允许使用的HTTP方法**。

     ```js
     res.setHeader('Access-Control-Allow-Methods', 'POST, GET, DELETE, HEAD')
     
     // 允许所有的HTTP请求方法
     res.setHeader('Access-Control-Allow-Methods', '*')
     ```

7. CORS请求分类

   **根据请求方式和请求头的不同**，可以将CORS请求分为两大类，分别是：

   - 简单请求

     同时满足以下两大条件的请求，就属于简单请求：

     - `请求方式`：GET、POST、HEAD三者之一
     - `HTTP头部信息`不超过以下几种字段：**无自定义头部字段**、Accept、Accept-Language、Content-Language、DPR、Downlink、Sava-Data、Viewport-Width、Width、Content-Type（值仅限于text/plain、multipart/form-data、application/x-www-form-urlencoded三者之一）

   - 预检请求

     > **在浏览器与服务器正式通信之前，浏览器会先发送OPTION请求进行预检**，以获知服务器是否允许该实际请求，所以这一次的OPTION请求成为预检请求。
     >
     > 服务器成功响应预检请求后，才会发送真正的请求，并携带真实数据。

     只要符合以下任何一个条件的请求，都需要进行预检请求：

     - 请求方式为GET、POST、HEAD之外的请求Method类型
     - 请求头中包含自定义头部字段
     - 向服务器发送了`application/json`格式的数据（Content-Type的值）

   `简单请求`和`预检请求`之间的区别：

   - 简单请求的客户端与服务器之间只会发生一次请求；

   - 预检请求的客户端与服务器之间会发生两次请求：OPTION预检请求成功之后，才发起真正的请求。

     ![image-20231018150553568](https://gitee.com/v876774538/my-img/raw/master/image-20231018150553568.png)

#### 4.6 JSONP接口

1. 概念

   浏览器通过`<script>`标签的`src`属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式成为JSONP。

2. 特点

   - JSONP不属于真正的Ajax请求，因为它没有使用`XMLHttpRequest`这个对象
   - JSONP仅支持GET请求，不支持POST、PUT、DELETE等请求方式

3. 创建JSONP接口的注意事项

   **如果项目总能已经配置了CORS跨域资源共享，那么为了防止冲突，必须在配置CORS中间件之前声明JSONP的接口**，否则JSONP接口会被处理成开启了CORS的接口：

   ```js
   // 优先创建JSONP接口
   app.get('/api/jsonp', (req, res) => {
   	...
   })
   
   // 再配置CORS中间件
   app.use(cors())
   
   // 这是一个开启了CORS的接口
   app.get('/api/get', (req, res) => {
   
   })
   ```

4. 实现JSONP接口的步骤

   - 获取客户端发送的`回调函数的名字`
   - 得到要通过JSONP形式`发送给客户端的数据`
   - 根据前两步骤得到的数据，`拼接出一个函数调用的字符串`
   - 把上一步拼接得到的字符串，响应给客户端的`<script>`标签进行解析执行

   ```js
   app.get('/api/jsonp', (req, res) => {
   	// 获取客户端发送过来的回调函数的名字
   	const funcName = req.query.callback	// 前端发起JSONP请求 会自动携带一个callback = jQueryXXXXX的参数 jQueryXXXXX是随机生成的一个回调函数名称
   	// 得到要通过JSONP形式发送给客户端的数据
   	const data = {
   		name: 'zs',
   		age: 22
   	}
   	// 根据前两步得到的数据，拼接出一个函数调用的字符串
   	const scriptStr = `${funcName}(${JSON.stringify(data)})`
   	// 把上一步拼接得到的字符串响应给客户端的<script>标签进行解析执行
   	res.send(scriptStr)
   })
   ```

5. 在网页中使用jQuery发起JSONP请求

   调用`$.ajax()`函数，提供JSONP的配置选项，从而发起JSONP请求：

   ```js
   $('#btnJSONP').on('click', function() {
   	$.ajax({
   		method: 'GET',
   		url: 'http://127.0.0.1/api/jsonp',
   		dataType: 'jsonp',
   		success: function(res) {
   			console.log(res)
   		}
   	})
   })
   ```

   ![image-20231018152505063](https://gitee.com/v876774538/my-img/raw/master/image-20231018152505063.png)

#### 4.7 完整代码

```js
// app.js
// 导入express模块
const express = require('express')
// 创建express服务器实例
const app = express()

// cors中间件 解决跨域问题
const cors = require('cors')
app.use(cors())

// 配置解析表单数据的中间件
app.use(express.urlencoded({ extended: false }))

// 导入注册路由模块
const apiRouter = require('./apiRouter.js')
app.use('/api', apiRouter)

// 调用app.listen方法，指定端口号并启动Web服务
app.listen(80, () => {
	console.log('Express server running at http://127.0.0.1')
})
```

```js
// apiRouter.js 路由模块
const express = require('express')
const apiRouter = express.Router()

// 挂载对应的路由
apiRouter.get('/get', (req, res) => {
	// 获取到客户端通过查询字符串发送到服务器的数据
	const query = req.query
	// 调用send()方法把数据响应给客户端
	res.send({
		status: 0,	// 0 成功 1 失败
		msg: 'GET请求成功！',	// 状态描述
		data: query,	// 响应给客户端的具体数据
	})
})

apiRouter.post('/post', (req, res) => {
	// 获取客户端通过请求体发送到服务器的URL-encoded数据
	const body = req.body
	// 调用send()方法把数据响应给客户端
	res.send({
		status: 0,	// 0 成功 1 失败
		msg: 'POST请求成功！',	// 状态描述
		data: body,	// 响应给客户端的具体数据
	})
})

module.exports = apiRouter
```

### 5.MySQL

#### 5.1 数据库的基本概念

1. 数据库

   `数据库`(database)是用来**组织、存储和管理数据的仓库**。

   当今世界是一个充满数据的互联网世界。数据的来源很多，比如出行记录、消费记录、浏览的网页、发送的消息等等。除了文本类型的数据，图像、声音都是数据。

   为了方便管理互联网世界中的数据，`数据库管理系统`（简称：数据库）的概念应运而生。用户可以对数据库中的数据进行**新增、删除、更新、查询**（增删改查）等的操作。

2. 常见数据库及分类

   - `MySQL`数据库（目前使用范围最广、流行度最高的开源免费数据库）
   - Oracle数据库（收费）
   - SQL Server数据库（收费）
   - Mongodb数据库

   其中，MySQL、Oracle、SQL Server属于`传统型数据库`（关系型数据库/SQL数据库）；而Mongodb属于`新型数据库`（非关系型数据库/NoSQL数据库），它在一定程度上弥补了传统型数据库的缺陷。

3. 传统型数据库的数据组织结构

   传统型数据库的数据组织结构，与Excel中数据的组织结构类似。

   - Excel数据组织结构

     每个Excel中，数据的组织结构分别为`工作簿`、`工作表`、`数据行`、`列`这4大部分组成：

     ![image-20231018163454709](https://gitee.com/v876774538/my-img/raw/master/image-20231018163454709.png)

   - 传统型数据库的数据组织结构

     在传统型数据库中，数据的组织结构分为`数据库(database)`、`数据表(table)`、`数据行(row)`、`字段(field)`组成。

     ![image-20231018163633939](https://gitee.com/v876774538/my-img/raw/master/image-20231018163633939.png)

   - 实际开发中库、表、行、字段的关系

     在实际开发中，一般情况下，每个项目都对应**独立的数据库**。

     不同的数据，要存储到数据库的不同**表**中，例如：用户数据存储到`users`表中，图书数据存储到`books`表中；

     每个表中具体存储哪些信息，由**字段**来决定，例如：我们可以为`users`表设计`id`、`username`、`password`这3个字段；

     表中的行，代表**每一条具体的数据**。

#### 5.2 安装并配置MySQL

1. 需要安装的软件

   - `MySQL Server`：专门用来**提供数据存储和服务**的软件；
   - `MySQL Workbench`：**可视化的MySQL管理工具**，通过它可以方便地操作存储在MySQL Server中的数据

2. Windows环境下安装

   运行`mysql-installer-comunity-8.0.19.0.msi`安装包，即可一次性将MySQL Server和MySQL Workbench安装到电脑上。

   > 具体安装教程可参见 素材 -> MySQL for Windows -> 安装教程 - Windows系统安装MySql -> README.md

   ![image-20231018174906089](https://gitee.com/v876774538/my-img/raw/master/image-20231018174906089.png)

   黑马教程：https://www.bilibili.com/video/BV1a34y167AZ/?p=59&spm_id_from=333.880.my_history.page.click&vd_source=c4ed744f2963d241685bef44e5cbfc8b

#### 5.3 MySQL基本使用

1. Workbench的基本用法

   - 连接数据库

   ![image-20231019145050816](https://gitee.com/v876774538/my-img/raw/master/image-20231019145050816.png)

   - MySQL Workbench主界面组成部分

     ![image-20231019145245311](https://gitee.com/v876774538/my-img/raw/master/image-20231019145245311.png)

     ![image-20231019145329321](https://gitee.com/v876774538/my-img/raw/master/image-20231019145329321.png)

   ​	点击控制三个区域的显示隐藏。

   - 创建数据库

     ![image-20231019145502713](https://gitee.com/v876774538/my-img/raw/master/image-20231019145502713.png)

   ​	注意：数据库名称不要使用中文及空格，间隔尽量使用`_`

   - 创建数据表

     ![image-20231019145808626](https://gitee.com/v876774538/my-img/raw/master/image-20231019145808626.png)

     DataType数据类型：

     - `int`整数
     - `varchar(len)`字符串
     - `tinyint(1)`布尔值

     字段特殊标识：

     - `PK`(Primary Key)主键、唯一标识
     - `NN`(Not Null)值不允许为空
     - `UQ`(Unique)值唯一
     - `AI`(Auto Increment)值自动增长

     > id设为PK、NN、AI。

     ![image-20231019150728125](https://gitee.com/v876774538/my-img/raw/master/image-20231019150728125.png)

   - 向表中写入数据

     ![image-20231019150932405](https://gitee.com/v876774538/my-img/raw/master/image-20231019150932405.png)

2. 使用SQL管理数据库

   - SQL

     SQL(Structured Query Language)是`结构化查询语言`，专门用来`访问和处理数据库`的**编程语言**。能够让我们**以编程的形式，操作数据库里的数据**。

     - SQL是一门`数据库编程语言`
     - 使用SQL语言编写的代码叫做`SQL语句`
     - SQL语言只能在`关系型数据库`中使用

   - 作用

     对数据库进行增删改查，创建新数据库、表，创建存储过程、视图等。

   - `SELECT`语句

     `SELECT`语句用于从表中`查询`数据。执行的结果被存储在一个`结果表`（结果集）中，语法格式如下：

     ```sql
     -- 注释
     -- 从 FROM 指定的【表】中，查询出【所有的】数据
     -- * 表示【所有列】
     SELECT * FROM 表名称
     
     -- 从 FROM 指定的【表】中，查询出指定【列名称（字段）】的数据
     SELECT 列名称 FROM 表名称
     ```

     注意：SQL语句中的`关键字`对`大小写不敏感`。

     ```sql
     SELECT username, password FROM  users
     ```

     ![image-20231019153942266](https://gitee.com/v876774538/my-img/raw/master/image-20231019153942266.png)

   - `INSERT INTO`语句

     `INSERT INTO`语句用于向数据表中`插入`新的数据行。语法格式如下：

     ```sql
     -- 向指定的表中，插入如下几列数据，列的值通过 values 来一一指定
     -- 注意：列合值要一一对应，多个列合多个值之间，使用英文逗号分隔
     INSERT INTO 表名称 (列1, 列2, ...) VALUES （值1, 值2, ...）
     ```

     ```sql
     -- 插入一条username为'Tony Stark'，password为'098123'的数据
     INSERT INTO users (username, password) VALUES ('Tony Stark', '098123')
     ```

     ![image-20231019154419299](https://gitee.com/v876774538/my-img/raw/master/image-20231019154419299.png)

   - `UPDATE`语句

     `UPDATE`语句用于`修改`表中的数据。语法格式如下：

     ```sql
     -- UPDATE 指定更新的表
     -- SET 指定列对应的新值
     -- WHERE 指定更新的条件
     UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
     ```

     ```sql
     -- 把users表中id为4的用户密码更新为888888
     UPDATE users SET password = '888888' WHERE id = 4
     ```

     ```sql
     -- 把users表中id为2的用户密码和用户状态，分别更新为admin123和1
     UPDATE users SET password = 'admin123', status = 1 WHERE id = 2
     ```

   - `DELETE`语句

     `DELETE`语句用于`删除`表中的行。语法格式如下：

     ```sql
     -- 从指定的表中，根据 WHERE 条件，删除对应的数据行
     DELETE FROM 表名称 WHERE 列名称 = 值
     ```

     ```sql
     -- 从users表中删除id为4的用户
     DELETE FROM users WHERE id = 4
     ```

   - `WHERE`子句

     `WHERE`子句用于`限定`选择的标准。在SELECT、UPDATE、DELETE语句中，皆可使用`WHERE`子句来限定选择的标准。

     可以在WHERE子句中使用的**运算符**：

     | 操作符  |     描述     |
     | :------ | :----------: |
     | =       |     等于     |
     | <> / != |    不等于    |
     | >       |     大于     |
     | <       |     小于     |
     | >=      |   大于等于   |
     | <=      |   小于等于   |
     | BETWEEN | 在某个范围内 |
     | LIKE    | 搜索某种模式 |

     ```sql
     -- 查询 status 为1的所有用户信息
     SELECT * FROM users WHERE status = 1
     
     -- 查询 id 大于 2 的所有用户
     SELECT * FROM users WHERE id > 2
     
     -- 查询 username 不等于 admin 的所有用户
     SELECT * FROM users WHERE username != 'admin'
     ```

   - `AND`和`OR`运算符

     `AND`和`OR`运算符可以在WHERE子语句中**把两个或多个条件结合起来**。`AND`相当于且（js中的`&&`）；`OR`相当于或（js中的`||`）。

     ```sql
     -- 显示所有 status 等于0 且 id 小于3 的用户
     SELECT * FROM users WHERE status = 0 AND id < 3
     
     -- 显示所有 status 等于1 或 username 为zs的用户
     SELECT * FROM users WHERE status = 1 OR username = 'zs'
     ```

   - `ORDER BY`子句

     `ORDER BY`语句用于**根据指定的列**对**结果集**进行`排序`。

     `ORDER BY`语句默认按照`升序`对记录进行排序，升序关键字`ASC`；`降序`排列需要使用`DESC`关键字。

     ```sql
     -- 对users表中的数据按照status字段进行升序排序
     SELECT * FROM users ORDER BY status
     SELECT * FROM users ORDER BY status ASC
     
     -- 对users表中的数据按照id字段进行降序排序
     SELECT * FROM users ORDER BY id DESC
     ```

     **多重排序**：

     ```sql
     -- 对users表中的数据 先按照status字段进行降序排序 再按照usersname的字母顺序进行升序排序
     SELECT * FROM users ORDER BY status DESC, username ASC
     ```

   - `COUNT(*)`函数

     `COUNT(*)`函数用于返回查询结果的`总数据条数`。语法格式如下：

     ```sql
     SELECT COUNT(*) FROM 表名称
     ```

     ```sql
     -- 查询users表中status为0的总数据条数
     SELECT COUNT(*) FROM users WHERE status = 0
     ```

   - `AS`关键字

     使用`AS`关键字**给列设置别名**。示例如下：

     ```sql
     SELECT 列名 AS 别名 FROM 表名
     ```

     ```sql
     -- 使用AS关键字为COUNT列起别名
     SELECT COUNT(*) AS total FROM users WHERE status = 0
     
     -- username别名uname password别名upwd
     SELECT username AS uname, password AS upwd FROM users
     ```

#### 5.4 在Express中操作MySQL

1. 安装MySQL数据库第三方模块(`mysql`)

   ```shell
   npm install mysql
   ```

2. 通过mysql模块连接到MySQL数据库

   **`配置`mysql模块**：

   ```js
   // 导入mysql模块
   const mysql = require('mysql')
   // 建立MySQL数据库连接
   const db = mysql.createPool({
   	host: '127.0.0.1',	// 数据库IP地址
   	user: 'root',		// 登录数据库的账号
   	password: 'admin123',// 登录数据库的密码
   	database: 'my_db_01',// 指定操作的数据库
   })
   ```

3. 通过mysql模块执行SQL语句

   **测试mysql模块能否正常工作**：

   ```js
   // 调用query()函数，指定要执行的SQL语句
   db.query('SELECT 1', (err, res) => {
   	if (err) {
   		console.log(err.message)
   		return false
   	}
   	console.log(res)	// 打印[ RowDataPacket { '1': 1 } ]的结果，就证明数据库连接正常
   })
   ```

4. 查询数据

   ```js
   // 查询users表中的所有数据
   db.query('SELECT * FROM users', (err, res) => {
   	// 查询失败
   	if (err) {
   		console.log(err.message)
   		return false
   	}
   	// 查询成功
   	console.log(res)
   })
   ```

   ![image-20231019171702422](https://gitee.com/v876774538/my-img/raw/master/image-20231019171702422.png)

5. 插入数据

   ```js
   // 向users表中新增数据，其中username为'Spider-Man'，password为'pcc321'
   // 定义要插入的数据
   const user = {
       username: 'Spider-Man',
       password: 'pcc321'
   }
   // 待执行的sql语句
   // ?表示占位符
   const sqlStr = 'INSERT INTO users (username, password) VALUES (?, ?)'
   // 使用数组的形式依次为?占位符指定具体的值
   db.query(sqlStr, [user.username, user.password], (err, res) => {
       if (err) return console.log(err.message)
       // affectedRows 受影响的行数
       if (res.affectedRows == 1) {
           console.log('插入数据成功')
       }
   })
   ```

   向表新增数据时，如果`数据对象的每个属性`和`数据表的字段`**一一对应**，可以通过如下方式**快速插入数据**：

   ```js
   // 向users表中新增数据，其中username为'Spider-Man'，password为'pcc321'
   // 定义要插入的数据
   const user = {
       username: 'Spider-Man',
       password: 'pcc321'
   }
   // 待执行的sql语句
   // ?表示占位符
   const sqlStr = 'INSERT INTO users SET ?'
   // 直接将数据对象当做占位符的值
   db.query(sqlStr, user, (err, res) => {
       if (err) return console.log(err.message)
       // affectedRows 受影响的行数
       if (res.affectedRows == 1) {
           console.log('插入数据成功')
       }
   })
   ```

6. 更新数据

   ```js
   // 要更新的数据对象
   const user = {
   	id: 7,
   	username: 'aaa',
   	password: '000'
   }
   // 要执行的sql语句
   const sqlStr = 'UPDATE users SET username = ?, passowrd = ? WHERE id = ?'
   // 使用数组依次为占位符指定具体的值
   db.query(sqlStr, [user.username, user.password, user.id], (err, res) => {
       if (err) return console.log(err.message)
       if (res.affectedRows == 1) {
           console.log('更新数据成功')
       }
   })
   ```

   更新表数据时，如果`数据对象的每个属性`和`数据表的字段`**一一对应**，可以通过如下方式**快速更新数据**：

   ```js
   // 要更新的数据对象
   const user = {
   	id: 7,
   	username: 'aaa',
   	password: '000'
   }
   // 要执行的sql语句
   const sqlStr = 'UPDATE users SET ? WHERE id = ?'
   // 使用数组依次为占位符指定具体的值
   db.query(sqlStr, [user, user.id], (err, res) => {
       if (err) return console.log(err.message)
       if (res.affectedRows == 1) {
           console.log('更新数据成功')
       }
   })
   ```

7. 删除数据

   ```js
   // 要执行的SQL语句
   const sqlStr = 'DELETE FROM users WHERE id = ?'
   // 调用db.query()执行SQL语句的同时，为占位符指定具体的值
   // 注意：若SQL语句中存在多个占位符，必须使用数组为每个占位符指定具体的值；如果仅有一个占位符，可以省略数组
   db.query(sqlStr, 7, (err, res) => {
   	if (err) return console.log(err.message)
       if (res.affectedRows == 1) {
           console.log('删除数据成功')
       }
   })
   ```

8. 标记删除

   使用`DELETE`语句，会真正地把数据从表中删除（硬删除）。为了保险起见，推荐使用`标记删除`，来**模拟删除的动作**（软删除，便于恢复）。

   所谓的标记删除，就是在表中设置类似于`status`这样的**状态字段**，用来**标记当前这条数据是否被删除**。

   当用户执行了删除操作时，并不去执行`DELETE`语句直接将数据删除，而是执行`UPDATE`语句，将这条数据对应的`status`字段标记为删除即可。

   ```js
   db.query('UPDATE users SET status = 1 WHERE id = ?'， 6， (err, res) => {
   	if (err) return console.log(err.message)
       if (res.affectedRows == 1) {
           console.log('删除数据成功')
       }
   })
   ```

#### 5.5 前后端的身份认证











