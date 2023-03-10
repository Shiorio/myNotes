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

   

