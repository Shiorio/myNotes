# `Vue3+TS`结合写法详解

## 写在前面

```vue
<script setup lang="ts"></script>
```

script加上`lang="ts"`才能在写ts代码。

## 1.`defineProps`

### 1.1 基本使用

> 父传子，子定义接收变量及变量类型。

```ts
// 基本写法
const props = defineProps({
	money: {
		type: Number,
		required: true
	},
	car: {
		type: String,
		require: false,
		default: '红旗'
	}
})

consoel.log(props.money)
console.log(props.car)
```

### 1.2 通过泛型参数来定义props的类型

```ts
//defineProps 声明组件属性
const props = defineProps<{
    money: number	// 父组件传递该值时必须提供一个数字类型的值
    car?: string	// 父组件可以传递一个字符串类型的值 也可以不传递（? 非必须）
}>
```

### 1.3 `withDefaults`给props设置默认值

```ts
import { withDefaults } from 'vue'
const defaultProp = withDefaults(defineProps<{
	money: number
	car?: string
}>(), {
	money: 10000,
	car: '红旗'
})
console.log(defaultProp)
```

### 1.4 `响应式语法糖`解构+`defineProps`简化写法

```ts
const { money, car = '红旗' } = defineProps<{ money: number car?: string }>()
```

**注意：**

该语法糖需要**显式地选择开启**，因为它还是一个实验性特性。

并且响应式语法糖即将移除，建议使用`withDefaults`过度。

```ts
// vite.config.ts
export default defineConfig({
	plugins:[
		vue({
			reactivityTransform: true
		})
	]
})
```

## 2.`defineEmits`

### 2.1 基本使用

```ts
const emit = defineEmits(['changeMoney', 'changeCar'])
```

### 2.2 泛型参数

```ts
const emit = defineEmits<{
	(e: 'changeMoney', money: number): void
	(e: 'changeCar', car: string): void
}>
```

## 3.`ref`

> `ref()`会隐式地依据数据推导类型。

### 3.1 简单类型

> 如果是简单类型，推荐使用`类型推导`。

```ts
const money = ref(10)	// 括号内为初始值
```

### 3.2 复杂类型

> 如果是复杂类型，推荐使用`指定泛型`。

```ts
type Todo = {
	id: number
	name: string
	done: boolen
}
const list = ref<Todo[]>([])

setTimeout(() => {
    list.value = [
        {
            id: 1, name: '吃饭', done: false
        },
        {
            id: 2, name: '睡觉', done: true
        }
    ]
}, 1000)
```

复杂数据一般是后台返回数据，默认值是空，无法进行类型推导。

## 4.`reactive`

`reactive()`也会隐式地依据数据推导类型。

`ref()`适用于基本数据类型及复杂对象，而`reactive()`主要用于复杂对象及嵌套数据解构。

### 4.1 默认值属性固定

> 默认值属性固定，推荐使用类型推导。

```ts
const book = reactive({ title: 'Vue3在线医疗' })	// 推导类型 { title: string }
```

### 4.2 根据默认值推导不出我们需要的类型

> 根据默认值推导不出我们需要的类型，推荐使用`接口`或者`类型别名`给变量指定类型。

```ts
type Book = {
	title: string
	year?: number
}
const book: Book = reative({
	title: 'Vue3 在线医疗'
})
book.year = 2022
```

**注意：**官方不推荐使用 `reactive()` 的泛型参数，因为底层和 `ref()` 实现不一样。

## 5.`computed`

### 5.1 基本使用

```ts
import { ref, computed } from 'vue'
const count = ref(100)
const doubleCount = computed(() => count.value * 2)	// computed()会从其计算函数的返回值上推导出类型
```

### 5.2 泛型参数显式指定类型

```ts
const doubleMoney = computed<string>(() => (count.value * 2).toFixed(2))
// 若返回值不是string类型会报错
```

## 6.事件处理

### 6.1 不加类型

> 不加类型，`event`默认是`any`类型，类型不安全。

```vue
<script setup lang="ts">
    // 参数event隐式具有any类型
    const handleChange = (event) => {
        console.log(event.target.value)
    }
</script>

<template>
	<input type="text" @change="handleChange" />
</template>
```

### 6.2 添加类型

```ts
const handleChange = (event: Event) => {
    console.log((event.target as HTMLInputElement).value)
}
```

## 7.`Template Ref`

> 模板`ref`需要通过一个显式指定的泛型参数，建议默认值`null`

```vue
<script setup lang="ts">
	import { ref, onMounted } from 'vue'
    const el = ref<HTMLInputElement | null>(null)
    
    onMounted(() => {
        el.value?.focus()
    })
</script>

<template>
	<input ref="el"/>
</template>
```

**注意：**

1. 为了严格的类型安全，有必要在访问`el.value`时使用可选链或类型守卫；
2. 这是因为直到组件被挂载前，这个ref的值都是初始的`null`，并且由于`v-if`的行为将引用的元素卸载时也可以被设置为`null`

## 8.非空断言

处理类型可能是`null`或`undefined`的值，下面的属性或函数的访问赋值：

### 8.1 可选链

```vue
<script setup lang="ts">
	import { onMounted, ref } from 'vue'
    
    const input = ref< HTMLInputElement | null >(null)
    onMounted(() => {
        console.log(input.value?.value)	// if(input.value) { console.log(input.value.value) }
    })
</script>

<template>
	<div>
        App组件
    </div>
	<input type="text" ref="input" value="abc"/>
</template>
```

### 8.2 逻辑判断

