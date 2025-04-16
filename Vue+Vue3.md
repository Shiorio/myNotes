# Vue核心

## 一、Vue简介

一套用于**构建用户界面**的**渐进式**JavaScript框架。

渐进式：Vue可以自底向上逐层应用。简单应用只需一个轻量小巧的核心库，复杂应用可以引入各式各样的Vue插件。

API文档：https://cn.vuejs.org/v2/api/

## 二、初识Vue

### 1.Vue特点

1. 采用**组件化**模式，提高代码复用率，且让代码更好维护。

2. **声明式**编码，让编码人员无需直接操作DOM，提高开发效率。

   ![image-20220228210948202](https://gitee.com/v876774538/my-img/raw/master/image-20220228210948202.png)

3. 使用**虚拟DOM**+优秀的**Diff算法**，尽量复用DOM节点。 

   ![image-20220228211252679](https://gitee.com/v876774538/my-img/raw/master/image-20220228211252679.png)

   ![image-20220228211341351](https://gitee.com/v876774538/my-img/raw/master/image-20220228211341351.png)


### 2.Hello小案例

```vue
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>初识Vue</title>
    <!-- 引入Vue.js -->
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
    <!-- 容器 -->
    <div id="root">
        <h1>Hello，{{name}}!</h1>
    </div>

    <script type="text/javascript">
        Vue.config.productionTip = false; // 阻止Vue在启动时生成生产提示

        // 创建Vue实例
        new Vue({
            el: '#root',
            // data 存储数据 供el指定的容器使用
            data: {
                name: "Shiori"
            }
        })
    </script>
</body>

</html>
```

1. 想让Vue工作，就必须创建一个**Vue实例**，且要传入一个**配置对象**（如el、data）；
2. root容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法；
3. root容器里的代码被称为**Vue模板**；
4. 一个容器只能由一个Vue实例接管；
5. 真实开发中只有一个Vue实例，并且会配合着组件一起使用；
6. {{xxx}}中写的是**js表达式**，且xxx可以自动读取到data中的所有属性；
7. 一旦data中的数据发生改变，那么模板中用到该数据的地方也会自动更新。

## 三、模板语法

```vue
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>模板语法</title>
    <!-- 引入Vue -->
    <script src="../js/vue.js"></script>
</head>

<body>
    <div id="root">
        <h1>插值语法</h1>
        <h3>你好，{{name}}</h3>
        <hr>

        <h1>指令语法</h1>
        <a v-bind:href="school.url">点我去{{school.name}}学习1</a>
        <!-- v-bind简写 -->
        <a :href="school.url">点我去{{school.name}}学习2</a>

        <!-- 插值语法往往用于指定标签体内容
             而v-bind则用于指定标签属性内容 -->
    </div>

    <script>
        Vue.config.productionTip = false;
        // 阻止Vue在启动时生成生产提示

        new Vue({
            el: '#root',
            data: {
                name: 'Shiori',
                school: {
                    name: '尚硅谷',
                    url: 'http://www.atguigu.com'
                }
            }
        })
    </script>
</body>

</html>
```

1. 插值语法：
   - 功能：用于解析标签体内容；
   - 写法：{{xxx}}。
2. 指令语法：
   - 功能：用于解析标签（包括：标签属性、标签体内容、绑定事件……）；
   - 举例：v-bind:href="xxx" 或简写为:href="xxx"。
3. **插值语法**往往用于指定**标签体**内容，而**v-bind**则用于指定**标签属性**内容。

## 四、数据绑定

```vue
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>数据绑定</title>
    <!-- 引入Vue.js -->
    <script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
    <!-- 容器 -->
    <div id="root">
        单向数据绑定：
        <input type="text" v-bind:value="name">
        <!-- 输入框修改不影响data数据 -->
        双向数据绑定：
        <input type="text" v-model:value="name">
        <!-- 输入框修改改变data数据 -->
        <!-- v-model只能用在表单类元素（输入类元素）上 -->

        <!-- 简写 -->
        单向数据绑定：
        <input type="text" :value="name">
        <!-- 输入框修改不影响data数据 -->
        双向数据绑定：
        <input type="text" v-model="name">
    </div>

    <script type="text/javascript">
        Vue.config.productionTip = false; // 阻止Vue在启动时生成生产提示

        // 创建Vue实例
        new Vue({
            el: '#root',
            // data 存储数据 供el指定的容器使用
            data: {
                name: 'Shiori'
            }
        })
    </script>
</body>

</html>
```

1. **单向绑定(v-bind)**：数据只能从data流向页面；

2. **双向绑定(v-model)**：数据不仅能从data流向页面，还可以从页面流向data。

   备注：

   - 双向绑定一般用在表单类元素上（如，input、select等）；
   - **v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。**

**el与data的两种写法：**

- el两种写法：

1. new Vue的时候配置el属性；
2. 先创建Vue实例，然后通过vm.$mount('#root')指定el的值。

- data两种写法：

1. 对象式；
2. 函数式（用到组件时，data必须采用函数式，否则会报错）

注意：由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this指向的就不再是Vue实例了。

```js
const v = new Vue({
	// el 第一种写法
	// el:'#root'
    // data 第一种写法：对象式
    /*
	data:{
		name:'Shiori'
	}*/
	
	// data第二种写法：函数式
    // data(){}
    data:function(){
        return{
            name:'Shiori'
        }
    }
})
// el 第二种写法
v.$mount('#root');
```

## 五、MVVM模型

### 1.理解MVVM模型（Model-View-ViewModel）

1. M：模型（Model）：对应data中的数据；
2. V：视图（View）：模板；
3. VM：视图模型（ViewModel）：Vue实例对象

![image-20220315104914760](https://gitee.com/v876774538/my-img/raw/master/image-20220315104914760.png)

![image-20220315110148464](https://gitee.com/v876774538/my-img/raw/master/image-20220315110148464.png)

### 2.数据代理

#### 2.1 Object.defineproperty方法

`**Object.defineProperty()**` 方法会直接**在一个对象上定义一个新属性，或者修改一个对象的现有属性**，并返回此对象。

```js
Object.defineProperty(obj, prop, descriptor);
// obj 要定义属性的对象
// prop 要定义或修改的属性的名称或Symbol
// descriptor 要定义或修改的属性描述符
// 返回值 被传递给函数的对象
```

```js
let number = 20;
let person = {
    name:'张三',
    sex:'男',
}
Object.defineProperty(person, 'age', {
    value: 18,
    enumerabel: true,	// 控制属性是否可以被枚举，默认值为false
    writable: true,	// 控制属性是否可以被修改，默认值为false
    configurable: true	// 控制属性是否可以被删除，默认值为false
    
    // 当有人读取person的age属性时，get函数就会被调用，且返回值就是age的值
    get() {
    	console.log('有人读取age属性了');
    	return number;
	}
	// 当有人修改person的age属性时，set函数就会被调用，且会收到修改的具体值
	set(value) {
        console.log('有人修改了age属性，且值是',value);
    }
})
```

#### 2.2 数据代理概念

通过一个对象代理对另一个对象中属性的操作（读/写）。

```js
let obj1 = {x:100};
let obj2 = {y:200};

Object.defineProperty(obj2, 'x', {
	get() {
		return obj1.x;
	},
	set(value) {
		obj1.x = value;
	}
})
```

![image-20220315113613581](https://gitee.com/v876774538/my-img/raw/master/image-20220315113613581.png)

#### 2.3 Vue中的数据代理

![image-20220315114524788](https://gitee.com/v876774538/my-img/raw/master/image-20220315114524788.png)

![image-20220315114945383](https://gitee.com/v876774538/my-img/raw/master/image-20220315114945383.png)

1. Vue中的数据代理：

   通过vm对象来代理data对象中属性的操作（读/写）

2. Vue中数据代理的好处：

   更加方便地操作data中的数据

3. 基本原理：

   通过Object.defineProperty()把data对象中所有属性添加到vm上；

   为每个添加到vm上的属性，都指定一个getter/setter；

   在getter/setter内部操作（读/写）data中对应的属性。

## 六、事件处理

### 1.事件的基本使用

1. 使用**v-on**指令或**@**绑定事件（如v-on:click="showInfo"，@click="showInfo"）；
2. 事件的回调需要配置在methods对象中，methods中配置的函数不用箭头函数。

### 2.事件修饰符

在事件处理程序中调用 `event.preventDefault()` （阻止元素发生默认的行为）或 `event.stopPropagation()` （阻止冒泡）是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。

为了解决这个问题，Vue.js 为 `v-on` 提供了**事件修饰符**。

- **.stop**：相当于js中的event.stopPropagation()，防止事件冒泡；
- **.prevent**：相当于js中的event.preventDefault()，防止执行默认行为；
- .capture：使用事件的捕获模式，与事件冒泡的方向相反，事件捕获由外到内；
- .self：只会触发自己范围内的事件，不包含子元素（只有event.target是当前操作的元素时才触发事件，冒泡无法触发）；
- **.once**：只会触发一次；
- .passive：使元素的默认行为立即执行，无需等待事件回调执行完毕。

```vue
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

注意：使用修饰符时，顺序很重要。因此，用v-on:click.prevent.self会阻止所有的点击，而v-on:click.self.prevent只会阻止对元素自身的点击。

**关于passive：**

不要把 `.passive` 和 `.prevent` 一起使用，因为 `.prevent` 将会被忽略，同时浏览器可能会向你展示一个警告（passive和prevent冲突）。请记住，`.passive` 会告诉浏览器你**不想阻止事件的默认行为**。

【浏览器只有等内核线程执行到事件监听器对应的JavaScript代码时，才能知道内部是否会调用preventDefault函数来阻止事件的默认行为，所以浏览器本身是没有办法对这种场景进行优化的。这种场景下，用户的手势事件无法快速产生，会导致页面无法快速执行滑动逻辑，从而让用户感觉到页面卡顿。】

 通俗点说就是每次事件产生，浏览器都会去查询一下是否有preventDefault阻止该次事件的默认动作。我们加上**passive就是为了告诉浏览器，不用查询了，我们没用preventDefault阻止默认动作。**

### 3.按键修饰符

```html
<!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
<input v-on:keyup.enter="submit">
```

Vue未提供别名的按键，我们可以直接将 [`KeyboardEvent.key`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key/Key_Values) 暴露的任意有效按键名**转换为 kebab-case** （短横线命名）来作为修饰符。

```html
<input v-on:keyup.page-down="onPageDown">
```

#### 3.1 按键码

使用 `keyCode` 去指定具体的按键（不推荐）：

```html
<input v-on:keyup.13="submit">
```

为了在必要的情况下支持旧浏览器，Vue 提供了绝大多数常用的按键码的**别名**：

- .enter
- .tab
- .delete
- .esc
- .space
- .up
- .down
- .left
- .right

还可以通过全局**config.keyCodes**对象自定义按键修饰符别名：

```js
Vue.config.keyCodes.自定义键名 = 键码;

// 可以使用 `v-on:keyup.f1`
Vue.config.keyCodes.f1 = 112;
```

### 4.系统修饰键

- .ctrl
- .alt
- .shift
- .meta（在 Mac 系统键盘上，meta 对应 command 键 (⌘)。**在 Windows 系统键盘 meta 对应 Windows 徽标键 (⊞)。**在 Sun 操作系统键盘上，meta 对应实心宝石键 (◆)。在其他特定键盘上，尤其在 MIT 和 Lisp 机器的键盘、以及其后继产品，比如 Knight 键盘、space-cadet 键盘，meta 被标记为“META”。在 Symbolics 键盘上，meta 被标记为“META”或者“Meta”。）

1. 配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发；
2. 配合keydown使用：正常触发事件。

```html
<!-- Alt + C -->
<input v-on:keyup.alt.67="clear">

<!-- Ctrl + Click -->
<div v-on:click.ctrl="doSomething">Do something</div>
```

#### 4.1 .exact修饰符

.exact修饰符云讯控制**由精确的系统修饰符组合触发**的事件。

```html
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button v-on:click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button v-on:click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button v-on:click.exact="onClick">A</button>
```

#### 4.2 鼠标按钮修饰符

- .left
- .right
- .middle

## 七、计算属性与侦听器

### 1.计算属性

1. 定义：要用的属性不存在，要通过已有属性计算得来；
2. 原理：底层借助了Object.defineproperty方法提供的getter和setter；
3. get函数什么时候执行？
   - 初次读取时会执行一次；
   - 当依赖的数据发生改变时会被再次调用。
4. 优势：与methods实现相比，内部有缓存机制，效率更高、调试方便。
5. 备注：
   - 计算属性最终会出现在vm上，直接读取使用即可；
   - 如果计算属性要被修改，必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。

```html
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```

```js
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
})
```

结果：

Original message: "Hello"

Computed reversed message: "olleH"

这里我们声明了一个计算属性 `reversedMessage`。我们提供的函数将用作 property `vm.reversedMessage` 的 **getter 函数**：

```js
console.log(vm.reversedMessage) // => 'olleH'
vm.message = 'Goodbye'
console.log(vm.reversedMessage) // => 'eybdooG'
```

姓名案例：

```html
<div id="root">
	姓：<input type="text" v-model:value="firstName">
	名：<input type="text" v-model:value="lastName">
	姓名：<span>{{fullName}}</span>
</div>
```

```js
var vm = new Vue({
	el: '#id',
	data: {
		firstName:'张',
		lastName:'三'
	},
	computed: {
        // 完整写法
        fullName: {
            get() {
                return this.firstName + ' ' + this.lastName;
            }
            set(value) {
        		var names = value.split(' ');
    			this.firstName = names[0];
                 this.lastName = names[names.length - 1];
    		}
        }
        // 简写
		fullName: function() {
			return this.firstName + this.lastName;
		}
		fullName() {
			return this.firstName + this.lastName;
		}
	}
})
```

### 2.侦听器

1. 被监视的属性必须存在；
2. 当**被监视的属性变化**时，回调函数自动调用，进行相关操作；
3. 监视的两种写法：
   - new Vue时传入watch配置；
   - 通过vm.$watch监视

#### 2.1 天气案例

```html
<div id="root">
	<h2>今天天气很{{info}}</h2>
	<button @click="changeWeather">切换天气</button>
</div>
```

```js
var vm = new Vue({
	el: '#root',
	data:{
		isHot: true
	},
	computed: {
		info() {
			return isHot ? '炎热' : '凉爽';
		}
	}
	methods: {
		changeWeather() {
			isHot = !isHot;
		}
	}
    // 1. new Vue时传入watch配置
    watch: {
        isHot: {
            immediate: true,	// 初始化时让handler调用一下
            // handler什么时候调用？档isHot发生改变时
            handler(newValue, oldValue) {
                console.log('isHot被修改了', newValue, oldValue);
            }
        }
    }
	// 简写
	watch: {
        isHot(newValue, oldValue) {
            console.log('isHot被修改了', newValue, oldValue);
        }
    }
})
// 2. 通过vm.$watch监视
vm.$watch('isHot', {
    immediate: true,
    handler(newValue, oldValue) {
        console.log('isHot被修改了', newValue, oldValue);
    }
})
// 简写
vm.$watch('isHot', function(newValue, oldValue) {
    console.log('isHot被修改了', newValue, oldValue);
})
```

#### 2.2 深度监听

1. Vue中的watch默认不监听对象内部值的改变（一层）；
2. 但配置deep:true（深度监听）后就可以检测对象内部值的改变（多层）。

```html
<div id="root">
	<h2>a的值是：{{numbers.a}}</h2>
	<button @click="numbers.a++">点我让a+1</button>
    <h2>b的值是：{{numbers.b}}</h2>
	<button @click="numbers.b++">点我让b+1</button>
    <button @click="numbers={a:123,b:456}">
        彻底替换掉numbers
    </button>
</div>
```

```js
var vm = new Vue({
	el: '#root',
	data:{
		numbers: {
            a: 1,
            b: 1
        }
	},
    watch: {
        // 监视多级结构中某个属性的变化
        'numbers.a': {
        	handler() {
    			console.log('a被改变了');
			}         
        },
        // 监视多级结构中所有属性的变化
        numbers: {
            deep: true,
            handler(){
                console.log('numbers改变了');
            }
        }
    }
})
```

### 3.watch与computed对比

#### 3.1 姓名案例对比

```html
<div id="demo">{{ fullName }}</div>
```

使用侦听属性完成：

```js
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
})
```

与计算属性版本比较：

```js
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```

#### 3.2 区别

1. computed能完成的功能，watch都能完成；
2. watch能完成的功能，computed不一定能完成，比如，watch可以进行异步操作。

#### 3.3 两个重要原则

1. 所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm或组件实例对象；
2. 所有不被Vue所管理的函数（**定时器的回调函数、ajax的回调函数**等），最好写成箭头函数，这样this的指向才是vm或组件实例对象。

## 八、class与style绑定

### 1.class样式绑定

`:class="xxx"`	xxx可以是字符串、对象、数组。

- 字符串写法适用于：类名不确定，要动态获取；
- 对象写法适用于：要绑定多个样式，个数不确定，名字也不确定；
- 数组写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用。

### 2.style样式绑定

`:style="{fontSize: xxx + 'px'}"`	其中xxx是动态值；

`:style="[a, b]"`	其中a、b是样式对象。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>绑定样式</title>
    <!-- 引入vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="root">
        <!-- 绑定class样式：字符串写法 适用于：样式的类名不确定，需要动态指定 -->
        <div class="basic" :class="mood" @click="changeMood"></div>
        <!-- 绑定class样式：数组写法   适用于：要绑定的样式个数不确定、名字也不确定 -->
        <div class="basic" :class="arr">{{name}}</div>
        <!-- 绑定class样式：对象写法   适用于：要绑定的样式个数不确定、名字确定，但要动态地决定用不用 -->
        <div class="basic" :class="classObj">{{name}}</div><br><br>

        <!-- 绑定style样式：对象写法 -->
        <div class="basic" :style="{fontSize: fontSize +'px'}">{{name}}</div>
        <div class="basic" :style="styleObj">{{name}}</div>
        <!-- 绑定style样式：数组写法 -->
        <div class="basic" :style="[styleObj,styleObj2]">{{name}}</div>
        <div class="basic" :style="styleArr">{{name}}</div>
    </div>
</body>
<style>
    .basic {
        width: 200px;
        height: 50px;
        border: 1px solid black;
    }

    .normal {
        background-color: white;
    }

    .happy {
        background-color: pink;
    }

    .sad {
        background-color: skyblue;
    }

    .atguigu1 {
        background-color: purple;
    }

    .atguigu2 {
        font-size: 28px;
    }

    .atguigu3 {
        font-weight: 500;
    }
</style>
<script>
    Vue.config.productionTip = false;
    var vm = new Vue({
        el: '#root',
        data: {
            name: 'Shiori',
            mood: 'normal',
            arr: ['atguigu1', 'atguigu2', 'atguigu3'],
            classObj: {
                atguigu1: true,
                atguigu2: true,
                atguigu3: true
            },
            fontSize: 40,
            styleObj: {
                // 驼峰式命名
                fontSize: '40px'
            },
            styleObj2: {
                color: 'red'
            },
            styleArr:[{
                fontSize:'40px'
            },{
                color:'red'
            }]
        },
        methods: {
            changeMood() {
                const arr = ['happy', 'sad', 'normal'];
                // Math.random 随机生成[0,1)的数
                // Math.floor 向下取整
                const index = Math.floor(Math.random() * 3);
                this.mood = arr[index];
            }
        }
    })
</script>

</html>
```

![image-20220316103641308](https://gitee.com/v876774538/my-img/raw/master/image-20220316103641308.png)

对于数组写法的样式绑定，我们可以通过对数组的操作自由地操纵样式：

![image-20220316100319724](https://gitee.com/v876774538/my-img/raw/master/image-20220316100319724.png)

## 九、条件渲染

### 1.使用v-show做条件渲染

```html
<h2 v-show="show">Hello1</h2>
```

```js
data: {
    show: false
}
```

![image-20220316104541572](https://gitee.com/v876774538/my-img/raw/master/image-20220316104541572.png)

带有v-show的元素始终会被渲染并保留在DOM中。v-show只是简单地切换元素的CSS property display。

### 2.使用v-if做条件渲染

```html
<h2 v-if="show">Hello2</h2>
```

![image-20220316104744145](https://gitee.com/v876774538/my-img/raw/master/image-20220316104744145.png)

**v-if指令用于条件性地渲染一块内容。**这块内容只会在指令的表达式返回truthy值的时候被渲染。v-if是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地销毁和重建。

```html
<h2 v-if="show">Hello2</h2>
<div v-if="n===1">Angular</div>
<div v-else-if="n===2">React</div>
<div v-else>Vue</div>
<button class="btn" @click="n++">点我n+1</button>
```

```js
data: {
    show: false,
    n:0
}
```

配合template使用：template不会破坏原有结构

```html
<template v-if="n===1">
    <h2>Hello</h2>
    <h2>World</h2>
    <h2>!</h2>
</template>
```

### 3.总结

1. v-if：

   - 写法：v-if="表达式"	v-else-if="表达式"	v-else="表达式"

   - 适用于：切换频率较低的场景；
   - 特点：不展示的DOM元素直接被移除；
   - 注意：v-if可以和v-else-if、v-else一起使用，但要求结构不能被“打断”。

2. v-show：

   - 写法：v-show="表达式"

   - 适用于：切换频率较高的场景；
   - 特点：不展示的DOM元素不被移除，保持渲染，只是使用样式隐藏。

## 十、列表渲染

### 1.v-for指令

- 用于展示列表数据；
- 语法：v-for="(item, index) in xxx" :key="yyy";
- 可遍历：**数组、对象**、字符串、指定次数。

```html
<div id="root">
    <!-- 遍历数组 -->
    <ul v-for="item in persons" :key="item.id">
        <li>{{item.id}}</li>
        <li>{{item.name}}</li>
        <li>{{item.age}}</li>
    </ul>
    <br><br>
    <ul v-for="(item, index) in persons" :key="index">
        <li>{{item.name}}</li>
        <li>{{index}}</li>
    </ul>
    <br><br>
    <!-- 遍历对象 -->
    <ul v-for="(value, k) in car" :key="k">
        <li>{{k}}--{{value}}</li>
    </ul>
    <br><br>
    <!-- 遍历字符串 -->
    <ul v-for="(value, k) in str" :key="k">
        <li>
            {{k}}--{{value}}
        </li>
    </ul><br><br>
    <!-- 遍历指定次数 -->
    <ul v-for="(number, index) in 5" :key="index">
        <li>
            {{index}}--{{number}}
        </li>
    </ul>
</div>
```

```js
var vm = new Vue({
    el: '#root',
    data: {
        persons: [{
                id: '001',
                name: '张三',
                age: 18
            },
            {
                id: '002',
                name: '李四',
                age: 18
            },
            {
                id: '003',
                name: '王五',
                age: 18
            },
        ],
        car: {
            name: '奥迪A8',
            price: '70万',
            color: '黑色'
        },
        str: 'Hello'
    },
    methods: {

    },
}
```

遍历数组：

![image-20220316135507784](https://gitee.com/v876774538/my-img/raw/master/image-20220316135507784.png)

![image-20220316135519199](https://gitee.com/v876774538/my-img/raw/master/image-20220316135519199.png)

遍历对象：

![image-20220316135627659](https://gitee.com/v876774538/my-img/raw/master/image-20220316135627659.png)

遍历字符串：

![image-20220316135649371](https://gitee.com/v876774538/my-img/raw/master/image-20220316135649371.png)

遍历指定次数：

![image-20220316135709877](https://gitee.com/v876774538/my-img/raw/master/image-20220316135709877.png)

### 2.key的作用与原理

使用index作为key可能导致的数据错乱情况：

![image-20220316114608390](https://gitee.com/v876774538/my-img/raw/master/image-20220316114608390.png)

使用唯一标识id作为key：

![image-20220316114753345](https://gitee.com/v876774538/my-img/raw/master/image-20220316114753345.png)

#### 2.1 虚拟DOM中key的作用

key是虚拟DOM对象的标识，当状态中的数据发生变化时，Vue会根据【新数据】生成【行的虚拟DOM】，随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较。

对比规则如2.2。

#### 2.2 对比规则

1. 旧虚拟DOM中找到了与新虚拟DOM相同的key：
   - 若虚拟DOM中内容没变，直接使用之前的真实DOM；
   - 若虚拟DOM中内容改变，则生成新的真实DOM，随后替换掉页面中之前的真实DOM。
2. 旧虚拟DOM中未找到与新虚拟DOM相同的key：
   - 创建新的真实DOM，随后渲染到页面。

#### 2.3 用index作为key可能引发的问题

1. 若对数据进行：逆序添加、逆序删除等破坏顺序的操作，会产生没有必要的真实DOM更新。界面效果没有问题，但影响效率。
2. 若结构中还包含输入类DOM：会产生错误的DOM更新。产生界面效果问题。

#### 2.4 开发中如何选择key

1. 最好使用每条数据的唯一标识作为key，比如id、手机号、身份证号、学号等；
2. 若不存在对数据的逆序添加、删除等破坏顺序的操作，仅用于渲染列表展示，使用index作为key也是没有问题的。

#### 2.5 官方说明

key的特殊属性主要用在Vue的虚拟DOM算法，在新旧nodes对比时辨识VNodes。如果不适用key，Vue会使用一种最大限度减少动态元素并且尽可能的尝试地修改/复用相同类型元素的算法。而使用key时，它会基于key的变化重新排列元素顺序，并且会移除key不存在的元素。

有相同父元素的子元素必须有独特的key。重复的key会造成渲染错误。

### 3.列表过滤

实现目标：

![image-20220318095430036](https://gitee.com/v876774538/my-img/raw/master/image-20220318095430036.png)

![image-20220318095439537](https://gitee.com/v876774538/my-img/raw/master/image-20220318095439537.png)

```html
<!-- 准备好一个容器 -->
<div id="root">
    <h2>人员列表</h2>
    <input type="text" placeholder="请输入姓名" v-model="keyWord">
    <ul>
        <li v-for="(item,index) in filtPersons" :key="item.id">{{item.id}}--{{item.name}}</li>
    </ul>
</div>
```

#### 3.1 watch实现

```js
Vue.config.productionTip = false;
// watch实现
var vm = new Vue({
    el: '#root',
    data: {
        keyWord:'',
        persons: [{
                id: '001',
                name: '马冬梅',
                sex: '女',
                age: 18
            },
            {
                id: '002',
                name: '周冬雨',
                sex: '女',
                age: 18
            },
            {
                id: '003',
                name: '周杰伦',
                sex: '男',
                age: 19
            },
            {
                id: '004',
                name: '温兆伦',
                sex: '男',
                age: 19
            },
        ],
        filtPersons:[]
    },
    watch:{
        // keyWord(val){
        // 初始时页面上没有列表
        //     this.filtPersons = this.persons.filter((item)=>{
        //         // 判断name包含val
        //         return item.name.indexOf(val) !== -1
        //     })
        // }
        keyWord: {
            // 初始时调用一次
            immediate: true,
            handler(val) {
                this.filtPersons = this.persons.filter((item)=>{
                    return item.name.indexOf(val) !== -1
                })
            }
        }

    },
    methods: {

    },
})
```

#### 3.2 computed实现

```js
Vue.config.productionTip = false;
// computed实现
var vm = new Vue({
    el: '#root',
    data: {
        keyWord: '',
        persons: [{
                id: '001',
                name: '马冬梅',
                sex: '女',
                age: 18
            },
            {
                id: '002',
                name: '周冬雨',
                sex: '女',
                age: 18
            },
            {
                id: '003',
                name: '周杰伦',
                sex: '男',
                age: 19
            },
            {
                id: '004',
                name: '温兆伦',
                sex: '男',
                age: 19
            },
            // computed要赋给不存在的值
            // filtPersons:[]
        ],
    },
    computed:{
        filtPersons() {
            return this.persons.filter((item)=>{
                return item.name.indexOf(this.keyWord) !== -1
            })
        }
    },
    methods: {

    },
})
```

### 4.列表排序

```html
<!-- 准备好一个容器 -->
<div id="root">
    <h2>人员列表</h2>
    <input type="text" placeholder="请输入姓名" v-model="keyWord">
    <button @click="changeSort(2)">年龄升序</button>
    <button @click="changeSort(1)">年龄降序</button>
    <button @click="changeSort(0)">原顺序</button>
    <ul>
        <li v-for="(item,index) in filtPersons" :key="item.id">{{item.id}}--{{item.name}}--{{item.age}}</li>
    </ul>
</div>
```

```js
Vue.config.productionTip = false;
// computed实现
var vm = new Vue({
    el: '#root',
    data: {
        keyWord: '',
        sortType: 0,    // 0 原顺序 1 降序 2 升序
        persons: [{
                id: '001',
                name: '马冬梅',
                sex: '女',
                age: 18
            },
            {
                id: '002',
                name: '周冬雨',
                sex: '女',
                age: 17
            },
            {
                id: '003',
                name: '周杰伦',
                sex: '男',
                age: 25
            },
            {
                id: '004',
                name: '温兆伦',
                sex: '男',
                age: 19
            },
        ],
    },
    computed:{
        filtPersons() {
            const arr = this.persons.filter((item)=>{
                return item.name.indexOf(this.keyWord) !== -1
            })
            // 判断是否需要排序
            if (this.sortType) {
                // 判断排序方式
                // 注意sort方法会更改原数组
                arr.sort((a,b)=>{
                    // 降序 b-a 升序 a-b
                    return this.sortType==1 ? b.age-a.age : a.age-b.age;
                })
            }
            return arr;
        }
    },
    methods: {
        changeSort(val) {
            this.sortType = val;
        }
    },
})
```

![image-20220318101424557](https://gitee.com/v876774538/my-img/raw/master/image-20220318101424557.png)

![image-20220318101435760](https://gitee.com/v876774538/my-img/raw/master/image-20220318101435760.png)

![image-20220318101450176](https://gitee.com/v876774538/my-img/raw/master/image-20220318101450176.png)

### 5.Vue监测数据原理

Vue为了更加简洁，当data的数据是数组或对象的时候，动态地添加或删除，视图将不会更新。

#### 5.1 	Vue.set()

```js
Vue.set(target, propertyName/index, value);
vm.$set(target, propertyName/index, value);
```

- `{Object | Array} target`
- `{string | number} propertyName/index`
- `{any} value`

向**响应式对象**中添加一个 property，并确保这个新 property 同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新 property，因为 Vue 无法探测普通的新增 property (比如 `this.myObject.newProperty = 'hi'`)

```html
<template>
    <p v-for="item in items" :key="item.id">
        {{item.message}}
    </p>
    <button class="btn" @click="dynamicClick()">动态赋值</button> 
</template>    
<script>
data() {
        return {
           items:[
               {message:"Test one",id:"1"},
               {message:"Test two",id:"2"},
               {message:"Test three",id:"3"}
              ]
            }
        },
methods: {
    dynamicClick:function(){
            //this.items[0]={message:"Change Test",id:'10'}
            this.$set(this.items,0,{message:"ChangeTest",id:'10'})
            console.log(this.items,'----------')
    },
}
</script>
```

注意：注意对象不能是 Vue 实例，或者 Vue 实例的根数据对象。

#### 5.2 数组更新检测

Vue将被侦听的数组的变更方法进行了包括，所以它们也会触发视图更新。这些被包裹过的方法包括：

- push()
- pop()
- shift()
- unshift()
- splice()
- sort()
- reverse()

```js
example.items.push({message:'Baz'});
```

#### 5.3 总结

1. Vue会监视data中所有层次的数据。

2. 监测对象中的数据：

   通过setter实现监视，且要在new Vue时就传入要监测的数据。

   - 对象中后追加的属性，Vue默认不做响应式处理；
   - 如需给后添加的属性做响应式，请使用如下API：
     - Vue.set(target, propertyName/index, value)
     - vm.$set(target, propertyName/index, value)

3. 监测数组中的数据：

   通过包裹数组更新元素的方法实现，本质做了两件事：

   - 调用原生对应的方法对数组进行更新；
   - 更新解析模板，进而更新页面。

4. 在Vue修改数组中的某个元素时一定要用如下方法：

   - 使用这些API：push()、pop()、shift()、unshift()、splice()、sort()、reverse()
   - Vue.set()或vm.$set()
   - 特别注意：Vue.set()和vm.$set()不能给vm或vm的根数据对象添加属性。

## 十一、收集表单数据

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>收集表单数据</title>
    <!-- 引入vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="root">
        <form action="" @submit="submitForm">
            <label for="account">账户：</label>
            <!-- trim 去掉前后空格 -->
            <input type="text" id="account" v-model.trim="userInfo.account"><br>
            <label for="password">密码：</label>
            <input type="password" id="password" v-model="userInfo.password"><br>
            <label for="age">年龄：</label>
            <!-- number 数据转换 -->
            <input type="number" id="age" v-model.number="userInfo.age"><br>
            <label for="sex">性别：</label>
            <input type="radio" name="sex" id="sex" v-model="userInfo.sex" value="male" checked>男
            <input type="radio" name="sex" id="sex" v-model="userInfo.sex" value="female">女<br>
            <label for="hobby">爱好：</label>
            <input type="checkbox" id="hobby" v-model="userInfo.hobby" value="study">学习
            <input type="checkbox" id="hobby" v-model="userInfo.hobby" value="eat">吃饭
            <input type="checkbox" id="hobby" v-model="userInfo.hobby" value="game">打游戏<br>
            <label for="campus">所属校区：</label>
            <select name="campus" id="campus" v-model="userInfo.campus">
                <option value="">请选择校区</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
                <option value="shenzhen">深圳</option>
            </select><br>
            <label for="other">其他信息</label><br>
            <textarea name="other" id="other" cols="30" rows="10" v-model="userInfo.other"></textarea><br>
            <input type="checkbox" v-model="userInfo.agree">阅读并接受<a href="http://www.atguigu.com">《用户协议》</a><br>
            <button>提交</button>
        </form>
    </div>
</body>
<script>
    Vue.config.productionTip = false;
    var vm = new Vue({
        el: '#root',
        data: {
            userInfo: {
                account: '',
                password: '',
                sex: '',
                hobby: [],
                campus: '',
                other: '',
                agree: false
            }

        },
        methods: {
            submitForm() {
                console.log(JSON.stringify(this.userInfo));
            }
        },
    })
</script>

</html>
```

1. 若`<input type="text"/>`，v-model收集value值，用户输入value值；
2. 若`<input type="radio"/>`，v-model收集value值，需要给标签配置value值；
3. 若`<input type="checkbox"/>`，
   - 未配置input的value属性，那么收集的就是checked（true/false)
   - 配置input的value属性：
     - v-model的初始值为非数组，那么收集到的就是checked(true/false)；
     - v-model的初始值为数组，那么收集到的就是由checkbox value组成的数组。
4. v-model 3个修饰符：
   - lazy：失去焦点时再收集数据；
   - number：输入字符串转为有效的数字；
   - trim：输入收尾空格过滤。

## 十二、过滤器

### 1.局部过滤器

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>过滤器</title>
    <!-- 引入vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <!-- 引入dayjs -->
    <script src="../js/dayjs.min.js"></script>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>显示格式化后的时间</h2>
        <!-- 计算属性实现 -->
        <h3>现在是：{{fmtTime}}</h3>
        <!-- methods实现 -->
        <h3>现在是：{{getFmtTime()}}</h3>
        <!-- 过滤器实现 -->
        <h3>现在是：{{time | timeFormater}}</h3>
        <!-- 过滤器 传参 -->
        <h3>现在是：{{time | timeFormater('YYYY年MM月DD日 HH:mm:ss')}}</h3>
        <!-- 过滤器 串联 -->
        <h3>现在是：{{time | timeFormater('YYYY年MM月DD日 HH:mm:ss') | mySlice}}</h3>
    </div>
</body>
<script>
    Vue.config.productionTip = false;
    var vm = new Vue({
        el: '#root',
        data: {
            time: ''
        },
        mounted() {
            this.getTime();
            
        },
        computed: {
            fmtTime() {
                return dayjs().format('YYYY年MM月DD日 HH:mm:ss') // 格式化
            }
        },
        methods: {
            getFmtTime() {
                return dayjs().format('YYYY年MM月DD日 HH:mm:ss');
            },
            getTime() {
                this.time = new Date();
                console.log(this.time);
            }
        },
        // 过滤器
        filters: {
            timeFormater(value, str) {
                return dayjs().format(str);
            },
            mySlice(value) {
                return value.slice(0,4);
            }
        }
    })
</script>

</html><!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>过滤器</title>
    <!-- 引入vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <!-- 引入dayjs -->
    <script src="../js/dayjs.min.js"></script>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>显示格式化后的时间</h2>
        <!-- 计算属性实现 -->
        <h3>现在是：{{fmtTime}}</h3>
        <!-- methods实现 -->
        <h3>现在是：{{getFmtTime()}}</h3>
        <!-- 过滤器实现 -->
        <h3>现在是：{{time | timeFormater}}</h3>
        <!-- 过滤器 传参 -->
        <h3>现在是：{{time | timeFormater('YYYY年MM月DD日 HH:mm:ss')}}</h3>
        <!-- 过滤器 串联 -->
        <h3>现在是：{{time | timeFormater('YYYY年MM月DD日 HH:mm:ss') | mySlice}}</h3>
    </div>
</body>
<script>
    Vue.config.productionTip = false;
    var vm = new Vue({
        el: '#root',
        data: {
            time: ''
        },
        mounted() {
            this.getTime();
            
        },
        computed: {
            fmtTime() {
                return dayjs().format('YYYY年MM月DD日 HH:mm:ss') // 格式化
            }
        },
        methods: {
            getFmtTime() {
                return dayjs().format('YYYY年MM月DD日 HH:mm:ss');
            },
            getTime() {
                this.time = new Date();
                console.log(this.time);
            }
        },
        // 过滤器
        filters: {
            timeFormater(value, str) {
                return dayjs().format(str);
            },
            mySlice(value) {
                return value.slice(0,4);
            }
        }
    })
</script>

</html>
```

过滤器串联的传参示意：

![image-20220318162436359](https://gitee.com/v876774538/my-img/raw/master/image-20220318162436359.png)

### 2.全局过滤器

```js
Vue.filter(id, [definition]);
```

- `{string} id`
- `{Function} [definition]`

注册或获取全局过滤器。

```js
// 注册
Vue.filter('my-filter', function (value) {
  // 返回处理后的值
})

// getter，返回已注册的过滤器
var myFilter = Vue.filter('my-filter')
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>过滤器</title>
    <!-- 引入vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    <!-- 引入dayjs -->
    <script src="../js/dayjs.min.js"></script>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>显示格式化后的时间</h2>
        <h3>现在是：{{time | timeFormater('YYYY年MM月DD日 HH:mm:ss') | mySlice}}</h3>
    </div>
</body>
<script>
    Vue.config.productionTip = false;
    // 过滤器（全局）
    Vue.filter('mySlice', function(value) {
        return value.slice(0,4);
    })
    var vm = new Vue({
        el: '#root',
        data: {
            time: ''
        },
        mounted() {
            this.getTime();
        },
        methods: {
            getTime() {
                this.time = new Date();
                console.log(this.time);
            }
        },
        // 过滤器（局部）
        filters: {
            timeFormater(value, str) {
                return dayjs().format(str);
            },
        }
    })
</script>

</html>
```

过滤器配合`v-bind:属性`使用：

```
<h3 :x="msg | mySlice">尚硅谷</h3>
```

```js
data:{
	msg:'你好，尚硅谷'
}
```

![image-20220318163643387](https://gitee.com/v876774538/my-img/raw/master/image-20220318163643387.png)

注意：**禁止配合v-model使用**。

## 十三、内置指令

### 1.v-text

1. 作用：向其所在的节点中渲染文本内容。
2. 与插值语法的区别：v-text会替换掉节点中的内容，{{xxx}}不会。

```html
<!-- 准备好一个容器 -->
<div id="root">
    <div>{{name}}</div>
    <div v-text="name"></div>
</div>
```

```js
Vue.config.productionTip = false;
var vm = new Vue({
    el: '#root',
    data: {
        name:'尚硅谷'
    },
    methods: {

    },
})
```

### 2.v-html

1. 作用：向指定节点中渲染包含html结构的内容；
2. 与插值语法的区别：
   - v-html会替换掉节点中所有的内容，{{xxx}}不会；
   - v-html可以识别Html结构。
3. 注意：**v-html有安全性问题！**
   - 在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击；
   - 一定要**在可信的内容上使用v-html**，绝对不要用在用户提交的内容上！

```html
<!-- 准备好一个容器 -->
<div id="root">
    <div class="content" v-for="(item,index) in list" :key="index">
        <div class="title">{{item.title}}</div>
        <div class="des" v-html="item.des"></div>
    </div>
</div>
```

```js
Vue.config.productionTip = false;
var vm = new Vue({
    el: '#root',
    data: {
        list:[{
            title: '标题',
            des: '<br>描述'
        }]
    },
    methods: {

    },
})
```

![image-20220318170947989](https://gitee.com/v876774538/my-img/raw/master/image-20220318170947989.png)

![image-20220318170954334](https://gitee.com/v876774538/my-img/raw/master/image-20220318170954334.png)

### 3.v-cloak

1. **没有值，不需要表达式**，本质是一个特殊属性，**在Vue实例创建完毕并接管容器后，会删掉v-cloak属性。**
2. 作用：使用CSS配合v-cloak可以解决网速慢时页面展示出未经渲染的画面的问题。

```css
[v-cloak] {
  display: none;
}
```

```html
<div v-cloak>
  {{ message }}
</div>
```

### 4.v-once

1. v-once所在节点**在初次动态渲染后，就视为静态内容**；
2. 之后数据的改变都不会引起v-once所在结构的更新，可用于优化性能。

```html
<!-- 准备好一个容器 -->
<div id="root">
    <h2 v-once>初始化的n值是：{{n}}</h2>
    <h2>当前的n值是：{{n}}</h2>
    <button @click="n++">点我n+1</button>
</div>
```

```js
var vm = new Vue({
    el: '#root',
    data: {
        n:0
    },
    methods: {

    },
})
```

![image-20220318172533547](https://gitee.com/v876774538/my-img/raw/master/image-20220318172533547.png)

### 5.v-pre

1. v-pre指令可使Vue**跳过其所在节点的编译过程**；
2. 可以利用v-pre跳过没有使用指令语法、插值语法的节点，加快编译。

```html
<span v-pre>{{ this will not be compiled }}</span>
```

![image-20220318173138301](https://gitee.com/v876774538/my-img/raw/master/image-20220318173138301.png)

## 十四、自定义指令

### 1.局部自定义指令

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>自定义指令</title>
    <!-- 引入vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="root">
        <h2>当前的n值是：<span v-text="n"></span></h2>
        <!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span></h2> -->
        <h2>放大10倍后的n值是：<span v-big="n"></span></h2>
        <button @click="n++">点我n+1</button><br>
        <input type="text" v-fbind:value="n">
    </div>
</body>
<script>
    Vue.config.productionTip = false;
    var vm = new Vue({
        el: '#root',
        data: {
            n: 0
        },
        methods: {

        },
        // 自定义指令
        directives: {
            // 函数式
            // big:function() {

            // }
            // big函数何时被调用？
            // 1.指令与元素成功绑定时（一开始）；
            // 2.指令所在的模板被重新解析时。

            // 完整形式
            // 命名用-隔开
            
            // 'big-number'(element, binding) {
            //     console.log(element, binding.value);
            //     element.innerText = binding.value * 10;
            // },
            big(element, binding) {
                console.log(element, binding.value);
                element.innerText = binding.value * 10;
            },

            // fbind(element, binding) {
            //     element.value = binding.value;
            //     element.focus();    // 获取焦点 // 不奏效   // 需要在出现在页面后调用才能奏效
            // }
            // 对象式
            fbind: {
                // 指令与元素成功绑定时调用
                bind(element, binding) {
                    element.value = binding.value;
                },
                // 指令所在元素被插入页面时调用
                inserted(element, binding) {
                    element.focus();
                },
                // 指令所在的模板被重新解析时调用
                update(element, binding) {
                    element.value = binding.value;
                }
            }
        }
    })
</script>

</html>
```

### 2.全局自定义指令

```js
Vue.directive(id, [definition])
```

- `{string} id`
- `{Function | Object} [definition]`

注册或获取全局指令。

```js
// 注册
Vue.directive('my-directive', {
  bind: function () {},
  inserted: function () {},
  update: function () {},
  componentUpdated: function () {},
  unbind: function () {}
})

// 注册 (指令函数)
Vue.directive('my-directive', function () {
  // 这里将会被 `bind` 和 `update` 调用
})

// getter，返回已注册的指令
var myDirective = Vue.directive('my-directive')
```

### 3.总结

1. 定义语法

   - 局部指令：

     ```js
     new Vue({
     	directives: {
     		指令名: {
     			配置对象;
     		}
     	}
     })
     // 或
     new Vue({
     	directives() {}
     })
     ```

   - 全局指令：

     ```js
     Vue.directive(指令名, {
     	配置对象;
     	}
     )
     // 或
     Vue.directive(指令名, function() {
     	// 回调函数
     })
     ```

2. 配置对象中常用的3个回调

   - bind：指令与元素成功绑定时调用；
   - inserted：指令所在元素被插入页面时调用；
   - update：指令所在模板结构被重新解析时调用。

3. 备注

   - 指令定义时不加v-，使用时加v-；
   - 指令明若由多个单词构成，要使用kebab-case命名方式，而不采取camelCase命名。

## 十五、生命周期

### 1.概念

生命周期又名生命周期回调函数、生命周期函数、生命周期钩子。是Vue在关键时刻帮我们调用的一些特殊名称的函数。

生命周期函数的名字不可更改，但函数的具体内容是由程序员根据需求编写的。

生命周期函数中的this指向是**vm**或**组件实例对象**。

### 2.生命周期钩子

![image-20220321104237558](https://gitee.com/v876774538/my-img/raw/master/image-20220321104237558.png)

![image-20220321111238386](https://gitee.com/v876774538/my-img/raw/master/image-20220321111238386.png)

### 3.生命周期实例方法

#### 3.1 挂载

```js
vm.$mount( [elementOrSelector] )
```

- `{Element | string} [elementOrSelector]`
- `{boolean} [hydrating]`

如果 Vue 实例在实例化时没有收到 el 选项，则它处于“未挂载”状态，没有关联的 DOM 元素。可以使用 `vm.$mount()` **手动地挂载一个未挂载的实例**。

如果没有提供 `elementOrSelector` 参数，模板将被渲染为文档之外的的元素，并且你必须使用原生 DOM API 把它插入文档中。

这个方法返回实例自身，因而可以链式调用其它实例方法。

```js
var MyComponent = Vue.extend({
  template: '<div>Hello!</div>'
})

// 创建并挂载到 #app (会替换 #app)
new MyComponent().$mount('#app')

// 同上
new MyComponent({ el: '#app' })

// 或者，在文档之外渲染并且随后挂载
var component = new MyComponent().$mount()
document.getElementById('app').appendChild(component.$el)
```

#### 3.2 更新

```js
vm.$forceUpdate()
```

迫使 Vue 实例**重新渲染**。注意它仅仅影响实例本身和插入插槽内容的子组件，而不是所有子组件。

#### 3.3 销毁

```js
vm.$destroy()
```

完全销毁一个实例。**清理它与其它实例的连接，解绑它的全部指令及事件监听器（自定义的，不包含原生）**。

触发 `beforeDestroy` 和 `destroyed` 的钩子。

注意：在大多数场景中你不应该调用这个方法。最好使用 `v-if` 和 `v-for` 指令以数据驱动的方式控制子组件的生命周期。

### 4.总结

1. 常用的生命周期钩子
   - mounted：可进行发送ajax请求、启动定时器、绑定自定义事件、订阅消息等初始化操作；
   - beforeDestroy：可进行清除定时器、解绑自定义事件、取消订阅消息等收尾工作。
2. 关于销毁Vue实例
   - 销毁后借助Vue开发者工具看不到任何信息；
   - 销毁后自定义事件会失效，但原生DOM事件依然有效；
   - 一般不会在beforeDestroy中操作数据，因为纵使对数据进行操作，也不会再触发更新流程。

## 十六、组件

### 1.模块与组件、模块化与组件化

#### 1.1 模块

1. 理解：向外提供特定功能的js程序，一般就是个js文件。
2. 作用：复用js，简化js的编码，提高js运行效率。

#### 1.2 组件

1. 理解：用来实现应用中局部（特定）功能**代码**和**资源**的**集合**。
2. 作用：复用编码，简化项目编码，提高运行效率。

### 2.非单文件组件

**一个文件中包含有n个组件。**

#### 2.1 基本使用

1. 定义组件（创建组件）

   ```js
   Vue.extend(options)
   // options和new Vue(options)时传入的options几乎相同，但也存在一点区别：
   // 1)el不写。最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器；
   // 2)data必须写成函数式。避免组件被复用时数据存在应用关系
   ```

2. 注册组件（全局/局部）

   - 局部：靠new Vue时传入components选项

     ```js
     var vm = new Vue({
         el: '#root',
         // 组件注册（局部）
         components: {
             // 组件名: 组件
         },
         data: {
     
         },
         methods: {
     
         },
     })
     ```

   - 全局：

     ```js
     Vue.component('组件名', 组件);
     ```

3. 使用组件（写组件标签）

   ```html
   <组件名></组件名>
   ```

   

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>基本使用</title>
    <!-- 引入vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="root">
        <hello></hello>
        <school></school>
        <hr>
        <student></student>
    </div>
    <div id="root1">
        <hello></hello>
    </div>
</body>
<script>
    Vue.config.productionTip = false;

    const school = Vue.extend({
        template: `
            <div>
                <h2>学校名：{{schoolName}}</h2>
                <h2>学校地址：{{address}}</h2>
            </div>
        `,
        // 组件中data只能写成函数式
        data() {
            return {
                // 不写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于谁
                schoolName: '尚硅谷',
                address: '北京昌平'
            }
        }
    })
    const student = Vue.extend({
        template: `
            <div>
                <h2>学生名：{{studentName}}</h2>
                <h2>学生年龄：{{age}}</h2>
            </div>
        `,
        data() {

            return {
                studentName: '张三',
                age: 18
            }
        }
    })
    const hello = Vue.extend({
        template: `
            <div>
                <h2>Hello!{{name}}</h2>
            </div>
        `,
        data() {
            return {
                name: 'Shiori'
            }
        }
    })
    // 组件注册（全局）
    Vue.component('hello', hello);
    // 创建vm Vue实例对象
    var vm = new Vue({
        el: '#root',
        // 组件注册（局部）
        components: {
            // school: school,
            school,
            student
        },
        data: {

        },
        methods: {

        },
    })
    var vm1 = new Vue({
        el: '#root1',
        data: {

        },
        methods: {

        }
    })
</script>

</html>
```

#### 2.2 注意点

1. 关于组件名

   - 一个单词组成：首字母大写/小写均可；

   - 多个单词组成：

     - kebab-case命名：my-school
     - CamelCase命名：MySchool（需要Vue脚手架支持）

   - 备注：

     - 组件名尽可能回避HTML中已有的元素名称，例如，h1、h2……

     - 可以使用name配置项指定组件在开发者工具中呈现的名字

       ```js
       const s = Vue.extend({
       	name:'atguigu',
       	template:`...`,
       	data() {
       		...
       	}
       })
       ```

       ![image-20220321154849419](https://gitee.com/v876774538/my-img/raw/master/image-20220321154849419.png)

2. 关于组件标签

   - ```html
     <school></school>
     ```

   - ```html
     </school>
     <!-- 自闭合写法 -->
     <!-- 不使用脚手架时，会导致后续组件不能渲染 -->
     ```

3. 一个简写方式

   ```js
   const school = Vue.extend(options);
   // 可以简写为
   const school = options
   // 但是本质上还是调用Vue.extend
   ```

   ```js
   const hello = {
       template: `
           <div>
               <h2>Hello!{{name}}</h2>
           </div>
       `,
       data() {
           return {
               name: 'Shiori'
           }
       }
   }
   ```

#### 2.3 组件嵌套

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>组件嵌套</title>
    <!-- 引入vue.js -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <!-- 准备好一个容器 -->
    <div id="root">
    </div>
</body>
<script>
    Vue.config.productionTip = false;
    const student = Vue.extend({
        template: `
            <div>
                <h2>学生名：{{studentName}}</h2>
                <h2>学生年龄：{{age}}</h2>
            </div>
        `,
        data() {

            return {
                studentName: '张三',
                age: 18
            }
        }
    })
    const school = Vue.extend({
        template: `
            <div>
                <h2>学校名：{{schoolName}}</h2>
                <h2>学校地址：{{address}}</h2>
                <hr>
                <student></student>
            </div>
        `,
        // 组件中data只能写成函数式
        data() {
            return {
                // 不写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于谁
                schoolName: '尚硅谷',
                address: '北京昌平'
            }
        },
        // 组件注册
        components: {
            student
        }
    })
    const hello = Vue.extend({
        template: `
            <div>
                <h2>Hello!{{name}}</h2>
            </div>
        `,
        data() {
            return {
                name: 'Shiori'
            }
        }
    })
    // app管理所有组件
    const app = Vue.extend({
        template: `
            <div>
                <hello></hello>
                <school></school>
            </div>
        `,
        components: {
            school,
            hello
        }
    })
    var vm = new Vue({
        el: '#root',
        template: `
            <div>
                <app></app>
            </div>
        `,
        components: {
            app
        },
        data: {
        },
        methods: {

        },
    })
</script>

</html>
```

#### 2.4 VueComponent构造函数

1. school组件本质是一个名为**VueComponent的构造函数**，且不是程序员定义的，而是由Vue.extend生成的。

2. 我们只需要`<school></school>`或`</school>`，**Vue在解析时就会帮我们创建school组件的实例对象**。

3. 特别注意：**每次调用Vue.extend，返回的都是一个全新的VueComponent！**（每个组件相互独立）

4. 关于this指向：

   - 组件配置中：

     data函数、methods中的函数、watch中的函数、computed中的函数，它们的this指向的均是VueComponent实例对象；

   - new Vue()配置中：

     data函数、methods中的函数、watch中的函数、computed中的函数，它们的this指向的均是Vue实例对象。

5. VueComponent的实例对象，也可以称为组件实例对象。因为组件是可复用的Vue实例，所以它们与new Vue接收相同的选项，例如data、computed、watch、methods以及生命周期钩子等，仅有例外是像el这样根实例特有的选项。

#### 2.5 一个重要的内置关系

1. 内置关系：`VueComponent.prototype.__proto__ === Vue.prototype`
2. 关系作用：**让组件实例对象可以访问到Vue原型上的属性、方法**。

![image-20220321165225353](https://gitee.com/v876774538/my-img/raw/master/image-20220321165225353.png)

### 3.单文件组件

一个文件中只包含有1个组件。

1. 组件1 School.vue

   ```vue
   <template>
     <!-- 组件的结构 -->
     <div class="index">
       <h2>学生姓名：{{ studentName }}</h2>
       <h2>学生年龄：{{ age }}</h2>
     </div>
   </template>
   <script>
   // 组件交互相关的代码（数据、方法等）
   export default {
     // 组件交互相关的代码（数据、方法等）
     // 默认暴露
     data: {
       studentName: "Shiori",
       age: "22",
     },
   };
   </script>
   <style scoped>
   /* 组件样式 */
   </style>
   ```

2. 组件2 Student.vue

   ```vue
   <template>
     <!-- 组件的结构 -->
     <div class="index">
       <h2>学生姓名：{{ studentName }}</h2>
       <h2>学生年龄：{{ age }}</h2>
     </div>
   </template>
   <script>
   // 组件交互相关的代码（数据、方法等）
   export default {
     // 组件交互相关的代码（数据、方法等）
     // 默认暴露
     data: {
       studentName: "Shiori",
       age: "22",
     },
   };
   </script>
   <style scoped>
   /* 组件样式 */
   </style>
   ```

3. 汇总（总管）所有组件 App.vue

   ```vue
   // <v 生成模板快捷键
   <template>
     <!-- 组件的结构 -->
     <!-- 模板中必须且只有一个根元素 -->
     <div class="index">
       <Student></Student>
       <hr />
       <School></School>
     </div>
   </template>
   <script>
   // 组件引入
   import School from "./School.vue";
   import Student from "./Student.vue";
   // 组件交互相关的代码（数据、方法等）
   export default {
     components: { Student, School },
   };
   </script>
   <style scoped>
   /* 组件样式 */
   </style>
   ```

4. 入口文件 main.js

   ```js
   // main.js 入口文件
   import App from './App.vue'
   
   new Vue({
       el: '#root',
       template: `<App></App>`,
       components: {
           App
       }
   })
   ```

5. 使用页面 index.html

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>测试</title>
   </head>
   <body>
       <div id="root"></div>
       <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
       <script src="./main.js"></script>
   </body>
   </html>
   ```

   备注：实际上不能运行（需要Vue脚手架环境）

   

# Vue脚手架

## 一、初始化脚手架

### 1.说明

1. **Vue脚手架（Vue CLI, Vue Command Line Interface）**是Vue官方提供的**标准化开发工具**。
2. 文档：https://cli.vuejs.org/zh/guide/

### 2.步骤

1. 全局安装@vlue/cli

   ```
   npm install -g @vue/cli
   ```

2. 切换到创建项目的目录，使用命令创建项目

   ```
   vue create xxx
   ```

3. 启动项目

   ```
   npm run serve
   ```

4. 终止项目

   ```
   ctrl+c
   ```

## 二、Vue基础项目框架

1. **node_modules** **项目依赖js包**

   ```
   // 加载依赖包
   npm install
   ```

2. public 存放主页面（index.html）以及页签图标（favicon.ico）或一些静态资源（图片），需要注意，放在public文件夹中的静态资源，webpack进行打包时会原封不动地打包到dist文件夹中

3. **src** 项目根目录，**源码文件夹**

   - assets 静态资源，需要注意，放置在assets文件夹中的静态资源，在webpack打包时，会被当做一个模块，打包到js文件中
   - components 组件（非路由组件）
   - router 路由
   - store 状态管理
   - **views** **页面**中展示的内容
   - **App.vue** 项目的**根组件**，汇总所有组件
   - **main.js** 项目的**入口文件**，也是程序中最先执行的文件
   - .gitignore git版本管制忽略的配置
   - **package.json** 应用包配置文件，记录了项目名称、项目中存在的依赖等信息，我们可以将其认为是项目的“身份证”
   - package-lock.json 包版本控制文件（缓存性文件）
   - babel.config.js babel的配置文件。babel是一个js编译器，主要作用是将ECMAScript2015+|版本的代码，转换为向后兼容的js语法，以便能运行在当前和旧版本的浏览器或其他环境中。Vue项目中普遍使用ES6语法，若要求兼容低版本浏览器，就需要引入Babel，将ES6转换为ES5。

4. README.md 应用描述文件

## 三、render函数

### 1.render函数详解

render函数即渲染函数，它是个函数，它的参数也是一个函数(createElement)。

1. render函数的返回值(VNode)

   **VNode**（虚拟节点），也就是我们要渲染的节点。

2. render函数的参数(createElement)

   **createElement**是render函数的参数，本身也是个函数，并且有三个参数：

   - createElement函数的返回值(VNode)
   - createElement函数的参数
     - HTML标签字符串，组件选项对象，或者解析上述任何一种的一个 async 异步函数。类型：{String | Object | Function}。**必需**。
     - 一个包含模板相关属性的数据对象你可以在 template 中使用这些特性。类型：{Object}。可选。
     - 子虚拟节点 (VNodes)，由 `createElement()` 构建而成，也可以使用字符串来生成“文本虚拟节点”。类型：{String | Array}。可选。

   ```js
    /**
     * render: 渲染函数
     * 参数: createElement
     * 参数类型: Function
    */
    render: function (createElement) {
      let _this = this['$options'].parent	// 我这个是在 .vue 文件的 components 中写的，这样写才能访问this
      let _header = _this.$slots.header   	// $slots: vue中所有分发插槽，不具名的都在default里
    
      /**
       * createElement 本身也是一个函数，它有三个参数
       * 返回值: VNode，即虚拟节点
       * 1. 一个 HTML 标签字符串，组件选项对象，或者解析上述任何一种的一个 async 异步函数。必需参数。{String | Object | Function} - 就是你要渲染的最外层标签
       * 2. 一个包含模板相关属性的数据对象你可以在 template 中使用这些特性。可选参数。{Object} - 1中的标签的属性
       * 3. 子虚拟节点 (VNodes)，由 `createElement()` 构建而成，也可以使用字符串来生成“文本虚拟节点”。可选参数。{String | Array} - 1的子节点，可以用 createElement() 创建，文本节点直接写就可以
       */
      return createElement(       
        // 1. 要渲染的标签名称：第一个参数【必需】      
        'div',   
        // 2. 1中渲染的标签的属性，详情查看文档：第二个参数【可选】
        {
          style: {
            color: '#333',
            border: '1px solid #ccc'
          }
        },
        // 3. 1中渲染的标签的子元素数组：第三个参数【可选】
        [
          'text',   // 文本节点直接写就可以
          _this.$slots.default,  // 所有不具名插槽，是个数组
          createElement('div', _header)   // createElement()创建的VNodes
        ]
      )
    }
   ```

### 2.关于不同版本的Vue

- vue.js与vue.runtime.xxx.js的区别：

  - vue.js：完整版的Vue，包含核心功能+模板解析器；
  - vue.runtime.xxx.js：运行版的Vue，只包含核心功能，没有模板解析器。

- 由于vue.runtime.xxx.js没有模板解析器，不能使用template配置项，因此在main.js入口文件中，需要使用render函数接收到的createElement函数去指定具体内容。

  ```html
  <!-- index.html -->
  <!DOCTYPE html>
  <html lang="">
    <head>
      <meta charset="utf-8">
      <!-- 针对IE浏览器的一个特殊配置，含义是让IE浏览器以最高的渲染级别渲染页面 -->
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <!-- 开启移动端的理想视口 -->
      <meta name="viewport" content="width=device-width,initial-scale=1.0">
      <!-- 配置页签图标 -->
      <!-- <%= BASE_URL %>标识应用当前根目录下的favicon.ico图标 -->
      <link rel="icon" href="<%= BASE_URL %>favicon.ico">
      <!-- 配置网页标题 -->
      <title><%= htmlWebpackPlugin.options.title %></title>
    </head>
    <body>
      <!-- 若浏览器不支持js noscript标签中的元素就会被渲染 -->
      <noscript>
        <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
      </noscript>
      <div id="app"></div>
      <!-- built files will be auto injected -->
    </body>
  </html>
  
  ```

  ```vue
  // App.vue
  <template>
    <div id="app">
      <img alt="Vue logo" src="./assets/logo.png">
      <HelloWorld msg="Welcome to Your Vue.js App"/>
    </div>
  </template>
  
  <script>
  import HelloWorld from './components/HelloWorld.vue'
  
  export default {
    name: 'App',
    components: {
      HelloWorld
    }
  }
  </script>
  
  <style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  </style>
  
  ```

  ```js
  // main.js
  new Vue({
    render: h => h(App),	// 渲染App组件
  }).$mount('#app') // 将App组件放入index.html容器中
  ```

`render: h => h(App)`演变过程：

```js
render(createElement) {
	return createElement('h1','你好啊');
}

// 写成箭头函数
render: createElement => createElement('h1','你好啊');
render: h => h('h1','你好啊');
// 将创建的内容"'h1','你好啊'"替换为组件App
render: h => h(App);

// template:`<h1>你好啊</h1>`,
// components:{App}
```

## 四、默认配置

Vue脚手架隐藏了所有webpack相关的配置，若想查看具体的webpack配置，请执行：`vue inspect > output.js` （以管理员身份运行）

Vue CLI配置参考：https://cli.vuejs.org/zh/config/

## 五、ref

### 1.ref属性

`ref` 被用来**给元素或子组件注册引用信息**（id的替代）。引用信息将会注册在父组件的 `$refs` 对象上。**如果在普通的 DOM 元素上使用，引用指向的就是 真实DOM 元素；如果用在子组件上，引用就指向组件实例对象**：

```html
<!-- `vm.$refs.p` will be the DOM node -->
<p ref="p">hello</p>

<!-- `vm.$refs.child` will be the child component instance -->
<child-component ref="child"></child-component>
```

当 `v-for` 用于元素或组件的时候，引用信息将是包含 DOM 节点或组件实例的数组。

关于 ref 注册时间的重要说明：因为 ref 本身是作为渲染结果被创建的，在初始渲染的时候你不能访问它们 - 它们还不存在！`$refs` 也不是响应式的，因此你不应该试图用它在模板中做数据绑定。

### 2.vm.$refs

- **类型**：`Object`

- **只读**

- **详细**：

  一个对象，持有注册过 [`ref` attribute](https://cn.vuejs.org/v2/api/#ref) 的所有 DOM 元素和组件实例。

### 3.使用方式

1. 打标识：

   ```html
   <!-- 普通DOM元素 -->
   <h1 ref="xxx">...</h1>
   <!-- 组件 -->
   <School ref="xxx"></School>
   ```

2. 获取：

   ```js
   this.$refs.xxx
   ```

## 六、props

功能：让**组件接收**外部传过来的**数据**。（**父传子**）

1. 传递数据

   ```html
   <Demo name="xxx"/>
   ```

2. 接收数据

   ```js
   // 简单接收
   props:['name', 'age', 'sex']
   
   // 接收的同时对数据类型进行限制
   props: {
   name: String,
   age: Number,
   sex: String,
   },
   
   // 接收的同时对数据进行类型限制+默认值的指定+必要性的限制
   props: {
   name: {
     type: String, // 字符串型
     required: true, // 必须
   },
   age: {
     type: Number,
     default: 99, // 默认值
   },
   sex: {
     type: String,
     required: true,
   },
   },
   ```

   备注：props是只读的，Vue底层会监测你对props的修改，因此若进行修改，就会发出警告。若业务需求需要修改，那么请复制props的内容到data中，然后去修改data中的数据。

   ```vue
   // Student.vue
   <template>
     <div class="index">
       <h2>姓名：{{ name }}</h2>
       <h2>年龄：{{ myAge }}</h2>
       <h2>性别：{{ sex }}</h2>
       <button @click="updataAge">修改年龄</button>
     </div>
   </template>
   
   <script>
   export default {
     name: "Student",
     // 接收的同时对数据进行类型限制+默认值的指定+必要性的限制
     props: {
       name: {
         type: String, // 字符串型
         required: true, // 必须
       },
       age: {
         type: Number,
         default: 99, // 默认值
       },
       sex: {
         type: String,
         required: true,
       },
     },
     data() {
       return {
         myAge: this.age,
       };
     },
     methods: {
       updataAge() {
         this.myAge++;
       },
     },
   };
   </script>
   
   <style>
   </style>
   ```

   ```vue
   // App.vue
   <template>
     <div id="app">
       <Student name="Shi" :age="22" sex="女"></Student>
     </div>
   </template>
   
   <script>
   import Student from "./components/Student.vue";
   
   export default {
     name: "App",
     components: {
       Student,
     },
     data() {
       return {
   
       };
     },
   };
   </script>
   
   <style>
   #app {
     font-family: Avenir, Helvetica, Arial, sans-serif;
     -webkit-font-smoothing: antialiased;
     -moz-osx-font-smoothing: grayscale;
     text-align: center;
     color: #2c3e50;
     margin-top: 60px;
   }
   </style>
   
   ```

## 七、组件命名问题

### 1.问题

![image](https://img2022.cnblogs.com/blog/2346814/202202/2346814-20220219154434724-1439390361.png)

### 2.解决方法

> 关闭ESLint语法检查。

1. 在项目的**根目录**找到(没有就创建)`vue.config.js`文件

   ![image](https://img2022.cnblogs.com/blog/2346814/202202/2346814-20220219155716767-1957813855.png)

2. 在文件中添加如下内容

   ```js
   const { defineConfig } = require('@vue/cli-service')
   module.exports = defineConfig({
    lintOnSave:false
   })
   ```

3. 保存并重新编译（`npm run serve`）

## 八、mixin混入

功能：混入(mixin)提供了一种非常灵活的方式，来分发Vue组件中可复用的功能。可以把多个组件**共用的配置**提取成一个混入对象。

> 一个混入对象可以包含任意组件选项（如`data`、`methods`、`mounted`等等）。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。

1. 定义混合

   ```js
   export const mixin = {
       data(){...},
       methods: {
           ...
       },
   }
   ```

2. 使用混合

   ```js
   import {mixin} from "..."
   
   // 全局 main.js
   Vue.mixin(mixin)	// 一旦使用全局混入，它将影响每一个之后创建的 Vue 实例。
   				   // 使用恰当时，这可以用来为自定义选项注入处理逻辑。
   
   // 局部 xxx.vue
   mixins:[mixin]
   ```

## 九、插件

功能：用于增强Vue

本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据。

1. 定义插件

   ```js
   对象.install = function (Vue, options) {
   	// 1. 添加全局过滤器
   	Vue.filter(...)
   	
   	// 2. 添加全局指令
   	Vue.directive(...)
   	
   	// 3. 配置全局混入
   	Vue.mixin(...)
   	
   	// 4. 在原型上添加实例方法
   	Vue.prototype.$myMethod = funcion() {...}
   	Vue.prototype.$myProperty = xxx
   }
   ```

2. 使用插件

   ```js
   // 全局使用 main.js
   import xxx from "...."
   
   Vue.use(xxx)
   ```

## 十、scoped样式

### 1.scoped

作用：让样式在局部生效，防止类名冲突。

```vue
<style lang="less" scoped>
    .index {
        background-color: pink;
    }
</style>
```

### 2.公共样式

1. 公共样式可以写在：

   assets/style/目录

   ![img](https://www.h5w3.com/wp-content/uploads/2020/09/bVbMcWN.png)

   或static/css/目录下

2. 引入

   - 在main.js中引入

     ```js
     import Vue from 'vue'
     import App from './App' // 引入App这个组件
     import router from './router' /* 引入路由配置 */
     import axios from 'axios'
     import '../static/css/base.css' /*引入公共样式*/
     ```

   - 在index.html中引入

     ```html
     <!DOCTYPE html>
     <html>
       <head>
         <meta charset="utf-8">
         <meta name="viewport" content="width=device-width,initial-scale=1.0">
         <title>test</title>
         <link rel="stylesheet" type="text/css" href="static/css/base.css"/>
       </head>
       <body>
         <div id="app"></div>
         <!-- built files will be auto injected -->
       </body>
     </html>
     ```

   - 在App.vue中引入

     ```vue
     <template>
       <div id="app">
         <router-view/>
       </div>
     </template>
     <script>
     export default {
       name: 'app'
     }
     </script>
      
     <style>
       @import './../static/css/bse.css'; /*引入公共样式*/
     </style>
     ```

## 十一、TodoList案例

### 1.组件化编码流程

1. 拆分静态组件：组件按照功能点拆分，命名不与html元素冲突；
2. 实现动态组件：考虑好数据的存放位置，数据是一个组件使用，还是一些组件使用：
   - 一个组件使用：存放在组件自身即可；
   - 一些组件使用：存放在他们共同的父组件上。
3. 实现交互：从绑定事件开始。

### 2.props适用于

1. 父组件==>子组件
2. 子组件==>父组件（父组件先给子组件一个函数）

### 3.使用v-model注意

1. v-model绑定的值不能是props传过来的值（props原则上是不可修改的）
2. props传过来的若是对象类型的值，修改对象中的属性时Vue并不会报错，但不推荐这样做。

### 4.WebStorage

1. 存储内容大小一般支持5MB左右；
2. 浏览器通过Window.sessionStorage和Window.localStorage属性来实现本地存储机制。

#### 4.1 localStorage

localStorage 和 sessionStorage 属性允许在浏览器中存储 key/value 对的数据。

localStorage 用于**长久保存整个网站的数据**，保存的数据没有过期时间，直到手动去删除。

localStorage 属性是**只读**的。

**提示:** 如果你只想将数据保存在当前会话中，可以使用 [sessionStorage](https://www.runoob.com/jsref/prop-win-sessionstorage.html) 属性， 该数据对象临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。

```js
window.localStorage
```

1. 保存数据：

   ```js
   localStorage.setItem("key", "value");
   ```

   ```js
   let p = {name: "张三", age: 18};
   // 值默认会被转为字符串
   localStorage.setItem('msg1','Hello')
   localStorage.setItem('msg2',666);
   localStorage.setItem('person', JSON.stringify(p));
   ```

2. 读取数据：

   ```js
   var lastname = localStorage.getItem("key");
   ```

   ```js
   console.log(localStorage.getItem('msg1'));
   console.log(localStorage.getItem('msg2'));
   const result = localStorage.getItem('person');
   console.log(JSON.parse(result));
   ```

3. 删除数据：

   ```js
   localStorage.removeItem("key");
   ```

4. 清空数据：

   ```js
   localStorage.clear();
   ```

#### 4.2 sessionStorage

localStorage 和 sessionStorage 属性允许在浏览器中存储 key/value 对的数据。

sessionStorage 用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。

**提示:** 如果你想在浏览器窗口关闭后还保留数据，可以使用 [localStorage](https://www.runoob.com/jsref/prop-win-localstorage.html) 属性， 该数据对象没有过期时间，今天、下周、明年都能用，除非你手动去删除。

```js
window.sessionStorage
```

1. 保存数据：

   ```js
   sessionStorage.setItem("key", "value");
   ```

2. 读取数据：

   ```js
   var lastname = sessionStorage.getItem("key");
   ```

3. 删除数据：

   ```js
   sessionStorage.removeItem("key");
   ```

4. 清空数据：

   ```js
   sessionStorage.clear();
   ```

#### 4.3 备注

1. sessionStorage存储的内容会随着浏览器窗口的关闭而消失；
2. localStorage存储的内容，需要手动清除才会消失；
3. `xxxxxxStorage.getItem(xxx);`如果xxx对应的value获取不到，那么getItem的返回值是null；
4. `JSON.parse(null);`的结果依然是null。

### 5.组件自定义事件

#### 5.1 案例

1. App.vue

   ```html
   <template>
     <div id="app">
       <h1>你好！</h1>
         
       <!-- 通过父组件给子组件传递函数类型的props实现：子给父传递数据 -->
       <Student :getStudentName="getStudentName"></Student>
       <!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据（第一种写法 @/v-on） -->
       <!-- <School v-on:atguigu = "getSchoolName"></School>
       <School @atguigu = "getSchoolName"></School> -->
       <!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据（第二种写法 使用ref） -->
       <School ref="school" @click.native="show"></School>
       <!-- 对组件使用原生事件时，需要添加上.native修饰符 否则会被当做自定义事件处理 -->
         
       <button @click="unbind">解绑atguigu事件</button>
         
       <button @click="death">销毁当前School组件的实例</button>
   
     </div>
   </template>
   
   <script>
   import Student from "./components/Student.vue";
   import School from "./components/School.vue"
   
   export default {
     name: "App",
     components: {
       Student,
       School,
     },
     data() {
       return {
       };
     },
     methods: {
       // 接收姓名
       getStudentName(name) {
         console.log("App接收到了name",name);
       },
       getSchoolName(name) {
         console.log("getSchoolName被调用了！",name)
       },
       show() {
         alert("111");
       }
     },
     watch: {
     },
     mounted() {
       this.$refs.school.$on('atguigu',this.getSchoolName);
       // 调用了app中的getSchoolName方法，并且$on将该方法命名了一个atguigu事件名
     },
       // 解绑自定义事件
       unbind() {
         // this.$off('atguigu'); // 只适用于解绑一个自定义事件
         // this.$off(['atguigu', 'demo']); // 解绑多个自定义事件
         this.$off();  // 解绑所有自定义事件
       },
       // 销毁当前School组件实例
       death() {
         this.$destroy();  // 销毁后 所有School实例的自定义事件全都不奏效
       }
   };
   </script>
   
   <style>
   #app {
     margin: 100px auto;
     border: 1px solid #e5e5e5;
     width: 500px;
     padding: 20px 10px;
     box-sizing: border-box;
   }
   </style>
   ```

2. Student.vue

   ```html
   <template>
     <div class="index">
       <h2>姓名：{{ name }}</h2>
       <h2>年龄：{{ age }}</h2>
       <h2>性别：{{ sex }}</h2>
       <button @click="sendStudentName">发送学生姓名</button>
     </div>
   </template>
   
   <script>
   export default {
     name: "Student",
     data() {
       return {
         name: "shi",
         age: 22,
         sex: "女",
       };
     },
     props: ['getStudentName'],
     methods: {
       sendStudentName() {
         this.getStudentName(this.name);
       }
     },
   };
   </script>
   
   <style lang="less" scoped>
       .index {
           background-color: pink;
       }
   </style>
   ```

3. School.vue

   ```html
   <template>
     <div class="index">
       <h2>学校：{{ name }}</h2>
       <h2>地址：{{ address }}</h2>
       <button @click="sendSchoolName">发送学校名</button>
     </div>
   </template>
   
   <script>
   export default {
     name: "School",
     data() {
       return {
         name: "shangguigu",
         address: "beijing",
       };
     },
     methods: {
       sendSchoolName() {
         this.$emit('atguigu',this.name);
       }
     },
   };
   </script>
   
   <style>
   </style>
   ```

#### 5.2 总结

1. 一种组件间通信的方式，适用于：**子组件==>父组件**

2. 使用场景：A是父组件，B是子组件，B想给A传递数据，那么就在A中给B绑定自定义事件（事件的回调也在A中）

3. 绑定自定义事件：

   - 方法1，在父组件中：

     ```html
     <Demo @atguigu="test"/>
     <Demo v-on:atguigu="test"/>
     ```

   - 方法2，在父组件中：

     ```html
     <Demo ref="demo"/>
     <script>
         ...
     	methods: {
     		test() {
     			...
     		}
     	}
     	...
     	mounted() {
     		this.$refs.demo.$on('atguigu',this.test)
     	}
     </script>
     ```

   - 若想让自定义事件仅触发一次，使用`once`修饰符/`$once`方法

4. 触发自定义事件：

   ```js
   this.$emit('atguigu',数据);
   ```

5. 解绑自定义事件：

   ```js
   this.$off('atguigu');
   this.$off(['atguigu','demo']);
   this.$off();
   ```

6. 在组件上绑定原生DOM事件：需要使用`.native`修饰符

7. 注意：通过`this.$refs.xxx.$on('事件名',回调函数)`绑定自定义事件时，回调函数要么配置在methods中，要么采用箭头函数，否则this的指向会出问题！

### 6.全局事件总线（GlobalEventBus）

一种组件间通信的方式，用于实现**任意组件间通信**。

#### 6.1 案例

1. main.js

   ```js
   import Vue from 'vue'
   import App from './App.vue'
   
   Vue.config.productionTip = false
   
   const vm = new Vue({
     render: h => h(App),
     beforeCreate() {
       Vue.prototype.$bus = this; // 安装全局事件总线
     }
   }).$mount('#app')
   ```

2. App.vue

   ```vue
   <template>
     <div id="app">
       <h1>你好！</h1>
       <School></School>
       <Student></Student>
     </div>
   </template>
   
   <script>
   import Student from "./components/Student.vue";
   import School from "./components/School.vue"
   
   export default {
     name: "App",
     components: {
       Student,
       School,
     },
     data() {
       return {
       };
     },
     methods: {
     },
     watch: {
     },
     mounted() {
     }
   };
   </script>
   
   <style>
   #app {
     margin: 100px auto;
     border: 1px solid #e5e5e5;
     width: 500px;
     padding: 20px 10px;
     box-sizing: border-box;
   }
   </style>
   ```

3. School.vue

   ```vue
   <template>
     <div class="index">
       <h2>学校：{{ name }}</h2>
       <h2>地址：{{ address }}</h2>
       <button @click="sendSchoolName">发送学校名</button>
     </div>
   </template>
   
   <script>
   export default {
     name: "School",
     data() {
       return {
         name: "shangguigu",
         address: "beijing",
       };
     },
     methods: {
       sendSchoolName() {
         this.$bus.$emit('getSchoolName',this.name);
       }
     },
     mounted() {
       this.$bus.$on('getStudentName',(data)=>{
         console.log("我是School组件，我收到了数据",data);
       })
     },
     beforeDestroy() {
       this.$bus.$off('getStudentName');
     },
   };
   </script>
   
   <style>
   </style>
   ```

4. Student.vue

   ```vue
   <template>
     <div class="index">
       <h2>姓名：{{ name }}</h2>
       <h2>年龄：{{ age }}</h2>
       <h2>性别：{{ sex }}</h2>
       <button @click="sendStudentName">发送学生姓名</button>
     </div>
   </template>
   
   <script>
   export default {
     name: "Student",
     data() {
       return {
         name: "shi",
         age: 22,
         sex: "女",
       };
     },
     methods: {
       sendStudentName() {
         this.$bus.$emit('getStudentName',this.name);
       }
     },
     mounted() {
       this.$bus.$on('getSchoolName',(data)=>{
         console.log('我是Student组件，收到了数据',data);
       })
     },
     beforeDestroy() {
       this.$bus.$off('getSchoolName');
     },
   };
   </script>
   
   <style lang="less" scoped>
       .index {
           background-color: pink;
       }
   </style>
   ```

#### 6.2 总结

1. 安装全局事件总线

   ```js
   new Vue({
   	...
   	beforeCreate() {
   		Vue.prototype.$bus = this.	// 安装全局事件总线，this指向当前应用的vm
   	}
   })
   ```

2. 使用事件总线

   1. 接收数据：A组件想接收B组件的数据，那么就在A组件中**给$bus绑定自定义事件**，事件的**回调**（写在methods里或箭头函数）留在A组件自身。

      ```js
      methods() {
      	demo(data) {
      		....
      	}
      }
      ...
      mounted() {
      	// 给$bus绑定自定义事件'xxx'，并调用回调函数demo
      	this.$bus.$on('xxx',this.demo);
      }
      ```

   2. 提供数据：

      ```js
      this.$bus.$emit('xxx',data);
      ```

3. 在beforeDestroy钩子中，用`$off`**解绑当前组件所用到的事件**。

   ```js
   beforeDestroy() {
       this.$bus.$off('xxx');
   }
   ```

### 7.消息订阅与发布（pubsub）

1. 一种组件间通信的方式，适用于任意组件间通信。

2. 使用步骤：

   1. 安装pubsub：`npm i pubsub-js`

   2. 引入：`import pubsub from 'pubsub-js'`

   3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身。

      ```js
      methods() {
      	demo(msgName,data) {
      		...
      	}
      }
      ...
      mounted() {
      	this.pid = pubsub.subscribe('xxx', this.demo);	// 订阅消息
      }
      ```

   4. 提供数据：

      ```js
      pubsub.publish('xxx',data);
      ```

   5. 在beforeDestroy钩子中，用`pubsub.unscribe(this.pid);`取消订阅。

### 8.$nextTick

1. 语法：`this.$nextTick(回调函数)`
2. 作用：在**下一次DOM更新结束后**执行其指定的回调。当改变数据后，要**基于更新后的新DOM**进行某些操作时，要在nextTick所指定的回调函数中执行。（如先生成input，再获取焦点）。

## 十二、Vue封装的过渡与动画

1. 作用：在插入、更新或移除DOM元素时，在合适的时候给元素添加样式类名。

2. 图示：

   ![image-20220406110038176](https://gitee.com/v876774538/my-img/raw/master/image-20220406110038176.png)

3. 写法：

   1. 准备好样式：

      - 元素进入的样式：
        1. v-enter：进入的起点；
        2. v-enter-active：进入过程中；
        3. v-enter-to：进入的终点。
      - 元素离开的样式：
        1. v-leave：离开的起点；
        2. v-leave-active：离开过程中；
        3. v-leave-to：离开的终点。

   2. 使用`<transition>`包裹要过渡的元素时，并配置name属性：

      ```html
      <transition name="hello">
      	<h1 v-show="isShow">你好啊！</h1>
      </transition>
      ```

   3. 备注：若有多个元素需要过渡，则需要使用`<transition-group>`包裹元素，且需要对每个元素指定key值。

4. 案例：

   - 动画实现

     ```vue
     <template>
       <div class="index">
         <button @click="isShow = !isShow">显示/隐藏</button>
         <transition
           name="hello"
           appear
         >
           <h1 v-show="!isShow">你好啊！</h1>
         </transition>
       </div>
     </template>
     
     <script>
     export default {
       name: "Test",
       data() {
         return {
           isShow: true,
         };
       },
     };
     </script>
     
     <style>
     h1 {
       background-color: orange;
     }
     /* 动画实现 */
     /* 没配置name时：.v-enter-active */
     /* 进入时激活样式 */
     .hello-enter-active {
       animation: atguigu 1s linear;
     }
     /* 离开时激活样式 */
     .hello-leave-active {
       animation: atguigu 1s linear reverse;
     }
     @keyframes atguigu {
       from {
         transform: translateX(-100%);
       }
       to {
         transform: translateX(0px);
       }
     }
     </style>
     ```

   - 过渡实现

     ```vue
     <template>
       <div class="index">
         <button @click="isShow = !isShow">显示/隐藏</button>
         <transition
           name="hello"
           appear
         >
           <h1 v-show="!isShow">你好啊！</h1>
         </transition>
       </div>
     </template>
     
     <script>
     export default {
       name: "Test",
       data() {
         return {
           isShow: true,
         };
       },
     };
     </script>
     
     <style>
     h1 {
       background-color: orange;
     }
     /* 过渡实现 */
     /* 进入的起点、离开的终点 */
     .hello-enter,.hello-leave-to {
       transform:translateX(-100%);
     }
     .hello-enter-active,.hello-leave-active {
       transition: 0.5s linear;
     }
     /* 进入的终点、离开的起点 */
     .hello-enter-to,.hello-leave {
       transform: translateX(0);
     }
     </style>
     ```

   - 使用animate.css

     1. 安装

        ```
        npm install animate.css --save
        ```

     2. 引入

        ```js
        import 'animate.css';
        ```

     3. 添加动画的样式类名

        ```html
        <h1 class="animate__animated animate__bounce">An animated element</h1>
        ```

        ```html
        <transition-group
          name="animate__animated animate__bounce"
          enter-active-class="animate__swing"
          leave-active-class="animate__backOutUp"
          appear
        >
          <h1 v-show="!isShow" key="1">你好啊！</h1>
          <h1 v-show="isShow" key="2">Shiori</h1>
        </transition-group>
        ```

        

     ```vue
     <template>
       <div class="index">
         <button @click="isShow = !isShow">显示/隐藏</button>
         <transition-group
           name="animate__animated animate__bounce"
           enter-active-class="animate__swing"
           leave-active-class="animate__backOutUp"
           appear
         >
           <h1 v-show="!isShow" key="1">你好啊！</h1>
           <h1 v-show="isShow" key="2">Shiori</h1>
         </transition-group>
       </div>
     </template>
     
     <script>
     // 引入animate.css
     import "animate.css";
     export default {
       name: "Test",
       data() {
         return {
           isShow: true,
         };
       },
     };
     </script>
     
     <style>
     h1 {
       background-color: orange;
     }
     </style>
     ```



# Vue中的Ajax

## 一、解决开发环境Ajax跨域问题

### 1.脚手架配置代理`devServer.proxy`

> 如果你的前端应用和后端 API 服务器没有运行在同一个主机上，你需要在开发环境下将 API 请求代理到 API 服务器。这个问题可以通过 `vue.config.js` 中的 `devServer.proxy` 选项来配置。

`devServer.proxy` 可以是一个指向开发环境 API 服务器的字符串：

#### 1.1 方法一

在`vue.config.js`中添加如下配置：

```js
devServer: {
	proxy:"http://localhost:5000"	// 告诉开发服务器将任何未知请求（没有匹配到静态文件的请求）代理到http://localhost:5000
}
```

说明：

1. 优点：配置简单，请求资源时直接发给前端（8080）即可；
2. 缺点：不能配置多个代理，不能灵活地控制请求是否走代理；
3. 工作方式：当请求了前端不存在的资源时，那么该请求会转发给服务器（优先匹配前端资源）。

#### 1.2 方法二

编写`vue.config.js`配置具体代理规则：

```js
module.exports = {
	devServer: {
		proxy: {
			// api1 请求头 匹配所有以'/api1'开头的请求路径
			'/api1': {
				target: 'httpL//localhost:5000',	// 代理目标的基础路径
				ws: true,	// 用于支持websocket
				changeOrigin: true,	// 用于控制请求头中的host值（是否“说谎”）
                // changeOrigin设置为ture 服务器收到的请求头中的host为：localhost:5000（目标服务器）
                // changeOrigin设置为false 服务器收到的请求头中的host为：localhost:8080
				pathRewrite: {'^/api1':''}
			},
			'/api2': {
				target: 'httpL//localhost:5001',
				ws: true,
				changeOrigin: true,	
				pathRewrite: {'^/api2':''}
			},
		}
	}
}
```

说明：

1. 优点：可以配置多个代理，且可以灵活地控制请求是否走代理；

2. 缺点：配置略微繁琐，请求资源时必须**添加前缀**。

   ```js
   export default {
   	name:'App',
   	methods: {
   	getStudents() {
   		axios.get('http://localhost:5000/api/students').then(
   			response => {
   				console.log('请求成功了',response.data);
   			},
   			error => {
   				console.log('请求失败了',error.message);
   			}
   		)
   	}
   }
   ```

## 二、github用户搜索案例

### 1.公共css资源

1. 存放于`/src/assets/css`中

   ![image-20220406142806994](https://gitee.com/v876774538/my-img/raw/master/image-20220406142806994.png)

   在App.vue中通过import引入：

   ```js
   import './assets/css/bootstrap.css'
   ```

2. 存放于`/public/css`中

   ![image-20220406143002851](https://gitee.com/v876774538/my-img/raw/master/image-20220406143002851.png)

   在index.html中通过link引入第三方样式：

   ```html
   <link rel="stylesheet" href="<%= BASE_URL %>css/bootstrap.css"
   ```

### 2.接口地址

http://api.github.com/search/users?q=xxx

### 3.axios使用

#### 3.1 安装

```
npm install --save axios 
```

#### 3.2 main.js文件引入

```js
import Vue from 'vue'//引入vue
import axios from 'axios'//引入axios
Vue.prototype.$axios = axios;//把axios挂载到vue上
```

#### 3.3 使用

```js
getStore(){
	let that = this
	that.$axios({
    method: "post",//指定请求方式
    url: "/business-app/getCityShopList.cgi",//请求接口（相对接口，后面会介绍到）
    data: {
		cityId: cityId,
		data:{},
		isDebug:"1",
		longitude: "",
         latitude: ""
	}}).then(function(res){
    //接口成功返回结果执行
	}).catch(function(err){
	&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;//请求失败或者接口返回失败或者.then()中的代码发生错误时执行
	})
}

```

### 4.vue-resource

> vue-resource是Vue.js的一款插件，它可以通过[XMLHttpRequest](https://so.csdn.net/so/search?q=XMLHttpRequest&spm=1001.2101.3001.7020)或JSONP发起请求并处理响应。

#### 4.1 特点

1. 体积小：vue-resource非常小巧，在压缩以后只有大约12KB，服务端启用gzip压缩后只有4.5KB大小，这远比jQuery的体积要小得多。
2. 支持主流浏览器：和Vue.js一样，vue-resource除了不支持IE 9以下的浏览器，其他主流的浏览器都支持。
3. 支持Promise API和URI Templates：Promise是ES6的特性，Promise的中文含义为“先知”，Promise对象用于异步计算。 URI Templates表示URI模板，有些类似于ASP.NET MVC的路由模板。
4. 支持**拦截器**：拦截器是全局的，拦截器可以在请求发送前和发送请求后做一些处理。 拦截器在一些场景下会非常有用，比如请求发送前在headers中设置access_token，或者在请求失败时，提供共通的处理方式。

#### 4.2 使用

1. 安装

   ```
   npm install vue-resource --save-dev
   ```

2. 引用

   ```js
   /*引入Vue框架*/
   import Vue from 'vue'
   /*引入资源请求插件*/
   import VueResource from 'vue-resource'
   
   /*使用VueResource插件*/
   Vue.use(VueResource)
   ```

3. 语法

   ```js
   // 基于全局Vue对象使用http
   Vue.http.get('/someUrl', [options]).then(successCallback, errorCallback);
   Vue.http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);
   
   // 在一个Vue实例内使用$http
   this.$http.get('/someUrl', [options]).then(successCallback, errorCallback);
   this.$http.post('/someUrl', [body], [options]).then(successCallback, errorCallback);
   ```

   在发送请求后，使用**then方法来处理响应结果**，then方法有两个参数，第一个参数是响应成功时的回调函数，第二个参数是响应失败时的回调函数。

   then方法的回调函数也有两种写法，第一种是传统的函数写法，第二种是更为简洁的ES 6的Lambda写法：

   ```js
   // 传统写法
   this.$http.get('/someUrl', [options]).then(function(response){
       // 响应成功回调
   }, function(response){
       // 响应错误回调
   });
   
   // Lambda写法
   this.$http.get('/someUrl', [options]).then((response) => {
       // 响应成功回调
   }, (response) => {
       // 响应错误回调
   });
   ```

#### 4.3 请求API

- get(url, [options])
- head(url, [options])
- delete(url, [options])
- jsonp(url, [options])
- post(url, [body], [options])
- put(url, [body], [options])
- patch(url, [body], [options])

#### 4.4 options对象

发送请求时的options选项对象包含以下属性：

![img](https://images2018.cnblogs.com/blog/1158910/201803/1158910-20180328180239659-489672956.png)

#### 4.5 inteceptor拦截器

> 拦截器可以在请求发送前和发送请求后做一些处理。在response返回给successCallback或errorCallback之前，你可以修改response中的内容，或做一些处理。

![img](https://images2018.cnblogs.com/blog/1158910/201803/1158910-20180328185439691-1468459262.png)

```js
Vue.http.interceptors.push(function(request, next) {
    // ...
    // 请求发送前的处理逻辑
    // ...
    next(function(response) {
        // ...
        // 请求发送后的处理逻辑
        // ...
        // 根据请求的状态，response参数会返回给successCallback或errorCallback
        return response
    })
})
```

### 5.代码

#### 5.1 List.vue

```vue
<template>
	<div class="row">
		<!-- 展示用户列表 -->
		<div v-show="info.users.length" class="card" v-for="user in info.users" :key="user.login">
			<a :href="user.html_url" target="_blank">
				<img :src="user.avatar_url" style='width: 100px'/>
			</a>
			<p class="card-text">{{user.login}}</p>
		</div>
		<!-- 展示欢迎词 -->
		<h1 v-show="info.isFirst">欢迎使用！</h1>
		<!-- 展示加载中 -->
		<h1 v-show="info.isLoading">加载中....</h1>
		<!-- 展示错误信息 -->
		<h1 v-show="info.errMsg">{{info.errMsg}}</h1>
	</div>
</template>

<script>
	export default {
		name:'List',
		data() {
			return {
				info:{
					isFirst:true,
					isLoading:false,
					errMsg:'',
					users:[]
				}
			}
		},
		mounted() {
			this.$bus.$on('updateListData',(dataObj)=>{
				this.info = {...this.info,...dataObj}	// ES6合并对象
			})
		},
	}
</script>

<style scoped>
	.album {
		min-height: 50rem; /* Can be removed; just added for demo purposes */
		padding-top: 3rem;
		padding-bottom: 3rem;
		background-color: #f7f7f7;
	}

	.card {
		float: left;
		width: 33.333%;
		padding: .75rem;
		margin-bottom: 2rem;
		border: 1px solid #efefef;
		text-align: center;
	}

	.card > img {
		margin-bottom: .75rem;
		border-radius: 100px;
	}

	.card-text {
		font-size: 85%;
	}
</style>
```

#### 5.2 Seach.vue

```vue
<template>
	<section class="jumbotron">
		<h3 class="jumbotron-heading">Search Github Users</h3>
		<div>
			<input type="text" placeholder="enter the name you search" v-model="keyWord"/>&nbsp;
			<button @click="searchUsers">Search</button>
		</div>
	</section>
</template>

<script>
	export default {
		name:'Search',
		data() {
			return {
				keyWord:''
			}
		},
		methods: {
			searchUsers(){
				//请求前更新List的数据
				this.$bus.$emit('updateListData',{isLoading:true,errMsg:'',users:[],isFirst:false})
                // 模板字符串
				this.$http.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
					response => {
						console.log('请求成功了')
						//请求成功后更新List的数据
						this.$bus.$emit('updateListData',{isLoading:false,errMsg:'',users:response.data.items})
					},
					error => {
						//请求后更新List的数据
						this.$bus.$emit('updateListData',{isLoading:false,errMsg:error.message,users:[]})
					}
				)
			}
		},
	}
</script>

```

#### 5.3 App.vue

```vue
<template>
	<div class="container">
		<Search/>
		<List/>
	</div>
</template>

<script>
	import Search from './components/Search'
	import List from './components/List'
	export default {
		name:'App',
		components:{Search,List}
	}
</script>
```

#### 5.4 main.js

```js
//引入Vue
import Vue from 'vue'
//引入App
import App from './App.vue'
//引入插件
import vueResource from 'vue-resource'
//关闭Vue的生产提示
Vue.config.productionTip = false
//使用插件
Vue.use(vueResource)

//创建vm
new Vue({
	el:'#app',
	render: h => h(App),
	beforeCreate() {
		Vue.prototype.$bus = this	// 安装总线
	},
})
```

## 三、vue项目中常用的两个Ajax库

### 1.axios

> 通用的Ajax请求库，官方推荐，使用广泛。

### 2.vue-resource

> Vue插件库，vue1.x中使用广泛，官方已不再维护。

## 四、slot插槽

### 1.案例

#### 1.1 不使用插槽

**Category.vue**

```vue
<template>
  <div class="category">
      <h3 class="title">{{title}}分类</h3>
      <ul>
          <li v-for="(item,index) in listData" :key="index">{{item}}</li>
      </ul>
  </div>
</template>

<script>
export default {
    name:'Category',
    props:['title','listData']
}
</script>

<style>
    .category {
        background-color: skyblue;
        width: 200px;
        height: 300px;
    }
    .title {
        background-color: orange;
        text-align: center;
    }
</style>
```

**App.vue**

```vue
<template>
  <div id="app">
    <Category title="美食" :listData="foods"></Category>
    <Category title="游戏" :listData="games"></Category>
    <Category title="电影" :listData="films"></Category>
  </div>
</template>

<script>
import Category from "./components/Category.vue";

export default {
  name: "App",
  components: {
    Category,
  },
  data() {
    return {
      foods:['火锅','烧烤','小龙虾','牛排'],
      games:['红色警戒','穿越火线','劲舞团','超级玛丽'],
      films:['《教父》','《拆弹专家》','《你好，李焕英》','《尚硅谷》']
    };
  },
  methods: {},
  watch: {},
  mounted() {},
};
</script>

<style>
#app {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
</style>

```

![image-20220412111243969](https://gitee.com/v876774538/my-img/raw/master/image-20220412111243969.png)

#### 1.2 默认插槽

**Category.vue**

```vue
<template>
  <div class="category">
      <h3 class="title">{{title}}分类</h3>
      <!-- 定义一个插槽 -->
      <!-- “挖个坑” 等待组件的使用者进行填充 -->
      <slot>我是一些默认值，当组件的使用者未传递具体结构时，我会出现</slot>
  </div>
</template>

<script>
export default {
    name:'Category',
    props:['title','listData']
}
</script>

<style lang="less">
    .category {
        background-color: skyblue;
        width: 200px;
        height: 300px;
    }
    .title {
        background-color: orange;
        text-align: center;
    }
</style>
```

**App.vue**

```vue
<template>
  <div id="app">
    <Category title="美食">
      <img src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg" alt="" />
    </Category>
    <Category title="游戏"
      ><ul>
        <li v-for="(item, index) in games" :key="index">{{ item }}</li>
      </ul></Category
    >
    <Category title="电影">
      <video controls src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
    </Category>
  </div>
</template>

<script>
import Category from "./components/Category.vue";

export default {
  name: "App",
  components: {
    Category,
  },
  data() {
    return {
      foods: ["火锅", "烧烤", "小龙虾", "牛排"],
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
      films: ["《教父》", "《拆弹专家》", "《你好，李焕英》", "《尚硅谷》"],
    };
  },
  methods: {},
  watch: {},
  mounted() {},
};
</script>

<style>
#app {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
img {
    width: 100%;
}
video {
    width: 100%;
}
</style>

```

![image-20220412112637478](https://gitee.com/v876774538/my-img/raw/master/image-20220412112637478.png)

#### 1.3 具名插槽

**Category.vue**

```vue
<template>
  <div class="category">
      <h3 class="title">{{title}}分类</h3>
      <!-- 定义一个插槽 -->
      <!-- “挖个坑” 等待组件的使用者进行填充 -->
      <slot name="center">我是一些默认内容</slot>
      <slot name="footer">我是一些默认内容</slot>
  </div>
</template>

<script>
export default {
    name:'Category',
    props:['title','listData']
}
</script>

<style lang="less" scoped>
    .category {
        background-color: skyblue;
        width: 200px;
        height: 300px;
    }
    .title {
        background-color: orange;
        text-align: center;
    }
</style>
```

**App.vue**

```vue
<template>
  <div id="app">
    <Category title="美食">
      <img
        slot="center"
        src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg"
        alt=""
      />
      <a slot="footer" href="#">更多美食</a>
    </Category>
    <Category title="游戏"
      ><ul slot="center">
        <li v-for="(item, index) in games" :key="index">{{ item }}</li>
      </ul>
      <div class="foot" slot="footer">
        <a href="#">单机游戏</a>
        <a href="#">网络游戏</a>
      </div>
    </Category>
    <Category title="电影">
      <video
        slot="center"
        controls
        src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"
      ></video>
      <!-- template能包裹元素 且最终不生成真实的DOM元素 -->
      <!-- 针对template的新写法 v-slot:名字-->
      <template v-slot:footer>
        <div class="foot">
          <a href="#">经典</a>
          <a href="#">热门</a>
          <a href="#">推荐</a>
        </div>
        <h4>欢迎前来观影！</h4>
      </template>
    </Category>
  </div>
</template>

<script>
import Category from "./components/Category.vue";

export default {
  name: "App",
  components: {
    Category,
  },
  data() {
    return {
      foods: ["火锅", "烧烤", "小龙虾", "牛排"],
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
      films: ["《教父》", "《拆弹专家》", "《你好，李焕英》", "《尚硅谷》"],
    };
  },
  methods: {},
  watch: {},
  mounted() {},
};
</script>

<style lang="less" scoped>
#app,
.foot {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
img {
  width: 100%;
}
video {
  width: 100%;
}
h4 {
  text-align: center;
}
</style>

```

#### 1.4 作用域插槽

**Category.vue**

```vue
<template>
  <div class="category">
    <h3 class="title">{{ title }}分类</h3>
    <!-- 定义一个插槽 -->
    <!-- “挖个坑” 等待组件的使用者进行填充 -->
    <slot :games="games"></slot>
  </div>
</template>

<script>
export default {
  name: "Category",
  data() {
    return {
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
    };
  },
  props:['title'],
};
</script>

<style lang="less" scoped>
.category {
  background-color: skyblue;
  width: 200px;
  height: 300px;
}
.title {
  background-color: orange;
  text-align: center;
}
</style>
```

**App.vue**

```vue
<template>
  <div id="app">
    <Category title="游戏">
      <template scope="category">
        <ul>
          <li v-for="(item, index) in category.games" :key="index">
            {{ item }}
          </li>
        </ul>
      </template>
    </Category>

    <Category title="游戏"
      >]
      <!-- 解构赋值 -->
      <template scope="{games}">
        <ol>
          <li v-for="(item, index) in games" :key="index">
            {{ item }}
          </li>
        </ol>
      </template>
    </Category>

    <Category title="游戏"
      >]
      <!-- 解构赋值 -->
      <template slot-scope="{games}">
        <h4 v-for="(item, index) in games" :key="index">
          {{ item }}
        </h4>
      </template>
    </Category>
  </div>
</template>

<script>
import Category from "./components/Category.vue";

export default {
  name: "App",
  components: {
    Category,
  },
  data() {
    return {};
  },
  methods: {},
  watch: {},
  mounted() {},
};
</script>

<style lang="less" scoped>
#app,
.foot {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
img {
  width: 100%;
}
video {
  width: 100%;
}
h4 {
  text-align: center;
}
</style>

```

![image-20220412140332626](https://gitee.com/v876774538/my-img/raw/master/image-20220412140332626.png)

### 2.总结

1. 作用：让父组件可以向**子组件指定位置插入html结构**，也是组件通信方式的一种。适用于**父组件===>子组件**。

2. 分类：默认插槽、具名插槽、作用域插槽。

3. 使用方式：

   1. 默认插槽

      父组件：

      ```html
      <Category>
      	<div>Html结构1</div>
      </Category>
      ```

      子组件：

      ```html
      <template>
      	<div>
      		<!-- 定义插槽 -->
      		<slot>插槽默认内容<slot>
      	</div>
      </template>
      ```

   2. 具名插槽

      父组件：

      ```html
      <Category>
      	<template slot="center">
      		<div>Html结构1</div>
      	</template>
      	<template v-slot:footer>
      		<div>Html结构2</div>
      	</template>
      </Category>
      ```

      子组件：

      ```html
      <template>
      	<slot name="center">插槽默认内容</slot>
      	<slot name="footer">插槽默认内容</slot>
      </template>
      ```

   3. 作用域插槽

      > **数据在组件的自身（子），但根据数据生成的结构需要组件的使用者（父）来决定。** 如，games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定。

      父组件：

      ```html
      <Category>
      	<template scope="scopeData">
      		<ul>
      			<li v-for="(item, index) in scopeData.games" :key="index">{{item}}</li>
      		</ul>
      	</template>
          <template slot-scope="scopeData">
      		<ol>
      			<li v-for="(item, index) in scopeData.games" :key="index">{{item}}</li>
      		</ol>
      	</template>
      </Category>
      ```

      子组件：

      ```vue
      <template>
      	<div>
      		<!-- 将games传递给父组件 -->
      		<slot :games="games"></slot>
      	</div>
      </template>
      
      <script>
      	export default {
      		name:'Category',
      		props:['title'],
      		// 数据在子组件自身
      		data() {
      			return {
      				games:['红色警戒','穿越火线','剑网3'];
      			}
      		}
      	}
      </script>
      ```

# Vuex

## 一、概念

> 专门在Vue中实现**集中式状态（数据）管理**的一个**Vue插件**。对Vue应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。

### 1.图解

![image-20220412143428629](https://gitee.com/v876774538/my-img/raw/master/image-20220412143428629.png)

![image-20220412143810202](https://gitee.com/v876774538/my-img/raw/master/image-20220412143810202.png)

### 2.Github

https://github.com/vuejs/vuex

### 3.使用场景

**多个组件需要共享数据时**：

1. 多个组件依赖于同一状态；
2. 来自不同组件的行为需要变更同一状态。

## 二、案例

### 1.Vue实现

**Count.vue**

```vue
<template>
  <div class="index">
      <h1>当前求和为：{{this.sum}}</h1>
      <select name="" id="" v-model="number">
          <option :value="1">1</option>
          <option :value="2">2</option>
          <option :value="3">3</option>
      </select>
      <button @click="add">+</button>
      <button @click="sub">-</button>
      <button @click="inOddAdd">当前求和为奇数再加</button>
      <button @click="waitAdd">等一等再加</button>
  </div>
</template>

<script>
export default {
    name:'Count',
    data() {
        return {
            sum: 0, // 当前的和
            number: 1,  // 用户选择的数字
        }
    },
    methods: {
        add() {
            this.sum += this.number;
        },
        sub() {
            this.sum -= this.number
        },
        inOddAdd() {
            if (this.sum % 2) {
                this.sum += this.number;
            }
        },
        waitAdd() {
            setTimeout(()=>{
                this.sum += this.number;
            },500);
        }
    },
}
</script>

<style lang="less" scoped>
    select,button {
        margin-right: 5px;
    }
</style>
```

**App.vue**

```vue
<template>
  <div id="app">
    <Count></Count>
  </div>
</template>

<script>
import Count from './components/Count.vue'
export default {
  name: "App",
  components: {
    Count
  },
  data() {
    return {};
  },
  methods: {},
  watch: {},
  mounted() {},
};
</script>

<style lang="less" scoped>
#app {

}

</style>

```

### 2.Vuex实现

#### 2.1 Vuex工作原理

![image-20220412150035941](https://gitee.com/v876774538/my-img/raw/master/image-20220412150035941.png)

每一个 Vuex 应用的核心就是**store**，里面又包括:

1. state（数据）：用来存放数据源，就是公共状态;
2. getters（数据加工）：有的时候需要对数据源进行加工，返回需要的数据；
3. actions（事件）：要执行的操作，可以进行同步或者异步事件
4. mutations（执行）：操作结束之后，actions通过commit更新state数据源
5. modules：使用单一状态树，致使应用的全部状态集中到一个很大的对象，所以把每个模块的局部状态分装使每一个模块拥有本身的 state、mutation、action、getters、甚至是嵌套子模块；

所以，简单的来说，vuex的**工作流程**就是：

1. 通过dispatch去提交一个actions，
2. actions接收到这个事件之后，在actions中可以执行一些异步|同步操作，根据不同的情况去分发给不同的mutations，
3. actions通过commit去触发mutations，
4. mutations去更新state数据，state更新之后，就会通知vue进行渲染。

>  Vue Components（客户）==> Actions（服务员）==> Mutations（后厨）==> State（菜）

#### 2.2 搭建Vuex环境

1. 安装

   ```
   npm install vuex --save
   ```

   备注：Vue2中，使用Vuex3版本；Vue3中，使用Vuex4

2. 创建文件：**src/store/index.js**

   ```js
   // 创建Vuex中最为核心的store
   import Vue from 'vue'
   // 引入Vuex
   import Vuex from 'vuex'
   Vue.use(Vuex)
   
   // 准备Actions——用于响应组件中的动作
   const actions = {}
   // 准备Mutations——用于操作数据（State）
   const mutations = {}
   // 准备State——用于存储数据
   const state = {}
   
   // 创建Store并导出（暴露）store
   export default new Vuex.Store({
       actions,
       mutations,
       state,
   })
    
   ```

3. 在**main.js**中创建vm时传入store配置项

   ```js
   import Vue from 'vue'
   import App from './App.vue'
   import axios from 'axios'
   
   // 引入store
   import store from './store/index.js'
   
   
   Vue.config.productionTip = false
   Vue.prototype.$axios = axios; // 把axios挂载到Vue上
   
   const vm = new Vue({
     render: h => h(App),
     store,
     beforeCreate() {
       Vue.prototype.$bus = this; // 安装全局事件总线
     }
   }).$mount('#app')
   ```

#### 2.3 基本使用

1. 组件中读取vuex数据：$store.state.数据名

2. 组件中修改vuex数据：

   通知 `$store.dispatch('action中的方法名', 数据);`

   操作 `$store.commit('mutation中的方法名', 数据);`

   若没有网络请求或其他业务逻辑，在组件中也可以越过actions(直接commit)。

#### 2.4 实现

**Count.vue**

```vue
<template>
  <div class="index">
      <h1>当前求和为：{{$store.state.sum}}</h1>
      <select name="" id="" v-model="number">
          <option :value="1">1</option>
          <option :value="2">2</option>
          <option :value="3">3</option>
      </select>
      <button @click="add">+</button>
      <button @click="sub">-</button>
      <button @click="inOddAdd">当前求和为奇数再加</button>
      <button @click="waitAdd">等一等再加</button>
  </div>
</template>

<script>
export default {
    name:'Count',
    data() {
        return {
            number: 1,  // 用户选择的数字
        }
    },
    methods: {
        add() {
            // this.$store.dispatch('add', this.number);
            // 没有业务逻辑 跳过dispatch==>actions 直接commit==>mutations
            this.$store.commit('ADD', this.number);
        },
        sub() {
            // this.$store.dispatch('sub', this.number);
            this.$store.commit('SUB', this.number);
        },
        inOddAdd() {
            this.$store.dispatch('inOddAdd', this.number);
        },
        waitAdd() {
            this.$store.dispatch('waitAdd', this.number);
        }
    },
    mounted() {
        
    },
}
</script>

<style lang="less" scoped>
    select,button {
        margin-right: 5px;
    }
</style>
```

**src/store/index.js**

```js
// 创建Vuex中最为核心的store
import Vue from 'vue'
// 引入Vuex
import Vuex from 'vuex'
Vue.use(Vuex)

// 准备Actions——用于响应组件中的动作
const actions = {
    // 通知
    // add(context, value) {
    //     context.commit('ADD', value);
    // },
    // sub(context, value) {
    //     context.commit('SUB', value);
    // },
    inOddAdd(context, value) {
        if (context.state.sum % 2) {
            context.commit('ADD',value);
        }
    },
    waitAdd(context, value) {
        setTimeout(() => {
            context.commit('ADD', value);
        },500)
    }
}
// 准备Mutations——用于操作数据（State）
const mutations = {
    // 操作
    ADD(state, value) {
        state.sum += value;
    },
    SUB(state, value) {
        state.sum -= value;
    }
}
// 准备State——用于存储数据
const state = {
    sum:0,  // 当前总和
}

// 创建Store并导出（暴露）store
export default new Vuex.Store({
    actions,
    mutations,
    state,
})
 
```

**App.vue**

```vue
<template>
  <div id="app">
    <Count></Count>
  </div>
</template>

<script>
import Count from './components/Count.vue'
export default {
  name: "App",
  components: {
    Count
  },
  data() {
    return {};
  },
  methods: {},
  watch: {},
  mounted() {},
};
</script>

<style lang="less" scoped>
#app {

}

</style>

```

**main.js**

```js
import Vue from 'vue'
import App from './App.vue'
import axios from 'axios'

// 引入store
import store from './store/index.js'


Vue.config.productionTip = false
Vue.prototype.$axios = axios; // 把axios挂载到Vue上

const vm = new Vue({
  render: h => h(App),
  store,
  beforeCreate() {
    Vue.prototype.$bus = this; // 安装全局事件总线
  }
}).$mount('#app')
```

## 三、getters配置项

### 1.概念

> 当state中的数据需要经过加工后再使用时，我们可以使用getters进行**数据加工**。（类似于commputed）

### 2.使用

1. 在**store.js**中追加getters配置

   ```js
   ...
   const getters = {
   	bigSum(state) {
   		return state.sum * 10;
   	}
   }
   
   // 创建并暴露store
   export default new Vuex.Store({
   	...
   	getters,
   })
   ```

2. 组件中读取数据：`$store.getters.bigSum`

## 四、四个map方法

### 1.mapState方法

> 用于帮助我们映射**state**中的数据为**计算属性**。

```js
computed: {
    // 借助mapState生成计算属性，从state中读取数据
    // 1) 对象写法：
    ...mapState({ sum: "sum", school: "school", subject: "subject" }), // ... 扩展运算符 将mapState生成的函数展开
    // 2) 数组写法：
    ...mapState(['sum', 'school', 'subject']),
    // 相当于
    // sum() {
    //     return this.$store.state.sum;
    // },
},
```

### 2.mapGetters方法

> 用于帮助我们映射**getters**中的数据为**计算属性**。

```js
computed: {
    // 借助mapGetters生成计算属性，从state中读取数据
    // 1) 对象写法：
    ...mapGetters({ bigSum: "bigSum" }),
    // 2) 数组写法：
    ...mapGetters(['bigSum']),
    // 相当于
    // bigSum() {
    //     return this.$store.getters.bigSum;
    // },
 },
```

### 3.mapActions方法

> 用于帮助我们生成与actions对话的方法，即：包含$store.dispatch(xxx)的函数。

```js
methods: {
    // add() {
    //   // 没有业务逻辑 跳过dispatch==>actions 直接commit==>mutations
    //   this.$store.commit("ADD", this.number);
    // },
    // sub() {
    //   this.$store.commit("SUB", this.number);
    // },
    // 借助mapMutations生成对应的方法，方法中会调用commit去联系mutations
    // 1) 对象写法
    ...mapMutations({add:'ADD', sub:'SUB'}),
    // 2) 数组写法
    ...mapMutations(['ADD','SUB']),
  },
```

### 4.mapMutations方法

> 用于帮助我们生成与mutations对话的方法，即：包含$store.commit(xxx)的函数。

```js
methods: {
    // inOddAdd() {
    //   this.$store.dispatch("inOddAdd", this.number);
    // },
    // waitAdd() {
    //   this.$store.dispatch("waitAdd", this.number);
    // },
    // 借助mapActions生成对应的方法，方法中会调用dispatch去联系actions
    // 1) 对象写法
    ...mapActions({inOddAdd:'inOddAdd', waitAdd:'waitAdd'}),
    // 2) 数组写法
    ...mapActions(['inOddAdd', 'waitAdd']),
  },
```

求和案例优化：

```vue
<template>
  <div class="index">
    <h1>当前求和为：{{ sum }}</h1>
    <h1>当前求和放大十倍为：{{ bigSum }}</h1>
    <select name="" id="" v-model="number">
      <option :value="1">1</option>
      <option :value="2">2</option>
      <option :value="3">3</option>
    </select>
    <button @click="add(number)">+</button>
    <button @click="sub(number)">-</button>
    <button @click="inOddAdd(number)">当前求和为奇数再加</button>
    <button @click="waitAdd(number)">等一等再加</button>
  </div>
</template>

<script>
import { mapGetters, mapMutations, mapActions, mapState } from "vuex";

export default {
  name: "Count",
  data() {
    return {
      number: 1, // 用户选择的数字
    };
  },
  methods: {
    // 借助mapMutations生成对应的方法，方法中会调用commit去联系mutations
    // 1) 对象写法
    ...mapMutations({add:'ADD', sub:'SUB'}),
    // 2) 数组写法
    // ...mapMutations(['ADD','SUB']),

    // 借助mapActions生成对应的方法，方法中会调用dispatch去联系actions
    // 1) 对象写法
    ...mapActions({inOddAdd:'inOddAdd', waitAdd:'waitAdd'}),
    // 2) 数组写法
    // ...mapActions(['inOddAdd', 'waitAdd']),
  },
  mounted() {},
  computed: {
    // 借助mapState生成计算属性，从state中读取数据
    // 1) 对象写法：
    // ...mapState({ sum: "sum" }), // ... 扩展运算符 将mapState生成的函数展开
    // 2) 数组写法：
    ...mapState(['sum']),
    // 相当于
    // sum() {
    //     return this.$store.state.sum;
    // },

    // 借助mapGetters生成计算属性，从state中读取数据
    // 1) 对象写法：
    // ...mapGetters({ bigSum: "bigSum" }),
    // 2) 数组写法：
    ...mapGetters(['bigSum']),
    // 相当于
    // bigSum() {
    //     return this.$store.getters.bigSum;
    // },
  },
};
</script>

<style lang="less" scoped>
select,
button {
  margin-right: 5px;
}
</style>
```

## 五、模块化+命名空间

### 1.目的

让代码更好维护，使多种数据分类更加明确。

### 2.使用

1. 修改**store.js**

   ```js
   // 求和相关的配置
   const countOptions = {
       // 命名空间
       namespaced: true,
       actions: {
           // 通知
           inOddAdd(context, value) {
               if (context.state.sum % 2) {
                   context.commit('ADD', value);
               }
           },
           waitAdd(context, value) {
               setTimeout(() => {
                   context.commit('ADD', value);
               }, 500)
           }
       },
       mutations: {
           // 操作
           ADD(state, value) {
               state.sum += value;
           },
           SUB(state, value) {
               state.sum -= value;
           },
       },
       state: {
           sum: 0, // 当前总和
       },
       getters: {
           bigSum(state) {
               return state.sum * 10;
           }
       },
   }
   // 人员管理相关配置
   const personOptions = {
       // 命名空间
       namespaced: true,
       actions: {},
       mutations: {
           // 添加人员
           ADD_PERSON(state, value) {
               state.personList.unshift(value);
           }
       },
       state: {
           personList: [{
               id: '001',
               name: '张三'
           }, {
               id: '002',
               name: '李四'
           }]
       },
       getters: {},
   }
   
   ```

2. 开启命名空间后，组件中**读取state数据**

   ```js
   // 方式1：自己直接读取
   this.$store.state.personAbout.list
   
   // 方式2：借助mapState读取
   ...mapState('countAbout',['sum','school','subject']);
   ```

3. 开启命名空间后，组件中**读取getters数据**

   ```js
   // 方式1：自己直接读取
   this.$store.state['personAbout/firstPersonName']
   
   // 方式2：借助mapGetters读取
   ...mapGetters('countAbout',['bigSum']);
   ```

4. 开启命名空间后，组件中**调用dispatch**

   ```js
   // 方式1：自己直接调用
   this.$store.dispatch('personAbout/addPersonWang', person)
   
   // 方式2：借助mapActions
   ...mapActions('countAbout',{inOddAdd:'inOddAdd', waitAdd:'waitAdd'}),
   ```

5. 开启命名空间后，组件中**调用commit**

   ```js
   // 方式1：自己直接调用
   this.$store.commit('personAbout/ADD_PERSON', person)
   
   // 方式2：借助mapMutations
   ...mapMutations('countAbout',{add:'ADD', sub:'SUB'}),
   ```

### 3.小仓库

1. 目录

   ![image-20220429160636867](https://gitee.com/v876774538/my-img/raw/master/image-20220429160636867.png)

2. 小仓库

   ```js
   // 准备Actions——用于响应组件中的动作
   const actions = {}
   // 准备Mutations——用于操作数据（State）
   const mutations = {}
   // 准备State——用于存储数据
   const state = {}
   
   // 创建Store并导出（暴露）store
   export default({
       actions,
       mutations,
       state,
   })
   ```

3. 小仓库合并到大仓库

   ```js
   import Vue from 'vue';
   import Vuex from 'vuex';
   Vue.use(Vuex);
   // 引入小仓库
   // 将小仓库合并到大仓库
   import home from './home';
   // 对外暴露store类的一个实例
   export default new Vuex.Store({
       // 实现vuex仓库模块式开发存储数据
       modules: {
           home,
       }
   })
   ```

   

# Vue-router

## 一、相关理解

### 1.vue-router

> Vue的一个插件库，专门用来实现SPA应用。

### 2.SPA应用

1. 单页Web应用(Single Page Web Application, SPA)；
2. 整个应用只有**一个完整的页面**；
3. 点击页面中的导航链接**不会刷新页面**，只会做页面的**局部更新**；
4. 数据需要通过ajax请求获取。

![image-20220415095156426](https://gitee.com/v876774538/my-img/raw/master/image-20220415095156426.png)

### 3.路由

#### 3.1 什么是路由？

1. 一个路由（route）就是一组映射关系(key - value)；
2. key为路径，value可能是fuction或component。

#### 3.2 路由分类

1. 后端路由
   - value是function，用于处理客户端提交的请求；
   - 工作过程：服务器接收到一个请求时，根据**请求路径**找到**匹配的函数**来处理请求，返回响应数据。
2. 前端路由
   - value是component，用于展示页面内容；
   - 工作过程：当浏览器的路径改变时，对应的组件就会显示。

## 二、基本路由

### 1.基本使用

1. 安装vue-router

   ```
   npm i vue-router
   ```

   备注：vue2安装vue-router@3，vue3安装vue-router@4/vue-router（默认是最新版本）

2. 创建**src/router/index.js**编写router配置项

   ```js
   // 改文件专门用于创建整个应用的路由器
   import VueRouter from 'vue-router'
   // 引入组件
   import About from '../pages/About.vue'
   import Home from '../pages/Home.vue'
   
   // 创建并暴露一个路由器
   const router = new VueRouter ({
       routes:[
           {
               path:'/about',
               component: About
           },
           {
               path:'/home',
               component: Home
           }
       ]
   })
   
   // 暴露router
   export default router
   ```

3. **main.js**

   ```js
   import Vue from 'vue'
   import App from './App.vue'
   // 引入vue-router
   import VueRouter from 'vue-router'
   // 引入路由器配置项
   import router from './router'
   
   // 应用插件
   Vue.use(VueRouter);
   
   const vm = new Vue({
   	render: h => h(App),
   	router: router
   }).$mount('#app')
   ```

4. 借助`router-link`实现切换

   ```html
   <router-link active-class="active" to="/about">About</router-link>
   <router-link active-class="active" to="/home">Home</router-link>
   ```

5. 指定展示位置

   ```html
   <router-view></router-view>
   ```

### 2.注意

1. 路由组件通常存放在**pages**文件夹或**views**文件夹，一般组件通常存放在**components**文件夹；

   ![image-20220415104530955](https://gitee.com/v876774538/my-img/raw/master/image-20220415104530955.png)

2. 通过切换，“隐藏”了的路由组件，**默认**是被**销毁**掉的，等需要时再重新挂载；

3. 虽然只有一个路由器（router），但每个组件都有自己的`$route`属性，里面存储着自己的路由信息；

4. 整个应有只有一个router，可以用过组件的`$router`属性获取到。

## 三、嵌套（多级）路由

1. 配置路由规则，使用**children配置项**

   ```js
   export default new VueRouter({
       routes: [{
               path: '/about',
               component: About,
           },
           {
               path: '/home',
               component: Home,
               children: [
               {
                   path: 'message',
                   component: Message
               }, 
               {
                   path: 'news',
                   component: News
               }]
           }
       ]
   })
   ```

2. 借助`router-link`实现切换（需要写**完整路径**）

   ```html
   <router-link to="/home/news">News</router-link>
   ```

## 四、路由传参

### 1.query

1. 传递参数

   ```html
   <!-- 跳转路由并携带query参数，to的字符串写法 -->
   <router-link
     :to="`/home/message/messageDetail?id=${item.id}&title=${item.title}`"
     >{{ item.title }}</router-link
   >
   
   <!-- 跳转路由并携带query参数，to的对象写法 -->
   <router-link
     :to="{
       path: '/home/message/messageDetail',
       query: {
         id: item.id,
         title: item.title,
       },
     }"
   >
     {{ item.title }}
   </router-link>
   ```

2. 接收参数

   ```js
   $route.query.id
   $route.query.title
   ```

### 2.params

1. 配置路由，占位声明接收params参数

   ```js
   export default new VueRouter({
       routes: [{
               path: '/about',
               component: About,
           },
           {
               path: '/home',
               component: Home,
               children: [
               {
                   path: 'message',
                   name: 'message',
                   component: Message,
                   children: [
                       {
                           // 占位符:
                           path: 'messageDetail/:id/:title',	// 声明接收params参数
                           name: 'messageDetail',
                           component: MessageDetail,
                       },
                   ]
               }, 
               {
                   path: 'news',
                   component: News
               }]
           }
       ]
   })
   ```

2. 传递参数

   ```html
   <!-- 跳转并携带params 参数，to的字符串写法 -->
   <router-link :to="`/home/message/messageDetail/${item.id}/${item.title}`">{{ item.title }}</router-link>
   
   <!-- 跳转并携带params 参数，to的对象写法 -->
   <router-link
     :to="{
       name: 'messageDetail',
       params: {
         id: item.id,
         title: item.title
       }
     }"
   >
     {{ item.title }}
   </router-link>
   ```

   > 特别注意：路由携带params参数时，若使用to的对象写法，不能使用path配置项，必须使用name配置！（path配置时带有占位参数声明，此处无法匹配)。

3. 接收参数

   ```js
   $route.params.id
   $route.params.title
   ```

## 五、命名路由

> 给路由命名，必要时可以简化路由的跳转。

1. 给路由命名

   ```js
   export default new VueRouter({
       routes: [{
               path: '/about',
               component: About,
           },
           {
               path: '/home',
               component: Home,
               children: [
               {
                   path: 'message',
                   name: 'message',
                   component: Message,
                   children: [
                       {
                           path: 'messageDetail',
                           name: 'messageDetail',
                           component: MessageDetail,
                       }
                   ]
               }, 
               {
                   path: 'news',
                   component: News
               }]
           }
       ]
   })
   ```

2. 简化跳转

   ```html
   <!-- 跳转路由并携带query参数，to的对象写法 -->
   <!-- 简化前 -->
   <router-link
     :to="{
       path: '/home/message/messageDetail',
       query: {
         id: item.id,
         title: item.title,
       },
     }"
   >
     {{ item.title }}
   </router-link>
   
   <!-- 简化后 -->
   <!-- 注意！必须是对象写法 -->
   <router-link
     :to="{
       name: 'messageDetail',
       query: {
         id: item.id,
         title: item.title,
       },
     }"
   >
     {{ item.title }}
   </router-link>
   ```

## 六、路由的props配置

> 作用：让路由组件更方便地收到参数（params参数）

```js
export default new VueRouter({
    routes: [{
            path: '/about',
            component: About,
        },
        {
            path: '/home',
            component: Home,
            children: [{
                    path: 'message',
                    name: 'message',
                    component: Message,
                    children: [{
                            path: 'messageDetail/:id/:title',
                            name: 'messageDetail',
                            component: MessageDetail,
                            // props的第一种写法，值为对象
                            // 该对象中的所有key-value都会以props的形式传给Detail组件
                            // props: {
                            //     a: 1,
                            //     b: 'hello',
                            // }

                            // props的第二种写法，值为布尔值
                            // 若布尔值为真，就会把该路由组件收到的所有params参数，以props的形式传给Detail组件
                            // props: true

                            // props的第三种写法，值为函数
                            props($route) {
                                return {id:$route.query.id, title:$route.query.title}
                            }
                        },
                    ]
                },
                {
                    path: 'news',
                    component: News
                }
            ]
        }
    ]
})
```

```js
// 接收
prop:['id', 'title']
```

## 七、router-link的replace属性

1. 作用：控制路由跳转时操作浏览器历史记录的模式；

2. 浏览器的历史记录有两种写入方式：

   - **push**：**追加**历史记录
   - **replace**：**替换**当前记录（无法前进后退）

   路由跳转时默认为push

3. 开启replace模式：

   ```html
   <router-link replace .....>News</router-link>
   <router-link :replace="true" .....>News</router-link>
   ```

## 八、编程式路由导航

> 不借助<router-link>实现路由跳转，让路由跳转更加灵活。

```js
// 追加
this.$router.push({
	name:'messageDetail',
	params: {
		id: item.id,
		title: item.title
	}
})

// 替换
this.$router.replace({
	name:'messageDetail',
	params: {
		id: item.id,
		title: item.title
	}
})

this.$router.forward()	// 前进
this.$router.back()	// 后退
this.$router.go(n)	// 前进/后退
```

**区分$route和$router**

1. $route：一般用于获取路由信息，如路径、query、params等；
2. $router：用于编程式导航路由跳转

## 九、缓存路由组件

> 让不展示的路由组件**保持挂载**，不被销毁。

```html
<keep-alive include="News">
	<router-view></router-view>
</keep-alive>
```

## 十、两个新的生命周期钩子

> **路由组件所独有**的两个钩子，用于**捕获路由组件的激活状态**。

### 1.activated

路由组件被激活时触发。

```js
activated() {
	console.log('News组件被激活了');
    this.timer = setInterval(() => {
        console.log('@');
        this.opacity -= 0.01;
        if (this.opacity <= 0) {
            this.opacity = 1;
        }
    }, 16)
}
```

### 2.deactivated

路由组件失活时触发。

```js
deactivated() {
	console.log('News组件失活了');
    clearInterval(this.timer);
}
```

## 十一、路由守卫

> 对路由进行权限控制。

### 1.全局守卫

#### 1.1 前置守卫

```js
router.beforeEach((to, from, next) => { 
 	//	to: 目标路由
 	//	from: 当前路由  
 	// next() 跳转  一定要调用！
	next(false);//不让走
    next(true);//继续前行
    next('/login')//走哪
    next({path:'/detail/2',params:{},query:{}})//带点货

    // 守卫业务
    if(to.path=='/login' || to.path=='/reg' ){    
      next(true)
    }
    else{
    	//是否登录的判断
    	if(没有登录过){
        	next('/login');
    	}
    	else{
        	next(true);
    	}
    }
})
```

#### 1.2 后置守卫

```js
router.afterEach((to,from)=>{
	//全局后置守卫业务
})
```

**src/router/index.js**

```js
// 改文件专门用于创建整个应用的路由器
import VueRouter from 'vue-router'
// 引入组件
import About from '../pages/About/About.vue'
import Home from '../pages/Home/Home.vue'
import Message from '../pages/Home/Message/Message.vue'
import MessageDetail from '../pages/Home/Message/MessageDetail.vue'
import News from '../pages/Home/News.vue'

// 创建并暴露一个路由器
const router = new VueRouter({
    routes: [{
            path: '/about',
            component: About,
            // 路由元信息
            meta: {
                isAuth: false,
                title: '关于',
            },
        },
        {
            path: '/home',
            component: Home,
            meta: {
                isAuth: false,
                title: '主页',
            },
            children: [{
                    path: 'message',
                    name: 'message',
                    component: Message,
                    meta: {
                        isAuth: true,
                        title: '消息',
                    },

                    children: [{
                            path: 'messageDetail/:id/:title',
                            name: 'messageDetail',
                            component: MessageDetail,
                            meta: {
                                isAuth: true,
                                title: '详情',
                            },
                            props($route) {
                                return {
                                    id: $route.query.id,
                                    title: $route.query.title
                                }
                            }
                        },
                    ]
                },
                {
                    path: 'news',
                    component: News,
                    meta: {
                        isAuth: true,
                        title: '新闻'
                    },

                }
            ]
        }
    ]
})

// 全局前置路由守卫
// 路由每次切换之前被调用
router.beforeEach((to, from, next) => {
    // 判断是否需要鉴权
    if (to.meta.isAuth) {
        if (localStorage.getItem('school') === 'atguigu') {
            next(); // 放行
        } else {
            alert('无权限查看！');
        }
    } else {
        next(); // 放行
    }
})

// 全局后置路由守卫
// 路由每次切换之后被调用
router.afterEach((to, from) => {
    document.title = to.meta.title;
})

export default router
```

### 2.独享守卫

```js
{
    path: '/user',
    component: User,
    //路由独享守卫
    beforeEnter: (to, from, next) => { //路由独享守卫 前置 
        // 判断是否需要鉴权
    	if (to.meta.isAuth) {
        	if (localStorage.getItem('school') === 'atguigu') {
            	next(); // 放行
        	} else {
            	alert('无权限查看！');
        	}
    	} else {
        	next(); // 放行
    	}
    }
},
```

### 3.组件内守卫

```js
// 在组件内部写：
// 组件内部钩子
export default {
    // 通过路由规则，进入该组件时被调用
	beforeRouteEnter(to, from, next) {
		// 前置
    	// 不！能！获取组件实例 `this`
    	// 因为当守卫执行前，组件实例还没被创建
	},

	// 在当前路由改变，但是该组件被复用时调用
	beforeRouteUpdate(to, from, next) {
    	// 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    	// 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    	// 可以访问组件实例 `this`
	},
    
    // 通过路由规则，离开该组件时被调用
	beforeRouteLeave(to, from, next) {
    	//后置
    	// 导航离开该组件的对应路由时调用
    	// 可以访问组件实例 `this`
	},
}

```

## 十二、路由器的两种工作模式

1. 对于一个url来说，什么是hash值？——#及其后面的内容就是hash值。

   ![image-20220415164309862](https://gitee.com/v876774538/my-img/raw/master/image-20220415164309862.png)

2. hash值不会包含在HTTP请求中，即：**hash值不会带给服务器**。

3. hash模式：

   - 地址中永远带着#号，不美观；
   - 以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法；
   - 兼容性较好。

   ![image-20220415164645767](https://gitee.com/v876774538/my-img/raw/master/image-20220415164645767.png)

4. history模式：

   - 地址干净，美观；
   - 兼容性与hash模式相比较差；
   - 应用部署上线时需要后端人员支持，解决刷新页面时服务器404的问题。

## 十三、路由懒加载

### 1.方式一

结合Vue的异步组件和Webpack的代码分析

```js
const Home = resolve => { 
    require. ensure(['../ components/Home.vue'], () => { 
        resolve(require('../ components/Home.vue')) 
    })
};
```

### 2.方式二

AMD写法

```js
const About = resolve => require(
    [' ../ components/ About.vue'], resolve);
```

### 3.方式三

在ES6中，我们可以有更加简单的写法来组织Vue异步组件和Webpack的代码分割

```js
const Home = () => import(' . ./ components/Home.vue ' )
```

### 4.路由懒加载的效果

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210114221625407.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTYwNjA2Nw==,size_16,color_FFFFFF,t_70)

# Vue UI组件库

## 一、移动端常用UI组件库

1. Vant https://youzan.github.io/vant/#/zh-CN
2. Cube UI https://didi.github.io/cube-ui/#/zh-CN
3. Mint UI https://mint-ui.github.io/#!/zh-cn

## 二、PC端常用UI组件库

1. Element UI https://element.eleme.cn/#/zh-CN
2. iView UI https://www.iviewui.com/docs/introduce
3. Ant Design for Vue https://antdv.com/components/button-cn/

# Vue2尚品汇项目

## 一、项目搭建

### 1.脚手架使用

#### 1.1 vue-cli2.x

```
vue init webpack 项目名称
```

#### 1.2 vue-cli3.x

```
vue create 项目名称
```

### 2.配置

#### 2.1 配置项目运行自动打开浏览器

**package.json**

```json
"scripts": {
    "serve": "vue-cli-service serve --open"
  },
```

**vue.config.js**

```js
devServer: {
    open:true,
    host:'localhost'
}
```

#### 2.2 关闭ESLnit校验

**vue.config.js**

```js
module.exports = {
	// 关闭eslint
	lintOnSave: false
}
```

#### 2.3 配置src文件夹简写方式（别名）

**jsconfig.json**

```json
{
	"compilerOptions": {
		"baseUrl": "./",
		"path": {
			"@/*": [
				"src/*"
			]
		}
	},
	"exclude": [
		"node_modules",
		"dist"
	]
}
```

目前vue2已经自动配置好了，不需要手动再配置也能用。

#### 2.4 路由配置

1. 安装路由

   ```
   npm install vue-router --save
   ```

   --save 可以让你安装的依赖，在package.json文件当中进行记录

2. 创建路由管理文件夹`router/index.js`

3. 创建路由组件，存放在`views`或`pages`文件夹中

4. 在`router/index.js`中配置路由

   ```js
   import Vue from 'vue'
   import VueRouter from 'vue-router'
   
   // 使用插件
   Vue.use(VueRouter)
   
   // 配置路由
   export default new VueRouter({
     mode:'history',
     // 配置路由
     routes:[
       // 重定向
       // 在项目刚跑起来的时候，访问/立马将其定向到首页
       {
         path:'/',
         redirect:'/home'
       },
       {
         path:'/home',
         name:'home',
         component: () => import('@/pages/home/index'),
         // 路由元信息
         meta: {
           title:'首页'
         }
       },
       {
         path:'/search',
         name:'search',
         component: () => import('@/pages/search/index'),
         meta: {
           title:'搜索'
         }
       },
       {
         path:'/login',
         name:'login',
         component: () => import('@/pages/login/index'),
         meta: {
           title:'登录'
         }
       },
       {
         path:'/register',
         name:'register',
         component: () => import('@/pages/login/register'),
         meta: {
           title:'注册'
         }
       },
     ]
   })
   
   ```

5. `main.js`引入注册

### 3.less使用

1. 安装less less-loader@5

   项目采用less样式，而浏览器不识别less语法，因此需要一些loader进行处理，将less语法转换为css语法

   ```
   npm install --save less less-loader@5
   ```

2. 在编写样式时设置

   ```
   <style lang="less" scoped>
   </style>
   ```

### 4.清除vue页面默认样式

1. 清除样式文件**reset.css**

   ```css
   /* 清除内外边距 */
   body, h1, h2, h3, h4, h5, h6, hr, p, blockquote,
   dl, dt, dd, ul, ol, li,
   pre,
   fieldset, lengend, button, input, textarea,
   th, td {
       margin: 0;
       padding: 0;
   }
   
   /* 设置默认字体 */
   body,
   button, input, select, textarea { /* for ie */
       /*font: 12px/1 Tahoma, Helvetica, Arial, "宋体", sans-serif;*/
       font: 12px/1.3 "Microsoft YaHei",Tahoma, Helvetica, Arial, "\5b8b\4f53", sans-serif; /* 用 ascii 字符表示，使得在任何编码下都无问题 */
       color: #333;
   }
   
   
   h1 { font-size: 18px; /* 18px / 12px = 1.5 */ }
   h2 { font-size: 16px; }
   h3 { font-size: 14px; }
   h4, h5, h6 { font-size: 100%; }
   
   address, cite, dfn, em, var, i{ font-style: normal; } /* 将斜体扶正 */
   b, strong{ font-weight: normal; } /* 将粗体扶细 */
   code, kbd, pre, samp, tt { font-family: "Courier New", Courier, monospace; } /* 统一等宽字体 */
   small { font-size: 12px; } /* 小于 12px 的中文很难阅读，让 small 正常化 */
   
   /* 重置列表元素 */
   ul, ol { list-style: none; }
   
   /* 重置文本格式元素 */
   a { text-decoration: none; color: #666;}
   
   
   /* 重置表单元素 */
   legend { color: #000; } /* for ie6 */
   fieldset, img { border: none; }
   button, input, select, textarea {
       font-size: 100%; /* 使得表单元素在 ie 下能继承字体大小 */
   }
   
   /* 重置表格元素 */
   table {
       border-collapse: collapse;
       border-spacing: 0;
   }
   
   /* 重置 hr */
   hr {
       border: none;
       height: 1px;
   }
   .clearFix::after{
   	content:"";
   	display: block;
   	clear:both;
   }
   /* 让非ie浏览器默认也显示垂直滚动条，防止因滚动条引起的闪烁 */
   html { overflow-y: scroll; }
   
   a:link:hover{
       color : rgb(79, 76, 212) !important;
       text-decoration: underline;
   }
   
   /* 清除浮动 */
   .clearfix::after {
       display: block;
       height: 0;
       content: "";
       clear: both;
       visibility: hidden;
   }
   ```

2. 引入样式文件

   vue是单页面开发，我们只需要修改**public/index.html**文件

   ```html
   <link ref="stylesheet" href="<%= BASE_URL %>css/reset.cs
   ```

## 二、组件

### 1.全局组件

#### 1.1 商品分类导航三级联动组件

**pages/home/TypeNav/index.vue**

```vue
<script>
export default {
	name:'TypeNav'
}
</script>
```

#### 1.2 全局注册

**main.js**

```js
// 全局组件
import TypeNav from '@/pages/home/TypeNav'
// Vue.component('组件名', 组件);
Vue.component(TypeNav.name, TypeNav);
```

#### 1.3 使用

```vue
<template>
  <div class="index">
    <!-- 商品分类导航 -->
    <!-- 全局组件不用单独再在页面中import引入 也不需要在components中注册 -->
    <TypeNav></TypeNav>
  </div>
</template>  
```

### 2.局部组件

#### 2.1 首页顶部组件

**components/Header/index.vue**

#### 2.2 使用

```vue
<template>
  <div id="app">
    <!-- 使用 -->
    <Header></Header>
    <router-view></router-view>
    <!-- Home/Search页面显示 -->
    <Footer v-if="$route.meta.footerShow"></Footer>
  </div>
</template>

<script>
// 引入
import Header from '@/components/Header/index.vue';
import Footer from '@/components/Footer/index.vue';

export default {
  name: 'App',
  // 注册
  components: {
    Header,
    Footer,
  }
}
</script>

<style>
#app {

}
</style>

```

## 三、nprogress进度条的使用

### 1.安装

```
npm install --save nprogress
```

### 2.使用

**main.js** 引入

```js
// 引入进度条
import nprogress from 'nprogress'
// 引入进度条样式
import 'nprogress/nprogress.css'
```

在拦截器中使用

```js
// 请求拦截器：在发送请求前……
axios.interceptors.request.use((config) => {
    // config：配置对象，包含请求头headers
    // 进度条动画开始
    nprogress.start();
    return config;
}, function (error) {
    // 请求错误
    return Promise.reject(error);
})
// 响应拦截器
axios.interceptors.response.use((config) => {
    // 成功的回调函数：服务器响应数据返回后……
    // 进度条结束
    nprogress.done();
    return res.data;
}, function (error) {
    // 响应报错
    return Promise.reject(error);
})
```

# Nuxt

## 一、Nuxt介绍

官方文档地址：https://www.nuxtjs.cn/guide

### 1.1 概述

> Nuxt框架提供了一种基于`Vue.js`的**服务器端渲染方案**(SSR)。可以**让Vue应用在服务器端进行渲染**，从而提高页面的加载速度和`SEO`。

1. CSR

   `CSR(Client Side Rendering)`，`客户端渲染`。常见的`SPA`所使用的渲染方式，只要在客户端渲染的过程中使用到了js，**数据是通过客户端发送请求获取**并渲染的，都可以算作客户端渲染。

   CSR优点：

   - **减轻服务器压力**。服务器直接返回未加工的html，让渲染工作在客户端进行，后端专注于API开发从而实现真正的前后端分离。
   - 用户在**后续访问的操作体验好**。后续访问和页面切换速度快。

   CSR缺点：

   - **不利于SEO**。无法获取渲染后的最终html，爬虫无法爬取信息。
   - **首屏渲染时间长**。首屏加载所有资源，拖慢加载时间。

2. SSR

   `SSR(Server Side Rendering)`，即`服务器端渲染`。在服务器端对Vue页面进行渲染生成`html`页面，再将html页面传递给浏览器。

   在`Next.js`中，如果启用了SSR，那么每次请求都会重新生成页面。

   SSR优点：

   - **有利于SEO**。页面内容都在服务器生成，搜索引擎直接就可以抓取到最终页面结果。
   - **有利于首屏渲染**。

   SSR缺点：

   - **服务器压力大**。后续访问的页面切换加大服务器压力，高并发时更加明显。
   - 页面交互/跳转都会导致整个页面刷新，**体验较差**。

3. 应用场景

   

4. 



# Vue3快速上手

## 一、Vue3简介

- 2020年9月18日，Vue.js发布3.0版本，代号：One Piece（海贼王）
- 耗时2年多、2600+次提交、30+个RFC、600+次PR、99位贡献者
- github上的tags地址：https://github.com/vuejs/core/releases/tag/v3.0.0

## 二、Vue3提升

### 1.性能提升

- 打包大小减少41%
- 初次渲染快55%、更新渲染快133%
- 内存减少54%
- ...

### 2.源码升级

- 使用Proxy代替DefineProperty实现响应式
- 重写虚拟DOM的实现和Tree-Shaking（一个通常用于描述移除JavaScript上下文中的未应用代码(dead-code)行为的术语，即剔除没必要的代码）
- ...

### 3.拥抱TypeScript

- Vue3可以更好地支持TypeScript

### 4.新的特性

1. Composition API(组合API)
   - setup配置
   - ref与reactive
   - watch与watchEffect
   - provide与inject
   - ...
2. 新的内置组件
   - Fragment
   - Teleport
   - Suspense
3. 其他改变
   - 新的生命周期钩子
   - data选项应始终被声明为一个函数
   - 移除keyCode支持作为v-on的修饰符

## 三、创建Vue3.0工程

### 1.使用vue-cli创建

官方文档：http://cli.vuejs.org/zh/guide/creating-a-project.html#vue-create

```
## 查看@vue/cli版本，确保@vue/cli版本在4.5.0以上
vue --V
## 安装或升级你的@vue/cli
npm install -g @vue/cli
## 创建
vue create vue_test
## 启动
cd vue_test
npm run serve
```

### 2.使用vite创建

官方文档：http://v3.cn.vuejs.org/guide/installation.html#vite

vite官网：https://vitejs.cn

- 什么是vite？——新一代前端构建工具。
- 优势：
  - 开发环境中，无需打包操作，可快速地冷启动；
  - 轻量快速的热重载(HMR)；
  - 真正的按需编译，不再等待整个应用编译完成。

```
## 创建工程
npm init vite-app <project-name>
## 进入工程目录
cd <project-name>
## 安装依赖
npm install
## 运行
npm run dev
```

### 3.关闭语法检查

**vue.config.js**

```js
module.exports = {
	lintOnSave:false,	// 关闭语法检查
}
```

### 4.分析工程结构

#### 4.1 main.js

![image-20220420174710727](https://gitee.com/v876774538/my-img/raw/master/image-20220420174710727.png)

#### 4.2 App.vue

![image-20220420174804770](https://gitee.com/v876774538/my-img/raw/master/image-20220420174804770.png)

## 四、常用Composition API

### 1.拉开序幕的setup

1. 理解：Vue3.0中一个新的配置项，值为一个函数；
2. setup是所有Composition API（组合式API）“表演的舞台”；
3. **组件中所用到的数据、方法等，均要配置在setup中**；
4. setup函数的两种返回值：
   - **若返回一个对象，则对象中的属性、方法，在模板中均可以直接使用！**
   - 若返回一个渲染函数，则可以自定义渲染内容。
5. 注意：
   - 尽量不要与vue2.x配置混用：
     - vue2.x配置（data、methods、computed...）中**可以访问到**setup中的属性、方法；
     - 但在setup中**不能访问到**vue2.x配置（data、methods、computed...）；
     - 若有重名，setup优先。
   - **setup不能是一个async函数**，因为返回值不再是return的对象，而是promise，模板看不到return对象中的属性。（一个函数被`async`修饰后，返回值就是一个被`promise`包裹的对象，**除非组件是异步引入的，且需要Suspense的配合**）

### 2.ref函数

1. 作用：定义一个**响应式的数据**

2. 语法：`const xxx = ref(initValue)`

   - 创建一个包含响应式数据的**引用对象**（reference对象，简称ref对象）

   - 在JS中操作数据：`xxx.value`

     ref加工后的数据：

     ![image-20230207101107224](https://gitee.com/v876774538/my-img/raw/master/image-20230207101107224.png)

     ```vue
     <template>
         <h2>
             姓名：{{ name }}
         </h2>
         <h2>
             年龄：{{ age }}
         </h2>
         <button @click="changeInfo">
             修改信息
         </button>
     </template>
     
     <script>
         import {ref} from 'vue'
         export default {
         	name: 'App',
             setup() {
                 // 数据
                 let name = ref('张三')
                 let age = 18
                 let job = ref({
                     type: '前端',
                     salary:'30K'
                 })
                 
                 // 方法
                 function chagneInfo() {
                     // name = '李四'
                     // age = 48
                     // 修改
                     name.value = '李四'
                     age.value = 48
                     console.log(name, age)
                     job.value.type = '后端'
                 }
                 
                 // 返回一个对象（常用）
                 return {
                     name,
                     age,
                     changeInfo
                 }
             }
         }
     </script>
     ```

   - 模板中读取数据：不需要`.value`，而是直接`<div>{{ xxx }}</div>`

3. 说明：

   - **接收的数据可以是：基本类型、也可以是对象类型**
   - 基本类型的数据：响应式依然是靠`Object.defineProperty()`的`get`和`set`完成的
   - 对象类型的数据：内部“求助”了Vue3.0中的一个新函数——`reactive`函数

### 3.reactive函数

1. 作用：定义一个**对象类型**的**响应式数据**

2. 语法：`const 代理对象 = reactive(被代理对象)`。接收一个对象（或数组），返回一个代理器对象（proxy对象）

3. 说明：

   - reactive定义的响应式数据是**深层次的**

     ```vue
     <template>
         <h2>
             姓名：{{ name }}
         </h2>
         <h2>
             年龄：{{ age }}
         </h2>
         <h2>
             性别：{{ sex }}
         </h2>
         <button @click="changeInfo">
             修改信息
         </button>
     </template>
     
     <script>
         import {ref} from 'vue'
         export default {
         	name: 'App',
             setup() {
                 // 数据
                 let name = ref('张三')
                 let age = 18
                 let job = reactvie({
                     type: '前端',
                     salary:'30K'.
                     sex: '女',
                     a: {
                     	b: {
                     		c: 200
     	    		    }
         	      	}
                 })
             let hobby = reative(['打游戏', '听歌', '看动漫'])
                 
                 // 方法
                 function chagneInfo() {
                     // 修改
                     name.value = '李四'
                     age.value = 48
                     console.log(name, age)
                     
                     job.type = 'UI设计师'
                     job.salary = '60K'
                     job.a.b.c = 999	// 深层嵌套
                     job.hobby[0] = '学习'
                 }
                 
                 // 返回一个对象（常用）
                 return {
                     name,
                     age,
                     changeInfo
                 }
             }
         }
     </script>
     ```

   - 内部基于ES6的Proxy实现，通过代理对象操作源对象内部数据都是响应式的。

### 4.Vue3.0中的响应式原理

#### 4.1 Vue2.x的响应式

1. 实现原理：

   - 对象类型：通过`Object.defineProperty()`**对对象的已有属性值的读取、修改进行拦截**（**数据劫持**）

   - 数组类型：通过**重写更新数组的一系列方法**来实现拦截

     ```js
     let person = {
         name: '张三',
         age: 18
     }
     
     // 模拟vue2中实现响应式
     let p = {}
     Object.defineProperty(p, 'name', {
     	get() {
             // 有人读取name时调用
             return person.name
         },
     	set() {
             // 有人修改name时调用
             person.name = value
         }
     })
     
     // 当直接新增、删除属性时，无法监听到
     ```

2. 存在问题：

   - 直接**新增、删除属性**，界面不会更新
   - 直接通过**下标修改数组**，界面不会自动更新

3. 解决方法：

   - 在实例内部可以使用`$set`和`$delete`

     ```js
     this.$set(this.age, 'age', 18)
     this.$delete(this.age, 'age')
     ```

   - 调用Vue的`set`和`delete`

     ```js
     import Vue from 'vue'
     
     Vue.set(vm.age, 'age', 18)
     Vue.delete(vm.age, 'age')
     ```

#### 4.2 Vue3.x的响应式

1. 实现原理：

   - 通过**Proxy（代理）**：**拦截对象中任意属性的变化**，包括，属性值的读写、属性的添加、属性的删除等

   - 通过**Reflect（反射）**：对被代理对象的属性**进行操作**

   - MDN文档中描述的Proxy与Reflect：

     - Proxy：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy
     - Reflect：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect

     ```js
     let person = {
         name: '张三',
         age: 18
     }
     
     // 模拟Vue3中的响应式
     // 拦截
     const p = new Proxy(person, {
         // 获取
     	get(target, propName) {
     		console.log(target, propName)
     		// return target[propName]	// propName是字符串
             return Reflect.get(target, propName)
     	},
         // 新增/修改
     	set(target, propName, value) {
     		console.log(target, propName, value)
             // target[propName] = value
             Reflect.set(target, propName, value)
     	},
         // 删除
         deleteProperty(target, propName) {
         	console.log(target, propName)
             // return delete target[propName]
             return Reflect.deleteProperty(target, propName)
     	},
     })
     
     p.name = '李四'
     ```

### 5.reactive对比ref

1. 定义角度
   - `ref`用来定义**基本类型数据**，ref也可以用来定义对象或数组类型数据，但它内部会自动通过`reactive`转为代理对象；
   - `reactive`用来定义**对象（或数组）类型数据**；
2. 原理角度
   - ref通过`Object.defineProperty()`的`get`和`set`来实现响应式（**数据劫持**）
   - reactive通过使用`Proxy`来实现响应式，并通过`Reflect`操作源对象内部的数据
3. 使用角度
   - ref定义的数据：操作数据需要`.value`，读取数据时模板中直接读取不需要`.value`
   - reactive定义的数据：操作数据与读取数据：均不需要`.value`

### 6.setup的两个注意点

1. setup执行的时机
   - 在`beforceCreate`之前执行一次，this是`undefined`
2. setup的参数
   - props：值为对象，包含组件外部传递过来、且**组件内部声明接收了的属性**
   - context：上下文对象
     - attrs：值为对象，包含组件外部传递过来，但**没有在props配置中声明的属性**，相当于`this.$attrs`
     - slots：收到的插槽内容，相当于`this.$slots`
     - **emit：分发自定义事件的函数，相当于`this.$emit`**

### 7.计算属性与监视

#### 7.1 computed函数

1. 与Vue2.x中的computed配置功能一致

2. 写法：

   ```html
   <template>
       <h1>信息</h1>
       姓：<input type="text" v-model="person.firstName">
       名：<input type="tex" v-model="person.lastName">
       全名：{{ fullName }}
   </template>
   ```

   **Vue2**

   ```js
   // vue2
   computed: {
   	fullName() {
   		return this.person.firstName + this.person.lastName
   	}
   }
   ```

   **Vue3 简单写法**

   ```js
   import { reactive } from '@vue/reactivity'
   import { computed } from '@vue/runtime-core'
   export default {
       name: 'Demo',
       setup() {
           // 数据
           let person = reactive({
               firstName: '张',
               lastName: '三',
           })
   
           // 简单写法
           person.fullName = computed(() => {
               return person.firstName + person.lastName
           })
   
           return {
               person,
           }
       },
   }
   ```

   **Vue3 完整写法**

   ```html
   <template>
       <h1>信息</h1>
       姓：<input type="text" v-model="person.firstName">
       名：<input type="tex" v-model="person.lastName">
       全名：{{ person.fullName }}
       <div style="margin-top:20px">
           修改全名：<input type="text" v-model="person.fullName">
       </div>
   </template>
   ```

   ```js
   import { reactive } from '@vue/reactivity'
   import { computed } from '@vue/runtime-core'
   export default {
       name: 'Demo',
       setup() {
           // 数据
           let person = reactive({
               firstName: '张',
               lastName: '三',
           })
   
           // 完整写法 考虑读写
           person.fullName = computed({
               get() {
                   return person.firstName + person.lastName
               },
               // 修改
               set(value) {
                   person.firstName = value.slice(0, 1)
                   person.lastName = value.slice(1, value.length)
               },
           })
           return {
               person,
           }
       },
   }
   ```

   ![image-20230207154320301](https://gitee.com/v876774538/my-img/raw/master/image-20230207154320301.png)

#### 7.2 watch函数

1. 与Vue2.x中watch的配置功能一致

2. 写法：

   **Vue2**

   ```js
   watch: {
   	// 简单
   	sum(newValue, oldValue) {
   		console.log('sum的值变化了', newValue, oldValue)
   	}
   	// 完整
   	sum: {
   		immediate: true,	// 立即
   		deep: true,	// 深度监听
   		handler(newValue, oldValue) {
   			console.log('sum的值变化了', newValue, oldValue)
   		}
   	}
   }
   ```

   **Vue3**

   - 情况1：监视`ref`所定义的响应式数据

     ```html
     <template>
         <h2>当前求和为：{{ sum }}</h2>
         <button @click="sum++">点我+1</button>
     </template>
     ```

     ```js
     setup() {
         // 数据
         let sum = ref(0)
     
         // 监听
         watch(sum, (newValue, oldValue) => {
             console.log('sum变化了', newValue, oldValue)
         }, {
             immediate: true
         })
     },
     ```

   - 情况2：监视多个`ref`定义的响应式数据

     ```js
     setup() {
         // 数据
         let sum = ref(0)
         let msg = ref('你好啊')
     
         // 监听
         // 1. 分多个watch写
         watch(sum, (newValue, oldValue) => {
             console.log('sum变化了', newValue, oldValue)
         })
         watch(msg, (newValue, oldValue) => {
             console.log('msg变化了', newValue, oldValue)
         })
         
         // 2. 组合成一个
         watch([sum, msg], (newValueArr, oldValueArr) => {
             console.log('sum或msg变化了', newValueArr, oldValueArr)
         })
     },
     ```

   - 情况3：监视reactive定义的响应式数据

     ```html
     <template>
         <h2>
             姓名：{{ person.name }}
         </h2>
         <h2>
             年龄：{{ person.age }}
         </h2>
         <h2>工作：{{ person.job.j1.post }}</h2>
         <div style="margin-top: 20px">
             修改姓名：<input type="text" v-model="person.name">
         </div>
         <div style="margin-top: 20px">
             <button @click="person.age++">
                 增长年龄
             </button>
         </div>
         <div style="margin-top: 20px;">
             修改工作：<input type="text" v-model="person.job.j1.post">
         </div>
     </template>
     ```

     ```js
     setup() {
         let person = reactive({
             name: '张三',
             age: 18,
             job: {
                 j1: {
                     salary: '10k',
                     post: '前端工程师',
                 },
             },
         })
     
         watch(person, (newValue, oldValue) => {
             console.log('person变化了', newValue, oldValue)
             // watch监视reactive定义的响应式数据，无法获得正确的oldValue！
             // watch监视reacitve定义的响应式数据，强制开启了深度监听，配置deep: false无效
         })
     
         return {
             person,
         }
     },
     ```

   - 情况4：监视reactive定义的响应式数据中的某个属性

     ```js
     setup() {
         let person = reactive({
             name: '张三',
             age: 18,
             job: {
                 j1: {
                     salary: '10k',
                     post: '前端工程师',
                 },
             },
         })
     
         watch(() => person.age, (newValue, oldValue) => {
             console.log('person.age变化了', newValue, oldValue)
         })
     
         return {
             person,
         }
     },
     ```

   - 情况5：监视reactive定义的响应式数据中的某些属性

     ```js
     setup() {
         let person = reactive({
             name: '张三',
             age: 18,
             job: {
                 j1: {
                     salary: '10k',
                     post: '前端工程师'
                 }
             }
         })
     
         watch([() => person.name, () => person.age], (newValue, oldValue) => {
             console.log('person.name或person.age变化了', newValue, oldValue)
         })
     
         return {
             person,
         }
     }
     ```

   - 特殊情况：监视reactive定义的响应式数据中的**某个属性**（嵌套对象），可开启deep

     ```js
     setup() {
         let person = reactive({
             name: '张三',
             age: 18,
             job: {
                 j1: {
                     salary: '10k',
                     post: '前端工程师'
                 }
             }
         })
     
         watch(() => person.job, (newValue, oldValue) => {
             console.log('person.job变化了', newValue, oldValue)
         }, { deep: true })
     
         return {
             person,
         }
     }
     ```

     ![image-20230207164610587](https://gitee.com/v876774538/my-img/raw/master/image-20230207164610587.png)

3. 注意：

   - 监视reactive定义的响应式数据时，`oldValue`**无法正常获取**，并且**强制开启了深度监听**（deep配置无效）
   - 监视reactive定义的响应式数据中**某个属性**时`deep`配置有效

#### 7.3 watchEffect函数

1. watch和watchEffect的区别

   - `watch`：既要**指明监视的属性，也要指明监视的回调**；
   - `watchEffect`：**不用指明监视哪个属性**，监视的**回调中用到哪个属性，那就监视哪个属性**

2. watchEffect有点像computed，区别如下

   - `computed`：注重的计算出来的值（回调函数的返回值），所以**必须要写返回值**；
   - `watchEffect`：更**注重过程**（回调函数的函数体），**可以不用写返回值**

3. 写法：

   ```js
   let sum = ref(0)
   let person = {
   	name: '张三',
   	age: 18
   }
   
   // watchEffect所指定的回调中用到的数据只要发生变化，就直接重新执行回调
   watchEffect(() => {
   	const x1 = sum.value
   	const x2 = person.age	// 某一个数据改变回调都会执行
   	console.log('watchEffect配置的回调执行了')
   })
   ```

### 8.生命周期

#### 8.1 vue2生命周期

![image-20230207172422730](https://gitee.com/v876774538/my-img/raw/master/image-20230207172422730.png)

#### 8.2 vue3生命周期

![组件生命周期图示](https://cn.vuejs.org/assets/lifecycle.16e4c08e.png)

生命周期钩子API索引：https://cn.vuejs.org/api/options-lifecycle.html

#### 8.3 注意

- > Vue3.0中可以**继续使用Vue2.x中的生命周期钩子**，但有有两个被更名：
  >
  > - ```beforeDestroy```改名为 ```beforeUnmount```
  > - ```destroyed```改名为 ```unmounted```

  ```js
  // 配置项形式使用生命周期钩子
  beforeCreate() {
  	...
  }
  ...
  ```

- Vue3.0也提供了 **Composition API 形式的生命周期钩子**，与Vue2.x中钩子对应关系如下：

  - `beforeCreate`===>`setup()`
  - `created`=======>`setup()`
  - `beforeMount` ===>`onBeforeMount`
  - `mounted`=======>`onMounted`
  - `beforeUpdate`===>`onBeforeUpdate`
  - `updated` =======>`onUpdated`
  - `beforeUnmount` ==>`onBeforeUnmount`
  - `unmounted` =====>`onUnmounted`

  ```js
  // 组合式API形式使用生命周期钩子
  setup() {
  	console.log('setUp')
      
      onBeforeMount(() => {
      	console.log('beforeMount')
      })
      
      onMounted(() => {
      	console.log('mounted')
      })
      
      onBeforeUpdate(() => {
      	console.log('beforeUpdate')
      })
      
      onUpdated(() => {
      	console.log('updated')
      })
      
      onBeforeUnmount(() => {
      	console.log('beforeUnmount')
      })
      
      onUnmounted(() => {
      	console.log('unmounted')
      })
  }
  ```

- 配置项形式使用生命周期钩子与组合式API形式同时存在的情况下，组合式API的执行时机更优先

### 9.自定义hook函数

#### 9.1 概念

> 本质是一个函数，**把setup函数中使用的Composition API进行封装**。

#### 9.2 使用场景

- 逻辑复用：当多个组件需要共享相同的逻辑时，我们可以将这些逻辑封装成一个Hook，然后在需要的组件中导入并使用，这样可以避免代码重复，提高代码的复用性；
- 逻辑拆分：对于复杂的组件，我们可以使用Hooks将组件的逻辑拆分成多个独立的函数，每个函数负责处理一部分的逻辑，这样可以使组件的代码更加清晰、易于维护；
- 副作用管理：Hooks中的函数可以访问组件的响应式数据，并且可以在组件的生命周期中执行副作用操作（如定时器、事件监听等）。通过使用Hooks，我们可以更好地管理这些副作用操作，确保它们在组件卸载时得到正确的清理。

#### 9.3 书写规范

> - 命名规范：自定义Hooks应该**以“use”为前缀**，以区分其他函数和变量。例如：`useUserInfo`、`useMousePosition`等。同时，命名应清晰明了，准确描述Hooks的功能。
> - 参数与返回值：自定义Hooks应该接收明确的参数，并返回需要在组件中使用的响应式数据、方法、计算属性等。返回的对象应该具有清晰的属性名和结构。
> - 副作用管理：如果自定义Hooks包含副作用操作（如定时器、事件监听等），应确保在组件卸载时正确清理这些副作用。可以使用`onMounted`、`onUnmounted`等生命周期钩子来管理副作用的添加和移除。
> - 文档注释：为自定义Hooks编写清晰的文档注释是非常重要的，说明其用途、参数、返回值和使用示例。这将有助于其他开发者理解和使用你的自定义Hooks。
> - 类型定义（如果使用TypeScript）：为自定义Hooks提供类型定义可以确保更好的类型安全性和编辑器支持。使用TypeScript的泛型功能可以增加Hooks的灵活性和可复用性。
> - 测试：为自定义Hooks编写单元测试是确保其正确性和稳定性的重要手段。测试应该覆盖各种使用场景和边界情况。

#### 9.4 注意

hook本质上就是函数，utils和vue自定义hooks的区别：

- utils：不涉及响应式的函数
- hooks：涉及Vue的一些响应式API，如`ref/reactive/computed/watch/onMounted`

类似于vue2中的mixin

#### 9.5 示例

**实现单击屏幕输出当前点击坐标**

- 普通实现

  ```vue
  <template>
  
  </template>
  
  <script>
  import { onBeforeUnmount, onMounted } from '@vue/runtime-core'
  import { reactive } from 'vue'
  export default {
      name: 'Demo2',
      setup() {
          let point = reactive({
              x: 0,
              y: 0,
          })
  
          function savePoint(event) {
              point.x = event.pageX
              point.y = event.pageY
              console.log(point.x, point.y)
          }
  
          // 挂载
          onMounted(() => {
              window.addEventListener('click', savePoint)
          })
  
          // 销毁之前
          onBeforeUnmount(() => {
              window.removeEventListener('click', savePoint)
          })
  
          return {
              point,
          }
      },
  }
  </script>
  
  <style>
  </style>
  ```

- hook实现

  **Demo2.vue**在组件中使用

  ```js
  <template>
  
  </template>
  
  <script>
  // 引入hook
  import usePoint from '../hooks/userPoint.js'
  export default {
      name: 'Demo2',
      setup() {
          const point = usePoint()
          return {
              point,
          }
      },
  }
  </script>
  
  <style>
  </style>
  ```

  **userPoint.js**

  ```js
  /*
   * @Description: 
   * @Version: 1.0
   * @Author: sjy
   * @Date: 2023-02-08 09:50:34
   * @LastEditors: sjy
   * @LastEditTime: 2023-02-08 09:58:41
   */
  import { reactive } from "vue"
  import { onBeforeUnmount, onMounted } from '@vue/runtime-core'
  
  export default function () {
      // 实现鼠标打点的数据
      let point = reactive({
          x: 0,
          y: 0,
      })
  
      // 方法
      function savePoint (event) {
          point.x = event.pageX
          point.y = event.pageY
          console.log(point.x, point.y)
      }
  
      // 钩子
      // 挂载
      onMounted(() => {
          window.addEventListener('click', savePoint)
      })
  
      // 销毁之前
      onBeforeUnmount(() => {
          window.removeEventListener('click', savePoint)
      })
  
      return point
  }
  
  ```

#### 9.6 常用第三方Hooks推荐

1. **Vueuse**：Vueuse是一个基于Vue3 Composition API的实用函数集合，包含了大量有用的自定义Hooks，如`useMouse`、`useKeyboardJs`、`useLocalStorage`等。它是Vue3生态中最受欢迎的第三方Hooks库之一。
2. **@vue/reactivity**：这是Vue官方提供的响应式库，虽然它不是一个Hooks库，但其中的函数和工具可以与Composition API结合使用，帮助我们创建自定义的Hooks来处理响应式数据和副作用。例如，我们可以使用`reactive`、`ref`、`computed`等函数来创建响应式数据和计算属性。

### 10.toRefs

1. 作用：创建一个`ref`对象，**其value值指向另一个对象中的某个属性**（**引用**）

   ![image-20230208102451250](https://gitee.com/v876774538/my-img/raw/master/image-20230208102451250.png)

   ![image-20230208102533622](https://gitee.com/v876774538/my-img/raw/master/image-20230208102533622.png)

2. 语法：`const name = toRef(person, 'name')`

3. 应用：将**响应式对象中的某个属性单独提供给外部使用**时

   ```vue
   <template>
       <h2>
           姓名：{{ name }}	// 不用再写person.name ...
       </h2>
       <h2>
           年龄：{{ age }}
       </h2>
       <h2>工作：{{ post }}</h2>
       <div style="margin-top: 20px">
           修改姓名：<input type="text" v-model="name">
       </div>
       <div style="margin-top: 20px">
           <button @click="age++">
               增长年龄
           </button>
       </div>
       <div style="margin-top: 20px;">
           修改工作：<input type="text" v-model="post">
       </div>
       <div style="margin-top: 20px">
           {{ person }}
       </div>
   </template>
   
   <script>
   import { reactive, toRef } from 'vue'
   export default {
       setup() {
           let person = reactive({
               name: '张三',
               age: 18,
               job: {
                   j1: {
                       salary: '10k',
                       post: '前端工程师',
                   },
               },
           })
           return {
               person,
               name: toRef(person, 'name'),
               age: toRef(person, 'age'),
               post: toRef(person.job.j1, 'post'),
           }
       },
   }
   </script>
   
   <style>
   </style>
   ```

   ![image-20230208103346221](https://gitee.com/v876774538/my-img/raw/master/image-20230208103346221.png)

4. 扩展：`toRefs`和`toRef`功能一致，但可以批量创建多个`ref`对象，语法`toRefs(person)`

   ```js
   return {
   	...toRefs[person]	// 解构
   }
   ```

## 五、其他Composition API

### 1.shallowReactive与shallowRef

1. `shallowReactive`：只处理对象**最外层属性**的响应式（**浅响应式**）
2. `shallowRef`：只处理基本数据类型的响应式，**不进行对象的响应式处理**（不借用reactive）
3. 应用：
   - 有一个对象数据，解构较深，但变化时只是外层属性变化 ==> `shallowReactive`
   - 有一个对象数据，后续功能不会修改该对象中的属性，而是生成新的对象进行替换 ==> `shallowRef`

### 2.readonly与shallowReadonly

1. `readonly`：让响应式数据变为只读的（深只读，数据无法修改）
2. `shallowRef`：让一个响应式数据变为只读的（浅只读）
3. 应用：
   - 不希望数据被修改时，尤其当接收别人传递的数据时

### 3.toRaw与markRaw

1. `toRaw`:
   - 作用：将一个由`reactive`生成的**响应式对象**转为**普通对象**
   - 应用：用于读取响应式对象对应的普通对象，对这个普通对象的所有操作，不会引起页面更新
2. `markRaw`：
   - 作用：标记一个对象，**使其永远不会再成为响应式对象**
   - 应用：
     - 有些值不应被设置为响应式的，如复杂的第三方类库等；
     - 当渲染具有不可变数据源的大列表时，跳过响应式转换可以提高性能

### 4.customRef

1. 作用：创建一个自定义的ref，并对其依赖项跟踪和更新触发进行显式控制

2. 实现防抖效果：

   ```vue
   <template>
   	<input type="text" v-model="keyword">
   	<h3>{{ keyword }}</h3>
   </template>
   
   <script>
   	import { ref, customRef } from 'vue'
   	export default {
   		name: 'Demo',
   		setup() {
   			// 自定义一个ref
   			function myRef(value, delay) {
   				let timer
   				// 通过customRef去实现自定义
   				return customRef((track, trigger) => {
   					return {
   						// 读取
   						get() {
   							track()	// 告诉Vue这个value值是需要被“追踪”的
   							return value
   						},
   						// 设置值
   						set() {
   							clearTimeout(timer)	// 清空计时器
   							timer = setTimeout(() => {
   								value = newValue
   								trigger()	// 告诉Vue更新界面
   							}, delay)
   						}
   					}
   				})
   			}
   			let keyword = myRef('hello', 500)	// 使用程序员自定义的ref
   			return {
   				keyword
   			}
   		}
   	}
   </script>
   ```


### 5.provide与inject

![image-20230223102742696](https://gitee.com/v876774538/my-img/raw/master/image-20230223102742696.png)

1. 作用：实现**祖孙（后代）间**通信

2. 套路：父组件有一个`provide`选项来**提供数据**，子组件有一个`inject`选项来开始**使用这些数据**

3. 写法：

   - 祖组件

     ```js
     setup() {
     	...
     	let car = reactive({ name: '奔驰', price: '40万'})
     	provide('car', car)	// 给自己的后代组件传递数据
     	...
     }
     ```

   - 后代组件

     ```js
     setup(props, context) {
     	....
     	const car = inject('car')
     	return { car }
     	...
     }
     ```

### 6.响应式数据的判断

- isRef：检查一个值是否为`ref`对象；
- isReactive：检查一个对象是否是由`reactive`创建的响应式代理；
- isReadonly：检查一个对象是否是由`readonly`创建的只读代理；
- isProxy：检查一个对象是否是由`reactive`或者`readonly`方法创建的代理。

```js
import { ref, reactive, readonly, isRef, isReactive, isReadonly, isProxy }
export default {
	setup() {
		let car = reactive({name: '奔驰', price: '40w' })
		let sum = ref(0)
		let car2 = readonly(car)
		
		console.log(isRef(sum))	// true
		console.log(isReactive(car))	// true
		console.log(isReadonly(car2))	// true
		console.log(isProxy(car))	// true
		
		return {...toRefs(car)}
	},
}
```

## 六、Composition API的优势

### 1.Options API存在的问题

使用传统OptionsAPI（配置式API）时，新增或修改一个需求，分别需要在`data`、`methods`、`computed`...里修改（不集中）。

<div style="width:600px;height:370px;overflow:hidden;float:left">
    <img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f84e4e2c02424d9a99862ade0a2e4114~tplv-k3u1fbpfcp-watermark.image" style="width:600px;float:left" />
</div>
<div style="width:300px;height:370px;overflow:hidden;">
    <img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e5ac7e20d1784887a826f6360768a368~tplv-k3u1fbpfcp-watermark.image" style="zoom:50%;width:560px;left" /> 
</div>

### 2.Composition API的优势

我们可以更加优雅地组织我们的代码、函数，让相关功能的代码能够更加有序地组织在一起。

<div style="width:500px;height:340px;overflow:hidden;float:left">
    <img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bc0be8211fc54b6c941c036791ba4efe~tplv-k3u1fbpfcp-watermark.image"style="height:360px"/>
</div>
<div style="width:430px;height:340px;overflow:hidden;">
    <img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6cc55165c0e34069a75fe36f8712eb80~tplv-k3u1fbpfcp-watermark.image"style="height:360px"/>
</div>

## 七、新的组件

### 1.Fragment

Fragment（**碎片化节点**）

在Vue2中，组件只能有一个根元素。当我们新建一个Vue页面时，通常会有多个不同的元素节点。我们会在最外层包裹一个`<div></div>`来使其成为这个页面的根节点，但这并不友好，有时候我们并不需要这个`<div></div>`元素。

vue3中新增了一个类似DOM的标签元素`<Fragment></Fragment>`。如果在vue页面中有多个元素节点，那么在编译时vue就会在这些元素节点上添加一个`<Fragment></Fragment>`标签，并且这个标签不会出现在DOM树中

- 在Vue2中，组件必须有一个根标签；
- 在Vue3中，**组件可以没有根标签，内部会将多个标签包裹在一个Fragment虚拟元素中**。
- 好处：减少标签层级，减小内存占用。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2775d41052494e11a532195eec67b656~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

### 2.Teleport

- `Teleport`是一种能够将我们的`组件html结构`移动到指定位置的技术。

  ```vue
  <!-- 移动到body位置 参考body进行定位 -->
  <teleport to="body">
  	<div v-if="isShow" class="mask">
          <div class="diaLog">
              <h3>
                  我是一个弹窗
              </h3>
              <button @click="isShow = false">
                  关闭
              </button>
          </div>
      </div>
  </teleport>
  
  <style lang="less" scoped>
      .mask {
          position: absolute;
          // 居中
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%)
          background-color: rgba(0, 0, 0, 0.5)
      }
  </style>
  ```

### 3.Suspense

1. **等待异步组件时渲染一些额外内容**，让应用有更好的用户体验。

2. 使用步骤：

   - 异步引入组件

     ```js
     // import Child from './components/Child'	// 静态引入
     import { defineAsyncComponent } from 'vue'
     const Child = defineAsyncComponent(() => import('./components/Child.vue'))	// 异步引入
     
     export default {
         conponents: {
             Child
         }
     }
     ```

   - 使用`Suspense`包裹组件，并配置好`default`、`fallback`

     ```vue
     <template>
     	<div class="app">
     		<h3>我是App组件</h3>
     		<Suspense>
     			// 放置真正想展示的内容
     			<template v-slot:default>
     				<Child/>
     			</template>
     			// 展示loading
     			<template v-slot:fallback>
     				<h3>加载中.....</h3>
     			</template>
     		</Suspense>
     	</div>
     </template>
     ```

## 八、其他

### 1.全局API的转义

- vue2.x有许多全局API和配置

  - 例如：注册全局组件、全局指令等

    ```js
    // 注册全局组件
    Vue.component('MyButton', {
    	data: () => ({
    		count: 0
    	}),
    	template: '<button @click="count++">Clicked {{ count }} times.</button>'
    })
    
    // 注册全局指令
    Vue.directive('focus', {
    	inserted: el => el.focus()
    })
    ```

    

- Vue3.0中对这些API做出了调整：

  - 将全局的API，即：```Vue.xxx```调整到应用实例（```app```）上

    | 2.x 全局 API（```Vue```） | 说明                   | 3.x 实例 API (`app`)                        |
    | ------------------------- | ---------------------- | ------------------------------------------- |
    | Vue.config.xxxx           | 配置                   | app.config.xxxx                             |
    | Vue.config.productionTip  | 生产提示               | <strong style="color:#DD5145">移除</strong> |
    | Vue.component             | 全局组件               | app.component                               |
    | Vue.directive             | 全局指令               | app.directive                               |
    | Vue.mixin                 | 全局混入               | app.mixin                                   |
    | Vue.use                   | 使用插件               | app.use                                     |
    | Vue.prototype             | 挂载到原型（全局变量） | app.config.globalProperties                 |

## 2.其他改变

- data选项应始终被声明为一个函数。

- 过渡类名的更改：

  - Vue2.x写法

    ```css
    .v-enter,
    .v-leave-to {
      opacity: 0;
    }
    .v-leave,
    .v-enter-to {
      opacity: 1;
    }
    ```

  - Vue3.x写法

    ```css
    .v-enter-from,
    .v-leave-to {
      opacity: 0;
    }
    
    .v-leave-from,
    .v-enter-to {
      opacity: 1;
    }
    ```

- 移除 `keyCode` 作为 v-on 的修饰符，同时也不再支持```config.keyCodes```

- 移除 `v-on.native`修饰符 

  - 父组件中绑定事件

    ```vue
    <my-component
      v-on:close="handleComponentEvent"
      v-on:click="handleNativeClickEvent"
    />
    ```

  - 子组件中**声明自定义事件**

    ```vue
    <script>
      export default {
        emits: ['close']
      }
    </script>
    ```

- 移除 `过滤器（filter） `

  > 过滤器虽然这看起来很方便，但它需要一个自定义语法，打破大括号内表达式是 “只是 JavaScript” 的假设，这不仅有学习成本，而且有实现成本！**建议用方法调用或计算属性去替换过滤器。**

- ......

