# TypeScript

## 一、快速入门

### 1.初识TypeScript

#### 1.1 TypeScript介绍

TypeScript是一种由微软开发的开源、跨平台的编程语言。它是**JavaScript的超集**，**最终会被编译为JavaScript代码**。

> 2012年10月，微软发布了首个公开版本的TypeScript，2013年6月19日，在经历了一个预览版之后微软正式发布了正式版TypeScript。
>
> TypeScript的作者是安德斯·海尔斯伯格，C#的首席架构师。它是开源和跨平台的编程语言。
>
> TypeScript扩展了JavaScript的语法，所以任何现有的JavaScript程序可以运行在TypeScript环境中。
>
> TypeScript是**为大型应用的开发而设计**，并且可以编译为JavaScript。
>
> **TypeScript 是 JavaScript 的一个超集**，主要提供了**类型系统**和**对 ES6+ 的支持**，它由 Microsoft 开发，代码[开源于 GitHub (opens new window)](https://github.com/Microsoft/TypeScript)上。

![image-20230224174405964](https://gitee.com/v876774538/my-img/raw/master/image-20230224174405964.png)

#### 1.2 TypeScript特点

1. 始于JavaScript，归于JavaScript

   TypeScript可以编译出纯净、简介的JavaScript代码，并且**可以运行在任何浏览器上、Node.js环境中和任何支持ECMAScript3（或更高版本）的JavaScript引擎中**。

2. 强大的类型系统

   **类型系统**允许JavaScript开发者卡在开发JavaScript应用程序时使用高效的开发工具和常用操作，如**静态检查**和**代码重构**。

3. 先进的JavaScript

   TypeScript提供最新和不断发展的JavaScript特性，包括那些来自2015年的ECMAScript和未来的提案中的特性，比如异步功能和Decorators，以帮助建立健壮的组件。

### 2.TypeScript开发环境搭建

1. 下载Node.js

   - 64位：http://nodejs.org/dist/v14.15.1/node-v14.15.1-x64.msi
   - 32位：http://nodejs.org/dist.v14.15.1/node-v14.15.1-x86.msi

2. 安装Node.js

3. 全局安装typeScript

   ```sh
   npm install -g typescript
   ```

4. 安装检查

   ```sh
   tsc -V
   ```

5. 创建一个ts文件

6. 使用tsc对ts文件进行编译

   - 进入命令行

   - 进入ts文件所在目录

   - 执行命令：

     ```sh
     tsc xxx.ts
     ```

### 3.第一个TypeScript程序

#### 3.1 编写TS程序

`/typeScript/helloworld.ts`

```ts
function greeter(person) {
	return 'Hello,' + person
}

let user = 'Shiori'
console.log(greeter(user))
```

#### 3.2 手动编译代码

命令行运行TypeScript编译器：

```sh
tsc helloworld.ts
```

![image-20230227145106046](https://gitee.com/v876774538/my-img/raw/master/image-20230227145106046.png)

#### 3.3 vscode自动编译

1. 生成配置文件`tsconfig.json`

   ```sh
   tsc --init
   ```

2. 修改`tsconfig.json`配置

   ```sh
   "outDir": "./js",
   "strict": false,
   ```

3. 启动监视任务

   终端 -> 运行任务 -> 监视tsconfig.json

### 4.基本类型

#### 4.1 类型声明

- 类型声明是TS非常重要的一个特点，通过类型声明可以指定TS在变量（形参、实参）的类型。
- 指定类型后，当为变量赋值时，TS编译器会自动检查值是否符合类型声明，符合则成功赋值，反之则报错。
- 简而言之，**类型声明给变量设置了类型，使得变量只能存储某种类型的值**。

```ts
let 变量: 类型;
let 变量: 类型 = 值;
function fn(参数: 类型, 参数:类型): 类型 {
	...
    return ...
}
    
function fn1(参数: 类型, 参数:类型) => 类型 {
    ...
    return ...
}
```

#### 4.2 自动类型判断

- TS拥有自动类型判断机制。

- 当对变量的声明和赋值同时进行时，TS编译器会自动判断变量的类型，因此如果你的变量声明和赋值同时进行，可以省略类型声明。

  ```ts
  let c: boolean = false;
  
  let c = false;
  ```

#### 4.3 类型

|    类型     |       例子        |                          描述                           |
| :---------: | :---------------: | :-----------------------------------------------------: |
|   number    |    1, -33, 2.5    |                        任意数字                         |
|   string    | 'hi', "hi", `hi`  |                       任意字符串                        |
|   boolean   |    true、false    |                    布尔值true或false                    |
|   字面量    |      其本身       |              限制变量的值就是该字面量的值               |
|     any     |         *         |          任意类型（可以赋值给别的类型的变量）           |
| **unknown** |         *         | 未知类型，**类型安全的any**（无法赋值给别的类型的变量） |
|    void     | 空值（undefined） |      没有值（或undefined），主要用作**函数返回值**      |
|    never    |      没有值       |       不能是任何值，主要用作**函数返回（报错）**        |
|   object    |  {name:'孙悟空'}  |                      任意的JS对象                       |
|    array    |      [1,2,3]      |                       任意JS数组                        |
|    tuple    |       [4,5]       |           元素，TS新增类型，**固定长度数组**            |
|    enum     |    enum{A, B}     |                 **枚举**，TS中新增类型                  |

- number

  ```ts
  let decimal: number = 6;	// 10进制
  let hex: number = 0xf00d;	// 十六进制
  let binary: number = 0b1010;	// 二进制
  let octal: number = 0o744;	// 八进制
  let big: bigint = 100n;	// 大整型
  ```

- boolean

  ```ts
  let isDone: boolean = false;
  ```

- string

  ```ts
  let color: string = "blue";
  color = 'red';
  
  let fullName: string = 'Bob Bobbington';
  let sentence: string = `Hello, my name is ${fullName}`
  ```

- 字面量

  使用字面量**指定变量的类型**，通过**字面量可以确定变量的取值范围**

  ```ts
  let color: 'red' | 'blue' | 'black';
  let num: 1 | 2 | 3 | 4 | 5;
  
  let id: string | number;	// 使用|连接多个类型（联合类型）
  ```

- any

  ```ts
  let d: any = 4;
  d = 'hello';
  d = true;
  ```

- unknown

  ```ts
  let notSure: unknown = 4;
  notSure = 'hello'
  ```

- void

  ```ts
  let unusable: void = undefined;
  ```

- never

  ```ts
  function error(message: string): never {
  	throw new Error(message)
  }
  ```

- object

  ```ts
  let obj: object = {};
  
  let obj: { name: string, age?: number };	// 限制对象属性	// ?表示可选属性
  obj = { name: '孙悟空' }
  
  let obj:{ name:string, [propName: string]: any };	// name加任意字符串属性名
  c = { name: '孙悟空', age: 18, gender: '男'}
  ```

- array

  ```ts
  let list: number[] = [1, 2, 3];
  let list: Array<number> = [1, 2, 3];
  ```

- tuple

  ```ts
  let x: [string, number];	// 元组 类型和长度固定的数组 => tuple
  x = ["hello", 10];
  ```

- enum

  ```ts
  // 类似数据库字典
  enum Color {
  	Red = 1,
  	Green = 2,
  	Blue = 4,
  }
  
  let c: Color = Color.Green;
  
  enum Sex {
      male = 0,
      female = 1,
  }
  
  let i: { name: string, sex: Sex };
  i = {
      name: '孙悟空',
      sex: sex.male
  }
  console.log(i == Sex.male)
  ```

- 类型断言

  在有些情况下，变量的类型对于我们来说是很明确的，但是TS编译器却并不清楚。

  此时，我们可以通过**类型断言**（断言，判断的语言）来**告诉编译器变量的类型**，断言有以下两种形式：

  - ```ts
    let someValue: unknown = "this is a string";
    let strLength: number = (someValue as string).length;
    ```

  - ```ts
    let someValue: unknown = "this is a string";
    let strLength: number = (<string>someValue).length;
    ```

- 类型别名

  ```ts
  type myType = string;
  let m: myType;
  
  type myType1 = 1 | 2 | 3 | 4 | 5;
  let k: myType1;
  let l: myType1;
  ```

### 5.编译选项

#### 5.1 自动编译文件

- 编译那件时，使用`-w`（监视）指令后，TS编译器会自动监视文件的变化，并在文件发生变动时自动对文件进行重新编译。

- 示例：

  ```sh
  tsc xxx.ts -w
  ```

  ![image-20230227162412929](https://gitee.com/v876774538/my-img/raw/master/image-20230227162412929.png)

#### 5.2 自动编译整个项目

- 直接使用`tsc`命令，就可以自动将当前项目下的所有ts文件编译为js文件

- 但是能直接使用tsc命令的前提是，要先在项目根目录下创建一个ts的配置文件`tsconfig.json`

- 配置选项：

  - `include`

    指定需要被编译文件所在的目录

    默认值：`["**/*"]`

    ```json
    "include": ["src/**/*", "tests/**/*"]
    ```

    上述示例中，所有src目录和tests目录下文件都会被编译。

  - `exclude`

    定义需要排除在外的目录

    默认值：`["node_modules", "bower_components", "jspm_packages]`

    ```json
    "exclude": ["./src/hello/**/*"]
    ```

    上述示例中，src下hello目录下的文件都不会被编译。

  - `extends`

    定义被继承的配置文件

    ```json
    "extends": "./configs/base"
    ```

    当前配置文件中会自动包含config目录下base.json中的所有配置信息，类似于引入一个外部文件。

  - `files`

    指定被编译文件的列表，只有需要编译文件较少时才会用到

    ```json
    "files": [
        "core.ts",
        "sys.ts",
        "types.ts",
        "scanner.ts",
        "parser.ts",
        "utilities.ts",
        "binder.ts",
        "checker.ts",
        "tsc.ts"
    ]
    ```

    上述列表中的文件都会被TS编译器所编译。

  - **`compilerOptions`**

    在compilerOptions中包含多个子选项，用来完成对编译的配置。

    1. 项目选项

       - `target`

         设置ts代码编译的目标版本

         可选值：ES3（默认）、ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext

         ```json
         "compilerOptions": {
             "target": "ES6"
         }
         ```

       - `lib`

         指定代码运行时所包含的库（宿主环境，依赖库）

         可选值：ES5、ES6/ES2015、ES7/ES2016、ES2017、ES2018、ES2019、ES2020、ESNext、DOM、WebWorker、ScriptHost……

         ```json
         "compilerOptions": {
             "target": "ES6",
             "lib": ["ES6", "DOM"],
             "outDir": "dist",
             "outFile": "dist/aa.js"
         }
         ```

       - `module`

         设置编译后代码使用的模块系统

         可选值：CommonJS、UMD、AMD、System、ES2020、ESNext、None

         ```json
         "compilerOptions": {
             "module": "CommonJS"
         }
         ```

       - `outDir`

         指定编译后文件的所在目录

         默认情况下，编译后的js文件会和ts文件位于相同目录

         ```json
         "compilerOptions": {
             "outDir": "dist"
         }
         ```

         设置后编译后的js文件将会生成到dist目录。

       - `outFile`

         **将所有的文件编译为一个js文件**

         默认会将所有的编写在全局作用域中的代码合并为一个js代码，如果module指定了None、System或AMD，则会将模块一起合并到文件之中

         后期使用打包工具配合合并。

         ```json
         "compilerOptions": {
             "outFile": "dist/app.js"
         }
         ```

       - `rootDir`

         **指定代码的根目录**，默认情况下编译后文件的目录结构会以最长的公共目录为根目录，通过rootDir可以手动指定根目录

         ```json
         "compilerOptions": {
             "rootDir": "./src"
         }
         ```

       - `allowJs`

         定义是否对js文件进行编译，默认false

       - `checkJs`

         是否对js文件进行检查，默认false

         ```json
         "compilerOptions": {
             "allowJs": true,
             "checkJs": true
         }
         ```

       - `removeComments`

         是否删除注释，默认false

       - `noEmit`

         不对代码进行编译，不生成编译文件，默认false

       - `sourceMap`

         是否生成sourceMap

         默认值：false

    2. 严格检查

       - **`strict`**

         启用所有的严格检查，默认值为true，设置后相当于开启了所有的严格检查（总开关）

       - `alwaysStrict`

         总是以严格模式对代码进行编译

       - `noImplicitAny`

         禁止隐式的any类型

       - `noImplicitThis`

         禁止类型不明确的this

       - `strictBindCallApply`

         严格检查bind、call和apply的参数列表

       - `strictFunctionTypes`

         严格检查函数的类型

       - `strictNullChecks`

         严格的空值检查

       - `strictPropertyInitialization`

         严格检查属性是否初始化

    3. 额外检查

       - `noFallthroughCasesInSwitch`

         检查switch语句包含正确的break

       - `noImplicitReturns`

         检查函数没有隐式的返回值

       - `noUnusedLocals`

         检查未使用的局部变量

       - `noUnusedParameters`

         检查未使用的参数

    4. 高级

       - `allowUnreachableCode`

         检查不可达代码

         可选值：

         - true，忽略不可达代码
         - false，不可达代码将引起错误

       - **`noEmitOnError`**

         - 有错误的情况下不进行编译
         - 默认值：false

### 6.Webpack

#### 6.1 初始化项目

进入项目根目录，执行`npm init -y`，创建`package.json`文件

#### 6.2 下载构建工具

```sh
npm i -D webpack webpack-cli webpack-dev-server typescript ts-loader clean-webpack-plugin
```

- `webpack`：构建工具webpack
- `webpack-cli`：webpack的命令行工具
- `webpack-dev-server`：webpack的开发服务器
- `typescript`：ts编译器
- `ts-loader`：ts加载器，用于在webpack中编译ts文件
- `html-webpack-plugin`：webpack中的html插件，用来**自动创建html文件**
- `clean-webpack-plugin`：webpack**清除插件**，每次构建都会先清除目录

#### 6.3 webpack配置文件

根目录下创建webpack的配置文件`webpack.config.js`

```js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");

module.exports = {
    optimization:{
        minimize: false // 关闭代码压缩，可选
    },
    
	// 指定入口文件
    entry: "./src/index.ts",
    
    devtool: "inline-source-map",
    
    devServer: {
        contentBase: './dist'
    },
    
	// 指定打包文件所在目录
    output: {
        // 指定打包文件的目录
        path: path.resolve(__dirname, "dist"),
        // 打包后的文件
        filename: "bundle.js",
        environment: {
            arrowFunction: false // 关闭webpack的箭头函数，可选
        }
    },

    // 设置引用模块
    resolve: {
        extensions: [".ts", ".js"]
    },
    
    // 指定webpack打包时使用的模块
    module: {
        // 指定要加载的规则
        rules: [
            {
                // 指定规则生效的文件
                test: /\.ts$/,
                // 要使用的loader
                use: {
                   loader: "ts-loader"     
                },
                // 排除文件
                exclude: /node_modules/
            }
        ]
    },

    // 配置webpack插件
    plugins: [
        new CleanWebpackPlugin(),
        new HtmlWebpackPlugin({
            title:'这是一个自定义的title'
        }),
    ]

}
```

#### 6.4 ts配置文件

根目录下创建`tsconfig.json`，配置可选

```json
{
    "include": ["src/**/*"],
    "compilerOptions": {
        "target": "ES2015",
        "module": "ES2015",
        "strict": true
    }
}

```

#### 6.5 修改package.json

添加如下配置：

```json
{
  ...略...
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
    // 启动webpack内置服务器
    "start": "webpack serve --open chrome.exe"
  },
  ...略...
}
```

#### 6.6 编译

在src下创建ts文件，并在并命令行执行```npm run build```对代码进行编译，或者执行```npm start```来启动开发服务器。

```sh
npm run build
```

![image-20230227174524159](C:%5CUsers%5CAdministrator%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20230227174524159.png)

```sh
npm start
```

### 7.Babel

结合Babel来对代码进行转换，以使其可以兼容到更多浏览器。

#### 7.1 安装依赖包

```sh
npm i -D @babel/core @babel/preset-env babel-loader core-js
```

- `@babel/core`：babel核心工具
- `@babel/preset-env`：babel的预定义环境
- `@babel-loader`：babel在webpack中的加载器
- `core-js`：core-js用来**使老版本浏览器支持新版ES语法**

#### 7.2 修改webpack.config.js配置文件

```js
// 指定打包恩建所在目录
output: {
    ...
    environment: {
        arrowFunction: false,	// 告诉webpack不使用箭头函数	// 兼容IE用
    }
}

...略...
module: {
    rules: [
        {
            // 识别出哪些文件会被转换
            test: /\.ts$/,
            // 定义在进行转换时，使用哪个loader
            use: [
                {
                    loader: "babel-loader",
                    options:{
                        // 设置预定义的环境
                        presets: [
                            [
                                // 指定环境的插件
                                "@babel/preset-env",
                                // 配置信息
                                {
                                    // 指定浏览器版本（兼容目标浏览器）
                                    "targets":{
                                        "chrome": "58",
                                        "ie": "11"
                                    },
                                    // 指定corejs版本
                                    "corejs":"3",
                                    // 使用corejs的方式
                                    "useBuiltIns": "usage"	// 按需加载
                                }
                            ]
                        ]
                    }
                },
                {
                    loader: "ts-loader",

                }
            ],
            exclude: /node_modules/
        }
    ]
}
...略...
```

如此一来，使用ts编译后的文件将会再次被babel处理，**使得代码可以在大部分浏览器中直接使用**，可以在配置选项的**targets中指定要兼容的浏览器版本**。

## 二、面向对象

**简而言之就是程序之中所有的操作都需要通过对象来完成。**

举例来说：

- 操作浏览器要使用window对象
- 操作网页要使用document对象
- 操作控制台要使用console对象

一切操作都要通过对象，也就是所谓的面向对象，那么对象到底是什么呢？这就要先说到程序是什么，计算机程序的本质就是对现实事物的抽象，抽象的反义词是具体，比如：照片是对一个具体的人的抽象，汽车模型是对具体汽车的抽象等等。程序也是对事物的抽象，在程序中我们可以表示一个人、一条狗、一把枪、一颗子弹等等所有的事物。一个事物到了程序中就变成了一个对象。

在程序中所有的对象都被分成了两个部分数据和功能，以人为例，人的姓名、性别、年龄、身高、体重等属于数据，人可以说话、走路、吃饭、睡觉这些属于人的功能。数据在对象中被成为属性，而功能就被称为方法。所以简而言之，在程序中一切皆是对象。

### 1.类(class)

> 要想面向对象，操作对象，首先便要拥有对象，那么下一个问题就是如何创建对象。要创建对象，必须要先定义类，所谓的类可以理解为对象的模型，程序中可以根据类创建指定类型的对象，举例来说：可以通过Person类来创建人的对象，通过Dog类创建狗的对象，通过Car类来创建汽车的对象，不同的类可以用来创建不同的对象。

#### 1.1 定义类

```ts
class 类名 {
	属性名: 类型;
	
	// 构造函数
	constructor(参数: 类型) {
		this.属性名 = 参数;
	}
	
	方法名() {
		...
	}
}
```

#### 1.2 示例

```ts
class Person {
	name: string;
	age: number;
	
	constructor(name: string, age: number) {
		this.name = name;
		this.age = age;
	}
	
	sayHello() {
		console.log(`大家好，我是${this.name}，今年${this.age}岁。`);
	}
}
```

#### 1.3 使用

```ts
const p = new Person('孙悟空', 18);
p.sayHello()
```

### 2.面向对象的特点

#### 2.1 封装

对象实质上就是属性和方法的容器，它的主要作用就是存储属性和方法，这就是所谓的封装。

默认情况下，对象的属性是可以任意地修改的，为了确保数据的安全性，在TS中可以**对属性的权限进行设置**：

- 只读(`readonly`)

  readonly开头的属性表示一个只读的属性，只读不可修改。

- 属性的三种修饰符

  - public（公有的）（默认）：可以在类、子类和对象中修改（任意位置修改）

    ```ts
    class Person {
    	public name: string;
    	public age: number;
    	
        // 构造函数 在对象创建时调用
    	constructor(name: string, age: number) {
            // this指向当前实例
    		this.name = name;
    		this.age = age;	// 1.可以在类中修改
    	}
    	
    	sayHello() {
    		console.log(`大家好，我是${this.name}，今年${this.age}岁。`);
    	}
    }
    
    // Person的子类
    class Employee extends Person {
    	constructor(name: string, age: number) {
    		super(name, age);
    		this.name = name;	// 2.子类中可以修改
    	}
    }
    
    const p = new Person('孙悟空', 18);
    p.name = '猪八戒';	// 3.可以通过对象修改
    ```

  - protected（保护的）：可以在类、子类中修改

  - private（私有的）：可以在类中修改，对于一些不希望被任意修改的属性，可以将其设置为private

- 属性存取器

  在类中定义一组读取、设置属性的方法，这种**对属性读取或设置**的属性被称为**属性存取器**，掌握属性的控制权，使代码更健壮。

  **读取属性**的方法叫做`setter`方法，**设置属性**的方法叫做`getter`方法。

  ```ts
  class Person {
  	private _name: string;
  	
  	constructor(name:string) {
  		this._name = name;
  	}
      
      // 定义方法
      // getName() {
      //     return this._name
      // }
  	
  	get name() {
  		return this._name;
  	}
  	
  	set name(name: string) {
          ...	// 可以做判断...
  		this._name = name;
  	}
  }
  
  const p = new Person('孙悟空');
  console.log(p.name);	// 通过getter读取私有的name属性
  p.name = '猪八戒';	// 通过setter修改私有的name属性
  ```

- 静态属性(`static`)

  静态属性（方法）也称为类属性，**使用静态属性无需创建实例，直接通过类就可以使用**。

  ```ts
  class Tools {
  	static PI = 3.1415926;
  	static sum(num1: number, num2: number) {
  		return num1 + num2;
  	}
  }
  
  console.log(Tools.PI);
  console.log(Tools.sum(123, 456));	// 无需实例 直接通过类使用
  ```

#### 2.2 继承

- 通过继承(`extends`)，可以将其他类的属性和方法引入到当前类中。

  ```ts
  class Animal {
      name: string;
      age: number;
  
      constructor(name: string, age: numnber) {
          this.name = name;
          this.age = age;
      }
  }
  
  class Dog extends Animal {
      bark() {
          console.log(`${this.name}在汪汪叫！`)
      }
  }
  
  const dog = new Dog('旺财', 4);
  dog.bark();
  ```

  通过继承，可以将多个类中共有的代码写在一个父类中，这样只需要写一次即可让所有子类都同时拥有父类中的属性。

- **重写**：发生继承时，如果子类中的方法会**替换掉父类中的同名方法**，这就称为方法的重写。

  ```ts
  class Animal{
      name: string;
      age: number;
  
      constructor(name: string, age: number) {
          this.name = name;
          this.age = age;
      }
  
      run() {
          console.log(`父类中的run方法！`);
      }
  }
  
  class Dog extends Animal{
  
      bark() {
          console.log(`${this.name}在汪汪叫！`);
      }
  
      run() {
          console.log(`子类中的run方法，会重写父类中的run方法！`);
      }
  }
  
  const dog = new Dog('旺财', 4);
  dog.bark();
  ```

- **super关键字**：`super`关键字是对父类的直接引用，该关键字可以引用父类的属性和方法。

  ```ts
  class Animal{
      name: string;
      age: number;
  
      constructor(name: string, age: number) {
          this.name = name;
          this.age = age;
      }
  
      run() {
          console.log(`父类中的run方法！`);
      }
  }
  
  class Dog extends Animal{
  
      bark() {
          console.log(`${this.name}在汪汪叫！`);
      }
  
      run() {
      	super.run();
          console.log(`子类中的run方法，会重写父类中的run方法！`);
      }
  }
  
  const dog = new Dog('旺财', 4);
  dog.bark();
  ```

- **抽象类**：`abstract`开头的类。抽象类是**专门用来被其他类继承的类**，它只能被其他类所继承，而**不能用来创建实例**。

  ```ts
  // 定义抽象方法
  abstract class Animal {
      // 定义抽象方法
      // 没有方法体，抽象方法只能定义在抽象类中，且子类必须对抽象方法进行重写！
      abstract run(): void;
      
      bark(){
          console.log('动物在叫~');
      }
  }
  
  class Dog extends Animals {
      run() {
          console.log('狗在跑~');
      }
  }
  
  class Cat extends Animals {
      run() {
          console.log('猫在跑~')
      }
  }
  ```

### 3.接口(Interface)

> 接口的作用类似于抽象类，不同点在于接口中的所有方法和属性都是没有实值的，换句话说接口中的所有方法都是抽象方法。**接口主要负责定义一个类的结构，而不考虑实际值**，接口可以去限制一个对象的接口，对象只有包含接口中定义的所有属性和方法时才能匹配接口。同时，可以让一个类去实现接口，实现接口时类中要保护接口中的所有属性。

**描述一个对象的类型**（类型声明）：

1. type

   ```ts
   type myType = {
   	name: string,
   	age: number,
   	[propname: string]: any
   }
   
   const obj: myType = {
       name: 'sss',
       age: 111
   }
   ```

2. 接口

   ```ts
   interface myInterface {
       name: string;
       age: number;
   }
   
   const obj: myInterface = {
       name: 'sss',
       age: 111
   }
   ```

   ```ts
   // 接口可以重复声明
   interface myInterface {
       name: string;
       age: number;
   }
   
   interface myInterface {
   	gender: string;
   }
   
   const obj: myInterface = {
       name: 'sss',
       age: 111,
       gender: '男'
   }
   ```

定义类时，可以使类去实现一个接口。实现接口就是**使类满足接口的要求**。

```ts
interface Person{
    name: string;
    sayHello():void;
}

class Student implements Person{
    name: string;
    
    constructor(name: string) {
        this.name = name
    }

    sayHello() {
        console.log('大家好，我是' + this.name);
    }
}
```

### 4.泛型(Generic)

定义一个函数或类时，有些情况下**无法确定其中要使用的具体类型**（返回值、参数、属性的类型不能确定），此时泛型便能够发挥作用。

1. any

   ```ts
   function test(arg: any): any{
   	return arg;
   }
   ```

   上例中，test函数有一个参数类型不确定，但是能确定的是其返回值的类型和参数的类型是相同的。

   由于类型不确定所以参数和返回值均使用了any，很明显这样做是**不合适**的：

   - 使用any会关闭TS的类型检查
   - 不能体现出参数和返回值是相同的类型

2. 泛型

   ```ts
   function test<T>(arg: T): T{
   	return arg;
   }
   ```

   这里的`<T>`就是泛型，T仅仅是我们给这个类型起的名字，设置泛型后即可在函数中使用T来表示该类型。

   **使用**：

   - 直接使用

     ```ts
     test(10)
     ```

     利用ts的自动推断，直接传递参数使用。

   - 指定类型

     ```ts
     test<number>(10)
     ```

     在函数后手动指定泛型类型。

   - 可以同时指定多个泛型，泛型之间用逗号隔开

     ```ts
     function test<T, K>(a: T, b: K): K {
     	...
     	return b
     }
     
     test<number, string>(10, 'hello')
     ```

   - 利用接口约束泛型的范围（`T extends MyInter`表示泛型T必须是MyInter的子类）

     ```ts
     interface MyInter {
     	length: number;
     }
     
     function test<T extends MyInter>(arg: T): number {
     	return arg.length;
     }
     ```

   - 类使用泛型

     ```ts
     class MyClass<T> {
     	prop: T;
     	
     	costructor(prop: T) {
     		this.prop = prop
     	}
     }
     ```