```ts
if (input.value) {
	console.log(input.value.value)
	input.value.value = '123'
}
```

## 9.类型声明文件

### 9.1 基本介绍

项目中安装的第三方库中都是打包后的`js`代码，但我们使用的时候却有对应的`ts`类型提示，这是因为在第三方库中的`js`代码都有对应的`ts`类型声明文件。

> 通俗来讲，在`TypeScript`中义`.d.ts`为后缀的文件，我们称之为`TypeScript`类型声明文件，它的主要作用是描述`JavaScript`模块内所有导出成员的类型信息。

- `.ts`文件
  1. 既**包含类型信息**又**可执行代码**
  2. 可以被编译为`.js`文件然后执行代码
  3. 用途：编写程序代码的地方
- `.d.ts`文件
  1. 只包含类型信息的类型声明文件
  2. 不会生成`.js`文件，仅用于**提供类型信息**，在`.d.ts`文件中不允许出现可执行的代码，只用于提供类型
  3. 用途：为`js`提供类型信息

```ts
// src/types/env.d.ts

/** 声明 vite 环境变量的类型（如果未声明则默认是 any） */
interface ImportMetaEnv {
  readonly VITE_APP_TITLE: string
  readonly VITE_BASE_API: string
  readonly VITE_ROUTER_HISTORY: "hash" | "html5"
  readonly VITE_PUBLIC_PATH: string
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}
```

```
// src/.env.development

# 开发环境自定义的环境变量（命名必须以 VITE_ 开头）

## 后端接口公共路径（如果解决跨域问题采用反向代理就只需写公共路径）
VITE_BASE_API = '/api/v1'

## 路由模式 hash 或 html5
VITE_ROUTER_HISTORY = 'hash'

## 开发环境地址前缀（一般 '/'，'./' 都可以）
VITE_PUBLIC_PATH = '/'
```

### 9.2 内置类型声明文件

在使用数组时，数组所有方法都会有相应的代码提示以及类型信息：

```ts
const strs = ['a', 'b', 'c']
// 鼠标放在forEach上查看类型
strs.forEach
```

TypeScript给JS运行时可用的所有标准化内置 API 都提供了声明文件，这个声明文件就是**内置类型声明文件**。

> 可以通过`Ctrl+鼠标左键`来查看内置类型声明文件内容。查看`forEach`的类型声明，在`VSCode`中会自动跳转到 `lib.es5.d.ts`类型声明文件中。像window、document等`BOM`、`DOM`API 也都有相应的类型声明文件`lib.dom.d.ts`。

### 9.3 第三方库类型声明文件

1. 库本身自带类型声明文件

   - 比如`axios`安装后可查看`node_modules/axios`可发现对应的类型声明文件；
   - 导入`axios`后会加载对应的类型文件，提供该库的类型声明。

2. 由`DefinitelyTyped`提供

   - 比如`jquery`安装后导入，提示：需要安装`@types/jquery`类型声明包；

   - `DefinitelyTyped`是一个`github`仓库，用来提供高质量`TypeScript`类型声明；

   - 当安装`@types/*`类型声明包后，`ts`也会自动加载该类声明包，以提供该库的类型声明

     [TypeScript: Search for typed packages (typescriptlang.org)](https://www.typescriptlang.org/dt/search/)

     可以搜索是否有对应的 `@types/*`

### 9.4 自定义类型声明文件

1. 共享类型（重要）

   如果多个`.ts`文件中都用到同一个类型，此时可以创建`.d.ts`文件提供该类型，实现类型共享。

   具体操作步骤：

   - 创建`index.d.ts`类型声明文件
   - 创建需要共享的类型，并使用`export`导出
   - 在需要使用共享类型的`.ts`文件中，通过`import`导入

   ```ts
   // data.d.ts
   // 频道对象
   export type ChannelItem = {
       id: number;
       name: string;
   }
   
   // 频道接口响应数据
   export type ChannelData = {
       data: {
           channels: ChannelItem[]
       };
       message: string;
   }
   ```

   ```ts
   // APP.vue
   import { ref, onMounted } from 'vue'
   import axios from 'axios'
   import { ChannelItem, ChannelData } from '../data'
   
   const channels = ref<ChannelItem[]>([])
   
   onMounted(() => {
       axios.request<ChannelData>({
           url: 'http://geek.itheima.net/v1_0/channels'
       }).then((res) => {
           channels.value = res.data.data.channels
       })
   })
   ```

2. 给`js`文件提供类型

   在导入`.js`文件时，`ts`会自动加载与`.js`同名的`.d.ts`文件，以提供类型声明。

   `declare`关键字：

   用于类型声明，为其他地方（比如`.js`文件）中已存在的变量声明类型，而不是创建一个新的变量。

   - 对于`type` `interface`等明确就是`ts`类型的（只能在`ts`中使用的），可以省略`declare`关键字；
   - 其他`js`变量，应该使用`declare`关键字明确指定此处用于类型声明。

   ```ts
   // add/index.js
   const add = (a, b) => {
       return a + b
   }
   
   const point = (p) => {
       console.log('坐标', p.x, p.y)
   }
   
   export { add, point }
   ```

   ```ts
   // add/index.d.ts
   declare const add: (a: number, b: number) => number
   
   type position = {
       x: number;
       y: number;
   }
   declare const point: (p: Position) => void
   
   export { add, point }
   ```

   ```ts
   // main.ts
   import { add, point } from './add'
   
   add(3, 10)
   point({x: 100, y: 200})
   ```

   