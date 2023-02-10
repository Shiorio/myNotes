# uni-app的基本使用

## 一、uni-app介绍

> uni-app是一个使用vue.js开发**所有前端应用**的框架。开发者编写一套代码，就可以发布到IOS、Android、H5、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉）等多个平台。

## 二、环境搭建

### 1.HbuilderX

HBuilderX是前端通用开发工具，但为uni-app做了特别强化。

### 2.微信开发者工具

https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html

## 三、利用HbuilderX初始化项目

## 四、目录结构

### 1.目录结构

一个uni-app工程，默认包含如下目录及文件：

```
┌─uniCloud              云空间目录，阿里云为uniCloud-aliyun,腾讯云为uniCloud-tcb（详见uniCloud）
│─components            符合vue组件规范的uni-app组件目录
│  └─comp-a.vue         可复用的a组件
├─hybrid                App端存放本地html文件的目录
├─platforms             存放各平台专用页面的目录
├─pages                 业务页面文件存放的目录
│  ├─index
│  │  └─index.vue       index页面
│  └─list
│     └─list.vue        list页面
├─static                存放应用引用的本地静态资源（如图片、视频等）的目录，注意：静态资源只能存放于此
├─uni_modules           存放[uni_module](/uni_modules)规范的插件。
├─wxcomponents          存放小程序组件的目录
├─main.js               Vue初始化入口文件
├─App.vue               应用配置，用来配置App全局样式以及监听 应用生命周期
├─manifest.json         配置应用名称、appid、logo、版本等打包信息
├─pages.json            用来对uni-app进行全局配置，配置页面路由、导航条、选项卡等页面类信息
└─uni.scss              这里是uni-app内置的常用样式变量 
```

unpackage 打包目录，在这里有各个平台的打包文件。

- 编译到任意平台时，`static` 目录下的文件均会被完整打包进去，且不会编译。非 `static` 目录下的文件（vue、js、css 等）只有被引用到才会被打包编译进去。
- `static` 目录下的 `js` 文件不会被编译，如果里面有 `es6` 的代码，不经过转换直接运行，在手机设备上会报错。
- `css`、`less/scss` 等资源不要放在 `static` 目录下，建议这些公用的资源放在自建的 `common` 目录下。
- HbuilderX 1.9.0+ 支持在根目录创建 `ext.json`、`sitemap.json` 等小程序需要的文件。

### 2.开发规范

1. 页面文件遵循Vue单文件组件（SFC）规范；
2. 组件标签靠近小程序规范；
3. 接口能力（JS API）靠近微信小程序规范，但需将前缀`wx`替换为`uni`；
4. 数据绑定及事件处理同Vue.js规范，同时补充了App及页面的生命周期；
5. 为兼容多端运行，建议使用flex布局进行开发。

## 五、全局配置和页面配置

> `pages.json` 文件用来对 uni-app 进行全局配置，决定页面文件的路径、窗口样式、原生的导航栏、底部的原生tabbar 等。
>
> 它类似微信小程序中`app.json`的**页面管理**部分。注意定位权限申请等原属于`app.json`的内容，在uni-app中是在manifest中配置。

| 属性                                                         | 类型         | 必填 | 描述                    | 平台兼容   |
| :----------------------------------------------------------- | :----------- | :--- | :---------------------- | :--------- |
| [globalStyle](https://uniapp.dcloud.io/collocation/pages#globalstyle) | Object       | 否   | 设置默认页面的窗口表现  |            |
| [pages](https://uniapp.dcloud.io/collocation/pages#pages)    | Object Array | 是   | 设置页面路径及窗口表现  |            |
| [easycom](https://uniapp.dcloud.io/collocation/pages#easycom) | Object       | 否   | 组件自动引入规则        | 2.5.5+     |
| [tabBar](https://uniapp.dcloud.io/collocation/pages#tabbar)  | Object       | 否   | 设置底部 tab 的表现     |            |
| [condition](https://uniapp.dcloud.io/collocation/pages#condition) | Object       | 否   | 启动模式配置            |            |
| [subPackages](https://uniapp.dcloud.io/collocation/pages#subPackages) | Object Array | 否   | 分包加载配置            |            |
| [preloadRule](https://uniapp.dcloud.io/collocation/pages#preloadrule) | Object       | 否   | 分包预下载规则          | 微信小程序 |
| [workers(opens new window)](https://developers.weixin.qq.com/miniprogram/dev/framework/workers.html) | String       | 否   | `Worker` 代码放置的目录 | 微信小程序 |
| [leftWindow](https://uniapp.dcloud.io/collocation/pages#leftwindow) | Object       | 否   | 大屏左侧窗口            | H5         |
| [topWindow](https://uniapp.dcloud.io/collocation/pages#topwindow) | Object       | 否   | 大屏顶部窗口            | H5         |
| [rightWindow](https://uniapp.dcloud.io/collocation/pages#rightwindow) | Object       | 否   | 大屏右侧窗口            | H5         |

### 1.通过globalStyle进行全局配置

在pages.json中，通过globalStyle进行全局配置。

用于设置应用的状态栏、导航条、标题、窗口背景色等。

| 属性                         | 类型     | 默认值  | 描述                                                   |
| ---------------------------- | -------- | ------- | ------------------------------------------------------ |
| navigationBarBackgroundColor | HexColor | #f7f7f7 | 导航栏背景颜色（同状态栏背景色）                       |
| navigationBarTextStyle       | String   | white   | 导航栏标题颜色及状态栏前景颜色，**仅支持black/white**  |
| navigationBarTitleText       | String   |         | 导航栏标题文字内容                                     |
| backgroundColor              | HexColor | #ffffff | 窗口的背景色                                           |
| backgroundTextStyle          | String   | dark    | 下拉loading样式，仅支持**dark/light**                  |
| enablePullDownRefresh        | Boolean  | false   | 是否开启下拉刷新，详见页面生命周期                     |
| onReachBottomDistance        | Number   | 50      | 页面上拉触底事件触发时距页面底部距离，**单位只支持px** |

```json
"globalStyle": {
    "navigationBarTextStyle": "black",
    "navigationBarTitleText": "uni-app",
    "navigationBarBackgroundColor": "#F8F8F8",
    "backgroundColor": "#F8F8F8"
}
```

### 2.创建新的message页面

右键pages新建message目录，在message目录下右键新建.vue文件，并选择基本模板。

```vue
<template>
	<view>
		...
	</view>
</template>

<script>
</script>

<style>
</style>
```

### 3.通过pages来配置页面

在pages.json中，通过pages进行页面配置。

| 属性  | 类型   | 描述                                                         |
| ----- | ------ | ------------------------------------------------------------ |
| path  | String | 配置页面路径                                                 |
| style | Object | 配置页面窗口表现，[详见](https://uniapp.dcloud.io/collocation/pages.html#style) |

```json
"pages":[
	{
		//pages数组中第一项表示应用启动页，参考：https://uniapp.dcloud.io/collocation/pages
		"path": "pages/message/index",
		"style": {
			"navigationBarBackgroundColor": "#007AFF",
			"navigationBarTextStyle": "white",
			"enablePullDownRefresh": true,
			"disableScroll": true,
            // 设置编译到H5平台的特定样式
			"h5": {
                // 下拉刷新
				"pullToRefresh": {
					"color": "#007AFF"
				}
			}
		}
	},{
        "path": "pages/index/index",
        "style": {
            "navigationBarBackgroundColor": "007AFF",
            "navigationBarTextStyle": "white",
        }
    }
]
```

注意：

- pages节点的第一项为应用入口页（首页）；
- **应用中新增/减少页面，都需要对pages数组进行修改**；
- 文件名**不需要写后缀**，框架会自动寻找路径下的页面资源。

### 4.配置tabBar

如果应用是一个多tab应用，可以通过tabBar配置项指定tab栏表现，以及tab切换时显示的对应页。

在pages.json中，通过tabBar进行tab栏配置。

| 属性            | 类型     | 必填 | 默认值 | 描述                                       | 平台差异说明             |
| --------------- | -------- | ---- | ------ | ------------------------------------------ | ------------------------ |
| color           | HexColor | 是   |        | tab上的文字默认颜色                        |                          |
| selectedColor   | HexColor | 是   |        | tab上的文字选中时的颜色                    |                          |
| backgroundColor | HexColor | 是   |        | tab的背景色                                |                          |
| borderStyle     | String   | 否   | black  | tabBar上边框的颜色，仅支持black/white      | App 2.3.4+支持其他颜色值 |
| list            | Array    | 是   |        | tab的列表                                  |                          |
| position        | String   | 否   | bottom | 可选值**bottom/top**，tabBar在页面中的位置 | top值仅微信小程序支持    |

其中list接收一个数组，数组中的每个项都是一个对象，其属性值如下：

| 属性             | 类型   | 必填 | 说明                                                         |
| ---------------- | ------ | ---- | ------------------------------------------------------------ |
| pagePath         | String | 是   | 页面路径，必须在pages中先定义                                |
| text             | String | 是   | tab上按钮的文字，在5+App和H5平台为非必填，例如中间可放一个没有文字的+号图标 |
| iconPath         | String | 否   | 图片路径。icon大小限制为40kb，建议尺寸为81px*81px。当position为top时，此参数有无效，且不支持网络图片、不支持字体图标 |
| selectedIconPath | String | 否   | 选中时的图片路径。                                           |

```json
"tabBar": {
	"list": [
		{
			"text": "首页",
			"pagePath": "pages/index/index",
			"iconPath": "static/tabs/home.png",
			"selectedIconPath": "static/tabs/home-active.png"
		}, {
			"text": "信息".
			"pagePath": "pages/message/index",
			"iconPath": "static/tabs/message.png",
			"selectedIconPath": "static/tabs/message-active.png"
		}
	]
}
```

注意：

- 当设置position为top时，将不会显示icon；
- tabBar中的list是一个数组，只能配置最少2个、最多5个tab。tab按照数组的顺序排序。

### 5.condition启动模式配置

启动模式配置，仅开发期间生效，用于**模拟直达页面的场景**。如：小程序转发后，用户点击所打开的页面。

| 属性    | 类型   | 是否必填 | 描述                             |
| ------- | ------ | -------- | -------------------------------- |
| current | Number | 是       | 当前激活的模式，list节点的索引值 |
| list    | Array  | 是       | 启动模式列表                     |

list说明：

| 属性  | 类型   | 是否必填 | 描述                                   |
| ----- | ------ | -------- | -------------------------------------- |
| name  | String | 是       | 启动模式名称                           |
| path  | String | 是       | 启动页面路径                           |
| query | String | 否       | 启动参数，可在页面的`onLoad`函数里获得 |

```json
"condition": {
	"current": 0,
	"list": [
		{
			"name": "详情页",
			"path": "pages/detail/detail",
			"query": "id=80"
		}
	]
}
```



## 六、uni-app组件的基本使用

> uni-app为开发者提供了丰富的基础组件，开发者可以像搭积木一样，组合各种组件拼接成自己的应用。
>
> uni-app的组件，就像HTML中的div、p、span等标签的作用一样，**用于搭建页面的基础结构**。

组件使用的官方文档：https://uniapp.dcloud.io/component/

```vue
<template>
	<view>
		<button size="mini">按钮</button>
	</view>
</template>
```

注意：按照[vue单文件组件规范 (opens new window)](https://cn.vuejs.org/v2/guide/single-file-components.html)，每个vue文件的根节点必须为 `<template>`，且这个 `<template>` 下只能且必须有一个根 `<view>` 组件。

### 1.视图容器-view

#### 1.1 组件属性

| 属性名                     | 类型    | 默认值 | 说明                                                         |
| :------------------------- | :------ | :----- | :----------------------------------------------------------- |
| hover-class                | String  | none   | 指定按下去的样式类。当 `hover-class="none"` 时，没有点击态效果 |
| **hover-stop-propagation** | Boolean | false  | 指定是否阻止本节点的祖先节点出现点击态（**阻止冒泡**），App、H5、支付宝小程序、百度小程序不支持（支付宝小程序、百度小程序文档中都有此属性，实测未支持） |
| hover-start-time           | Number  | 50     | 按住后**多久出现**点击态，单位毫秒                           |
| hover-stay-time            | Number  | 400    | 手指松开后点击态**保留时间**，单位毫秒                       |

- 视图容器；
- 它类似于传统html中的div，用于包裹各种元素内容。

#### 1.2 代码案例

```vue
<template>
	<view class="box2" hover-class="box2_active">
		<view 
			class="box1" 
			hover-class="box1_active"
			hover-stop-propagation 
			:hover-start-time="2000" 
			:hover-stay-time="2000" >
		</vidw>
	</view>
</template>

<style>
	.box1 {
		width: 200px;
		height: 200px;
	}
	.box1_active {
		background-color: red;	
	}
	.box2 {
		width: 100px;
		height: 100px;
	}
	.box2_active {
		background-color: blue;
	}
</style>
```



### 2.基础内容-text

#### 2.1 组件属性

| 属性名      | 类型    | 默认值 | 说明                                                         | 平台差异说明        |
| :---------- | :------ | :----- | :----------------------------------------------------------- | :------------------ |
| selectable  | Boolean | false  | 文本是否可选                                                 | App、H5、快手小程序 |
| user-select | Boolean | false  | 文本是否可选                                                 | 微信小程序          |
| space       | String  |        | 显示连续空格，可选值：ensp（中文字符空格一半大小）、emsp（中文字符空格大小）、nbsp（根据字体设置的空格大小） | App、H5、微信小程序 |
| decode      | Boolean | false  | 是否解码                                                     | App、H5、微信小程序 |

- **text组件**相当于**行内标签**，在同一行显示；
- 除了文本节点以外的其他节点都无法长按选中。

#### 2.2 代码案例

```vue
<template>
	<text selectable>长按可选</text>
	<text space="ensp">显示连续空格     中文字符空格一半大小</text>
</template>
```

### 3.表单组件-button

按钮。

#### 3.1 组件属性

| 属性名                 | 类型    | 默认值       | 说明                                                         | 生效时机                   | 平台差异说明                                             |
| :--------------------- | :------ | :----------- | :----------------------------------------------------------- | :------------------------- | :------------------------------------------------------- |
| size                   | String  | default      | 按钮的大小，可选值：default（默认）、mini（小尺寸）          |                            |                                                          |
| type                   | String  | default      | 按钮的样式类型，可选值：primary（微信小程序、360小程序为绿色，App、H5、百度小程序、支付宝小程序、飞书小程序、快应用为蓝色，字节跳动小程序为红色，QQ小程序为浅蓝色。如想在多端统一颜色，请改用default，然后自行写样式）、default（白色）、warn（红色） |                            |                                                          |
| plain                  | Boolean | false        | 按钮是否镂空，背景色透明                                     |                            |                                                          |
| **disabled**           | Boolean | false        | **是否禁用**                                                 |                            |                                                          |
| loading                | Boolean | false        | 名称前是否带 loading 图标                                    |                            | H5、App(App-nvue 平台，在 ios 上为雪花，Android上为圆圈) |
| form-type              | String  |              | 用于 `<form>` 组件，点击分别会触发 `<form>` 组件的 **submit**/**reset** 事件 |                            |                                                          |
| open-type              | String  |              | 开放能力                                                     |                            |                                                          |
| hover-class            | String  | button-hover | 指定按钮按下去的样式类。当 hover-class="none" 时，没有点击态效果 |                            | App-nvue 平台暂不支持                                    |
| hover-start-time       | Number  | 20           | 按住后多久出现点击态，单位毫秒                               |                            |                                                          |
| hover-stay-time        | Number  | 70           | 手指松开后点击态保留时间，单位毫秒                           |                            |                                                          |
| app-parameter          | String  |              | 打开 APP 时，向 APP 传递的参数，open-type=launchApp时有效    |                            | 微信小程序、QQ小程序                                     |
| hover-stop-propagation | boolean | false        | 指定是否阻止本节点的祖先节点出现点击态                       |                            | 微信小程序                                               |
| lang                   | string  | 'en'         | 指定返回用户信息的语言，zh_CN 简体中文，zh_TW 繁体中文，en 英文。 |                            | 微信小程序                                               |
| session-from           | string  |              | 会话来源，open-type="contact"时有效                          |                            | 微信小程序                                               |
| send-message-title     | string  | 当前标题     | 会话内消息卡片标题，open-type="contact"时有效                |                            | 微信小程序                                               |
| send-message-path      | string  | 当前分享路径 | 会话内消息卡片点击跳转小程序路径，open-type="contact"时有效  |                            | 微信小程序                                               |
| send-message-img       | string  | 截图         | 会话内消息卡片图片，open-type="contact"时有效                |                            | 微信小程序                                               |
| show-message-card      | boolean | false        | 是否显示会话内消息卡片，设置此参数为 true，用户进入客服会话会在右下角显示"可能要发送的小程序"提示，用户点击后可以快速发送小程序消息，open-type="contact"时有效 |                            | 微信小程序                                               |
| @getphonenumber        | Handler |              | 获取用户手机号回调                                           | open-type="getPhoneNumber" | 微信小程序                                               |
| @getuserinfo           | Handler |              | 用户点击该按钮时，会返回获取到的用户信息，从返回参数的detail中获取到的值同uni.getUserInfo | open-type="getUserInfo"    | 微信小程序                                               |
| @error                 | Handler |              | 当使用开放能力时，发生错误的回调                             | open-type="launchApp"      | 微信小程序                                               |
| @opensetting           | Handler |              | 在打开授权设置页并关闭后回调                                 | open-type="openSetting"    | 微信小程序                                               |
| @launchapp             | Handler |              | 从小程序打开 App 成功的回调                                  | open-type="launchApp"      | 微信小程序                                               |

**open-type有效值说明**

| 值               | 说明                                                         | 平台差异说明                                                 |
| :--------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| feedback         | 打开“意见反馈”页面，用户可提交反馈内容并上传日志             | App、微信小程序、QQ小程序                                    |
| share            | 触发用户转发                                                 | 微信小程序、百度小程序、支付宝小程序、字节跳动小程序、飞书小程序、QQ小程序、快手小程序 |
| getUserInfo      | 获取用户信息，可以从@getuserinfo回调中获取到用户信息         | 微信小程序、百度小程序、QQ小程序、快手小程序                 |
| contact          | 打开客服会话，如果用户在会话中点击消息卡片后返回应用，可以从 @contact 回调中获得具体信息 | 微信小程序、百度小程序                                       |
| getPhoneNumber   | 获取用户手机号，可以从@getphonenumber回调中获取到用户信息    | 微信小程序、百度小程序、字节跳动小程序、支付宝小程序、快手小程序。App平台另见[一键登陆(opens new window)](https://uniapp.dcloud.net.cn/univerify) |
| launchApp        | 小程序中打开APP，可以通过app-parameter属性设定向APP传的参数  | [微信小程序 (opens new window)](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/launchApp.html)、[QQ小程序(opens new window)](https://q.qq.com/wiki/develop/miniprogram/frame/open_ability/open_app.html) |
| openSetting      | 打开授权设置页                                               | 微信小程序、百度小程序                                       |
| getAuthorize     | 支持小程序授权                                               | 支付宝小程序                                                 |
| contactShare     | 分享到通讯录好友                                             | 支付宝小程序                                                 |
| lifestyle        | 关注生活号                                                   | 支付宝小程序                                                 |
| openGroupProfile | 呼起QQ群资料卡页面，可以通过group-id属性设定需要打开的群资料卡的群号，同时manifest中必须配置groupIdList | QQ小程序基础库1.4.7版本+                                     |

#### 3.2 点击事件

button 组件的点击遵循 vue 标准的 @click事件。

button 组件没有 url 属性，如果要跳转页面，可以在@click中编写，也可以在button组件外面套一层 navigator 组件。举例，如需跳转到about页面，可按如下几种代码写法执行：

```vue
<template>
	<view>
		<navigator url="/pages/about/about">
            <button type="default">通过navigator组件跳转到about页面</button>
    	</navigator>
		<button type="default" @click="goto('/pages/about/about')">
            通过方法跳转到about页面
    	</button>
		<button type="default" @click="navigateTo('/pages/about/about')">
            跳转到about页面
    	</button><!-- 这种写法只有h5平台支持，不跨端，不推荐使用 -->
	</view>
</template>
<script>
	export default {
		methods: {
			goto(url) {
				uni.navigateTo({
					url:url
				})
			}
		}
	}
</script>
```

### 4.媒体组件-image

图片。 

#### 4.1 组件属性

| 属性名                 | 类型        | 默认值        | 说明                                                         | 平台差异说明                                       |
| :--------------------- | :---------- | :------------ | :----------------------------------------------------------- | :------------------------------------------------- |
| src                    | String      |               | 图片资源地址                                                 |                                                    |
| **mode**               | String      | 'scaleToFill' | 图片裁剪、缩放的模式                                         |                                                    |
| lazy-load              | Boolean     | false         | 图片懒加载。只针对page与scroll-view下的image有效             | 微信小程序、百度小程序、字节跳动小程序、飞书小程序 |
| fade-show              | Boolean     | true          | 图片显示动画效果                                             | 仅App-nvue 2.3.4+ Android有效                      |
| webp                   | boolean     | false         | 默认不解析 webP 格式，只支持网络资源                         | 微信小程序2.9.0                                    |
| show-menu-by-longpress | boolean     | false         | 开启长按图片显示识别小程序码菜单                             | 微信小程序2.7.0                                    |
| draggable              | boolean     | true          | 是否能拖动图片                                               | H5 3.1.1+、App（iOS15+）                           |
| @error                 | HandleEvent |               | 当错误发生时，发布到 AppService 的事件名，事件对象event.detail = {errMsg: 'something wrong'} |                                                    |
| @load                  | HandleEvent |               | 当图片载入完毕时，发布到 AppService 的事件名，事件对象event.detail = {height:'图片高度px', width:'图片宽度px'} |                                                    |

注意：

- `<image>` 组件**默认宽度 300px、高度 225px**；`app-nvue平台，暂时默认为屏幕宽度`
- `src` 仅支持相对路径、绝对路径，支持 base64 码；
- 页面结构复杂，css样式太多的情况，使用 image 可能导致样式生效较慢，出现 “闪一下” 的情况，此时设置 `image{will-change: transform}` ,可优化此问题。
- 自定义组件里面使用 `<image>`时，若 `src` 使用相对路径可能出现路径查找失败的情况，故建议使用绝对路径。
- webp格式的图片在Android上是内置支持的。iOS上不同平台不一样，具体如下：app-vue下，iOS不支持；app-nvue下，iOS支持；微信小程序2.9.0起，iOS支持。
- svg 格式的图片在不同的平台支持情况不同。具体为：app-nvue 不支持 svg 格式的图片，小程序上只支持网络地址。

**mode有效值说明**

mode 有 14 种模式，其中 5 种是缩放模式，9 种是裁剪模式。

| 模式 | 值              | 说明                                                         |
| :--- | :-------------- | :----------------------------------------------------------- |
| 缩放 | **scaleToFill** | **不保持纵横比缩放图片，使图片的宽高完全拉伸至填满 image 元素** |
| 缩放 | **aspectFit**   | **保持纵横比缩放图片，使图片的长边能完全显示出来。也就是说，可以完整地将图片显示出来。** |
| 缩放 | **aspectFill**  | **保持纵横比缩放图片，只保证图片的短边能完全显示出来。**也就是说，图片通常只在水平或垂直方向是完整的，另一个方向将会发生截取。 |
| 缩放 | **widthFix**    | 宽度不变，高度自动变化，保持原图宽高比不变                   |
| 缩放 | heightFix       | 高度不变，宽度自动变化，保持原图宽高比不变 **App 和 H5 平台 HBuilderX 2.9.3+ 支持、微信小程序需要基础库 2.10.3** |
| 裁剪 | top             | 不缩放图片，只显示图片的顶部区域                             |
| 裁剪 | bottom          | 不缩放图片，只显示图片的底部区域                             |
| 裁剪 | center          | 不缩放图片，只显示图片的中间区域                             |
| 裁剪 | left            | 不缩放图片，只显示图片的左边区域                             |
| 裁剪 | right           | 不缩放图片，只显示图片的右边区域                             |
| 裁剪 | top left        | 不缩放图片，只显示图片的左上边区域                           |
| 裁剪 | top right       | 不缩放图片，只显示图片的右上边区域                           |
| 裁剪 | bottom left     | 不缩放图片，只显示图片的左下边区域                           |
| 裁剪 | bottom right    | 不缩放图片，只显示图片的右下边区域                           |

## 七、uni-app中的样式

- `rpx`即响应式`px`。一种根据屏幕宽度自适应的动态单位。以750宽的屏幕为基准，750rpx恰好为屏幕宽度，屏幕变宽，rpx实际显示效果也会等比放大。

  > 1rpx = 0.5px = 1物理像素
  >
  > 如在iPhone6上，屏幕宽度为375px，共有750个物理像素，则750rpx = 375px = 750物理像素。

- 使用`@import`语句可以导入外联样式表，`@import`后跟需要导入的外联样式表的相对路径，用`;`表示语句结束。

  ```vue
  <style>
  	@import url('./common.css);
          ...
  </style>
  ```

- 支持基本常用的选择器，class、id、element等。

- 在uni-app中不能使用`*`选择器。

- page相当于body节点。

- 定义在App.vue中的样式为全局样式，作用域每一个页面。在pages目录下的vue文件中定义的样式则是局部样式，只作用在响应的页面，并会覆盖App.vue中相同的选择器。

- uni-app支持使用字体图标，使用方式与普通web项目相同，需要注意以下几点：

  - 字体文件小于40kb，uni-app会自动将其转化为base64格式；

  - 字体文件大于等于40kb，需开发者自己转换，否则使用将不生效；

  - 字体文件的引用路径**推荐使用以`~@`开头的绝对路径**。

    ```css
    @font-face {
    	font-family: testi-icon;
    	src: url('~@/static/iconfont.ttf');
    }
    ```

  **字体图标使用**

  - 在static目录下新建`fonts`目录，将iconfont.css及字体图标文件复制到fonts中；

  - 全局使用：

    - 在App.vue中，使用`@import url(~@/static/fonts/iconfont.css)`引入iconfont.css文件；

    - 在iconfont.css文件中修改所有的引入字体图标路径，在路径前面加`~@/static/fonts/`；

    - 使用view标签，添加iconfont对应的字体图标类名即可。

      ```vue
      <view class="iconfont icon-tupian"></view>
      ```

  - 局部使用：

    - 使用方法与全局基本一致，但局部使用在要使用字体图标的vue文件中引入iconfont.css即可。

- **uni.scss**

  ![image-20220425101323589](https://gitee.com/v876774538/my-img/raw/master/image-20220425101323589.png)

  - 声明变量：`$变量名称: 变量值;`

## 八、uni-app中的数据绑定

### 1.数据定义

在页面中定义数据方式与vue中相同，直接在data中定义数据即可。

```js
export default {
	data() {
		return {
			msg: 'hello-uni'
		}
	}
}
```

### 2.插值表达式的使用

- 利用插值表达式渲染基本数据

  ```vue
  <view>{{msg}}</view>
  ```

- 在插值表达式中使用三元运算符

  ```vue
  <view>{{flag ? '我是真的' : '我是假的'}}</view>
  ```

- 基本运算

  ```vue
  <view>{{1 + 1}}</view>
  ```

### 3.v-bind动态绑定

```js
export default {
	data() {
		return {
			imgUrl: 'http://destiny001.gitee.io/image/monkey_02.jpg'
		}
	}
}
```

利用`v-bind`进行渲染

```vue
<image v-bind:src="imgUrl"></image>
<image :src="imgUrl"></image>
```

### 4.v-for遍历

```js
export default {
	data() {
		return {
			list: [
				{
					name:'张三',
					age:21
				},
				{
					name:'李四',
					age:22
				},
				{
					name:'王五',
					age:20
				}
			]
		}
	}
}
```

利用`v-for`进行渲染

```vue
<view>
	<view v-for="(item, index) in list" :key="index">
		序号：{{index}}---姓名：{{item.name}}---年龄：{{item.age}}
	</view>
</view>
```

## 九、uni-app中的事件

### 1.事件绑定

在uni中的事件绑定与vue也是相同的，通过`v-on`进行事件的绑定，也可以简写为`@`。

```vue
<button @click="tapHandle">点我</button>
```

### 2.事件函数定义

```js
methods: {
	tapHandle() {
		console.log('点我了');
	}
}
```

### 3.事件传参

- 默认**若没有传递参数**，则事件函数第一个形参为**事件对象**

  ```vue
  <template>
  	<button @click="tapHandle">点我</button>
  </template>
  <script>
  methods: {
  	tapHandle(e) {
  		console.log(e);
  	}
  }
  </script>
  ```

  ![image-20220425150850364](https://gitee.com/v876774538/my-img/raw/master/image-20220425150850364.png)

- 若给事件函数传递参数了，则对应的事件函数形参接收的则是传递过来的数据

- 如果既想接收数据，又想得到事件对象，可以采取`$event`的方法（访问原始的DOM事件）

  ```vue
  <template>
  	<button @click="tapHandle(20, $event)">点我</button>
  </template>
  <script>
  methods: {
  	tapHandle(num, e) {
  		console.log(num);
  		console.log(e);
  	}
  }
  </script>
  ```

## 十、uni生命周期

> 生命周期的概念：一个对象从创建、运行到销毁的整个过程被称为生命周期。

### 1.应用的生命周期

在生命周期中每个阶段会伴随每个函数的触发，这些函数被称为生命周期函数。

uni-app支持如下**应用生命周期函数**：

| 函数名   | 说明                                                |
| -------- | --------------------------------------------------- |
| onLaunch | 当uni-app（应用）初始化完成时触发（全局只触发一次） |
| onShow   | 当uni-app（应用）启动，或从后台进入前台显示时       |
| onHide   | 当uni-app（应用）从前台进入后台                     |
| onError  | 当uni-app（应用）报错时触发                         |

### 2.页面的生命周期

uni-app支持如下**页面生命周期函数**：

| 函数名                | 说明                                                         | 平台差异说明                | 最低版本 |
| :-------------------- | :----------------------------------------------------------- | :-------------------------- | :------- |
| onInit                | 监听页面初始化，其参数同 onLoad 参数，为上个页面传递的数据，参数类型为 Object（用于页面传参），触发时机早于 onLoad | 百度小程序                  | 3.1.0+   |
| **onLoad**            | 监听页面加载，其**参数为上个页面传递的数据**，参数类型为 Object（用于页面传参），参考[示例](https://uniapp.dcloud.io/api/router#navigateto) |                             |          |
| **onShow**            | 监听页面显示。页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面 |                             |          |
| **onReady**           | 监听页面初次渲染完成。注意如果渲染速度快，会在页面进入动画完成前触发 |                             |          |
| **onHide**            | 监听页面隐藏                                                 |                             |          |
| onUnload              | 监听页面卸载                                                 |                             |          |
| onResize              | 监听窗口尺寸变化                                             | App、微信小程序、快手小程序 |          |
| **onPullDownRefresh** | 监听用户下拉动作，一般用于下拉刷新，参考[示例](https://uniapp.dcloud.io/api/ui/pulldown) |                             |          |
| **onReachBottom**     | 页面滚动到底部的事件（不是scroll-view滚到底），常用于下拉下一页数据。具体见下方注意事项 |                             |          |
| onPageScroll          | 监听页面滚动，参数为Object                                   | nvue暂不支持                |          |

官方文档：https://uniapp.dcloud.io/tutorial/page.html#lifecycle

**页面传参**

```js
//在起始页面跳转到test.vue页面并传递参数
uni.navigateTo({
	url: 'test?id=1&name=uniapp'
});
```

```js
// 在test.vue页面接受参数
export default {
	onLoad: function (option) { //option为object类型，会序列化上个页面传递的参数
		console.log(option.id); //打印出上个页面传递的参数。
		console.log(option.name); //打印出上个页面传递的参数。
	}
}
```



## 十一、下拉刷新

### 1.开启下拉刷新

在uni-app中有两种方式开启下拉刷新：

- 在`page.json`中，找到当前页面的pages节点，在`style`选项中开启`enablePullDownRefresh`，允许下拉刷新，在页面中手动下拉刷新；
- 通过调用`uni.startPullDownRefresh()`方法来开启下拉刷新。

```json
{
	"pages": [ //pages数组中第一项表示应用启动页，参考：https://uniapp.dcloud.io/collocation/pages
		{
			"path": "pages/index/index",
			"style": {
				"enablePullDownRefresh" : true,
				"navigationBarTitleText": "首页",
				"navigationBarBackgroundColor":"#3495FB",
				"navigationBarTextStyle":"white"
			}
		},
	],
}
```

### 2.监听下拉刷新

通过`onPullDownRefresh()`生命周期函数监听下拉刷新动作。

```js
export default {
	data() {
		return {
			arr: ['前端', 'Java', 'ui', '大数据']
		}
	},
	methods: {
		startPull() {
			uni.startPullDownRefresh();
		}
	},
	// 监听下拉刷新
	onPullDownRefresh() {
		console.log('触发下拉刷新了');
	}
}
```

### 3.关闭下拉刷新

通过`uni.stopPullDownRefresh()`方法停止当前页面下拉刷新动画。

```vue
<template>
	<view class="index">
		<button type="primary" @click="startPull">开启下拉刷新</button>
		<view v-for="(item, index) in arr" :key="index">
			{{item}}
		</view>
	</view>
</template>
export default {
	data() {
		return {
			arr: ['前端', 'Java', 'ui', '大数据']
		}
	},
	methods: {
		startPull() {
			uni.startPullDownRefresh();
		}
	},
	// 监听下拉刷新
	onPullDownRefresh() {
		console.log('触发下拉刷新了');
		setTimeout(() => {
			// 更新数据
			this.arr = ['ui', '大数据', '前端', 'Java']
			// 停止下拉刷新
			uni.stopPullDownRefresh();
		}, 1000);
	}
}
```

## 十二、上拉加载

### 1.监听页面触底事件

通过`onReachBottom()`页面周期函数监听页面触底事件。常用于下拉显示下一页数据。

```vue
<template>
	<view class="index">
		<view v-for="(item, index) in arr" :key="index">
			{{item}}
		</view>
	</view>
</template>
<script>
export default {
	data() {
		return {
			arr: ['前端', 'Java', 'ui', '大数据', '前端', 'Java', 'ui', '大数据', '前端', 'Java', 'ui', '大数据', ]
		}
	},
	methods: {
	},
	// 监听页面触底
	onReachBottom() {
		console.log('页面触底了');
		// 加载下一页数据
		this.arr = [...this.arr,...[list.arr]];	// ... 扩展运算符
	}
}
</script>

```

### 2.注意

可在pages.json里定义具体页面底部的触发距离[onReachBottomDistance](https://uniapp.dcloud.io/collocation/pages#globalstyle)。

比如设为50，那么滚动页面到距离底部50px时，就会触发onReachBottom事件。

## 十三、网络请求

在uni中可以调用`uni.request(Object)`方法发送网络请求。

注意：在**小程序**中，网络相关的API在使用前需要**配置域名白名单**。

**Object参数说明：**

|                 |                           |      |        |                                                    |                                                              |
| :-------------- | :------------------------ | :--- | :----- | :------------------------------------------------- | :----------------------------------------------------------- |
| 参数名          | 类型                      | 必填 | 默认值 | 说明                                               | 平台差异说明                                                 |
| **url**         | String                    | 是   |        | **开发者服务器接口地址**                           |                                                              |
| **data**        | Object/String/ArrayBuffer | 否   |        | **请求的参数**                                     | App 3.3.7 以下不支持 ArrayBuffer 类型                        |
| **header**      | Object                    | 否   |        | 设置**请求头**，header 中不能设置 Referer。        | App、H5端会自动带上cookie，且H5端不可手动修改                |
| **method**      | String                    | 否   | GET    | **请求方法**                                       |                                                              |
| timeout         | Number                    | 否   | 60000  | 超时时间，单位 ms                                  | H5(HBuilderX 2.9.9+)、APP(HBuilderX 2.9.9+)、微信小程序（2.10.0）、支付宝小程序 |
| dataType        | String                    | 否   | json   | 如果设为 json，会尝试对返回的数据做一次 JSON.parse |                                                              |
| responseType    | String                    | 否   | text   | 设置响应的数据类型。合法值：text、arraybuffer      | 支付宝小程序不支持                                           |
| sslVerify       | Boolean                   | 否   | true   | 验证 ssl 证书                                      | 仅App安卓端支持（HBuilderX 2.3.3+），不支持离线打包          |
| withCredentials | Boolean                   | 否   | false  | 跨域请求时是否携带凭证（cookies）                  | 仅H5支持（HBuilderX 2.6.15+）                                |
| firstIpv4       | Boolean                   | 否   | false  | DNS解析时优先使用ipv4                              | 仅 App-Android 支持 (HBuilderX 2.8.0+)                       |
| **success**     | Function                  | 否   |        | 收到开发者服务器成功返回的回调函数                 |                                                              |
| **fail**        | Function                  | 否   |        | 接口调用失败的回调函数                             |                                                              |
| complete        | Function                  | 否   |        | 接口调用结束的回调函数（调用成功、失败都会执行）   |                                                              |

```js
uni.request({
    url: 'https://www.example.com/request', //仅为示例，并非真实接口地址。
    data: {
        text: 'uni.request'
    },
    header: {
        'custom-header': 'hello' //自定义请求头信息
    },
    success: (res) => {
        console.log(res.data);
        this.text = 'request success';
    }
});
```

## 十四、数据缓存

### 1.uni.setStorage

`uni.setStorage(OBJECT)`将数据存储在本地缓存中指定的key中，会覆盖掉原来该key对应的内容。这是一个**异步**接口。

**OBJECT参数说明：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| key      | String   | 是   | 本地缓存中的指定的 key                                       |
| data     | Any      | 是   | 需要存储的内容，只支持原生类型、及能够通过 JSON.stringify 序列化的对象 |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

**示例**

```js
uni.setStorage({
	key: 'storage_key',
	data: 'hello',
	success: function () {
		console.log('success');
	}
});
```

### 2.uni.setStorageSync

`uni.setStorageSync(KEY, DATA)`将 data 存储在本地缓存中指定的 key 中，会覆盖掉原来该 key 对应的内容。这是一个**同步**接口。

**参数说明**

| 参数 | 类型   | 必填 | 说明                                                         |
| :--- | :----- | :--- | :----------------------------------------------------------- |
| key  | String | 是   | 本地缓存中的指定的 key                                       |
| data | Any    | 是   | 需要存储的内容，只支持原生类型、及能够通过 JSON.stringify 序列化的对象 |

**示例**

```javascript
try {
	uni.setStorageSync('storage_key', 'hello');
} catch (e) {
	// error
}
```

### 3.uni.getStorage

`uni.getStorage(OBJECT)`从本地缓存中异步获取指定 key 对应的内容。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| key      | String   | 是   | 本地缓存中的指定的 key                           |
| success  | Function | 是   | 接口调用的回调函数，res = {data: key对应的内容}  |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

**success 返回参数说明**

| 参数 | 类型 | 说明           |
| :--- | :--- | :------------- |
| data | Any  | key 对应的内容 |

**示例**

```javascript
uni.getStorage({
	key: 'storage_key',
	success: function (res) {
		console.log(res.data);
	}
});
```

### 4.uni.getStorageSync

`uni.getStorageSync(KEY)`从本地缓存中同步获取指定 key 对应的内容。

**参数说明**

| 参数 | 类型   | 必填 | 说明                   |
| :--- | :----- | :--- | :--------------------- |
| key  | String | 是   | 本地缓存中的指定的 key |

**示例**

```javascript
try {
	const value = uni.getStorageSync('storage_key');
	if (value) {
		console.log(value);
	}
} catch (e) {
	// error
}
```

### 5.uni.removeStorage

`uni.removeStorage(OBJECT)`从本地缓存中异步移除指定 key。

**OBJECT 参数说明**

| 参数名   | 类型     | 必填 | 说明                                             |
| :------- | :------- | :--- | :----------------------------------------------- |
| key      | String   | 是   | 本地缓存中的指定的 key                           |
| success  | Function | 是   | 接口调用的回调函数                               |
| fail     | Function | 否   | 接口调用失败的回调函数                           |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |

**示例**

```javascript
uni.removeStorage({
	key: 'storage_key',
	success: function (res) {
		console.log('success');
	}
});
```

### 6.uni.removeStorageSync

`uni.removeStorageSync(KEY)`从本地缓存中同步移除指定 key。

**参数说明**

| 参数名 | 类型   | 必填 | 说明                   |
| :----- | :----- | :--- | :--------------------- |
| key    | String | 是   | 本地缓存中的指定的 key |

**示例**

```javascript
try {
	uni.removeStorageSync('storage_key');
} catch (e) {
	// error
}
```

### 7.uni.clearStorage

`uni.clearStorage()`清理本地数据缓存。

**示例**

```javascript
uni.clearStorage();
```

### 8.uni.clearStorageSync

`uni.clearStorageSync()`同步清理本地数据缓存。

**示例**

```javascript
try {
	uni.clearStorageSync();
} catch (e) {
	// error
}
```

## 十五、上传、预览图片

### 1.上传图片

`uni.chooseImage(OBJECT)`方法从本地相册选择图片或使用相机拍照。

**OBJECT 参数说明**

| 参数名     | 类型          | 必填 | 说明                                                         | 平台差异说明                              |
| :--------- | :------------ | :--- | :----------------------------------------------------------- | :---------------------------------------- |
| count      | Number        | 否   | 最多可以选择的图片张数，默认9                                | 见下方说明                                |
| sizeType   | Array<String> | 否   | original 原图，compressed 压缩图，默认二者都有               | App、微信小程序、支付宝小程序、百度小程序 |
| extension  | Array<String> | 否   | 根据文件拓展名过滤，每一项都不能是空字符串。默认不过滤。     | H5(HBuilder X2.9.9+)                      |
| sourceType | Array<String> | 否   | album 从相册选图，camera 使用相机，默认二者都有。如需直接开相机或直接选相册，请只使用一个选项 |                                           |
| crop       | Object        | 否   | 图像裁剪参数，设置后 sizeType 失效                           | App 3.1.19+                               |
| success    | Function      | 是   | 成功则返回图片的本地文件路径列表 tempFilePaths               |                                           |
| fail       | Function      | 否   | 接口调用失败的回调函数                                       | 小程序、App                               |
| complete   | Function      | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |                                           |

- count 值在 H5 平台的表现，基于浏览器本身的规范。目前测试的结果来看，只能限制单选/多选，并不能限制数量。并且，在实际的手机浏览器很少有能够支持多选的。

**示例**

```vue
<template>
	<view>
		<button type="primary" @click="chooseImg">上传图片</button>
        <!-- 渲染图片 -->
         <view class="imgGroup">
    		<image v-for="(item,index) in imgArr" :key="index" :src="item"></image>
    	</view>
	</view>
</template>

<script>
export default {
	data() {
		// 存储图片
		imgArr: [],
	},
	methods: {
		chooseImg() {
			uni.chooseImage({
				count: 5,	// 最多可选择图片张数
				success: (res) => {
                    this.imgArr = res.tempFilePaths;
                    console.log(this.imgArr);
                }
			})
		}
	}
}
</script>
```

### 2.预览图片

`uni.previewImage(OBJECT)`预览图片。

**OBJECT 参数说明**

| 参数名           | 类型          | **必填**     | **说明**                                                     | **平台差异说明** |
| :--------------- | :------------ | :----------- | :----------------------------------------------------------- | :--------------- |
| **current**      | String/Number | 详见下方说明 | current 为**当前显示图片的链接/索引值**，不填或填写的值无效则为 urls 的第一张 |                  |
| urls             | Array<String> | 是           | 需要预览的图片链接列表                                       |                  |
| indicator        | String        | 否           | 图片指示器样式，可取值："default" - 底部圆点指示器； "number" - 顶部数字指示器； "none" - 不显示指示器。 | App              |
| loop             | Boolean       | 否           | 是否可循环预览，默认值为 false                               | App              |
| longPressActions | Object        | 否           | 长按图片显示操作菜单，如不填默认为**保存相册**               | App 1.9.5+       |
| **success**      | Function      | 否           | 接口调用成功的回调函数                                       |                  |
| fail             | Function      | 否           | 接口调用失败的回调函数                                       |                  |
| complete         | Function      | 否           | 接口调用结束的回调函数（调用成功、失败都会执行）             |                  |

**示例**

```vue
<template>
	<view>
		<button type="primary" @click="chooseImg">上传图片</button>
        <!-- 渲染图片 -->
         <view class="imgGroup">
    		<image
    			v-for="(item,index) in imgArr" 
    			:key="index" 
    			:src="item"
    			@click="previewImg(item)"></image>
    	</view>
	</view>
</template>

<script>
export default {
	data() {
		// 存储图片
		imgArr: [],
	},
	methods: {
		// 选择图片
		chooseImg() {
			uni.chooseImage({
				count: 5,	// 最多可选择图片张数
				success: (res) => {
                    this.imgArr = res.tempFilePaths;
                    console.log(this.imgArr);
                }
			})
		},
		// 预览图片
		previewImg(current) {
			console.log(current);
			uni.previewImage({
				current,
				urls: this.imgArr,	// 需要预览的图片链接列表
				loop: true,	// 允许循环预览
			})
		}
		
	}
}
</script>
```

## 十六、条件注释实现跨端兼容

条件编译是用特殊的注释作为标记，在编译时根据这些特殊的注释，**将注释里的代码编译到不同的平台**。

写法：以`#ifdef 平台标识`开头，以`#endif`结尾。

平台标识：

| 值         | 平台                           |
| ---------- | ------------------------------ |
| APP-PLUS   | 5+APP                          |
| H5         | H5                             |
| MP-WEIXIN  | 微信小程序                     |
| MP-ALIPAY  | 支付宝小程序                   |
| MP-BAIDU   | 百度小程序                     |
| MP-TOUTIAO | 头条小程序                     |
| MP-QQ      | QQ小程序                       |
| MP         | 微信/支付宝/百度/头条/QQ小程序 |

```vue
<!-- #ifdef H5 -->
<view>
	H5页面会显示
</view>
<!-- #endif -->
<!-- #ifdef MP-WEIXIN -->
<view>
	微信小程序会显示
</view>
<!-- #endif -->
<!-- #ifdef APP-PLUS -->
<view>
	APP会显示
</view>
<!-- #endif -->
```

## 十七、uni中的导航跳转

### 1.声明式导航跳转

利用**navigator组件**进行页面跳转。

该**组件**类似HTML中的`<a>`组件，但只能跳转本地页面。目标页面必须在pages.json中注册。

**属性说明**

| 属性名                 | 类型    | 默认值          | 说明                                                         | 平台差异说明               |
| :--------------------- | :------ | :-------------- | :----------------------------------------------------------- | :------------------------- |
| **url**                | String  |                 | 应用内的跳转链接，值为相对路径或绝对路径，如："../first/first"，"/pages/first/first"，注意不能加 `.vue` 后缀 |                            |
| **open-type**          | String  | navigate        | 跳转方式                                                     |                            |
| delta                  | Number  |                 | 当 open-type 为 'navigateBack' 时有效，表示回退的层数        |                            |
| animation-type         | String  | pop-in/out      | 当 open-type 为 navigate、navigateBack 时有效，窗口的显示/关闭动画效果，详见：[窗口动画](https://uniapp.dcloud.io/api/router#animation) | App                        |
| animation-duration     | Number  | 300             | 当 open-type 为 navigate、navigateBack 时有效，窗口显示/关闭动画的持续时间。 | App                        |
| hover-class            | String  | navigator-hover | 指定点击时的样式类，当hover-class="none"时，没有点击态效果   |                            |
| hover-stop-propagation | Boolean | false           | 指定是否阻止本节点的祖先节点出现点击态                       | 微信小程序                 |
| hover-start-time       | Number  | 50              | 按住后多久出现点击态，单位毫秒                               |                            |
| hover-stay-time        | Number  | 600             | 手指松开后点击态保留时间，单位毫秒                           |                            |
| target                 | String  | self            | 在哪个小程序目标上发生跳转，默认当前小程序，值域self/miniProgram | 微信2.0.7+、百度2.5.2+、QQ |

**open-type 有效值**

| 值            | 说明                                                         | 平台差异说明                     |
| :------------ | :----------------------------------------------------------- | :------------------------------- |
| **navigate**  | 对应 uni.navigateTo 的功能（默认，保留当前页面，跳转到应用内的某个页面，使用`uni.navigateBack`可以返回到原页面） |                                  |
| redirect      | 对应 uni.redirectTo 的功能（关闭当前页面，跳转到应用内的某个页面） |                                  |
| **switchTab** | 对应 uni.switchTab 的功能（跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面） |                                  |
| reLaunch      | 对应 uni.reLaunch 的功能（关闭所有页面，打开到应用内的某个页面） | 字节跳动小程序与飞书小程序不支持 |
| navigateBack  | 对应 uni.navigateBack 的功能（关闭当前页面，返回上一页面或多级页面。可通过 `getCurrentPages()` 获取当前的页面栈，决定需要返回几层） |                                  |
| exit          | 退出小程序，target="miniProgram"时生效                       | 微信2.1.0+、百度2.5.2+、QQ1.4.7+ |

#### 1.1跳转到普通页面

```vue
<navigator url="/pages/about/about" hover-class="navigator-hover">
	<button type="default">跳转到关于界面</button>
</navigator>
```

#### 1.2 跳转到tabBar界面

```vue
<navigator url="/pages/message/message" open-type="switchTab">
	<button type="default">跳转到Tab信息界面</button>
</navigator>
```

### 2.编程式导航跳转

利用路由与页面跳转API实现导航跳转。

#### 2.1 uni.navigateTo(OBJECT)

保留当前页面，跳转到应用内的某个页面，使用`uni.navigateBack`可以返回到原页面。

**OBJECT参数说明**

| 参数              | 类型     | 必填 | ****默认值**** | 说明                                                         | ****平台差异说明**** |
| :---------------- | :------- | :--- | :------------- | :----------------------------------------------------------- | :------------------- |
| **url**           | String   | 是   |                | 需要跳转的应用内**非 tabBar 的页面的路径** , **路径后可以带参数**。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2'，path为下一个页面的路径，下一个页面的**onLoad函数**可**得到传递的参数** |                      |
| animationType     | String   | 否   | pop-in         | 窗口显示的动画效果，详见：[窗口动画](https://uniapp.dcloud.io/api/router#animation) | App                  |
| animationDuration | Number   | 否   | 300            | 窗口动画持续时间，单位为 ms                                  | App                  |
| events            | Object   | 否   |                | 页面间通信接口，用于监听被打开页面发送到当前页面的数据。2.8.9+ 开始支持。 |                      |
| **success**       | Function | 否   |                | 接口调用成功的回调函数                                       |                      |
| fail              | Function | 否   |                | 接口调用失败的回调函数                                       |                      |
| complete          | Function | 否   |                | 接口调用结束的回调函数（调用成功、失败都会执行）             |                      |

```vue
<template>
	<button @click="goDetail">
        跳转到详情页
    </button>
	<button @click="goMessage">
        跳转到信息页
    </button>
</template>

<script>
export default {
    methods: {
        goDetail() {
            // 普通页面
            uni.navigateTo({
                url: '/pages/detail/detail'
            })
        },
        goMessage() {
            // tabBar页面
            uni.switchTab({
                url: '/pages/message/message'
            })
        }
    }
}
</script>
```

**传递参数**

```js
//在起始页面跳转到test.vue页面并传递参数
uni.navigateTo({
	url: 'test?id=1&name=uniapp'
});
```

```js
// 在test.vue页面接受参数
export default {
	onLoad: function (option) { //option为object类型，会序列化上个页面传递的参数
		console.log(option.id); //打印出上个页面传递的参数。
		console.log(option.name); //打印出上个页面传递的参数。
	}
}
```

#### 2.2 uni.redirectTo(OBJECT)

关闭当前页面，跳转到应用内的某个页面。

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| url      | String   | 是   | 需要跳转的应用内非 tabBar 的页面的路径，路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2' |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

#### 2.3 uni.reLaunch(OBJECT)

关闭所有页面，打开到应用内的某个页面。

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| url      | String   | 是   | 需要跳转的应用内页面路径 , 路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2'，如果跳转的页面路径是 tabBar 页面则不能带参数 |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

#### 2.4 uni.switchTab(OBJECT)

跳转到**tabBar页面**，并关闭其他所有非 tabBar 页面。

**OBJECT参数说明**

| 参数     | 类型     | 必填 | 说明                                                         |
| :------- | :------- | :--- | :----------------------------------------------------------- |
| url      | String   | 是   | 需要跳转的 tabBar 页面的路径（需在 pages.json 的 tabBar 字段定义的页面），路径后不能带参数 |
| success  | Function | 否   | 接口调用成功的回调函数                                       |
| fail     | Function | 否   | 接口调用失败的回调函数                                       |
| complete | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行）             |

```json
// pages.json
{
  "tabBar": {
    "list": [{
      "pagePath": "pages/index/index",
      "text": "首页"
    },{
      "pagePath": "pages/other/other",
      "text": "其他"
    }]
  }
}
```

```js
// other.vue
uni.switchTab({
	url: '/pages/index/index'
});
```

#### 2.5 uni.navigateBack(OBJECT)

关闭当前页面，返回上一页面或多级页面。可通过 `getCurrentPages()` 获取当前的页面栈，决定需要返回几层。

**OBJECT参数说明**

| 参数              | 类型     | 必填 | 默认值                                           | 说明                                                         | 平台差异说明 |
| :---------------- | :------- | :--- | :----------------------------------------------- | :----------------------------------------------------------- | :----------- |
| **delta**         | Number   | 否   | 1                                                | **返回的页面数**，如果 delta 大于现有页面数，则返回到首页。  |              |
| animationType     | String   | 否   | pop-out                                          | 窗口关闭的动画效果，详见：[窗口动画](https://uniapp.dcloud.io/api/router#animation) | App          |
| animationDuration | Number   | 否   | 300                                              | 窗口关闭动画的持续时间，单位为 ms                            | App          |
| success           | Function | 否   | 接口调用成功的回调函数                           |                                                              |              |
| fail              | Function | 否   | 接口调用失败的回调函数                           |                                                              |              |
| complete          | Function | 否   | 接口调用结束的回调函数（调用成功、失败都会执行） |                                                              |              |

```js
// 注意：调用 navigateTo 跳转时，调用该方法的页面会被加入堆栈，而 redirectTo 方法则不会。见下方示例代码

// 此处是A页面
uni.navigateTo({
	url: 'B?id=1'
});

// 此处是B页面
uni.navigateTo({
	url: 'C?id=1'
});

// 在C页面内 navigateBack，将返回A页面
uni.navigateBack({
	delta: 2
});
```

## 十八、uni-app中组件的创建

### 1.组件的创建

在uni-app中，可以通过创建一个后缀名为vue的文件，创建一个组件。

其他组件使用该组件时，可以通过`import`方式将其导入，然后通过components进行注册即可。

- 创建login组件，在components中创建login目录。然后新建login.vue文件

  ![image-20220426105152690](https://gitee.com/v876774538/my-img/raw/master/image-20220426105152690.png)

  ```vue
  <template>
  	<view>
  		这是一个自定义组件
  	</view>
  </template>
  
  <script>
  </script>
  ```

- 在其他组件中导入该组件并注册

  ```js
  import login from "@/components/login/login.vue"
  ```

- 注册组件

  ```js
  export default {
  	components: {
  		login
  	}
  }
  ```

- 使用组件

  ```vue
  <template>
  	<view>
  		<login></login>
  	</view>
  </template>
  ```

### 2.组件的生命周期函数

`uni-app` 组件支持的生命周期，**与vue标准组件的生命周期相同**。这里没有页面级的onLoad等生命周期：

| 函数名        | 说明                                                         | 平台差异说明 | 最低版本 |
| :------------ | :----------------------------------------------------------- | :----------- | :------- |
| beforeCreate  | 在实例初始化之前被调用。[详见(opens new window)](https://cn.vuejs.org/v2/api/#beforeCreate) |              |          |
| **created**   | 在实例创建完成后被立即调用。[详见(opens new window)](https://cn.vuejs.org/v2/api/#created)我们可以在created中对**数据**进行**初始化**。 |              |          |
| beforeMount   | 在挂载开始之前被调用。[详见(opens new window)](https://cn.vuejs.org/v2/api/#beforeMount) |              |          |
| **mounted**   | **挂载到实例上**去之后调用。[详见 (opens new window)]我们可以在mounted()中**操作DOM**。(https://cn.vuejs.org/v2/api/#mounted)注意：此处并不能确定子组件被全部挂载，如果需要子组件完全挂载之后在执行操作可以使用`$nextTick`[Vue官方文档(opens new window)](https://cn.vuejs.org/v2/api/#Vue-nextTick) |              |          |
| beforeUpdate  | 数据更新时调用，发生在虚拟 DOM 打补丁之前。[详见(opens new window)](https://cn.vuejs.org/v2/api/#beforeUpdate) | 仅H5平台支持 |          |
| updated       | 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。[详见(opens new window)](https://cn.vuejs.org/v2/api/#updated) | 仅H5平台支持 |          |
| beforeDestroy | 实例销毁之前调用。在这一步，实例仍然完全可用。[详见(opens new window)](https://cn.vuejs.org/v2/api/#beforeDestroy) |              |          |
| **destroyed** | Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。[详见(opens new window)](https://cn.vuejs.org/v2/api/#destroyed) |              |          |

## 十九、组件通讯

### 1.父组件=>子组件

父组件向子组件传递数据：

```vue
<template>
	<view>
		我是父组件
		<!-- 子组件 -->
		<test :msg="msg"></test>
	</view>
</template>

<script>
import test from "@/components/test/test.vue"
export default {
    components: {
        test
    }
}
</script>
```

子组件通过`props`来接收父组件传递的值：

```vue
<template>
	<view>
    	我是子组件：{{msg}}
    </view>
</template>

<script>
export default {
    props: ['msg']
}
</script>
```

### 2.子组件=>父组件

> 通过$emit触发**自定义事件**

子组件向父组件传递数据：

```vue
<template>
	<view>
    	我是子组件：{{msg}}
    	<button @click="sendMsg">向父组件传值</button>
    </view>
</template>

<script>
export default {
    data() {
        return {
            hobby: '打游戏'
        }
    }
    props: ['msg'],
    methods: {
        sendMsg() {
            // 触发
            this.$emit('myEvent', this.hobby);
        }
    }
}
</script>
```

父组件接收数据：

```vue
<template>
	<view>
		我是父组件
		<!-- 子组件 -->
         <!-- 自定义事件 myEvent 回调函数 getHobby-->
		<test :msg="msg" @myEvent="getHobby"></test>
         <view>爱好：{{hobby}}</view>
	</view>
</template>

<script>
import test from "@/components/test/test.vue"
export default {
    data() {
        return {
            hobby:''
        }
    },
    components: {
        test
    },
    methods: {
        getHobby(hobby) {
            console.log(hobby);
            this.hobby = hobby;
        }
    }
}
</script>
```

### 3.兄组件<=>弟组件

#### 2.1 uni.$emit(eventName, OBJECT)

**触发全局的自定义事件**。附加参数都会**传**给监听器回调。

| 属性      | 类型   | 描述                   |
| --------- | ------ | ---------------------- |
| eventName | String | 事件名                 |
| OBJECT    | Object | 触发事件携带的附加参数 |

**代码示例**

```javascript
uni.$emit('update',{msg:'页面更新'})
```

#### 2.2 uni.$on(eventName, callback)

**监听全局的自定义事件**。事件可以由 `uni.$emit` 触发，回调函数会**接收**所有传入事件触发函数的额外参数。

| 属性      | 类型     | 描述           |
| --------- | -------- | -------------- |
| eventName | String   | 事件名         |
| callback  | Function | 事件的回调函数 |

**代码示例**

```javascript
uni.$on('update',function(data){
    console.log('监听到事件来自 update ，携带参数 msg 为：' + data.msg);
})
```

#### 2.3 uni.$off([eventName, callback])

移除全局自定义事件监听器。

| 属性      | 类型            | 描述           |
| --------- | --------------- | -------------- |
| eventName | Array＜String＞ | 事件名         |
| callback  | Function        | 事件的回调函数 |

**Tips**

- 如果没有提供参数，则移除所有的事件监听器；
- 如果**只提供**了**事件**，则**移除该事件所有的监听器**；
- 如果同时提供了事件与回调，则只移除这个回调的监听器；
- 提供的回调必须跟$on的回调为同一个才能移除这个回调的监听器；



用法类似于Vue中的**全局事件总线**：

```vue
<template>
	<view>
        我是组件A
        <view>num={{num}}</view>
	</view>
</template>

<script>
export default {
    data() {
        return {
            num: 0
        }
    },
    methods: {

    },
    onLoad() {
        // 全局监听
        uni.$on('updateNum', num => {
            this.num += num;
        })
    },
    onUnload() {
        // 销毁
        uni.$off('updateNum');
    }
}
</script>
```

```vue
<template>
	<view>
    	我是组件B
        <button @click="addNum">+</button>
    </view>
</template>

<script>
export default {
    data() {
        return {
            num: 0
        }
    },
    methods: {
        addNum() {
            this.num++;
            // 触发全局的定义事件
            uni.$emit('updateNum', this.num);
        }
    }
}
</script>
```

## 二十、uni-ui组件库的基本介绍和使用

官方文档：https://uniapp.dcloud.io/component/uniui/quickstart.html

# uni-app 黑马商城项目

## 一、request请求封装

### 1.common/api.js

```js
const BASE_URL = 'https://api-hmugo-web.itheima.net/api/public/v1'
export const myRequest = (options) => {
	return new Promise((resolve, reject) => {
		uni.request({
			url: BASE_URL + options.url,
			method: options.method || 'GET',
			data: options.data || {},
			success: (res) => {
				if (res.data.meta.status != 200) {
					return uni.showToast({
						title: '获取数据失败'
					})
				}
				resolve(res);
			},
			fail: (err) => {
				uni.showToast({
					title: '请求接口失败'
				})
				reject(err);
			}
		})
	})
}

```

### 2.main.js引入

```js
import {myRequest} from './common/api.js'
```

### 3.调用请求

```js
// 获取轮播图数据
getSwiperList() {
    this.$myRequest({
        url: '/home/swiperdata'
    }).then(res => {
        // promise对象，promise对象的值PromiseResult获取只能通过.then()方法获取！
        this.swiperList = res.data.message;
    })
}
```



