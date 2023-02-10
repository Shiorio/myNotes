# HTML简介

## 一、网页的相关概念

1. 网站：在因特网上根据一定的规则，使用HTML等制作的用于展示特定内容的相关**网页的集合**。
2. 网页：主要是由文字、图像和超链接等元素构成。当然除了这些元素，网页中还可以包括音频、视频以及Flash等。通常是**HTML格式的文件**（以.htm或.html为后缀结尾），通过浏览器来阅读。
3. HTML：**超文本标记语言**（Hyper Text Markup Language），它是用来描述网页的一种语言。
4. 超文本：①它可以加入图片、声音、动画、多媒体等内容（超越了文本限制）；②它还可以从一个文件跳转到另一个文件，与世界各地主机的文件连接（超级链接文本）。
5. 网页的形成：前端人员开发代码----->浏览器显示代码（解析、渲染）----->生成最后的Web页面。

## 二、常用浏览器及其内核

1. 浏览器是网页显示、运行的平台。常用的浏览器：IE浏览器、火狐（Firefox）、**谷歌（Chrome）**、Safari、Opera等。

2. 浏览器内核：浏览器内核（渲染引擎）。负责读取网而言内容，整理信息，计算网页的显示方式并显示页面。

   | 浏览器       | 内核    | 备注                                            |
   | ------------ | ------- | ----------------------------------------------- |
   | IE           | Trident | IE、猎豹安全、360极速浏览器、百度浏览器         |
   | firefox      | Gecko   | 火狐浏览器内核                                  |
   | Safari       | Webkit  | 苹果浏览器内核                                  |
   | Chrome/Opera | Blink   | Chrome/Opera浏览器内核，Blink其实是Webkit的分支 |

   目前国内一般浏览器都会采用Webkit/Blink内核，如360、UC、QQ、搜狗等。

3. **Web标准**

   - **Web标准**是由W3C组织和其他标准化组织制定的**一系列标准的集合**。W3C（万维网联盟）是国际最著名的标准化组织。

   - Web标准都构成：主要包括结构（Structure）、表现（Presentation）和行为（Behavior）三个方面。

     | 标准 | 说明                                                         |
     | ---- | ------------------------------------------------------------ |
     | 结构 | 结构用于对**网页元素**进行整理和分类，现阶段主要学的是**HTML** |
     | 表现 | 表现用于设置网页元素的版式、颜色、大小等**外观样式**，主要指**CSS** |
     | 行为 | 行为是指网页模型的定义及交互的编写，现阶段主要学的是**javascript** |

     Web标准提出的最佳体验方案：**结构、样式、行为相分离**。

# HTML标签

## 一、HTML语法规范

1. 基本语法概述

   - HTML标签是**由尖括号包围的关键词**，例如<html>
   - **双标签**：包含开始标签和结束标签，例如<html>和</html>
   - **单标签**：例如<br/>

2. 标签关系

   - 双标签关系可以分为两类：**包含关系**与**并列关系**。

   - 包含关系：

     ```html
     <head>
     	<title></title>
     </head>
     ```

   - 并列关系：

     ```html
     <head></head>
     <body></body>
     ```

## 二、HTML基本结构标签

```html
<html>
	<head>
		<title>我的第一个页面</title>
	</head>
	<body>
		1234
	</body>
</html>
```

| 标签名          | 定义       | 说明                                               |
| --------------- | ---------- | -------------------------------------------------- |
| <html></html>   | HTML标签   | 页面中最大的标签，我们称为**根标签**               |
| <head></head>   | 文档的头部 | 在head标签中我们必须要设置的标签是**title**        |
| <title></title> | 文档的标题 | 让页面拥有一个属于自己的网页标题                   |
| <body></body>   | 文档的主题 | 元素包含文档的所有内容，页面内容基本都放到body里面 |

![image-20210701145835839](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210701145835839.png)

## 三、DOCTYPE和lang以及字符集的作用

1.  <!DOCTYPE>标签

   **文档类型声明**，作用是告诉浏览器使用哪种HTML版本来显示网页。

   ```html
   <!DOCTYPE html>
   ```

   当前页面采取的是最新的HTML5的版本来显示网页的。

   **注意：**

   - < !DOCTYPE>声明位于文档中最前的位置
   - < !DOCTYPE>**不是一个HTML标签**，它就是文档类型声明标签

2. lang语言

   用来定义当前文档显示的语言：

   - en定义语言为英语
   - zh-CN定义语言为中文

   简单来说定义en就是英文网页，定义为zh-CN就是中文网页，但其实相对于文档显示来说，定义成en的文档也可以显示中文，同理定义成zh-CN的文档也可以显示英文

   **对浏览器和搜索引擎有提示作用**

3. 字符集

   字符集（Character set）是多个字符的集合，以便计算机能够识别和存储各种文字。

   在<head>标签内，可以通过**<meta>**标签的**charset**属性来规定HTML文档应该使用哪种字符编码。

   ```html
   <meta charset="UTF-8" />
   ```

   charset常用的值有：GB2312、BIG5、GBK和UTF-8，其中**UTF-8**也被称为**万国码**，其中包含了全世界所有国家需要用到的字符。

## 四、HTML常用标签

1. 标签语义

   **标签的含义。**根据标签的语义，在合适的地方给一个最为合理的标签，可以让页面结构更清晰。

   ![image-20210701155446140](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210701155446140.png)

   ![image-20210701155602442](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210701155602442.png)

2. **标题标签<h1>-<h6>**

   单词head的缩写，意为头部、标题。

   ```html
   <h1>我是一级标题</h1>
   ```

   标签语义：作为标题使用，并且根据重要性递减。

   特点：

   - 加了标题的文字会变得**加粗**，字号也会依次**变大**
   - 一个标题独占一行

3. **段落标签<p>和换行标签<br/>**

   1）p是paragraph的缩写，用于**定义段落**，它可以将网页分为若干个段落。

   ```html
   <p>我是一个段落标签</p>
   ```

   **特点：**

   - 文本在一个段落中会根据浏览器窗口的大小**自动换行**
   - **段落和段落中保有一定空隙**

   2）在HTML中，一个段落中的文字会从左到右依次排序，直到浏览器窗口的右端，然后才自动换行，如果希望某段文本强制**换行显示**，就需要用到换行标签<br/>

   ```html
   <br/>
   ```

   br是单词break的缩写，意为打断、换行。

   **特点：**

   - 单标签
   - 只是简单地开始新的一行，跟段落不同，段落之间会插入一段垂直距离（空隙）

4. 文本格式化标签

   标签语义：突出重要性，比普通文字更重要

   | 语义   | 标签                         | 说明                           |
   | ------ | ---------------------------- | ------------------------------ |
   | 加粗   | <strong></strong>或者<b></b> | 更推荐使用<strong>，语义更强烈 |
   | 倾斜   | <em></em>或者<i></i>         | 更推荐使用<em>，语义更强烈     |
   | 删除线 | <del></del>或者<s></s>       | 更推荐使用<del>，语义更强烈    |
   | 下划线 | <ins></ins>或者<u></u>       | 更推荐使用<ins>，语义更强烈    |

5. `<div>`和`<span>`标签

   `<div>`和`<span>`标签都是**没有语义**的，它们是用来**装内容的盒子**，用来**布局**。

   ```html
   <div>这是头部</div>
   <span>今日价格</span>
   ```

   div是division的缩写，表示分割、分区；

   span的意思是跨度、跨距。

   **特点：**

   - div是**块元素**，**独占一行**，可以理解为一个大盒子
   - span是**行内元素**，一行可以放多个span，可以理解为小盒子

6. **图像标签和路径**

   1）图像标签

   在HTML标签中，<img>标签用于定义HTML页面中的图像。

   ```html
   <img src="图像URL" />
   ```

   img是单词image的缩写，意为图像。

   | 属性      | 属性值   | 说明                                               |
   | --------- | -------- | -------------------------------------------------- |
   | **src**   | 图片路径 | **必须属性**，用于指定图像文件的路径和文件名       |
   | **alt**   | 文本     | **替换文本**，当图像不能显示时显示的文字           |
   | **title** | 文本     | **提示文本**，当鼠标放到图像上时显示的文字         |
   | width     | 像素     | 设置图像的宽度，若只修改宽度，高度会自动等比例缩放 |
   | height    | 像素     | 设置图像的高度，若只修改高度，宽度会自动等比例缩放 |
   | border    | 像素     | 设置图像的边框粗细（一般在CSS中设定）              |

   **注意：**

   - 图像标签可以拥有多个属性，但都要写在标签名后面
   - 属性之间不分先后顺序，属性和属性之间以空格分隔
   - 属性采用键值对的格式，即**属性="属性值"**

   2）路径

   - 相对路径：

     以引用文件所在位置为参考基础，而建立出的目录路径

     | 相对路径分类 | 符号 | 说明                                                        |
     | ------------ | ---- | ----------------------------------------------------------- |
     | 同一级路径   |      | 图像文件位于HTML文件同一级，如<img src="baidu.gif"/>        |
     | 下一级路径   | /    | 图像文件位于HTML文件下一级，如<img src="images/baidu.gif"/> |
     | 上一级路径   | ../  | 图像文件位于HTML文件上一级，如<img src="../baidu.gif"/>     |

   - 绝对路径：是指目录下的绝对位置，直接到达目标位置，通常是从盘符开始的路径

     例如，"D:\web\img\logo.gif"或完整的网页图片地址"http://www.itcast.cn/images/logo.gif"

7. **超链接标签**

   在HTML标签中，<a>标签用于定义超链接，作用是从一个页面链接到另一个页面。

   - 链接的语法格式

     ```html
     <a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
     ```

     使文字或图像具有超链接的功能。

     a是anchor的缩写，意为锚。

     | 属性   | 作用                                                         |
     | ------ | ------------------------------------------------------------ |
     | href   | 用于指定链接**目标的url地址（必须属性）**，当为标签应用href属性时，它就具有了超链接的功能 |
     | target | 用于指定**链接页面的打开方式**，其中_self为默认值， _blank为在新窗口中打开 |

   - 链接的分类

     ①外部链接，例如

     ```html
     <a href="http://www.baidu.com">百度</a>
     ```

     ②内部链接，网站内部页面之间的相互链接，直接链接内部页面名称即可，例如

     ```html
     <a href="index.html">首页</a>
     ```

     ③空链接，即没有确定链接目标，例如

     ```html
     <a href="#">首页</a>
     ```

     ④下载链接，href里面地址是一个文件或者压缩包，点击将会下载这个文件，例如

     ```html
     <a href="img.zip">下载文件</a>
     ```

     ⑤网页元素链接，在网页中的各种网页元素，如文本、图像、表格、音频、视频等都可以添加超链接，例如

     ```html
     <a href="http://www.baidu.com">
     	<img src="img.jpg"/>
     </a>
     ```

     ⑥锚点链接，当我们点击这个连接，可以快速定位到**页面中的某个位置**

     - 在锚点链接文本的href属性中，设置属性值为**#名字**的形式，如：

       ```html
       <a href="#two">第2集</a>
       ```

     - 找到目标位置标签，里面添加一个id属性=刚才的名字，如：
     
       ```html
       <h3 id="two">第2集介绍</h3>
       ```


## 五、HTML中的注释和特殊字符

1. 注释

   如果需要在HTML文档中添加一些便于阅读和理解但又不需要显示在页面中的注释文字，就需要使用注释标签。

   HTML中的注释以**"<!--"开头，以"-->"**结束。

   **快捷键ctrl+/**。

2. 特殊字符

   在HTML页面中，一些特殊的符号很难或者不方便直接使用，此时我们就可以使用下面的字符来替代：

   | 特殊字符 | 描述       | 字符代码    |
   | -------- | ---------- | ----------- |
   |          | **空格**   | **&nbsp ;** |
   | **<**    | **小于号** | **&lt ;**   |
   | **>**    | **大于号** | **&gt ;**   |
   | ￥       | 人民币     | &yen ;      |
   | &        | 和号       | &amp ;      |
   | ©        | 版权       | &copy ;     |
   | ®        | 注册商标   | &reg ;      |
   | °        | 角度       | &deg ;      |
   | ±        | 正负号     | &plusmn ;   |
   | ×        | 乘         | &times ;    |
   | ÷        | 除         | &divide ;   |
   | ²        | 平方       | &sup2 ;     |
   | ³        | 立方       | &sup3 ;     |

## 六、表格标签基本使用

- 表格的主要作用

  主要**用于显示、展示数据**，因为它可以让数据显示的非常规整，可读性好。特别是后台展示数据时，能够熟练运用表格就显得很重要。

- 表格的基本语法

  ```html
  <table>
      <tr>
  		<th>表头单元格内的文字</td>
  		...
  	</tr>
  	<tr>
  		<td>单元格内的文字</td>
  		...
  	</tr>
  	...
  </table>
  ```

  - table是用于定义表格的标签
  - **tr**(table row)标签用于定义表格中的**行**，必须嵌套在table标签中
  - **td**(table data)用于定义表格中的**单元格**，必须嵌套在tr标签中
  - **th**(table head)定义表格中的**表头单元格**，必须嵌套在tr标签中，位于表格的第一行或第一列，表头单元格里面的文本内容加粗居中显示

- 表格属性（了解，多在CSS中实现）

  | 属性名      | 属性值              | 描述                                                |
  | ----------- | ------------------- | --------------------------------------------------- |
  | align       | left、center、right | 规定表格相对周围元素的对齐方式                      |
  | border      | 1或""               | 规定表格单元是否拥有边框，默认为“”，表示没有边框    |
  | cellpadding | 像素点              | 规定单元边沿与其内容之间的空白（内边距），默认1像素 |
  | cellspacing | 像素点              | 规定单元格之间的空白（外边距），默认2像素           |
  | width       | 像素值或百分比      | 规定表格的宽度                                      |
  
- 表格结构标签

  使用场景：因为表格可能很长，为了更好地表示表格的语义，可以将表格分割成表格头部和表格主体两大部分。在表格标签中，分别用：<thead>标签表示表格的头部区域，<tbody>标签表示表格的主体区域，这样可以更好地分清表格结构。

  ```html
  <table border="1" cellspacing="0" cellpadding="5" width="600" align="center">
          <thead>
              <tr>
                  <!-- td*6+回车 -->
                  <th>排名</th>
                  <th>关键词</th>
                  <th>趋势</th>
                  <th>今日搜索</th>
                  <th>最近七日</th>
                  <th>相关链接</th>
              </tr>
          </thead>
          <tbody>
              <!-- tr*7>td*6+回车 -->
              <tr>
                  <td>1</td>
                  <td>鬼吹灯</td>
                  <td></td>
                  <td>345</td>
                  <td>12345</td>
                  <td>
                      <a href="#">贴吧</a>
                      <a href="#">图片</a>
                      <a href="#">百科</a>
                  </td>
              </tr>
              <tr>
                  <td>2</td>
                  <td>盗墓笔记</td>
                  <td></td>
                  <td>124</td>
                  <td>6754</td>
                  <td>
                      <a href="#">贴吧</a>
                      <a href="#">图片</a>
                      <a href="#">百科</a>
                  </td>
              </tr>
              <tr>
                  <td>3</td>
                  <td>西游记</td>
                  <td></td>
                  <td>212</td>
                  <td>7654</td>
                  <td>
                      <a href="#">贴吧</a>
                      <a href="#">图片</a>
                      <a href="#">百科</a>
                  </td>
              </tr>
              <tr>
                  <td>4</td>
                  <td>东游记</td>
                  <td></td>
                  <td>23</td>
                  <td>1244</td>
                  <td>
                      <a href="#">贴吧</a>
                      <a href="#">图片</a>
                      <a href="#">百科</a>
                  </td>
              </tr>
              <tr>
                  <td>5</td>
                  <td>甄嬛传</td>
                  <td></td>
                  <td>121</td>
                  <td>4332</td>
                  <td>
                      <a href="#">贴吧</a>
                      <a href="#">图片</a>
                      <a href="#">百科</a>
                  </td>
              </tr>
              <tr>
                  <td>6</td>
                  <td>水浒传</td>
                  <td></td>
                  <td>576</td>
                  <td>8689</td>
                  <td>
                      <a href="#">贴吧</a>
                      <a href="#">图片</a>
                      <a href="#">百科</a>
                  </td>
              </tr>
              <tr>
                  <td>7</td>
                  <td>三国演义</td>
                  <td></td>
                  <td>234</td>
                  <td>3456</td>
                  <td>
                      <a href="#">贴吧</a>
                      <a href="#">图片</a>
                      <a href="#">百科</a>
                  </td>
              </tr>
          </tbody>
      </table>
  ```

  ![image-20210705170240469](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210705170240469.png)

- 合并单元格

  特殊情况下，可以把多个单元格合并为一个单元格。

  - 合并单元格的方式：

    - 跨行合并：rowspan="合并单元格的个数"

    - 跨列合并：colspan="合并单元格的个数"

      ![image-20210705170723963](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210705170723963.png)

  - 目标单元格：（写合并代码）

    - 跨行：最上侧单元格为目标单元格，在此处写合并代码
    - 跨列：最左侧单元格为目标单元格，在此处写合并代码

  ```html
  <table width="300" border="1" cellspacing="0" cellpadding="20">
          <tr>
              <td></td>
              <td colspan="2"></td>
          </tr>
          <tr>
              <td rowspan="2"></td>
              <td></td>
              <td></td>
          </tr>
          <tr>
              <td></td>
              <td></td>
          </tr>
      </table>
  ```

  ![image-20210705171556376](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210705171556376.png)

## 七、列表标签基本使用

表格是用来展示数据的，**列表是用来布局的**。

根据列表的使用情景，列表可以分为三大类：**无序列表**、**有序列表**和**自定义列表**。

- **无序列表**

  **<ul>**标签表示HTML中项目的无序列表，一般会以项目符号呈现列表项，而列表项使用**<li>**定义。

  ```html
  <ul>
  	<li>列表项1</li>
  	<li>列表项2</li>
  	<li>列表项3</li>
  	...
  </ul>
  ```

- 有序列表

  有序列表即有排列顺序的列表，其各个列表项会按照一定的顺序排列定义。

  在HTML标签中，**<ol>**标签用于定义有序列表，列表排序以数字来显示，并且使用**<li>**标签来定义列表项。

  ```html
  <ol>
  	<li>列表项1</li>
  	<li>列表项2</li>
  	<li>列表项3</li>
  	...
  </ol>
  ```

- 自定义列表

  自定义列表的使用场景：

  自定义列表常用于对术语或名词进行解释和描述，定义列表的列表项钱没有任何项目符号

  ![image-20210706160025118](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210706160025118.png)

  ```html
  <dl>
  	<dt>名词1</dt>
  	<dd>名词解释1</dd>
  	<dd>名词解释2</dd>
  	...
  </dl>
  ```

## 八、表单标签基本使用

- 表单的作用：**收集用户信息**。

- 表单的组成：在HTML中，一个完整的表单通常由**表单域**、**表单控件（表单元素）**和**提示信息**3个部分组成。

  ![image-20210706161046054](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210706161046054.png)

  - **表单域**：

    表单域是一个**包含表单元素的区域**。

    在HTML标签中，**<form>**标签用于定义表单域，以实现用户信息的收集和传递。**<form>会把它范围内的表单元素信息提交给服务器。**

    ```html
    <form action="url地址" method="提交方式" name="表单域名称">
    	各种表单元素控件
    </form>
    ```

    | 属性   | 属性值   | 作用                                               |
    | ------ | -------- | -------------------------------------------------- |
    | action | url地址  | 用于指定接收并处理表单数据的服务器程序的url地址    |
    | method | get/post | 用于设置表单数据的提交方式，其取值为get或post      |
    | name   | 名称     | 用于指定表单的名称，以区分同一个页面中的多个表单域 |

  - **表单控件**：

    - **input**输入表单元素

      **input标签用于收集用户信息**。<input>标签中包含一个**type**属性，根据不同的type属性值，输入字段拥有多种形式（文本字段、复选框、掩码后的文本控件、单选按钮、按钮等）。

      ```html
      <input type="属性值"/>
      ```

      | 属性值       | 描述                                                         |
      | ------------ | ------------------------------------------------------------ |
      | button       | 定义可点击按钮（多数情况下，用于通过javascript启动脚本）     |
      | **checkbox** | 定义复选框                                                   |
      | file         | 定义输入字段和“浏览”按钮，供文件上传                         |
      | hidden       | 定义隐藏的输入字段                                           |
      | image        | 定义图像形式的提交按钮                                       |
      | **password** | 定义密码字段，该字段中的字符将被掩码                         |
      | **radio**    | 定义单选按钮                                                 |
      | **reset**    | 定义重置按钮，重置按钮会清除表单中的所有数据                 |
      | **submit**   | 定义提交按钮，提价哦按钮会把表单数据发送到服务器             |
      | **text**     | 定义单行的输入字段，用户可在其中输入文本，默认宽度为20个字符 |

      除type属性外，<input>标签还有很多其他属性，其常用属性如下：

      | 属性      | 属性值       | 描述                                              |
      | --------- | ------------ | ------------------------------------------------- |
      | **name**  | 由用户自定义 | 定义input元素的名称                               |
      | **value** | 由用户自定义 | 定义input元素的值（默认值/初始值/传递给后台的值） |
      | checked   | checked      | 规定此input元素首次加载时应当被选中               |
      | maxlength | 正整数       | 规定输入字段中的字符的最大长度                    |

      ```html
      <form action="xxx.php" method="POST">
              <!-- 文本框 -->
              用户名：<input type="text" name="username" maxlength="6" placeholder="请输入用户名"><br>
              <!-- 密码框 -->
              密码：<input type="password" name="password"><br>
              <!-- 单选按钮 单选按钮必须有相同的name才能实现单选 -->
              性别：男<input type="radio" name="sex" value="男" checked="checked">女<input type="radio" name="sex" value="女"><br>
              <!-- 复选框 -->
              爱好：吃饭<input type="checkbox" name="hobbiy" value="吃饭">睡觉<input type="checkbox" name="hobbiy" value="睡觉">打豆豆<input type="checkbox" name="hobbiy" value="打豆豆"><br>
      
              <!-- 提交按钮 -->
              <input type="submit" value="免费注册"><br>
              <!-- 重置按钮 -->
              <input type="reset" value="重新填写"><br>
      
              <!-- 普通按钮 -->
              <input type="button" value="获取短信验证码"><br>
              <!-- 文件按钮 -->
              上传头像：<input type="file"><br>
          </form>
      ```

      ![image-20210706171236271](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210706171236271.png)

      1. name和value是每个表单元素都有的属性值，主要给后台人员使用
      2. **要求单选按钮和复选框要有相同的name值**
      3. checked属性主要针对单选按钮和复选框，主要作用一打开页面，就要可以默认选中某个表单元素
      4. maxlength是用户可以在表单元素输入的最大字符数，一般较少使用

    - **label**标签

      **<label>**标签**为input元素定义标注**。

      **<label>标签用于绑定一个表单元素**，当点击<label>标签内的文本时，浏览器就会自动将焦点（光标）转到或者选择对应的表单元素上，用来增加用户体验。

      ```html
      <label for="sex">男</label>
      <input type="radio" name="sex" id="sex">
      ```

      label标签**for属性的值**需要与被绑定的input标签中**id属性的值**对应。

      对上面代码添加<label>标签：

      ```html
      <form action="xxx.php" method="POST">
              <!-- 文本框 -->
              <label for="username">用户名：</label>
              <input type="text" name="username" id="username" maxlength="6" placeholder="请输入用户名"><br>
              <!-- 密码框 -->
              <label for="password">密码：</label>
              <input type="password" name="password" id="password"><br>
              <!-- 单选按钮 单选按钮必须有相同的name才能实现单选 -->
              性别：
              <label for="male">男</label>
              <input type="radio" name="sex" id="male" value="男" checked="checked">
              <label for="female">女</label>
              <input type="radio" name="sex" id="female" value="女"><br>
              <!-- 复选框 -->
              爱好：
              <label for="eat">吃饭</label>
              <input type="checkbox" name="hobbiy" id="eat" value="吃饭">
              <label for="sleep">睡觉</label>
              <input type="checkbox" name="hobbiy" id="sleep" value="睡觉">
              <label for="dadoudou">打豆豆</label>
              <input type="checkbox" name="hobbiy" id="dadoudou" value="打豆豆"><br>
      
              <!-- 提交按钮 -->
              <input type="submit" value="免费注册"><br>
              <!-- 重置按钮 -->
              <input type="reset" value="重新填写"><br>
      
              <!-- 普通按钮 -->
              <input type="button" value="获取短信验证码"><br>
              <!-- 文件按钮 -->
              上传头像：<input type="file"><br>
          </form>
      ```

    - **select**下拉表单元素

      - 使用场景：在页面中如果有多个选项让用户选择，并且想要节约页面空间时，我们可以使用<select>标签控件定义下拉列表。

      ![image-20210709214056550](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210709214056550.png)

      - 语法：

        ```html
        <select>
        	<option>选项1</option>
        	<option>选项2</option>
        	<option>选项3</option>
        	...
        </select>
        ```

      - 注意：

        - select中至少包含一对option（一个选项）
        - 在<option>中定义**selected="selected"**，即默认选中此项

    - **textarea**文本域元素

      - 使用场景：当用户输入内容较多时，我们就不能再使用文本框控件了，在表单元素中，<textarea>标签是用于定义多行文本输入的控件。

      - 语法：

        ```html
        <textarea rows="3" cols="20">
        	文本内容
        </textarea>
        ```

        rows="显示的行数"

        cols="每行中的字符数"，**实际开发中不会使用，都是用CSS来改变文本域大小**


# CSS简介

**CSS**是**层叠样式表(Cascading Style Sheets)**的简称，有时我们也会称之为**CSS样式表**或**级联样式表**。

CSS是一种标记语言。

CSS主要用于设置HTM页面中的**文本内容**（字体、大小、对齐方式等）、**图片和外形**（宽高、边距样式、边距等）以及**版面的布局和外观显示样式**。

## 一、CSS语法规范

CSS规范由两个主要的部分构成：**选择器**以及**一条或多条声明**。

![image-20210709230257710](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210709230257710.png)

- 选择器是用于指定CSS样式的HTML标签，花括号内是对该对象设置的具体样式
- 属性和属性值以“键值对”的形式出现（**属性：属性值;**）
- 属性是对指定的对象设置的样式属性，例如字体大小、文本颜色等

```css
<head>
	<style>
		p{
			color:red;
			font-size:12px;
		}
	</style>
</head>
```

## 二、CSS代码风格

1. 样式格式书写：展开格式

2. 样式大小写风格：**样式选择器、属性名、属性值关键字全部使用小写字母**，特殊情况除外

3. 样式空格风格：

   - 属性值前面，冒号后面，保留一个空格
   - 选择器（标签）和大括号中间保留空格

   ```css
   h3 {
   	color: pink;
   	font-size: 20px;
   }
   ```

## 三、CSS基础选择器

1. CSS选择器的作用

   选择器就是根据需求**选择标签用的**。

2. 选择器分类

   - **基础选择器**

     - **标签选择器**

       标签选择器（元素选择器）是指用**HTML标签名**作为选择器，按标签名称分类，为页面中某一类标签指定统一的CSS样式。

       - 语法：

         ```css
         标签名 {
         	属性1: 属性值1;
         	属性2: 属性值2;
         	属性3: 属性值3;
         	...
         }
         ```

       - 作用：标签选择器可以把某一类标签全部选择出来，比如所有的<div>标签或所有的<span>标签
       - 优点：能快速为页面中同类型的标签统一设置样式

     - **类选择器**

       如果你想**差异化选择不同的标签**，**单独选择一个或某几个标签**，就可以使用类选择器。

       - 语法：

         ```css
         .类名 {
         	属性1: 属性值1;
             ...
         }
         ```

         结构需要用**class属性**来**定义类名**，长名称或词组可以用短横线来为选择器命名，如star-sing，不要使用纯数字、中文等命名，尽量使用英文字母来表示。

         ```css
         .red {
         	color: red;
         }
         ```

         ```html
         <div class="red">变红色</div>
         ```

       - 多类名：

         我们可以给一个标签定义**多个类名**，从而达到更多的选择目的。

         ```html
         <div class="red font20">亚瑟</div>
         ```

     - **id选择器**

       id选择器可以为标有特定id的HTML元素指定特定的样式。

       **HTML元素以id属性来设置id选择器，CSS中id选择器以"#"来定义。**

       - 语法：

         ```css
         #id名 {
         	属性1: 属性值1;
         	属性2: 属性值2;
         	...
         }
         ```

         id选择器口诀：样式#定义，结构id调用，**只能调用一次**，别人切勿使用。

       - id选择器和类选择器的区别

         - 类选择器(class)好比人的名字，一个人可以有多个名字，同时一个名字也可以被多个人使用；
         - id选择器(id)好比人的身份证，具有唯一性，不得重复；
         - 类选择器在修改样式中使用最多，id选择器一般用于页面唯一性的元素上，经常和javaScript搭配使用。

     - **通配符选择器**

       在CSS中，**通配符选择器使用"*"定义**，它镖师选取页面中**所有元素**（标签）。

       - 语法：

         ```css
         * {
         	属性1: 属性值1;
         	属性2: 属性值2;
         	...
         }
         ```

         清除所有元素标签的内外边距：

         ```css
         * {
         	margin: 0;
         	padding: 0;
         }
         ```

   - **复合选择器**


## 四、CSS字体属性

CSS Fonts（字体）属性用于定义字体系列、大小、粗细和文字样式（如粗细）。

1. **字体系列**

   CSS使用**font-family**属性定义文本的字体系列。

   ```css
   p {
   	font-family: "微软雅黑";
   }
   div {
   	font-family: "Arial","Microsoft Yahei","微软雅黑";
   }
   ```

   - 各种字体之间必须使用英文状态下的逗号隔开；
   - 一般情况下，如果有空格隔开的多个单词组成的字体，需要加引号；
   - 尽量使用系统默认的字体，保证在任何用户的浏览器中都能正确显示。
   - 最常见的几个字体：**body {font-family: "Microsoft Yahei",tahoma,Arial,"Hiragino Sans GB";}**。

2. **字体大小**

   CSS使用**font-size**属性定义字体大小。

   ```css
   p {
   	font-size: 20px;
   }
   ```

   - px（像素）大小是网页最常用的单位；
   - 谷歌浏览器默认的文字大小是16px；
   - 不同浏览器可能默认显示的字号大小不一致，因此我们尽量给一个明确大小，不依靠默认大小；
   - 可以**给body指定整个页面的文字大小**。

3. **字体粗细**

   CSS使用**font-weight**属性设置文本字体的粗细。

   ```css
   p {
   	font-weight: bold;
   }
   ```

   | 属性值  | 描述                                     |
   | ------- | ---------------------------------------- |
   | normal  | 默认值（不加粗）                         |
   | bold    | 加粗                                     |
   | 100-900 | **400（normal），700（bold）后不跟单位** |

4. **文字样式**

   CSS使用**font-style**属性设置文本的风格。

   ```css
   p {
   	font-style: normal;
   }
   ```

   | 属性值 | 描述   |
   | ------ | ------ |
   | normal | 默认值 |
   | italic | 斜体   |

   让倾斜的字体不倾斜：

   ```css
   em,i {
   	font-style: normal;
   }
   ```

5. **字体复合属性**

   可以将以上文字样式综合来写，节约代码。

   ```css
   body {
   	font: font-style font-weight font-size/line-height font-family;
   }
   ```

   例如：

   ```css
   body {
   	font: italic 700 16px 'Microsoft yahei';
   }
   ```

   - 使用font属性时，必须按上面语法格式中的顺序书写，**不能更换顺序**，并且各个属性间以**空格隔开**；
   - 不需要设置的属性可以省略取默认值，但**必须保留font-size和font-family属性**，否则font复合属性将不起作用。


## 五、CSS文本属性

CSS Text（文本）属性克定义文本的外观，比如文本的颜色、对齐文本、装饰文本、文本缩进、行间距等。

1. **文本颜色**

   **color**属性用于定义文本的颜色。

   ```css
   div {
   	color: red;
   }
   ```

   | 表示           | 属性值                        |
   | -------------- | ----------------------------- |
   | 预定义的颜色值 | red,green,......              |
   | 十六进制       | #ff0000,#ff6600,#29d794       |
   | RGB代码        | rgb(255,0,0)或rgb(100%,0%,0%) |

2. **对齐文本**

   **text-align**属性用于设置元素内文本内容的水平对齐方式。

   ```css
   div {
   	text-align: center;
   }
   ```

   | 属性值 | 说明           |
   | ------ | -------------- |
   | left   | 左对齐（默认） |
   | center | 居中           |
   | right  | 右对齐         |

3. **装饰文本**

   **text-decoration**属性规定添加到文本的修饰，可以给文本添加下划线、删除线、上划线等。

   ```css
   div {
   	text-decoration: underline;
   }
   ```

   | 属性值       | 说明                    |
   | ------------ | ----------------------- |
   | none         | 没有装饰线（默认）      |
   | underline    | 下划线，链接a自带下划线 |
   | overline     | 上划线                  |
   | line-through | 删除线                  |

4. **文本缩进**

   **text-indent**属性用来指定文本的第一行的缩进，通常是将段落的首行缩进。

   ```css
   div {
   	text-indent: 20px;
   }
   ```

   缩进长度可以取负值。

   ```css
   p {
   	text-indent: 2em;
   }
   ```

   **em是一个相对单位**，就是**当前元素(font-size)1个文字的大小**，如果当前元素没有设置大小，则会按照父元素的1个文字大小。

5. **行间距**

   **line-height**属性用来设置段落内行间距（行高）。

   ```css
   p {
   	line-height: 26px;
   }
   ```

   ![image-20210714180942340](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210714180942340.png)

## 六、CSS的引入方式

1. CSS的三种样式表

   按照CSS样式**书写的位置**（或者引入的方式），CSS样式表可以分为三大类：

   - 行内样式表（行内式）
   - 内部样式表（嵌入式）
   - 外部样式表（链接式）

2. **内部样式表**

   内部样式表（内嵌样式表）是写到HTML页面内部，将所有的CSS代码抽取出来，单独放到一个<style>标签中。

   ```css
   <style>
   	div {
   		color: red;
   		font-size: 12px;
   	}
   </style>
   ```

   - 通过此种方式，可以方便地控制当前整个页面中的元素样式设置
   - 代码结构清晰，但是并没有实现结构与样式分离

3. **行内样式表**

   行内样式表（内联样式表）是**在元素标签内部的style属性中设定CSS样式**。适合修改简单样式。

   ```html
   <div style="color: red;font-size: 12px;">青春不常在</div>
   ```

   - style其实就是标签的属性
   - 可以控制当前的标签设置样式

4. **外部样式表**

   将**样式单独写到CSS文件**中，之后把CSS文件引入到HTML页面中使用。实际开发中都是使用外部样式表，适合于样式较多的情况。

   外部样式表引入：

   1. 新建一个后缀名为**.css**的样式文件，把所有CSS代码放入其中；

   2. 在HTML页面中，使用<link>标签引入文件。

      ```html
      <link rel="stylesheet" href="css文件夹路径">
      ```

## 七、Chrome调试工具

1. **Ctrl+滚轮**可以放大或缩小开发者工具代码的大小；
2. 左边是HTML元素结构，右边是CSS样式；
3. 右边CSS样式可以改动数值（左右箭头或者直接输入）和查看颜色；
4. **Ctrl+0**复原浏览器大小；
5. 如果点击元素，发现**右侧没有样式引入**，极有可能是**类名或者样式引入错误**；
6. 如果有样式，但是样式前面有**黄色感叹号**提示，则是**样式属性书写错误**。

# CSS基础

## 一、Emmet语法

Emmet语法的前身是Zen coding，它使用缩写来提高HTML/CSS的编写速度，VsCode内部已经集成了该语法。

1. 快速生成HTML结构语法

   - 生成标签：直接输入标签名按**Tab键**，如div+Tab键，直接生成<div></div>

   - 生成多个相同标签：如**div*3**，直接生成3个<div></div>

   - 生成父子关系标签：如**ul>li**，生成<ul><li></li></ul>

   - 生成兄弟关系标签：如**div+p**，生成<div></div><p></p>

   - 生成带类名或id名的标签：如**.demo，#two**，生成<div class="demo"></div>及 <div id="two"></div>

   - 自增符号：**$**，如.demo$*5，生成

     ```html
     <div class="demo1"></div>
     <div class="demo2"></div>
     <div class="demo3"></div>
     <div class="demo4"></div>
     <div class="demo5"></div>
     ```

   - 在生成的标签内部写内容：使用**{}**表示，如div{此地无银三百两}，生成<div>此地无银三百两</div>；div{$$}*5，生成

     ```html
     <div>01</div>
     <div>02</div>
     <div>03</div>
     <div>04</div>
     <div>05</div>
     ```

2. 快速生成CSS样式语法

   CSS基恩采取**简写**形式即可：

   1. 比如w200按tab键，即可生成width: 200px;
   2. 比如lh26按tab键，即可生成line-height: 26px;
   3. 比如tac按tab键，即可生成text-align: center;
   4. 比如ti2em按tab键，即可生成text-indent: 2em;
   5. 比如tdn按tab键，即可生成text-decoration: none;
   
3. 快速格式化代码

   - 快捷键：Shift+Alt+F

   - 设置保存页面时自动格式化代码：

     1. 文件---->首选项---->设置；

     2. 搜索emmet.include;

     3. 在settings.json下的用户中添加以下语句：

        ```
        "editor.formatOnType":true,
        "editor.formatOnSave":true
        ```

     新版本：

     ![image-20210718173129718](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210718173129718.png)

## 二、CSS选择器

- **后代选择器**

  后代选择器又称为**包含选择器**，可以选择父元素里面的子元素，其写法就是**把外层标签写在前面，内层标签写在后面，中间用空格分隔**。当标签发生嵌套时，内层标签就称为外层标签的后代。

  - 语法：

    ```css
    元素1 元素2 {
    	样式声明
    }
    ```

    上述语法表示选择**元素1里面的所有元素2**（后代元素）

    ```html
    <ol>
    	<li>我是ol的孩子</li>
    	<li>我是ol的孩子</li>
    	<li>我是ol的孩子</li>
    </ol>
    <ul>
        <li>我是ul的孩子</li>
        <li>我是ul的孩子</li>
        <li>我是ul的孩子</li>
    </ul>
    ```

    ```css
    ol li {
    	color: pink;
    }
    ```

    ![image-20210719180638677](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210719180638677.png)

  - 注意：

    - 元素1和元素2中间用**空格隔开**；
    - 元素1是父级，元素2是子级，最终选择的是元素2；
    - 元素2可以是儿子，也可以是孙子等，只要是元素1的**后代即可**；
    - 元素1和元素2**可以是任意基础选择器**。

- **子选择器**

  又称为子元素选择器，只能**选择作为某元素的最近一级子元素**。简单理解就是选亲儿子元素。

  - 语法：

    ```css
    元素1>元素2 {
    	样式声明
    }
    ```

    表示选择元素1里面的**所有直接后代（子元素）元素2**。

    ```html
    <div>
    	<a href="#">我是儿子</a>
    	<p>
        	<a href="#">我是孙子</a>
        </p>
    </div>
    ```

    ```css
    ol li {
    	color: pink;
    }
    ```

    ![image-20210719180722917](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210719180722917.png)

    对比后代选择器：

    ```css
    div a {
    	color: pink;
    }
    ```

    ![image-20210719181008648](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210719181008648.png)

  - 注意：

    - 元素1和元素2用**大于号**隔开；
    - 元素1是父级，元素2是子级，最终选择的是元素2；
    - 元素2**必须是亲儿子**，孙子、重孙之类都不归他

- **并集选择器**

  并集选择器可以选择多组标签，同时为他们定义相同的样式。通常用于集体声明。

  并集选择器是各选择器通过**英文逗号**连接而成，任何形式的选择器都可以作为并集选择器的一部分。

  - 语法：

    ```css
    元素1,元素2 {
    	样式声明
    }
    ```

    表示选择**元素1和元素2**。

    ```html
    <div>熊大</div>
    <p>熊二</p>
    <span>光头强</span>
    <ul class="pig">
    	<li>小猪佩奇</li>
    	<li>猪爸爸</li>
    	<li>猪妈妈</li>
    </ul>
    ```

    ```css
    div,
    p,
    .pig li {
    	color: pink;
    }
    ```

    ![image-20210719181753611](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210719181753611.png)

  - 注意：

    - 元素1和元素2中间用**逗号隔开**；
    - 逗号可以理解为**和**的意思；
    - 并集选择器通常用于集体声明。

- **伪类选择器**

  用于向某些选择器添加特殊效果，比如给链接添加特殊效果，或选择第1、第n个元素。

  伪类选择器书写最大的特点是用冒号（:）表示，比如:hover、:first-child。

  - 链接伪类选择器

    ```css
    a:link	//选择所有未被访问的链接
    a:visited	//选择所有已被访问的链接
    a:hover	//选择鼠标指针位于其上的链接
    a:active	//选择活动链接（鼠标按下还未弹起时）
    ```

    - 注意：

      - 为了确保生效，请按照**LVHA**的顺序声明：**:link,:visited,:hover,:active**
      - 记忆法：love hate或LV包包hao
      - 因为**a链接在浏览器中具有默认样式**，所以在实际工作中**需要给链接单独指定样式**

    - 链接伪类选择器实际工作开发中的写法

      ```css
      a {
      	color: #333;
          text-decoration: none;
      }
      a:hover {
      	color: #369;
      }
      ```

  - ：focus伪类选择器

    用于选取**获得焦点的表单元素**。

    焦点就是光标，一般情况**<input>类表单元素**才能获取，因此这个选择器也主要针对于表单元素来说。

    ```css
    input:focus {
    	background-color: yellow;
    }
    ```

    ![image-20210722180148070](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210722180148070.png)

## 三、CSS元素显示模式

元素显示模式就是元素（标签）以什么方式进行显示，比如<div>自己独占一行，一行可以放多个<span>。

HTML元素一般分为**块元素**和**行内元素**两种类型。

1. **块元素**

   常见的块元素有<h1>-<h6>、<p>、<div>、<ul>、<ol>、<li>等，其中**<div>**标签是**最典型的块元素**。

   - 特点：
     - **独占一行**；
     - 高度、宽度、外边距以及内边距都可以控制；
     - **宽度默认是容器（父级宽度）的100%**；
     - 是一个**容器盒子**，里面可以放行内或块级元素。
   - 注意：
     - **文字类的元素内不能使用块元素**；
     - < p >标签主要用于存放文字，因此标签内不能放块级元素，特别是不能放< div >；
     - 同理，<h1>-<h6>等都是文字类块级元素，里面也不能放其他块级元素。

2. **行内元素**

   常见的行内元素有<a>、<strong>、<b>、<em>、<i>、<del>、<s>、<ins>、<u>、<span>等，其中**<span>**标签是**最典型的行内元素**。有点地方也将行内元素称为**内联元素**。

   - 特点：

     - 相邻行内元素在一行上，一行可以显示多个；
     - **高、宽直接设置是无效的**；
     - **宽度默认就是它本身内容的宽度**；
     - 行内元素只能容纳文本或其他行内元素。

   - 注意：

     - 链接内不能再放链接；

     - **特殊情况链接<a>中可以放块级元素**，但是给<a>转换一下块级模式最安全

       ![image-20210722185155916](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210722185155916.png)

3. **行内块元素**

   在行内元素中有几个特殊的标签：**<img>、<input>、<td>**，他们**同时具有块元素和行内元素的特点**。

   - 特点：
     - 和相邻行内元素（行内块）在一行上，但是他们之间会有**空白缝隙**，**一行可以显示多个**（行内元素特点）；
     - 默认宽度就是它本身内容的宽度（行内元素特点）；
     - **高度、外边距以及内边距都可以控制**（块级元素特点）。

4. **元素显示模式转换**

   特殊情况：我们需要元素模式转换（一个模式的元素需要另一种模式的特性），比如想要增加链接<a>的触发范围。

   - **转换为块元素：display: block;**
   - **转换为行内元素：display: inline;**
   - **转换为行内块元素：display: inline-block;**

5. **单行文字垂直居中**

   - 解决方法：

     **让文字的行高等于盒子的高度**，就可以让文字在当前盒子内垂直居中。

     ![image-20210723175659209](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210723175659209.png)

     

     ```html
     <!DOCTYPE html>
     <html lang="en">
     
     <head>
         <meta charset="UTF-8">
         <meta http-equiv="X-UA-Compatible" content="IE=edge">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>Document</title>
         <style>
             div {
                 width: 270px;
                 height: 315px;
                 background-color: #535759;
             }
     
             a {
                 display: block;
                 text-decoration: none;
                 color: #FFFFFF;
                 font-size: 14px;
                 height: 45px;
                 text-indent: 2em;
                 /* 使文字行高等于盒子高度 */
                 line-height: 45px;
             }
     
             a:hover {
                 background-color: #FF7000;
             }
         </style>
     </head>
     
     <body>
         <div>
             <a href="#">手机 电话卡</a>
             <a href="#">电视 盒子</a>
             <a href="#">笔记本 平板</a>
             <a href="#">出行 穿戴</a>
             <a href="#">智能 路由器</a>
             <a href="#">健康 儿童</a>
             <a href="#">耳机 音响</a>
         </div>
     </body>
     
     </html>
     ```

     ![image-20210723180027116](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210723180027116.png)

   - 原理：

     ![image-20210723180252235](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210723180252235.png)

## 四、CSS背景

通过CSS背景属性，可以给页面元素添加背景样式。

1. **背景颜色**

   **background-color**属性定义了元素的背景颜色。

   ```css
   background-color: 颜色值;
   ```

   一般情况下，元素背景颜色的默认值是**transparent**（透明），我们也可以手动指定背景颜色为透明色。

2. **背景图片**

   **background-image**属性描述了元素的背景图像。实际开发常见于**logo**或者是一些**装饰性的小图片**、**超大的背景图片**。优点是非常便于控制位置。

   ```css
   background-image: none | url(url地址);
   ```

3. **背景平铺**

   如果需要在HTML页面上对背景图像进行平铺，可以使用**background-repeat**属性。

   ```css
   background-repeat: repeat | no-repeat | repeat-x | repeat-y;
   ```

   - repeat：在纵向和横向上面平铺（默认）；

     ![image-20210723181734283](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210723181734283.png)

   - no-repeat：不平铺；

     ![image-20210723181759682](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210723181759682.png)

   - repeat-x：沿x轴平铺；

     ![image-20210723181626617](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210723181626617.png)

   - repeat-y：沿y轴平铺。

     ![image-20210723181645277](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210723181645277.png)

4. **背景图片位置**

   利用**background-position**属性可以改变图片在背景中的位置。

   ```css
   background-position: x y;
   ```

   参数代表的意思：x坐标和y坐标。可以使用**方位名词**或者**精确单位**。

   | 参数值   | 说明                                                        |
   | -------- | ----------------------------------------------------------- |
   | length   | 百分数 \| 由浮点数字和单位标识符组成的长度值                |
   | position | top \| center \| bottom \| left \| center \| right 方位名词 |

   ```css
   background-position: center right;
   ```

   注意：

   1. 参数是方位名词
      - 如果指定的两个值都是方位名词，则两个值前后顺序无影响。比如left top和top left效果等价；
      - 如果只指定了一个方位名词，另一个值省略，则第二个值默认居中对齐。
   2. 参数是精确单位
      - 如果参数值是精确坐标，那么第一个肯定是x坐标，第二个为y坐标；
      - 若仅指定一个数值，那被指定的就是x坐标，y轴默认垂直居中。
   3. 参数是混合单位
      - 精确单位和方位名词可以混合使用，同样是第一个指定x，第二个指定y

5. **背景图像固定（背景附着）**

   **background-attachment**属性设置背景图像是否固定或者随页面的其余部分滚动。

   background-attachment后期可以用来制作**视差滚动**的效果。

   ```css
   background-attachment: scroll | fixed
   ```

   | 参数   | 作用                     |
   | ------ | ------------------------ |
   | scroll | 背景图像是随对象内容滚动 |
   | fixed  | 背景图像固定             |

6. **背景属性复合写法**

   为了简化背景属性的代码，可以将这些属性合并简写在同一个属性**background**中。

   ```css
   background: 背景颜色 背景图片地址 背景平铺 背景图像固定 背景图片位置;
   ```

   ```css
   background: transparent url(iamge.jpg) repeat-y fixed top;
   ```

7. **背景色半透明**

   ```css
   background: rgba(0, 0, 0, 0.3);
   ```

   r:red	g:green	b:blue	a:alpha

   alpha不透明度，取值范围在0~1之间

## 五、CSS三大特性

1. **层叠性**

   相同选择器对相同的样式进行设置，此时一个样式就会**覆盖（层叠）**另一个冲突的样式。层叠性主要解决样式冲突的问题。

   层叠性原则：

   - 样式冲突：遵循**后来居上**；
   - 样式不冲突：不会层叠（覆盖）。

2. **继承性**

   子标签会继承父标签的某些样式，比如文本颜色和字号。

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
       <style>
           div {
               color: pink;
               font-size: 14px;
           }
       </style>
   </head>
   
   <body>
       <div>
           龙生龙，凤生凤，
           <p>老鼠的儿子会打洞。</p>
       </div>
   </body>
   
   </html>
   ```

   ![image-20210727165031044](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210727165031044.png)

   - 恰当地使用继承可以简化代码，降低CSS样式的复杂性；
   - 子元素可以继承父元素的样式**（text-、font-、line-，以及color文字相关的属性）**

   

   **行高的继承性**

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
       <style>
           body {
               color: pink;
               font-size: 14px;
               font-family: 'Microsoft YaHei';
               /* 表示当前文字元素的1.5倍 */
               line-height: 1.5;
           }
   
           div {
               font-size: 16px;
               /* div行高：16*1.5=24px */
           }
       </style>
   </head>
   
   <body>
       <div>龙生龙，凤生凤，</div>
       <!-- p行高：14*1.5=21px -->
       <p>老鼠的儿子会打洞。</p>
   </body>
   
   </html>
   ```

   ![image-20210727165958327](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210727165958327.png)

   ![image-20210727170211290](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210727170211290.png)

   body行高1.5这样的写法最大的优势就是：子元素可以根据自己的文字大小自动调节行高。

3. **优先级**

   当同一个元素被多个选择器指定，就会有优先级产生。

   - 选择器相同：执行层叠；

   - 选择器不同：根据**选择器权重**执行。

     | 选择器               | 选择器权重 |
     | -------------------- | ---------- |
     | 继承 或 *            | 0,0,0,0    |
     | 元素选择器           | 0,0,0,1    |
     | 类选择器，伪类选择器 | 0,0,1,0    |
     | ID选择器             | 0,1,0,0    |
     | 行内样式style=""     | 1,0,0,0    |
     | !important 重要的    | ∞无穷大    |

     **“范围”越小，权重越大。**

   **权重叠加**：如果是复合选择器，则会有权重叠加，需要计算权重。**（权重虽然会叠加，但不会有进位）**

   ![image-20210727175743219](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210727175743219.png)

# CSS盒子模型

## 一、盒子模型

1. 网页布局的本质

   ![image-20210728180852943](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210728180852943.png)

2. 盒子模型（Box Model）组成

   **盒子模型**：把HTML页面中的布局元素看做是一个矩形的盒子，也就是一个盛装内容的容器。

   **CSS盒子模型**本质上是一个盒子，封装周围的HTML元素，它包括：**边框**、**外边距**、**内边距**和实际**内容**。

   ![image-20210728181446536](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210728181446536.png)

   ![image-20210728181508423](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210728181508423.png)

3. **边框（border）**

   border可以设置元素的边框。边框由边框宽度（**粗细**）、边框**样式**以及边框**颜色**组成。

   语法：

   ```css
   border: border-width || border-style || border-color
   ```

   | 属性         | 作用               |
   | ------------ | ------------------ |
   | border-width | 边框粗细，单位是px |
   | border-style | 边框样式           |
   | border-color | 边框颜色           |

   - border-width

     ```css
     border-width: 5px;
     ```

   - border-style

     ```css
     border-style: none | hidden | dotted | dashed |solid | double | groove | ridge |inset | outset;
     ```

     | 参数       | 说明                                                         |
     | ---------- | ------------------------------------------------------------ |
     | none       | 无边框，与任何指定的border-width值无关                       |
     | hidden     | 隐藏边框，IE不支持                                           |
     | **dotted** | 在MAC平台上IE4+、WINDOWS和UNIX平台上IE5.5+为**点线**，否则为实线 |
     | **dashed** | 在MAC平台上IE4+、WINDOWS和UNIX平台上IE5.5+为**虚线**，否则为实线 |
     | **solid**  | **实线边框**                                                 |
     | double     | 双线边框，两条单线与其间隔的和等于border-width值             |
     | groove     | 根据border-color的值画3D凹槽                                 |
     | ridge      | 根据border-color的值画菱形边框                               |
     | inset      | 根据border-color的值画3D凹边                                 |
     | outset     | 根据border-color的值画3D凸边                                 |

     ![image-20210728182855875](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210728182855875.png)

   - border-color

     ```css
     border-color: pink;
     ```

   边框的复合写法：

   ```css
   /* 没有顺序 */
   border: 1px solid red;
   ```

   边框的分开写法：

   ```css
   /* 只设定上边框，其余同理 */
   border-top: 1px solid red;
   ```

   - border-collapse

     表格的细线边框

     **border-collapse**属性控制浏览器绘制表格边框的方式。它控制相邻单元格的边框。

     语法：

     ```css
     border-collapse: collapse;
     ```
     - collapse：合并
     - border-collapse: collapse;**合并相邻的边框**

   边框会影响盒子的实际大小

   解决方案：

   - 测量盒子大小的时候不量边框；
   - 如果测量的时候包含了边框，则需要width/height减去边框宽度

4. **内边距（padding）**

   **padding**属性用于设置内边距，即**边框与内容之间的距离**。

   | 属性           | 作用     |
   | -------------- | -------- |
   | padding-left   | 左内边距 |
   | padding-right  | 右内边距 |
   | padding-top    | 上内边距 |
   | padding-bottom | 下内边距 |

   内边距的复合写法：

   | 值的个数                     | 表达意思                                                     |
   | ---------------------------- | ------------------------------------------------------------ |
   | padding: 5px;                | 表示上下左右都有5像素内边距；                                |
   | padding: 5px 10px;           | 表示上下内边距都是5像素，左右为10像素；                      |
   | padding: 5px 10px 20px;      | 表示上内边距为5像素，左右内边距10像素，下内边距20像素；      |
   | paddign: 5px 10px 20px 30px; | 表示上内边距5像素，右内边距10px，下内边距20px，左内边距30px，**顺时针** |

   注意：
   
   如果**盒子已经有了宽度和高度**，此时**再指定内边距**，会**撑大盒子**。
   
   解决方案：
   
   为保证盒子跟效果图大小一致，需要**将width/height减去多出来的内边距大小**。
   
   
   
   如果**盒子本身没有指定width/height属性**，则此时**padding不会撑开盒子大小**。
   
5. **外边距（margin）**

   **margin**属性用于设置外边距（盒子与盒子之间的距离）。

   | 属性          | 作用     |
   | ------------- | -------- |
   | margin-left   | 左外边距 |
   | margin-right  | 右外边距 |
   | margin-top    | 上外边距 |
   | margin-bottom | 下外边距 |

   **margin的复合写法跟padding完全一致。**

   - **外边距典型应用：让块级盒子水平居中**

     1. 盒子**指定宽度**(width)；
     2. 盒子**左右的外边距设置为auto**。

     ```css
     .header {
     	background-color: pink;
     	width: 500px;
         height: 200px;
         margin: 0 auto;
     }
     ```

     ![image-20210811191158914](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210811191158914.png)

     注意：以上方法是让块级元素水平居中，**行内元素或行内块元素居中采用给其父元素添加text-align: center的方法即可**。

     ```css
     .header {
     	background-color: pink;
     	width: 500px;
     	height: 200px;
     	margin: 0 auto;
     	
     	text-align: center;
     }
     ```

     ![image-20210811191553057](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210811191553057.png)

   - **外边距合并**

     使用margin定义块元素的**垂直外边距**时，可能会出现外边距的合并。

     1. **相邻块元素垂直外边距的合并**

        当上下相邻的两个块元素（兄弟关系）相遇时，如果上面的元素有下外边距margin-bottom，下面的元素有上外边距margin-top，则他们之间的**垂直间距不是margin-bottom与margin-top的合**，而是**取两个值中的较大者**。

        ![image-20210811194648974](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210811194648974.png)

        解决方案：

        尽量只给一个盒子添加margin值。

     2. **嵌套块元素垂直外边距的塌陷**

        对于两个嵌套关系（父子关系）的块元素，**父元素有上外边距同时子元素也有上外边距**，此时**父元素会塌陷较大的外边距值**。

        ![image-20210811195128492](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210811195128492.png)

        解决方案：

        1. 为父元素定义上边框；

        2. 为父元素定义上内边距；

        3. 为父元素添加overflow:hidden。

           ```css
           border: 1px solid transparent; 
           padding-top: 20px; 
           overflow: hidden;	/* 溢出隐藏 */
           ```

6. **清除网页元素的内外边距**

   ```css
   * {
   	padding:0;	/*清除内边距*/
   	margin:0;	/*清除外边距*/
   }
   ```

   **注意：行内元素为了照顾兼容性，尽量值设置左右内外边距**，不设置上下内外边距（不起效果）。但是转换为块级和行内元素就可以了。

## 二、PS基本操作

- **文件→打开**，打开要测量的图片；
- **ctrl+R**，调出标尺，或**视图→标尺**；
- 右击标尺，将单位改为**像素**；
- **ctrl+加号(+)/alt+上滚轮**放大视图，**ctrl+减号(-)/alt+下滚轮**缩小视图；
- **按住空格键**，鼠标变为抓手工具，拖动PS视图；
- 利用**选区工具**，可以测量大小；
- **ctrl+D**或者**点击旁边空白区**都可以取消选区。

![image-20210812190835471](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210812190835471.png)

## 三、圆角边框

在CSS3中，新增了**圆角边框**样式。

**border-radius**属性用于设置元素的边框圆角。

语法：

```css
border-radius: length;
```

- radius：半径；

- 原理：**（椭）圆与边框相切的交集形成圆角效果**。

  ![image-20210814161615566](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210814161615566.png)

- 参数值可以为**数值**或**百分比**的形式；

- **圆形**的做法：需要一个**正方形**盒子，把数值修改为高度或宽度的一半即可，或直接写为**50%**；

- 圆角矩形的做法：**长方形**盒子，将数值修改为**高度的一半**；

  ![image-20210814162316919](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210814162316919.png)

- 该属性是一个简写属性，实际上可以跟四个数值，分别代表**左上角、右上角、右下角、左下角**；跟两个数值，分别代表左上右下、右上左下（对角线）；

- 四个角可以分开写：border-top-left-radius、border-top-right-radius、border-bottom-right-radius和border-bottom-left-radius。

## 四、盒子阴影

我们可以使用**box-shadow**属性为盒子添加阴影。

```css
box-shadow: h-shadow v-shadow blur spread color inset;
```

| 值           | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| **h-shadow** | 必须。水平阴影的位置，允许负值                               |
| **v-shadow** | 必须。垂直阴影的位置，允许负值                               |
| blur         | 可选。模糊距离                                               |
| spread       | 可选。阴影的尺寸                                             |
| color        | 可选。阴影的颜色，参阅CSS颜色值。rgba(0, 0, 0, .3)半透明效果 |
| inset        | 可选。将外部阴影(outset)改为内部阴影                         |

注意：

1. **默认**是**外阴影(outset)**，但是**不可以写**这个单词，否则就会导致阴影无效；
2. 盒子**阴影不占用空间**，不会影响其他盒子的排列。

## 五、文字阴影

在CSS3中，我们可以使用**text-shadow**属性将阴影应用于文本。

语法：

```css
text-shadow: h-shadow v-shadow blur color;
```

| 值           | 描述                            |
| ------------ | ------------------------------- |
| **h-shadow** | 必须。水平阴影的位置，允许负值  |
| **v-shadow** | 必须。垂直阴影的位置，允许负值  |
| blur         | 可选。模糊的距离                |
| color        | 可选。阴影的颜色，参阅CSS颜色值 |

# CSS浮动

## 一、浮动

1. 传统网页布局的三种方式

   - **标准流（普通流/文档流）**

     所谓标准流，就是标签按照规定好的默认方式排列：

     - 块级元素独占一行，从上向下顺序排列；
     - 行内元素从左到右顺序排列，碰到腹肌元素边缘则自动换行。

   - **浮动**

     浮动可以改变元素标签默认的排列方式，浮动的典型应用：**让多个块级元素一行内排列显示**。

     网页布局第一准则：**多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动**；

     网页布局第二准则：**先设置盒子大小，再设置盒子位置**。

   - **定位**

2. **浮动**

   - 定义：**float**属性用于创建浮动框，将其移动到一边，**直到触及左边缘或右边缘包含块或另一个浮动框的边缘**。

   - 语法：

     ```css
     选择器 {
     	float: 属性值;
     }
     ```

     | 属性值 | 描述                   |
     | ------ | ---------------------- |
     | none   | 元素不浮动（**默认**） |
     | left   | 元素向左浮动           |
     | right  | 元素向右浮动           |

   - **浮动特性**：

     - 浮动元素会脱离标准流（**脱标**），浮动的盒子**不再保留原先的位置**，原先的位置让其他的标准流盒子占有，类似于word中浮于文字上方的效果；

       ![image-20210819180236023](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210819180236023.png)

     - 浮动元素会**一行内显示并且顶部对齐**；

       ![image-20210819180357250](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210819180357250.png)

       注意：浮动元素是互相贴靠在一起的，但如果父级宽度装不下这些浮动盒子，多出的盒子就会另起一行对齐

     - 浮动元素会具有行内块元素的特性。

       任何元素都可以设置浮动，添加浮动之后具有**行内块元素**相似的特性。

   - **浮动元素与标准流父级搭配使用**

     为了约束浮动元素位置，我们在网页布局中一般采取的策略是：

     **先用标准流父级排列上下位置，之后内部子元素采取浮动排列左右位置**，复合网页布局第一准则。

     ![image-20210819181358583](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210819181358583.png)



## 二、常见网页布局

1. 常见网页布局

   ![image-20210821195626767](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210821195626767.png)

   ![image-20210821195710008](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210821195710008.png)

   ![image-20210821195753446](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210821195753446.png)

2. 浮动布局注意点

   - 浮动和标准流的父盒子搭配：**先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置。**
   - 一个元素浮动了，理论上其余的兄弟元素也要浮动：一个盒子里面有多个盒子，如果其中一个盒子浮动了，那么其他兄弟也应该浮动，以防引起问题。**浮动的盒子只会影响浮动盒子后面的标准流，不会影响前面的标准流（前面的盒子独占一行）。**

## 三、清除浮动

1. 为什么要清除浮动

   由于父级盒子很多情况下，不方便给高度，但是子盒子浮动又不占有位置，最后父级盒子高度为0时，就会影响下面的标准流盒子。

   ![image-20210829180946122](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210829180946122.png)

2. 清除浮动的本质

   清除浮动的本质是**清除浮动元素造成的影响**。

   如果父盒子本身有高度，则不需要清除浮动。

   **清除浮动之后，父级就会根据浮动的子盒子自动检测高度，父级有了高度就不会影响下面的标准流了。**

3. 清除浮动

   语法：

   ```css
   选择器{
   	clear: 属性值;
   }
   ```

   | 属性值 | 描述                                       |
   | ------ | ------------------------------------------ |
   | left   | 不允许左侧有浮动元素（清除左侧浮动的影响） |
   | right  | 不允许右侧有浮动元素（清除右侧浮动的影响） |
   | both   | 同时清除左右两侧浮动的影响                 |

   实际工作中几乎只用**clear: both;**

   清除浮动的策略：**闭合浮动**。

4. 清除浮动方法

   - **额外标签法**，也成为隔墙法；
   - 父级添加overflow属性；
   - 父级添加after属性；
   - 父级添加双伪元素

5. **额外标签法**

   额外标签法会在浮动元素末尾添加一个空的标签，例如<div style="clear: both" ></div>，或者其他标签（如< br/>等）。

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
       <style>
           .box {
               width: 800px;
               background-color: blue;
           }
   
           .damao {
               width: 200px;
               height: 200px;
               float: left;
               background-color: black;
           }
   
           .ermao {
               width: 400px;
               height: 400px;
               float: left;
               background-color: pink;
           }
   
           .clear {
               clear: both;
           }
   
           .footer {
               width: 800px;
               height: 100px;
               background-color: yellow;
           }
       </style>
   </head>
   
   <body>
       <div class="box">
           <div class="damao">大毛</div>
           <div class="ermao">二毛</div>
           <!-- 隔墙 -->
           <div class="clear"></div>
       </div>
       <div class="footer"></div>
   </body>
   
   </html>
   ```

   - 优点：通俗易懂、书写方便；
   - 缺点：添加许多无意义标签，结构较差。
   - 注意：添加的标签必须是**块级元素**。

6. **给父级添加overflow**

   可以给父级添加overflow属性，将其属性值设置为**hidden**、**auto**或**scroll**。

   overflow: hidden; 意思是溢出隐藏。

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
       <style>
           .box {
               /* 清除浮动 */
               overflow: hidden;
               width: 800px;
               background-color: blue;
           }
   
           .damao {
               width: 200px;
               height: 200px;
               float: left;
               background-color: black;
           }
   
           .ermao {
               width: 400px;
               height: 400px;
               float: left;
               background-color: pink;
           }
   
           .footer {
               width: 800px;
               height: 100px;
               background-color: yellow;
           }
       </style>
   </head>
   
   <body>
       <div class="box">
           <div class="damao">大毛</div>
           <div class="ermao">二毛</div>
       </div>
       <div class="footer"></div>
   </body>
   
   </html>
   ```

   - 优点：代码简洁；
   - 缺点：无法显示溢出的部分。

7. **父级添加:after伪元素**

   :after 方法是**额外标签法的升级**，也是给父元素添加。

   本质是在大盒子内部的后端插入一个盒子。

   ```css
   .clearfix:after {
   	content: "";
       /* 转换为块元素 */
   	display: block;
   	height: 0;
       /* 清除浮动 */
   	clear: both;
   	visbility: hidden;
   }
   .clearfix {
   	/* css兼容IE6/7 */
   	*zoom: 1;
   }
   ```

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
       <style>
           .box {
               width: 800px;
               background-color: blue;
           }
   
           .clearfix:after {
               content: "";
               /* 转换为块元素 */
               display: block;
               height: 0;
               /* 清除浮动 */
               clear: both;
               visbility: hidden;
           }
   
           .clearfix {
               /* css兼容IE6/7 */
               *zoom: 1;
           }
   
           .damao {
               width: 200px;
               height: 200px;
               float: left;
               background-color: black;
           }
   
           .ermao {
               width: 400px;
               height: 400px;
               float: left;
               background-color: pink;
           }
   
           .footer {
               width: 800px;
               height: 100px;
               background-color: yellow;
           }
       </style>
   </head>
   
   <body>
       <div class="box clearfix">
           <div class="damao">大毛</div>
           <div class="ermao">二毛</div>
       </div>
       <div class="footer"></div>
   </body>
   
   </html>
   ```

   - 优点：结构清晰，没有增加标签；
   - 缺点：需要照顾低版本浏览器。
   - 代表网站：百度、淘宝、网易等。

8. **双伪元素清除浮动**

   本质是在大盒子内部的前后插入盒子。

   ```css
   .clearfix:before, .clearfix:after {
   	content: "";
   	display: table;
   }
   .clearfix:after {
   	clear: both;
   }
   .clearfix {
   	*zoom: 1;
   }
   ```

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
       <style>
           .box {
               width: 800px;
               background-color: blue;
           }
   
           .clearfix:before,
           .clearfix:after {
               content: "";
               display: table;
           }
   
           .clearfix:after {
               clear: both;
           }
   
           .clearfix {
               *zoom: 1;
           }
   
           .damao {
               width: 200px;
               height: 200px;
               float: left;
               background-color: black;
           }
   
           .ermao {
               width: 400px;
               height: 400px;
               float: left;
               background-color: pink;
           }
   
           .footer {
               width: 800px;
               height: 100px;
               background-color: yellow;
           }
       </style>
   </head>
   
   <body>
       <div class="box clearfix">
           <div class="damao">大毛</div>
           <div class="ermao">二毛</div>
       </div>
       <div class="footer"></div>
   </body>
   
   </html>
   ```

   - 优点：代码更简洁；
   - 缺点：需要照顾低版本浏览器。
   - 代表网站：小米、腾讯。

## 四、PS切图

1. 常见的图片格式

   - jpg图像格式：JPEG(JPG)对色彩的信息保留较好，高清、颜色较多，**产品类的图片经常用jpg格式**；
   - gif图像格式：GIF格式最多只能储存256色，所以通常用来显示简单图形及字体，但是可以保存透明背景和动画效果，实际**常用于一些图片小动画效果**；
   - png图像格式：一种新兴的网络图形格式，结合了gif和jpeg的优点，具有存储形式丰富的特点，能够保持透明背景。**如果想要切成背景透明的图片，清选择png格式*；
   - psd图像格式：psd格式是photoshop的转用格式，里面可以存放图层、通道、遮罩等多种设计稿，对我们前端人员来说，其最大的优点是**可以直接从上面复制文字、获得图片，还可以测量大小和距离。**

2. **图层切图**

   最简单的切图方式：右击图层→快速导出为PNG

   合并图层：选中多个图层→单击图层菜单→合并图层（Ctrl+E）

3. 切片切图

   切片工具：

   ![image-20210830190209702](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210830190209702.png)

   导出选中图片：

   文件菜单→导出→存储为web设备所用格式→选择所需图片格式→存储

4. **PS插件切图**

   **Cutterman**是一款运行在Photoshop中的插件，能够自动将所需的图层进行输出，以替代传统的手工”导出web所用格式“以及使用切片工具进行挨个切图的繁琐流程。

# 学成在线案例

1. **CSS属性书写顺序**（重点）

   建议遵循以下顺序：

   1. 布局定位属性：display / position / float / clear / visibility / overflow
   2. 自身属性：width / height / margin / padding / border / background
   3. 文本属性：color / font / text-decoration / text-align / vertical-align / white-space / break-word
   4. 其他属性（CSS3）：content / cursor / border-radius / box-shadow / text-shadow / background:linear-gradient...

   ```css
   .jdc {
   	display: block;
   	position: relatice;
   	float: left;
   	
   	width: 100px;
   	height: 100px;
   	margin: 0 10px;
   	padding: 20px 0;
   	
   	font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;
   	color: #333;
   	
   	background: rgba(0,0,0,.5);
   	border-radius: 10px;
   }
   ```

2. **页面布局整体思路**

   1. 确定页面的版心（可视区）；
   2. 分析页面中的行模块，以及每个行模块中的列模块；
   3. 行→标准流，列→浮动；
   4. 制作HTML结构，遵循先有结构，后有样式的原则。

3. 确定版心

   这个页面的版心是1200像素，每个版心都要水平居中对齐，可以**定义版心为公共类**：

   ```css
   .w {
       width: 1200px;
       margin: auto;
   }
   ```

4. 头部制作

   ![image-20210831203552541](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210831203552541.png)

   - 导航栏：

     实际开发中，我们不会直接用链接a，而是用li包含链接(li+a)的做法。

   - search搜索框：

     search大盒子中包含2个表单（input文本框及button按钮）
   
5. banner制作

   ![image-20210901202055042](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210901202055042.png)

6. 精品推荐模块

   ![image-20210901211400624](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210901211400624.png)

   - 版心大盒子水平居中goods精品，注意此处有盒子阴影；
   - 1号盒子为标题H3，左浮动；
   - 2号盒子放链接，左浮动，goods-item距离可以控制链接的左右外边距（行内元素只给左右内外边距）；
   - 3号盒子右浮动mod修改

7. 精品推荐大模块

   ![image-20210901214646424](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210901214646424.png)

   - 1号盒子为最大的盒子，box版心水平居中对齐；
   - 2号盒子为标题部分，box-hd，左侧标题为h3左浮动，右侧链接a右浮动；
   - 3号盒子为底下部分，box-bd，无序列表ul，由10个li组成
   
8. 底部模块

   ![image-20210902181947017](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210902181947017.png)

   - 1号为通栏大盒子，底部footer给高度，底色白色；
   - 2号为半新盒子，水平居中；
   - 3号盒子版权copyright，左对齐；
   - 4号盒子链接组links，右对齐

# 定位

## 一、定位组成

1. 定位：将盒子**定**在**某一个位置**，所以**定位也是在摆放盒子**，**按照定位的方式移动盒子**。

   ​		   定位可以**让盒子自由地在某个盒子内移动位置**或者**固定在屏幕中的某个位置**，并且**压住其他盒子**。

   

   ​		   定位=定位模式+边偏移。

   ​		   定位模式：用于指定一个元素在文档中的定位方式；

   ​		   边偏移：决定了该元素的最终位置。

2. 定位模式：通过CSS的**position**属性设置。

   | 值       | 语义         |
   | -------- | ------------ |
   | static   | **静态**定位 |
   | relative | **相对**定位 |
   | absolute | **绝对**定位 |
   | fixed    | **固定**定位 |

3. 边偏移：有**top、bottom、left和right** 4个属性。

   | 边偏移属性 | 示例          | 描述                                                     |
   | ---------- | ------------- | -------------------------------------------------------- |
   | top        | top: 80px;    | **顶端**偏移量，定义元素相对于其父元素**上边线**的距离。 |
   | bottom     | bottom: 80px; | **底部**偏移量，定义元素相对于其父元素**下边线**的距离。 |
   | left       | left: 80px;   | **左侧**偏移量，定义元素相对于其父元素**左边线**的距离。 |
   | right      | right: 80px;  | **右侧**偏移量，定义元素相对于其父元素**右边线**的距离。 |

## 二、静态定位static

静态定位是元素的**默认定位方式**，**无定位**的意思。

语法：

```css
选择器 {
	position: static;
}
```

- 静态定位按照标准流特性摆放位置，没有边偏移；
- 静态定位在布局中很少用到。

## 三、相对定位relative

相对定位是指元素相对于自己**原来的位置**来移动位置。、

语法：

```css
选择器 {
	position: relative;
}
```

- 相对于自己原来的位置来移动（**移动位置的时候其参照点是自己原来的位置**）；
- **原来在标准流的位置继续占有**，后面的盒子仍然以标准流的方式对待它（**不脱标，继续保留原来的位置**）。

## 四、绝对定位absolute（重要）

**绝对定位**是元素在移动位置的时候，相对于它**祖先元素**来说的。

语法：

```css
选择器 {
	position: absolute;
}
```

- 如果**没有祖先元素**或者**祖先元素没有定位**，则以浏览器为准定位；
- 如果祖先元素有定位（相对、绝对、固定定位），则以**最近一级的有定位祖先元素**为参考点移动位置；
- 绝对定位**不再占有原先的位置**（脱离标准流，脱标）。

**子绝父相**：

**子级使用绝对定位，父级则需要相对定位。**

- 子级绝对定位，不会占有位置，可以放到父级盒子里面的任何一个地方，不会影响其他的兄弟盒子；
- 父盒子需要加定位，将子盒子限制在父盒子内；
- 父盒子布局时，需要占有位置，因此父亲只能用相对定位。

## 五、固定定位fixed（重要）

**固定定位**是指元素**固定于浏览器可视区的位置**。

主要使用场景：浏览器页面滚动时元素的位置不发生改变。

语法：

```css
选择器 {
	position: fixed;
}
```

- 以浏览器的**可视窗口**为参照进行移动；
- 跟父元素没关系；
- 不随滚动条的滚动而滚动；
- 固定定位**不占有原先的位置**（固定定位也是脱标的，可以看做是一种特殊的绝对定位）。

**固定定位小技巧：固定在版心右侧位置**

小算法：

1. 让固定定位的盒子left: 50%，到浏览器可视区（版心）的一半位置；
2. 让固定定位的盒子margin-left: 版心宽度的一半距离，到版心宽度的一半位置。

```css
.fixed {
	position: fixed;
	/* 走浏览器宽度的一半 */
	left: 50%;
	/* 利用margin走版心盒子宽度的一半 */
	margin-left: 400px;
}
```

## 六、粘性定位sticky

**粘性定位**可以被认为是相对定位和固定定位的混合。

```css
选择器 {
	position: sticky;
	top: 10px;
    /* 当元素距离顶部10px时 变为粘性定位*/
}
```

- 以浏览器的**可视窗口**为参照移动元素（固定定位特点）；
- 粘性定位**占有原先的位置**（相对定位特点）；
- 必须添加top、left、right、bottom其中一个才有效果，不添加则视作相对定位。

与页面滚动搭配使用，兼容性较差，IE不支持。

## 七、定位总结

| 定位模式             | 是否脱标         | 移动位置               | 是否常用   |
| -------------------- | ---------------- | ---------------------- | ---------- |
| static静态定位       | 否               | 不移动                 | 很少       |
| **relative相对定位** | 否（占有位置）   | 相对于自身位置移动     | 常用       |
| **absolute绝对定位** | 是（不占有位置） | 相对带有定位的父级移动 | 常用       |
| **fixed固定定位**    | 是（不占有位置） | 相对浏览器可视区移动   | 常用       |
| sticky粘性定位       | 否（占有位置）   | 浏览器可视区           | 当前阶段少 |

## 八、定位的叠放次序z-index

在使用定位布局时，可能会出现盒子重叠的情况。

此时，我们可以使用**z-index**来控制盒子的上下顺序（z轴）。

```css
选择器 {
	z-index: 1;
}
```

- 数值可以是正整数、负整数或0，默认为auto。**数值越大，盒子越靠上；**
- 若数值相同，则按照书写顺序，遵从**“后来者居上”**的原则；
- 数字后面不能加单位；
- 只有定位的盒子才有z-index属性。

## 九、定位拓展

1. **绝对定位的盒子居中**

   水平居中：

   ```css
   .absolute {
   	position: absolute;
   	/* 走父容器宽度的50% */
   	left :50%;
   	/* margin 负值 往左边走自己盒子宽度的一半 */
   	margin-left: -100px;
   }
   ```

   垂直居中：

   ```css
   .absolute {
   	position: absolute;
   	/* 走父容器高度的一半 */
   	top: 50%;
   	/* margin 负值 往上走自己盒子高度的一半 */
   	margin-top: 100px;
   }
   ```

2. **定位的特殊特性**

   绝对定位和固定定位都和浮动类似

   - 行内元素添加绝对或固定定位，可以直接设置高度和宽度；
   - 块级元素添加绝对或固定定位，如果不给宽度或高度，默认大小是内容的大小。

3. **脱标的盒子不会触发外边距塌陷**

   浮动元素、绝对定位/固定定位元素（脱离标准流）都不会触发外边距合并的问题。

4. **绝对定位/固定定位会完全压住盒子**

   **浮动**只会**压住它下面标准流的盒子**，但**不会压住标准流盒内的文字/图片**；

   **绝对定位/固定定位**会**完全压住下面标准流的所有内容**。

   

   浮动之所以不会压住文字，是因为浮动产生的目的最初便是为了做文字环绕效果。

## 十、元素的显示与隐藏

比如网页广告。

1. **display**

   - **display: none;** 隐藏对象
   - **display: block;** 除了转换为块级元素外，同时还有显示元素的意思

   display隐藏元素后，**不再占有原来位置**。

2. **visibility**

   visibility可见性，用于指定一个元素是否可见。

   - **visibility: visible;**元素可视
   - **visibility: hidden;**元素隐藏

   visibility隐藏元素后，**继续占有原来的位置**。

3. **overflow**

   overflow本意是溢出，用于**对溢出部分**设置显示或隐藏。

   - **overflow: visible;**溢出部分显示
   - **overflow: hidden;**溢出部分隐藏
   - **overflow: scroll;**显示滚动条（不溢出也显示滚动条）
   - **overflow: auto;**在需要时对内容添加滚动条

# CSS高级技巧

## 一、精灵图

1. 为什么需要精灵图

   一个网页中往往会应用很多小的背景图像作为修饰，当网页中的图像过多时，服务器就会频繁地接收和发送请求图片，造成服务器请求压力过大的问题，这将大大降低页面的加载速度。

   **为了有效减少服务器接收和发送请求的次数，提高页面的加载速度**，出现了CSS精灵技术（也称CSS Sprites、CSS雪碧）。

   核心原理：**将网页中的一些小背景图像整合到一张大图中**，这样服务器只要请求一次就可以了。

2. 精灵图（sprites）的使用

   - 将多个小背景图片整合到一张大图片中；
   - 对盒子**添加背景图片**；
   - 移动背景图片位置，**background-position**，移动距离即目标图片的x和y坐标，一般情况下，精灵图都是负值；

## 二、字体图标

1. 字体图标的产生

   字体图标使用场景：主要用于显示**网页中通用、常用的一些小图标**。

   精灵图缺点：

   - 图片文件依然较大；
   - 图片本身放大或缩小会失真；
   - 一旦图片制作完成，想要更换非常复杂
   
    此时，有一种技术的出现就很好地解决了以上问题——**字体图标iconfont**。
   
   字体图标可以为前端工程师提供一种方便高效的图标使用方式，展示的是图标，但其**本质是字体**。
   
2. 字体图标的优点

   - 轻量级：一个字体图标比一系列的图像要小，一旦字体加载了，图标就会马上渲染出来，减少了服务器请求；
   - 灵活性：本质是蚊子，可以随便改变颜色、产生阴影、设置透明效果、旋转等；
   - 兼容性：几乎支持所有浏览器，可以放心使用。

3. 总结：

   - 结构和样式较为简单的小图标→字体图标；
   - 结构和样式较为复杂的小图片→精灵图。

4. **字体图标使用**

   1. 字体图标下载

      推荐下载网站：

      - **icomoon字库** http://icomoon.io
      - **阿里iconfont字库** http://www.iconfont.cn/

   2. 字体图标引入

      - 把下载包里面的fonts文件夹放入页面根目录下

        ![image-20210915175319032](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210915175319032.png)

      - 在CSS样式中全局声明字体：

        ```css
        @font-face {
        	font-family: 'icomoon';
        	src: url('fonts/icomoon.eot?7kkyc2');
        	src: url('fonts/icomoon.eot?7kkyc2#iefix') format('embedded-opentype'),
        	url('fonts/icomoon.ttf?7kkyc2') format('truetype'),
        	url('fonts/icomoon.woff?7kkyc2') format('woff'),
        	url('fonts/icomoon.svg?7kkyc2#icomoon') format('svg');
        	font-weight: normal;
        	font-style: normal;
        }
        ```

      - html标签内添加小图标

        ![image-20210915180047376](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210915180047376.png)

        ```html
        <span>	</span>
        ```

        ```css
        span {
        	font-family: 'icomoon';
        }
        ```

   3. 字体图标追加

      先把压缩包里面的**selection.json**上传，然后选中自己想要的新的图标，重新下载压缩包，并替换原来的文件即可。

      ![image-20210915200404217](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210915200404217.png)

## 三、CSS三角

网页中常见一些三角形，使用CSS可以直接画出来，不必做成图片或者字体图标。

![image-20210915200534432](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210915200534432.png)

1. 三角做法：

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>CSS三角制作</title>
       <style>
           .box1 {
               /* 宽高为0的盒子 */
               width: 0;
               height: 0;
               border-top: 10px solid red;
               border-right: 10px solid orange;
               border-bottom: 10px solid yellow;
               border-left: 10px solid green;
           }
   
           .box2 {
               width: 0;
               height: 0;
               /* 透明边框 */
               border: 10px solid transparent;
               border-left: 10px solid red;
               margin-top: 100px;
           }
       </style>
   </head>
   
   <body>
       <div class="box1"></div>
       <div class="box2"></div>
   </body>
   
   </html>
   ```

   ![image-20210915201444023](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210915201444023.png)

2. 示例

   利用绝对定位完成：

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>京东三角</title>
       <style>
           .jd {
               position: relative;
               width: 120px;
               height: 249px;
               background-color: pink;
               margin-top: 50px;
           }
   
           .jd span {
               position: absolute;
               right: 15px;
               top: -20px;
               width: 0;
               height: 0;
               /* 为了照顾兼容性 */
               line-height: 0;
               font-size: 0;
               border: 10px solid transparent;
               border-bottom: 10px solid pink;
           }
       </style>
   </head>
   
   <body>
       <div class="jd">
           <span></span>
       </div>
   </body>
   
   </html>
   ```

   ![image-20210915205539557](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210915205539557.png)

## 四、CSS用户界面样式

1. **鼠标样式cursor**

   ```css
   li {
   	cursor: pointer;
   }
   ```

   设置或检索在对象上移动的鼠标指针采用何种系统预定义的光标形状。

   | 属性值      | 描述         |
   | ----------- | ------------ |
   | default     | 小白（默认） |
   | pointer     | 小手         |
   | move        | 移动         |
   | text        | 文本         |
   | not-allowed |              |

2. **表单轮廓outline**

   取消表单轮廓线

   给表单添加**outline: 0;**或者**outline: none;** 样式，就可以去掉默认的蓝色边框。

   ```css
   input {
   	outline: none;
   }
   ```

3. **防止表单域拖拽resize**

   ```css
   textarea {
   	resize: none;
   }
   ```

## 五、vertical-align属性应用

1. 使用场景：经常用于设置图片或者表单（行内块元素）和文字垂直对齐。

2. 官方解释：用于设置一个元素的**垂直对齐方式**，但是它只针对于**行内元素或者行内块元素**有效。

3. 语法：

   ```css
   vertical-align: baseline | top | middle | bottom
   ```

   | 属性值   | 描述                                       |
   | -------- | ------------------------------------------ |
   | baseline | 默认，元素放置在父元素的**基线**上         |
   | top      | 把元素的顶端与行中**最高元素的顶端对齐**   |
   | middle   | 把元素放置在父元素的**中部**               |
   | bottom   | 把元素的顶端与行中**最低的元素的顶端对齐** |

   ![image-20210915220310606](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210915220310606.png)
   
4. 图片底侧空白缝隙解决方案

   原因：行内块元素会和文字的基线对齐

   解决方案：

   1. 给图片添加 **vertical-align: middle | top | bottom;** 等；
   2. 把图片转换为块级元素 display: block;

## 六、溢出文字省略号显示

1. **单行文本**溢出省略号显示

   ```css
   /* 1.强制一行内显示文本 */
   white-space: nowrap;	//不自动换行
   /* 2.超出部分隐藏 */
   overflow: hidden;
   /* 3.文字用省略号替代超出的部分 */
   text-overflow: ellipsis;
   ```

2. **多行文本**溢出省略号显示

   注意：多行文本溢出显示省略号，有**较大的兼容性问题**，**适合于webkit浏览器或移动端**。

   ```css
   /* 1.溢出部分隐藏 */
   overflow: hidden;
   /* 2.弹性伸缩很自模型显示 */
   display: -webkit -box;
   /* 3.限制在一个块元素显示的文本的行数 */
   -webkit-line-clamp: 2;
   /* 4.设置或检索伸缩盒子对象的子元素的排列方式 */
   -webkit-box-orient: vertical;
   ```

## 七、常见布局技巧

1. margin负值的运用

   让每个盒子margin左侧移动-1px，正好压住相邻盒子的边框；

   鼠标经过某个盒子的时候，提高当前盒子的层级（使用**相对定位**会压住其他标准流盒子/**z-index**提高层级），实现鼠标指向时边框变色。

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>margin负值的运用</title>
       <style>
           ul li {
               float: left;
               list-style: none;
               width: 150px;
               height: 200px;
               border: 1px solid red;
               margin-left: -1px;
           }
   
           ul li:hover {
               /* 1.使用相对定位 */
               position: relative;
               /* 2.或利用z-index提高层级*/
               /* z-index: 1; */
               border: 1px solid blue;
           }
       </style>
   </head>
   
   <body>
       <ul>
           <li>1</li>
           <li>2</li>
           <li>3</li>
           <li>4</li>
           <li>5</li>
       </ul>
   </body>
   
   </html>
   ```

   ![image-20210916201939384](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210916201939384.png)

   ![image-20210916204728915](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210916204728915.png)

2. 文字围绕浮动元素

   运用浮动元素不会压住文字的特性

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>文字围绕浮动元素的妙用</title>
       <style>
           * {
               margin: 0;
               padding: 0;
           }
   
           .box {
               width: 300px;
               height: 70px;
               background-color: pink;
               margin: 0 auto;
               padding: 5px;
           }
   
           .pic {
               float: left;
               margin-right: 5px;
               width: 120px;
               height: 60px;
           }
   
           .pic img {
               width: 100%;
           }
       </style>
   </head>
   
   <body>
       <div class="box">
           <div class="pic">
               <img src="./images/tudou.jpg" alt="">
           </div>
           <p>【锦集】热身赛-巴西0-1秘鲁 内马尔替补两人血染赛场</p>
       </div>
   </body>
   
   </html>
   ```

   ![image-20210916210846948](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210916210846948.png)

3. 行内块的巧妙运用

   - 行内块元素可以设置宽度高度；
   - 可以显示在一行上，且中间保有空隙（无需再设置margin值）；
   - 给父盒子添加text-align: center; 即可实现水平居中。

   ![image-20210916213221072](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210916213221072.png)

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>行内块的巧妙运用</title>
       <style>
           * {
               margin: 0;
               padding: 0;
           }
   
           a {
               text-decoration: none;
           }
   
           .box {
               text-align: center;
           }
   
           .box a {
               /* 行内块元素 */
               display: inline-block;
               width: 36px;
               height: 36px;
               background-color: #f7f7f7;
               border: 1px solid #ccc;
               text-align: center;
               line-height: 36px;
               color: #333;
               font-size: 14px;
           }
   
           .box .prev,
           .box .next {
               width: 85px;
           }
   
           .box .current,
           .box .elp {
               background-color: #fff;
               border: none;
           }
   
           .box input {
               height: 36px;
               width: 45px;
               border: 1px solid #ccc;
               /* 取消点击后轮廓线 */
               outline: none;
           }
   
           .box button {
               width: 60px;
               height: 36px;
               background-color: #f7f7f7;
               border: 1px solid #ccc;
           }
       </style>
   </head>
   
   <body>
       <div class="box">
           <a href="#" class="prev">&lt;&lt;上一页</a>
           <a href="#" class="current">2</a>
           <a href="#">3</a>
           <a href="#">4</a>
           <a href="#">5</a>
           <a href="#">6</a>
           <a href="#" class="elp">...</a>
           <a href="#" class="next">下一页&gt;&gt;</a>
           到第
           <input type="text">
           页
           <button>确定</button>
       </div>
   </body>
   
   </html>
   ```

   ![image-20210916214819307](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210916214819307.png)

4. CSS三角强化

   ![image-20210916215440682](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210916215440682.png)
   
   三角形实现原理：
   
   ```css
   .box1 {
               width: 0;
               height: 0;
               border-top: 100px solid pink;
               border-right: 50px solid skyblue;
               border-left: 0;
               border-bottom: 0;
           }
   ```
   
   ![image-20210917214932811](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210917214932811.png)
   
   ```css
   .box1 {
               width: 0;
               height: 0;
               /* 1.只保留右边框颜色 */
               border-color: transparent red transparent transparent;
               /* 2.边框样式都为solid */
               border-style: solid;
               /* 3.上边框宽度更大 右边框宽度稍小 */
               border-width: 22px 8px 0 0;
           }
   ```
   
   ![image-20210917215617261](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210917215617261.png)
   
   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>三角形的巧妙运用</title>
       <style>
           .price {
               width: 160px;
               height: 24px;
               border: 1px solid red;
               margin: 0 auto;
               line-height: 24px;
           }
   
           .miaosha {
               position: relative;
               float: left;
               width: 90px;
               height: 100%;
               background-color: red;
               text-align: center;
               color: #fff;
           }
   
           .miaosha i {
               position: absolute;
               right: 0;
               width: 0;
               height: 0;
               border-color: transparent #fff transparent transparent;
               border-style: solid;
               border-width: 24px 10px 0 0;
   
           }
   
           .origin {
               font-size: 12px;
               color: gray;
               /* 删除线 */
               text-decoration: line-through;
               padding-left: 10px;
           }
       </style>
   </head>
   
   <body>
       <div class="price">
           <span class="miaosha">￥1650
               <i></i>
           </span>
           <span class="origin">￥5650</span>
       </div>
   </body>
   
   </html>
   ```
   
   ![image-20210917220417710](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210917220417710.png)

## 八、CSS初始化

不同浏览器对有些标签的默认值是不同的，为了消除不同浏览器对HTML文本呈现的差异、照顾浏览器的兼容，我们需要对CSS初始化（重设浏览器样式，也称CSS reset）。

```css
	    /* 清除所有标签的内外边距 */
        * {
            margin: 0;
            padding: 0;
        }

        /* 使倾斜字体不倾斜 */
        em,
        i {
            font-style: normal;
        }

        /* 去掉li前的小圆点 */
        li {
            list-style: none;
        }

        img {
            /* border 0 照顾低版本浏览器 如果图片外面包含了链接会有边框的问题 */
            border: 0;
            /* 解决图片底侧有空白缝隙的问题 使和中线对齐*/
            vertical-align: middle;
        }

        button {
            /* 当鼠标经过button 鼠标样式变为小手 */
            cursor: pointer;
        }

        a {
            color: #666;
            ;
            text-decoration: none;
        }

        a:hover {
            color: #c81623;
        }

        button,
        input {
            font-family: Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53";
        }

        body {
            /* CSS3抗锯齿型 让文字显示的更加清晰 */
            -webkit-font-smoothing: antialiased;
            background-color: #fff;
            font: 12px/1.5 Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53";
            color: #666;
        }

        .hide,
        .none {
            /* 隐藏元素 */
            display: none;
        }

        /* 清除浮动 */
        .clearfix:after {
            visibility: hidden;
            clear: both;
            display: block;
            content: ".";
            height: 0;
        }

        .clearfix {
            *zoom: 1;
        }
```

**Unicode编码字体：**

把中文字体的名称用相应的Unicode编码来代替，这样就可以有效地避免浏览器解释CSS代码时出现代码的问题。

如，**黑体 \9ED1\4F53** **宋体 \5B8B\4F53** **微软雅黑 \5FAE\8F6F\96C5\9ED1**

# HTML5和CSS3提高

## 一、HTML5新特性

1. 新增**语义化标签**

   HTML5的新增特性主要针对以前的不足，增加了一些新的**标签**、**表单**和**表单属性**等。

   这些新特性都有兼容性问题，基本是IE9+以上版本的浏览器才支持，如果不考虑兼容性问题，可以大量使用这些新特性。

   - < header>：头部标签
   - < nav>：导航标签
   - < article>：内容标签
   - < section>：定义文档某个区域
   - < aside>：侧边栏标签
   - < footer>：尾部标签

   ![image-20210920180517374](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210920180517374.png)

   注意：

   - 这种语义化标签主要是针对**搜索引擎**的；
   - 这些新标签在页面中**可以使用多次**；
   - 在IE9中，需要把这些元素**转换为块级元素**。

2. 新增**多媒体标签**

   - < audio>：音频
   - < video>：视频

   使用它们可以很方便地在页面中嵌入音频和视频，而不再需要flash和其他浏览器插件。

   1. 视频<video>

      当前<video>元素支持三种视频格式，不同浏览器支持情况如下：

      ![image-20210920181530595](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210920181530595.png)

      **注意：尽量使用mp4格式。**

      语法：

      ```html
      <video src="文件地址" controls="controls"></video>
      ```

      考虑兼容问题实例：

      ```html
      <video width="320" height="240" controls>
      	<source src="movie.mp4" type="video/mp4">
      	<source src="movie.ogg" type="video/ogg">
      	您的浏览器暂不支持video标签。
      </video>
      ```

      常见属性：

      | 属性     | 值                                  | 描述                                                         |
      | -------- | ----------------------------------- | ------------------------------------------------------------ |
      | autoplay | autoplay                            | 视频就绪自动播放（谷歌浏览器需要添加muted来解决自动播放问题） |
      | controls | controls                            | 向用户显示播放控件                                           |
      | width    | pixels（像素）                      | 设置播放器宽度                                               |
      | height   | pixels（像素）                      | 设置播放器高度                                               |
      | loop     | loop                                | 播放完是否继续播放该视频（循环播放）                         |
      | preload  | auto（预加载视频）/none（不预加载） | 规定是否预加载视频（若有autoplay属性，则忽略该属性）         |
      | src      | url                                 | 视频url地址                                                  |
      | poster   | Imgurl                              | 加载等待的画面图片                                           |
      | muted    | muted                               | 静音播放                                                     |

   2. 音频<audio>

      当前<audio>元素支持三种音频格式：

      ![image-20210920182934964](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210920182934964.png)

      **注意：尽量使用mp3格式。**

      语法：

      ```html
      <audio src="文件地址" controls="controls"></audio>
      ```

      考虑兼容问题实例：

      ```html
      <audio controls="controls">
      	<source src="happy.mp3" type="audio/mprg">
      	<source src="happy.ogg" type="audio/ogg">
      	您的浏览器暂不支持<audio>标签。
      </audio>
      ```

      常见属性：

      | 属性     | 值       | 描述                           |
      | -------- | -------- | ------------------------------ |
      | autoplay | autoplay | 音频就绪后自动播放             |
      | controls | controls | 向用户显示播放控件，如播放按钮 |
      | loop     | loop     | 循环播放                       |
      | src      | url      | 音频的url地址                  |

      注意：谷歌浏览器禁止了音频自动播放（可以通过JS解决）

3. 新增**input类型**

   | 属性值        | 说明                        |
   | ------------- | --------------------------- |
   | type="email"  | 限制用户输入必须为Email类型 |
   | type="url"    | 限制用户输入必须为url类型   |
   | type="date"   | 限制用户输入必须为日期类型  |
   | type="time"   | 限制用户输入必须为时间类型  |
   | type="month"  | 限制用户输入必须为月类型    |
   | type="week"   | 限制用户输入必须为周类型    |
   | type="number" | 限制用户输入必须为数字类型  |
   | type="tel"    | 手机号码                    |
   | type="search" | 搜索框                      |
   | type="color"  | 生成一个颜色选择表单        |

4. 新增**表单属性**

   | 属性            | 值           | 说明                                                         |
   | --------------- | ------------ | ------------------------------------------------------------ |
   | required        | required     | 内容不能为空，必填                                           |
   | **placeholder** | **提示文本** | **表单的提示信息，存在默认值将不显示**                       |
   | autofocus       | autofocus    | 自动聚焦属性，页面加载完成自动聚焦到指定表单                 |
   | autocomplete    | off/on       | 当用户在字段开始键入时，浏览器基于之前键入过的值，显示出之前在字段中填写的选项。默认已经打开，即autocomplete="on"，关闭autocomplete="off"。需要放在表单内，同时加上name属性，同时成功提交。 |
   | **multiple**    | **multiple** | **可以多选文件提交**（配合文件域file使用）                   |

   修改提示文本颜色：

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>HTML5新增表单属性</title>
       <style>
           input::placeholder {
               color: pink;
           }
       </style>
   </head>
   
   <body>
       <input type="search" required="required" placeholder="名字">
       <input type="submit" value="提交">
   </body>
   
   </html>
   ```

   ![image-20210920223652291](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210920223652291.png)

## 二、CSS3新特性

### 1.新增选择器

- **属性选择器**

  属性选择器可以**根据元素特定属性**来选择元素，有了属性选择器，就可以不用借助类或id选择器。

  | 选择符        | 简介                                    |
  | ------------- | --------------------------------------- |
  | E[att]        | 选择具有att属性的E元素                  |
  | E[att="val"]  | 选择具有att属性且属性值等于val的E元素   |
  | E[att^="val"] | 匹配具有att属性且属性值以val开头的E元素 |
  | E[att$="val"] | 匹配具有att属性且属性值以val结尾的E元素 |
  | E[att*="val"] | 匹配具有att属性且属性值中含有val的E元素 |

  **注意：类选择器、属性选择器以及伪类选择器 权重都是10。**

- **结构伪类选择器**

  结构伪类选择器主要根据**文档结构**来选择元素，常用于根据父级选择里面的子元素。

  | 选择符            | 简介                        |
  | ----------------- | --------------------------- |
  | E :first-child    | 匹配父元素中的第一个子元素E |
  | E :last-child     | 匹配父元素中最后一个E元素   |
  | E :nth-child(n)   | 匹配父元素中的第n个子元素E  |
  | E :first-of-type  | 指定类型E的第一个           |
  | E :last-of-type   | 指定类型E的最后一个         |
  | E :nth-of-type(n) | 指定类型E的第n个            |

  **nth-child(n)：**

  选择某个父元素的一个或多个特定的子元素。

  **n可以是数字、关键字（even偶数 / odd奇数）或公式。**

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>CSS3新增结构伪类选择器</title>
      <style>
          /* 1.选择ul里的第一个叫li的孩子 */
          ul li:first-child {
              background-color: red;
          }
  
          /* 2.选择ul里的最后一个叫li的孩子 */
          ul li:last-child {
              background-color: blue;
          }
  
          /* 3.选择ul里的第二个叫li的孩子 */
          ul li:nth-child(2) {
              background-color: pink;
          }
      </style>
  </head>
  
  <body>
      <ul>
          <li>我是第1个孩子</li>
          <li>我是第2个孩子</li>
          <li>我是第3个孩子</li>
          <li>我是第4个孩子</li>
          <li>我是第5个孩子</li>
          <li>我是第6个孩子</li>
          <li>我是第7个孩子</li>
          <li>我是第8个孩子</li>
      </ul>
  </body>
  
  </html>
  ```

  ![image-20210922185913189](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210922185913189.png)

  **隔行变色：**

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>隔行变色</title>
      <style>
          ul li:nth-child(even) {
              background-color: #ccc;
          }
      </style>
  </head>
  
  <body>
      <ul>
          <li>我是第1个孩子</li>
          <li>我是第2个孩子</li>
          <li>我是第3个孩子</li>
          <li>我是第4个孩子</li>
          <li>我是第5个孩子</li>
          <li>我是第6个孩子</li>
          <li>我是第7个孩子</li>
          <li>我是第8个孩子</li>
      </ul>
  </body>
  
  </html>
  ```

  ![image-20210922190339461](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210922190339461.png)

  **常见公式：**

  n++循环（第0个元素或超出元素个数的部分会被忽略）

  | 公式 | 取值                           |
  | ---- | ------------------------------ |
  | 2n   | 偶数                           |
  | 2n+1 | 奇数                           |
  | 5n   | 5、10、15……                    |
  | n+5  | 从第5个开始（包含第5个）到最后 |
  | -n+5 | 前5个（包含第5个）             |

  **nth-child(n)和nth-of-type的区别：**

  - **nth-child**会把**所有的盒子**都排序号，在执行时，**先匹配序号，再看前面的元素类型**；
  - **nth-of-type**只会把**指定的元素类型**排列序号，再进行匹配。

- **伪元素选择器**

  伪元素选择器可以帮助我们**利用CSS创建新标签元素而不需要HTML标签**，从而简化HTML结构。

  | 选择符   | 简介                         |
  | -------- | ---------------------------- |
  | ::before | 在元素**内部的前面**插入内容 |
  | ::after  | 在元素**内部的后面**插入内容 |

  语法：

  ```css
  /* CSS3语法 */
  element::before {
  	样式
  }
  
  /* CSS2过时语法（仅用来支持IE8）*/
  element:before {
  	样式
  }
  
  /* 在每个p元素前插入内容 */
  p::before {
  	content:"Hello world!";
  }
  ```

  注意：

  - before和after创建一个元素，属于**行内元素**（不能直接设置宽高大小）；
  - 新创建的这个元素**在文档树中是找不到**的，所以我们称之为**伪元素**；
  - before和after必须有**content属性**；
  - 伪元素选择器和标签选择器一样，**权重为1**。

  使用场景：

  1. **配合字体图标**
  
     ```html
     <!DOCTYPE html>
     <html lang="en">
     
     <head>
         <meta charset="UTF-8">
         <meta http-equiv="X-UA-Compatible" content="IE=edge">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>伪元素选择器使用场景-字体图标</title>
         <style>
             @font-face {
                 font-family: 'iconfont';
                 /* Project id 2830819 */
                 /* 注意需为路径添加"http:"字样 */
                 src: url('http://at.alicdn.com/t/font_2830819_p10o7xxaqi.woff2?t=1632399390251') format('woff2'),
                     url('http://at.alicdn.com/t/font_2830819_p10o7xxaqi.woff?t=1632399390251') format('woff'),
                     url('http://at.alicdn.com/t/font_2830819_p10o7xxaqi.ttf?t=1632399390251') format('truetype');
             }
     
             div {
                 position: relative;
                 width: 200px;
                 height: 35px;
                 border: 1px solid black;
             }
     
             div::after {
                 position: absolute;
                 right: 10px;
                 top: 10px;
     
                 font-family: 'iconfont';
                 content: '\e65e';
             }
         </style>
     </head>
     
     <body>
         <div></div>
     </body>
     
     </html>
     ```
  
     ![image-20210923212738205](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210923212738205.png)
  
  2. **仿土豆半透明遮罩效果**
  
     ```html
     <!DOCTYPE html>
     <html lang="en">
     
     <head>
         <meta charset="UTF-8">
         <meta http-equiv="X-UA-Compatible" content="IE=edge">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>伪元素选择器使用场景-仿土豆效果</title>
         <style>
             .tudou {
                 position: relative;
                 width: 448px;
                 height: 252px;
             }
     
             .tudou::before {
                 /* 隐藏遮罩层 */
                 display: none;
                 position: absolute;
                 top: 0;
                 left: 0;
                 width: 100%;
                 height: 100%;
                 background: rgba(0, 0, 0, 0.3) url(./images/arr.png) no-repeat center;
                 /* 必须要有content属性 */
                 content: '';
             }
     
             /* 当鼠标经过.tudou 让.tudou::before的遮罩层显示 */
             .tudou:hover::before {
                 /* 显示遮罩层 */
                 display: block;
             }
         </style>
     </head>
     
     <body>
         <div class="tudou">
             <img src="./images/tudou.jpg" alt="">
         </div>
     </body>
     
     </html>
     ```
  
     ![image-20210923213904659](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210923213904659.png)
  
  3. **伪元素清除浮动**
  
     本质上是额外标签法（隔墙法）的升级。
  
     父级添加伪元素：
  
     ```css
     .clearfix::after {
         /* 伪元素必须写的属性 */
     	content: "";
         /* 使用伪元素创建的元素本身为行内元素，因此需要将其转换为块级元素 */
     	display: block;
         /* 使不看见这个元素 */
     	height: 0;
     	visibility: hidden;
         /* 核心代码清除浮动 */
         clear: both;
     }
     ```
  
     父级添加双伪元素：
  
     ```css
     .clearfix::before, .clearfix::after {
     	content: '';
         /* 转换为块元素并且使插入的两个盒子能够在同一行显示 */
     	display: table;
     }
     .clearfix::after {
     	clear: both;
     }
     ```

### 2.CSS3盒子模型

CSS3可以通过**box-sizing**来指定盒模型。

选择不同的属性值，我们计算盒子大小的方式将发生变化。

| **属性值**      | **计算方式**                                                 |
| --------------- | ------------------------------------------------------------ |
| **content-box** | width+padding+border（默认）                                 |
| **border-box**  | width（盒子最终大小就是width大小，宽度不会因padding及border撑开） |

### 3.CSS3其他特性

- **filter滤镜**

  filter CSS属性将模糊或颜色便宜等图形效果应用于元素。

  语法：

  ```css
  filter: 函数();
  ```

  图像模糊：

  ```css
  img {
      /* blur模糊处理 数值越大模糊效果越强 */
  	filter: blur(5px);
  }
  ```

- **calc函数**

  calc() 函数让你在声明CSS属性值时执行一些计算。

  语法：

  ```css
  width: calc(计算公式);
  ```

  让子盒子宽度永远比父盒子小30px：

  ```css
  .father {
  	width: 300px;
  	height: 200px;
  	background-color: pink;
  }
  
  .son {
  	width: calc(100% - 30px);
  	height: 30px;
  	background-color: skyblue;
  }
  ```

### 4.CSS3过渡（重点）

过渡（transition）是CSS3中具有颠覆性的特征之一。

我们可以在不使用flash动画或JavaScript的情况下，为元素从一种样式变换为另一种样式时添加效果（**过渡动画**）。

低版本浏览器不支持（IE9以下版本）。

经常**与:hover一起搭配使用**。

语法：

```css
/* 单个属性设置过渡动画 */
transition: 要过渡的属性 花费时间 运动曲线 何时开始;
/* 多个属性变化用逗号隔开 */
transition: 要过渡的属性 花费时间 运动曲线 何时开始, 要过渡的属性 花费时间 运动曲线 何时开始, ...;
/* 对所有属性变化添加过渡动画 */
transition: all 花费时间 运动曲线 何时开始;
```

- 属性：指定要变化的CSS属性，比如宽度、高度、背景颜色、内外边距……若想要所有的属性都变化过渡，**填写all即可**；

- 花费时间：单位为秒（s），如0.5s，**必须写单位**；

- 运动曲线：默认为ease，可省略；

- 何时开始：单位为秒（s），必须写单位，可以设置延迟触发时间，默认为0s（可省略）。

  **![image-20210924154856072](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210924154856072.png)**

**CSS过渡练习-进度条：**http://127.0.0.1:5500/demo10/demo10_9.html

```css
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS3过渡练习-进度条</title>
    <style>
        .bar {
            width: 150px;
            height: 15px;
            border: 1px solid red;
            border-radius: 7px;
        }

        .bar_in {
            width: 50%;
            height: 100%;
            background-color: red;
            border-top-left-radius: 7px;
            border-bottom-left-radius: 7px;
            transition: width 0.5s;
        }

        .bar:hover .bar_in {
            width: 100%;
            border-top-right-radius: 7px;
            border-bottom-right-radius: 7px;
        }
    </style>
</head>

<body>
    <div class="bar">
        <div class="bar_in"></div>
    </div>
</body>

</html>
```

### 5.CSS32D转换

**转换（transform）**是CSS3中具有颠覆性的特征之一，可以实现元素的位移、旋转、缩放等效果。

2D转换是**改变标签在二维平面上的位置和形状**的一种技术。

二维坐标系：

![image-20211016235058136](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211016235058136.png)

可以简单理解为**变形**：

- **移动：translate**

  2D移动是2D转换里面的一种功能，可以改变元素在页面中的位置，类似定位。

  语法：

  ```css
  transform: translate(x,y);
  
  /* 或者分开写 */
  transform: translateX(n);
  transform: translateY(n);
  ```

  注意：

  - translate最大优点：**不会影响到其他元素的位置**；
  - translate中的**百分比单位是相对于自身元素**的 translate:(50%,50%);
  - 对行内标签没有效果。

  **让盒子实现水平垂直居中：定位配合translate**

  ```css
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>2D转换:移动</title>
      <style>
          div {
              position: relative;
              width: 500px;
              height: 500px;
              background-color: pink;
          }
  
          p {
              position: absolute;
              /* 使p在div盒子中水平居中 */
              top: 50%;
              left: 50%;
              transform: translate(-50%, -50%);
              
              width: 200px;
              height: 200px;
              background-color: purple;
          }
      </style>
  </head>
  
  <body>
      <div>
          <p></p>
      </div>
  </body>
  
  </html>
  ```

- **旋转：rotate**

  2D旋转指的是让元素在二维平面内顺时针或逆时针旋转。

  语法：

  ```css
  transform: rotate(度数);
  ```

   注意：

  - rotate内跟**度数**，**单位为deg**，例如，rotate(45deg);
  - 角度为正时，为顺时针，反之，为逆时针；
  - 默认旋转的中心为元素的中心点。

  **旋转+过渡：**

  ```css
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>2D转换：旋转rotate</title>
      <style>
          img {
              width: 200px;
              height: 200px;
              transition: transform 2s;
          }
  
          img:hover {
              transform: rotate(360deg);
          }
      </style>
  </head>
  
  <body>
      <img src="./images/u=2349051550,3710028665&fm=26&fmt=auto.webp.jpg" alt="">
  </body>
  
  </html>
  ```

   **设置转换中心点：**

  ```css
  transform-origin: x y;
  ```

  - x y**默认**转换的中心点是**元素的中心(50%,50%)**；
  - 还可以给x y设置**像素或方位名词(top/bottom/left/right/center)** **左下角(left bottom)**。

  旋转案例：

  ```css
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>2D转换：旋转rotate</title>
      <style>
          div {
              width: 200px;
              height: 200px;
              border: 1px solid pink;
              margin: 100px auto;
              overflow: hidden;
          }
  
          div::before {
              content: '黑马';
              display: block;
              width: 100%;
              height: 100%;
              background-color: hotpink;
              transform: rotate(90deg);
              transform-origin: left bottom;
              transition: transform 2s;
          }
  
          div:hover::before {
              transform: rotate(0deg);
          }
      </style>
  </head>
  
  <body>
      <div></div>
  </body>
  
  </html>
  ```

  file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo11/demo11_3.html

- **缩放：scale**

  缩放，顾名思义，即放大和缩小。

  语法：

  ```css
  transform: scale(x,y);
  ```

  注意：

  - transform: scale(1,1);宽和高都放大一倍，相当于没有放大；
  - transform: scale(2,2);宽和高都放大两倍；
  - transform: scale(2);只写一个参数，相当于scale(2,2)；
  - transform: scale(0.5,0.5);缩小0.5倍；
  - scale缩放的优点：可以设置转换中心点进行缩放，且不影响其他盒子。

  **鼠标悬停时图片放大：**

  ```css
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>2D转换：旋转rotate</title>
      <style>
          div {
              width: 220px;
              height: 120px;
              overflow: hidden;
          }
  
          img {
              width: 100%;
              transition: transform 1s;
          }
  
          img:hover {
              transform: scale(1.2, 1.2);
          }
      </style>
  </head>
  
  <body>
      <div>
          <img src="./images/QQ图片20190922001517.jpg" alt="">
      </div>
  </body>
  
  </html>
  ```

  file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo11/demo11_4.html

  **分页按钮：**

  ```css
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>2D转换：缩放scale</title>
      <style>
          li {
              list-style: none;
              float: left;
              width: 30px;
              height: 30px;
              line-height: 30px;
              text-align: center;
              border-radius: 100%;
              border: 1px solid pink;
              margin: 10px;
              transition: transform 0.2s;
          }
  
          li:hover {
              transform: scale(1.2, 1.2);
          }
      </style>
  </head>
  
  <body>
      <ul>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
          <li>5</li>
          <li>6</li>
          <li>7</li>
      </ul>
  </body>
  
  </html>
  ```
  
  file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo11/demo11_5.html
  
  **2D转换综合写法：**
  
  注意：
  
  - 同时使用多个转换时，其格式为：transform: translate() rotate() scale() ...等**（用空格分隔）**；
  - 其顺序会影响转换的效果（先旋转会改变坐标轴方向）；
  - **当我们同时有位移和其他属性的时候，记得要将位移放到最前面。**
  
  ```css
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>2D转换：综合写法</title>
      <style>
          div {
              width: 100px;
              height: 100px;
              background-color: pink;
              transition: transform 1s;
          }
  
          div:hover {
              transform: translate(300px, 0px) rotate(360deg);
          }
      </style>
  </head>
  
  <body>
      <div></div>
  </body>
  
  </html>
  ```
  
  file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo11/demo11_6.html

### 6.CSS3动画

**动画（animation）**是CSS3中具有颠覆性的特征之一，我们可以通过设置多个节点来精确地控制一个或一组动画，常用来实现复杂的动画效果。

相比较过渡，动画可以实现更多变化、更多控制、连续自动播放等效果。

1. 用**keyframes定义动画**（类似于定义类选择器）

   ```css
   @keyframes 动画名称 {
   	0% {
   		width: 100px;
   	}
   	100% {
   		width: 200px;
   	}
   }
   ```

   **动画序列：**

   - **0%是动画的开始，100%是动画的完成。**这样的规则就是动画序列；
   - 在@keyframes中规定某项CSS样式，就能创建由当前样式逐渐变为新样式的动画效果；
   - 动画是使元素从一种样式逐渐变为另一种样式的效果。您可以改变任意多的样式任意多的次数；
   - 请用百分比来规定变化发生的时间，或用关键词"**from**"和"**to**"（等同于0%和100%）。

2. **调用动画**

   ```css
   .div {
   	/* 调用动画 */
   	animation-name: 动画名称；
   	/* 持续时间 */
   	animation-duration: 持续时间;
   }
   ```

   ```css
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>CSS3动画</title>
       <style>
           /* 定义动画 */
           @keyframes move {
   
               /* 开始状态 */
               0% {
                   transform: translate(0, 0);
               }
               /* 关键帧百分比需要是整数，是总时间的划分 */
               25% {
                   transform: translate(1000px, 0);
               }
   
               50% {
                   transform: translate(1000px, 500px);
               }
   
               75% {
                   transform: translate(0, 500px);
               }
   
               /* 结束状态 */
               100% {
                   transform: translate(0px, 0px);
               }
           }
   
           div {
               width: 200px;
               height: 200px;
               background-color: pink;
               /* 调用动画 */
               animation-name: move;
               /* 持续时间 */
               animation-duration: 8s;
           }
       </style>
   </head>
   
   <body>
       <div></div>
   </body>
   
   </html>
   ```

3. **动画常见属性**

   | 属性                      | 描述                                                         |
   | ------------------------- | ------------------------------------------------------------ |
   | **@keyframes**            | **规定动画**                                                 |
   | animation                 | 所有动画属性的简写属性，除了animation-play-state属性         |
   | **animation-name**        | **规定@keyframes动画的名称（必须）**                         |
   | **animation-duration**    | **规定动画完成一个周期所花费的时间（秒s/毫秒ms），默认是0（必须）** |
   | animation-timing-function | 规定动画的速度曲线，默认为ease，linear（匀速）               |
   | animation-delay           | 规定动画何时开始（延迟），默认是0                            |
   | animation-iteration-count | 规定动画播放的次数，默认是1，还有**infinite（无限循环）**    |
   | animation-direction       | 规定动画是否在下一周期逆向播放，默认是normal，**逆播放alternate** |
   | animation-play-state      | 规定动画是否正在运行或暂停，默认为running，暂停为pause       |
   | animation-fill-mode       | 规定动画结束后状态，保持forwards，回到起始backwards          |

4. **动画简写**

   ```css
   animation: 动画名称 持续时间 运动曲线 何时开始 播放次数 是否反方向 动画结束状态;
   ```

   - 简写属性不包含animation-play-state；
   - 暂停动画：animation-play-state: pause;常与鼠标经过等配合使用；
   - 实现动画重新走回来，而不是直接跳回来的效果：animation-direction: alternate;；
   - 动画结束后，停在结束位置：animation-fill-mode: forwards;。

5. **大数据热点图案例**

   ```css
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>大数据热点图</title>
       <style>
           body {
               background-color: black;
           }
   
           .map {
               position: relative;
               width: 747px;
               height: 617px;
               background: url(./images/map.png);
               margin: 0 auto;
           }
   
           .city {
               position: absolute;
               top: 227px;
               right: 193px;
           }
   
           .dotted {
               width: 8px;
               height: 8px;
               background-color: #09f;
               border-radius: 100%;
           }
   
           /* 属性选择器 */
           .city div[class^="pulse"] {
               position: absolute;
               /* 保证波纹在父盒子最中央 */
               top: 50%;
               left: 50%;
               transform: translate(-50%, -50%);
               width: 8px;
               height: 8px;
               border-radius: 100%;
               box-shadow: 0 0 12px #009dfd;
               /* 调用动画 */
               animation-name: pulse;
               /* 持续时间 */
               animation-duration: 1.2s;
               /* 无限循环 */
               animation-iteration-count: infinite;
               /* 速度曲线 */
               animation-timing-function: linear;
               /* 结束状态保持 */
               animation-fill-mode: forwards;
           }
   
           .city .pulse2 {
               animation-delay: 0.4s;
           }
   
           .city .pulse3 {
               animation-delay: 0.8s;
           }
   
           /* 水波纹扩散动画 */
           @keyframes pulse {
               0% {}
   
               70% {
                   /* 用scale放大了话会同时将阴影放大，效果不理想 */
                   /* transform: scale(4, 4); */
                   width: 40px;
                   height: 40px;
                   /* 透明度 */
                   opacity: 1;
               }
   
               100% {
                   width: 70px;
                   height: 70px;
                   opacity: 0;
               }
           }
       </style>
   </head>
   
   <body>
       <div class="map">
           <div class="city">
               <div class="dotted"></div>
               <div class="pulse1"></div>
               <div class="pulse2"></div>
               <div class="pulse3"></div>
           </div>
       </div>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo12/demo12_2.html

6. **速度曲线细节**

   | 属性值      | 描述                                                         |
   | ----------- | ------------------------------------------------------------ |
   | linear      | 匀速，动画从头到尾的速度是相同的                             |
   | ease        | 默认，动画从低速开始，然后加快，在结束前变慢                 |
   | ease-in     | 动画从低速开始                                               |
   | ease-out    | 动画以低速结束                                               |
   | ease-in-out | 动画以低速开始和结束                                         |
   | steps()     | 指定时间函数中的间隔数量（步长），就是分几步来完成我们的动画 |

   **打字机效果：**

   ```css
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>打字机效果</title>
       <style>
           body {
               background-color: black;
           }
   
           div {
               font-size: 20px;
               width: 0;
               height: 30px;
               line-height: 30px;
               color: #fff;
               /* 动画调用 */
               animation-name: w;
               /* 持续时间 */
               animation-duration: 4s;
               /* 速度曲线 */
               animation-timing-function: steps(10);
               /* 结束状态 */
               animation-fill-mode: forwards;
               /* 强制文字一行内显示 */
               white-space: nowrap;
               /* 溢出隐藏 */
               overflow: hidden;
           }
   
           @keyframes w {
               0% {
                   width: 0;
               }
   
               100% {
                   width: 200px;
               }
           }
       </style>
   </head>
   
   <body>
       <div>生命是华丽错觉</div>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo12/demo12_3.html

   **奔跑北极熊：**

   ```css
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>奔跑的北极熊</title>
       <style>
           body {
               position: relative;
               background-color: #ccc;
           }
   
           .bear {
               position: absolute;
               width: 200px;
               height: 100px;
               background: url(./images/bear.png);
               animation: bear 1s steps(8) infinite, move 4s linear forwards;
           }
   
           /* 熊本身走路的动作 */
           @keyframes bear {
               0% {
                   background-position: 0 0;
               }
   
               100% {
                   background-position: -1600px 0;
               }
           }
   
           /* 熊走到中间 */
           @keyframes move {
               0% {
                   left: 0;
               }
   
               100% {
                   left: 50%;
                   transform: translateX(-50%);
               }
           }
       </style>
   </head>
   
   <body>
       <div class="bear"></div>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo12/demo12_4.html

### 7.CSS33D转换

1. **三维坐标系**

   ![image-20211019191102828](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211019191102828.png)

   **注意：y轴正方向是往下！z轴往屏幕外为正，往内为负。**

2. **3D位移：translate3D**

   ```css
   /* x轴移动 */
   transform: translateX(x);
   /* y轴移动 */
   transform: translateY(y);
   /* z轴移动，translateZ一般用px单位 */
   transform: translateZ(z);
   
   transform: translate3d(x, y, z);
   ```

3. **3D旋转rotate3d**

   3D旋转指让元素在三维平面内沿着**x轴、y轴、z轴或自定义轴**进行旋转。

   ```css
   transform: rotateX(度数);
   transform: rotateY(度数);
   transform: rotateZ(度数);
   /* 沿自定义轴旋转 */
   transform: rotate3d(x,y,z,deg);
   ```

   旋转方向遵循**左手准则**：

   ![image-20211019195036428](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211019195036428.png)

   **沿自定义轴旋转（了解）：**

   ```css
   /* x y z表示旋转轴的矢量，表示你是否希望沿着该轴旋转，最后一个表示旋转的角度 */
   trasform: rotate3d(x,y,z,deg);
   ```

   旋转轴的矢量：

   ```css
   transform: rotate3d(1,1,0,45deg);
   ```

   ![image-20211019195828120](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211019195828120.png)

4. **透视perspective**

   - 通过使用透视在网页中产生3D效果（添加**立体效果**）；
   - 透视也称为**视距**：人的眼睛到屏幕的距离，**距离视觉点越近在电脑平面中成像越大，反之越小**；
   - 透视的单位是像素px；

   - 透视**写在被观察元素的父盒子上面**：d，视距，z，图像距离屏幕的距离。视距越小，立体感会越强。

     ![image-20211019192911040](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211019192911040.png)

5. **3D呈现transform-style**

   - transform-style 控制子元素是否开启三维立体环境；
   - **transform-style: flat;** 子元素不开启三维立体空间（默认）；
   - **transform-style:  preserve-3d;** 子元素开启立体空间；
   - **代码写在父级**，但影响的是子盒子。

   ```css
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>3D转换：呈现</title>
       <style>
           body {
               perspective: 500px;
           }
   
           .box {
               position: relative;
               width: 200px;
               height: 200px;
               margin: 100px auto;
               transition: all 2s;
               transform-style: preserve-3d;
           }
   
           .box:hover {
               transform: rotateY(60deg);
   
           }
   
           .box div {
               position: absolute;
               top: 0;
               left: 0;
               width: 100%;
               height: 100%;
               background-color: pink;
           }
   
           .box div:last-child {
               background-color: purple;
               transform: rotateX(60deg);
           }
       </style>
   </head>
   
   <body>
       <div class="box">
           <div></div>
           <div></div>
       </div>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo13/demo13_2.html

6. 案例1：两面翻转的盒子

   ```css
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>两面翻转的盒子</title>
       <style>
           body {
               perspective: 500px;
           }
   
           .box {
               position: relative;
               width: 300px;
               height: 300px;
               margin: 100px auto;
               transition: transform 1s;
               transform-style: preserve-3d;
           }
   
           .front,
           .back {
               position: absolute;
               width: 100%;
               height: 100%;
               border-radius: 100%;
               text-align: center;
               line-height: 300px;
               color: #fff;
           }
   
           .front {
               background-color: pink;
               z-index: 1;
           }
   
           .back {
               background-color: purple;
               transform: rotateY(180deg);
           }
   
           .box:hover {
               transform: rotateY(180deg);
           }
       </style>
   </head>
   
   <body>
       <div class="box">
           <div class="front">黑马程序员</div>
           <div class="back">黑马程序员</div>
       </div>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo13/demo13_3.html

7. 案例2：3D导航栏

   ![image-20211019205846732](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211019205846732.png)

   ```css
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>3D导航栏</title>
       <style>
           li {
               float: left;
               list-style: none;
               width: 120px;
               height: 35px;
               perspective: 500px;
               margin: 0 10px;
               text-align: center;
               line-height: 35px;
           }
   
           .box {
               position: relative;
               width: 100%;
               height: 100%;
               transform-style: preserve-3d;
               transition: transform .4s;
           }
   
           .front,
           .bottom {
               position: absolute;
               left: 0;
               top: 0;
               width: 100%;
               height: 100%;
           }
   
           .front {
               background-color: pink;
               z-index: 1;
               /* z轴移动只能用px做单位 */
               transform: translateZ(17.5px);
           }
   
           .bottom {
               background-color: purple;
               /* 存在移动时尽量先移动（旋转后轴会改变） */
               transform: translateY(50%) rotateX(-90deg);
           }
   
           .box:hover {
               transform: rotateX(90deg);
           }
       </style>
   </head>
   
   <body>
       <ul>
           <li>
               <div class="box">
                   <div class="front">黑马程序员</div>
                   <div class="bottom">黑马程序员</div>
               </div>
           </li>
           <li>
               <div class="box">
                   <div class="front">黑马程序员</div>
                   <div class="bottom">黑马程序员</div>
               </div>
           </li>
           <li>
               <div class="box">
                   <div class="front">黑马程序员</div>
                   <div class="bottom">黑马程序员</div>
               </div>
           </li>
           <li>
               <div class="box">
                   <div class="front">黑马程序员</div>
                   <div class="bottom">黑马程序员</div>
               </div>
           </li>
           <li>
               <div class="box">
                   <div class="front">黑马程序员</div>
                   <div class="bottom">黑马程序员</div>
               </div>
           </li>
           <li>
               <div class="box">
                   <div class="front">黑马程序员</div>
                   <div class="bottom">黑马程序员</div>
               </div>
           </li>
       </ul>
   </body>
   
   </html>
   ```

8. 案例3：旋转木马

   ![image-20211019210126734](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211019210126734.png)

   ```css
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>旋转木马</title>
       <style>
           body {
               perspective: 1000px;
           }
   
           section {
               position: relative;
               width: 300px;
               height: 200px;
               margin: 100px auto;
               transform-style: preserve-3d;
               animation-name: rotate;
               animation-duration: 4s;
               animation-timing-function: linear;
               animation-iteration-count: infinite;
           }
   
           section div {
               position: absolute;
               top: 0;
               left: 0;
               width: 100%;
               height: 100%;
               background: url(./images/dog.jpg);
           }
   
           section div:nth-child(1) {
               transform: translateZ(200px);
           }
   
           section div:nth-child(2) {
               transform: rotateY(-90deg) translateZ(200px);
           }
   
           section div:nth-child(3) {
               transform: rotateY(180deg) translateZ(200px);
           }
   
           section div:nth-child(4) {
               transform: rotateY(90deg) translateZ(200px);
           }
   
           @keyframes rotate {
               0% {
                   transform: rotateY(0deg);
               }
   
               100% {
                   transform: rotateY(180deg);
               }
           }
       </style>
   </head>
   
   <body>
       <section>
           <div></div>
           <div></div>
           <div></div>
           <div></div>
       </section>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo13/demo13_5.html

# 广义的HTML5

1. 广义的HTML5是HTML5本身+CSS3+JavaScript；
2. 这个集合有时成为HTML5和朋友们，通常缩写为HTML5；
3. 虽然HTML5的一些特性仍然不被某些浏览器支持，但它是一种发展趋势。
4. HTML5 MDN介绍：https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML

# 品优购项目

## 一、项目搭建

1. 需要创建如下文件夹：

   | 名称             | 说明     |
   | ---------------- | -------- |
   | 项目文件夹       | shopping |
   | 样式类图片文件夹 | images   |
   | 样式文件夹       | css      |
   | 产品类图片文件夹 | upload   |
   | 字体类文件夹     | fonts    |
   | 脚本文件夹       | js       |

2. 需要创建如下文件：

   | 名称              | 说明       |
   | ----------------- | ---------- |
   | 首页              | index.html |
   | CSS初始化样式文件 | base.css   |
   | CSS公共样式文件   | common.css |

## 二、favicon图标

**favicon.ico**一般用于作为缩略的网站标志，显示在浏览器的地址栏或标签上。

目前主要的浏览器都支持favicon.ico图标。

![image-20210924172221188](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20210924172221188.png)

1. 制作favicon图标
   - 将品优购图标切成png图片；
   - 借助第三方网站将png图片转换为ico图标，例如 比特虫：http://www.bitbug.net/ ；
   
2. 将favicon图标放到网站根目录

3. 在HTML页面引入favicon图标

   在html页面中的<head></head>元素之间引入代码：

   ```css
   <link rel="shortcut icon" href="favicon.ico" type="image/x-icon"/>
   ```

## 三、网站TDK三大标签SEO优化

**SEO（Search Engine Optimization）**汉译为**搜索引擎优化**，是一种利用搜索引擎的规则提高网站在有关搜索引擎内自然排名的方式。

SEO的目的是对网站进行深度优化，帮助网站获取免费的流量，进而在搜索引擎上提升网站的排名、提高网站知名度。

页面必须有三个标签用来符合SEO优化：

- **title**

  网站标题。title具有不可替代性，是我们页内的第一个重要标签，是搜索引擎了解网页的入口和对网页主题归属的最佳判断点。

  建议：**网站名（产品名）-网站的介绍**（尽量不要超过30个汉字）

  例如：

  - 京东（JD.COM）-综合网购首选-正品低价、品质保障、配送及时、轻松购物！
  - 小米商城-小米5s、红米Note4、小米MIX、小米笔记本官方网站

- **description**

  简要说明网站主要功能。

  建议：description作为网站的总体业务和主题概括，多采用“我们是……”、“我们提供……”、“xxx网作为……”、“电话：010……”之类语句。

  例如：

  - <meta name="description" content="京东JD.COM-专业的综合往上购物商城，销售家电、数码通讯、电脑、家居百货、服装服饰、母婴、图书、食品等数万个品牌优质商品。便捷、诚信的服务，为您提供愉悦的往上购物体验！" />

- **keyword**

  页面关键词，是搜索引擎的关注点之一。

  keywords最好限制为6~8个关键词，关键词之间用英文逗号隔开，采用**关键词1, 关键词2**的形式。

  例如：

  <meta name="keywords" content="网上购物,网上商城,手机,笔记本,电脑,MP3,CD,VCD,DV,相机,数码,配件,手表,存储卡,京东" />

## 四、首页制作

1. 常用模块类命名

   | 名称             | 说明                  |
   | ---------------- | --------------------- |
   | 快捷导航栏       | shortcut              |
   | 头部             | header                |
   | 标志             | logo                  |
   | 购物车           | shopcar               |
   | 搜索             | search                |
   | 热点词           | hotwrods              |
   | 导航             | nav                   |
   | 导航左侧         | dropdown 包含 .dd .dt |
   | 导航右侧         | navitems              |
   | 页面底部         | footer                |
   | 页面底部服务模块 | mod_service           |
   | 页面底部帮助模块 | mod_help              |
   | 页面底部版权模块 | mod_copyright         |

2. LOGO SEO优化

   - logo里面**首先放一个h1标签**，目的是为了提权，告诉搜索引擎，这个地方很重要；
   - h1里里面再放一个**链接**，用于返回首页，把**logo作为链接的背景图片**即可；
   - 为了让搜索引擎收录我们，**链接里面要放文字（网站名称），但是文字不要显示出来**。
     - 方法1：text-indent 将文字移到盒子外面（text-indent: -9999px），然后overflow: hidden;
     - 方法2：font-size: 0;
   - 给链接添加一个**title属性**，这样鼠标放到logo上时就可以看到提示文字。
   
3. 选项卡

   原理：

   ![image-20211008230429709](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211008230429709.png)

# Web服务器

**服务器**（主机）是提供个计算服务的设备，**它也是一台计算机**。在网络环境下，根据服务器提供的服务类型不同，服务器又分为文件服务器、数据库服务器、应用程序服务器、**Web服务器**等。

**Web服务器一般指网站服务器**，是指驻留于因特网上某种类型计算机的程序，可以向浏览器等Web客户端提供文档，也可以放置网站文件，让全世界浏览；也可以防止数据文件，供全世界下载。

以下服务器为我们主要指的Web服务器：

根据服务器在网络中所在的位置不同，又可以分为**本地服务器**和**远程服务器**。

- 本地服务器

  将自己的电脑设置为本地服务器。主要在局域网中访问。

- 远程服务器

  远程服务器通常是别的公司为我们提供的一台电脑（主机），我们只要把网站项目上传到这台电脑上，任何人就都可以利用**域名**访问我们的网站了。

  比如域名www.mi.com 可以访问小米网站

**将自己的网站上传到远程服务器：**

注意：一般稳定的服务器都是需要收费的，比如阿里云。

推荐免费远程服务器（免费空间）：http://free.3v.do/

1. 在免费空间网站注册账号；
2. 记录主机名、用户名、密码、域名；
3. 利用cutftp软件上传网站到远程服务器；
4. 在浏览器中输入域名，即可访问品优购网站。

# 浏览器私有前缀

浏览器私有前缀是为了兼容老版本的写法，比较新版本的浏览器无须添加。

1. 私有前缀

   - -moz-：firefox
   - -ms-：IE
   - -webkit-：Safari、Chrome
   - -o-：Opera

2. 提倡写法

   ```css
   -moz-border-radius: 10px;
   -webkit-border-radius: 10px;
   -o-border-radius: 10px;
   border-radius: 10px;
   ```

# 移动端基础

## 一、浏览器现状

- PC端常见浏览器：360、谷歌、火狐、QQ、百度、搜狗、IE；

- 移动端常见浏览器：UC、QQ、欧朋、百度、360、谷歌、搜狗、猎豹……

国内的UC、QQ以及百度等手机浏览器都是根据Webkit修改过来的内核，国内尚且没有自主研发的内核。

**总结：兼容移动端主流浏览器，处理Webkit内核浏览器即可。**

## 二、手机屏幕现状

- 移动端设备屏幕尺寸繁多，碎片化严重；
- Android：480×800,480×854，540×960,720×1280,1080×1920等；
- IOS：640×960,640×1136,750×1334,1242×2208；
- 由于常用尺寸单位为px，开发者无需关注分辨率。

## 三、移动端调试方法

- Chrome DevTools（谷歌浏览器）模拟手机调试；

  ![image-20211019233343364](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211019233343364.png)

- 搭建本地Web服务器，使手机和服务器处于同一局域网内，通过手机访问；

- 使用外网服务器，直接通过IP或域名访问。

# 视口

**视口（Viewport）**就是显示页面内容的屏幕区域。视口可以分为布局视口、视觉视口和**理想视口**。

## 一、布局视口 Layout Viewport

- 一般移动端设备都默认设置了一个布局视口，用于解决早期PC端页面在手机上显示的问题；
- IOS、Android基本都将这个视口分辨率设置在980px，所以PC上的网页大多都能在手机上呈现，只不过元素看起来很小，一般默认可以通过手动缩放网页。

## 二、视觉视口 Visual  Viewport

- 指的是用户正在看到的**网站的区域**；
- **我们可以通过缩放去操作视觉视口**，这并不会影响布局视口，布局视口仍然保持着原来的宽度。

## 三、理想视口 Ideal  Viewport

- 为了使网站在移动端能有理想的浏览宽度而设定，使用户能在屏幕内看到完整且清晰的网页；
- 需要手动添写meta视口标签通知浏览器操作；
- **meta视口标签**的主要目的：使布局视口的宽度和理想视口的宽度一致。

**meta视口标签：**

```html
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

| 属性          | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| width         | 宽度设置的是viewport宽度，可以设置**device-width（设备宽度）**特殊值 |
| initial-scale | 初始缩放比，大于0的数字                                      |
| maximum-scale | 最大缩放比，大于0的数字                                      |
| minimum-scale | 最小缩放比，大于0的数字                                      |
| user-scalable | 是否允许用户缩放，yes或no（1或0）                            |

# 二倍图

## 一、物理像素&物理像素比

- **物理像素点（分辨率）**指的是**屏幕显示的最小颗粒**，是物理真实存在的。（由厂商在出厂时即设置好，如苹果6/7/8 屏幕分辨率为750×1334像素）；
- **PC端页面中1px＝1物理像素，而移动端的1px不一定＝1物理像素**（Retina视网膜屏幕显示技术，可以将更多的物理像素点压缩至一块屏幕中，从而达到更高的分辨率的效果，并提高屏幕显示的细腻程度）；
- 1px能显示的物理像素点的个数，称为**物理像素比**或屏幕像素比。

![image-20211020000044178](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211020000044178.png)

## 二、多倍图

- 对于一张50px×50px的图片，在手机Retina屏幕中打开，按照物理像素比就会放大倍数，造成图片的模糊；
- 在标准viewport设置中，使用倍图来提高图片质量，解决在高清设备中模糊的问题；
- 通常使用二倍图，因为iphone6/7/8的影响，甚至还存在三倍图、四倍图的情况，具体看实际开发公司需求；
- 背景图片注意缩放问题。

```css
/*
	当我们需要一个50×50像素的图片，直接放到物理像素比2的iphone8中就会放大2倍（100×100）；
	我们直接放一个100×100的图片，然后手动将图片大小缩小为50×50，这样就可以得到比我们实际需求大2倍的图片，这种方式就是二倍图。 */

/* 以iphone8为例 */
img {
	/* 原始图片 100*100 */
	width:50px;
	height: 50px;
}

.box {
	/* 原始图片100*100 */
	background-size: 50px 50px;
}
```

## 三、背景缩放 background-size

**background-size**属性规定背景图像的尺寸。

```css
background-size: 背景图片宽度 背景图片高度;
/* 省略高度，等比缩放 */
background-size: 背景图片宽度;
```

- 单位：长度 | 百分比（相对于父盒子） | cover | contain；
- cover：将背景图高度宽度等比拉伸，以使背景图像**完全覆盖背景区域**，超出部分则直接隐藏（可能导致图片显示不全）；
- contain：将背景图高度宽度等比拉伸，以使其**宽度或高度完全适应内容区域**（高度或宽度铺满盒子就不再进行拉伸，可能有部分空白区域）。

## 四、多倍图切图

3x、2x、1x分别对应三倍图、二倍图以及一倍图原图：

![image-20211020002904712](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211020002904712.png)

# 移动端开发选择

## 一、移动端开发方案

1. **单独制作**移动端页面（主流）

   如，京东商城手机版、淘宝触屏版、苏宁易购手机版……

   通常情况下，网址域名前面加**m(mobile)**即可打开移动端。

   通过**设备判断**，用户通过移动设备打开的情况，将**跳转到移动端页面**。

   

2. **响应式页面**兼容移动端（其次）

   如，三星手机官网……

   通过**判断屏幕宽度来改变样式**，以适应不同终端。

   缺点：制作麻烦，需要花大量精力去调试兼容性问题。

# 移动端技术解决方案

## 一、移动端浏览器

移动端浏览器基本以Webkit内核为主，因此我们只考虑Webkit的兼容性问题：

- 我们可以放心地使用H5标签以及CSS3样式；
- 同时浏览器的私有前缀我们只需要考虑添加Webkit即可。

## 二、CSS初始化

移动端CSS初始化推荐使用**normalize.css/**

Normalize.css：

- 保护了有价值的默认值；
- 修复了浏览器的BUG；
- 是模块化的；
- 拥有详细的文档。

官网地址：http://necolas.github.io/normalize.css/

## 三、CSS3盒子模型

- 传统模式宽度计算：盒子的宽度=width+border+padding；
- CSS3盒子模型：盒子的宽度=width（包含了border和padding）。

```css
/* CSS3盒子模型 */
box-sizing: border-box;
/* 传统盒子模型 */
box-sizing: content-box;
```

## 四、特殊样式

```css
/* CSS3盒子模型 */
box-sizing: border-box;
-webkit-box-sizing: border-box;
/* 清除点击高亮 */
-webkit-tap-highlight-color: transparent;
/* 清除浏览器默认外观（IOS）*/
-webkit-appearance: none;
/* 禁用长按页面时弹出菜单 */
img,a {
	-webkit-touch-callout: none;
}
```

# 移动端常见布局

## 一、移动端技术选型

### 1.单独制作移动端页面

#### 1）流式布局（百分比布局）

流式布局，即百分比布局，也称非固定像素布局；

通过**盒子的宽度设置成百分比**的方式来根据屏幕宽度进行伸缩，不受固定像素的限制，内容向两侧填充；

流式布局方式是移动Web开发使用的较为常见的布局方式。

为保证盒子的内容在合理范围内，设置最大/最小宽度/高度：

- **max-width 最大宽度（max-height 最大高度）**
- **min-width 最小宽度（min-height 最小高度）**



案例：京东移动端首页

1. 设置视口标签以及引入初始化样式文件

   ```css
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0"  user-scalable=no, maximum-scale=1.0
           minimum-scale=1.0>
       <!-- 引入CSS初始化文件 -->
       <link rel="stylesheet" href="css/normalize.css">
       <!-- 引入首页样式文件 -->
       <link rel="stylesheet" href="css/index.css">
       <title>京东移动端首页</title>
   </head>
   ```

2. 常用初始化样式

   ```css
   body {
       width: 100%;
       min-width: 320px;
       max-width: 640px;
       margin: 0 auto;
       background-color: #fff;
       font-size: 14px;
       font-family: -apple-system, Helvetica, sans-serif;
       line-height: 1.5;
       color: #666;
   }
   ```

3. 图片格式

   - DPG图片压缩技术

     京东自主研发推出的DPG图片压缩技术，经测试该技术可直接节省用户近50%的浏览器流量，极大地提升了用户的网页打开速度，能够兼容jpeg，实现全平台、全浏览器的兼容支持，经过内部和外部上万张图片的人眼浏览器测试后发现，压缩后的图片和Webp的清晰度对比没有差距。

   - webp图片格式

     谷歌开发的一种旨在加快图片加载速度的图片格式。图片压缩体积大约只有jpeg的2/3，并能节省大量的服务器宽带资源和数据空间。
   
4. file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo14/index.html

   ![image-20211025224627413](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211025224627413.png)

#### 2）**flex弹性布局**

1. 传统布局与flex弹性布局

   - 传统布局
     - 兼容性好；
     - 布局繁琐；
     - 局限性，不能在移动端很好地布局。
   - flex弹性布局
     - 操作方便，布局极为简单，移动端应用广泛；
     - PC端浏览器支持情况较差；
     - IE11或更低版本，不支持或仅部分支持。
   - 建议
     - PC端采用传统布局；
     - 移动端或不考虑兼容性的PC端页面布局采用flex弹性布局。

2. flex布局原理

   flex是flexible box的缩写，意为“弹性布局”，用来为盒状模型提供最大的灵活性，任何一个容器都可以指定为flex布局。

   - 当我们为父盒子设置flex布局后，子元素的float、clear和vertical-align属性都将失效；
   - 伸缩布局=弹性布局=伸缩盒布局=弹性盒布局=flex布局。

   采用了flex布局的元素，称为flex容器（flex container），简称“容器”。它的所有子元素自动称为容器成员，称为flex项目（flex item），简称“项目”。

   子容器既可以横向排列，也可以纵向排列。

   **总结：通过给父盒子添加flex属性，来控制子盒子的位置和排列方式。**

   ```css
   display: flex;
   ```

3. **flex布局父项常见属性**

   | 属性                | 说明                                                |
   | ------------------- | --------------------------------------------------- |
   | flex-direction      | 设置主轴方向                                        |
   | **justify-content** | **设置主轴上子元素的排列方式**                      |
   | flex-wrap           | 设置子元素是否换行                                  |
   | **align-content**   | **设置侧轴上子元素的排列方式（多行）**              |
   | align-items         | 设置侧轴上的子元素排列方式（单行）                  |
   | flex-flow           | 复合属性，相当于同时设置了flex-direction和flex-wrap |

   1. **flex-direction 设置主轴方向**

      - 主轴与侧轴

        在flex布局中，分为主轴和侧轴两个方向（行和列，x轴和y轴）

        - 默认的主轴方向：x轴方向，水平向右；
        - 默认的侧轴方向：y轴方向，水平向下。

        ![image-20211025011405356](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211025011405356.png)

      - 属性值

        flex-direction属性决定了主轴的方向**（项目的排列方向）**

        | 属性值         | 说明             |
        | -------------- | ---------------- |
        | row            | 默认值，从左往右 |
        | row-reverse    | 从右往左         |
        | column         | 从上往下         |
        | column-reverse | 从下往上         |

   2. **justify-content 设置主轴上子元素排列方式**

      justify-content属性定义了项目在主轴上的对齐方式。

      | 属性值            | 说明                                            |
      | ----------------- | ----------------------------------------------- |
      | flex-start        | 默认值，从头部开始，若主轴是x轴，即从左往右     |
      | flex-end          | 从尾部开始排列                                  |
      | **center**        | **在主轴上居中对齐，若主轴是x轴，实现水平居中** |
      | **space-around**  | **平分剩余空间**                                |
      | **space-between** | **先两边贴边，再平分剩余空间**                  |

   3. **flex-wrap 子元素是否换行**

      默认情况下，项目都排在一条线（轴线）上，不换行（排列不下的情况下，会修改子盒子的宽/高）。

      | 属性值   | 说明           |
      | -------- | -------------- |
      | nowrap   | 默认值，不换行 |
      | **wrap** | **换行**       |

   4. **align-items 设置侧轴上子元素排列方式（单行）**

      align-items属性控制子项在侧轴上的排列方式，在子项为单行的时候使用。

      | 属性值     | 说明           |
      | ---------- | -------------- |
      | flex-start | 从上往下       |
      | flex-end   | 从下往上       |
      | **center** | **居中**       |
      | stretch    | 拉伸（默认值） |

   5. **align-content 设置侧轴上子元素排列方式（多行）**

      设置子项在侧轴上的排列方式，并且**只能用于子项出现换行的情况**，在单行下是没有效果的。

      | 属性值            | 说明                                     |
      | ----------------- | ---------------------------------------- |
      | flex-start        | 默认值，从侧轴的头部开始排列             |
      | flex-end          | 从侧轴的尾部开始排列                     |
      | **center**        | **在侧轴中间显示**                       |
      | **space-around**  | **在侧轴平分剩余空间**                   |
      | **space-between** | **子项在侧轴先两边贴边，再平分剩余空间** |
      | **stretch**       | **设置子项元素高度为平分父元素高度**     |

   6. flex-flow

      flex-flow属性是flex-direction和flex-wrap属性的复合属性。

      ```css
      flex-flow: row wrap;
      ```

4. **flex布局子项常见属性**

   1. **flex属性**

      flex属性定义子项分配**剩余空间**，**用flex来表示子项所占的分数**。

      ```css
      .item {
      	flex: <number>;	/* 默认为0 */
      }
      ```

   2. align-self 控制子项自己在侧轴上的排列方式

      align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。

      默认值为auto，表示继承父元素的align-items属性，若没有父元素，则等同于stretch。

   3. order属性定义项目的排列顺序

      **数值越小，排序越靠前，默认为0。**

      注意：和z-index不一样，z-index数值越大，摆放越靠上。

      ```css
      div span:nth-child(2) {
      /* 默认是0 -1比0小所以在前面 */
      	order: -1;
      }
      ```

5. 案例：携程移动端

   1. 常见flex布局思路

      ![image-20211026003655456](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211026003655456.png)

   2. **背景渐变 linear-gradient**

      背景线性渐变

      ![image-20211026003811344](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211026003811344.png)

      语法：

      ```css
      background: linear-gradient(起始方向, 颜色1, 颜色2, ...);
      
      background: -webkit-linear-gradient(left, red, blue);
      background: -webkit-linear-gradient(left, top, red, blue);
      ```

      注意：

      - 背景渐变**必须添加浏览器的私有前缀**才能生效；
      - 起始方向可以是：**方位名词**或**度数**，默认为top（从上往下渐变）。


#### 3）less+rem适配布局+媒体查询布局

1. rem基础

   - rem单位

     rem（root em）是一个相对单位，类似于em，em是父元素字体大小。

     不同的是，**rem的基准是相对于html元素的字体大小**。

     比如，根元素（html）设置font-size: 12px；非根元素设置width: 2rem;则换成px表示就是width: 24px。

   - rem优点

     通过修改html中文字的大小来改变页面中元素的大小，对页面中的元素进行整体控制。

2. 媒体查询

   媒体查询（Media Query）是CSS3新语法。

   - 使用@media查询，可以针对不同的媒体类型定义不同的样式；
   - **@media可以针对不同的屏幕尺寸设置不同的样式；**
   - 在你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度**重新渲染**；
   - 目前针对很多苹果、Android手机、平板等设备都可以用到媒体查询。

   语法：

   ```css
   @media mediatype and|not|only (media feature) {
   	css-code;
   }
   ```

   - **mediatype 媒体类型：**

     将不同的终端设备划分成不同的类型，称为媒体类型。

     | 值         | 说明                               |
     | ---------- | ---------------------------------- |
     | all        | 用于所有设备                       |
     | print      | 用于打印机和打印预览               |
     | **screen** | 用于电脑屏幕、平板电脑、只能手机等 |

   - **and|not|only 关键字：**

     | 值      | 说明                                               |
     | ------- | -------------------------------------------------- |
     | **and** | 将多个媒体特性连接到一起，相当于”且“，**不可省略** |
     | not     | 排除某个媒体类型，相当于“非”，可以省略             |
     | only    | 指定某个特定的媒体类型，可以省略                   |

   - **media feature 媒体特性：**

     每种媒体类型都具有各自不同的特性，根据不同媒体类型的媒体特性设置不同的显示风格。

     | 值        | 说明                                 |
     | --------- | ------------------------------------ |
     | width     | 定义输出设备中页面可见区域的宽度     |
     | min-width | 定义输出设备中页面最小可见区域的宽度 |
     | max-width | 定义输出设备中页面最大可见区域的宽度 |

   案例：根据页面宽度改变背景颜色

   ```css
   /* 媒体查询可以根据不同的屏幕尺寸改变不同的样式 */
   
   /* 在屏幕上 并且 最大可见区域的宽度 549px 设置我们想要的样式 */
   /* 当屏幕宽度小于540px时 显示背景颜色为蓝色 */
   @media screen and (max-width: 539px) {
   	body {
   		background-color: blue;
   	}
   }
   /* 当屏幕宽度处于540px-970px之间时 显示背景颜色为绿色*/
   @media screen and (min-width: 540px) and (max-width: 969px) {
   	body {
   		background-color: green;
   	}
   }
   /* 根据css的层叠性 写如下代码也ok */
   /* 从小到大写或从大到小写 代码会更加简洁！ */
   /*
   @media screen and (min-width: 540px) {
   	body {
   		background-color: green;
   	}
   }
   */
   /* 当屏幕宽度大于等于970px时 显示背景颜色为红色*/
   @media screen and (min-width: 970px) {
   	body {
   		background-color: red;
   	}
   }
   ```

   案例：rem+媒体查询实现元素动态大小变化

   ```css
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>媒体查询+rem实现元素变化</title>
       <style>
           * {
               margin: 0;
               padding: 0;
           }
   
           @media screen and (min-width: 320px) {
               html {
                   font-size: 50px;
               }
           }
   
           @media screen and (min-width: 640px) {
               html {
                   font-size: 100px;
               }
           }
   
           .top {
               height: 1rem;
               font-size: .5rem;
               background-color: green;
               color: #fff;
               text-align: center;
               line-height: 1rem;
           }
       </style>
   </head>
   
   <body>
       <div class="top">购物车</div>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo16/demo16_1.html

   引入资源：

   当样式比较繁多的时候，我们可以针对不同的媒体使用不同的stylesheets（样式表）。

   原理就是直接**在link中判断设备的尺寸，然后引入不同的css文件**。

   ```css
   <link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css">
   ```

   ```css
   <link rel="stylesheet" media="screen and (min-width: 320px)" href="style320.css">
   <link rel="stylesheet" media="screen and (min-width: 640px)" href="style640.css">
   ```

3. less基础

   CSS的弊端：

   CSS是一门非程序式语言，没有变量、函数、SCOPE（作用域）等概念。

   - CSS需要书写大量看似没有逻辑的代码，CSS冗余度是比较高的；
   - 不方便维护及拓展，不利于复用；
   - CSS没有很好的计算能力（calc有兼容性问题）；
   - 非前端开发工程师往往会因为缺少CSS编写经验而很难写出组织良好且易于维护的CSS代码项目。

   less介绍：

   **less（Leaner Style Sheets）是一门CSS扩展语言，也称为CSS预处理器。**

   作为CSS的一种形式的扩展，它并没有减少CSS的功能，而是在现有的CSS语法上，**为CSS加入了程序式语言的特性（动态特性）**——

   在CSS语法的基础上，引入了变量，Mixin（混入），运算以及函数等功能，大大简化了CSS的编写，并且降低了CSS的维护成本。

   就像它的名称一样，less帮助我们用更少的代码做更多的事。

   less中文网址：http://lesscss.cn/

   常见的CSS预处理器：Sass、Less、Stylus

   less使用：

   1. 新建一个后缀名为**.less**的文件，在该文件中书写less语句。

   2. less变量

      ```less
      @变量名: 值;
      @color: pink;
      @font14: 14px;
      ```

      变量命名规范：

      - 必须以@为变量前缀；
      - 不能包含特殊字符；
      - 不能以数字开头；
      - 大小写敏感。

   3. less编译

      本质上，less包含一套自定义的语法以及一个解析器，用户根据这些语法定义自己的样式规则，这些规则最终会通过解析器，编译生成对应的CSS文件。

      **Easy LESS插件：**

      Easy LESS插件用来把less文件编译为css文件。我们只需要保存.less文件，就会自动生成.css文件。

   4. less嵌套

      ```less
      .header {
      	width: 200px;
      	height: 200px;
      	background-color: pink;
          // 1.less嵌套 子元素的样式直接写到父元素里面
      	a {
      		color: red;
              // 2.伪类选择器、伪元素选贼器、交集选择器 内层选择器的前面需要加&（若有&符号 它就被解析为父元素自身或父元素的伪类）
              &:hover {
                  color: blue;
              }
              &::before {
                  content: '';
              }
      	}
      }
      
      .nav {
          .logo {
              color: green;
          }
      }
      ```

   5. less运算

      less提供了加（+）、减（-）、乘（*）、除（/）算术运算，在less中，任何数字、颜色或者变量都可以参与运算。

      ```less
      //在less中这样写
      @width: (10px +5);
      div {
      	border: @width solid red;
          width: ((@width + 5) * 2);
      }
      ```

      ```css
      /* 生成的css */
      div {
      	border: 15px solid red;
      	width: 40px
      }
      ```

      - 运算符的左右两侧必须敲一个空格隔开；
      - 新版本运算要加括号；
      - 两个数参与运算，若只有一个数有单位，最后的结果以这个单位为准；
      - 两个数参与运算，若两个数都有单位，最后的结果以第一个单位为准。

4. rem适配方案

   使用**媒体查询**根据不同设备比例**设置html字体大小**，然后**页面元素使用rem做尺寸单位**，当html字体大小发生变化时，元素尺寸也同时发生变化，达到等比缩放适配的目的。

   1. rem实际开发适配方案

      - 按照设计稿与设备宽度的比例，动态计算并设置html根标签的font-size大小：（媒体查询）；
      - CSS中，设计稿元素的宽、高、相对位置等取值，按照同等比例换算为rem单位的值。

   2. rem适配方案技术使用（市场主流）

      - 技术方案1：less+媒体查询+rem

        设计稿常见尺寸宽度：

        | 设备             | 常见宽度                                                     |
        | ---------------- | ------------------------------------------------------------ |
        | iphone 4/5       | 640px                                                        |
        | **iphone 6/7/8** | **750px**                                                    |
        | android          | 320px、360px、375px、384px、400px、414px、500px、720px。**大部分4.7~5寸的安卓设备为720px** |

        一般情况下，我们以一套或两套效果图适应大部分的屏幕，放弃极端屏幕或对其降级，牺牲一些效果。

        **基本以750为准。**

        动态设置html标签font-size大小：

        ![image-20211029193546223](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211029193546223.png)

        元素大小取值方法：

        - html font-size = 屏幕宽度 / 划分份数
        - 页面元素的rem值 = 页面元素值（px） / （屏幕宽度 / 划分份数）
        - 页面元素的rem值 = 页面元素值（px） / html font-size

      - 技术方案2：flexible.js+rem

        手机淘宝团队推出的简洁高效的移动端适配库。

        我们再也不需要写不同屏幕的媒体查询，因为flexible.js中做了处理。

        它的原理是把当前设备划分为**十等分**，但是不同设备下，比例还是一致的。

        我们要做的，就是确定好**当前设备的html文字大小**即可。比如当前设计稿为750px，我们只需把html文字大小设置为75px（750px  / 10），页面元素rem值=页面元素px值 / 75。剩余的，由flexible.js计算。

        github地址：https://github.com/amfe/lib-flexible

        

5. 案例：苏宁首页（技术方案1）

   1. 新建index.less文件

      ```less
      // @import 可以把一个样式文件导入另一个样式文件里
      // link 是将一个样式文件引入到html页面中
      @import "common";
      ```

   2. body样式

      ```less
      body {
          min-width: 320px;
          width: 15rem;
          margin: 0 auto;
          line-height: 1.5;
          font-family: Arial, Helvetica, sans-serif;
          background-color: #f2f2f2;
      }
      ```

   3. file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/suning/index.html

6. 案例：苏宁首页（技术方案2）

   1. 在页面中引入js文件

      ```html
      <script src="js/flexible.js"></script>
      ```

   2. VSCode px转换rem插件 **cssrem**

      ![image-20211029222638448](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211029222638448.png)

      设置转换基准值：
   
      ![image-20211029222703184](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211029222703184.png)
   
   3. file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/suning%20copy/index.html

#### 4）混合布局

### 2.响应式页面兼容移动端

#### 1）媒体查询+Bootstrap

1. 响应式开发

   - 原理

     使用**媒体查询**针对不同宽度的设备进行布局和样式的设置，从而达到适配不同设备的目的。

   - 响应式布局容器

     响应式需要一个父级作为布局容器，来配合子级元素来实现变化效果。

     在不同的屏幕下，通过媒体查询来改变这个布局容器的大小，再改变里面子元素的排列方式和大小，从而实现不同屏幕下，看到不同的页面布局和样式变化。

     | 设备划分                 | 尺寸区间             | 宽度设置 |
     | ------------------------ | -------------------- | -------- |
     | 超小屏幕（手机）         | < 768px              | 100%     |
     | 小屏设备（平板）         | >= 768px ~ < 992px   | 750px    |
     | 中等屏幕（桌面显示器）   | >= 992px ~ <  1200px | 910px    |
     | 宽屏设备（大桌面显示器） | >= 1200px            | 1170px   |

   - 案例：响应式导航栏

     ```html
     <!DOCTYPE html>
     <html lang="en">
     
     <head>
         <meta charset="UTF-8">
         <meta http-equiv="X-UA-Compatible" content="IE=edge">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>响应式导航栏</title>
         <style>
             * {
                 margin: 0;
                 padding: 0;
             }
     
             ul {
                 list-style: none;
             }
     
             .container {
                 width: 750px;
                 margin: 0 auto;
             }
     
             .container ul li {
                 float: left;
                 width: 93.75px;
                 height: 30px;
                 background-color: green;
             }
     
             @media screen and (max-width: 767px) {
                 .container {
                     width: 100%;
                 }
     
                 .container ul li {
                     width: 33.33%;
                 }
             }
         </style>
     </head>
     
     <body>
         <div class="container">
             <ul>
                 <li>导航栏1</li>
                 <li>导航栏2</li>
                 <li>导航栏3</li>
                 <li>导航栏4</li>
                 <li>导航栏5</li>
                 <li>导航栏6</li>
                 <li>导航栏7</li>
                 <li>导航栏8</li>
             </ul>
         </div>
     </body>
     
     </html>
     ```

     file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo17/demo17_2.html

2. Bootstrap前端开发框架

   - 简介

     Bootstrap来自Twitter，是目前最受欢迎的前端框架。Bootstrap基于HTML、CSS和JavaScript，简洁灵活，使得Web开发更加快捷。

     - 中文官网：http://www.bootcss.com/
     - 官网：http://getbootstrap.com/
     - 推荐使用：http://bootstrap.css88.com/

     框架：顾名思义即一套架构，它有 比较完整的网页功能解决方案，而且控制权在框架本身，有预制样式库、组件和插件。使用者要按照框架所规定的某种规范进行开发。
     
   - 优点

     - 标准化的html+css编码规范
     - 提供了一套简洁、直观、强悍的组件
     - 有自己的生态圈，不断地更新迭代
     - 让开发更简单，提高了开发的效率

   - Bootstrap使用

     1. 创建文件夹结构

        ![image-20211108195315695](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211108195315695.png)

        ![image-20211108195714545](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211108195714545.png)

     2. 创建html骨架结构

        ```html
        <!doctype html>
        <html lang="zh-CN">
        
        <head>
            <meta charset="utf-8">
            <meta http-equiv="X-UA-Compatible" content="IE=edge">
            <meta name="viewport" content="width=device-width, initial-scale=1">
            <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
            <title>Bootstrap 101 Template</title>
        
            <!-- Bootstrap -->
            <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css"
                integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">
        
            <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
            <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
            <!--[if lt IE 9]>
              <script src="https://cdn.jsdelivr.net/npm/html5shiv@3.7.3/dist/html5shiv.min.js"></script>
              <script src="https://cdn.jsdelivr.net/npm/respond.js@1.4.2/dest/respond.min.js"></script>
            <![endif]-->
        </head>
        
        <body>
            <h1>你好，世界！</h1>
        
            <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
            <script src="https://cdn.jsdelivr.net/npm/jquery@1.12.4/dist/jquery.min.js"
                integrity="sha384-nvAa0+6Qg9clwYCGGPpDQLVpLNn0fRaROjHqs13t4Ggj3Ez50XnGQqc/r8MhnRDZ" crossorigin="anonymous">
            </script>
            <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
            <script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"
                integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd" crossorigin="anonymous">
            </script>
        </body>
        
        </html>
        ```

     3. 引入相关样式文件

        ```html
        /* Bootstrap 核心样式 */
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
        ```

     4. 书写内容

        - 直接拿Bootstrap预先定义好的样式来使用（Bootstrap通过类名来定义样式）；
        - 我们可以利用自己书写的样式去覆盖原来的样式，修改Bootstrap原来的样式，注意权重问题；
        - 学好Bootstrao的关键在于，**它定义了哪些样式，以及这些样式能实现什么样的效果**。

   - 布局容器

     Bootstrap需要为页面内容和栅格系统包裹一个.container容器，Bootstrap预先定义好了这个类，提供了两个作此用处的类。

     1. container类
        - 用于**固定宽度**并支持**响应式布局**的容器；
        - 大屏（>=1200px），宽度定为1170px；
        - 中屏（>=992px），宽度定为970px；
        - 小屏（>=768px），宽度定为750px；
        - 超小屏（100%）。
     2. container-fluid类
        - 用于**100% 宽度，占据全部视口（viewport）的容器**；
        - 占据全部视口（Viewport）的容器；
        - 适合于单独做移动端开发

3. Bootstrap栅格系统

   - 栅格系统简介

     栅格系统（gridsystems），也有人将其翻译为网格系统，它是指将页面布局划分为等宽的列，然后通过列数的定义来模块化页面的布局。

     Bootstrap提供了一套响应式、移动设备优先的流式栅格系统，系统会自动将container容器分为**最多12列**。

   - 栅格选项参数

     栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，你的内容就可以放入这些创建好的布局中。

     ![image-20211108202911940](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211108202911940.png)

     - 行（row）必须放到container布局容器里面；
     - 我们实现列的平均划分，需要给列添加**类前缀**；
     - xs（extra small）：超小；sm（small）：小；md（medium）：中等；lg（large）：大；
     - 列（column）大于12，多余的列所在的元素将被作为一个整体另起一行排列；
     - 每一列默认有15像素的padding；
     - 可以同时为一列指定多个设备的类名，以便划分不同份数，例如，class="col-md-4 col-sm-6"。

     ```html
     <div class="container">
             <div class="row">
                 <div class="col-lg-3">1</div>
                 <div class="col-lg-3">2</div>
                 <div class="col-lg-3">3</div>
                 <div class="col-lg-3">4</div>
             </div>
             <!-- 若孩子的份数相加等于12 则孩子能占满整个container容器的宽度 -->
             <div class="row">
                 <div class="col-lg-6">1</div>
                 <div class="col-lg-2">2</div>
                 <div class="col-lg-2">3</div>
                 <div class="col-lg-2">4</div>
             </div>
             <!-- 若孩子的份数相加小于12 则孩子占不满整个container宽度 留下空白 -->
             <div class="row">
                 <div class="col-lg-6">1</div>
                 <div class="col-lg-2">2</div>
                 <div class="col-lg-2">3</div>
                 <div class="col-lg-1">4</div>
             </div>
             <!-- 若孩子的份数相加大于12 则大于12的部分另起一行显示 -->
             <div class="row">
                 <div class="col-lg-6">1</div>
                 <div class="col-lg-2">2</div>
                 <div class="col-lg-2">3</div>
                 <div class="col-lg-3">4</div>
             </div>
         </div>
     ```

   - 列嵌套

     栅格系统内置的栅格系统将内容再次嵌套。简单理解就是一个列内再分成若干份小列。

     我们可以通过添加一个新的.row元素和一系列**.col-sm-*** 元素到已经存在的.col-sm-* 元素内。

     ![image-20211108204644963](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211108204644963.png)

     ```html
     <div class="container">
             <div class="row">
                 <div class="col-md-4">
                     <!-- 在做嵌套的时候 最好加一个新的行row 这样可以取消父元素的padding值 而且高度继承父亲 -->
                     <div class="row">
                         <div class="col-md-6">a</div>
                         <div class="col-md-6">b</div>
                     </div>
                 </div>
                 <div class="col-md-4">2</div>
                 <div class="col-md-4">3</div>
             </div>
         </div>
     ```

   - 列偏移

     使用**.col-md-offset-*** 类可以将列向右侧偏移。这些类实际是通过使用*选择器为当前元素增加了左侧的边距（margin）。

     ![image-20211108205745288](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211108205745288.png)
     
     ```html
     <div class="container">
             <div class="row">
                 <!-- 左右对齐 -->
                 <div class="col-md-3">左侧</div>
                 <!-- 偏移的份数 = 12 - 两个盒子的份数 = 6 -->
                 <div class="col-md-3 col-md-offset-6">右侧</div>
             </div>
             <div class="row">
                 <!-- 居中对齐 -->
                 <!-- 偏移份数 = (12 - 盒子份数) / 2 = 4 -->
                 <div class="col-md-4 col-md-offset-4">居中</div>
             </div>
         </div>
     ```
     
   - 列排序

     通过使用**.col-md-push-*** 和**.col-md-pull-*** 类就可以很容易地改变列的顺序。

     ![image-20211109195903386](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211109195903386.png)

     ```html
     <div class="container">
             <div class="row">
                 <div class="col-md-4">左侧</div>
                 <div class="col-md-8">右侧</div>
             </div>
             <div class="row">
                 <div class="col-md-4 col-md-push-8">左侧</div>
                 <div class="col-md-8 col-md-pull-4">右侧</div>
             </div>
         </div>
     ```

   - 响应式工具

     为了加快对移动设备的页面开发工作，**利用媒体查询功能**，并使用这些工具类可以方便地针对不同设备**隐藏页面内容**。

     | 类名       | 超小屏 | 小屏 | 中屏 | 大屏 | 说明                                         |
     | ---------- | ------ | ---- | ---- | ---- | -------------------------------------------- |
     | .hidden-xs | 隐藏   | 可见 | 可见 | 可见 | 在超小屏（手机）下隐藏，其他屏幕下显示       |
     | .hidden-sm | 可见   | 隐藏 | 可见 | 可见 | 在小屏（平板）下隐藏，其他屏幕下显示         |
     | .hidden-md | 可见   | 可见 | 隐藏 | 可见 | 在中屏（桌面显示器）下隐藏，其他屏幕下显示   |
     | .hidden-lg | 可见   | 可见 | 可见 | 隐藏 | 在大屏（大桌面显示器）下隐藏，其他屏幕下显示 |

     与之相反的是**visible-xs visible-sm visible-md visible-lg**，用于**显示某个页面内容**。

     | 类名        | 超小屏 | 小屏 | 中屏 | 大屏 | 说明           |
     | ----------- | ------ | ---- | ---- | ---- | -------------- |
     | .visible-xs | 可见   | 隐藏 | 隐藏 | 隐藏 | 只在超小屏显示 |
     | .visible-sm | 隐藏   | 可见 | 隐藏 | 隐藏 | 只在小屏显示   |
     | visible-md  | 隐藏   | 隐藏 | 可见 | 隐藏 | 只在中屏显示   |
     | visible-lg  | 隐藏   | 隐藏 | 隐藏 | 可见 | 只在大屏显示   |

4. 案例：阿里百秀首页

   1. 需求分析

      - 技术选型

        方案：响应式页面开发

        技术：Bootstrap框架

        设计图：1280px设计尺寸

      - 页面布局分析

        ![image-20211109202007803](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211109202007803.png)

      - 屏幕划分

        - 中屏幕和大屏幕布局一致，因此我们列定义为col-md-*即可；
        - 小屏幕与超小屏幕布局都有发生变化，因此我们需要为小及超小屏幕根据需求改变布局；
        - 策略：先布局md及以上的PC端，再根据实际需求修改小屏幕和超小屏幕的特殊布局样式。

   2. 页面制作

      - container宽度修改

        设计效果图采取的是1280px，而Bootstrap中container宽度最大为1170px，因此我们需要手动修改container的宽度。

        ```css
        /* 修改container的最大宽度为1280 */
        @media screen and (min-width: 1280px) {
            .container {
                width: 1280px;
            }
        }
        ```
        
      
   3. ```html
      <!doctype html>
      <html lang="zh-CN">
      
      <head>
          <meta charset="utf-8">
          <meta http-equiv="X-UA-Compatible" content="IE=edge">
          <meta name="viewport" content="width=device-width, initial-scale=1">
          <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
          <title>阿里百秀</title>
      
          <!-- Bootstrap -->
          <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css"
              integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">
          <link rel="stylesheet" href="./css/index.css">
      
          <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
          <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
          <!--[if lt IE 9]>
            <script src="https://cdn.jsdelivr.net/npm/html5shiv@3.7.3/dist/html5shiv.min.js"></script>
            <script src="https://cdn.jsdelivr.net/npm/respond.js@1.4.2/dest/respond.min.js"></script>
          <![endif]-->
      </head>
      
      <body>
          <div class="container">
              <div class="row">
                  <header class="col-md-2">
                      <div class="logo">
                          <a href="#">
                              <img src="./images/logo.png" alt="" class="hidden-xs">
                              <span class="visible-xs">阿里百秀</span>
                          </a>
                      </div>
                      <div class="nav">
                          <ul>
                              <li><a href="#" class="glyphicon glyphicon-camera">生活馆</a></li>
                              <li><a href="#" class="glyphicon glyphicon-picture">自然汇</a></li>
                              <li><a href="#" class="glyphicon glyphicon-phone">科技潮</a></li>
                              <li><a href="#" class="glyphicon glyphicon-eye-open">奇趣事</a></li>
                              <li><a href="#" class="glyphicon glyphicon-ice-lolly-tasted">美食节</a></li>
                          </ul>
                      </div>
                  </header>
                  <article class="col-md-7">
                      <div class="row">
                          <!-- 新闻 -->
                          <div class="news clearfix">
                              <ul>
                                  <li>
                                      <a href="#">
                                          <img src="./upload/lg.png" alt="">
                                          <p>阿里百秀</p>
                                      </a>
                                  </li>
                                  <li>
                                      <a href="#">
                                          <img src="./upload/1.jpg" alt="">
                                          <p>奇了 成都一小区护卫神似马云 市民纷纷求合影</p>
                                      </a>
                                  </li>
                                  <li>
                                      <a href="#">
                                          <img src="./upload/2.jpg" alt="">
                                          <p>奇了 成都一小区护卫神似马云 市民纷纷求合影</p>
                                      </a>
                                  </li>
                                  <li>
                                      <a href="#">
                                          <img src="./upload/3.jpg" alt="">
                                          <p>奇了 成都一小区护卫神似马云 市民纷纷求合影</p>
                                      </a>
                                  </li>
                                  <li>
                                      <a href="#">
                                          <img src="./upload/4.jpg" alt="">
                                          <p>奇了 成都一小区护卫神似马云 市民纷纷求合影</p>
                                      </a>
                                  </li>
                              </ul>
                          </div>
                          <!-- 发表 -->
                          <div class="publish">
                              <div class="row">
                                  <div class="col-sm-9">
                                      <h3>生活馆 关于指甲的10个健康知识 你知道几个？</h3>
                                      <p class="text-muted hidden-xs">alibaixiu 发布于 2015-11-23</p>
                                      <p class="hidden-xs">指甲是经常容易被人们忽略的身体部位，事实上，从指甲的健康情况可以看出一个人的身体健康情况，快来看看10个暗藏在指甲里的知识吧！</p>
                                      <p class="text-muted">阅读(2417)评论(1)赞(18)</p>
                                      <span class="hidden-xs">标签：健康 / 感染 / 指甲 / 疾病 / 皮肤 / 营养 / 趣味生活</span>
                                  </div>
                                  <div class="col-sm-3 pic hidden-xs">
                                      <img src="./upload/3.jpg" alt="">
                                  </div>
                              </div>
                              <div class="row">
                                  <div class="col-sm-9">
                                      <h3>生活馆 关于指甲的10个健康知识 你知道几个？</h3>
                                      <p class="text-muted hidden-xs">alibaixiu 发布于 2015-11-23</p>
                                      <p class="hidden-xs">指甲是经常容易被人们忽略的身体部位，事实上，从指甲的健康情况可以看出一个人的身体健康情况，快来看看10个暗藏在指甲里的知识吧！</p>
                                      <p class="text-muted">阅读(2417)评论(1)赞(18)</p>
                                      <span class="hidden-xs">标签：健康 / 感染 / 指甲 / 疾病 / 皮肤 / 营养 / 趣味生活</span>
                                  </div>
                                  <div class="col-sm-3 pic hidden-xs">
                                      <img src="./upload/3.jpg" alt="">
                                  </div>
                              </div>
                              <div class="row">
                                  <div class="col-sm-9">
                                      <h3>生活馆 关于指甲的10个健康知识 你知道几个？</h3>
                                      <p class="text-muted hidden-xs">alibaixiu 发布于 2015-11-23</p>
                                      <p class="hidden-xs">指甲是经常容易被人们忽略的身体部位，事实上，从指甲的健康情况可以看出一个人的身体健康情况，快来看看10个暗藏在指甲里的知识吧！</p>
                                      <p class="text-muted">阅读(2417)评论(1)赞(18)</p>
                                      <span class="hidden-xs">标签：健康 / 感染 / 指甲 / 疾病 / 皮肤 / 营养 / 趣味生活</span>
                                  </div>
                                  <div class="col-sm-3 pic hidden-xs">
                                      <img src="./upload/3.jpg" alt="">
                                  </div>
                              </div>
      
      
                          </div>
                      </div>
      
                  </article>
                  <aside class="col-md-3">
                      <a href="#" class="banner">
                          <img src="./upload/zgboke.jpg" alt="">
                      </a>
                      <a href="#" class="hot">
                          <span class="btn btn-primary">热搜</span>
                          <h4 class="text-primary">欢迎加入中国博客联盟</h4>
                          <p class="text-muted">这里收录了国内各个领域的优秀博客，是一个全人工编辑的开放式博客联盟交流和展示平台……</p>
                      </a>
                  </aside>
              </div>
          </div>
          <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
          <script src="https://cdn.jsdelivr.net/npm/jquery@1.12.4/dist/jquery.min.js"
              integrity="sha384-nvAa0+6Qg9clwYCGGPpDQLVpLNn0fRaROjHqs13t4Ggj3Ez50XnGQqc/r8MhnRDZ" crossorigin="anonymous">
          </script>
          <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
          <script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"
              integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd" crossorigin="anonymous">
          </script>
      </body>
      
      </html>
      ```
   
      ```css
      /* 修改container的最大宽度为1280 */
      @media screen and (min-width: 1280px) {
          .container {
              width: 1280px;
          }
      }
      
      body {
          background-color: #f5f5f5;
      }
      
      .container {
          background-color: #fff;
      }
      
      ul {
          list-style: none;
          margin: 0;
          padding: 0;
      }
      
      a {
          color: #666;
          text-decoration: none;
      }
      
      a:hover {
          text-decoration: none;
      }
      
      header {
          padding-left: 0 !important;
      }
      
      .logo {
          background-color: #429ad9;
      }
      
      .logo img {
          /* 居中显示 */
          display: block;
          /* logo图片不进行缩放 */
          max-width: 100%;
          margin: 0 auto;
      }
      
      .logo span {
          display: block;
          height: 50px;
          line-height: 50px;
          text-align: center;
          color: #fff;
          font-size: 18px;
      }
      
      .nav {
          background-color: #eee;
          border-bottom: 1px solid #ccc;
      }
      
      
      
      
      .nav ul li a {
          display: block;
          height: 50px;
          line-height: 50px;
          padding-left: 30px;
          font-size: 16px;
      }
      
      
      .nav ul li a::before {
          vertical-align: middle;
          padding-right: 5px;
      }
      
      .nav ul li a:hover {
          background-color: #fff;
          color: #333;
      }
      
      .news ul li {
          float: left;
          width: 25%;
          height: 128px;
          padding-right: 10px;
          margin-bottom: 10px;
      }
      
      .news ul li:nth-child(1) {
          float: left;
          width: 50%;
          height: 266px;
      }
      
      .news ul li a {
          position: relative;
          display: block;
          width: 100%;
          height: 100%;
      }
      
      .news ul li a img {
          width: 100%;
          height: 100%;
      }
      
      .news ul li a p {
          position: absolute;
          left: 0;
          bottom: 0;
          width: 100%;
          height: 41px;
          background: rgba(0, 0, 0, .5);
          color: #fff;
          font-size: 12px;
          margin-bottom: 0;
          padding: 5px 10px;
      }
      
      .news ul li:nth-child(1) a p {
          line-height: 41px;
          font-size: 20px;
          padding: 0 10px;
      }
      
      .publish {
          border-top: 1px solid #ccc;
      }
      
      .publish .row {
          border-bottom: 1px solid #ccc;
      }
      
      .pic {
          margin: 10px 0;
      }
      
      .pic img {
          width: 100%;
      }
      
      .banner img {
          width: 100%;
      }
      
      .hot {
          display: block;
          margin-top: 20px;
          padding: 0 20px 20px 20px;
          border: 1px solid #ccc;
      }
      
      .hot span {
          border-radius: 0;
          -webkit-border-radius: 0;
          -moz-border-radius: 0;
          -ms-border-radius: 0;
          -o-border-radius: 0;
          margin-bottom: 20px;
      }
      
      .hot p {
          font-size: 12px;
      }
      
      @media screen and (max-width: 991px) {
          .nav ul li {
              float: left;
              width: 20%;
          }
      
          article {
              margin-top: 10px;
          }
      }
      
      
      @media screen and (max-width:767px) {
          .nav ul li a {
              font-size: 14px;
          }
      
          .news ul li {
              width: 50%;
          }
      
          .news ul li:nth-child(1) {
              width: 100%;
          }
      
          .publish h3 {
              font-size: 14px;
          }
      }
      ```
   
      file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/alibaixiu/index.html

# 上传码云并发布部署静态网站

## 一、准备工作

下载git软件、注册码云账号

1. 码云创建新的仓库：heimamm；

2. **利用git提交** 将本地网站提交到码云gitee新建的仓库中；

   - 在网站**根目录**右键 - git bash here

   - 第一次使用git提交，需要配置全局选项

     ```
     git config --global user.name "用户名"
     git config --global user.email "邮箱地址"
     ```

   - 初始化仓库

     ```
     git init
     ```

   - 将本地文件放到暂存区

     ```
     git add .
     ```

   - 将本地文件放入本地仓库

     ```
     git commit -m '提交信息（主要修改内容与类型）'
     ```

   - 链接远程仓库

     ```
     git remote add origin 新建的仓库地址
     ```

   - 把本地仓库的文件推送到远程仓库 push

     ```
     git push -u origin master
     ```

3. 直接在网站内点击文件上传（文件数量有上限且有时间间隔限制）

   - ![image-20211107180143187](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211107180143187.png)

   - ![image-20211107180025168](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211107180025168.png)

4. 码云部署发布静态网站

   - 在当前仓库中，点击“服务”菜单，选择gitee pages

     ![image-20211107175408807](C:\Users\SJY\AppData\Roaming\Typora\typora-user-images\image-20211107175408807.png)

# 初识JavaScript

## 一、JavaScript 是什么

- JavaScript是世界上最流行的语言之一，是一种运行在客户端的脚本语言（Script 脚本）。
- 脚本语言：不需要编译，运行过程中由js解释器（js引擎）**逐行来进行解释并执行**。
- 现在也可以基于Node.js技术进行服务器端编程。

![image-20211113202250453](https://gitee.com/v876774538/my-img/raw/master/image-20211113202250453.png)

## 二、JavaScript 的作用

- **表单动态校验**（密码强度检测）（JS产生最初的目的）
- 网页特效
- 服务端开发（Node.js）
- 桌面程序（Electron）
- App（Cordova）
- 控制硬件-物联网（Ruff）
- 游戏开发（Cocos2d-js）

## 三、HTML/CSS/JS 的关系

1. HTML/CSS 标记语言——描述类语言
   - HTML决定网页结构和内容，相当于人的身体；
   - CSS决定网页呈现给用户的模样，相当于人的衣服。
2. JS 脚本语言——编程类语言
   - 实现业务逻辑和页面控制，相当于人的各种动作。

## 四、浏览器执行JS

1. 浏览器两大组成部分：渲染引擎和JS引擎
   - 渲染引擎：用来解析HTML和CSS，俗称内核，比如Chrome浏览器的blink，老版本的webkit；
   - JS引擎：也称为JS解释器。用来读取网页中的JavaScript代码，对其处理后运行，比如Chrome浏览器的V8。
2. 浏览器本身并不会执行JS代码，而是**通过内置JavaScript引擎（解释器）来执行JS代码**。JS引擎执行代码时逐行解释每一句源码（转换为机器语言），然后由计算机执行，所以JavaScript语言归为脚本语言，会逐行解释执行。

## 五、JS 的组成

![image-20211113203438216](https://gitee.com/v876774538/my-img/raw/master/image-20211113203438216.png)

1. ECMAScript

   ECMAScript是由ECMA国际（原欧洲计算机制造商协会）进行标准化的一门编程语言，这种语言在万维网上应用广泛，它往往被称为JavaScript（网景公司）或JScript（微软公司），但实际上后两者是ECMAScript语言的实现和扩展。

   **ECMAScript：ECMAScript规定了JS的变成语法和基础核心知识，是所有浏览器厂商共同遵守的一套JS语法工业标准。**

2. DOM

   DOM，即文档对象模型（Document Object Model，简称DOM）。是W3C组织推荐的处理可扩展标记语言的**标准编程接口**。

   通过DOM提供的接口可以对页面上的各种元素进行操作（大小、位置、颜色等）。

3. BOM

   BOM，即浏览器对象模型（Browser Object Model，简称BOM）。是指浏览器对象模型，它提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。通过BOM可以操作浏览器窗口，比如弹出框、控制浏览器跳转、获取分辨率等。

## 六、JS 初体验

1. 三种书写位置

   - 行内

     ```html
     <input type="button" value="确认" onclick="alert('ok')">
     ```

     - 可以将单行或少量JS代码写在HTML标签的事件属性中（以on开头的属性），如onclick；
     - 注意单双引号的使用：在**HTML**中，我们推荐使用**双引号**，但在**JS**中，我们推荐使用**单引号**；
     - 可读性差，在HTML中编写大量JS代码时，不方便阅读；
     - 引号易错，引号多层嵌套时，非常容易弄混；
     - 仅在特殊情况下使用。

   - 内嵌

     ```html
     <script>
             alert('Hello！');
     </script>
     ```

     - 可以将多行JS代码写到<script>标签中；
     - 内嵌JS是学习时最常用的方式。

   - 外部

     ```html
     <script src="my.js"></script>
     ```

     - 利用HTML页面代码结构化，把大段JS代码独立到HTML页面之外，既美观，又方便文件级别的复用；
     - 引用外部JS文件的script标签中间不可以写代码；
     - 适合JS代码量较大的情况。

2. JS注释

   - 单行注释

     ```js
     // 单行注释
     // 快捷方式 ctrl +　/
     ```

   - 多行注释

     ```js
     /* 
     	多行注释
     	默认快捷方式 shift + alt + a 修改为 ctrl + shift + /
     */
     ```

3. JavaScript 输入输出语句

   ```js
   // 浏览器弹出警示框
   alert(msg);
   
   // 浏览器控制台打印输出信息
   console.log(msg);
   
   // 浏览器弹出输入框，用户可以输入
   prompt(info);
   ```

# 变量

## 一、变量概述

1. 本质：变量是程序在内存中申请的一块用来存放数据的空间。
2. 通俗：变量是用于存放数据的容器。我们通过变量名获取数据，甚至对数据进行修改。

## 二、变量使用

1. 声明

   ```js
   // 声明一个名称为age的变量
   var age;
   ```

2. 赋值

   ```js
   // 给age 这个变量赋值为10
   age = 10;
   ```

   **声明**一个**变量并赋值**，我们称之为**变量的初始化**。

   ```js
   var myname = 'SJY';
   ```

3. 案例：弹出用户名

   ```js
   var name = prompt('请输入您的名字：');
   alert(name);
   ```

## 三、变量语法扩展

1. 更新变量

   一个变量被重新赋值后，它原有的值将被覆盖，变量值以最后一次赋值为准。

2. 同时声明多个变量

   ```js
   var age = 10, name = 'sjy', sex = '女';
   ```

3. 声明变量的特殊情况

   | 情况                        | 说明                  | 结果      |
   | --------------------------- | --------------------- | --------- |
   | var age; console.log(age);  | 只声明不赋值          | undefined |
   | console.log(age);           | 不声明不赋值 直接使用 | error     |
   | age = 10; console.log(age); | 不声明只赋值          | 10        |

## 四、变量命名规范

- 由字母（A-Z、a-z）、数字（0-9）、下划线（_ ）、美元符号（$）组成，如，usrAge、num01、_name；
- 严格区分大小写；
- 不能以数字开头；
- 不能是关键字、保留字，如，var、for、while；
- 变量名必须有意义；
- 遵守驼峰命名法，首字母小写，后面单词的首字母需要大写，如myFirstName。

# 数据类型

## 一、数据类型简介

1. 为什么需要数据类型

   在计算机中，不同的数据所需占用的存储空间是不同的。为了便于把数据分成所需内存大小不同的数据，充分利用存储空间，于是定义了不同的数据类型。

2. 变量的数据类型

   变量是用来存储值的空间，变量的数据类型决定了如何将代表这些值的位存储到计算机内存中。

   **JavaScript是一种弱类型语言（动态语言）。**因此，就算不提前声明变量的类型，在程序运行过程中，变量的数据类型也会被自动确定。

   ```js
   var age = 10;	// 数字型
   var areYouOk = 'Yes';	// 字符串
   ```

   JavaScript拥有动态类型，因此，相同变量的数据类型也可以发生改变：

   ```js
   var x = 6;	// x为数字
   var x = 'Bill';	// x为字符串
   ```

3. 数据类型的分类

   - 简单数据类型：Number, String, Boolean, Undefined, Null
   - 复杂数据类型：Object

## 二、简单数据类型

| 简单数据类型 | 说明                                               | 默认值    |
| ------------ | -------------------------------------------------- | --------- |
| Number       | 数字型，包含整型、浮点型，如21、0.21               | 0         |
| Boolean      | 布尔型，如true、false，等价于1和0                  | false     |
| String       | 字符串类型，如'张三'                               | ''        |
| Undefined    | var a; 声明了变量a后却没有赋值，此时a = undefined; | undefined |
| Null         | var a = null; 声明了变量a为空值                    | null      |

### 1.数字型Number

1. 数字型进制

   ```js
   // 1.八进制数字序列范围：0-7
   var num1 = 07;	// 对应十进制7
   var num2 = 023;	// 对应十进制19	
   var num3 = 08;	// 对应十进制8
   
   // 2.十六进制数字序列范围：0-9 A-F
   var num = 0xA;	// 对应十进制10
   ```

2. 数字型范围

   ```js
   alert(Number.MAX_VALUE);	// 1.7976931348623157e+308
   alert(Number.MIN_VALUE);	// 5e-324
   ```

3. 数字型三个特殊值

   ```js
   alert(Infinity);	// Infinity 无穷大
   alert(-Infinity);	// -Infinity 无穷小
   alert(NaN);	// NaN 无法计算，代表一个非数值
   ```

4. 验证非数值：**isNaN()**

   ```js
   //	isNaN() 用来判断是否非数值 并将返回一个值：是数值→flase 非数值→true
   console.log(isNaN(12));//	结果为flase
   console.log(isNaN(''));//	结果为true
   ```

### 2.字符串型String

1. 字符串型

   ```js
   var strMsg1 = "我爱北京天安门~";
   var strMsg2 = '天安门上太阳升~';
   ```

    推荐使用**单引号**包裹。

2. 字符串型嵌套：**外双内单，外单内双**。

   ```js
   var str = 'Do you know"Coco"?';
   ```

3. 字符串转义符：以 \ 开头

   | 转义符 | 说明          |
   | ------ | ------------- |
   | \n     | 换行符        |
   | \\     | 反斜杠 \      |
   | \'     | ' 单引号      |
   | \"     | " 双引号      |
   | \t     | tab 缩进      |
   | \b     | 空格（blank） |

4. 字符串长度：**length属性**

   ```js
   var str = 'my name is andy.';
   console.log(str.length);
   ```

5. 字符串拼接：**字符串 + 任何类型（自动转换为字符串） = 拼接之后的新字符串**

   ```js
   console.log('沙漠' + '骆驼');	// 沙漠骆驼
   
   var str = 'my name is';
   console.log(str + 'andy.');	// my name is andy.
   
   var age = 21;
   console.log('我今年' + age);	// 我今年21
   
   console.log(12 + 12);	// 24
   console.log('12' + 12);	// '1212'
   ```

### 3.布尔型Boolean

布尔型仅有两个值：true和false。

1. 当布尔型参加运算时：ture的值为1，false的值为0。

   ```js
   console.log(true + 1);	// 2
   console.log(false + 1); 	// 1
   ```


### 4.undefined 

声明后没有呗赋值的变量会有一个默认值undefined，称为**未定义数据类型**。

### 5.null

一个声明变量赋予null值，即里面存的值为**空**。

```js
var vari = null;
console.log('你好' + vari);	// 你好null
console.log(11 + vari);	// 11
console.log(true + vari);	// 1
```

## 三、获取变量数据类型

1. 获取检测变量的数据类型**typeof**

   ```js
   var num = 10;
   console.log(typeof num);	// numver
   
   var str = 'pink';
   console.log(typeof str);	// string
   
   var flag = true;
   console.log(typeof flag);	// boolean
   
   var timer = null;
   console.log(typeof timer);	// object
   ```

2. 字面量

   字面量是在源代码中一个固定值的表示法，通俗来说，就是字面量表示如何表达这个值。

   - 数字字面量：8，9，10；
   - 字符串字面量：'黑马程序员'，'大前端'；
   - 布尔字面量：true，false。

## 四、数据类型转换

### 1.转换为字符串

| 方式                           | 说明                         | 案例                                    |
| ------------------------------ | ---------------------------- | --------------------------------------- |
| toString()                     | 转成字符串                   | var num = 1; alert**(num.toString()**); |
| String() 强制转换函数          | 转成字符串                   | var num = 1; alert(**String(num)**);    |
| **加号拼接字符串**（隐式转换） | 和字符串拼接的结果都是字符串 | var num = 1; alert(num + "我是字符串"); |

### 2.转换为数字型

| 方式                    | 说明                         | 案例                |
| ----------------------- | ---------------------------- | ------------------- |
| parseInt(string) 函数   | 将string类型转成整数数值型   | parseInt('78')      |
| parseFloat(string) 函数 | 将string类型转成浮点数数值型 | parseFloat('78.21') |
| Number() 强制转换函数   | 将string类型转换为数值型     | Number('12')        |
| js 隐式转换（- * /）    | 利用算术隐式转换为数值型     | '12' - 0            |

```js
// parseInt
console.log(parseInt('3.14'));	// 3
console.log(parseInt('120px'));	// 120
console.log(parseInt('rem120px'));	// NaN

// parseFloat
console.log(parseFloat('3.14'));	// 3.14
console.log(parseFloat('120px'));	// 120
console.log(parseFloat('rem120px'));	// NaN

// Number()
var str = '123';
console.log(Number(str));	// 123
console.log(Number('12'));	// 12

// 算术运算
console.log('12' - 0);	// 12
console.log('123' - '120');	// 3
console.log('123' + '120');	// '123120'
```

### 3.转换为布尔型

| 方式           | 说明                 | 案例            |
| -------------- | -------------------- | --------------- |
| Boolean() 函数 | 其他类型转换为布尔型 | Boolean('true') |

```js
// - 代表空、否定的值会转换为false，如''、0、NaN、null、undefined；
// - 其余值会被转换为true
console.log(Boolean(''));	// false
console.log(Boolean(0));	// false
console.log(Boolean(NaN));	// false
console.log(Boolean(null));	// false
console.log(Boolean(undefined));	// false
console.log(Boolean('小白'));	// true
console.log(Boolean(12));	// true
```

# 编译和解释语言的区别

## 一、解释型语言和编译型语言

1. 概述

   计算机不能直接理解任何除机器语言以外的语言，所以必须要把程序员所写的程序语言翻译成机器语言才能够执行。程序语言翻译成机器语言的工具，被称为翻译器。

   翻译器的翻译方式有两种：一种是**编译**，另外一种是**解释**。两种方式之间的区别在与**翻译的时间点不同**。

   - 编译器：在**代码执行之前进行编译**，生成中间代码文件；
   - 解释器：在**运行时进行及时解释**，并立即执行（当编译器以解释方式运行时，也称为解释器）。

2. 执行过程

   ![image-20211116165737539](https://gitee.com/v876774538/my-img/raw/master/image-20211116165737539.png)

## 二、标识符、关键字、保留字

1. 标识符：指开发人员为变量、属性、函数、参数取的名字。**标识符不能是关键字或保留字。**

2. 关键字：指JS本身已经使用了的字，我们不能再使用它们充当变量名、方法名。

   ```js
   break case catch continue default delete do else finally for function if in instanceof new return switch this throw try typeof var void while with ...
   ```

3. 保留字：即预留的关键字，同样不能使用它们做变量名或方法名。

   ```js
   boolean byte char class const debugger double enum export extends final float goto implements import int interface long native package private promtected public short static super synchronized throws transient volatile ...
   ```

# JavaScript 运算符

运算符（operator）也被称为**操作符**，用于实现赋值、比较和执行算术运算等功能的符号。

## 一、算术运算符

1. 概述

   算术运算符使用的符号，用于执行两个变量或值的算术运算。

   | 运算符 | 描述 | 示例        |
   | ------ | ---- | ----------- |
   | +      | 加   | 1 + 1 = 2   |
   | -      | 减   | 2 - 1 = 1   |
   | *      | 乘   | 1 * 2 = 2   |
   | /      | 除   | 1 / 2 = 0.5 |
   | %      | 取余 | 9 % 2 = 1   |

2. 浮点数精度问题

   浮点数的最高精度是17位小数，但在进行算术运算时其精度远远不如整数。

   ```js
   var result = 0.1 + 0.2;	// 0.30000000000000004
   console.log (0.07 * 100);	// 7.00000000000001
   ```

   注意：浮点数不直接拿来运算，也**不要直接判断两个浮点数是否相等！**

## 二、递增和递减运算符

1. 概述

   若需要反复给数字变量加或减去1，可以使用递增（++）和递减（--）运算符来完成。

2. 递增运算符

   前置递增运算符：**先自加1，后返回值**

   ```js
   var num = 10;
   ++num;	// 类似于 num = num + 1;
   console.log(num);	// 11
   
   var p = 10;
   console.log(++p + 10);	// 21
   ```

   后置递增运算符：**先返回值，后自加1**

   ```js
   var num = 10;
   num++;	// 类似于 num = num + 1;
   console.log(num);	// 11
   
   var p = 10;
   console.log(p++ + 10);	// 20
   console.log(p);	// 11
   ```

    递增运算符练习：

   ```js
   var a = 10;
   ++a;	// 11
   var b = ++a + 2;	// 14
   console.log(b);
   
   var c = 10;
   c++;
   var d = c++ + 2;	// 13
   console.log(d);
   
   var e = 10;
   var f = e++ + ++e;	// f = 10 + 12 = 22;
   console.log(f);
   console.log(e);	// 12
   ```

## 三、比较运算符

比较运算符（关系运算符）是两个数据进行比较时所使用的运算符，比较运算后，会返回一个布尔值（true / fasle）作为比较运算的结果。

| 运算符  | 说明                           | 案例        | 结果  |
| ------- | ------------------------------ | ----------- | ----- |
| <       | 小于                           | 1 <  2      | true  |
| >       | 大于                           | 1 > 2       | false |
| >=      | 大于等于                       | 2 >= 2      | true  |
| <=      | 小于等于                       | 3 <= 2      | false |
| ==      | 判等                           | 37 == '37'  | true  |
| !=      | 不等                           | 37 != 37    | false |
| === !== | 全等（要求值、数据类型都一致） | 37 === '37' | false |

## 四、逻辑运算符

1. 概述

   逻辑运算符（布尔运算符）是用来进行布尔值运算的运算符，其返回值也是布尔值。

   | 运算符 | 说明 | 示例            | 结果   |
   | ------ | ---- | --------------- | ------ |
   | &&     | 与   | true && false   | false  |
   | \|\|   | 或   | true \|\| false | true   |
   | !      | 非   | !true           | false0 |

2. 逻辑运算符练习

   ```js
   var num = 7;
   var str = "我爱你~中国~";
   
   console.log(num > 5 && str.length >= num);	// true
   console.log(num < 5 && str.length >= num);	// false
   console.log(!(num < 10));	// false
   console.log(!(num < 10 || str.length == num));	// false
   ```

3. 短路运算（逻辑中断）

   短路运算原理：当有多个表达式（值）时，左边的表达式值可以确定结果时，就不再继续运算右边表达式的值。

   1. 逻辑与

      - 语法：**表达式1 && 表达式2**
      - 若第一个表达式的值为真，则返回表达式2；
      - 若第一个表达式的值为假，则返回表达式1。

      ```js
      console.log(123 && 456);	// 456
      console.log(0 && 456);	// 0
      console.log(0 && 1 + 2 && 456 * 5678);	// 0
      ```

   2. 逻辑或

      - 语法：**表达式1 || 表达式2**
      - 若第一个表达式的值为真，则返回表达式1；
      - 若第一个表达式的值为假，则返回表达式2。

      ```js
      console.log(123 || 456);	// 123
      console.log(123 || 456 || 456 + 123);	// 123
      console.log(0 || 456 || 456 + 123);	// (456 || 456 + 123)	// 456
      
      var num = 0;
      console.log(123 || num++);	// 123
      console.log(num);	// 0
      ```

## 五、赋值运算符

赋值运算符，就是用来把数据赋值给变量的运算符。

| 运算符     | 说明                 | 示例                                          |
| ---------- | -------------------- | --------------------------------------------- |
| =          | 直接赋值             | var usrName = '值';                           |
| +=、-=     | 加、减一个数后再赋值 | var age = 10; age +=5; // age = age + 5 = 15; |
| *=、/=、%= | 乘、除。取余后再赋值 | var age = 2; age*= 5; // age = age * 5 = 10;  |

## 六、运算符优先级

| 优先级 | 运算符     | 顺序               |
| ------ | ---------- | ------------------ |
| 1      | 小括号     | ()                 |
| 2      | 一元运算符 | ++ -- !            |
| 3      | 算术运算符 | **先* / % 后 + -** |
| 4      | 关系运算符 | > >= < <=          |
| 5      | 相等运算符 | == != === !==      |
| 6      | 逻辑运算符 | **先&& 后\|\|**    |
| 7      | 赋值运算符 | =                  |
| 8      | 逗号运算符 | ,                  |

```js
console.log(4 >= 6 || '人' != '阿凡达' && ！（12 * 2 == 144） && true);
// 0 || 1 && !0 && 1
// 0 || 1 && 1 && 1
// true

var num = 10;
console.log(5 == num / 2 && (2 + 2 *num).toString() === '22');
// 1 && 1
// true
```

# JavaScript 流程控制

## 一、流程控制

在一个程序执行过程中，各条代码的执行顺序对程序的结果有着直接影响。很多时候我们需要通过控制代码的执行顺序来实现我们要完成的功能。

流程控制主要有三种结构，分别是：**顺序结构**、**分支结构**和**循环结构**。

![image-20211116195924247](https://gitee.com/v876774538/my-img/raw/master/image-20211116195924247.png)

## 二、顺序流程控制

程序中最简单、最基本的流程控制。它没有特定的语法结构，程序会按照代码的先后顺序依次执行。

## 三、分支流程控制

由上而下执行代码的过程中，根据不同的条件，执行不同的代码路径，从而得到不同的结果。

### 1.if

```js
if (条件表达式) {
	// 执行语句
}
```

```js
if (条件表达式) {
	// 执行语句
}
else {
	// 执行语句
}
```

```js
if (条件表达式1) {
	// 执行语句
}
else if (条件表达式2) {
	// 执行语句
}
else if (条件表达式3) {
	// 执行语句
}
...
else {
	// 执行语句
}
```

### 2.switch

switch语句也是多分支语句，它用于基于不同的条件来执行不同的代码。

当要**针对变量设置一系列的特定值选项**时，就可以使用swith。

```js
switch(表达式) {
	case value1:
		// 执行语句1;
		break;	// 执行完退出，否则在执行完后会直接继续执行下一个case内的执行语句...
	case value2:
		// 执行语句2;
		break;
	...
	default:
		// 执行最后的语句;
}
```

练习：查询水果

```js
var fruit = prompt('请输入您想购买的水果：');
switch (fruit) {
    case '柑橘':
        alert('5.00元/斤');
        break;
    case '葡萄':
        alert('68.00元/斤');
        break;
    case '草莓':
        alert('40.00元/斤');
        break;
    default:
        alert('抱歉，没有您查询的水果！');
}
```



## 四、三元表达式

由三元运算符组成的式子称为三元表达式。三元表达式也能做一些简单的条件选择。

```js
// 若条件表达式结果为真 返回表达式1的值；
// 若条件表达式结果为假 则返回表达式2的值
条件表达式 ? 表达式1 : 表达式2;
```

```js
var num = 10;
var result = num > 5 ? '是的' : '不是';
console.log(result);	// 是的
```

练习：数字补0

用户输入数字，若数字小于10，则在前面补0，如01、09；若数字大于10，则不需要补，如20。

```js
var num = prompt("请输入号码：");
var result = num < 10 ? '0' + num : num;
console.log(result);
```

## 五、循环流程控制

循环的目的：重复执行某些代码。

在程序中，一组被重复执行的语句被称之为**循环体**，能否继续重复执行，取决于循环的**终止条件**。由循环体及循环的终止条件组成的语句，称为**循环语句**。

### 1.for

```js
for (初始化变量;条件表达式;操作表达式) {
	// 循环体
}
```

```js
for (var i = 1; i <= 100; i++) {
	console.log('hello');
}
```

断点调试：

浏览器中按F12 --> sources --> 找到需要调试的文件 --> 在程序的某一行设置断点

- watch：监视，通过watch可以监视变量的值的变化。
- F11：程序单步执行，让程序一行一行地执行，方便观察watch中变量值的变化。

练习：求1-100之间所有整数的累加和

```js
var sum = 0;
for (var i = 1; i <= 100; i++) {
    sum += i;
    console.log(sum);
}
alert('1-100之间所有整数的累加和为：' + sum);
```

练习：求1-100之间所有能被3整除的数的和

```js
var sum = 0;
for (var i = 1; i <= 100; i++) {
    if (i % 3 == 0) {
        sum += i;
    }
    console.log(sum);
}
alert('1-100之间所有能被3整除的数的和为：' + sum);
```

 练习：求学生成绩

```js
var num = prompt('请输入班级学生人数：');
var sum = 0;
var score = 0;
var average = 0;
for (i = 1; i <= num; i++) {
    score = prompt('请输入第' + i + '位学生的成绩：');
    sum += parseFloat(score);
}
average = sum / num;
alert('班级平均分为：' + average);
```

练习：打印☆（双重for循环）

```js
// 1
var rows = prompt('请输入行数：');
var str = '';
// 层
for (var i = 1; i <= rows; i++) {
    // 清空
    str = '';
    for (var j = 1; j <= i; j++) {
        // 每行上的星星
        str = str + '☆';

    }
    console.log(str);
}

// 2
var rows = prompt('请输入行数：');
var str = '';
for (var i = 1; i <= rows; i++) {
    for (var j = i; j <= i; j++) {
        str = str + '☆';
    }
    str = str + '\n';
}
console.log(str);
```

![image-20211117185907005](https://gitee.com/v876774538/my-img/raw/master/image-20211117185907005.png)

练习：打印九九乘法表

```js
var str = '';
for (i = 1; i <= 9; i++) {
    for (j = 1; j <= i; j++) {
        str = str + j + '×' + i + '=' + i * j + ' ';
    }
    str = str + '\n';
}
console.log(str);
```

![image-20211117191908578](https://gitee.com/v876774538/my-img/raw/master/image-20211117191908578.png)

### 2.while

```js
while (条件表达式) {
	// 循环体
}
```

练习：计算1-100之间所有整数的和

```js
var sum = 0;
var i = 1;
while (i <= 100) {
	sum += i;
	i++;
}
console.log(sum);
```

### 3.do...while

是while循环的变体。该循环会**先执行一次代码块**，然后再对条件表达式进行判断，若条件为真，就会重复执行循环体，否则退出循环。

```js
do {
	// 循环体
} while (条件表达式)
```

练习：弹出一个提示框：“你爱我吗？”，若输入我爱你，就提示结束，否则一直询问

```js
do {
	var msg = prompt('你爱我吗？');
} while( msg !== '我爱你')
alert ('我也爱你！');
```

### 4.continue

**continue关键字**用于立即跳出**本次循环**，**进入下一次循环**。

```js
for (var i = 1; i <= 5; i++) {
	if (i == 3) {
		continue;
	}
	console.log('第' + i + '次循环');
}
```

### 5.break

**break关键字**用于立即跳出**整个循环**（**循环结束**）。

```js
for (var i = 1; i <= 5; i++) {
	if(i == 3) {
		break;
	}
	console.log('第' + i + '次循环');
}
```

# JavaScript 命名规范及语法格式

### 1.标识符规范

- 变量、函数的命名必须要有意义；
- 变量的名称一般用名词，函数的名称一般用动词。

### 2.操作符规范

- 操作符的左右两侧各保留一个空格。

### 3.单行注释规范

- 单行注释// 后跟一个空格。

  ```js
  // 单行注释
  ```

### 4.其他规范

![image-20211117194510996](https://gitee.com/v876774538/my-img/raw/master/image-20211117194510996.png)

# JavaScript 数组

## 一、数组的概念

数组指**一组数据的集合**，其中的每个数据被称作**元素**，在数组中可以**存放任意类型的元素**。

数组是一种**将一组数据存储在单个变量名下**的优雅方式。

```js
var arr = [1,2,3,4,5];
```

## 二、创建数组

1. 利用new创建数组

   ```js
   var 数组名 = new Array();
   var arr = new Array();	// 创建一个新的空数组
   ```

2. 利用数组字面量创建数组

   ```js
   var 数组名 = [];	// 创建一个空的数组
   var arr = ['小白', '小黑', '大黄', '瑞奇'];
   var arr1 = [1, 2, 'SJY', true];
   ```

## 三、获取数组中的元素

索引（下标）：用来访问数组元素的序号（从0开始）。

```js
数组名[索引]
```

## 四、遍历数组

```js
var arr = ['red', 'green', 'blue'];
for (var i = 0; i < 3; i++) {
	console.log(arr[i]);
}
```

数组长度（数组中元素个数）：**数组名.length**

```js
var arr = ['red', 'green', 'blue'];
for (var i = 0; i < arr.length; i++) {
	console.log(arr[i]);
}
```

练习：数组求和及平均值

```js
var arr = [2, 6, 1, 7, 4];
var sum = 0;
var average = 0;
for (var i = 0; i < arr.length; i++) {
    sum += arr[i];
}
console.log(sum);
average = sum / arr.length;
console.log(average);
```

练习：筛选数组中最大值

```js
var arr = [2, 6, 77, 52, 25, 7];
var max = arr[0];
for (var i = 1; i < arr.length; i++) {
    if (max < arr[i]) {
        max = arr[i];
    }
}
console.log(max);
```

练习：数组转换为分割字符串

```js
var arr = ['red', 'green', 'blue', 'pink'];
var str = '';
for (var i = 0; i < arr.length; i++) {
    str += arr[i] + '|';
}
// 删除字符串最后一个字符
// substr() 方法可在字符串中抽取从 开始 下标开始的指定数目的字符。
// string.substr(start,length)
str = str.substr(0, str.length - 1);
console.log(str);
```

## 五、数组中新增元素

1. 通过修改length长度新增数组元素

   - 可以通过修改length长度来实现数组扩容的目的；

   - length属性是可读写的。

     ```js
     var arr = ['red', 'green', 'blue'];
     console.log(arr.length);
     arr.length = 5;
     console.log(arr);	// ['red', 'green', 'blue', empty × 2]
     console.log(arr[4]);	// undefined
     ```

2. 通过修改索引号增加数组元素

   - 可以通过修改数组索引的方式追加数组元素。

     ```js
     var arr = ['red', 'green', 'blue'];
     arr[3] = 'pink';
     console.log(arr);	// ['red', 'green', 'blue', 'pink']
     ```

3. 练习：新建数组存放10个整数（1-10）

   ```js
   var arr = [];
   for (var i = 0; i < 10; i++) {
   	arr[i] = i + 1;
   }
   console.log(arr);
   ```

4. 练习：将数组[2, 0, 6, 1, 77, 0, 52, 0, 25, 7]中大于等于10的元素选出来，放入新数组

   ```js
   // 1
   var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
   var newArr = [];
   var j = 0;
   for (var i = 0; i < arr.length; i++) {
   	if (arr[i] >= 10) {
   		newArr[j] = arr[i];
   		j++;
   	}
   }
   console.log(newArr);
   
   // 2
   var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
   var newArr = [];
   for (var i = 0; i < arr.length; i++) {
   	if (arr[i] >= 10) {
   		newArr[newArr.length] = arr[i];
   	}
   }
   console.log(newArr);
   ```

## 六、数组案例

1. 翻转数组

   ```js
   var arr = ['red', 'green', 'blue', 'pink', 'purple'];
   var newArr = [];
   for (var i = arr.length - 1; i >= 0; i--) {
       newArr[newArr.length] = arr[i];
   }
   console.log(newArr);
   ```

2. 冒泡排序

   ```js
   var arr = [5, 2, 3, 1, 4];
   var temp = 0;
   for (var i = 0; i < arr.length - 1; i++) {
       for (var j = 0; j < arr.length - i; j++)
           if (arr[j] > arr[j + 1]) {
               temp = arr[j];
               arr[j] = arr[j + 1];
               arr[j + 1] = temp;
           }
   }
   console.log(arr);
   ```

# JavaScript 函数

## 一、函数的概念

在JS里面，可能会定义非常多相同或功能相似的代码，这些代码可能需要大量地重复使用。此时我们就可以使用JS中的函数。

**函数**：就是封装了一段**可以被重复调用执行的代码块**。

## 二、函数的使用

1. 声明函数

   ```js
   function 函数名(参数) {
   	// 函数体
   }
   
   function sayHi() {
       console.log('hi~');
   }
   ```

   - function为声明函数的**关键字**，必须小写；
   - 函数名一般采用动词；
   - 函数不调用，自己不执行。

2. 调用函数

   ```js
   函数名();
   
   sayHi();
   ```

3. 函数的封装

   所谓函数的封装就是把一个或多个功能通过函数的方式封装起来，对外值提供一个简单的函数接口。

## 三、函数的参数

1. 形参和实参

   - 形参：形式上的参数，函数定义的时候传递的参数；
   - 实参：实际上的参数，函数调用的时候传递的参数。

   ```js
   // 声明
   function 函数名(形参1, 形参2, ...) {
   	// 函数体
   }
   // 调用
   函数名(实参1, 实参2, ...);
   ```

2. 函数形参和实参个数不匹配问题

   ```
   function getSum(num1, num2) {
   	console.log(num1 + num2);
   }
   // 1.若实参个数与形参个数一致 则正常输出结果
   getSum(1, 2);	// 3
   // 2.若实参个数多于形参个数 则只取得到与形参个数匹配的实参
   getSum(1, 2, 3);	// 3
   // 3.若实参个数少于形参个数 多余的形参定义为undefined 最终结果就是NaN
   getSum(1);	// NaN
   ```
   

## 四、函数的返回值

```js
function 函数名() {
	// 函数体
	return 需要返回的结果;
}
函数名();
```

练习：利用函数求任意两个数的最大值

```js
function getMax(num1, num2) {
	if (num1 >= num2) {
		return num1;
	}
	else {
		return num2;
	}
    // num1 > num2 ? num1 : num2;
}
console.log(getMax(22, 35));	// 35
```

练习：利用函数求任意一个数组中的最大值

```js
function getArrMax(arr) {
    var max = arr[0];
    for (var i = 0; i < arr.length; i++) {
        if (max < arr[i]) {
            max = arr[i];
        }
    }
    return max;
}
var arr = [0, 4, 6, 2, 1];
var max = getArrMax(arr);
console.log(max);
```

注意：

- **return终止函数**：return语句之后的代码不被执行；

- return返回的结果只能是一个值；

  ```js
  function fuc(num1, num2) {
  	return num1, num2;	// 返回的结果是最后一个值
  }
  
  function fuc(num1, num2) {
  	return [num1, num2];	// 返回的结果可以是一个数组
  }
  ```

- 函数没有return，返回undefined。

## 五、arguments的使用

当我们不确定有多少个参数传递的时候，可以用arguments来获取。

在JavaScript中，arguments实际上它是**当前函数的一个内置对象**。所有函数都内置了一个arguments对象，arguments对象中**存储了传递的所有实参**。

```js
function fn() {
	console.log(arguments);	// arguments(3) [1, 2, 3]	// arguments存储了传递的所有实参
}
fn(1, 2, 3);
```

arguments的展示形式是一个伪数组，伪数组具有以下特点：

- 可以遍历，具有length属性；
- 按索引方式存储数据；
- 但不具有数组的push、pop方法。

练习：利用函数求任意个数的最大值

```js
function getMax() {
	var max = arguments[0];
	console.log(arguments);
	for (var i = 1; i < arguments.length; i++) {
		if (max < arguments[i]) {
			max = arguments[i];
		}
	}
	return max;
}
var max = getMax(1, 2, 5 , 3, 4);
console.log(max);
```

## 六、函数案例

1. 输出用户输入的年份的二月份天数：

   ```js
   function isRunYear(year) {
       var flag = false;
       if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
           flag = true;
       }
       return flag;
   }
   
   function getFebDay() {
       var year = prompt('请输入年份：');
       if (isRunYear(year)) {
           alert('当前年份是闰年，2月份有29天');
       } else {
           alert('当前年份是平年，2月份有28天');
       }
   }
   
   getFebDay();
   ```

## 七、函数的两种声明方式

1. 利用函数关键字自定义函数（命名函数）

   ```js
   function 函数名() {
   	// 函数体
   }
   ```

2. 函数表达式**（匿名函数）**

   ```js
   var 变量名 = function() {
       // 函数体
   }
   ```

   ```js
   var fun = function() {
   	console.log('我是函数表达式');
   }
   fun();
   // fun是变量名 不是函数名
   ```

# JavaScript 作用域

## 一、作用域

1. 作用域概述

   通常来说，一段程序代码中所用到的名字并不总是有效可用的，而限定这个名字的可用性的代码范围，就是这个名字的作用域。

   作用域的使用提高了程序逻辑的局部性，增强了程序的可靠性，减少了名字冲突。

2. 全局作用域：整个script标签，或单独的js文件

3. 局部作用域：只在函数内部起效果和作用

## 二、变量的作用域

在JavaScript中，根据作用域不同，分为：**全局变量**和**局部变量**。

1. 全局变量：在全局作用域下的变量，在全局下都可以使用。

   注意：如果在函数内部，没有声明直接赋值的变量，也属于全局变量！

   ```js
   function fuc() {
   	var num1 = 10;	// 局部变量
   	num2 = 20;	// 全局变量
   }
   ```

2. 局部变量：在局部作用域下的变量，仅在函数内部作用。

   注意：函数的形参也可以看做是局部变量。

3. 从执行效率来看全局变量和局部变量：

   - 全局变量只有在浏览器关闭的时候才会销毁，比较占内存资源；
   - 局部变量当我哦们程序执行完毕就会销毁，比较节约内存资源。

4. JS没有块级作用域

   - 在ES6的时候新增的块级作用域；
   - 块级作用域{} if {} for {}。

## 三、作用域链

- 只要是代码，就至少有一个作用域；

- 写在函数内部的，即局部作用域；

- 如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域；

- 根据在内部函数可以访问外部函数变量的这种机制，用**链式查找**决定哪些数据能被内部函数访问，就称作**作用域链**。**（就近原则）**

  ```js
  var num = 10;
  // 外部函数
  function fn() {
  	var num = 20;
  	// 内部函数
  	function fun() {
  		console.log(num);	// 20
  	}
  }
  fn();
  ```

  ```js
  function f1() {
  	var num = 123;
  	function f2() {
  		console.log(num);	// 123
  	}
  	f2();
  }
  var num = 456;
  f1();
  ```

  ```js
  var a = 1;
  function fn1() {
  	var a = 2;
  	var b = '22';
  	fn2();
  	function fn2() {
  		var a = 3;
  		fn3();
  		function fn3() {
  			var a = 4;
  			console.log(a);	// 4
  			console.log(b);	// '22'
  		}
  	}
  }
  fn1();
  ```

# JavaScript 预解析

## 一、预解析

JavaScript代码是由浏览器中的JavaScript解析器来执行的。

JavaScript解析器在运行JavaScript代码的时候分为两步：**预解析**和**代码执行**。

- 预解析：JS引擎会把JS中所有的**var**还有**function提升到当前作用域的最前面**。
- 代码执行：按照代码书写顺序从上往下执行。

## 二、变量预解析和函数预解析

1.   变量预解析（变量提升）：把所有的变量声明提升到**当前作用域的最前面**，**不提升赋值操作**。

   ```js
   console.log(num);
   var num = 10;	// undefined
   
   // 相当于
   var num;
   console.log(num);	// undefined
   num = 10;
   ```

   ```js
   fun();
   var fun = function() {
   	console.log(22);	// 报错
   }
   
   // 相当于
   var fun;
   fun();	// 报错
   fun = function() {
   	console.log(22);
   }
   ```

2. 函数预解析（函数提升）：把所有的函数声明提升到**当前作用域的最前面**，不调用函数。

   ```js
   fn();
   function fn() {
   	console.log(11);	// 11
   }
   
   // 相当于
   function fn() {
   	console.log(11);
   }
   fn();
   ```

3. 案例：

   ```js
   var num = 10;
   fun();
   function fun() {
   	console.log(num);	// undefined
   	var num = 20;
   }
   
   // 相当于
   var num;
   function fun() {
   	var num;
   	console.log(num);	// undefined
   	num = 20;
   }
   num = 10;
   fun();
   ```

   ```js
   var num = 10;
   function fn() {
   	console.log(num);
   	var num = 20;
   	console.log(num);
   }
   fn();
   
   // 相当于
   var num;
   function fn() {
   	var num;
   	console.log(num);	// undefined
   	num = 20;
   	console.log(num);	// 20
   }
   num = 10;
   fn();
   ```

   ```js
   var a = 18;
   f1();
   function f1() {
   	var b = 9;
   	console.log(a);
   	console.log(b);
   	var a = '123';
   }
   
   // 相当于
   var a;
   function f1() {
   	var b;
   	var a;
   	b = 9;
   	console.log(a);	// undefined
   	console.log(b);	// 9
   	a = '123';
   }
   a = 18;
   f1();
   ```

   ```js
   f1();
   console.log(c);
   console.log(b);
   console.log(a);
   function f1() {
   	var a = b = c = 9;	// var a = 9; b = 9; c = 9;
   	console.log(a);
   	console.log(b);
   	console.log(c);
   }
   
   // 相当于
   function f1() {
   	var a;
   	a = 9; b = 9; c = 9;	// b和c当全局变量看
   	console.log(a);	// 9
   	console.log(b);	// 9
   	console.log(c);	// 9
   }
   f1();
   console.log(c);	// 9
   console.log(b);	// 9
   console.log(a);	// 报错
   ```

# JavaScript 对象

## 一、对象

1. 概述

   在JavaScript中，对象是一组无序的**相关属性和方法的集合**。所有的食物都是对象，如，字符串、数值、数组、函数等。

   - 属性：事物的**特征**，在对象中用**属性**来表示（常用名词）；
   - 方法：事物的**行为**，在对象中用**方法**表示（常用动词）。

2. 意义

   保存一个值时，可以使用变量，保存多个值（一组值）时，可以使用数组，我们可以用对象保存一个个体的完整信息。

   JS中的对象表达结构更加清晰，更强大，如某人的个人信息在对象中的表达结构如下：

   ```js
   person.name = '张三';
   person.sex = '男';
   person.age = 23;
   person.height = 178;
   ```

## 二、创建对象的三种方式

1. 利用**字面量**创建对象

   ```js
   // 创建一个空的对象
   var obj = {};
   
   //创建一个对象
   var obj = {
       uname: '张三',
       sex: '男',
       age: 23,
       height: 178,
       sayHi: function() {
           console.log('hi~');
       }
   }
   ```

   - 属性或方法采取**键值对**的形式；
   - 多个属性与方法用**逗号**隔开；
   - 方法冒号后跟的是一个**匿名函数**。

   使用对象

   ```js
   // 调用对象属性
   // 1)对象名.属性名
   console.log(obj.uname);
   // 2)对象名['属性名']
   console.log(obj['age']);
   
   // 调用对象方法
   // 对象名.方法名
   obj.sayHi();
   ```

2. 利用**new Object**创建对象

   ```js
   var obj = new Object();
   obj.name = '张三';
   obj.sex = '男';
   obj.age = 23;
   obj.height = 178;
   obj.sayHi = function() {
   	console.log('hi~');
   }
   ```

   - 利用 =  赋值的方法添加对象的属性和方法；
   - 每个属性和方法之间用分号分隔。

3. 利用**构造函数**创建对象

   使用前两种创建对象的方式，一次只能创建一个对象。

   我们可以利用构造函数，重复创建对象的属性和方法。构造函数，就是把我们对象里面一些相同的属性和方法抽象出来封装到函数里面。

   ```js
   // 声明 
   function 构造函数名() {
   	this.属性 = 值;
   	this.方法 = function() {}
   }
   
   // 使用
   new 构造函数名();
   // 通过new关键字创建对象的过程我们也称为对象的实例化
   ```
   
   ```js
   // 构造函数名字首字母要大写
   function Star(uname, age, sex) {
   	this.name = uname;
   	this.age = age;
   	this.sex = sex;
       this.sing = function(sang) {
           console.log(sang);
       }
   }
   var ldh = new Star('刘德华', 60， '男');
   ldh.sing('冰雨');
   ```

## 三、new关键字

new关键字执行过程：

- new构造函数在内存中创建一个空的对象；
- this指向刚才创建的空对象；
- 执行构造函数内部代码，给空对象添加属性和方法；
- 返回这个新对象。

## 四、遍历对象属性

**for...in** 语句用于对数组或者对象的属性进行循环操作。

```js
for (变量 in 对象) {

}
```

```js
var obj = {
    uname: '张三',
    sex: '男',
    age: 23,
    height: 178,
    sayHi: function() {
        console.log('hi~');
    }
}

// 变量 常用 k 或者 key
for (var key in obj) {
	console.log(key);	// 对象属性名
	console.log(obj[key]);	// 对象属性值
}
```

# JavaScript 内置对象

## 一、内置对象

JavaScript中的对象分为3种：**自定义对象**、**内置对象**、**浏览器对象**。

**内置对象**：JS语言自带的一些对象。这些对象供开发者使用并提供了一些常用的或最基本且必要的功能（属性和方法）。内置对象最大的优点就是帮助我们快速开发。如Math、Date、Array、String等。

## 二、查文档

学习一个内置对象的使用，只要学会其常用成员的使用即可，我们可以通过查询文档进行学习（MDN / W3C）。

Mozilla 开发者网络（MDN）提供了有关开放网络技术（Open Web）的信息，包括HTML、CSS和万维网及HTML5应用的API。

官网：https://developer.mozilla.org/zh-CN/

## 三、Math对象

Math是一个内置对象，它具有数学常数和函数的属性和方法。不是一个函数对象。

Math数学对象不是一个构造函数，所以我们不需要通过new来调用，而是直接使用里面的属性和方法即可。

1. 属性

   | 属性         | 说明                                                         |
   | ------------ | ------------------------------------------------------------ |
   | Math.E       | 欧拉常数，也是自然对数的底数，约等于 2.718。                 |
   | Math.LN2     | 2 的自然对数，约等于 0.693。                                 |
   | Math.LN10    | 10 的自然对数，约等于 2.303。                                |
   | Math.LOG2E   | 以 2 为底的 E 的对数，约等于 1.443。                         |
   | Math.LOG10E  | 以 10 为底的 E 的对数，约等于 0.434。                        |
   | **Math.PI**  | **圆周率**，一个圆的周长和直径之比，约等于 3.14159。         |
   | Math.SQRT1_2 | 二分之一 ½ 的平方根，同时也是 2 的平方根的倒数 12，约等于 0.707。 |
   | Math.SQRT2   | 2 的平方根，约等于 1.414。                                   |

2. 方法

   | 方法                        | 说明                                                         |
   | --------------------------- | ------------------------------------------------------------ |
   | **Math.abs(x)**             | 返回一个数的**绝对值**。                                     |
   | Math.acos(x)                | 返回一个数的反余弦值。                                       |
   | Math.acosh(x)               | 返回一个数的反双曲余弦值。                                   |
   | Math.asin(x)                | 返回一个数的反正弦值。                                       |
   | Math.asinh(x)               | 返回一个数的反双曲正弦值。                                   |
   | Math.atan(x)                | 返回一个数的反正切值。                                       |
   | Math.atanh(x)               | 返回一个数的反双曲正切值。                                   |
   | Math.atan2(y, x)            | 返回 y/x 的反正切值。                                        |
   | Math.cbrt(x)                | 返回一个数的立方根。                                         |
   | **Math.ceil(x)**            | 返回大于一个数的最小整数，即一个数**向上取整**后的值。       |
   | Math.clz32(x)               | 返回一个 32 位整数的前导零的数量。                           |
   | Math.cos(x)                 | 返回一个数的余弦值。                                         |
   | Math.cosh(x)                | 返回一个数的双曲余弦值。                                     |
   | Math.exp(x)                 | 返回欧拉常数的参数次方，Ex，其中 x 为参数，E 是欧拉常数（2.718...，自然对数的底数）。 |
   | Math.expm1(x)               | 返回 exp(x) - 1 的值。                                       |
   | **Math.floor(x)**           | 返回小于一个数的最大整数，即一个数**向下取整**后的值。       |
   | Math.fround(x)              | 返回最接近一个数的单精度浮点型表示。                         |
   | Math.hypot([x[, y[, …]]])   | 返回其所有参数平方和的平方根。                               |
   | Math.imul(x, y)             | 返回 32 位整数乘法的结果。                                   |
   | Math.log(x)                 | 返回一个数的自然对数（㏒e，即 ㏑）。                         |
   | Math.log1p(x)               | 返回一个数加 1 的和的自然对数（㏒e，即 ㏑）。                |
   | Math.log10(x)               | 返回一个数以 10 为底数的对数。                               |
   | Math.log2(x)                | 返回一个数以 2 为底数的对数。                                |
   | **Math.max([x[, y[, …]]])** | 返回零到多个数值中**最大值**。                               |
   | **Math.min([x[, y[, …]]])** | 返回零到多个数值中**最小值**。                               |
   | Math.pow(x, y)              | 返回一个数的 y 次幂。                                        |
   | **Math.random()**           | 返回一个 **0 到 1 之间的伪随机数（取值范围为 [0, 1) ）**。   |
   | **Math.round(x)**           | 返回**四舍五入**后的整数。                                   |
   | Math.sign(x)                | 返回一个数的符号，得知一个数是正数、负数还是 0。             |
   | Math.sin(x)                 | 返回一个数的正弦值。                                         |
   | Math.sinh(x)                | 返回一个数的双曲正弦值。                                     |
   | Math.sqrt(x)                | 返回一个数的平方根。                                         |
   | Math.tan(x)                 | 返回一个数的正切值。                                         |
   | Math.tanh(x)                | 返回一个数的双曲正切值。                                     |
   | Math.toSource()             | 返回字符串 "Math"。                                          |
   | Math.trunc(x)               | 返回一个数的整数部分，直接去除其小数点及之后的部分。         |

3. 练习：封装自己的数学对象

   ```js
   var myMath = {
       PI: 3.141592653,
       max: function () {
           var max = arguments[0];
           for (var i = 1; i < arguments.length; i++) {
               if (max < arguments[i]) {
                   max = arguments[i];
               }
           }
           return max;
       },
       min: function () {
           var min = arguments[0];
           for (var i = 1; i < arguments.length; i++) {
               if (min > arguments[i]) {
                   max = arguments[i];
               }
           }
           return min;
       }
   }
   
   console.log(myMath.PI)
   console.log(myMath.max(1, 5, 9));
   console.log(myMath.min(1, 5, 9));
   ```

4.   得到两数之间的随机整数（不包含这两个数）

   ```js
   function getRandomInt(min, max) {
   	min = Math.ceil(min);
   	max = Math.floor(max);
   	return Math.floor(Math.random() * (max - min)) + min;
   }
   ```

   得到两书之间的随机整数（包含这两个数）

   ```js
   function getRandomInt(min, max) {
   	min = Math.ceil(min);
   	max = Math.floor(max);
   	return Math.floor(Math.random() * (max - min + 1)) + min;
   }
   ```

5. 练习：随机点名

   ```js
   function getRandomInt(min, max) {
   	min = Math.ceil(min);
   	max = Math.floor(max);
   	return Math.floor(Math.random() * (max - min + 1)) + min;
   }
   
   var student = ['张三', '李四', '王舞', '齐六', '解八', '吴九'];
   console.log(student[getRandomInt(0,student.length - 1)]);
   ```

6. 练习：猜数字游戏

   ```js
   function getRandomInt(min, max) {
       min = Math.ceil(min);
       max = Math.floor(max);
       return Math.floor(Math.random() * (max - min + 1)) + min;
   }
   var num = getRandomInt(1, 10);
   while (true) {
       var userNum = prompt('猜数字（1-10）：');
       if (userNum > num) {
           alert('大了！');
       } else if (userNum < num) {
           alert('小了！');
       } else if (userNum == num) {
           alert('恭喜！您猜对了！');
           break;
       } else {
           alert('请输入数字！');
       }
   }
   ```

## 四、日期对象

创建Date实例用来处理**日期和时间**。

日期对象是一个**构造函数**，必须使用new来调用我们的日期对象。

```js
new Date();
new Date(value);
new Date(dateString);
new Date(year, monthIndex [, day [, hours [, minutes [, seconds [, milliseconds]]]]]);
```

- 如果没有输入任何参数，则Date的构造器会依据**系统的当前时间**来创建一个Date对象；
- 参数常见写法：

```js
var date1 = new Date(2019, 10, 1);
console.log(date1);	// 返回的是11月而不是10月	// 比实际月份大1个月

var date2 = new Date(2019-10-1);
console.log(date2);	// 返回的是 Tue Oct 01 2019 00:00:00 GMT+0800
```

日期格式化：

| 方法名        | 说明                            | 代码               |
| ------------- | ------------------------------- | ------------------ |
| getFullYear() | 获取当前年                      | dObj.getFullYear() |
| getMonth()    | 获取当前月（0-11）              | dObj.getMonth()    |
| getDate()     | 获取当天日期                    | dObj.getDate()     |
| getDay()      | 获取当前星期（从周日0 - 周六6） | dObj.getDay()      |
| getHours()    | 获取当前小时                    | dObj.getHours()    |
| getMinutes()  | 获取当前分钟                    | dObj.getMinutes()  |
| getSeconds()  | 获取当前秒钟                    | dObj.getSeconds()  |

```js
var week = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
var date = new Date();

var year = date.getFullYear();
var month = date.getMonth() + 1;
var dates = date.getDate();
var day = date.getDay();

console.log('今天是' + year + '年' + month + '月' + dates + '日' + week[day]);
```

```js
function getTime() {
	var time = new Date();
	var h = time.getHours();
	h = h < 10 ? '0' + h : h;	// 补0
	var m = time.getMinutes();
	m = m < 10 ? '0' + m : m;
	var s = time.getSeconds();
	s = s < 10 ? '0' + s : s;
	return h + ':' + m + ':' + s;
}
console.log(getTime());
```

获取日期总的毫秒形式：

Date对象是基于1970年1月1日（世界标准时间）起的毫秒数

```js
// 1. 通过valueOf() getTime()
var date = new Date();
console.log(date.valueOf());	// 当前时间距离1970.1.1 总的毫秒数
console.log(date.getTime());

// 2. 简单的写法（最常用写法）
var date = +new Date();	// +new Date() 返回的就是总的毫秒数

// 3. H5新增 获得总毫秒数
console.log(Date.now());
```

案例：倒计时

```js
function countDown(time) {
    var nowTime = +new Date(); // 返回当前时间的总毫秒数
    var inputTime = +new Date(time); // 返回预设时间的总毫秒数
    var times = (inputTime - nowTime) / 1000; // 剩余时间总毫秒数 转换为s
    var d = parseInt(times / 60 / 60 / 24); // 天
    d = d < 10 ? '0' + d : d;
    var h = parseInt(times / 60 / 60 % 24); // 时
    h = h < 10 ? '0' + h : h;
    var m = parseInt(times / 60 % 60); // 分
    m = m < 10 ? '0' + m : m;
    var s = parseInt(times % 60); // 秒
    s = s < 10 ? '0' + s : s;
    return d + '天' + h + '时' + m + '分' + s + '秒';
}
console.log(countDown('2021-12-12 00:00:00'));
```

## 五、数组对象

### 1.数组对象的创建

- 字面量

  ```js
  var arr = [1, 2, 3];
  console.log(arr[0]);
  ```

- new Array()

  ```js
  var arr = new Array(2);
  console.log(arr);	// Array(2) [empty × 2]
  
  var arr = new Array(2, 3);
  console.log(arr);	// Array(2) [2, 3]
  ```

### 2.检测是否为数组

- **instanceof**

  ```js
  var arr = [];
  var obj = {};
  console.log(arr instanceof Array);	// true
  console.log(obj instanceof Array);	// false
  ```

- **Array.isArray()**

  ```
  var arr = [];
  var obj = {};
  console.log(Array.isArray(arr));	// true
  console.log(Array.isArray(obj));	// false
  ```

  H5新增的方法，IE9以上版本支持。

### 3.添加或删除数组元素

| 方法名                | 说明                               | 返回值               |
| --------------------- | ---------------------------------- | -------------------- |
| **push(参数1...)**    | 在数组末尾添加一个或多个元素       | 返回新的长度         |
| **pop()**             | 删除数组最后一个元素，将数组长度-1 | 返回它删除的元素的值 |
| **unshift(参数1...)** | 在数组开头添加一个或多个元素       | 返回新的长度         |
| **shift()**           | 删除数组的第一个元素，将数组长度-1 | 返回它删除的元素的值 |

```js
var arr = [1, 2, 3];
arr.push(4);
console.log(arr);	// [1, 2, 3, 4]
arr.pop();
console.log(arr);	// [1, 2, 3]
arr.unshift(0);
console.log(arr);	// [0, 1, 2, 3]
arr.shift();
console.log(arr);	// [1, 2, 3]
```

练习：筛选数组

```js
var salary = [1500, 1200, 2000, 2100, 1800];
var newSalary = [];
for (var i = 0; i < salary.length; i++) {
	if (salary[i] <= 2000) {
		// newSalary[newSalary.length] = salary[i];
		newSalary.push(salary[i]);
	}
}
console.log(newSalary);
```

### 4.数组排序

| 方法名        | 说明                   |
| ------------- | ---------------------- |
| **reverse()** | 翻转数组中元素的顺序   |
| **sort()**    | 对数组内的元素进行排序 |

```js
var arr = ['blue', 'red', 'pink'];
arr.reverse();
console.log(arr);	// ['pink', 'red', 'blue']
```

```js
var arr = [3, 4, 7, 1];
arr.sort();
console.log(arr);	// [1, 3, 4, 7] √

var arr = [13, 4, 77, 1, 7];
arr.sort();
console.log(arr);	// [1, 13, 4, 7, 77] ×

// sort()排序完美写法
var arr = [13, 4, 77, 1, 7];
arr.sort(function(a, b) {
	return a - b;	// 升序
});
console.log(arr);	// [1, 4, 7, 13, 77]
arr.sort(function(a, b) {
    return b - a;	// 降序
})
console.log(arr);	// [77, 13, 7, 4, 1]
```

### 5.数组索引方法

| 方法名        | 说明                                                       | 返回值                                     |
| ------------- | ---------------------------------------------------------- | ------------------------------------------ |
| **indexOf()** | 查找数组中第一个满足条件的给定元素的索引号（从前往后查找） | 如果**存在，返回索引号，不存在，则返回-1** |
| lastIndexOf() | 查找数组中第一个满足条件的给定元素的索引号（从后往前查找） | 如果存在，返回索引号，不存在，则返回-1     |

```js
var arr = ['red', 'green', 'blue', 'pink', 'blue'];
console.log(arr.indexOf('blue'));	// 2
console.log(arr.lastIndexOf('blue'));	// 4
```

练习：数组去重

```js
var arr = ['c', 'a', 'z', 'a', 'x', 'a', 'x', 'c', 'b'];
var newArr = [];

// 遍历旧数组 拿旧数组元素去查询新数组中是否已经存在，若存在 则不添加，反之，添加
for (var i = 0; i < arr.length; i++) {
	var flag = newArr.indexOf(arr[i]);
	if (flag == -1) {
		newArr.push(arr[i]);
	}
}
console.log(newArr);
```

### 6.数组转换为字符串

| 方法名         | 说明                                         | 返回值         |
| -------------- | -------------------------------------------- | -------------- |
| toString()     | 把数组转换为字符串，用逗号分隔每一项         | 返回一个字符串 |
| join('分隔符') | 该方法用于把数组中的所有元素转换为一个字符串 | 返回一个字符串 |

```js
var arr = [1, 2, 3];
console.log(arr.toString());	// 1,2,3
console.log(arr.join('&'));	// 1&2&3
```

### 7.其他

| 方法名      | 说明                                                         | 返回值                                     |
| ----------- | ------------------------------------------------------------ | ------------------------------------------ |
| concat()    | 连接两个或多个数组（不影响原数组）                           | 返回一个新的数组                           |
| **slice()** | 返回一个新的数组对象，这一对象是一个由 `begin` 和 `end` 决定的原数组的**浅拷贝**（包括 `begin`，不包括`end`） | 返回被**截取**项目的新数组（不影响原数组） |
| splice()    | 通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容 | 返回被删除项目的新数组（影响原数组）       |

```js
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// expected output: Array ["camel", "duck"]

console.log(animals.slice(1, 5));
// expected output: Array ["bison", "camel", "duck", "elephant"]

console.log(animals.slice(-2));
// expected output: Array ["duck", "elephant"]

console.log(animals.slice(2, -1));
// expected output: Array ["camel", "duck"]
```

```js
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at index 1
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "June"]

months.splice(4, 1, 'May');
// replaces 1 element at index 4
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "May"]

// 从索引 3 的位置开始删除 1 个元素
var myFish = ['angel', 'clown', 'drum', 'mandarin', 'sturgeon'];
var removed = myFish.splice(3, 1);
// 运算后的 myFish: ["angel", "clown", "drum", "sturgeon"]
// 被删除的元素: ["mandarin"]

// 从索引 2 的位置开始删除 1 个元素，插入“trumpet”
var myFish = ['angel', 'clown', 'drum', 'sturgeon'];
var removed = myFish.splice(2, 1, "trumpet");
// 运算后的 myFish: ["angel", "clown", "trumpet", "sturgeon"]
// 被删除的元素: ["drum"]
```

## 六、字符串对象

1. 基本包装类型：把简单数据类型包装为复杂数据类型，这样基本数据类型就拥有了属性和方法。

   ```js
   var str = 'andy';
   console.log(str.length);	// 只有复杂数据类型才有属性和方法 简单数据类型为什么会拥有length属性？
   
   // JS会把基本数据类型包装为复杂数据类型，其执行过程如下：
   // 1. 把简单数据类型包装为复杂数据类型
   var temp = new String('andy');
   // 2. 把临时变量的值赋给str
   str = temp;
   // 3. 销毁临时变量
   temp = null;
   ```

2. 字符串不可变：表面上我们修改字符串是更改了字符串的内容，但实际上是**开辟**了**新的内存空间**，将**地址指向新的空间**。

   ![image-20211127174338870](https://gitee.com/v876774538/my-img/raw/master/image-20211127174338870.png)

   由于字符串的不可变性，所以不要大量拼接字符串！（每次拼接都会产生新的字符串）

   ```js
   var str = '';
   // 由于字符串的不可变，在大量拼接字符串的时候会有效率问题
   for (var i = 1; i <= 1000000; i++) {
   	str += i;
   }
   console.log(str);	// 这个结果需要花费大量时间来显示，因为需要不断地开辟新的空间
   ```

3. 根据字符返回位置

   | 方法名        | 说明                                                         | 返回值                                 |
   | ------------- | ------------------------------------------------------------ | -------------------------------------- |
   | **indexOf()** | 查找字符串中第一个满足条件的给定元素的索引号（从前往后查找） | 如果存在，返回索引号，不存在，则返回-1 |
   | lastIndexOf() | 查找字符串中第一个满足条件的给定元素的索引号（从后往前查找） | 如果存在，返回索引号，不存在，则返回-1 |

   ```js
   // 字符串对象 根据字符返回位置
   // str.indexOf('要查找的字符',[起始查找位置]);
   var str = '改革春风吹满地';
   console.log(str.indexOf('春'));	// 2
   ```

   练习：查找字符串中元素出现的位置及次数

   ```js
   var str = 'abcoefoxyozzopp';
   var s = 'o';
   var n = 0; // 记录次数
   var index = str.indexOf(s);
   while (index != -1) {
       console.log(index);
       n++;
       index = str.indexOf(s, index + 1);
   }
   console.log(s + ' 共出现了：' + n + '次');
   	
   ```

   | 方法名            | 说明                                                        | 使用              |
   | ----------------- | ----------------------------------------------------------- | ----------------- |
   | charAt(index)     | 返回指定位置的字符                                          | str.cahrAt(0)     |
   | charCodeAt(index) | 获取指定位置处字符的ASCII码**（用于判断用户按下了什么键）** | str.charCodeAt(0) |
   | str[index]        | 获取指定位置处字符                                          | str[0]            |

   练习：统计出现最多的字符以及它出现的次数

   ```js
   // 判断对象是否有某属性：对象['属性名']
   var str = 'abcoefoxyozzopp';
   var o = {};
   for (var i = 0; i < str.length; i++) {
       var char = str[i];
       // 如果是o.char 就变成了o中的属性char一直做累加
       if (o[char]) {
           o[char]++;
       } else {
           o[char] = 1;
       }
   }
   console.log(o);
   getMax(o);
   
   function getMax(obj) {
       var max = 0;
       var ch = '';
       // 对象遍历
       for (var k in obj) {
           if (max < obj[k]) {
               max = obj[k];
               ch = k;
           }
       }
       console.log('出现最多的字符为：' + ch);
       console.log('出现次数为：' + max);
   }
   ```

4. **字符串操作方法**（重点）

   | 方法名                        | 说明                                                 |
   | ----------------------------- | ---------------------------------------------------- |
   | concat(str1, str2, str3, ...) | concat()方法用于连接两个或多个字符串。等效于+        |
   | **substr(start, length)**     | 从start位置（索引号）开始，length为取的个数          |
   | slice(start, end)             | 截取start到end位置的字符 **[start, end)**            |
   | substring(start, end)         | 截取start到end位置的字符 **[start, end)** 不接受负值 |

5. 替换字符串以及转换为数组

   | 方法名                                | 说明                     |
   | ------------------------------------- | ------------------------ |
   | replace('被替换字符', '替换为的字符') | 替换字符（只替换第一个） |
   | split('分隔符')                       | 字符转换为数组           |

   练习：字符替换

   ```js
   var str = 'abcoefoxyozzopp';
   var ch = 'o';
   while (str.indexOf(ch) != -1) {
   	str.replace(ch, '*');
   }
   console.log(str);
   ```

   练习：字符串转换为数组

   ```js
   var str = 'red,pink,blue';
   console.log(str.split(','));
   
   var str = 'red&pink&blue';
   console.log(str.split('&'));
   ```

# 简单数据类型和复杂数据类型

## 一、简单类型和复杂类型

**简单类型**又称为**基本数据类型**或**值类型**，**复杂类型**又叫做**引用类型**。

- 值类型：简单数据类型/基本数据类型，在存储变量中存储的是**值**本身，因此叫做值类型，如string，number，boolean，undefined，null（空的对象）；
- 引用类型：复杂数据类型，在存储变量中存储的仅仅是**地址**，因此叫做引用数据类型。通过new关键字创建的对象（系统对象、自定义对象），如Object、Array、Date等。

## 二、堆和栈

1. 栈：由操作系统自动分配释放，存放函数的参数值、局部变量的值等。其操作方式类似于数据结构中的栈。**简单数据类型存放到栈里面**，直接开辟一个空间存放数据的值；
2. 堆：存储复杂类型，一般由程序员进行分配释放，若程序员不释放，由垃圾回收机制回收。**复杂数据类型存放到堆里面**，首先在栈里面存放地址（十六进制），然后由地址指向堆里的数据。

## 三、简单类型传参

 函数的形参也可以看做是一个变量。

当我们把一个值类型变量作为参数传给形参时，其实是把变量在栈空间里的值复制了一份给形参，因此不论在方法内部对形参做任何改变，都不会影响外部变量。

```js
function fn(a) {
	a++;
	console.log(a);	// 11
}
var x = 10;
fn(x);
console.log(x);	// 10
```

## 四、复杂类型传参

 函数的形参也可以看做是一个变量。不同的是，当我们把引用变量传给形参时，是把变量在栈空间里保存的堆地址复制给形参，形参和实参保存的是同一个堆地址，操作的是同一个对象，因此在方法内部进行操作，会影响外部变量。

```js
function Person(name) {
	this.name = name;
}
function f1(x) {	// x = p
	console.log(x.name);	// 2. 刘德华
	x.name = '张学友';
	console.log(x.name);	// 3. 张学友
}
var p = new Person('刘德华');
console.log(p.name);	// 1. 刘德华
f1(p);
console.log(p.name); // 4. 张学友
```

![image-20211128205633475](https://gitee.com/v876774538/my-img/raw/master/image-20211128205633475.png)

# Web APIs

## 一、Web APIs 和 JS的关联性

1. JS组成

   ![image-20211128210058506](https://gitee.com/v876774538/my-img/raw/master/image-20211128210058506.png)

2. JS基础阶段以及Web APIs阶段

   ![image-20211128210225023](https://gitee.com/v876774538/my-img/raw/master/image-20211128210225023.png)

   JS基础学习ECMAScript 基础语法为后面做铺垫，Web APIs是JS的应用，大量使用JS基础语法做交互效果。

## 二、API 和 Web API

1. API

   API（Application Programming Interface，应用程序编程接口）是一些预先定义的函数。目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无序访问源码或理解内部工作机制的细节。

2. Web API

   Web API是浏览器提供的一套操作**浏览器功能**和**页面元素**的API（**BOM**和**DOM**）。

   MDN详细API文档：https://developer.mozilla.org/zh-CN/docs/Web/API

# DOM

## 一、DOM简介

1. 文档对象模型（Document Object Model，简称**DOM**），是W3C组织推荐的处理可扩展标记语言（HTML或XML）的标准**编程接口**。

   W3C已经定义了一系列的DOM接口，通过这些DOM接口可以改变网页的内容、结构和样式。

2. DOM树

   ![image-20211129173200554](https://gitee.com/v876774538/my-img/raw/master/image-20211129173200554.png)

   - **文档**：一个页面就是一个文档，DOM中使用document表示；
   - **元素**：页面中的所有标签都是元素，DOM中使用element表示；
   - **节点**：网页中的所有内容都是节点（标签、属性、文本、注释等），DOM中使用node表示。

   **DOM把以上内容都看做是对象。**

## 二、获取元素

### 1.根据元素ID获取 getElementById()

使用getElementById()方法可以**获取带有ID的元素对象**。

示例：

```html
// HTML
<!DOCTYPE html>
<html>
<head>
  <title>getElementById example</title>
</head>
<body>
  <p id="para">Some text here</p>
  <button onclick="changeColor('blue');">blue</button>
  <button onclick="changeColor('red');">red</button>
</body>
</html>
```

```js
// JavaScript
function changeColor(newColor) {
  var elem = document.getElementById('para');
  elem.style.color = newColor;
}
```

- 参数 **id** 是**大小写敏感的字符串**；

- 方法返回的是的是一个**元素对象**。

  在控制台中显示指定JavaScript对象的属性，并通过类似文件树样式的交互列表显示：

  ```js
  console.log(object);
  ```

### 2.根据标签名获取 getElementsByTagName()

使用getElementsByTagName()方法可以返回**带有指定标签名的对象的集合**。

```js
elements = element.getElementsByTagName(tagName);
```

- 返回的是获取过来元素对象的集合，以**伪数组**的形式存储；
- 可以采取遍历的方式，依次打印里面的元素对象；
- 得到的元素对象是**动态**的；
- 通过**element指定父元素**。

```js
// check the alignment on a number of cells in a table.
var table = document.getElementById("forecast-table");
// var table = document.getElementsByTagName('table');
// var cells = table[0].getElementsByTagName('td');
var cells = table.getElementsByTagName("td");
for (var i = 0; i < cells.length; i++) {
    var status = cells[i].getAttribute("data-status");
    if ( status == "open" ) {
        // grab the data
    }
}
```

### 3.通过HTML5新增的方式获取

- **getElementsByClassName()**

  ```js
  var elements = document.getElementsByClassName(names); // or:
  var elements = rootElement.getElementsByClassName(names);
  ```

- **querySelector()**

  querySelector方法返回文档中**与指定选择器或选择器组匹配的第一个**。

  ```js
  var element = document.querySelector(selectors);
  ```

  ```js
  // 返回当前文档中第一个类名为 "myclass" 的元素
  var el = document.querySelector(".myclass");
  
  // 返回当前文档中id为 "nav" 的元素
  val el = document.querySelector("#nav");
  
  // 返回当前文档中第一个li
  val el = document.querySelector("li");
  
  // 一个class属性为"user-panel main"的div元素<div>(<div class="user-panel main">)内包含一个name属性为"login"的input元素<input> (<input name="login"/>) 
  var el = document.querySelector("div.user-panel.main input[name='login']");
  ```

- **querySelectorAll()**

  返回与指定的选择器组匹配的文档中的**元素列表** (使用深度优先的先序遍历文档的节点)。

  ```js
  var elementList = parentNode.querySelectorAll(selectors);
  ```

  ```js
  // 活的当前稳当中所有类名为".box"的元素
  var allBox = document.querySelectorAll('.box');
  console.log(allBox);
  ```

### 4.特殊元素获取

- 获取body元素

  ```js
  var bodyEle = document.body;	// 返回body元素对象
  console.log(bodyEle);
  console.dir(bodyEle);	// 显示对象的所有属性和方法
  ```

- 获取html元素

  ```js
  var htmlEle = document.documentElement;	// 返回html元素对象
  console.log(htmlEle);
  ```

## 三、事件基础

1. 事件概述

   JavaScript使我们有能力创建动态页面，而事件是可以被JavaScript监测到的行为（**触发—响应** 机制）。

2. 事件三要素

   - 事件源
   - 事件类型
   - 事件处理程序

3. 执行事件的步骤

   - 获取事件源
   - 注册事件（绑定事件）
   - 添加事件处理程序（采取函数赋值方式）

   ```html
   <button id = "btn">唐伯虎</button>
   <script>
   	// 1. 获取事件源
   	var btn = document.getElementById('btn');
   	// 2. 绑定事件 btn.onclick
       // 事件类型：如鼠标点击(onclick) 鼠标经过 键盘按下...
   	// 3. 事件处理程序 btn.onclick = function(){}
   	btn.onclick = function() {
   		alert('点秋香');
   	}
   </script>
   ```

4. 常见的鼠标事件

   | 鼠标事件    | 触发条件         |
   | ----------- | ---------------- |
   | **onclick** | 鼠标点击左键触发 |
   | onmouseover | 鼠标经过触发     |
   | onmouseout  | 鼠标离开触发     |
   | onfocus     | 获得鼠标焦点触发 |
   | onblur      | 失去鼠标焦点触发 |
   | onmousemove | 鼠标移动触发     |
   | onmouseup   | 鼠标弹起触发     |
   | onmousedown | 鼠标按下触发     |

## 四、操作元素

JavaScript的DOM操作可以改变网页内容、结构和样式，我们可以利用DOM操作元素来改变元素里面的内容、属性等。

### 1.改变元素内容

`element.innerText`修改从起始位置到终止为止的内容，但会去除html标签，同时空格和换行也会去掉；

`element.innerHTML`修改起始位置到终止位置的全部内容，包括html标签，同时保留空格和换行。

注意：这两个元素是**可**以**读写**的。

```html
<p>我是文字</p>
<script>
	var p = document.querySelector('p');
	console.log(p.innerText);
</script>
```

```html
<button>获取时间</button>
<div></div>
<p></p>
<script>
    // 1. 获取元素
    var btn = document.querySelector('button');
    var div = document.querySelector('div');
    // 2. 注册事件
    // 3. 事件处理程序
    btn.onclick = function () {
        div.innerText = getDate();
    }

    function getDate() {
        var week = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
        var date = new Date();

        var year = date.getFullYear();
        var month = date.getMonth() + 1;
        var dates = date.getDate();
        var day = date.getDay();

        return '今天是' + year + '年' + month + '月' + dates + '日' + week[day];
    }
    
    // 不添加事件进行内容修改
    var p = document.querySelector('p');
    p.innerText = getDate();
</script>
```

innerText与innerHTML的区别：

- **innerText不识别HTML标签（去除HTML标签），会去除空格和换行；**
- **innerHTML则会保留HTML标签，保留空格和换行。**

### 2.修改元素属性

```html
<button id="ldh">刘德华</button>
<button id="zxy">张学友</button>
<img src="images/ldh.jpg" alt="" title="刘德华">
<script>
	// 1. 获取元素
	var ldh = document.getElementById('ldh');
	var zxy = document.getElementById('zxy');
	var img = document.querySelector('img');
	// 2. 注册事件
	zxy.onclick = function() {
		img.src = 'images/zxy.jpg';
		img.title = '张学友';
	}
	ldh.onclick = function() {
		img.src = 'images/ldh.jpg';
		img.title = '刘德华';
	}
</script>
```

案例：分时问候

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>分时问候</title>
    <style>
        img {
            width: 300px;
        }
    </style>
</head>

<body>
    <img src="images/z.gif" alt="">
    <div>早上好！</div>
    <script>
        var img = document.querySelector('img');
        var div = document.querySelector('div');

        // 日期对象
        var date = new Date();
        var h = date.getHours();
        if (h < 9) {
            img.src = 'images/z.gif';
            div.innerText = '早上好！';
        } else if (h < 13) {
            img.src = 'images/s.gif';
            div.innerText = '上午好！';
        } else if (h < 18) {
            img.src = 'images/x.gif';
            div.innerText = '下午好！';
        } else {
            img.src = 'images/w.gif';
            div.innerText = '晚上好！';
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo19/demo19_2.html

### 3.修改表单属性

利用DOM可以操作如type、value、checked、selected、disabled等属性。

```html
<button>按钮</button>
<input type="text" placeholder="输入内容">
<script>
    var btn = document.querySelector('button');
    var input = document.querySelector('input');
    btn.onclick = function () {
        input.placeholder = '被点击了！';
    }
</script>
```

案例：仿京东显示隐藏密码明文

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>仿京东显示隐藏密码明文</title>
    <style>
        .box {
            position: relative;
            width: 400px;
            border-bottom: 1px solid #ccc;
            margin: 100px auto;
        }

        .box input {
            width: 370px;
            height: 30px;
            border: 0;
            outline: none;
        }

        .box img {
            position: absolute;
            top: 2px;
            right: 2px;
            width: 24px;
        }
    </style>
</head>

<body>
    <div class="box">
        <label for="">
            <img src="images/close.png" alt="" id="eye">
        </label>
        <input type="password" id="pwd">
    </div>
    <script>
        var eye = document.getElementById('eye');
        var pwd = document.getElementById('pwd');
        var flag = 0;
        eye.onclick = function () {
            if (flag == 0) {
                pwd.type = 'text';
                eye.src = 'images/open.png';
            } else {
                pwd.type = 'password';
                eye.src = 'images/close.png';
            }
            flag = !flag;
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo19/demo19_4.html

### 4.样式属性操作

我们可以通过JS修改元素的大小、颜色、位置等样式。

`element.style`行内样式操作；

`element.className`类名样式操作。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div></div>
    <script>
        var div = document.querySelector('div');
        div.onclick = function () {
            div.style.backgroundColor = 'purple';
            // 注意：
            // js中的样式采取驼峰命名法，如fontSize、backgroundColor
            // js中修改style样式操作，产生的是行内样式，css权重较高
        }
    </script>
</body>

</html>
```

案例：淘宝点击关闭二维码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>淘宝关闭二维码</title>
    <style>
        .box {
            position: relative;
            width: 74px;
            height: 88px;
            border: 1px solid #ccc;
            margin: 100px auto;
            font-size: 12px;
            text-align: center;
            color: #f40;
            /* display: block; */
        }

        .box img {
            width: 60px;
            margin-top: 5px;
        }

        .close-btn {
            position: absolute;
            top: -1px;
            left: -16px;
            width: 14px;
            height: 14px;
            border: 1px solid #ccc;
            line-height: 14px;
            font-family: Arial, Helvetica, sans-serif;
            cursor: pointer;
        }
    </style>
</head>

<body>
    <div class="box">
        淘宝二维码
        <img src="images/tao.png" alt="">
        <i class="close-btn">×</i>
    </div>
    <script>
        var btn = document.querySelector('.close-btn');
        var box = document.querySelector('.box');
        btn.onclick = function () {
            box.style.display = 'none';
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E3%80%9027%E3%80%91%E6%BA%90%E7%A0%81+%E8%AF%BE%E4%BB%B6+%E8%BD%AF%E4%BB%B6/07-10%20JavaScript%E7%BD%91%E9%A1%B5%E7%BC%96%E7%A8%8B/02-WebAPI%E7%BC%96%E7%A8%8B%E8%B5%84%E6%96%99/Web%20APIs-day01/2-%E6%A1%88%E4%BE%8B/14-%E5%85%B3%E9%97%AD%E6%B7%98%E5%AE%9D%E4%BA%8C%E7%BB%B4%E7%A0%81%E6%A1%88%E4%BE%8B.html

案例：循环精灵图背景

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>循环精灵图背景</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        li {
            list-style: none;
        }

        .box {
            width: 250px;
            margin: 100px auto;
        }

        .box li {
            float: left;
            width: 24px;
            height: 24px;
            background-color: pink;
            margin: 15px;
            background: url(images/sprite.png) no-repeat;
        }
    </style>
</head>

<body>
    <div class="box">
        <ul>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
    <script>
        // 获取所有的li
        var lis = document.querySelectorAll('li');
        for (var i = 0; i < lis.length; i++) {
            var y = i * 44;
            // 0 0 // 0 -44px // 0 -88px...
            lis[i].style.backgroundPosition = '0 ' + (-y) + 'px';
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo19/demo19_7.html

使用className修改样式属性：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>通过className修改样式属性</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }

        .change {
            background-color: purple;
        }
    </style>
</head>

<body>
    <div></div>
    <script>
        var div = document.querySelector('div');
        div.onclick = function () {
            this.className = 'change';
        }
    </script>
</body>

</html>
```

- 如果样式修改较多，可以采取操作类名方式更改元素样式；
- class由于是个保留字，因此使用className来操作元素类名属性；
- className会直接**更改元素的类名**（而不是追加）。

案例：密码框验证信息

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>密码框验证信息</title>
    <style>
        div {
            width: 600px;
            margin: 100px auto;
        }

        input {
            outline: none;
        }

        .message {
            display: inline-block;
            font-size: 12px;
            color: #ccc;
            background: url(images/mess.png) no-repeat left center;
            padding-left: 20px;
        }

        .right {
            color: green;
            background: url(images/right.png) no-repeat left center;
        }

        .wrong {
            color: red;
            background: url(images/wrong.png) no-repeat left center;
        }
    </style>
</head>

<body>
    <div>
        <input type="password" class="ipt">
        <p class="message">请输入6-16位密码</p>
    </div>
    <script>
        var ipt = document.querySelector('.ipt');
        var msg = document.querySelector('.message');
        ipt.onblur = function () {
            // console.log(ipt.value);
            if (6 <= ipt.value.length && ipt.value.length <= 16) {
                msg.className = 'message right';
                msg.innerHTML = '输入正确'

            } else {
                msg.className = 'message wrong';
                msg.innerHTML = "输入错误，请输入6-16位"
            }
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo19/demo19_9.html

### 5.排他思想

如果有同一组元素，我们想要某一个元素实现某种样式，就需要用到**循环**的**排他思想**算法：

1. 所有元素全部清除样式（干掉其他人）；
2. 给当前元素设置样式（留下我自己）。

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
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <script>
        // var btn = document.querySelectorAll('button');
        var btns = document.getElementsByTagName('button');
        for (var i = 0; i < btns.length; i++) {
            btns[i].onclick = function () {
                // 1）先去掉所有按钮的背景颜色
                for (var j = 0; j < btns.length; j++) {
                    btns[j].style.backgroundColor = '';
                }
                // 2）修改当前选择的按钮的背景颜色
                this.style.backgroundColor = 'pink';
            }
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo19/demo19_10.html

案例：百度换肤效果

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>百度换肤效果</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        body {
            background: url(images/1.jpg) no-repeat center top;
        }

        .baidu {
            overflow: hidden;
            width: 410px;
            margin: 200px auto;
            padding-top: 3px;
            border: 1px solid #ccc;
        }

        .baidu li {
            float: left;
            list-style: none;
            margin: 0 1px;
        }

        .baidu img {
            width: 100px;
        }
    </style>
</head>

<body>
    <ul class="baidu">
        <li><img src="images/1.jpg" alt=""></li>
        <li><img src="images/2.jpg" alt=""></li>
        <li><img src="images/3.jpg" alt=""></li>
        <li><img src="images/4.jpg" alt=""></li>
    </ul>
    <script>
        // var imgs = document.getElementsByTagName('img');
        var imgs = document.querySelector('.baidu').querySelectorAll('img');
        var body = document.body;
        for (var i = 0; i < imgs.length; i++) {
            imgs[i].onclick = function () {
                // 图片路径
                var src = this.src;
                body.style.backgroundImage = 'url(' + src + ')';
            }
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo20/demo20_2.html

案例：新浪财经表格隔行变色

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>表格隔行变色效果</title>
    <style>
        table {
            width: 800px;
            margin: 100px auto;
            text-align: center;
            /* 为表格设置合并边框模型 */
            border-collapse: collapse;
            font-size: 14px;
        }

        thead tr {
            height: 30px;
            background-color: skyblue;
        }

        tbody tr {
            height: 30px;
        }

        tbody td {
            border-bottom: 1px solid #d7d7d7;
            font-size: 12px;
            color: blue;
        }

        /* css做法 */
        /* tbody tr:hover {
            background-color: pink;
        } */
    </style>
</head>

<body>
    <table>
        <thead>
            <tr>
                <th>代码</th>
                <th>名称</th>
                <th>最新公布净值</th>
                <th>累计净值</th>
                <th>前单位净值</th>
                <th>净值增长率</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>002526</td>
                <td>农银金穗3个月定制开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>002526</td>
                <td>农银金穗3个月定制开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>002526</td>
                <td>农银金穗3个月定制开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>002526</td>
                <td>农银金穗3个月定制开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>002526</td>
                <td>农银金穗3个月定制开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>
            <tr>
                <td>002526</td>
                <td>农银金穗3个月定制开放债券</td>
                <td>1.075</td>
                <td>1.079</td>
                <td>1.074</td>
                <td>+0.047%</td>
            </tr>

        </tbody>
    </table>
    <!-- js做法 -->
    <script>
        var trs = document.querySelector('tbody').querySelectorAll('tr');
        for (var i = 0; i < trs.length; i++) {
            // 鼠标经过事件
            trs[i].onmouseover = function () {
                this.style.backgroundColor = 'pink';
            }
            // 鼠标离开事件
            trs[i].onmouseout = function () {
                this.style.backgroundColor = '';
            }
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo20/demo20_3.html

案例：表单全选以及取消全选

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>表单全选以及取消全选</title>
    <style>
        .wrap table {
            width: 500px;
        }

        .wrap thead tr {
            background-color: skyblue;
            height: 40px;
            color: #fff;
        }

        .wrap tbody tr {
            height: 30px;
            text-align: center;
        }
    </style>
</head>

<body>
    <div class="wrap">
        <table>
            <thead>
                <tr>
                    <th>
                        <input type="checkbox" id="j_tbAll">
                    </th>
                    <th>商品</th>
                    <th>价钱</th>
                </tr>
            </thead>
            <tbody id="j_tb">
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>iPhone8</td>
                    <td>8000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>iPhone8</td>
                    <td>8000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>iPhone8</td>
                    <td>8000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>iPhone8</td>
                    <td>8000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>iPhone8</td>
                    <td>8000</td>
                </tr>
                <tr>
                    <td>
                        <input type="checkbox">
                    </td>
                    <td>iPhone8</td>
                    <td>8000</td>
                </tr>
            </tbody>
        </table>
    </div>
    <script>
        var checkAll = document.getElementById('j_tbAll');
        var checks = document.getElementById('j_tb').getElementsByTagName('input');
        checkAll.onclick = function () {
            // 全选按钮当前的选中状态 this.checked
            for (var i = 0; i < checks.length; i++) {
                checks[i].checked = this.checked;
            }
        }
        // 给每一个单选按钮绑上事件
        for (var i = 0; i < checks.length; i++) {
            checks[i].onclick = function () {
                var flag = true;
                for (var j = 0; j < checks.length; j++) {
                    if (checks[j].checked == false) {
                        flag = false;
                        break;
                    }
                }
                if (flag == true) {
                    checkAll.checked = true;
                } else {
                    checkAll.checked = false;
                }
            }
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo20/demo20_4.html

### 6.自定义属性的操作

1. 获取属性值

   `element.属性`获取内置属性值（元素本身自带的属性）

   `element.getAttribute('属性');`主要获取自定义的属性

2. 设置属性值

   `element.属性 = 值`

   `element.setAttribute('属性', 值);`

   ```js
   div.setAttribute('class', 'footer');
   ```

3. 移除属性

   `element.removeAttribute('属性');`

4. 案例：**tab栏切换**

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>tab栏切换布局分析</title>
       <style>
           * {
               margin: 0;
               padding: 0;
           }
   
           li {
               list-style: none;
           }
   
           .tab {
               width: 978px;
               margin: 100px auto;
           }
   
           .tab_list {
               height: 39px;
               border: 1px solid #ccc;
               background-color: #f1f1f1;
           }
   
           .tab_list li {
               float: left;
               height: 39px;
               line-height: 39px;
               padding: 0 20px;
           }
   
           /* 被选中的tab栏 */
           .tab_list .current {
               background-color: #c81623;
               color: #fff;
           }
   
           .item {
               display: none;
           }
       </style>
   </head>
   
   <body>
       <div class="tab">
           <div class="tab_list">
               <ul>
                   <li class="current">商品介绍</li>
                   <li>规格与包装</li>
                   <li>售后保障</li>
                   <li>商品评价</li>
                   <li>手机社区</li>
               </ul>
           </div>
           <div class="tab_con">
               <div class="item" style="display:block">商品介绍模块内容</div>
               <div class="item">规格与包装模块内容</div>
               <div class="item">售后保障模块内容</div>
               <div class="item">商品评价模块内容</div>
               <div class="item">手机社区模块内容</div>
           </div>
       </div>
       <script>
           var tabs = document.querySelector('.tab_list').querySelectorAll('li');
           var items = document.querySelectorAll('.item');
           for (var i = 0; i < tabs.length; i++) {
               // 为tab设置索引
               tabs[i].setAttribute('index', i);
               tabs[i].onclick = function () {
                   for (var j = 0; j < tabs.length; j++) {
                       tabs[j].className = '';
                   }
                   this.className = 'current';
                   for (var j = 0; j < tabs.length; j++) {
                       items[j].style.display = 'none';
                   }
                   // 需要获取该自定义属性
                   var index = this.getAttribute('index');
                   items[index].style.display = 'block';
               }
           }
       </script>
   </body>
   
   </html>
   ```

   ### 7.自定义属性
   
   自定义属性目的：**为了保存并使用数据。**有些数据可以保存到页面中而不用保存到数据库中。
   
   自定义属性是通过**getAttribute('属性')**来获取。但有些自定义属性很容易引起歧义，不容易判断是元素的内置属性还是自定义属性。
   
   1. 设置H5自定义属性
   
      H5规定，自定义属性**以data-开头**作为属性名并赋值。
   
      例如，`<div data-index='1'></div>`
   
   2. 获取H5自定义属性
   
      - 兼容性获取：`element.getAttribute('data-index');`
      - H5新增获取：`element.dataset.index` 或 `element.dataset['index']`。
   
      dataset是一个集合，里面存放了所有以data开头的自定义属性。
   
      若自定义属性里面含有**多个-链接**的单词，我们获取时采取**驼峰命名法**：
   
      ```js
      console.log(div.getAttribute('data-list-name'));
      console.log(div.dataset.listName);
      ```

## 五、节点操作

1. 意义

   获取元素通常使用两种方式：

   1. 利用DOM提供的方法获取元素
      - document.getElementById()
      - document.getElementsByTagName()
      - document.querySelector()....
      - 逻辑性不强、繁琐
   2. 利用节点层级关系获取元素
      - 利用父子兄节点关系获取元素
      - 逻辑性强、兼容性较差

2. 节点概述

   网页中的所有内容都是节点（标签、属性、文本、注释...），在DOM中，节点使用node来表示。

   HTML DOM树中的所有节点均可通过JavaScript进行访问，所有HTML元素（节点）均可被修改，也可以创建或删除。

   一般的，节点至少拥有**nodeType（节点类型）**、**nodeName（节点名称）**和**nodeValue（节点值）**这三个基本属性。

   - 元素节点nodeType为1；
   - 属性节点nodeType为2；
   - 文本节点nodeType为3（文字、空格、换行等）。

3. 节点层级

   利用DOM树可以把节点划分为不同的层级关系，常见的是**父子兄层级关系**。

   ![image-20211204204200985](https://gitee.com/v876774538/my-img/raw/master/image-20211204204200985.png)

   1. 74父级节点 `node.parentNode`

      ```html
      <div class="demo">
      	<div class="box">
              <span class="erweima">×</span>
          </div>
      </div>
      <script>
          var erweima = document.querySelector('.eraweima');
          console.log(erweima.parentNode);
      // 相当于 document.querySelector('.box');    
      // 得到的是离元素最近的父级节点，若找不到则返回null
      </script>
      ```

   2. 子节点

       `parentNode.childNodes`（标准）

      ```html
      <ul>
      	<il></il>
          <li></li>
          <li></li>
          <li></li>
      </ul>
      <script>
      	var ul = document.querySelector('ul');
          for (var i = 0; i < ul.childNodes.length; i++) {
              
              if (ul.childNodes[i].nodeType == 1) {
                  // 判断ul.childNodes[i] 是否为元素节点
                  console.log(ul.childNodes[i]);
              }
          }
      </script>
      ```

      **`parentNode.children`（非标准）**

      parentNode.children是一个只读属性，返回所有的子**元素节点**。它只返回子元素节点，其余节点不返回。

      ```html
      <ul>
      	<il></il>
          <li></li>
          <li></li>
          <li></li>
      </ul>
      <script>
      	var ul = document.querySelector('ul');
          console.log(ul.children);
      </script>
      ```

      `parentNode.firstChild` 获取元素的第一个子节点

      `parentNode.firstElementChild` 获取元素的第一个子元素节点（IE9以上支持）

      `parentNode.lastChild` 获取元素的最后一个子节点

      `parentNode.lastElementChild` 获取元素的最后一个子元素节点（IE9以上支持）

      实际开发解决兼容性问题同时获取第一个/最后一个子元素节点：

      ```js
      // 第一个
      console.log(ol.children[0]);
      // 最后一个
      console.log(ol.children[ol.children.length - 1]);
      ```

      案例：新浪下拉菜单
      
      ```html
      <!DOCTYPE html>
      <html lang="en">
      
      <head>
          <meta charset="UTF-8">
          <meta http-equiv="X-UA-Compatible" content="IE=edge">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>新浪下拉菜单</title>
          <style>
              * {
                  margin: 0;
                  padding: 0;
              }
      
              ul {
                  list-style: none;
              }
      
              a {
                  text-decoration: none;
                  font-size: 14px;
              }
      
              .nav {
                  margin: 100px;
              }
      
              .nav>li {
                  float: left;
                  width: 80px;
                  height: 41px;
                  line-height: 41px;
                  text-align: center;
              }
      
              .nav li a {
                  display: block;
                  width: 100%;
                  height: 100%;
                  color: #333;
              }
      
              .nav>li>a:hover {
                  background-color: #eee;
              }
      
              .nav li ul {
                  display: none;
                  font-size: 14px;
                  border-left: 1px solid #FECC5B;
                  border-right: 1px solid #FECC5B;
              }
      
              .nav ul li {
                  border-bottom: 1px solid #FECC5B;
              }
          </style>
      </head>
      
      <body>
          <ul class="nav">
              <li>
                  <a href="#">微博</a>
                  <ul>
                      <li>私信</li>
                      <li>评论</li>
                      <li>@我</li>
                  </ul>
              </li>
              <li>
                  <a href="#">微博</a>
                  <ul>
                      <li>私信</li>
                      <li>评论</li>
                      <li>@我</li>
                  </ul>
              </li>
              <li>
                  <a href="#">微博</a>
                  <ul>
                      <li>私信</li>
                      <li>评论</li>
                      <li>@我</li>
                  </ul>
              </li>
              <li>
                  <a href="#">微博</a>
                  <ul>
                      <li>私信</li>
                      <li>评论</li>
                      <li>@我</li>
                  </ul>
              </li>
          </ul>
          <script>
              var nav = document.querySelector('.nav');
              var lis = nav.children;
              for (var i = 0; i < lis.length; i++) {
                  lis[i].onmouseover = function () {
                      // 让其第二个孩子（ul）显示
                      this.children[1].style.display = 'block';
                  }
                  lis[i].onmouseout = function () {
                      this.children[1].style.display = 'none';
                  }
              }
          </script>
      </body>
      
      </html>
      ```
      
   3. 兄弟节点

       | 代码                    | 说明                                                         |
       | ----------------------- | ------------------------------------------------------------ |
       | node.nextSibling        | 返回当前元素的下一个兄弟节点，找不到则返回null。同样，也是包含所有节点 |
       | node.previousSibling    | 返回当前元素的上一个兄弟节点，找不到则返回null。同样，也是包含所有节点 |
       | node.nextElementSibling | 返回当前元素的下一个兄弟元素节点，找不到则返回null           |
       | node.previousSibling    | 返回当前元素的上一个兄弟元素节点，找不到则返回null           |

       查找兄弟元素节点同时解决兼容性问题：封装兼容性函数

       ```js
       function getNextElementSibling(element) {
       	var el = element;
       	while (el = el.nextSibling) {
       		if (el.nodeType === 1) {
       			return el;
       		}
       	}
       	return null;
       }
       ```

   4. 创建节点

       `document.createElement('tagName')`

       document.createElement()方法创建由tagName指定HTML元素。因为这些元素原先不存在，是根据我们的需求动态生成的，因此我们也称其为**动态创建元素节点**。

   5. 添加节点

       `node.appendChild(child)`

       node.appendChild()方法将一个节点**添加到指定父节点的子节点列表末尾**。类似于CSS里面的after伪元素。

       ```js
       // 创建节点
       var li = document.createElement('li');
       // 父节点
       var ul = document.querySelector('ul');
       // 添加节点
       ul.appendChild(li);
       ```

       `node.insertBefore(child, 指定元素)`

       node.insertBefore()方法将一个节点**添加到父节点的指定子节点前面**。类似于CSS中before伪元素。

       ```html
       <body>
           <ul>
               <!-- 将li插入到此处 -->
               <li>123</li>
               <li>456</li>
           </ul>
           <script>
       		// 创建节点
       		var li = document.createElement('li');
       		var ul = document.createElement('ul');
               // 添加节点
               ul.insertBefore(li, ul.children[0]);
       	</script>
       </body>
       
       ```

       案例：简单版发布留言

       ```html
       <!DOCTYPE html>
       <html lang="en">
       
       <head>
           <meta charset="UTF-8">
           <meta http-equiv="X-UA-Compatible" content="IE=edge">
           <meta name="viewport" content="width=device-width, initial-scale=1.0">
           <title>简单版发布留言</title>
           <style>
               * {
                   margin: 0;
                   padding: 0;
               }
       
               ul {
                   list-style: none;
               }
           </style>
       </head>
       
       <body>
           <textarea name="" id="" cols="30" rows="10"></textarea>
           <button>发布</button>
           <ul>
       
           </ul>
           <script>
               var btn = document.querySelector('button');
               var text = document.querySelector('textarea');
               var ul = document.querySelector('ul');
               btn.onclick = function () {
                   if (text.value == '') {
                       alert('您没有输入内容');
                       return false;
                   } else {
                       var li = document.createElement('li');
                       ul.appendChild(li);
                       var msg = text.value;
                       li.innerHTML = msg;
                       text.value = '';
                   }
       
               }
           </script>
       </body>
       
       </html>
       ```

       file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo20/demo20_7.html

   6. 删除节点

       `node.removeChild(child)`

       node.removeChild() 方法从DOM中删除一个子节点，返回删除的节点。

       ```html
       <!DOCTYPE html>
       <html lang="en">
       
       <head>
           <meta charset="UTF-8">
           <meta http-equiv="X-UA-Compatible" content="IE=edge">
           <meta name="viewport" content="width=device-width, initial-scale=1.0">
           <title>依次删除节点</title>
       </head>
       
       <body>
           <button>
               删除
           </button>
           <ul>
               <li>张三</li>
               <li>李四</li>
               <li>王五</li>
           </ul>
           <script>
               var btn = document.querySelector('button');
               var ul = document.querySelector('ul');
               btn.onclick = function () {
                   if (ul.children.length) {
                       ul.removeChild(ul.children[0]);
                       if (ul.children.length == 0) {
                           // 禁用按钮
                           this.disabled = true;
                       }
                   }
               }
           </script>
       </body>
       
       </html>
       ```

       案例：删除留言

       ```html
       <!DOCTYPE html>
       <html lang="en">
       
       <head>
           <meta charset="UTF-8">
           <meta http-equiv="X-UA-Compatible" content="IE=edge">
           <meta name="viewport" content="width=device-width, initial-scale=1.0">
           <title>删除留言案例</title>
           <style>
               * {
                   margin: 0;
                   padding: 0;
               }
       
               ul {
                   list-style: none;
               }
       
               li {
                   width: 400px;
                   background-color: pink;
                   border: 1px dotted #ccc;
               }
       
               li a {
                   float: right;
                   font-size: 14px;
               }
           </style>
       </head>
       
       <body>
           <textarea name="" id="" cols="30" rows="10"></textarea>
           <button>发布</button>
           <ul>
       
           </ul>
           <script>
               var btn = document.querySelector('button');
               var text = document.querySelector('textarea');
               var ul = document.querySelector('ul');
               btn.onclick = function () {
                   if (text.value == '') {
                       alert('您没有输入内容');
                       return false;
                   } else {
                       var li = document.createElement('li');
                       ul.appendChild(li);
                       // javascript:;阻止链接跳转
                       var msg = text.value + "<a href='javascript:;'>删除</a>";
                       li.innerHTML = msg;
                       text.value = '';
                       var deles = document.querySelectorAll('a');
                       for (var i = 0; i < deles.length; i++) {
                           deles[i].onclick = function () {
                               ul.removeChild(this.parentNode);
                           }
                       }
                   }
               }
           </script>
       </body>
       
       </html>
       ```

   7. 复制节点

       `node.cloneNode()`

       node.cloneNode()方法**返回调用该方法的节点的一个副本**。也称为克隆节点/拷贝节点。

       ```html
       <ul>
           <li>1</li>
           <li>2</li>
           <li>3</li>
       </ul>
       <script>
       	var ul = document.querySelector('ul');
           // 复制节点 只复制节点 不复制内容
           var li = ul.children[0].cloneNode();
           // 添加节点
           ul.appendChild(li);
       </script>
       ```

       - 若**括号内的参数为空或false**，则是**浅拷贝**，只复制节点本身，而不复制内容；
       - 若**括号内参数为true**，则是**深拷贝**，复制节点本身的同时复制内容。

       案例：动态生成表格

       ```html
       <!DOCTYPE html>
       <html lang="en">
       
       <head>
           <meta charset="UTF-8">
           <meta http-equiv="X-UA-Compatible" content="IE=edge">
           <meta name="viewport" content="width=device-width, initial-scale=1.0">
           <title>动态生成表格</title>
           <style>
               table {
                   width: 500px;
                   margin: 100px auto;
                   text-align: center;
                   /* 为表格设置合并边框模型 */
                   border-collapse: collapse;
               }
       
               th,
               td {
                   border: 1px solid #333;
               }
       
               thead tr {
                   height: 40px;
                   background-color: #ccc;
               }
           </style>
       </head>
       
       <body>
           <table>
               <thead>
                   <tr>
                       <th>姓名</th>
                       <th>科目</th>
                       <th>成绩</th>
                       <th>操作</th>
                   </tr>
               </thead>
               <tbody>
               </tbody>
           </table>
           <script>
               // 1. 准备学生信息
               var stu = [{
                   name: '张三',
                   subject: 'JavaScript',
                   score: 100
               }, {
                   name: '李四',
                   subject: 'JavaScript',
                   score: 98
               }, {
                   name: '王五',
                   subject: 'JavaScript',
                   score: 99
               }, {
                   name: '赵六',
                   subject: 'JavaScript',
                   score: 88
               }, {
                   name: '陈七',
                   subject: 'JavaScript',
                   score: 0
               }];
               var tbody = document.querySelector('tbody');
               for (var i = 0; i < stu.length; i++) {
                   // 创建行
                   var tr = document.createElement('tr');
                   tbody.appendChild(tr);
                   // 根据对象内容创建单元格
                   for (var k in stu[i]) {
                       var td = document.createElement('td');
                       td.innerHTML = stu[i][k];
                       tr.appendChild(td);
                   }
                   // 创建最后的删除单元格
                   var del = document.createElement('td');
                   del.innerHTML = "<a href='javascript:;'>删除</a>";
                   tr.appendChild(del);
               }
               // 删除操作
               var as = document.querySelectorAll('a');
               for (var i = 0; i < as.length; i++) {
                   as[i].onclick = function () {
                       // 要删除的tr是a的爸爸的爸爸
                       tbody.removeChild(this.parentNode.parentNode);
                   }
               }
           </script>
       </body>
       
       </html>
       ```

       file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo20/demo20_10.html
       
   8. 三种动态创建元素的区别
   
       | 方法                     | 区别                                                         |
       | ------------------------ | ------------------------------------------------------------ |
       | document.write()         | 直接将内容写入页面的内容流，但是文档流执行完毕后，它会导致**页面全部重绘** |
       | element.innerHTML        | 将内容写入某个DOM节点，不会导致页面全部重绘。创建多个元素时效率最高（不采取直接拼接字符串的形式，而是采取数组形式拼接），结构稍微复杂 |
       | document.createElement() | 创建多个元素的效率稍微低一些，但是结构更清晰                 |
   
       ```js
       var inner = document.querySelector('.inner');
       /*
       for (var i = 0; i <= 100; i++) {
       	inner.innerHTML += '<a href="#"></a>';	// 重复的字符拼接影响效率
       }*/
       var array = [];
       for (var i = 0; i < 100; i++) {
           array.push('<a href="#"></a>');
       }
       inner.innerHTML = array.join('');	// 比createElement效率更高
       
       var create = document.querySelector('.create');
       for (var i = 0; i <= 100; i++) {
       	var a = document.createElement('a');
       	create.appendChild(a);
       }
       ```

## 六、DOM重点核心（总结）

关于DOM操作，我们主要针对元素的创建、增、删、改、查、属性操作、事件操作。

### 1.创建

1. `document.write`
2. `innerHTML`
3. `createElement`

### 2.增

1. `appendChild`
2. `insertBefore`

### 3.删

1. `removeChild`

### 4.改

1. 修改元素属性：src、href、title等；
2. 修改普通元素内容：**innerHTML**、**innerText**；
3. 修改表单元素：value、type、disabled等；
4. 修改元素样式：style、className

### 5.查

1. DOM提供的API方法：getElementById、getElementsByTagName （古老，不推荐）；
2. H5提供的API方法：**querySelector**、**querySelectorAll**（推荐）；
3. 利用节点操作获取元素：父（**parentNode**）、子（**children**）、兄弟（previousElementSibling、nextElementSibling）（推荐）

### 6.属性操作（主要针对自定义属性）

1. **setAttribute**：设置属性值
2. **getAttribute**：获取属性值
3. **removeAttribute**：移除属性

### 7.事件操作

| 鼠标事件    | 触发条件     |
| ----------- | ------------ |
| onclick     | 鼠标左键点击 |
| onmouseover | 鼠标经过     |
| onmouseout  | 鼠标离开     |
| onfocus     | 获得鼠标焦点 |
| onblur      | 失去鼠标焦点 |
| onmousemove | 鼠标移动     |
| onmouseup   | 鼠标弹起     |
| onmousedown | 鼠标按下     |

# 事件高级

## 一、注册事件（绑定事件）

1. 注册事件概述

   给元素添加事件，就称为**注册事件**或**绑定事件**。

2. 注册事件方式

   1. 传统方式

      利用on开头的事件，如onclick：

      ```html
      <button onclick = 'alert('hi~')'></button>
      ```

      ```js
      btn.onclick = function() {
      }
      ```

      注册事件具有**唯一性**（同一元素同一事件只能设置一个处理函数，后注册的处理函数将会覆盖前面注册的处理函数）。

   2. 监听注册

      W3C标准推荐方式。

      **addEventListener()** 方法（在IE9之前的IE不支持该方法，可用attachEvent()代替）。

      特点：**同一个元素同一个事件可以注册多个监听器**，按注册顺序依次进行。

      1. **addEventListener()**

         ```
         eventTarget.addEventListener(type, listener[, useCapture]);
         ```

         eventTarget.addEventListener() 方法将制定的监听器注册到eventTarget（目标对象）上，当该对象触发指定的事件时，就会执行事件处理函数。

         - type：事件类型字符串，比如**click、mouseover**；
         - listener：事件处理函数，事件发生时，会调用该监听函数；
         - useCapture： 可选参数，是一个布尔值，默认为false。

         ```js
         var btns = document.querySelectorAll('button');
         // 1. 传统方式注册事件
         btns[0].onclick = function() {
         	alert('hi');	// 不弹出
         }
         btns[0].onclick = function() {
         	alert('how are you');	// 弹出
         }
         
         // 2. 事件监听注册事件
         btns[1].addEventListener('click', function() {
         	alert('22');	// 弹出
         })
         btns[1].addEventListener('click', function() {
         	alert('33');	// 弹出
         })
         // 同一个对象可以添加多个监听器（事件处理程序）
         ```

      2. attachEvent()

         ```js
         eventTarget.attachEvent(eventNameWithOn, callback);
         ```

         eventTarget.attachEvent() 方法将制定的监听器注册到eventTarget（目标对象）上，当该对象触发指定的事件时，指定的回调函数就会被执行。

         - eventNameWithOn：事件类型字符串，比如**onclick、onmouseover**；
         - callback：事件处理函数，当目标触发事件回调函数被调用

         注意：

         - IE独有；
         - 仅有IE9之前的版本支持。

      3. 注册事件兼容性解决方案

         ```js
         function addEventListener(element, eventName, fn) {
         	// 判断当前浏览器是否支持addEventListener方法
         	if (element.addEventListener) {
         		element.addEventListener(eventName, fn);
         	} else if (element.attachEvent) {
         		element.attachEvent('on' + eventName, fn);
         	} else {
         		// 相当于 element.onclick = fn;
         		element['on' + eventName] = fn;
         	}
         }
         ```

## 二、删除事件（解绑事件）

1. 传统注册方式

   ```js
   eventTarget.onclick = null;
   ```

2. 监听注册方式

   ```js
   eventTarget.removeEventListener(type, listener[, useCapture]);
   ```

   ```js
   var divs = document.querySelectorAll('div');
   divs[0].onclick = function() {
   	alert(11);
   	// 1. 传统方式删除事件
   	divs[0].onclick = null;
   }
   divs[1].addEventListener('click', fn);
   function fn() {
   	alert(22);
       // 2.监听注册方式删除事件
       divs[1].removeEventListener('click', fn);
   }
   divs[2].attachEvent('onclick', fn1);
   function fn1() {
       alert(33);
       divs[3].detachEvent('onclick', fn1);
   }
   ```

   删除事件兼容性解决方案：

   ```js
   function removeEventListener(element, eventName, fn) {
   	// 判断当前浏览器是否支持 removeEventListener 方法
   	if (element.removeEventListener) {
   		element.removeEventListener(eventName, fn);
   	} else if (element.detachEvent) {
   		element.detachEvent('on' + eventName, fn);
   	} else {
   		element['on' + eventName] = null;
   	}
   }
   ```

## 三、DOM事件流

**事件流**描述的是从页面中接收事件的顺序。

事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即**DOM事件流**。

![image-20211209155409195](https://gitee.com/v876774538/my-img/raw/master/image-20211209155409195.png)

DOM事件流分为3个阶段：

1. 捕获阶段
2. 当前目标阶段
3. 冒泡阶段

注：

- **事件冒泡**：由IE最早提出，指事件开始时由具体的元素接收，然后逐级向上传播到DOM最顶层节点的过程。（**从下往上**）
- **事件捕获**：网景最早提出，由DOM最顶层节点开始，然后逐级向下传播到具体元素接收的过程。（**从上往下**）

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM事件流</title>
    <style>
        .father {
            position: relative;
            width: 300px;
            height: 300px;
            margin: 100px auto;
            background-color: pink;
        }

        .son {
            position: absolute;
            left: 50%;
            top: 50%;
            margin-left: -50px;
            margin-top: -50px;
            width: 100px;
            height: 100px;
            line-height: 100px;
            text-align: center;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son">son</div>
    </div>
    <script>
        // 捕获阶段
        // 点击后先弹出father 再弹出son
        var son = document.querySelector('.son');
        son.addEventListener('click', function () {
            alert('son');
        }, true);	// 默认第三个参数是false
        var father = document.querySelector('.father');
        father.addEventListener('click', function () {
            alert('father');
        }, true);
        // 冒泡阶段
        // 点击后先弹出son 再弹出father
        var son = document.querySelector('.son');
        son.addEventListener('click', function () {
            alert('son');
        }, false);
        var father = document.querySelector('.father');
        father.addEventListener('click', function () {
            alert('father');
        }, false);
    </script>
</body>

</html>
```

注意：

- 在实际开发中我们很少使用事件捕获，更关注事件冒泡；
- 有些事件是没有冒泡的，比如onblur、onfocus、onmouseenter、onmouseleave。

## 四、事件对象

1.  概述

   ```js
   eventTarget.onclick = function(event) {};
   eventTarget.addEventListener('click', function(event) {});
   // event就是事件对象 我们还喜欢写成e或者evt
   ```

   **event对象代表事件的状态**，比如键盘按键的状态、鼠标的位置、鼠标按钮的状态等。

   事件发生后，**跟事件相关的一系列信息数据的集合都放到这个对象里面**，这个对象就是事件对象event，它有很多属性和方法。

2. 使用

   ```js
   // 这个event是形参 由系统帮我们设定为事件对象 不需要传递实参过去
   // 当我们注册事件时 event对象就被系统自动创建 并依次传递给事件监听器（事件处理函数）
   var div = document.querySelector('div');
   div.onclick = function(e) {
   	e = e || window.event;
   	// 解决兼容性问题
   	// ie678通过window.event查看
   	console.log(e);
   }
   ```

3. 常见的属性和方法

   | 事件对象属性方法        | 说明                                                       |
   | ----------------------- | ---------------------------------------------------------- |
   | **e.target**            | 返回触发事件的对象（标准）                                 |
   | e.srcElement            | 返回触发事件的对象（非标准 IE6-8使用）                     |
   | **e.type**              | 返回事件的类型 比如click mouseover                         |
   | **e.cancelBubble**      | 阻止冒泡（非标准 IE6-8使用）                               |
   | e.returnValue           | 阻止默认事件（默认行为 非标准 IE6-8使用 比如不让链接跳转） |
   | **e.preventDefault()**  | 阻止默认事件（默认行为 标准 比如不让链接跳转）             |
   | **e.stopPropagation()** | 阻止冒泡（标准）                                           |

   1. 返回触发事件对象

      ```js
      var div = document.querySelector('div');
      div.addEventListener('click', function(e) {
      	console.log(e.target);	// 返回触发事件的对象
      	console.log(this);	// 返回绑定事件的对象
      });
      
      var ul = document.quertySelector('ul');
      ul.addEventListener('click', function(e) {
      	console.log(this);	// ul
      	console.log(e.target);	// li
      })
      ```

      兼容性处理：

      ```js
      div.onclick = function(e) {
      	e = e || window.event;
      	var target = e.target || e.srcElement;
      	console.log(target);
      }
      ```

   2. 阻止默认行为：

      ```js
      var a = document.querySelector('a');
      // 监听方式
      a.addEventListener('click', function(e) {
          e.preventDefault();	// DOM标准写法
      })
      
      // 传统方式
      a.onclick = function(e) {
      	// 普通浏览器
      	e.preventDefault();
      	// 低版本浏览器
      	e.returnValue;
      	// return false也能阻止默认行为 且没有兼容性问题
      	return false;	// 只限于传统的注册方式
      }
      ```

## 五、阻止事件冒泡

1. 标准写法：事件对象**stopPropagation()**方法

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>DOM事件流</title>
       <style>
           .father {
               position: relative;
               width: 300px;
               height: 300px;
               margin: 100px auto;
               background-color: pink;
           }
   
           .son {
               position: absolute;
               left: 50%;
               top: 50%;
               margin-left: -50px;
               margin-top: -50px;
               width: 100px;
               height: 100px;
               line-height: 100px;
               text-align: center;
               background-color: purple;
           }
       </style>
   </head>
   
   <body>
       <div class="father">
           <div class="son">son</div>
       </div>
       <script>
           // 冒泡阶段
           // 点击后先弹出son 再弹出father
           var son = document.querySelector('.son');
           son.addEventListener('click', function (e) {
               alert('son');
               e.stopPropagation();	// 阻止冒泡
           }, false);
           var father = document.querySelector('.father');
           father.addEventListener('click', function () {
               alert('father');
           }, false);
       </script>
   </body>
   
   </html>
   ```

2. 非标准写法：**cancelBubble**属性阻止冒泡，非标准，IE6-8使用

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>DOM事件流</title>
       <style>
           .father {
               position: relative;
               width: 300px;
               height: 300px;
               margin: 100px auto;
               background-color: pink;
           }
   
           .son {
               position: absolute;
               left: 50%;
               top: 50%;
               margin-left: -50px;
               margin-top: -50px;
               width: 100px;
               height: 100px;
               line-height: 100px;
               text-align: center;
               background-color: purple;
           }
       </style>
   </head>
   
   <body>
       <div class="father">
           <div class="son">son</div>
       </div>
       <script>
           // 冒泡阶段
           // 点击后先弹出son 再弹出father
           var son = document.querySelector('.son');
           son.addEventListener('click', function (e) {
               alert('son');
               e.cancelBubble = true;	// 阻止冒泡
           }, false);
           var father = document.querySelector('.father');
           father.addEventListener('click', function () {
               alert('father');
           }, false);
       </script>
   </body>
   
   </html>
   ```

## 六、事件委托（代理、委派）

1. 概述

   事件委托也称为事件代理，在jQuery中称为事件委派。

2. 原理

   不是为每个子节点单独设置事件监听器，而是**事件监听器设置在其父节点上**，然后利用冒泡原理影响每个子节点。

   如：给ul注册点击事件，然后利用事件对象的target来找到当前点击的li，由于点击li，事件会冒泡到ul上，ul有注册事件，就会触发事件监听器。

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>事件委托</title>
   </head>
   
   <body>
       <ul>
           <li>我是小li</li>
           <li>我是小li</li>
           <li>我是小li</li>
           <li>我是小li</li>
           <li>我是小li</li>
       </ul>
       <script>
           var ul = document.querySelector('ul');
           ul.addEventListener('click', function (e) {
               // alert('这是弹框！');
               // 清除其他小li的背景颜色
               for (var i = 0; i < ul.children.length; i++) {
                   this.children[i].style.backgroundColor = '';
               }
               // 给点击的小li修改背景颜色
               e.target.style.backgroundColor = 'pink';
           })
       </script>
   </body>
   
   </html>
   ```

3. 作用

   只操作了一次DOM，提高了程序的性能。

## 七、常用的鼠标事件

1. 常用的鼠标事件

   | 鼠标事件    | 触发事件         |
   | ----------- | ---------------- |
   | onclick     | 鼠标点击左键触发 |
   | onmouseover | 鼠标经过触发     |
   | onmouseout  | 鼠标离开触发     |
   | onfocus     | 获得鼠标焦点触发 |
   | onblur      | 失去鼠标焦点触发 |
   | onmousemove | 鼠标移动触发     |
   | onmouseup   | 鼠标弹起触发     |
   | onmousedown | 鼠标按下触发     |

2. 禁止鼠标右键菜单

   contextmenu主要控制何时显示上下文菜单，主要用于程序员取消默认的上下文菜单。

   ```js
   document.addEventListener('contextmenu', function(e) {
   	e.preventDefault();	// 阻止默认事件
   })
   ```

3. 禁止鼠标选中

   selectstart控制选中。

   ```js
   document.addEventListener('selectstart', function(e) {
   	e.preventDefault();	// 阻止默认事件
   })
   ```

4. **mouseenter** 和 **mouseover**的区别

   - 当鼠标移动到元素上时就会触发mouseenter事件。
   - mouseenter事件与mouseover类似，但**mouseover在鼠标经过自身盒子时会触发，经过子盒子还会触发**，**mouseenter指挥在经过自身盒子时触发**。（mouseenter不会冒泡）。
   - **mouseenter**搭配**mouseleave**，同样不会冒泡。

5. **鼠标事件对象 MouseEvent**

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>鼠标事件对象</title>
   </head>
   
   <body>
       <script>
           document.addEventListener('click', function (event) {
               console.log(event);
           })
       </script>
   </body>
   
   </html>
   ```

   ![image-20211210170413321](https://gitee.com/v876774538/my-img/raw/master/image-20211210170413321.png)

   | 鼠标事件对象属性 | 说明                                   |
   | ---------------- | -------------------------------------- |
   | clientX          | 返回鼠标相对于浏览器窗口可视区的X坐标  |
   | clientY          | 返回鼠标相对于浏览器窗口可视区的Y坐标  |
   | **pageX**        | 返回鼠标相对于文档页面的X坐标 IE9+支持 |
   | **pageY**        | 返回鼠标相对于文档页面的Y坐标 IE9+支持 |
   | screenX          | 返回鼠标相对于电脑屏幕的X坐标          |
   | screenY          | 返回鼠标相对于电脑屏幕的Y坐标          |

   案例：跟随鼠标的天使

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>跟随鼠标的天使</title>
       <style>
           /* body {
               position: relative;
           } */
   
           img {
               position: absolute;
           }
       </style>
   </head>
   
   <body>
       <img src="./images/angel.gif" alt="">
       <script>
           var angle = document.querySelector('img');
           document.addEventListener('mousemove', function (e) {
               // 最新鼠标坐标
               var x = e.pageX;
               var y = e.pageY;
   
               // 不要忘记单位！
               angle.style.top = y - 40 + 'px';
               angle.style.left = x - 50 + 'px';
           })
       </script>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo20/demo20_13.html

## 八、常用的键盘事件

1. 常用键盘事件

   | 键盘事件   | 触发条件                                                     |
   | ---------- | ------------------------------------------------------------ |
   | onkeyup    | 某个键盘按键被松开时触发                                     |
   | onkeydown  | 某个键盘按键被按下时触发                                     |
   | onkeypress | 某个键盘按键被按下时触发（但不识别功能键，如ctrl、shift、箭头等） |

   注：三个事件的执行顺序：**keydown --- keypress --- keyup**

2. **键盘事件对象 KeyboardEvent**

   | 键盘事件对象属性 | 说明                    |
   | ---------------- | ----------------------- |
   | keyCode（淘汰）  | 返回该键的**ASCII码值** |
   | **key**          | **返回用户按下的键**    |

   ![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi0.hdslb.com%2Fbfs%2Farticle%2Fd39a7c1571da459cf92059feeb39e0619e3934ec.jpg&refer=http%3A%2F%2Fi0.hdslb.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1641721472&t=993ea332eb95fd38cb618a033b5b2f72)

   注：

   - **keyup和keydown事件不区分大小写（KeyCode）**，如A和a得到的都是65。

   案例：模拟京东按键输入内容

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>模拟京东按键输入内容</title>
   </head>
   
   <body>
       <input type="text">
       <!-- 检测用户是否按下了S键，若按下S键，将光标定位到搜索框内 -->
       <script>
           var search = document.querySelector('input');
           // 使用keydown了话会导致S输入到搜索框内
           document.addEventListener('keyup', function (e) {
               console.log(e.key);
               var key = e.key;
               // 用户按下S键
               if (key == 's' || key == 'S') {
                   // 将光标定位到搜索框内
                   search.focus();
               }
           })
       </script>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo20/demo20_14.html

   案例：模拟京东快递单号查询

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>模拟京东快递单号查询</title>
       <style>
           * {
               margin: 0;
               padding: 0;
           }
   
           .search {
               position: relative;
               width: 178px;
               margin: 100px auto;
           }
   
           input {
               outline: none;
           }
   
           .con {
               position: absolute;
               top: -40px;
               width: 171px;
               border: 1px solid #ccc;
               padding: 5px 0;
               box-shadow: 0 2px 4px rgba(0, 0, 0, .2);
               font-size: 18px;
               color: #333;
               display: none;
           }
   
           .con::before {
               content: '';
               width: 0;
               height: 0;
               position: absolute;
               top: 30px;
               left: 26px;
               border: 8px solid #000;
               border-style: solid dashed dashed;
               border-color: #fff transparent transparent;
           }
       </style>
   </head>
   
   <body>
       <div class="search">
           <div class="con"></div>
           <input type="text" placeholder="请输入您的快递单号" class="orderID">
       </div>
       <script>
           var con = document.querySelector('.con');
           var id = document.querySelector('.orderID');
           id.addEventListener('keyup', function (e) {
               if (this.value == '') {
                   // 快递单号里面的内容为空，则隐藏大字号盒子
                   con.style.display = 'none';
               } else {
                   // 快递单号输入内容时，上面的大字号盒子显示
                   con.style.display = 'block';
                   // 快递单号里面的值获取过来赋值给con盒子
                   con.innerText = this.value;
               }
           })
           // 失去焦点时隐藏con盒子
           id.addEventListener('blur', function (e) {
               con.style.display = 'none';
           })
           // 获得焦点时显示con盒子
           id.addEventListener('focus', function (e) {
               // 要求输入框内容不为空
               if (this.value !== '') {
                   con.style.display = 'block';
               }
           })
       </script>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo20/demo20_15.html

# BOM

## 一、BOM概述

**BOM**（Browser Object Model）即**浏览器对象模型**，它提供了独立于内容且与浏览器窗口进行交互的对象，其核心对象是Window。

**BOM由一系列相关的对象构成**，并且每个对象都提供了很多方法与属性。

BOM缺乏标准，JavaScript语法的标准化组织是ECMA，DOM的标准化组织是W3C，BOM最初是Netscape浏览器标准的一部分，因此兼容性较差。

### 1.DOM与BOM的区别

| DOM                      | BOM                                        |
| ------------------------ | ------------------------------------------ |
| **文档**对象模型         | **浏览器**对象模型                         |
| 把文档当做对象来看待     | 把浏览器当做对象来看待                     |
| 顶级对象是**document**   | 顶级对象是**window**                       |
| 主要学习的是操作页面元素 | 主要学习的是浏览器窗口交互的一些对象       |
| W3C标准规范              | 浏览器厂商在各自浏览器上定义的，兼容性较差 |

### 2.BOM的构成

![image-20211210202428147](https://gitee.com/v876774538/my-img/raw/master/image-20211210202428147.png)

window对象是浏览器的顶级对象，它具有双重角色：

1. 它是**JS访问浏览器窗口的一个接口**；

2. 它是一个**全局对象**。定义在全局作用域中的变量、函数都会变成window对象的属性和方法。在调用时可以省略window，像alert()、prompt()等实际上都是window对象方法。

   ```js
   var num = 10;
   console.log(num);
   console.log(window.num);	// 实际上的完整写法
   
   function fn() {
       console.log(11);
   }
   fn();
   window.fn();	// 实际上的完整写法
   ```

   注意：window下的一个特殊属性 **window.name**（声明变量尽量避免name）。

## 二、Window对象的常见事件

### 1.窗口加载事件

```js
window.onload = function() {}
// 或者
window.addEventListener('load', function() {})
```

**window.onload**为**窗口（页面）加载事件**。当**文档内容完全加载**（包括图像、脚本文件、CSS文件等）时触发该事件。

注：

- 有了window.onload就可以把JS代码写到页面元素的上方。因为onload是等页面内容全部加载完毕，才去执行处理函数；
- window.onload传统注册事件方式只能写一次，如果存在多个，以最后一个window.onload为准；
- addEventListener没有限制。

```js
document.addEventListener('DOMContentLoaded', function() {})
```

**DOMContentLoaded**事件触发时，**DOM加载完成时触发**，不包括样式表、图片、flash等。IE9以上支持。

### 2.调整窗口大小事件

```js
window.onresize = function() {}
// 或者
window.addEventListener('resize', function(){})
```

**window.onresize**是**调整窗口大小加载事件**。

注：

- 只要窗口大小发生像素变化，就会触发该事件；
- 我们经常利用这个事件完成**响应式布局**（**window.innerWidth** 获得**当前窗口的宽度**）。

## 三、定时器

### 1.setTimeout()

```js
window.setTimeout(调用函数名, [延迟的毫秒数, 参数1, 参数2, ...]);
```

setTimeout()方法用于设置一个定时器，该定时器**在定时到期后执行函数**。

注：

- window在书写时可省略；

- 延时时间的单位是毫秒，该参数可省略（默认为0，立刻执行）；

- 调用函数可以**直接写函数、函数名**或采用字符串'函数名()'三种形式；

- 页面中可能有很多定时器，我们可以给定时器加标识符（名字）。

  ```js
  function callback() {
      console.log('boom');
  }
  var timer1 = setTimeout(callback, 3000);
  var timer2 = setTimeout(callback, 5000);
  ```

setTimeout()这个调用函数我们也成为**回调函数callback**。

普通函数是按照代码顺序直接调用的，而这个函数，需要等待时间，再去调用函数，因此成为回调函数。

曾经学习的`element.onclick = fuction(){}`或`element.addEventListener('click', fn);`里面的函数也属于回调函数。

#### 1.1 案例：5s后自动关闭广告

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>5s后自动关闭广告</title>
</head>

<body>
    <img src="./images/ad.jpg" alt="" class="ad">
    <script>
        var ad = document.querySelector('.ad');
        var adTimer = setTimeout(function () {
            ad.style.display = 'none';
        }, 5000);
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo21/demo21_1.html

#### 1.2  clearTimeout()

```js
window.clearTimeout(timeoutID)
```

clearTimeout()方法用于**取消调用setTimeout()创建的定时器**（**停止定时器**）。

注：

- window在书写时可省略；
- timeoutID即为定时器设置的标识符。

### 2.setInterval()

```js
window.setInterval(回调函数名, [间隔的秒数, 参数1, 参数2, ...]);
```

setInterval()方法**重复调用一个函数**，**每隔这个时间**，就去**调用一次回调函数**。

注：

- window在书写时可省略；
- 延时时间的单位是毫秒，该参数可省略（默认为0，立刻执行）；
- 调用函数可以**直接写函数、函数名**或采用字符串'函数名()'三种形式；
- 页面中可能有很多定时器，我们可以给定时器加标识符（名字）。

#### 2.1 案例：倒计时效果

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>倒计时效果</title>
    <style>
        .countDown {
            width: 200px;
            margin: 200px auto;
        }

        .hour,
        .minute,
        .second {
            display: inline-block;
            width: 40px;
            height: 40px;
            background-color: #333;
            font-size: 20px;
            color: #fff;
            text-align: center;
            line-height: 40px;
        }
    </style>
</head>

<body>
    <div class="countDown">
        <span class="hour">1</span>
        <span class="minute">2</span>
        <span class="second">3</span>
    </div>
    <script>
        var hour = document.querySelector('.hour');
        var minute = document.querySelector('.minute');
        var second = document.querySelector('.second');
        // 先调用一次 防止刷新页面时有空白
        countDown('2021-12-16 00:00:00');

        // 设置定时器
        setInterval(countDown, 1000, '2021-12-16 00:00:00');
        // 倒计时函数
        function countDown(time) {
            var nowTime = +new Date(); // 返回当前时间的总毫秒数
            var inputTime = +new Date(time); // 返回预设时间的总毫秒数
            var times = (inputTime - nowTime) / 1000; //剩余时间总秒数

            var h = parseInt(times / 60 / 60 % 24); // 时
            h = h < 10 ? '0' + h : h;
            hour.innerHTML = h;

            var m = parseInt(times / 60 % 60); // 分
            m = m < 10 ? '0' + m : m;
            minute.innerHTML = m;

            var s = parseInt(times % 60); // 秒
            s = s < 10 ? '0' + s : s;
            second.innerHTML = s;
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo21/%E5%80%92%E8%AE%A1%E6%97%B6%E6%95%88%E6%9E%9C.html

#### 2.2 clearInterval()

```js
window.clearInterval(intervalID);
```

clearInterval()方法用于**取消通过setInterval()建立的定时器**。

注：

- window在书写时可省略；
- timeoutID即为定时器设置的标识符。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>清除setInterval定时器</title>
</head>

<body>
    <button class="start">开始</button>
    <button class="stop">停止</button>
    <script>
        var start = document.querySelector('.start');
        var stop = document.querySelector('.stop');

        // 定义全局变量 定时器timer
        var timer = null;

        // 打印函数
        function printMsg() {
            console.log('hello!');
        }

        start.addEventListener('click', function () {
            timer = setInterval(printMsg, 1000);
        })
        stop.addEventListener('click', function () {
            clearInterval(timer);
        })
    </script>
</body>

</html>
```

#### 2.3 案例：发送短信

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>发送短信</title>
</head>

<body>
    手机号码：
    <input type="text">
    <button>发送</button>
    <script>
        var btn = document.querySelector('button');
        var time = 5;
        btn.addEventListener('click', function () {
            // 禁用按钮
            btn.disabled = true;

            // 设置定时器 修改按钮文字内容
            var timer = setInterval(function () {
                if (time >= 1) {
                    btn.innerHTML = '请在' + time + '秒后再尝试发送';
                    time--;
                } else {
                    // 清除定时器
                    clearInterval(timer);
                    // 复原按钮
                    btn.disabled = false;
                    btn.innerHTML = '发送';
                }

            }, 1000)
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo21/%E5%8F%91%E9%80%81%E7%9F%AD%E4%BF%A1.html

### 3.this指向问题

this的指向在函数定义的时候是无法确定的，只有函数执行时才能确定this究竟指向谁。

一般情况下，this的最终指向是调用它的对象。

1. 全局作用域或普通函数中，this指向全局对象window（定时器里面的this指向window）；

2. 方法调用中，谁调用this就指向谁；

3. 构造函数中this指向构造函数的实例。

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>this指向问题</title>
   </head>
   
   <body>
       <button>点击</button>
       <script>
           // this 指向问题 一般情况下this的最终指向的是那个调用它的对象
           // 1. 全局作用域或者普通函数中this指向全局对象window（ 注意定时器里面的this指向window）
           console.log(this);
   
           function fn() {
               console.log(this);
           }
           window.fn();
           window.setTimeout(function () {
               console.log(this);
           }, 1000);
           // 2. 方法调用中谁调用this指向谁
           var o = {
               sayHi: function () {
                   console.log(this); // this指向的是 o 这个对象
               }
           }
           o.sayHi();
           var btn = document.querySelector('button');
           btn.addEventListener('click', function () {
               console.log(this); // 事件处理函数中的this指向的是btn这个按钮对象
           })
           // 3. 构造函数中this指向构造函数的实例
           function Fun() {
               console.log(this); // this 指向的是Fun的实例对象
           }
           var fun = new Fun();
       </script>
   </body>
   
   </html>
   ```

## 四、JS执行机制

### 1.JS是单线程

JavaScript语言的一大特点就是**单线程**。

这是由JavaScript这门脚本语言诞生的使命所致——处理页面中用户的交互，以及操作DOM。我们对某个DOM元素进行添加和删除操作，应该先进行添加，再进行删除，不能同时进行。

### 2.同步和异步

利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程。于是，JS出现了**同步和异步**——

1. 同步：**前一个任务结束后再执行后一个任务**，程序的执行顺序与任务的排列顺序一致；

2. 异步：某件事情花费时间较长，在做这件事情的同时，还可以去处理其他事情（通俗地举例，烧水的同时去烧菜）。

   ```js
   console.log(1);
   setTimeout(function () {
       console.log(3);
   }, 1000);
   console.log(2);
   // 输出结果： 1 2 3
   ```

### 3.同步任务和异步任务

1. **同步任务**：同步任务都在主线程上执行，形成一个**执行栈**；

2. **异步任务**：JS的异步任务是通过回调函数实现的。一般而言，异步任务有以下三种类型：

   - 普通事件，如click、resize等
   - 资源加载，如load、error等
   - 定时器，包括setInterval、setTimeout等

   异步任务相关回调函数添加到**任务队列**（消息队列）中。

### 4.JS执行机制

1. 先执行**执行栈中的同步任务**；
2. **异步任务放入任务队列**中（不执行）；
3. 一旦执行栈中的**所有同步任务执行完毕**，系统就会按次序**读取任务队列中的异步任务**——被读取的异步任务结束等待状态，进入执行栈，开始执行。

![image-20211212203305235](https://gitee.com/v876774538/my-img/raw/master/image-20211212203305235.png)

主线程不断地重复获得任务、执行任务、再获取任务、再执行任务……所以这种机制被称为**事件循环**（event loop）。

## 五、location对象

### 1.概述

window对象给我们提供了一个**location属性**，用于**获取、设置窗体的URL，或解析URL**。

因为这个属性返回的是一个对象，所以我们也称这个属性为**location对象**。

### 2.URL

**统一资源定位符（Uniform Resourse Locator, URL）**是互联网上标准资源的地址。

互联网上的每个文件都有一个唯一的URL，它包含的信息指出文件的位置以及浏览器应该怎样处理它。

URL一般语法格式：

```
protocol://host[:post]/path/[?query]#fragment
http://www.itcast.cn/index.html?name=andy&age=18#link
```

- protocol：通信协议，常用的有http、ftp、maito等；
- host：主机（域名）；
- port：端口号，可选。省略时使用方案的默认端口，如http的默认端口为80；
- path：路径，由0或多个'/'符号隔开的字符串，一般用来表示主机上的一个目录或文件地址；
- query：参数，以键值对的形式通过&符号分隔开；
- fragment：片段，#后面内容，常用于锚点链接。

### 3.location对象属性

| 属性                | 返回值                |
| ------------------- | --------------------- |
| **location.href**   | **获取或设置整个URL** |
| location.host       | 返回主机（域名）      |
| location.port       | 返回端口号            |
| location.pathname   | 返回路径              |
| **location.search** | **返回参数**          |
| location.hash       | 返回片段              |

#### 3.1 案例：5秒后自动跳转页面

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>5s后跳转页面</title>
</head>

<body>
    <div></div>
    <script>
        var div = document.querySelector('div');
        var time = 5;

        setInterval(function () {
            if (time >= 1) {
                div.innerText = time + 's后跳转页面……';
                time--;
            } else {
                location.href = 'https://www.baidu.com/';
            }
        }, 1000)
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo21/5s%E5%90%8E%E8%B7%B3%E8%BD%AC%E9%A1%B5%E9%9D%A2.html

#### 3.2 案例：获取URL参数

```html
// login.html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>登录</title>
</head>

<body>
    <form action="index.html">
        用户名：
        <input type="text" name="uname">
        <input type="submit" value="登录">
    </form>
    <script>
    </script>
</body>

</html>
```

```html
// index.html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>首页</title>
</head>

<body>
    <div></div>
    <script>
        var div = document.querySelector('div');
        console.log(location.search);
        // 1. 获取参数 利用substr去掉'?'
        var params = location.search.substr(1);
        // 2. 利用=分割键和值 变成字符串数组
        var arr = params.split('=');
        console.log(arr);
        div.innerHTML = '欢迎您，' + arr[1] + '！';
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo21/%E8%8E%B7%E5%8F%96URL%E5%8F%82%E6%95%B0/login.html

### 4.location对象方法

| 方法               | 返回值                                                     |
| ------------------ | ---------------------------------------------------------- |
| location.assign()  | 可用于跳转页面，也称为重定向页面（记录历史，可以后退页面） |
| location.replace() | 替换当前页面（不记录历史，不能后退页面）                   |
| location.reload()  | 重新加载页面（相当于刷新）                                 |

## 六、navigator对象

navigator对象包含**有关浏览器的信息**。

我们最常用的有userAgent，该属性可以返回由客户机发送服务器的user-agent头部的值。

判断用户用什么终端打开页面，实现跳转：

```js
if ((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Androd|Moblie|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|WOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    window.location.href = '';	// 手机
} else {
    window.location.href = '';	// 电脑
}
```

## 七、history对象

history对象用于与**浏览器历史记录**进行交互。

该对象中包含用户在浏览器窗口中访问过的URL。

| 方法      | 作用                                         |
| --------- | -------------------------------------------- |
| back()    | 后退                                         |
| forward() | 前进                                         |
| go(参数)  | 参数为n则前进n个页面，参数为-n则后退-n个页面 |

# PC端网页特效

## 一、元素偏移量offset系列

### 1.概述

offset（偏移量），我们使用offset系列相关属性可以**动态地**得到该元素的位置（偏移）、大小等信息。

- 活的元素距离带有定位父元素的位置；
- 获得元素自身的大小（宽度、高度）。

注意：返回的数值都不带单位。

### 2.常用属性

| 属性                 | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element.offsetParent | 返回作为该元素**带有定位的父级元素**，若父级都没有定位，则返回body |
| element.offsetTop    | 返回元素相对带有定位的父元素上方的偏移                       |
| element.offsetLeft   | 返回元素相对带有定位的父元素左边框的偏移                     |
| element.offsetWidth  | 返回自身包括padding、边框、内容区的宽度，返回数值不带单位    |
| element.offsetHeight | 返回自身包括padding、边框、内容区的高度，返回数值不带单位    |

### 3.offset与style的区别

| offset                                            | style                                           |
| ------------------------------------------------- | ----------------------------------------------- |
| offset可以得到任意样式表中的样式值                | style只能得到行内样式表中的样式值               |
| offset系列活的的**数值是没有单位**的              | style获得的是带**有单位的字符串**               |
| **offsetWidth包含padding+border+width**           | **style.width获得不包含padding和border的值**    |
| offsetWidth等属性是**只读**属性，只能获取不能赋值 | style.width是**可读写**属性，可以获取也可以赋值 |
| **获取元素大小位置，使用offset**                  | **修改元素的值，使用style**                     |

### 4.案例：获取鼠标在盒子内的坐标

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>获取鼠标在盒子内的坐标</title>
    <style>
        .box {
            background-color: pink;
            width: 200px;
            height: 200px;
            margin: 200px auto;
        }
    </style>
</head>

<body>
    <div class="box"></div>
    <script>
        var box = document.querySelector('.box');
        box.addEventListener('mousemove', function (e) {
            // // 鼠标点击在整个页面中的位置
            // console.log(e.pageX);
            // console.log(e.pageY);
            // // 盒子的位置
            // console.log(box.offsetLeft);
            // console.log(box.offsetTop);
            // 鼠标在盒子内的坐标
            var x = e.pageX - this.offsetLeft;
            var y = e.pageY - this.offsetTop;
            this.innerHTML = '(' + x + ', ' + y + ')';
        })
    </script>
</body>

</html>
```

### 5.案例：模态框拖拽

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>可拖动的模态框</title>
    <style>
        ul,
        li,
        ol,
        dl,
        dt,
        dd,
        div,
        p,
        span,
        h1,
        h2,
        h3,
        h4,
        h5,
        h6,
        a {
            padding: 0px;
            margin: 0px;
        }

        a {
            text-decoration: none;
            color: #000;
        }

        .login-header {
            width: 100%;
            height: 30px;
            line-height: 30px;
            text-align: center;
            font-size: 24px;
        }

        .login {
            display: none;
            /* 定位在中间 */
            position: fixed;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            width: 512px;
            height: 280px;
            border: 1px solid #ebebeb;
            background-color: #fff;
            box-shadow: 0px 0px 20px #ddd;
            z-index: 9999;
        }

        .login-title {
            position: relative;
            width: 100%;
            height: 40px;
            line-height: 40px;
            text-align: center;
            margin: 10px 0 0 0;
            font-size: 18px;
            cursor: move;
        }

        .login-title span {
            position: absolute;
            top: -30px;
            right: -20px;
            width: 40px;
            height: 40px;
            font-size: 12px;
            border: 1px solid #ebebeb;
            border-radius: 20px;
            background: #fff;
        }

        .login-input-content {
            margin-top: 20px;
        }

        .login-input {
            overflow: hidden;
            margin: 0px 0px 20px 0px;
        }

        .login-input label {
            float: left;
            width: 90px;
            height: 35px;
            line-height: 35px;
            text-align: right;
            font-size: 14px;
            padding-right: 10px;
        }

        .login-input .list-input {
            float: left;
            width: 350px;
            height: 35px;
            line-height: 35px;
            border: 1px solid #ebebeb;
            text-indent: 5px;
        }

        .login-button {
            width: 50%;
            line-height: 40px;
            text-align: center;
            font-size: 14px;
            margin: 30px auto 0px auto;
            border: 1px solid #ebebeb;
        }

        .login-bg {
            display: none;
            width: 100%;
            height: 100%;
            position: fixed;
            top: 0;
            left: 0;
            background: rgba(0, 0, 0, .3);
        }
    </style>
</head>

<body>
    <div class="login-header"><a id="link" href="javascript:;">点击，弹出登录框</a></div>
    <div id="login" class="login">
        <div id="title" class="login-title">登录会员
            <span><a id="closeBtn" href="javascript:void(0);" class="close-login">关闭</a></span>
        </div>
        <div class="login-input-content">
            <div class="login-input">
                <label>用户名：</label>
                <input type="text" placeholder="请输入用户名" name="info[username]" id="username" class="list-input">
            </div>
            <div class="login-input">
                <label>登录密码：</label>
                <input type="password" placeholder="请输入登录密码" name="info[password]" id="password" class="list-input">
            </div>
        </div>
        <div id="loginBtn" class="login-button"><a href="javascript:void(0);" id="login-button-submit">登录</a></div>
    </div>
    <!-- 遮盖层 -->
    <div id="bg" class="login-bg"></div>
    <script>
        // 登录框
        var login = document.querySelector('.login');
        // 遮罩
        var mask = document.querySelector('.login-bg');
        // 登录框弹出按钮
        var link = document.querySelector('#link');
        // 关闭按钮
        var closeBtn = document.querySelector('#closeBtn');
        // 登录框标题（拖动）
        var title = document.querySelector('#title');

        link.addEventListener('click', function () {
            login.style.display = 'block';
            mask.style.display = 'block';
        })
        closeBtn.addEventListener('click', function () {
            login.style.display = 'none';
            mask.style.display = 'none';
        })

        // 拖拽效果
        title.addEventListener('mousedown', function (e) {
            // 获得鼠标在盒子内的坐标
            var x = e.pageX - login.offsetLeft;
            var y = e.pageY - login.offsetTop;
            document.addEventListener('mousemove', move); // 任何时候都可以移动鼠标 事件源是document

            // 盒子移动
            function move(e) {
                login.style.left = e.pageX - x + 'px';
                login.style.top = e.pageY - y + 'px';
            }

            // 鼠标弹起 鼠标移动事件移除
            document.addEventListener('mouseup', function () {
                document.removeEventListener('mousemove', move);
            })
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo22/%E5%8F%AF%E6%8B%96%E5%8A%A8%E7%9A%84%E6%A8%A1%E6%80%81%E6%A1%86.html

### 6.案例：仿京东放大镜效果

```html
// detail.html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>手机详情页！</title>
    <meta name="description" content="品优购JD.COM-专业的综合网上购物商城,销售家电、数码通讯、电脑、家居百货、服装服饰、母婴、图书、食品等数万个品牌优质商品.便捷、诚信的服务，为您提供愉悦的网上购物体验!" />
    <meta name="Keywords" content="网上购物,网上商城,手机,笔记本,电脑,MP3,CD,VCD,DV,相机,数码,配件,手表,存储卡,品优购" />
    <!-- 引入facicon.ico网页图标 -->
    <link rel="shortcut icon" href="favicon.ico" type="image/x-icon" />
    <!-- 引入css 初始化的css 文件 -->
    <link rel="stylesheet" href="css/base.css">
    <!-- 引入公共样式的css 文件 -->
    <link rel="stylesheet" href="css/common.css">
    <!-- 引入详情页面的css文件 -->
    <link rel="stylesheet" href="css/detail.css">
    <!-- 引入我们的js 文件 -->
    <script src="js/detail.js"></script>
</head>

<body>
    <!-- 顶部快捷导航start -->
    <div class="shortcut">
        <div class="w">
            <div class="fl">
                <ul>
                    <li>品优购欢迎您！ </li>
                    <li>
                        <a href="#">请登录</a>
                        <a href="#" class="style-red">免费注册</a>
                    </li>
                </ul>
            </div>
            <div class="fr">
                <ul>
                    <li><a href="#">我的订单</a></li>
                    <li class="spacer"></li>
                    <li>
                        <a href="#">我的品优购</a>
                        <i class="icomoon"></i>
                    </li>
                    <li class="spacer"></li>
                    <li><a href="#">品优购会员</a></li>
                    <li class="spacer"></li>
                    <li><a href="#">企业采购</a></li>
                    <li class="spacer"></li>
                    <li><a href="#">关注品优购</a> <i class="icomoon"></i></li>
                    <li class="spacer"></li>
                    <li><a href="#">客户服务</a> <i class="icomoon"></i></li>
                    <li class="spacer"></li>
                    <li><a href="#">网站导航</a> <i class="icomoon"></i></li>
                </ul>
            </div>
        </div>
    </div>
    <!-- 顶部快捷导航end  -->
    <!-- header制作 -->
    <div class="header w">
        <!-- logo -->
        <div class="logo">
            <h1>
                <a href="index.html" title="品优购">品优购</a>
            </h1>
        </div>
        <!-- search -->
        <div class="search">
            <input type="text" class="text" value="请搜索内容...">
            <button class="btn">搜索</button>
        </div>
        <!-- hotwrods -->
        <div class="hotwrods">
            <a href="#" class="style-red">优惠购首发</a>
            <a href="#">亿元优惠</a>
            <a href="#">9.9元团购</a>
            <a href="#">美满99减30</a>
            <a href="#">办公用品</a>
            <a href="#">电脑</a>
            <a href="#">通信</a>
        </div>
        <div class="shopcar">
            <i class="car"> </i>我的购物车 <i class="arrow">  </i>
            <i class="count">80</i>
        </div>
    </div>
    <!-- header 结束 -->
    <!-- nav start -->
    <div class="nav">
        <div class="w">
            <div class="dropdown fl">
                <div class="dt"> 全部商品分类 </div>
                <div class="dd" style="display: none;">
                    <ul>
                        <li class="menu_item"><a href="#">家用电器</a> <i>  </i> </li>
                        <li class="menu_item">
                            <a href="list.html">手机</a> 、
                            <a href="#">数码</a> 、
                            <a href="#">通信</a>
                            <i>  </i>
                        </li>
                        <li class="menu_item"><a href="#">电脑、办公</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">家居、家具、家装、厨具</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">男装、女装、童装、内衣</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">个户化妆、清洁用品、宠物</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">鞋靴、箱包、珠宝、奢侈品</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">运动户外、钟表</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">汽车、汽车用品</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">母婴、玩具乐器</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">食品、酒类、生鲜、特产</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">医药保健</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">图书、音像、电子书</a> <i> </i> </li>
                        <li class="menu_item"><a href="#">彩票、旅行、充值、票务</a> <i> </i> </li>
                        <li class="menu_item"><a href="#">理财、众筹、白条、保险</a> <i>  </i> </li>
                    </ul>
                </div>
            </div>
            <!-- 右侧导航 -->
            <div class="navitems fl">
                <ul>
                    <li><a href="#">服装城</a></li>
                    <li><a href="#">美妆馆</a></li>
                    <li><a href="#">传智超市</a></li>
                    <li><a href="#">全球购</a></li>
                    <li><a href="#">闪购</a></li>
                    <li><a href="#">团购</a></li>
                    <li><a href="#">拍卖</a></li>
                    <li><a href="#">有趣</a></li>
                </ul>
            </div>
        </div>
    </div>
    <!-- nav end -->

    <!-- 详情页内容部分	 -->
    <div class="de_container w">
        <!-- 面包屑导航 -->
        <div class="crumb_wrap">
            <a href="#">手机、数码、通讯</a> 〉 <a href="#">手机   </a> 〉 <a href="#">Apple苹果   </a> 〉 <a href="#">iphone 6S Plus系类</a>
        </div>
        <!-- 产品介绍模块 -->
        <div class="product_intro clearfix">
            <!-- 预览区域 -->
            <div class="preview_wrap fl">
                <div class="preview_img">
                    <img src="upload/s3.png" alt="">
                    <div class="mask"></div>
                    <div class="big">
                        <img src="upload/big.jpg" alt="" class="bigImg">
                    </div>
                </div>

                <div class="preview_list">
                    <a href="#" class="arrow_prev"></a>
                    <a href="#" class="arrow_next"></a>
                    <ul class="list_item">
                        <li>
                            <img src="upload/pre.jpg" alt="">
                        </li>
                        <li class="current">
                            <img src="upload/pre.jpg" alt="">
                        </li>
                        <li>
                            <img src="upload/pre.jpg" alt="">
                        </li>
                        <li>
                            <img src="upload/pre.jpg" alt="">
                        </li>
                        <li>
                            <img src="upload/pre.jpg" alt="">
                        </li>
                    </ul>
                </div>
            </div>
            <!-- 产品详细信息 -->
            <div class="itemInfo_wrap fr">
                <div class="sku_name">
                    Apple iPhone 6s（A1700）64G玫瑰金色 移动通信电信4G手机
                </div>
                <div class="news">
                    推荐选择下方[移动优惠购],手机套餐齐搞定,不用换号,每月还有花费返
                </div>
                <div class="summary">
                    <dl class="summary_price">
                        <dt>价格</dt>
                        <dd>
                            <i class="price">￥5299.00 </i>

                            <a href="#">降价通知</a>

                            <div class="remark">累计评价612188</div>

                        </dd>
                    </dl>
                    <dl class="summary_promotion">
                        <dt>促销</dt>
                        <dd>
                            <em>加购价</em> 满999.00另加20.00元，或满1999.00另加30.00元，或满2999.00另加40.00元，即可在购物车换 购热销商品 详情 》

                        </dd>
                    </dl>
                    <dl class="summary_support">
                        <dt>支持</dt>
                        <dd>以旧换新，闲置手机回收 4G套餐超值抢 礼品购</dd>
                    </dl>
                    <dl class="choose_color">
                        <dt>选择颜色</dt>
                        <dd>
                            <a href="javascript:;" class="current">玫瑰金</a>
                            <a href="javascript:;">金色</a>
                            <a href="javascript:;">白色</a>
                            <a href="javascript:;">土豪色</a>
                        </dd>
                    </dl>
                    <dl class="choose_version">
                        <dt>选择版本</dt>
                        <dd>
                            <a href="javascript:;" class="current">公开版</a>
                            <a href="javascript:;">移动4G</a>
                        </dd>
                    </dl>
                    <dl class="choose_type">
                        <dt>购买方式</dt>
                        <dd>
                            <a href="javascript:;" class="current">官方标配</a>
                            <a href="javascript:;">移动优惠购</a>
                            <a href="javascript:;">电信优惠购</a>
                        </dd>
                    </dl>
                    <div class="choose_btns">
                        <div class="choose_amount">
                            <input type="text" value="1">
                            <a href="javascript:;" class="add">+</a>
                            <a href="javascript:;" class="reduce">-</a>
                        </div>
                        <a href="#" class="addcar">加入购物车</a>
                    </div>
                </div>
            </div>
        </div>


        <!-- 产品细节模块 product_detail	 -->
        <div class="product_detail clearfix">
            <!-- aside -->
            <div class="aside fl">
                <div class="tab_list">
                    <ul>
                        <li class="first_tab ">相关分类</li>
                        <li class="second_tab current">推荐品牌</li>
                    </ul>
                </div>
                <div class="tab_con">

                    <ul>
                        <li>
                            <img src="upload/aside_img.jpg" alt="">
                            <h5>华为 HUAWEI P20 Pro 全面屏徕卡</h5>
                            <div class="aside_price">¥19</div>
                            <a href="#" class="as_addcar">加入购物车</a>
                        </li>
                        <li>
                            <img src="upload/aside_img.jpg" alt="">
                            <h5>华为 HUAWEI P20 Pro 全面屏徕卡</h5>
                            <div class="aside_price">¥19</div>
                            <a href="#" class="as_addcar">加入购物车</a>
                        </li>
                        <li>
                            <img src="upload/aside_img.jpg" alt="">
                            <h5>华为 HUAWEI P20 Pro 全面屏徕卡</h5>
                            <div class="aside_price">¥19</div>
                            <a href="#" class="as_addcar">加入购物车</a>
                        </li>
                        <li>
                            <img src="upload/aside_img.jpg" alt="">
                            <h5>华为 HUAWEI P20 Pro 全面屏徕卡</h5>
                            <div class="aside_price">¥19</div>
                            <a href="#" class="as_addcar">加入购物车</a>
                        </li>
                        <li>
                            <img src="upload/aside_img.jpg" alt="">
                            <h5>华为 HUAWEI P20 Pro 全面屏徕卡</h5>
                            <div class="aside_price">¥19</div>
                            <a href="#" class="as_addcar">加入购物车</a>
                        </li>
                        <li>
                            <img src="upload/aside_img.jpg" alt="">
                            <h5>华为 HUAWEI P20 Pro 全面屏徕卡</h5>
                            <div class="aside_price">¥19</div>
                            <a href="#" class="as_addcar">加入购物车</a>
                        </li>


                    </ul>
                </div>
            </div>
            <!-- detail -->
            <div class="detail fr">
                <div class="detail_tab_list">
                    <ul>
                        <li class="current">商品介绍</li>
                        <li>规格与包装</li>
                        <li>售后保障</li>
                        <li>商品评价（50000）</li>
                        <li>手机社区</li>
                    </ul>
                </div>
                <div class="detail_tab_con">
                    <div class="item">
                        <ul class="item_info">
                            <li>分辨率：1920*1080(FHD)</li>
                            <li>后置摄像头：1200万像素</li>
                            <li>前置摄像头：500万像素</li>
                            <li>核 数：其他</li>
                            <li>频 率：以官网信息为准</li>
                            <li>品牌： Apple ♥关注</li>
                            <li>商品名称：APPLEiPhone 6s Plus</li>
                            <li>商品编号：1861098</li>
                            <li>商品毛重：0.51kg</li>
                            <li>商品产地：中国大陆</li>
                            <li>热点：指纹识别，Apple Pay，金属机身，拍照神器</li>
                            <li>系统：苹果（IOS）</li>
                            <li>像素：1000-1600万</li>
                            <li>机身内存：64GB</li>
                        </ul>
                        <p>
                            <a href="#" class="more">查看更多参数</a>
                        </p>
                        <img src="upload/detail_img1.jpg" alt="">
                        <img src="upload/detail_img2.jpg" alt="">
                        <img src="upload/detail_img3.jpg" alt="">
                    </div>
                    <!-- 
					<div class="item">规格与包装</div>
					<div class="item">售后保障</div> 
					-->
                </div>
            </div>
        </div>

    </div>
    <!-- 详情页内容部分	 -->

    <!-- footer start -->
    <div class="footer">
        <div class="w">
            <!-- mod_service -->
            <div class="mod_service">
                <ul>
                    <li>
                        <i class="mod-service-icon mod_service_zheng"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                    <li>
                        <i class="mod-service-icon mod_service_kuai"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                    <li>
                        <i class="mod-service-icon mod_service_bao"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                    <li>
                        <i class="mod-service-icon mod_service_bao"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                    <li>
                        <i class="mod-service-icon mod_service_bao"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                </ul>
            </div>
            <!-- mod_help -->
            <div class="mod_help">
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item mod_help_app">
                    <dt>帮助中心</dt>
                    <dd>
                        <img src="upload/erweima.png" alt="">
                        <p>品优购客户端</p>
                    </dd>
                </dl>
            </div>

            <!-- mod_copyright  -->
            <div class="mod_copyright">
                <p class="mod_copyright_links">
                    关于我们 | 联系我们 | 联系客服 | 商家入驻 | 营销中心 | 手机品优购 | 友情链接 | 销售联盟 | 品优购社区 | 品优购公益 | English Site | Contact U
                </p>
                <p class="mod_copyright_info">
                    地址：北京市昌平区建材城西路金燕龙办公楼一层 邮编：100096 电话：400-618-4000 传真：010-82935100 邮箱: zhanghj+itcast.cn <br> 京ICP备08001421号京公网安备110108007702
                </p>
            </div>
        </div>
    </div>
    <!-- footer end -->
</body>

</html>
```

```css
// detail.css
/*详情页的样式文件*/

.de_container {
    margin-top: 20px;
}

.crumb_wrap {
    height: 25px;
}

.crumb_wrap a {
    margin-right: 10px;
}

.preview_wrap {
    width: 400px;
    height: 590px;
}

.preview_img {
    position: relative;
    height: 398px;
    border: 1px solid #ccc;
}

.mask {
    display: none;
    position: absolute;
    top: 0;
    left: 0;
    width: 300px;
    height: 300px;
    background: #FEDE4F;
    opacity: .5;
    border: 1px solid #ccc;
    cursor: move;
}

.big {
    display: none;
    position: absolute;
    left: 410px;
    top: 0;
    width: 500px;
    height: 500px;
    background-color: pink;
    z-index: 999;
    border: 1px solid #ccc;
    overflow: hidden;
}

.big img {
    position: absolute;
    top: 0;
    left: 0;
}

.preview_list {
    position: relative;
    height: 60px;
    margin-top: 60px;
}

.list_item {
    width: 320px;
    height: 60px;
    margin: 0 auto;
}

.list_item li {
    float: left;
    width: 56px;
    height: 56px;
    border: 2px solid transparent;
    margin: 0 2px;
}

.list_item li.current {
    border-color: #c81623;
}

.arrow_prev,
.arrow_next {
    position: absolute;
    top: 15px;
    width: 22px;
    height: 32px;
    background-color: purple;
}

.arrow_prev {
    left: 0;
    background: url(../img/arrow-prev.png) no-repeat;
}

.arrow_next {
    right: 0;
    background: url(../img/arrow-next.png) no-repeat;
}

.itemInfo_wrap {
    width: 718px;
}

.sku_name {
    height: 30px;
    font-size: 16px;
    font-weight: 700;
}

.news {
    height: 32px;
    color: #e12228;
}

.summary dl {
    overflow: hidden;
}

.summary dt,
.summary dd {
    float: left;
}

.summary dt {
    width: 60px;
    padding-left: 10px;
    line-height: 36px;
}

.summary_price,
.summary_promotion {
    position: relative;
    padding: 10px 0;
    background-color: #fee9eb;
}

.price {
    font-size: 24px;
    color: #e12228;
}

.summary_price a {
    color: #c81623;
}

.remark {
    position: absolute;
    right: 10px;
    top: 20px;
}

.summary_promotion {
    padding-top: 0;
}

.summary_promotion dd {
    width: 450px;
    line-height: 36px;
}

.summary_promotion em {
    display: inline-block;
    width: 40px;
    height: 22px;
    background-color: #c81623;
    text-align: center;
    line-height: 22px;
    color: #fff;
}

.summary_support dd {
    line-height: 36px;
}

.choose_color a {
    display: inline-block;
    width: 80px;
    height: 41px;
    background-color: #f7f7f7;
    border: 1px solid #ededed;
    text-align: center;
    line-height: 41px;
}

.summary a.current {
    border-color: #c81623;
}

.choose_version {
    margin: 10px 0;
}

.choose_version a,
.choose_type a {
    display: inline-block;
    height: 32px;
    padding: 0 12px;
    background-color: #f7f7f7;
    border: 1px solid #ededed;
    text-align: center;
    line-height: 32px;
}

.choose_btns {
    margin-top: 20px;
}

.choose_amount {
    position: relative;
    float: left;
    width: 50px;
    height: 46px;
    background-color: pink;
}

.choose_amount input {
    width: 33px;
    height: 44px;
    border: 1px solid #ccc;
    text-align: center;
}

.add,
.reduce {
    position: absolute;
    right: 0;
    width: 15px;
    height: 22px;
    border: 1px solid #ccc;
    background-color: #f1f1f1;
    text-align: center;
    line-height: 22px;
}

.add {
    top: 0;
}

.reduce {
    bottom: 0;
    /*禁止鼠标样式*/
    cursor: not-allowed;
    /* pointer  小手  move  移动  */
}

.addcar {
    float: left;
    width: 142px;
    height: 46px;
    background-color: #c81623;
    text-align: center;
    line-height: 46px;
    font-size: 18px;
    color: #fff;
    margin-left: 10px;
    font-weight: 700;
}

.product_detail {
    margin-bottom: 50px;
}

.aside {
    width: 208px;
    border: 1px solid #ccc;
}

.tab_list {
    overflow: hidden;
    height: 34px;
}


/*把背景颜色 底边框都给 li*/

.tab_list li {
    float: left;
    background-color: #f1f1f1;
    border-bottom: 1px solid #ccc;
    height: 33px;
    text-align: center;
    line-height: 33px;
}


/*鼠标单击 li 变化样式   背景变白色 去掉下边框 文字变颜色*/

.tab_list .current {
    background-color: #fff;
    border-bottom: 0;
    color: red;
}

.first_tab {
    width: 104px;
}

.second_tab {
    width: 103px;
    border-left: 1px solid #ccc;
}

.tab_con {
    padding: 0 10px;
}

.tab_con li {
    border-bottom: 1px solid #ccc;
}

.tab_con li h5 {
    /*超出的文字省略号显示*/
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    font-weight: 400;
}

.aside_price {
    font-weight: 700;
    margin: 10px 0;
}

.as_addcar {
    display: block;
    width: 88px;
    height: 26px;
    border: 1px solid #ccc;
    background-color: #f7f7f7;
    margin: 10px auto;
    text-align: center;
    line-height: 26px;
}

.detail {
    width: 978px;
}

.detail_tab_list {
    height: 39px;
    border: 1px solid #ccc;
    background-color: #f1f1f1;
}

.detail_tab_list li {
    float: left;
    height: 39px;
    line-height: 39px;
    padding: 0 20px;
    text-align: center;
    cursor: pointer;
}

.detail_tab_list .current {
    background-color: #c81623;
    color: #fff;
}

.item_info {
    padding: 20px 0 0 20px;
}

.item_info li {
    line-height: 22px;
}

.more {
    float: right;
    font-weight: 700;
    font-family: 'icomoon';
}
```

```js
window.addEventListener('load', function () {
    var preview_img = document.querySelector('.preview_img');
    var mask = document.querySelector('.mask');
    var big = document.querySelector('.big');

    preview_img.addEventListener('mouseover', function () {
        // 鼠标移过 黄色遮挡层及放大预览模块显示
        mask.style.display = 'block';
        big.style.display = 'block';
    })

    // 鼠标移动
    preview_img.addEventListener('mousemove', function (e) {
        var x = e.pageX - this.offsetLeft;
        var y = e.pageY - this.offsetTop; // 鼠标在盒子内的坐标
        var maskX = x - mask.offsetWidth / 2;
        var maskY = y - mask.offsetHeight / 2; // 修改黄色遮挡层坐标
        var maskXMax = this.offsetWidth - mask.offsetWidth;
        var maskYMax = this.offsetHeight - mask.offsetHeight; // 遮挡层移动最大坐标
        if (maskX <= 0) {
            maskX = 0;

        } else if (maskX >= maskXMax) {
            maskX = maskXMax;
        }
        if (maskY <= 0) {
            maskY = 0;
        } else if (maskY >= maskYMax) {
            maskY = maskYMax;
        }
        mask.style.left = maskX + 'px';
        mask.style.top = maskY + 'px'; // 黄色遮罩层移动

        var bigImg = document.querySelector('.bigImg');
        var bigXMax = bigImg.offsetWidth - big.offsetWidth;
        var bigYMax = bigImg.offsetHeight - big.offsetHeight; // 大图片最大移动坐标
        var bigX = bigXMax * maskX / maskXMax;
        var bigY = bigYMax * maskY / maskYMax;
        bigImg.style.left = -bigX + 'px';
        bigImg.style.top = -bigY + 'px';

    })

    // 鼠标离开
    preview_img.addEventListener('mouseout', function () {
        // 鼠标移开 黄色遮挡层及放大预览模块显示
        mask.style.display = 'none';
        big.style.display = 'none';
    })
})
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo22/05-%E4%BA%AC%E4%B8%9C%E6%94%BE%E5%A4%A7%E9%95%9C%E6%95%88%E6%9E%9C/detail.html

## 二、元素可视区client系列

### 1.概述

我们通过client系列的相关属性来获取元素可视区的相关信息。通过client系列的相关属性可以动态地得到该元素的边框大小、元素大小等。

| 属性                 | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| elemnt.clientTop     | 返回元素上边框的大小                                         |
| element.clientLeft   | 返回元素坐标狂的大小                                         |
| element.clientWidth  | 返回自身包括padding、内容区的宽度（**不含边框**，返回数值不带单位） |
| element.clientHeight | 返回自身包括padding、内容区的高度（**不含边框**，返回数值不带单位） |

注：和offset最大的区别就是，client返回宽度/高度不包含边框。

### 2.案例：淘宝flexible.js源码分析

#### 2.1 立即执行函数

立即执行函数：不需要调用，立马能够自己执行的函数。

```js
// 写法
(function() {
    // 函数体
})();

// 或
(function() {
    // 函数体
}());
```

```js
(function(a, b) {
    console.log(a + b);
})(1, 2);

(function(a, b) {
    console.log(a + b);
}(1, 2));
```

作用：创建一个独立的作用域，避免命名冲突问题。

#### 2.2 pageshow事件

下面三种情况都会刷新页面都会触发 load 事件。

1.a标签的超链接

2.F5或者刷新按钮（强制刷新）

3.前进后退按钮

但是 火狐中，有个特点，有个“往返缓存”，这个缓存中不仅保存着页面数据，还保存了DOM和JavaScript的状态；实际上是将整个页面都保存在了内存里。

所以此时后退按钮不能刷新页面。

此时可以使用 **pageshow事件**来触发。，这个事件**在页面显示时触发**，无论页面是否来自缓存。在重新加载页面中，pageshow会在load事件触发后触发；根据事件对象中的persisted来判断是否是缓存中的页面触发的pageshow事件。注意**这个事件给window添加**。

## 三、元素滚动scroll系列

### 1.概述

我们使用scroll系列的相关属性可以动态地得到该元素的大小、滚动距离等信息。

| 属性                 | 作用                                               |
| -------------------- | -------------------------------------------------- |
| element.scrollTop    | 返回被卷去的上侧距离，返回数值不带单位             |
| element.scrollLeft   | 返回被卷去的左侧距离，返回数值不带单位             |
| element.scrollWidth  | 返回**自身实际**的宽度，不含边框，返回数值不带单位 |
| element.scrollHeight | 返回**自身实际**的高度，不含边框，返回数值不带单位 |

![image-20211217211510337](https://gitee.com/v876774538/my-img/raw/master/image-20211217211510337.png)

### 2.页面被卷去的头部

若浏览器的高/宽度不足以显示整个页面，将会自动出现滚动条。

当滚动条向下滚动时，页面上部分被隐藏的高度，就称为页面被卷去的头部。滚动条在滚动时会触发**onscroll事件**。

### 3.案例：仿淘宝固定右侧侧边栏

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>仿淘宝固定侧边栏</title>
    <style>
        .w {
            width: 1200px;
            margin: 10px auto;
        }

        .slider-bar {
            position: absolute;
            top: 300px;
            left: 50%;
            margin-left: 600px;
            width: 45px;
            height: 130px;
            background-color: pink;

        }

        span {
            position: absolute;
            bottom: 0;
            display: none;
            cursor: pointer;
        }

        .header {
            height: 150px;
            background-color: skyblue;
        }

        .banner {
            height: 250px;
            background-color: steelblue;
        }

        .main {
            height: 1000px;
            background-color: teal;
        }
    </style>
</head>

<body>
    <div class="slider-bar">
        <span class="goBack">返回顶部</span>
    </div>
    <div class="header w">头部区域</div>
    <div class="banner w">banner区域</div>
    <div class="main w">主体区域</div>
    <script>
        // 页面被卷去的头部：可以通过window.pageYOffset获得
        // 页面被卷去的左侧：可以通过window.pageXOffset获得
        // 元素内容被卷去的头部：element.scrollTop
        var sliderBar = document.querySelector('.slider-bar');
        var banner = document.querySelector('.banner');
        var bannerTop = banner.offsetTop;
        var sliderBarTop = sliderBar.offsetTop - banner.offsetTop;
        var main = document.querySelector('.main');
        var mainTop = main.offsetTop;
        var goBack = document.querySelector('.goBack');
        document.addEventListener('scroll', function () {
            // console.log(window.pageYOffset);
            if (window.pageYOffset >= bannerTop) {
                sliderBar.style.position = 'fixed';
                sliderBar.style.top = sliderBarTop + 'px';
            } else {
                sliderBar.style.position = 'absolute';
                sliderBar.style.top = '300px';
            }
            if (window.pageYOffset >= mainTop) {
                goBack.style.display = 'block';
            } else {
                goBack.style.display = 'none';
            }
        })
        goBack.addEventListener('click', function () {
            // 返回顶部
            document.body.scrollTop = 0;
            document.documentElement.scrollTop = 0;
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo22/%E4%BB%BF%E6%B7%98%E5%AE%9D%E5%9B%BA%E5%AE%9A%E4%BE%A7%E8%BE%B9%E6%A0%8F.html

页面被卷去的头部兼容性解决方案：

- 声明了DTD，使用document.documentElement.scrollTop；

- 未声明DTD，使用document.body.scrollTop；

- 新方法window.pageYOffset及window.pageXOffset，IE9开始支持。

  ```js
  funcstion getScroll() {
  	return {
  		left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft || 0,
  		top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0
  	};
  }
  
  // 使用：
  // getScroll().left
  ```

### 4.三大系列总结

| 属性                | 作用                                                         |
| ------------------- | ------------------------------------------------------------ |
| element.offsetWidth | 返回自身包括padding、边框、内容区的宽度，返回数值不带单位    |
| element.clientWidth | 返回自身包括padding。内容区的宽度，不含边框，返回数值不带单位 |
| element.scrollWidth | 返回自身实际的宽度，不含边框，返回数值不带单位               |

主要用法：

- **offset**系列常用于获取**元素位置**：**offsetLeft、offsetTop**
- **client**系列常用于获取**元素大小**：**clientWidth**、**clientHeight**
- **scroll**系列常用于获取**滚动距离**：**scrollTop**、**scrollLeft**
- **页面的滚动距离**通过：**window.pageXOffset**及**window.pageYOffset**获得

## 四、动画函数封装

### 1.动画原理

通过定时器setInterval()不断移动盒子位置。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>动画原理</title>
    <style>
        div {
            position: absolute;
            left: 0;
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div></div>
    <script>
        var div = document.querySelector('div');
        // console.log(div.offsetLeft);
        var timer = setInterval(move, 10);

        function move() {
            div.style.left = div.offsetLeft + 1 + 'px';
            if (div.offsetLeft == document.documentElement.clientWidth - div.clientWidth) {
                clearInterval(timer);
            }
        }
    </script>
</body>

</html>
```

### 2.动画函数简单封装

```js
// obj 目标对象 target 目标位置
function animateMove(obj, target) {
	var timer = setInterval(function() {
		obj.style.left = obj.offsetLeft + 1 + 'px';
		if (obj.offsetLeft == target) {
			clearInterval(timer);
		}
	}, 10);
}
```

### 3.动画函数给不同元素记录不同定时器

JS是一门动态语言，可以很方便地**给当前对象添加属性**。避免了每次都用var开辟新的空间，节省空间。

```js
// obj 目标对象 target 目标位置
function animateMove(obj, target) {
    // 让元素只有一个定时器执行 避免如多次点击导致的元素开启多个定时器的问题
    clearInterval(obj.timer);
    
	obj.timer = setInterval(function() {
		obj.style.left = obj.offsetLeft + 1 + 'px';
		if (obj.offsetLeft == target) {
			clearInterval(obj.timer);
		}
	}, 10);
}
```

### 4.缓动动画原理

所谓缓动动画就是让元素的运动速度有所变化，最常见的是让元素慢慢地停下。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>缓动动画</title>
    <style>
        div {
            position: absolute;
            left: 0;
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div></div>
    <script>
        var div = document.querySelector('div');
        animateMove(div, 500);

        // 1. 让盒子每次移动的距离慢慢变小
        // 2. 核心算法：(目标值 - 当前位置) / 10 = 每次移动的距离步长
        function animateMove(obj, target) {
            var step = (target - obj.offsetLeft) / 100;
            // 考虑到正着走和倒着走的问题
            step = step > 0 ? Math.ceil(step) : Math.floor(step);

            // 让元素只有一个定时器执行 避免如多次点击导致的元素开启多个定时器的问题
            clearInterval(obj.timer);

            obj.timer = setInterval(function () {
                obj.style.left = obj.offsetLeft + step + 'px';
                if (obj.offsetLeft == target) {
                    clearInterval(obj.timer);
                }
            }, 15);
        }
    </script>


</body>

</html>
```

### 5.动画函数添加回调函数

回调函数原理：**将函数作为一个参数传到另一个函数内**，当函数执行完之后，再执行我们穿进去的函数，这个过程就称为**回调**。

```js
var div = document.querySelector('div');
animateMove(div, 500, callback);

// 1. 让盒子每次移动的距离慢慢变小
// 2. 核心算法：(目标值 - 当前位置) / 10 = 每次移动的距离步长
function animateMove(obj, target, callback) {
    var step = (target - obj.offsetLeft) / 100;
    // 考虑到正着走和倒着走的问题
    step = step > 0 ? Math.ceil(step) : Math.floor(step);

    // 让元素只有一个定时器执行 避免如多次点击导致的元素开启多个定时器的问题
    clearInterval(obj.timer);

    obj.timer = setInterval(function () {
        obj.style.left = obj.offsetLeft + step + 'px';
        if (obj.offsetLeft == target) {
            clearInterval(obj.timer);
            if (callback) {
                callback(obj);
            }
        }
    }, 15);
}

function callback(obj) {
    obj.style.backgroundColor = 'skyblue';
}
```

### 6.动画函数封装到单独JS文件

1. 单独新建一个JS文件

   ```js
   // animate.js
   function animateMove(obj, target, callback) {
       var step = (target - obj.offsetLeft) / 10;
       // 考虑到正着走和倒着走的问题
       step = step > 0 ? Math.ceil(step) : Math.floor(step);
   
       // 让元素只有一个定时器执行 避免如多次点击导致的元素开启多个定时器的问题
       clearInterval(obj.timer);
   
       obj.timer = setInterval(function () {
           obj.style.left = obj.offsetLeft + step + 'px';
           if (obj.offsetLeft == target) {
               clearInterval(obj.timer);
               if (callback) {
                   callback(obj);
               }
           }
       }, 15);
   }
   ```

2. 引入JS文件

   ```html
   <script scr="animate.js"></script>
   ```

3. 示例：

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>动画函数的使用</title>
       <style>
           .sliderbar {
               position: fixed;
               right: 0;
               bottom: 100px;
               width: 40px;
               height: 40px;
               text-align: center;
               line-height: 40px;
               cursor: pointer;
               color: #fff;
           }
   
           .con {
               position: absolute;
               left: 0;
               top: 0;
               width: 200px;
               height: 40px;
               background-color: pink;
               z-index: -1;
           }
       </style>
       <script src="animate.js"></script>
   </head>
   
   <body>
       <div class="sliderbar">
           <span>←</span>
           <div class="con">问题反馈</div>
       </div>
       <script>
           var sliderbar = document.querySelector('.sliderbar');
           var con = document.querySelector('.con');
           sliderbar.addEventListener('mouseenter', function () {
               animateMove(con, -160, function () {
                   sliderbar.children[0].innerHTML = '→';
               });
           });
           sliderbar.addEventListener('mouseleave', function () {
               animateMove(con, 0, function () {
                   sliderbar.children[0].innerHTML = '←';
   
               });
           })
       </script>
   </body>
   
   </html>
   ```

   file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo22/%E5%8A%A8%E7%94%BB%E5%87%BD%E6%95%B0%E7%9A%84%E4%BD%BF%E7%94%A8.html

## 五、常见网页特效案例

### 1.网页轮播图

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <title>品优购-综合网购首选-正品低价、品质保障、配送及时、轻松购物！</title>
    <meta name="description" content="品优购JD.COM-专业的综合网上购物商城,销售家电、数码通讯、电脑、家居百货、服装服饰、母婴、图书、食品等数万个品牌优质商品.便捷、诚信的服务，为您提供愉悦的网上购物体验!" />
    <meta name="Keywords" content="网上购物,网上商城,手机,笔记本,电脑,MP3,CD,VCD,DV,相机,数码,配件,手表,存储卡,品优购" />
    <!-- 引入facicon.ico网页图标 -->
    <link rel="shortcut icon" href="favicon.ico" type="image/x-icon" />
    <!-- 引入css 初始化的css 文件 -->
    <link rel="stylesheet" href="css/base.css">
    <!-- 引入公共样式的css 文件 -->
    <link rel="stylesheet" href="css/common.css">
    <!-- 引入 首页的css文件 -->
    <link rel="stylesheet" href="css/index.css">
    <!-- 这个animate.js 必须写到 index.js的上面引入 -->
    <script src="js/animate.js"></script>
    <!-- 引入我们首页的js文件 -->
    <script src="js/index.js"></script>
</head>

<body>
    <!-- 顶部快捷导航start -->
    <div class="shortcut">
        <div class="w">
            <div class="fl">
                <ul>
                    <li>品优购欢迎您！ </li>
                    <li>
                        <a href="#">请登录</a>
                        <a href="#" class="style-red">免费注册</a>
                    </li>
                </ul>
            </div>
            <div class="fr">
                <ul>
                    <li><a href="#">我的订单</a></li>
                    <li class="spacer"></li>
                    <li>
                        <a href="#">我的品优购</a>
                        <i class="icomoon"></i>
                    </li>
                    <li class="spacer"></li>
                    <li><a href="#">品优购会员</a></li>
                    <li class="spacer"></li>
                    <li><a href="#">企业采购</a></li>
                    <li class="spacer"></li>
                    <li><a href="#">关注品优购</a> <i class="icomoon"></i></li>
                    <li class="spacer"></li>
                    <li><a href="#">客户服务</a> <i class="icomoon"></i></li>
                    <li class="spacer"></li>
                    <li><a href="#">网站导航</a> <i class="icomoon"></i></li>
                </ul>
            </div>
        </div>
    </div>
    <!-- 顶部快捷导航end  -->
    <!-- header制作 -->
    <div class="header w">
        <!-- logo -->
        <div class="logo">
            <h1>
                <a href="index.html" title="品优购">品优购</a>
            </h1>
        </div>
        <!-- search -->
        <div class="search">
            <input type="text" class="text" value="请搜索内容...">
            <button class="btn">搜索</button>
        </div>
        <!-- hotwrods -->
        <div class="hotwrods">
            <a href="#" class="style-red">优惠购首发</a>
            <a href="#">亿元优惠</a>
            <a href="#">9.9元团购</a>
            <a href="#">美满99减30</a>
            <a href="#">办公用品</a>
            <a href="#">电脑</a>
            <a href="#">通信</a>
        </div>
        <div class="shopcar">
            <i class="car"> </i>我的购物车 <i class="arrow">  </i>
            <i class="count">80</i>
        </div>
    </div>
    <!-- header 结束 -->
    <!-- nav start -->
    <div class="nav">
        <div class="w">
            <div class="dropdown fl">
                <div class="dt"> 全部商品分类 </div>
                <div class="dd">
                    <ul>
                        <li class="menu_item"><a href="#">家用电器</a> <i>  </i> </li>
                        <li class="menu_item">
                            <a href="list.html">手机</a> 、
                            <a href="#">数码</a> 、
                            <a href="#">通信</a>
                            <i>  </i>
                        </li>
                        <li class="menu_item"><a href="#">电脑、办公</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">家居、家具、家装、厨具</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">男装、女装、童装、内衣</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">个户化妆、清洁用品、宠物</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">鞋靴、箱包、珠宝、奢侈品</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">运动户外、钟表</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">汽车、汽车用品</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">母婴、玩具乐器</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">食品、酒类、生鲜、特产</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">医药保健</a> <i>  </i> </li>
                        <li class="menu_item"><a href="#">图书、音像、电子书</a> <i> </i> </li>
                        <li class="menu_item"><a href="#">彩票、旅行、充值、票务</a> <i> </i> </li>
                        <li class="menu_item"><a href="#">理财、众筹、白条、保险</a> <i>  </i> </li>
                    </ul>
                </div>
            </div>
            <!-- 右侧导航 -->
            <div class="navitems fl">
                <ul>
                    <li><a href="#">服装城</a></li>
                    <li><a href="#">美妆馆</a></li>
                    <li><a href="#">传智超市</a></li>
                    <li><a href="#">全球购</a></li>
                    <li><a href="#">闪购</a></li>
                    <li><a href="#">团购</a></li>
                    <li><a href="#">拍卖</a></li>
                    <li><a href="#">有趣</a></li>
                </ul>
            </div>
        </div>
    </div>
    <!-- nav end  -->
    <!-- main 模块 -->
    <div class="w">
        <div class="main">
            <div class="focus fl">
                <!-- 左侧按钮 -->
                <a href="javascript:;" class="arrow-l">
                    &lt;
                 </a>
                <!-- 右侧按钮 -->
                <a href="javascript:;" class="arrow-r">  </a>
                <!-- 核心的滚动区域 -->
                <ul>
                    <li>
                        <a href="#"><img src="upload/focus.jpg" alt=""></a>
                    </li>
                    <li>
                        <a href="#"><img src="upload/focus1.jpg" alt=""></a>
                    </li>
                    <li>
                        <a href="#"><img src="upload/focus2.jpg" alt=""></a>
                    </li>
                    <li>
                        <a href="#"><img src="upload/focus3.jpg" alt=""></a>
                    </li>
                </ul>
                <!-- 小圆圈 -->
                <ol class="circle">

                </ol>
            </div>
            <div class="newsflash fr">
                <div class="news">
                    <div class="news-hd">
                        品优购快报
                        <a href="#">更多</a>
                    </div>
                    <div class="news-bd">
                        <ul>
                            <li><a href="#">【特惠】爆款耳机5折秒！</a></li>
                            <li><a href="#">【特惠】母亲节，健康好礼低至5折！</a></li>
                            <li><a href="#">【特惠】爆款耳机5折秒！</a></li>
                            <li><a href="#">【特惠】9.9元洗100张照片！</a></li>
                            <li><a href="#">【特惠】长虹智能空调立省1000</a></li>
                        </ul>
                    </div>
                </div>
                <div class="lifeservice">
                    <ul>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_huafei"></i>
                                <p>话费</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                            <span class="hot"></span>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                        <li>
                            <a href="#">
                                <i class="service_ico service_ico_feiji"></i>
                                <p>机票</p>
                            </a>
                        </li>
                    </ul>
                </div>
                <div class="bargain">
                    <img src="upload/bargain.jpg" alt="">
                </div>
            </div>
        </div>
    </div>

    <!-- 推荐服务模块 start -->
    <div class="recommend w">
        <div class="recom-hd fl">
            <img src="img/clock.png" alt="">
            <h3>今日推荐</h3>
        </div>
        <div class="recom-bd fl">
            <ul>
                <li>
                    <a href="#">
                        <img src="upload/pic.jpg" alt="">
                    </a>
                </li>
                <li>
                    <a href="#">
                        <img src="upload/pic.jpg" alt="">
                    </a>
                </li>
                <li>
                    <a href="#">
                        <img src="upload/pic.jpg" alt="">
                    </a>
                </li>
                <li class="last">
                    <a href="#">
                        <img src="upload/pic.jpg" alt="">
                    </a>
                </li>

            </ul>
        </div>
    </div>
    <!-- 推荐服务模块 end -->

    <!-- 楼层区 start -->
    <div class="floor">
        <div class="jiadian w">
            <div class="box-hd">
                <h3>家用电器</h3>
                <div class="tab-list">
                    <ul>
                        <li><a href="#" class="style-red">热门</a>|</li>
                        <li><a href="#">大家电</a>|</li>
                        <li><a href="#">生活电器</a>|</li>
                        <li><a href="#">厨房电器</a>|</li>
                        <li><a href="#">个护健康</a>|</li>
                        <li><a href="#">应季电器</a>|</li>
                        <li><a href="#">空气/净水</a>|</li>
                        <li><a href="#">新奇特</a>|</li>
                        <li><a href="#">高端电器</a></li>
                    </ul>
                </div>
            </div>
            <div class="box-bd">
                <ul class="tab-con">
                    <li class="w209">
                        <ul class="tab-con-list">
                            <li>
                                <a href="#">节能补贴</a>
                            </li>
                            <li>
                                <a href="#">4K电视</a>
                            </li>
                            <li>
                                <a href="#">空气净化器</a>
                            </li>
                            <li>
                                <a href="#">IH电饭煲</a>
                            </li>
                            <li>
                                <a href="#">滚筒洗衣机</a>
                            </li>
                            <li>
                                <a href="#">电热水器</a>
                            </li>
                        </ul>
                        <img src="upload/floor-1-1.png" alt="">
                    </li>
                    <li class="w329">
                        <img src="upload/pic1.jpg" alt="">
                    </li>
                    <li class="w219">
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-2.png" alt="">
                            </a>
                        </div>
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-3.png" alt="">
                            </a>
                        </div>
                    </li>
                    <li class="w220">
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-4.png" alt="">
                            </a>
                        </div>
                    </li>
                    <li class="w220">
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-5.png" alt="">
                            </a>
                        </div>
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-6.png" alt="">
                            </a>
                        </div>
                    </li>
                </ul>
                <!-- <ul class="tab-con">
					<li>1</li>
					<li>2</li>
					<li>3</li>
					<li>4</li>
					<li>5</li>
				</ul> -->
            </div>
        </div>
        <div class="shouji w">
            <div class="box-hd">
                <h3>手机通讯</h3>
                <div class="tab-list">
                    <ul>
                        <li><a href="#" class="style-red">热门</a>|</li>
                        <li><a href="#">大家电</a>|</li>
                        <li><a href="#">生活电器</a>|</li>
                        <li><a href="#">厨房电器</a>|</li>
                        <li><a href="#">个护健康</a>|</li>
                        <li><a href="#">应季电器</a>|</li>
                        <li><a href="#">空气/净水</a>|</li>
                        <li><a href="#">新奇特</a>|</li>
                        <li><a href="#">高端电器</a></li>
                    </ul>
                </div>
            </div>
            <div class="box-bd">
                <ul class="tab-con">
                    <li class="w209">
                        <ul class="tab-con-list">
                            <li>
                                <a href="#">节能补贴</a>
                            </li>
                            <li>
                                <a href="#">4K电视</a>
                            </li>
                            <li>
                                <a href="#">空气净化器</a>
                            </li>
                            <li>
                                <a href="#">IH电饭煲</a>
                            </li>
                            <li>
                                <a href="#">滚筒洗衣机</a>
                            </li>
                            <li>
                                <a href="#">电热水器</a>
                            </li>
                        </ul>
                        <img src="upload/floor-1-1.png" alt="">
                    </li>
                    <li class="w329">
                        <img src="upload/pic1.jpg" alt="">
                    </li>
                    <li class="w219">
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-2.png" alt="">
                            </a>
                        </div>
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-3.png" alt="">
                            </a>
                        </div>
                    </li>
                    <li class="w220">
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-4.png" alt="">
                            </a>
                        </div>
                    </li>
                    <li class="w220">
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-5.png" alt="">
                            </a>
                        </div>
                        <div class="tab-con-item">
                            <a href="#">
                                <img src="upload/floor-1-6.png" alt="">
                            </a>
                        </div>
                    </li>
                </ul>
                <!-- <ul class="tab-con">
					<li>1</li>
					<li>2</li>
					<li>3</li>
					<li>4</li>
					<li>5</li>
				</ul> -->
            </div>
        </div>
    </div>
    <!-- 楼层区 end -->
    <!-- 固定电梯导航 -->
    <div class="fixedtool">
        <ul>
            <li class="current">家用电器</li>
            <li>手机通讯</li>
            <li>家用电器</li>
            <li>家用电器</li>
            <li>家用电器</li>
            <li>家用电器</li>
        </ul>
    </div>
    <!-- footer start -->
    <div class="footer">
        <div class="w">
            <!-- mod_service -->
            <div class="mod_service">
                <ul>
                    <li>
                        <i class="mod-service-icon mod_service_zheng"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                    <li>
                        <i class="mod-service-icon mod_service_kuai"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                    <li>
                        <i class="mod-service-icon mod_service_bao"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                    <li>
                        <i class="mod-service-icon mod_service_bao"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                    <li>
                        <i class="mod-service-icon mod_service_bao"></i>
                        <div class="mod_service_tit">
                            <h5>正品保障</h5>
                            <p>正品保障，提供发票</p>
                        </div>
                    </li>
                </ul>
            </div>
            <!-- mod_help -->
            <div class="mod_help">
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item">
                    <dt>购物指南</dt>
                    <dd> <a href="#">购物流程 </a></dd>
                    <dd> <a href="#">会员介绍 </a></dd>
                    <dd> <a href="#">生活旅行/团购 </a></dd>
                    <dd> <a href="#">常见问题 </a></dd>
                    <dd> <a href="#">大家电 </a></dd>
                    <dd> <a href="#">联系客服 </a></dd>
                </dl>
                <dl class="mod_help_item mod_help_app">
                    <dt>帮助中心</dt>
                    <dd>
                        <img src="upload/erweima.png" alt="">
                        <p>品优购客户端</p>
                    </dd>
                </dl>
            </div>

            <!-- mod_copyright  -->
            <div class="mod_copyright">
                <p class="mod_copyright_links">
                    关于我们 | 联系我们 | 联系客服 | 商家入驻 | 营销中心 | 手机品优购 | 友情链接 | 销售联盟 | 品优购社区 | 品优购公益 | English Site | Contact U
                </p>
                <p class="mod_copyright_info">
                    地址：北京市昌平区建材城西路金燕龙办公楼一层 邮编：100096 电话：400-618-4000 传真：010-82935100 邮箱: zhanghj+itcast.cn <br> 京ICP备08001421号京公网安备110108007702
                </p>
            </div>
        </div>
    </div>
    <!-- footer end -->
</body>

</html>
```

```css
/* index.css */
/*这个文件里面放的是 首页的样式*/

.main {
    width: 980px;
    height: 455px;
    margin-left: 219px;
    margin-top: 10px;
}

.focus {
    position: relative;
    width: 721px;
    height: 455px;
    background-color: purple;
    overflow: hidden;
}

.focus ul {
    position: absolute;
    top: 0;
    left: 0;
    width: 600%;
}

.focus ul li {
    float: left;
}

.arrow-l,
.arrow-r {
    display: none;
    position: absolute;
    top: 50%;
    margin-top: -20px;
    width: 24px;
    height: 40px;
    background: rgba(0, 0, 0, .3);
    text-align: center;
    line-height: 40px;
    color: #fff;
    font-family: 'icomoon';
    font-size: 18px;
    z-index: 2;
}

.arrow-r {
    right: 0;
}

.circle {
    position: absolute;
    bottom: 10px;
    left: 50px;
}

.circle li {
    float: left;
    width: 8px;
    height: 8px;
    /*background-color: #fff;*/
    border: 2px solid rgba(255, 255, 255, 0.5);
    margin: 0 3px;
    border-radius: 50%;
    /*鼠标经过显示小手*/
    cursor: pointer;
}

.current {
    background-color: #fff;
}

.newsflash {
    width: 250px;
    height: 455px;
}

.news {
    height: 163px;
    border: 1px solid #ccc;
}

.news-hd {
    height: 32px;
    /*dotted 点线  dashed  虚线*/
    border-bottom: 1px dotted #ccc;
    padding: 0 15px;
    font-size: 14px;
    line-height: 32px;
}

.news-hd a {
    float: right;
    font-size: 12px;
    font-family: 'icomoon';
}

.news-bd {
    padding: 10px 0 0 15px;
}

.news-bd li {
    height: 23px;
}

.lifeservice {
    overflow: hidden;
    height: 208px;
    border: 1px solid #ccc;
    border-top: none;
}

.lifeservice ul {
    width: 252px;
}

.lifeservice li {
    position: relative;
    float: left;
    width: 62px;
    height: 70px;
    border-right: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
}

.lifeservice li a {
    display: block;
    /* overflow: hidden; 解决i 引起的 外边距塌陷合并的问题*/
    overflow: hidden;
    height: 100%;
}

.lifeservice li p {
    text-align: center;
}

.hot {
    position: absolute;
    right: 0;
    top: 0;
    width: 12px;
    height: 15px;
    background: url(../img/jian.jpg) no-repeat;
}

.service_ico {
    display: block;
    width: 24px;
    height: 24px;
    background: url(../img/icons.png) no-repeat;
    margin: 10px auto;
}

.service_ico_huafei {
    background-position: -17px -16px;
}

.service_ico_feiji {
    width: 26px;
    background-position: -78px -16px;
}

.bargain {
    height: 75px;
    margin-top: 5px;
}


/*推荐模块*/

.recommend {
    height: 163px;
    margin-top: 10px;
}

.recom-hd {
    width: 200px;
    height: 163px;
    background-color: #5c5251;
    text-align: center;
}

.recom-hd img {
    margin: 30px 0 10px 0;
}

.recom-hd h3 {
    font-size: 18px;
    color: #fff;
    font-weight: normal;
}

.recom-bd {
    width: 1000px;
    height: 163px;
    background-color: #ebebeb;
}

.recom-bd li {
    float: left;
    width: 249px;
    height: 145px;
    border-right: 1px solid #ccc;
    margin-top: 10px;
}

.recom-bd .last {
    border-right: 0;
}


/*floor 楼层区*/

.box-hd {
    height: 30px;
    border-bottom: 2px solid #c81623;
    margin-top: 25px;
}

.box-hd h3 {
    float: left;
    font-size: 18px;
    color: #c81623;
}

.tab-list {
    float: right;
    line-height: 30px;
}

.tab-list li {
    float: left;
}

.tab-list li a {
    margin: 0 15px;
}

.box-bd {
    height: 360px;
}

.w209 {
    width: 209px;
    background-color: #f9f9f9;
}

.w329 {
    width: 329px;
}

.w219 {
    width: 219px;
    border-right: 1px solid #ccc;
}

.w220 {
    width: 220px;
    border-right: 1px solid #ccc;
}

.tab-con li {
    float: left;
    height: 360px;
}

.tab-con-item {
    border-bottom: 1px solid #ccc;
}

.tab-con-list {
    overflow: hidden;
    margin-bottom: 15px;
}

.tab-con-list li {
    width: 86px;
    height: 32px;
    line-height: 32px;
    border-bottom: 1px solid #ccc;
    margin-left: 10px;
    text-align: center;
}

.box-bd li {
    overflow: hidden;
}

.box-bd img {
    /*过渡写到本身上， 谁做动画，给谁加*/
    transition: all .2s;
}


/*我们鼠标经过图片 往右走 8px*/

.box-bd img:hover {
    margin-left: 8px;
}


/*电梯导航*/

.fixedtool {
    position: fixed;
    top: 100px;
    left: 50%;
    margin-left: -676px;
    width: 66px;
    background-color: #fff;
}

.fixedtool li {
    height: 32px;
    line-height: 32px;
    text-align: center;
    font-size: 12px;
    border-bottom: 1px solid #ccc;
    cursor: pointer;
}

.fixedtool .current {
    background-color: #c81623;
    color: #fff;
}
```

```js
// animate.js
function animate(obj, target, callback) {
    // console.log(callback);  callback = function() {}  调用的时候 callback()

    // 先清除以前的定时器，只保留当前的一个定时器执行
    clearInterval(obj.timer);
    obj.timer = setInterval(function() {
        // 步长值写到定时器的里面
        // 把我们步长值改为整数 不要出现小数的问题
        // var step = Math.ceil((target - obj.offsetLeft) / 10);
        var step = (target - obj.offsetLeft) / 10;
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        if (obj.offsetLeft == target) {
            // 停止动画 本质是停止定时器
            clearInterval(obj.timer);
            // 回调函数写到定时器结束里面
            // if (callback) {
            //     // 调用函数
            //     callback();
            // }
            callback && callback();	// 短路运算
        }
        // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
        obj.style.left = obj.offsetLeft + step + 'px';

    }, 15);
}
```

```js
// index.js
window.addEventListener('load', function () {
    // 轮播图
    var focus = document.querySelector('.focus');
    var focusWidth = focus.offsetWidth;
    var ul = focus.querySelector('ul');

    // 小圆圈
    var ol = focus.querySelector('.circle');
    var circle = 0; // 控制小圆圈播放
    // 动态生成小圆圈
    for (var i = 0; i < ul.children.length; i++) {
        // 创建li节点
        var li = document.createElement('li');
        // 插入到ol
        ol.appendChild(li);
        // 自定义属性 记录当前小圆圈索引号
        li.setAttribute('index', i);
        // 绑定点击事件
        li.addEventListener('click', function () {
            for (var j = 0; j < ol.children.length; j++) {
                ol.children[j].className = '';
            }
            this.className = 'current';
            // 图片滚动
            // ul移动距离：小圆圈的索引号 × 图片宽度
            var index = this.getAttribute('index');
            // 将index赋给num
            num = index;
            // 将index赋给circle
            circle = index;
            var target = num * focusWidth;
            animate(ul, -target);
        })
    }
    ol.children[0].className = 'current';

    // 左右箭头
    var arrow_l = document.querySelector('.arrow-l');
    var arrow_r = document.querySelector('.arrow-r');
    var num = 0;
    var flag = true; // 节流阀
    // 克隆第一章图片放到ul的最后面
    var first = ul.children[0].cloneNode(true);
    ul.appendChild(first);
    focus.addEventListener('mouseenter', function () {
        arrow_l.style.display = 'block';
        arrow_r.style.display = 'block';
        // 停止自动播放定时器
        clearInterval(timer);
        timer = null;
    })
    focus.addEventListener('mouseleave', function () {
        arrow_l.style.display = 'none';
        arrow_r.style.display = 'none';
        // 启动自动播放定时器
        timer = setInterval(function () {
            // 手动调用点击事件
            arrow_r.click();
        }, 5000);
    })
    arrow_l.addEventListener('click', function () {
        // 节流阀 动画播放完后才进行下一次点击 防止点击过快
        if (flag) {
            flag = false;
            if (num == 0) {
                num = ul.children.length - 1;
                ul.style.left = -num * focusWidth + 'px';
            }
            num--;
            var target = num * focusWidth;
            animate(ul, -target, function () {
                flag = true;
            });

            circle--;
            if (circle < 0) {
                circle = ol.children.length - 1;
            }
            for (var i = 0; i < ol.children.length; i++) {
                ol.children[i].className = '';
            }
            ol.children[circle].className = 'current';
        }
    })
    arrow_r.addEventListener('click', function () {
        if (flag) {
            flag = false;
            // 无缝滚动：将ul第一个li复制一份 放到ul最后面 当图片滚动到克隆的最后一张图片时 让Ul快速地、不做动画地跳到最左侧（left = 0）
            if (num == ul.children.length - 1) {
                ul.style.left = 0;
                num = 0;
            }
            num++;
            var target = num * focusWidth;
            animate(ul, -target, function () {
                flag = true;
            });
            // 小圆圈跟随变化
            circle++;
            if (circle > ol.children.length - 1) {
                circle = 0;
            }
            for (var i = 0; i < ol.children.length; i++) {
                ol.children[i].className = '';
            }
            ol.children[circle].className = 'current';
        }

    })

    // 自动播放
    var timer = this.setInterval(function () {
        // 手动调用点击事件
        arrow_r.click();
    }, 5000)
})
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo22/05-%E8%BD%AE%E6%92%AD%E5%9B%BE%E5%88%B6%E4%BD%9C/index.html

### 2.带有动画的返回顶部

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>带有动画的返回顶部</title>
    <style>
        .w {
            width: 1200px;
            margin: 10px auto;
        }

        .slider-bar {
            position: absolute;
            top: 300px;
            left: 50%;
            margin-left: 600px;
            width: 45px;
            height: 130px;
            background-color: pink;

        }

        span {
            position: absolute;
            bottom: 0;
            display: none;
            cursor: pointer;
        }

        .header {
            height: 150px;
            background-color: skyblue;
        }

        .banner {
            height: 250px;
            background-color: steelblue;
        }

        .main {
            height: 1000px;
            background-color: teal;
        }
    </style>
</head>

<body>
    <div class="slider-bar">
        <span class="goBack">返回顶部</span>
    </div>
    <div class="header w">头部区域</div>
    <div class="banner w">banner区域</div>
    <div class="main w">主体区域</div>
    <script>
        // 页面被卷去的头部：可以通过window.pageYOffset获得
        // 页面被卷去的左侧：可以通过window.pageXOffset获得
        // 元素内容被卷去的头部：element.scrollTop
        var sliderBar = document.querySelector('.slider-bar');
        var banner = document.querySelector('.banner');
        var bannerTop = banner.offsetTop;
        var sliderBarTop = sliderBar.offsetTop - banner.offsetTop;
        var main = document.querySelector('.main');
        var mainTop = main.offsetTop;
        var goBack = document.querySelector('.goBack');
        document.addEventListener('scroll', function () {
            // console.log(window.pageYOffset);
            if (window.pageYOffset >= bannerTop) {
                sliderBar.style.position = 'fixed';
                sliderBar.style.top = sliderBarTop + 'px';
            } else {
                sliderBar.style.position = 'absolute';
                sliderBar.style.top = '300px';
            }
            if (window.pageYOffset >= mainTop) {
                goBack.style.display = 'block';
            } else {
                goBack.style.display = 'none';
            }
        })
        goBack.addEventListener('click', function () {
            // 返回顶部
            // document.body.scrollTop = 0;
            // document.documentElement.scrollTop = 0;
            animate(window, 0);
        })

        // 动画函数
        function animate(obj, target, callback) {
            // console.log(callback);  callback = function() {}  调用的时候 callback()

            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function () {
                // 步长值写到定时器的里面
                // 把我们步长值改为整数 不要出现小数的问题
                var step = (target - window.pageYOffset) / 10;
                step = step > 0 ? Math.ceil(step) : Math.floor(step);
                if (window.pageYOffset == target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                    // 回调函数写到定时器结束里面
                    // if (callback) {
                    //     // 调用函数
                    //     callback();
                    // }
                    callback && callback();
                }
                // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
                window.scroll(0, window.pageYOffset + step);

            }, 15);
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo22/%E5%B8%A6%E6%9C%89%E5%8A%A8%E7%94%BB%E7%9A%84%E8%BF%94%E5%9B%9E%E9%A1%B6%E9%83%A8.html

### 3.筋斗云案例

```html
<!DOCTYPE html>
<html>

<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        * {
            margin: 0;
            padding: 0
        }

        ul {
            list-style: none;
        }

        body {
            background-color: black;
        }

        .c-nav {
            width: 900px;
            height: 42px;
            background: #fff url(images/rss.png) no-repeat right center;
            margin: 100px auto;
            border-radius: 5px;
            position: relative;
        }

        .c-nav ul {
            position: absolute;
        }

        .c-nav li {
            float: left;
            width: 83px;
            text-align: center;
            line-height: 42px;
        }

        .c-nav li a {
            color: #333;
            text-decoration: none;
            display: inline-block;
            height: 42px;
        }

        .c-nav li a:hover {
            color: white;
        }

        .c-nav li.current a {
            color: #0dff1d;
        }

        .cloud {
            position: absolute;
            left: 0;
            top: 0;
            width: 83px;
            height: 42px;
            background: url(images/cloud.gif) no-repeat;
        }
    </style>
    <script src="animate.js"></script>
</head>

<body>
    <div id="c_nav" class="c-nav">
        <span class="cloud"></span>
        <ul>
            <li class="current"><a href="#">首页新闻</a></li>
            <li><a href="#">师资力量</a></li>
            <li><a href="#">活动策划</a></li>
            <li><a href="#">企业文化</a></li>
            <li><a href="#">招聘信息</a></li>
            <li><a href="#">公司简介</a></li>
            <li><a href="#">我是佩奇</a></li>
            <li><a href="#">啥是佩奇</a></li>
        </ul>
    </div>
    <script>
        window.addEventListener('load', function () {
            var cloud = document.querySelector('.cloud');
            var c_nav = document.querySelector('.c-nav');
            var lis = document.querySelectorAll('li');
            var current = 0; // 筋斗云起始位置
            for (var i = 0; i < lis.length; i++) {
                lis[i].addEventListener('mouseenter', function () {
                    animate(cloud, this.offsetLeft);
                });
                lis[i].addEventListener('mouseleave', function () {
                    animate(cloud, current);
                })
                lis[i].addEventListener('click', function () {
                    current = this.offsetLeft;
                    for (var j = 0; j < lis.length; j++) {
                        lis[j].className = '';
                    }
                    this.className = 'current'; //修改点击字体颜色
                })
            }
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo22/07-%E7%AD%8B%E6%96%97%E4%BA%91%E5%AF%BC%E8%88%AA%E6%A0%8F/demo%20js%E9%83%A8%E5%88%86.html#

# 移动端网页特效

## 一、触屏事件

### 1.概述

移动端浏览器兼容性较好，可以放心地使用原生JS书写效果。但是移动端也有自己特殊的地方，比如**触屏事件（触摸事件）touch**。

touch对象代表一个触摸点。触屏事件可响应用户手指/触控笔对屏幕或触控板的操作。

常见触屏事件：

| touch事件      | 说明                            |
| -------------- | ------------------------------- |
| **touchstart** | 当手指触摸到一个DOM元素时触发   |
| **touchmove**  | 当手指在一个DOM元素上滑动时触发 |
| **touchend**   | 当手指从一个DOM元素上移开时触发 |

### 2.触摸事件对象 TouchEvent

TouchEvent是一类描述手指在触摸平面的状态变化的事件。用于描述一个或多个触点，使开发者可以检测触点的移动，触点的增加和减少等。

三个常见对象列表：

| 触摸列表          | 说明                                           |
| ----------------- | ---------------------------------------------- |
| touches           | 正在触摸屏幕的所有手指的列表                   |
| **targetTouches** | 正在触摸当前DOM元素的手指的列表                |
| changedTouches    | 手指状态发生了改变的列表（从无到有，从有到无） |

### 3.移动端拖动元素

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>移动端拖动元素</title>
    <style>
        div {
            position: absolute;
            top: 0;
            left: 0;
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div></div>
    <script>
        var div = document.querySelector('div');
        var x = 0;
        var y = 0; // 盒子坐标
        var startX = 0;
        var startY = 0; // 手指初始坐标
        div.addEventListener('touchstart', function (e) {
            // console.log(e);
            startX = e.targetTouches[0].pageX;
            startY = e.targetTouches[0].pageY;
            x = this.offsetLeft;
            y = this.offsetTop;
        })
        div.addEventListener('touchmove', function (e) {
            // console.log(e);
            var moveX = e.targetTouches[0].pageX - startX;
            var moveY = e.targetTouches[0].pageY - startY; // 手指移动距离
            // 盒子坐标 = 盒子初始坐标 + 手指移动距离
            this.style.left = x + moveX + 'px';
            this.style.top = y + moveY + 'px';
            e.preventDefault(); // 阻止屏幕滚动的默认行为
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo23/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E6%8B%96%E5%8A%A8%E5%85%83%E7%B4%A0.html

## 二、移动端常见特效

### 1.移动端轮播图

classList属性：

classList属性是HTML5新增的属性，返回元素的类名。IE10以上版本支持。

该属性用于在元素中**添加**、**移除**以及**切换CSS类**。

```js
// 添加类
element.classList.add('current');

// 移除类
element.classList.remove('current');

// 切换类（有就去掉 没有就加上）
element.classList.toggle('current');
```

```html
<!-- idnex.html -->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport"
        content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <title>携程在手，说走就走</title>
    <link rel="stylesheet" href="css/normalize.css">
    <link rel="stylesheet" href="css/index.css">
    <script src="js/index.js"></script>
</head>

<body>
    <!-- 顶部搜索模块 -->
    <div class="search-index">
        <div class="search">搜索：目的地/酒店/景点/航班号</div>
        <a href="#" class="user">
            <span>我 的</span>
        </a>
    </div>
    <!-- 焦点图 -->
    <div class="focus">
        <ul>
            <li>
                <img src="./upload/focus3.jpg" alt="">
            </li>
            <li>
                <img src="./upload/focus1.jpg" alt="">
            </li>
            <li>
                <img src="./upload/focus2.jpg" alt="">
            </li>
            <li>
                <img src="./upload/focus3.jpg" alt="">
            </li>
            <li>
                <img src="./upload/focus1.jpg" alt="">
            </li>
        </ul>
        <!-- 小圆点 -->
        <ol>
            <li class="current"></li>
            <li></li>
            <li></li>
        </ol>
    </div>
    <!-- 局部导航栏 -->
    <ul class="local-nav">
        <li>
            <a href="#">
                <span class="local-nav-icon-icon1"></span>
                <span>景点·玩乐</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="local-nav-icon-icon2"></span>
                <span>周边游</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="local-nav-icon-icon3"></span>
                <span>美食林</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="local-nav-icon-icon4"></span>
                <span>一日游</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="local-nav-icon-icon5"></span>
                <span>当地攻略</span>
            </a>
        </li>
    </ul>
    <!-- 主导航栏 -->
    <nav>
        <div class="nav-common">
            <div class="nav-items">
                <a href="#">海外酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
        </div>
        <div class="nav-common">
            <div class="nav-items">
                <a href="#">海外酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
        </div>
        <div class="nav-common">
            <div class="nav-items">
                <a href="#">海外酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
        </div>
    </nav>
    <!-- 侧导航栏 -->
    <ul class="subnav-entry">
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon1"></span>
                <span>WiFi电话卡</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon2"></span>
                <span>保险·签证</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon3"></span>
                <span>外币兑换</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon4"></span>
                <span>购物</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon5"></span>
                <span>当地向导</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon6"></span>
                <span>自由行</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon7"></span>
                <span>境外玩乐</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon8"></span>
                <span>礼品卡</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon9"></span>
                <span>信用卡</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon-icon10"></span>
                <span>更多</span>
            </a>
        </li>
    </ul>
    <!-- 销售模块 -->
    <div class="sales-box">
        <div class="sales-hd">
            <h2>热门活动</h2>
            <a href="#" class="more">获取更多福利</a>
        </div>
        <div class="sales-bd">
            <div class="row">
                <a href="#">
                    <img src="upload/pic1.jpg" alt="">
                </a>
                <a href="#">
                    <img src="upload/pic2.jpg" alt="">
                </a>
            </div>
            <div class="row">
                <a href="#">
                    <img src="upload/pic3.jpg" alt="">
                </a>
                <a href="#">
                    <img src="upload/pic4.jpg" alt="">
                </a>
            </div>
            <div class="row">
                <a href="#">
                    <img src="upload/pic5.jpg" alt="">
                </a>
                <a href="#">
                    <img src="upload/pic6.jpg" alt="">
                </a>
            </div>
        </div>
    </div>
</body>

</html>
```

```css
/* index.css */
body {
    max-width: 540px;
    min-width: 320px;
    margin: 0 auto;
    font: normal 14px/1.5 Tahoma, "Lucida Grande", Verdana, "Microsoft Yahei", STXihei, hei;
    color: #000;
    background-color: #f2f2f2;
    overflow-x: hidden;
    -webkit-tap-highlight-color: transparent;
}

a {
    color: #222;
    text-decoration: none;
}

div {
    /* css3盒子模型 */
    box-sizing: border-box;
}

ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

/* 顶部搜索模块 */
.search-index {
    position: fixed;
    top: 0;
    /*居中*/
    left: 50%;
    transform: translateX(-50%);
    -webkit-transform: translateX(-50%);
    -moz-transform: translateX(-50%);
    -ms-transform: translateX(-50%);
    -o-transform: translateX(-50%);
    display: flex;
    /*固定的盒子必须有宽度*/
    width: 100%;
    min-width: 320px;
    max-width: 540px;
    height: 44px;
    background-color: #f6f6f6;
    border-bottom: 1px solid #ccc;
}

.search {
    position: relative;
    flex: 1;
    height: 26px;
    /* css3模型计算高度包含了边框，若行高直接=26px，会导致文字偏下 */
    line-height: 24px;
    border: 1px solid #ccc;
    border-radius: 5px;
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    -ms-border-radius: 5px;
    -o-border-radius: 5px;
    margin: 7px;
    padding-left: 25px;
    font-size: 12px;
    color: #666;
}

.search::before {
    content: '';
    /* display: block; */
    position: absolute;
    top: 5px;
    left: 5px;
    width: 15px;
    height: 15px;
    background: url(../images/sprite.png) no-repeat -59px -279px;
    background-size: 104px auto;
}

.user {
    width: 44px;
    height: 44px;
    text-align: center;
    font-size: 12px;
    color: #2eaae0;
}

.user::before {
    content: '';
    display: block;
    width: 23px;
    height: 23px;
    background: url(../images/sprite.png) no-repeat -60px -195px;
    background-size: 104px auto;
    margin: 4px auto -2px;
}

/* 焦点图 */
.focus {
    position: relative;
    padding-top: 44px;
    overflow: hidden;
}

.focus img {
    width: 100%;
}

.focus ul {
    overflow: hidden;
    width: 500%;
    margin-left: -100%;
}

.focus ul li {
    float: left;
    width: 20%;
}

.focus ol {
    position: absolute;
    bottom: 5px;
    right: 5px;
    margin: 0;
}

.focus ol li {
    display: inline-block;
    width: 5px;
    height: 5px;
    background-color: #fff;
    list-style: none;
    border-radius: 2px;
    transition: all .3s;
}

.focus ol li.current {
    width: 15px;
}

/* 局部导航栏 */
.local-nav {
    display: flex;
    height: 64px;
    background-color: #fff;
    margin: 3px 4px;
    border-radius: 8px;
    -webkit-border-radius: 8px;
    -moz-border-radius: 8px;
    -ms-border-radius: 8px;
    -o-border-radius: 8px;
}

.local-nav li {
    flex: 1;
}

.local-nav li a {
    display: flex;
    flex-direction: column;
    /* 侧轴居中对齐 */
    align-items: center;
    font-size: 12px;
}

/* 利用属性选择器快速更换背景图 */
.local-nav li [class^="local-nav-icon"] {
    width: 32px;
    height: 32px;
    background: url(../images/localnav_bg.png) no-repeat 0 0;
    background-size: 32px auto;
    margin-top: 8px;
}

/* 注意权重 */
.local-nav li a .local-nav-icon-icon2 {
    background-position: 0 -32px;
}

.local-nav li a .local-nav-icon-icon3 {
    background-position: 0 -64px;
}

.local-nav li a .local-nav-icon-icon4 {
    background-position: 0 -96px;
}

.local-nav li a .local-nav-icon-icon5 {
    background-position: 0 -128px;
}

/* 主导航栏 */
nav {
    border-radius: 8px;
    -webkit-border-radius: 8px;
    -moz-border-radius: 8px;
    -ms-border-radius: 8px;
    -o-border-radius: 8px;
    margin: 0 4px 3px;
    overflow: hidden;
}

.nav-common {
    display: flex;
    height: 88px;
    background-color: pink;
}

.nav-common:nth-child(1) {
    /* 线性渐变背景颜色 */
    /* 背景渐变必须添加浏览器私有前缀 */
    background: -webkit-linear-gradient(left, #fa5a55, #FA994D);
}

.nav-common:nth-child(2) {
    margin: 3px 0;
    background: -webkit-linear-gradient(left, #4D9AF2, #53BBF2);
}

.nav-common:nth-child(3) {
    background: -webkit-linear-gradient(left, #2EBAB0, #6FCA61);
}

.nav-items {
    flex: 1;
    display: flex;
    flex-direction: column;
}

.nav-items:nth-child(-n+2) {
    border-right: 1px solid #fff;
}

.nav-items a {
    flex: 1;
    text-align: center;
    line-height: 44px;
    color: #fff;
    font-size: 14px;
    text-shadow: 1px 1px rgba(0, 0, 0, 0.1);
}

.nav-items a:nth-child(1) {
    border-bottom: 1px solid #fff;
}

/* 第一列的a不加边框 */
.nav-items:nth-child(1) a {
    border: 0;
    /* 靠底端对齐 水平居中 */
    background: url(../images/hotel.png) no-repeat bottom center;
    background-size: 121px auto;
}

/* 侧导航栏 */
.subnav-entry {
    display: flex;
    flex-wrap: wrap;
    border-radius: 8px;
    -webkit-border-radius: 8px;
    -moz-border-radius: 8px;
    -ms-border-radius: 8px;
    -o-border-radius: 8px;
    background-color: #fff;
    margin: 0 4px;
}

.subnav-entry li {
    /* 可以用%表示 相对于父亲来说 */
    flex: 20%;
}

.subnav-entry li a {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.subnav-entry li a [class^="subnav-entry-icon"] {
    width: 28px;
    height: 28px;
    margin-top: 4px;
    background: url(../images/subnav-bg.png) no-repeat 0 0;
    background-size: 28px;
}

.subnav-entry li a .subnav-entry-icon-icon2 {
    background-position: 3px -28px;
}

.subnav-entry li a .subnav-entry-icon-icon3 {
    background-position: 3px -62px;
}

.subnav-entry li a .subnav-entry-icon-icon4 {
    background-position: 2px -97px;
}

.subnav-entry li a .subnav-entry-icon-icon5 {
    background-position: 1px -127px;
}

.subnav-entry li a .subnav-entry-icon-icon6 {
    background-position: 6px -162px;
}

.subnav-entry li a .subnav-entry-icon-icon7 {
    background-position: 1px -194px;
}

.subnav-entry li a .subnav-entry-icon-icon8 {
    background-position: 1px -224px;
}

.subnav-entry li a .subnav-entry-icon-icon9 {
    background-position: 0px -254px;
}

.subnav-entry li a .subnav-entry-icon-icon10 {
    background-position: 3px -284px;
}

/* 销售模块 */
.sales-box {
    margin: 4px;
    border-top: 1px solid #ccc;
    background-color: #fff;
}

.sales-hd {
    position: relative;
    height: 44px;
    border-bottom: 1px solid #ccc;
}

.sales-hd h2 {
    position: relative;
    /* 文字不显示 */
    text-indent: -999px;
    overflow: hidden;
}

.sales-hd h2::after {
    content: '';
    position: absolute;
    top: 8px;
    left: 20px;
    display: block;
    width: 79px;
    height: 15px;
    background: url(../images/hot.png) no-repeat 0 -20px;
    background-size: 79px auto;
}

.more {
    position: absolute;
    top: 0px;
    right: 5px;
    padding: 3px 20px 3px 10px;
    background: -webkit-linear-gradient(left, #ff506c, #ff6bc6);
    border-radius: 15px;
    -webkit-border-radius: 15px;
    -moz-border-radius: 15px;
    -ms-border-radius: 15px;
    -o-border-radius: 15px;
    color: #fff;
}

.more::after {
    content: '';
    position: absolute;
    top: 9px;
    right: 9px;
    width: 7px;
    height: 7px;
    border-top: 2px solid #fff;
    border-right: 2px solid #fff;
    transform: rotate(45deg);
    -webkit-transform: rotate(45deg);
    -moz-transform: rotate(45deg);
    -ms-transform: rotate(45deg);
    -o-transform: rotate(45deg);
}

.row {
    display: flex;
}

.row a {
    flex: 1;
    border-bottom: 1px solid #ccc;
}

.row a:nth-child(1) {
    border-right: 1px solid #ccc;
}

.row a img {
    width: 100%;
}
```

```js
// idnex.js
window.addEventListener('load', function () {
    // 轮播图
    var focus = document.querySelector('.focus');
    var ul = focus.children[0];
    var ol = focus.children[1];
    var focusWidth = focus.offsetWidth;
    // 自动轮播图片
    var index = 0;
    var timer = setInterval(function () {
        index++;
        var translatex = -index * focusWidth;
        ul.style.transition = 'all .3s';
        ul.style.transform = 'translateX(' + translatex + 'px)';
    }, 3000);
    // 监听过渡完成
    ul.addEventListener('transitionend', function () {
        if (index >= 3) {
            index = 0;
            var translatex = -index * focusWidth;
            ul.style.transition = 'none';
            ul.style.transform = 'translateX(' + translatex + 'px)';
        } else if (index < 0) {
            index = 2;
            var translatex = -index * focusWidth;
            ul.style.transition = 'none';
            ul.style.transform = 'translateX(' + translatex + 'px)';
        }
        // 小圆点跟随变化
        // 将ol中li带有current类名的选出来 去掉类名
        ol.querySelector('.current').classList.remove('current');
        // 为当前索引号的li加上current类名
        ol.children[index].classList.add('current');
    });
    // 手指触摸滑动
    var startX = 0;
    var moveX = 0;
    var flag = false;
    ul.addEventListener('touchstart', function (e) {
        startX = e.targetTouches[0].pageX;
        // 停止定时器
        clearInterval(timer);
    });
    ul.addEventListener('touchmove', function (e) {
        moveX = e.targetTouches[0].pageX - startX;
        // 移动盒子：盒子原来的位置+手指移动的距离
        var translatex = -index * focusWidth + moveX;
        ul.style.transition = 'none';
        ul.style.transform = 'translateX(' + translatex + 'px';
        flag = true;
        e.preventDefault(); // 阻止滚动屏幕行为
    });
    ul.addEventListener('touchend', function (e) {
        // 用户手指移动过我们再判断 否则不做判断效果
        if (flag) {
            // 播放上一张或下一张
            if (Math.abs(moveX) > 50) {
                // 左滑 moveX为负 播放下一张
                if (moveX < 0) {
                    index++;
                }
                // 右滑 moveX为正 播放上一张
                else {
                    index--;
                }
                var translatex = -index * focusWidth;
                ul.style.transition = 'all .3s';
                ul.style.transform = 'translateX(' + translatex + 'px)';
            }
            // 回弹效果
            else {
                var translatex = -index * focusWidth;
                ul.style.transition = 'all .3s';
                ul.style.transform = 'translateX(' + translatex + 'px)';
            }
        }

        // 启动定时器
        clearInterval(timer);
        timer = setInterval(function () {
            index++;
            var translatex = -index * focusWidth;
            ul.style.transition = 'all .3s';
            ul.style.transform = 'translateX(' + translatex + 'px)';
        }, 3000);
    })
})
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/xiecheng/index.html

### 2.返回顶部

```html
<!-- index.html -->
<!-- 返回顶部模块 -->
<div class="goBack"></div>
```

```css
/* index.css */
/* 返回顶部模块 */
.goBack {
    display: none;
    position: fixed;
    bottom: 50px;
    right: 20px;
    width: 30px;
    height: 30px;
    background: url(../images/goBack.png) no-repeat;
    background-size: 30px 30px;
}
```

```js
// index.js
// 返回顶部
var goBack = document.querySelector('.goBack');
var nav = document.querySelector('nav');
var navTop = nav.offsetTop;
window.addEventListener('scroll', function (e) {
if (window.pageYOffset >= navTop) {
    goBack.style.display = 'block';
} else {
    goBack.style.display = 'none';
}
})
goBack.addEventListener('click', function () {
window.scroll(0, 0);
})
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/xiecheng/index.html

## 三、移动端常用开发插件

### 1.什么是插件

JS插件即js文件，它遵循一定规范编写，方便程序展示效果，拥有特定功能且方便调用。如轮播图和瀑布流插件。

特点：一般为了解决某个问题而专门存在，功能单一，占用空间小。

### 2.插件使用

1. 引入js文件；
2. 按照规定语法使用。

### 2.click延时解决方案

**移动端click事件会有300ms的延时**，原因是移动端屏幕双击会缩放（double tap to zoom）页面。

1. 禁用缩放：浏览器禁用默认的双击缩放行为，并且去掉300ms的点击延迟。

   ```html
   <meta name="viewport" content="user-scalable=no">
   ```

2. 利用touch事件自己封装这个事件，解决300ms延迟：

   - 当我们手指触摸屏幕时，记录当前触摸时间；
   - 当我们手指离开屏幕时，用离开时间 - 触摸时间；
   - 若时间小于150ms，并且没有滑动屏幕，那么我们就将其定义为点击。

   ```js
   function tap (obj, callback) {
   	var isMove = false;
   	var startTime = 0;	// 用于记录触摸时间
   	obj.addEventListener('touchstart', function(e) {
   		startTime = Date.now();	// 记录触摸时间
   	});
   	obj.addEventListener('touchmove', function(e) {
   		isMove = true;	// 有滑动 不判定为点击
   	});
   	obj.addEventListener('touchend', function(e) {
   		if (!isMove && (Date.now() - startTime) < 150) {
   			// 无滑动行为且停留时间小于150ms 判定为点击
   			callback && callback();
   		}
   		isMove = false;
   		startTime = 0;	// 重置
   	})
   }
   
   // 调用
   tap(div, function() {
   	// 执行代码
   });
   
   ```

3. **fastclick插件**：

   github官方地址：https://github.com/ftlabs/fastclick

### 3.swiper触摸滑动插件

中文官网地址：https://www.swiper.com.cn/

### 4.superslide网站/触屏特效插件

中文官网地址：http://www.superslide2.com/

### 5.iscorll移动端滚动插件

github官方地址：https://github.com/cubiq/iscroll

### 6.zyMedia移动端视频插件

github官方地址：https://github.com/ireaderlab/zyMedia

## 四、移动端常用开发框架

### 1.概述

框架，顾名思义即一套架构，它会基于自身的特点向用户提供**一套较为完整的解决方案**。框架的控制权在框架本身，使用者需要按照框架所规定的某种规范进行开发。

前端常用框架：**Bootstrap、Vue、Angular、React**等。既能用于开发PC端，也能开发移动端。

### 2.Bootstrap

Bootstrap是一款简洁、直观、强悍的前端开发框架，它让Web开发更迅速、简单。

#### 2.1 本地引用

将Bootstrap下载到本地文件夹后解压（解压的Bootstrap文件必须和HTML在同一目录下）。

```html
<!-- css -->
<link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
<!-- jQuery -->
<!-- 注意，所有插件都依赖 jQuery （也就是说，jQuery必须在所有插件之前引入页面）。 -->
<script src="bootstrap/js/jquery.min.js"></script>
<!-- JavaScript -->
<srcipt src="bootstrap/js/bootstrap.min.js"></srcipt>
```

#### 2.2 在线引用

```html
<!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css" integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">

<!-- 可选的 Bootstrap 主题文件（一般不用引入） -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap-theme.min.css" integrity="sha384-6pzBo3FDv/PJ8r2KRkGHifhEocL+1X2rVCTTkUfGk7/0pbek5mMa1upzvWbrUbOZ" crossorigin="anonymous">

<!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
<script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js" integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd" crossorigin="anonymous"></script>
```

基本模板：

```html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css" integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">

    <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
    <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
    <!--[if lt IE 9]>
      <script src="https://cdn.jsdelivr.net/npm/html5shiv@3.7.3/dist/html5shiv.min.js"></script>
      <script src="https://cdn.jsdelivr.net/npm/respond.js@1.4.2/dest/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>你好，世界！</h1>

    <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
    <script src="https://cdn.jsdelivr.net/npm/jquery@1.12.4/dist/jquery.min.js" integrity="sha384-nvAa0+6Qg9clwYCGGPpDQLVpLNn0fRaROjHqs13t4Ggj3Ez50XnGQqc/r8MhnRDZ" crossorigin="anonymous"></script>
    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js" integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd" crossorigin="anonymous"></script>
  </body>
</html>
```

# 本地存储

随着互联网的快速发展，基于网页的应用越来越普遍，同时也变得越来越复杂，为了满足各种各样的需求，会经常性地在本地存储大量数据。

### 1.本地存储特性

- 数据 存储在用户浏览器中；
- 设置、读取方便，页面刷新不丢失数据；
- 容量较大，**sessionStorage**约5M、**localStorage**约20M；
- 只能存储**字符串**，可以将对象JSON.stringify()编码后存储。

### 2.window.sessionStorage

- **生命周期为关闭浏览器窗口**；
- 在**同一个窗口**（页面）下数据可以共享；
- 以键值对的形式存储使用。

```js
// 存储
sessionStorage.setItem(key, value);

// 获取
sessionStorage.getItem(key);

// 删除
sessiongStorage.removeItem(key);

// 清除所有数据
sessionStorage.clear();
```

### 3.window.localStorage

- **生命周期永久生效**，除非手动删除，否则关闭页面也会存在；
- 可以**多窗口**（页面）共享（**同一浏览器**可以共享）；
- 以键值对形式存储使用。

```js
// 存储
localStorage.setItem(key, value);

// 获取
localStorage.getItem(key);

// 删除
localStorage.removeItem(key);

// 清除所有数据
localStorage.clear();
```

### 4.案例：记住用户名

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>记住用户名</title>
</head>

<body>
    <input type="text" id="username">
    <input type="checkbox" name="" id="remember">记住我
    <button>提交</button>
    <script>
        var username = document.querySelector('#username');
        var remember = document.querySelector('#remember');
        var btn = document.querySelector('button');
        btn.addEventListener('click', function () {
            if (remember.checked) {
                localStorage.setItem('username', username.value);
            }
        })
        if (localStorage.getItem('username')) {
            username.value = localStorage.getItem('username');
        }
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo24/%E8%AE%B0%E4%BD%8F%E7%94%A8%E6%88%B7%E5%90%8D.html

# jQuery入门

## 一、概述

### 1.JavaScript库

即library，是一个**封装**好的特定**的集合**（**方法和函数**）。

简单理解，就是一个JS文件，里面堆我们原生的js代码进行了封装，存放到里面。这样我们就可以快速高效地使用这些封装好的功能。

比如jQuery，就是为了快速方便地操作DOM，里面基本都是函数（方法）。

常见JavaScript库：**jQuery**、Prototype、YUI、Dojo、Ext JS、移动端的zepto。

### 2.jQuery

jQuery是一个快速、简洁的JavaScript库，其设计宗旨是"write less, do more"，提倡写更少的代码，做更多的事情。

j-JavaScript，Query-查询。意思就是将js的DOM操作做了封装，我们可以快速地查询使用里面的功能。**jQuery封装了JavaScript常用的功能代码，优化了DOM操作、事件处理、动画设计和Ajax交互。**

优点：

- 轻量级；
- 跨浏览器兼容；
- 链式编程、隐式迭代；
- 对事件、样式、动画支持，大大简化了DOM操作；
- 支持插件扩展开发，有着丰富的第三方插件，例如，树形菜单、日期控件、轮播图等；
- 免费、开源。

## 二、基本使用

### 1.下载

官方网址：https://jquery.com

### 2.使用

1. 引入

   ```html
   <!-- jQuery引用 -->
   <script src="jquery.min.js"></script>
   ```

2. 使用

### 3.jQuery入口函数

```js
// 等待页面DOM加载完毕再执行js代码
$(function() {
	...	// 此处是页面DOM加载完成的入口
})

// 或
// 等待页面DOM加载完毕再执行js代码
$(document).ready(function() {
	...	// 此处是页面DOM加载完成的入口
})
```

1. 等待DOM结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jQuery帮我们完成了封装；
2. 相当于原生js中的DOMContentLoaded。

### 4.jQuery顶级对象$

1. **$是jQuery的别称**，在代码中可以使用jQuery代替$。但一般为了方便，通常都直接使用$。

2. $是jQuery的顶级对象，相当于原生JavaScript中的window。把元素利用$包装成jQuery对象，就可以调用jQuery方法。

   ```js
   $('div').hide();
   ```

### 5.jQuery对象和DOM对象

1. 用原生JS获取来的对象就是DOM对象；

   ```js
   var myDiv = document.querySelector('div');
   console.dir(myDiv);
   ```

2. 通过jQuery方式获取来的对象就是jQuery对象；

   ```js
   $('div');
   console.dir('div');
   ```

3. jQuery对象只能使用jQuery方法，DOM对象则使用原生的JavaScript属性和方法。

4. DOM对象与jQuery对象**相互转换**：

   由于原生js比jQuery更大，原生的一些属性和方法jQuery没有给我们封装，因此我们要想使用这些属性和方法需要将jQuery对象转换为DOM对象才行。

   - DOM对象转jQuery对象

     ```js
     $(DOM对象)；
     ```

     ```js
     // 1. 直接通过$获取
     $('video');
     
     // 2. 已经使用原生js获取DOM对象 转换为jQuery对象
     var myvideo = document.querySelector('video');
     $(myvideo);
     ```

   - jQuery对象转DOM对象

     ```js
     $('div')[index];	// index为索引号
     $('div').get(index);	// index为索引号
     ```

     ```
     $('video')[0].play();
     $('video').get(0).play();
     ```

# jQuery常用API

## 一、jQuery选择器

### 1.jQuery基础选择器

```js
$("选择器")	// 里面选择器直接写CSS选择器即可 但是要加引号
```

| 名称       | 用法            | 描述                     |
| ---------- | --------------- | ------------------------ |
| ID选择器   | $("#id")        | 获取指定ID的元素         |
| 全选选择器 | $("*")          | 匹配所有元素             |
| 类选择器   | $(".class")     | 获取同一类class的元素    |
| 标签选择器 | $("div")        | 获取同一类标签的所有元素 |
| 并集选择器 | $("div,p,li")   | 选取多个元素             |
| 交集选择器 | $("li.current") | 交集元素                 |

### 2.jQuery层级选择器

| 名称       | 用法       | 描述                                         |
| ---------- | ---------- | -------------------------------------------- |
| 子代选择器 | $("ul>li") | 获取亲儿子层级的元素，不会获取孙子层级的元素 |
| 后代选择器 | $("ul li") | 获取ul下的所有li元素，包括孙子等             |

### 3.隐式迭代

遍历内部DOM元素（伪数组形式存储）的过程就叫做**隐式迭代**。

即，给匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环。这简化了我们的操作，方便我们调用。

```html
<div>1</div>
<div>2</div>
<div>3</div>
<script>
	// 将3个div的背景颜色都改为粉色
    $("div").css("background", "pink");
</script>
```

### 4.jQuery筛选选择器

| 语法       | 用法          | 描述                                                   |
| ---------- | ------------- | ------------------------------------------------------ |
| :first     | $('li:first') | 获取第一个li元素                                       |
| :last      | $('li:last')  | 获取最后一个li元素                                     |
| :eq(index) | $(li:eq(2))   | 获取到的li元素中，选择索引号为2的元素（索引号从0开始） |
| :odd       | $('li:odd')   | 获取到的li元素中，选择索引号为奇数的元素               |
| :even      | $('li:even')  | 获取到的li元素中，选择索引号为偶数的元素               |

### 5.jQuery筛选方法

| 语法                | 用法                            | 说明                                                   |
| ------------------- | ------------------------------- | ------------------------------------------------------ |
| parent()            | $("li").parent();               | 查找父级                                               |
| parents('selector') | $('.four').parents('.one');     | 查找指定祖先                                           |
| children(selector)  | $("ul").children('li');         | 相当于$("ul>li")，查找亲儿子                           |
| find(selector)      | $("ul").find("li");             | 相当于$("ul li")，查找后代                             |
| siblings(selector)  | $(".first").siblings("li");     | 查找兄弟节点，**不包括自己本身**                       |
| nextAll([expr])     | $(".first").nextAll();          | 查找当前元素之后所有的同辈元素                         |
| prevAll([expr])     | $(".last").prevAll();           | 查找当前元素之前所有的同辈元素                         |
| hasClass(class)     | $("div").hasClass("protected"); | 检查当前的元素是否含有某个特定的类，如果有，则返回true |
| eq(index)           | $("li").eq(2);                  | 相当于$("li:eq(2)")                                    |

#### 5.1 案例：新浪下拉菜单

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>新浪下拉菜单</title>
    <!-- jQuery引用 -->
    <script src="jquery.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        ul {
            list-style: none;
        }

        a {
            text-decoration: none;
            color: #333;
        }

        .nav {
            margin: 100px;
        }

        .nav>li {
            float: left;
            width: 80px;
            height: 41px;
            line-height: 41px;
            text-align: center;
        }

        .nav>li>a {
            display: block;
            width: 100%;
            height: 100%;
            color: #333;
        }

        .nav>li>a:hover {
            background-color: #eee;
        }

        .nav li ul {
            display: none;
            font-size: 14px;
            border-left: 1px solid #FECC5B;
            border-right: 1px solid #FECC5B;
        }

        .nav li ul li {
            border-bottom: 1px solid #FECC5B;
        }
    </style>
</head>

<body>
    <ul class="nav">
        <li>
            <a href="#">微博</a>
            <ul>
                <li>私信</li>
                <li>评论</li>
                <li>@我</li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>私信</li>
                <li>评论</li>
                <li>@我</li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>私信</li>
                <li>评论</li>
                <li>@我</li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>私信</li>
                <li>评论</li>
                <li>@我</li>
            </ul>
        </li>
    </ul>
    <script>
        $(function () {
            $(".nav>li").mouseover(function () {
                // $(this) jQuery 当前元素 this不用加引号
                $(this).children("ul").show();
            });
            $(".nav>li").mouseout(function () {
                $(this).children("ul").hide();
            });
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/%E6%96%B0%E6%B5%AA%E4%B8%8B%E6%8B%89%E8%8F%9C%E5%8D%95.html

### 6.jQuery排他思想

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>jQuery排他思想</title>
    <!-- jQuery引用 -->
    <script src="jquery.min.js"></script>
    <style>
        button {
            outline: none;
        }
    </style>
</head>

<body>
    <button>点击</button>
    <button>点击</button>
    <button>点击</button>
    <button>点击</button>
    <button>点击</button>
    <button>点击</button>
    <button>点击</button>
    <button>点击</button>
    <script>
        $(function () {
        	// 隐式迭代
            $('button').click(function () {
                // 当前元素变化背景颜色
                $(this).css('background', 'pink');
                // 其余兄弟去掉背景颜色
                $(this).siblings('button').css('background', '');
            })
        })
    </script>
</body>

</html>
```

#### 6.1 案例：淘宝服饰精品案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>淘宝服饰精品案例</title>
    <script src="jquery.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        ul {
            list-style: none;
        }

        a {
            text-decoration: none;
            color: #333;
        }

        .wrapper {
            width: 250px;
            height: 248px;
            margin: 100px auto 0;
            border: 1px solid pink;
            border-right: 0;
            overflow: hidden;
        }

        #left,
        #content {
            float: left;
        }

        #left li {
            background: url(images/lili.jpg) repeat-x;
        }

        #left li a {
            display: block;
            width: 48px;
            height: 27px;
            border-bottom: 1px solid pink;
            line-height: 27px;
            text-align: center;
            color: black;
        }

        #left li a:hover {
            background: url(images/abg.gif) repeat-x;
        }

        #content {
            border-left: 1px solid pink;
            border-right: 1px solid pink;
        }
    </style>
</head>

<body>
    <div class="wrapper">
        <ul id="left">
            <li><a href="#">女靴</a></li>
            <li><a href="#">雪地靴</a></li>
            <li><a href="#">冬裙</a></li>
            <li><a href="#">呢大衣</a></li>
            <li><a href="#">毛衣</a></li>
            <li><a href="#">棉服</a></li>
            <li><a href="#">女裤</a></li>
            <li><a href="#">羽绒服</a></li>
            <li><a href="#">牛仔裤</a></li>
        </ul>
        <div id="content">
            <div><a href="#"><img src="./images/女靴.jpg" alt=""></a></div>
            <div><a href="#"><img src="./images/雪地靴.jpg" alt=""></a></div>
            <div><a href="#"><img src="./images/冬裙.jpg" alt=""></a></div>
            <div><a href="#"><img src="./images/呢大衣.jpg" alt=""></a></div>
            <div><a href="#"><img src="./images/毛衣.jpg" alt=""></a></div>
            <div><a href="#"><img src="./images/棉服.jpg" alt=""></a></div>
            <div><a href="#"><img src="./images/女裤.jpg" alt=""></a></div>
            <div><a href="#"><img src="./images/羽绒服.jpg" alt=""></a></div>
            <div><a href="#"><img src="./images/牛仔裤.jpg" alt=""></a></div>
        </div>
    </div>
    <script>
        $(function () {
            $('#left li').mouseover(function () {
                // 获取鼠标经过的小li的索引号
                var index = $(this).index();
                // console.log(index);
                // 隐藏其他兄弟 让索引图片显示
                $('#content div').eq(index).show();
                $('#content div').eq(index).siblings().hide();
                // 链式编程
                // $('#content div').eq(index).show().siblings().hide();
            })
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/%E6%B7%98%E5%AE%9D%E6%9C%8D%E9%A5%B0%E7%B2%BE%E5%93%81%E6%A1%88%E4%BE%8B.html#

## 二、jQuery样式操作

### 1.操作CSS方法

jQuery可以使用CSS方法来修改简单的元素样式，也可以操作类，修改多个样式。

1. 返回属性值

   ```js
   $(this).css('color');
   ```

2. 修改单一属性值

   ```js
   $(this).css('color', 'red');
   $('div').css('width', '300px');
   $('div').css('width', 300);	// 值是数字可以不跟单位和引号
   ```

3. 以对象的形式设置多组样式

   ```js
   $(this).css({'color':'white','font-size':'20px'});
   
   $('div').css({
       width: 400,
       height: 400,
       backgroundColor: 'red'	// 复合属性采取驼峰命名法
   });	// 采取对象形式时 属性名可以不加引号
   ```

### 2.设置类样式方法

作用等同于以前的classList，可以 类样式。

1. 添加类

   ```js
   $('div').addClass('current');
   ```

2. 删除类

   ```js
   $('div').removeClass('current');
   ```

3. 切换类

   ```js
   $('div').toggleClass('current');	// 存在则取消 不存在则添加
   ```

#### 2.1 案例：tab栏切换

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>tab栏切换布局分析</title>
    <script src="jquery.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        li {
            list-style: none;
        }

        .tab {
            width: 978px;
            margin: 100px auto;
        }

        .tab_list {
            height: 39px;
            border: 1px solid #ccc;
            background-color: #f1f1f1;
        }

        .tab_list li {
            float: left;
            height: 39px;
            line-height: 39px;
            padding: 0 20px;
        }

        /* 被选中的tab栏 */
        .tab_list .current {
            background-color: #c81623;
            color: #fff;
        }

        .item {
            display: none;
        }
    </style>
</head>

<body>
    <div class="tab">
        <div class="tab_list">
            <ul>
                <li class="current">商品介绍</li>
                <li>规格与包装</li>
                <li>售后保障</li>
                <li>商品评价</li>
                <li>手机社区</li>
            </ul>
        </div>
        <div class="tab_con">
            <div class="item" style="display:block">商品介绍模块内容</div>
            <div class="item">规格与包装模块内容</div>
            <div class="item">售后保障模块内容</div>
            <div class="item">商品评价模块内容</div>
            <div class="item">手机社区模块内容</div>
        </div>
    </div>
    <script>
        $('.tab_list li').click(function () {
            $(this).addClass('current').siblings().removeClass('current');
            // console.log($(this).index());
            var index = $(this).index();
            // $('.tab_con .item').eq(index).css('display', 'block').siblings().css('display', 'none');
            $('.tab_con .item').eq(index).show().siblings().hide();
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/tab%E6%A0%8F%E5%88%87%E6%8D%A2.html

#### 2.2 案例：购物车选中商品添加背景颜色

```js
// 全选
$('.checkall').change(function () {
    // console.log($(this).prop('checked'));
    $('.j-checkbox').prop('checked', $(this).prop('checked'));

    // 选中商品添加背景
    if ($(this).prop('checked')) {
        // 为所有购物车商品添加背景
        $('.cart-item').addClass('check-cart-item');
    } else {
        $('.cart-item').removeClass('check-cart-item');
    }

    getSum();
})
$('.j-checkbox').change(function () {
    // 复选框个数
    // console.log($('.j-checkbox').length);
    // 被选中的复选框个数
    // console.log($('.j-checkbox:checked').length);

    if ($('.j-checkbox:checked').length === $('.j-checkbox').length) {
        $('.checkall').prop('checked', true);
    } else {
        $('.checkall').prop('checked', false);
    }

    // 选中商品添加背景
    if ($(this).prop('checked')) {
        // 为当前选中的购物车商品添加背景
        $(this).parents('.cart-item').addClass('check-cart-item');
    } else {
        $(this).parents('.cart-item').removeClass('check-cart-item');
    }

    getSum();

})
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/02-%E8%B4%AD%E7%89%A9%E8%BD%A6/index.html

## 三、jQuery效果

jQuery为我们封装了许多动画效果，常见如下：

1. 显示隐藏：**show()**、**hide()**、toggle()
2. 滑动：slideDown()、slideUp()、slideToggle()
3. 淡入淡出：fadeIn()、fadeOut()、fadeToggle()、fadeTo()
4. 自定义动画：animate()

### 1.显示隐藏效果

1. 显示

   ```js
   show([speed,[easing],[fn]]);
   ```

   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

2. 隐藏

   ```
   hide([speed,[easing],[fn]]);
   ```

   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

3. 切换

   ```
   toggle([speed,[easing],[fn]]);
   ```

   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

### 2.滑动效果

1. 下拉滑动

   ```
   slideDown([speed,[easing],[fn]]);
   ```

   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

2. 上拉滑动

   ```
   slideUp([speed,[easing],[fn]]);
   ```

   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

3. 滑动切换

   ```
   slideToggle([speed,[easing],[fn]]);
   ```

   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

### 3.事件切换

```
hover([over,]out);
```

- over：鼠标移动到元素上时触发的函数（相当于mouseenter）；
- out：鼠标溢出元素时要触发的函数（相当于mouseleave）。

```js
$('.nav>li').hover(function () {
    $(this).children('ul').slideDown(200);
}, function () {
    $(this).children('ul').slideUp(200);
})
```

- 若只写一个函数，那么鼠标在经过及离开的时候都会触发这个函数。

```js
$('.nav>li').hover(function () {
    $(this).children('ul').slideToggle(200);
})
```

### 4.动画队列

1. 动画或效果队列

   动画或者效果一旦触发就会执行，若多次触发，就会造成多个动画或效果排队执行。

2. 停止排队

   ```js
   stop();
   ```

   - stop()方法用于停止动画或效果；
   - 注意：**stop()写到动画或者效果的前面，相当于停止结束上一次的动画。**

### 5.淡入淡出效果

1. 淡入效果

   ```
   fadeIn([speed,[easing],[fn]]);
   ```

   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

2. 淡出效果

   ```
   fadeOut([speed,[easing],[fn]]);
   ```

   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

3. 淡入淡出切换

   ```
   fadeToggle([speed,[easing],[fn]]);
   ```

   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

4. 调整透明度

   ```
   fadeTo(speed,opacity,[easing],[fn]);
   ```

   - opacity：透明度，必须写，0~1之间（必写）；
   - speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）（必写）；
   - easing：用来指定切换效果，默认为'swing'，可用参数'linear'；
   - fn：回调函数，在动画完成时执行函数，每个元素执行一次。

#### 5.1 案例：突出显示

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>突出显示</title>
    <script src="jquery.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        body {
            background-color: black;
        }

        ul {
            list-style: none;
        }

        .wrap {
            width: 630px;
            height: 394px;
            background-color: black;
            padding: 10px 0 0 10px;
            border: 1px solid #fff;
            margin: 100px auto;
        }

        .wrap ul li {
            float: left;
            margin: 0 10px 10px 0;
        }

        .wrap li a {
            display: block;
            width: 100%;
        }
    </style>
</head>

<body>
    <div class="wrap">
        <ul>
            <li><a href="#"><img src="images/01.jpg" alt=""></a></li>
            <li><a href="#"><img src="images/02.jpg" alt=""></a></li>
            <li><a href="#"><img src="images/03.jpg" alt=""></a></li>
            <li><a href="#"><img src="images/04.jpg" alt=""></a></li>
            <li><a href="#"><img src="images/05.jpg" alt=""></a></li>
            <li><a href="#"><img src="images/06.jpg" alt=""></a></li>
        </ul>
    </div>
    <script>
        $('.wrap li').hover(function () {
            $(this).siblings().stop().fadeTo(400, 0.5);
        }, function () {
            $(this).siblings().stop().fadeTo(400, 1);
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/%E7%AA%81%E5%87%BA%E6%98%BE%E7%A4%BA.html#

### 6.自定义动画 animate

```
animate(params,[speed],[easing],[fn]);
```

- paramas：想要更改的样式属性，以对象形式传递，必写。属性名可以不用带引号，如果是复合属性则需要采取驼峰命名法。其余参数都可以省略；
- speed：三种预定速度之一的字符串（'slow', 'normal', 'fast'）或表示动画时长的毫秒数值（如：1000）（必写）；
- easing：用来指定切换效果，默认为**'swing'（在开头/结尾移动慢，在中间移动快）**，可用参数**'linear'（匀速移动）**；
- fn：回调函数，在动画完成时执行函数，每个元素执行一次。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>自定义动画</title>
    <script src="jquery.min.js"></script>
    <style>
        div {
            position: absolute;
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <button>动起来</button>
    <div></div>
    <script>
        $(function () {
            $('button').click(function () {
                $('div').animate({
                    left: 500
                }, 1000, 'linear')
            })
        })
    </script>
</body>

</html>
```

#### 6.1 案例：王者荣耀手风琴案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>王者荣耀手风琴</title>
    <script src="jquery.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        a {
            text-decoration: none;
        }

        ul {
            list-style: none;
        }

        .king {
            width: 852px;
            margin: 100px auto;
            background: url(images/bg.png) no-repeat;
            /* overflow: hidden; */
            padding: 10px;
        }

        .king ul {
            overflow: hidden;
        }

        .king li {
            position: relative;
            float: left;
            width: 69px;
            height: 69px;
            margin-right: 10px;
        }

        .king .current {
            width: 224px;
        }

        .king img {
            display: block;
        }

        .king .big {
            display: none;
            width: 224px;
        }

        .king .small {
            position: absolute;
            top: 0;
            left: 0;
            width: 69px;
            height: 69px;
            border-radius: 5px;
        }

        .king .current .small {
            display: none;
        }

        .king .current .big {
            display: block;
        }
    </style>
</head>

<body>
    <div class="king">
        <ul>
            <li class="current">
                <a href="#">
                    <img src="images/m1.jpg" alt="" class="small">
                    <img src="images/m.png" alt="" class="big">
                </a>
            </li>
            <li>
                <a href="#">
                    <img src="images/l1.jpg" alt="" class="small">
                    <img src="images/l.png" alt="" class="big">
                </a>
            </li>
            <li>
                <a href="#">
                    <img src="images/c1.jpg" alt="" class="small">
                    <img src="images/c.png" alt="" class="big">
                </a>
            </li>
            <li>
                <a href="#">
                    <img src="images/w1.jpg" alt="" class="small">
                    <img src="images/w.png" alt="" class="big">
                </a>
            </li>
            <li>
                <a href="#">
                    <img src="images/z1.jpg" alt="" class="small">
                    <img src="images/z.png" alt="" class="big">
                </a>
            </li>
            <li>
                <a href="#">
                    <img src="images/h1.jpg" alt="" class="small">
                    <img src="images/h.png" alt="" class="big">
                </a>
            </li>
            <li>
                <a href="#">
                    <img src="images/t1.jpg" alt="" class="small">
                    <img src="images/t.png" alt="" class="big">
                </a>
            </li>
        </ul>
    </div>
    <script>
        $(function () {
            $('.king li').mouseenter(function () {
                // 当前li 宽度变为224px 小图片淡出 大图片淡入
                $(this).stop().animate({
                    width: 224
                }).find('.small').stop().fadeOut().siblings('.big').stop().fadeIn();
                // 当前li的兄弟 宽度变为96px 小图片淡入 大图片淡出
                $(this).siblings().stop().animate({
                    width: 69
                }).find('.small').stop().fadeIn().siblings('.big').stop().fadeOut();
            })
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/%E7%8E%8B%E8%80%85%E8%8D%A3%E8%80%80%E6%89%8B%E9%A3%8E%E7%90%B4.html

## 四、jQuery属性操作

### 1.设置或获取元素固有属性值 prop()

所谓元素固有属性就是元素本身自带的属性，比如<a>元素里面的href，比如<input>元素里面的type。

```js
// 获取属性
prop('属性')

// 设置属性
prop('属性', '属性值')
```

#### 1.1 案例：购物车全选

```js
// 全选
$('.checkall').change(function () {
    // console.log($(this).prop('checked'));
    $('.j-checkbox').prop('checked', $(this).prop('checked'));
})
$('.j-checkbox').change(function () {
    // 复选框个数
    // console.log($('.j-checkbox').length);
    // 被选中的复选框个数
    // console.log($('.j-checkbox:checked').length);

    if ($('.j-checkbox:checked').length === $('.j-checkbox').length) {
        $('.checkall').prop('checked', true);
    } else {
        $('.checkall').prop('checked', false);
    }
})
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/02-%E8%B4%AD%E7%89%A9%E8%BD%A6/index.html

### 2.设置或获取元素自定义属性值 attr()

```js
// 获取属性（类似于原生getAttribute()）
attr('属性')

// 设置属性（类似于原生setAttribute()）
attr('属性', '属性值')
```

### 3.数据缓存 data()

data()方法可以在指定的元素上存取数据，并不会修改DOM元素结构。**一旦页面刷新，之前存放的数据都将被移除。**

```js
// 附加数据
data('name', 'value')

// 获取数据
data('name')
```

```js
$('span').data('uname', 'andy');	// 数据存放在元素的内存里面

// 获取H5自定义属性
// <div data-index='2'></div>
console.log($('div').data('index'));
```

## 五、jQuery内容文本值

### 1.普通元素内容 html()

相当于原生的**innerHTML**。

```js
// 获取元素内容
html()

// 设置元素内容
html('内容')
```

### 2.普通元素文本内容 text()

相当于原生的**innerText**，只获取文字，忽略其中的标签。

```js
// 获取元素的文本内容
text()

// 设置元素的文本内容
text('文本内容')
```

### 3.表单的值 val()

相当于原生的**value**。

```js
// 获取表单的值
val()

// 设置表单的值
val('内容')
```

#### 3.1 案例：购物车增减商品数量及修改商品小计

```js
// 增减商品数量
// +
$('.increment').click(function () {
    // 当前商品已选择的数量
    var num = $(this).siblings('.itxt').val();
    num++;
    // 赋值给文本框
    $(this).siblings('.itxt').val(num);

    // 修改商品小计
    var price = $(this).parents('.p-num').siblings('.p-price').text().substr(1); // 单价 去掉开头的￥符号
    var totalPrice = (price * num).toFixed(2); // 总价  // toFixed(2) 保留2位小数
    $(this).parents('.p-num').siblings('.p-sum').text('￥' + totalPrice);
})
// -
$('.decrement').click(function () {
    var num = $(this).siblings('.itxt').val();
    if (num == 1) {
        return false; // 后面代码不必再执行
    }
    num--;
    $(this).siblings('.itxt').val(num);

    var price = $(this).parents('.p-num').siblings('.p-price').text().substr(1);
    var totalPrice = (price * num).toFixed(2);
    $(this).parents('.p-num').siblings('.p-sum').text('￥' + totalPrice);
})
// 用户直接修改文本框的值
$('.itxt').change(function () {
    var num = $(this).val();
    num = positiveInteger(num); // 限制输入为正整数
    // 修改文本框
    $(this).val(num);
    var price = $(this).parents('.p-num').siblings('.p-price').text().substr(1);
    var totalPrice = (price * num).toFixed(2);
    // 修改小计
    $(this).parents('.p-num').siblings('.p-sum').text('￥' + totalPrice);

})

// 正整数
function positiveInteger(value) {
    value = value.replace(/[^\d]/g, '');
    if ('' != value) {
        value = parseInt(value);
    }
    return value;
}
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/02-%E8%B4%AD%E7%89%A9%E8%BD%A6/index.html

## 六、jQuery元素操作

### 1.遍历元素

jQuery隐式迭代是对同一类元素做同样的操作，若我们需要给同一类元素做不同的操作，就需要用到**遍历**。

1. 语法1：

   ```js
   $('div').each(function(index, domEle) {
   	...;
   })
   ```

   - each()方法遍历匹配的每一个元素，用于**遍历DOM对象**；
   - index：元素的索引号；
   - domEle：每个**DOM元素对象**。

   ```js
   $(function() {
   	var arr = ['red', 'green', 'blue'];
   	$('div').each(function(index, domEle) {
   		$(domEle).css('color', arr[index]);
   	})
   })
   ```

2. 语法2：

   ```js
   $.each(object, function (index, element) {
   	...;
   })
   ```

   - $.each()方法可用于遍历任何对象。主要**用于数据处理**，如数组、对象；
   - index：元素的索引号；
   - element：遍历内容。

   ```js
   $(function() {
   	var arr = ['red', 'green', 'blue'];
   	$.each(arr, function(i, ele) {
   		console.log(i);
   		console.log(ele);
   	})
   })
   ```

#### 1.1 案例：购物车计算总件数和总额

```js
// 计算总件数和总额
function getSum() {
    var count = 0; // 总件数
    var money = 0;
    // 遍历所有被勾选的商品条目
    $('.j-checkbox:checked').each(function (index, domEle) {
        count += parseInt($(this).parent().siblings().find('.itxt').val());
        money += parseFloat($(this).parent().siblings('.p-sum').text().substr(1));
    })
    var totalMoney = money.toFixed(2); // 总额
    // 修改勾选件数
    $('.amount-sum em').text(count);
    // 修改勾选总额
    $('.price-sum em').text('￥' + totalMoney);
}
```

### 2.创建元素

```js
$('<li></li>');

var li = $('<li></li>');
```

### 3.添加元素

1. 内部添加（父子）

   ```js
   element.append('内容');
   ```

   把内容放到匹配元素内部的最后面，类似原生中的appendChild。

2. 外部添加（兄弟）

   ```js
   element.after('内容');	// 把内容放到目标元素后
   element.before('内容');	// 把内容放到目标元素前
   ```

### 4.删除元素

```js
element.remove();	// 删除匹配的元素（本身）
element.empty();	// 删除匹配的元素里面的子节点
element.html('');	// 清空匹配元素的内容
```

#### 4.1 案例：购物车删除商品

```js
// 删除商品
$('.p-action a').click(function () {
    $(this).parents('.cart-item').remove();
    getSum();
})
// 删除选中商品
$('.remove-batch').click(function () {
    $('.j-checkbox:checked').parents('.cart-item').remove();
    getSum();

})
// 清理购物车
$('.clear-all').click(function () {
    $('.cart-item').remove();
    getSum();

})
```

## 七、jQuery尺寸、位置操作

### 1.jQuery尺寸

| 方法                                 | 说明                                                  |
| ------------------------------------ | ----------------------------------------------------- |
| width() / height()                   | 取得匹配元素宽度和高度值，只算width / height          |
| innerWidth() / innerHeight()         | 取得匹配元素宽度和高度值，包含padding                 |
| outerWidth() / outerHeight()         | 取得匹配元素宽度和高度值，包含padding、border         |
| outerWidth(true) / outerHeight(true) | 取得匹配元素宽度和高度值，包含padding、border、margin |

- 参数为空：获取相应值，返回的是数字型；
- 参数为数字：修改相应值；
- **参数可以不必填写单位**。

### 2.jQuery位置

1. offset() 设置或获取元素偏移

   offset()方法设置或返回被选中元素相**对于文档的偏移坐标**，跟父级没关系。

   ```js
   console.log($('div').offset());
   console.log($('div').offset().top);	// 获取距离文档顶部的距离
   console.log($('div').offset().left);	// 获取距离文档左侧的距离
   
   // 修改
   $('div').offset({
       top: 200,
       left: 200
   });
   ```

2. position() 获取元素偏移

   position()方法用于返回被选元素**相对于带有定位的父级偏移坐标**，如果父级都没有定位，则以文档为准。

   只能用于获取，不能设置。

   ```js
   console.log($('div').position());
   ```

3. scrollTop / scrollLeft() 设置或获取元素被卷去的头部和左侧

   scrollTop()方法设置或返回被选元素**被卷去的头部**；

   scrollLeft()方法设置或返回被选元素**被卷去的左侧**。

   ```js
   // 页面滚动事件
   $(window).scroll(function() {
       console.log($(document).scrollTop());	// 获取页面被卷去头部
   })
   
   // 返回顶部
   $(document).scrollTop(0);
   ```

#### 2.1 案例：jQuery返回顶部

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>返回顶部</title>
    <script src="jquery.min.js"></script>
    <style>
        .w {
            width: 1200px;
            margin: 10px auto;
        }

        .slider-bar {
            position: absolute;
            top: 300px;
            left: 50%;
            margin-left: 600px;
            width: 45px;
            height: 130px;
            background-color: pink;

        }

        span {
            position: absolute;
            bottom: 0;
            display: none;
            cursor: pointer;
        }

        .header {
            height: 150px;
            background-color: skyblue;
        }

        .banner {
            height: 250px;
            background-color: steelblue;
        }

        .main {
            height: 1000px;
            background-color: teal;
        }
    </style>
</head>

<body>
    <div class="slider-bar">
        <span class="goBack">返回顶部</span>
    </div>
    <div class="header w">头部区域</div>
    <div class="banner w">banner区域</div>
    <div class="main w">主体区域</div>
    <script>
        $(function () {
            var bannerTop = $('.banner').offset().top;
            var mainTop = $('.main').offset().top;
            var sliderBarTop = $('.slider-bar').offset().top - bannerTop;
            $(window).scroll(function () {
                // console.log($(document).scrollTop());
                if ($(document).scrollTop() >= bannerTop) {
                    $('.slider-bar').css({
                        position: 'fixed',
                        top: sliderBarTop
                    });
                } else {
                    $('.slider-bar').css({
                        position: 'absolute',
                        top: 300
                    });
                }
                if ($(document).scrollTop() >= mainTop) {
                    $('.goBack').fadeIn();
                } else {
                    $('.goBack').fadeOut();
                }
            })
            // 返回顶部
            $('.goBack').click(function () {
                // 使用animate动画返回顶部
                // animate动画函数scrollTop属性
                $('body,html').animate({	// 元素做动画
                    scrollTop: 0
                });
            })
        })
    </script>
</body>

</html>
```

#### 2.2 案例：品优购电梯导航

```css
.fixedtool {
    display: none;
    position: fixed;
    top: 100px;
    left: 50%;
    margin-left: -676px;
    width: 66px;
    background-color: #fff;
}

.fixedtool li {
    height: 32px;
    line-height: 32px;
    text-align: center;
    font-size: 12px;
    border-bottom: 1px solid #ccc;
    cursor: pointer;
}

.fixedtool .current {
    background-color: #c81623;
    color: #fff;
}
```

```html
<!-- 左侧电梯导航 -->
<div class="fixedtool">
    <ul>
        <li class="current">家用电器</li>
        <li>手机通讯</li>
        <li>电脑办公</li>
        <li>精品家具</li>
    </ul>
</div>
```

```js
$(function () {
    var recomTop = $('.recom').offset().top;
    var flag = true; // 节流阀
    $(window).scroll(function () {
        toggleTool();

        // 页面滚动自动修改左侧导航栏选中（current）
        // each遍历floor区大模块，拿到每个模块元素和索引号
        // 判断条件：被卷去的头部大于等于内容区域每个模块的offset().top
        if (flag) {
            $('.floor .w').each(function (i, ele) {
                if ($(document).scrollTop() >= $(ele).offset().top) {
                    // 利用索引号找到相应的电梯导航li 为其添加current类
                    $('.fixedtool li').eq(i).addClass('current').siblings().removeClass('current');
                }
            })
        }

    })

    $('.fixedtool li').click(function () {
        // 修改背景色
        $(this).addClass('current').siblings().removeClass('current');
        // console.log($(this).index());
        var index = $(this).index();
        var current = $('.floor .w').eq(index).offset().top;
        // 页面动画滚动效果
        $('body,html').stop().animate({
            scrollTop: current
        }, function () {
            flag = true;
        })

        // 当我们点击小li 不需要执行滚动事件中添加类current的操作
        flag = false;
    })

    function toggleTool() {
        if ($(document).scrollTop() >= recomTop) {
            $('.fixedtool').fadeIn();
        } else {
            $('.fixedtool').fadeOut();
        }
    }
})
```

# jQuery事件

## 一、jQuery事件注册

```js
element.事件(function() {
	...
});

$('div').click(function() {
	// 事件处理程序
})
```

## 二、jQuery事件处理

### 1.on()

#### 1.1 绑定事件

on()方法在匹配元素上**绑定一个或多个事件**的事件处理函数。

```js
element.on(event,[selector],fn);

$('div').on({
    mouseenter: function() {
        $(this).css('background', 'skyblue');
    },
    click: function() {
        $(this).css('background', 'purple');
    },
    mouseleave: function() {
    	$(this).css('background', 'blue');
	}
})

$('div').on('mouseenter mouseleave', function() {
    $(this).toggleClass('current');
})
```

- events：一个或多个用空格分隔的事件类型，如"click"或"keydown"；
- selector：元素的子元素选择器。

#### 1.2 实现事件委派操作

事件委派：把原来加给子元素身上的事件绑定到父元素身上，就是把事件委派给父元素。

```js
$('ul').on('click', 'li', function() {
	alert('helo world');
})	// click绑定在ul身上，但触发对象是ul中的li
```

在此之前有bind()、live()、delegate()等方法来处理事件绑定或委派事件，新版本请用on替代他们。

#### 1.3 为动态创建的元素绑定事件

```js
$('ol').on('click', 'li', function() {
	alert('hello world');
})	// on可以给未来动态创建的元素绑定事件
var li = '<li></li>';
$('ol').append(li);
```

#### 1.4 案例：微博发布

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>微博发布</title>
    <script src="jquery.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        ul {
            list-style: none;
        }

        a {
            text-decoration: none;
        }

        .box {
            width: 600px;
            /* height: 200px; */
            margin: 100px auto;
            border: 1px solid #000;
            padding: 20px;
            /* text-align: center; */
        }

        .box .txt {
            width: 400px;
            outline: none;
        }

        .box ul li {
            border-bottom: 1px dashed blue;
            display: none;
        }

        .box li a {
            float: right;
        }
    </style>
</head>

<body>
    <div class="box" id="weibo">
        <span>微博发布</span>
        <textarea name="" class="txt" id="" cols="30" rows="10"></textarea>
        <button class="btn">发布</button>
        <ul></ul>
    </div>
    <script>
        $(function () {
            // 发布
            $('.btn').on('click', function () {
                if ($('.txt').val()) {
                    var li = $('<li></li>');
                    li.html($('.txt').val() + "<a href='javascript:;'>删除</a>");
                    $('.txt').val('');
                    $('ul').prepend(li);
                    li.stop().slideDown();
                }
            });

            // 删除
            $('ul').on('click', 'a', function () {
                $(this).parent('li').stop().slideUp(function () {
                    $(this).remove();
                });
            })
        })
    </script>
</body>

</html>
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/%E5%BE%AE%E5%8D%9A%E5%8F%91%E5%B8%83.html

### 2.off()

#### 2.1 解绑事件

off()方法可以移除通过on()方法添加的事件处理程序。

```js
$('div').off();	// 解除div身上的所有事件
$('div').off('click');	// 解除div身上绑定的点击事件
$('ul').off('click', 'li');	// 解绑事件委托
```

### 3.one()

如果有的**事件只**想**触发一次**，可以使用one()来绑定事件。使用与on()类似。

### 4.trigger()

有些事件我们希望它**自动触发**，比如轮播图自动播放功能。可以利用定时器自动触发，不必使用鼠标点击。

```js
element.click();	// 第一种简写形式
$('div').click();

element.trigger('type');	// 第二种自动触发模式
$('div').trigger('click');

element.triggerHandler('type');	// 第三种自动触发模式	// 不会触发元素的默认行为
$('div').triggerHandler('click');
```

## 三、jQuery事件对象

只要有事件触发，就会有事件对象产生。

```js
element.on(events, [selector], function(event) {
	...
})
```

1. 阻止默认行为

   ```js
   // 1.
   event.preventDefault();
   
   // 2.
   return false;
   ```

2. 阻止冒泡

   ```js
   event.stopPropagation();
   ```

# jQuery其他方法

## 一、jQuery拷贝对象

在jQuery中，如果想要**把某个对象拷贝（合并）给另一个对象使用**，可以使用**$.extend()**方法。

```js
$.extend([deep], target, object1, [objectN]);
```

- deep：true 深拷贝，false 浅拷贝（默认）；
- target：拷贝到的目标；
- object1：被拷贝的第一个对象；
- objectN：被拷贝的第N个对象。

```js
var targetObj = {};
var obj = {
	id: 1,
	name: 'andy'
};
$.extend(targetObj, obj);
```

注：**浅拷贝**是把被拷贝的对象**复杂数据类型**中的**地址**拷贝给目标对象，**修改目标对象会影响背靠背对象**。**深拷贝**则是**完全克隆**（拷贝的对象，而不是地址），**修改目标对象不会影响被拷贝的对象**。

## 二、多库共存

问题概述：

jQuery使用$作为标识符，随着jQuery的流行，其他js库也会用$作为标识符，一起使用就会引起冲突。

解决方案：

1. 把里面的$符号统一改为jQuery，如jQuery('div')；

2. jQuery变量规定新的名称：$.noConflict()，var xx = $.noConflict(); 用户自定义标识符。

   ```js
   var suibian = jQuery.noConflict();	// 让jQuery释放对$控制权 由用户自己决定
   console.log(suibian('span'));
   ```

## 三、jQuery插件

jQuery功能有限，想要更加复杂的特效效果，需要借助jQuery插件完成。

注：插件依赖jQuery，因此使用时需要先引入jQuery文件，再引入插件文件。

### 1.jQuery插件常用网站

1. jQuery插件库：http://www.jq22.com/
2. jQuery之家：http://www.htmleaf.com/

### 2.jQuery插件使用步骤

1. 引入相关文件（jQuery文件及插件文件）；
2. 复制相关html、css、js（调用插件）。

## 四、综合案例：toDoList

![image-20220104175645829](https://gitee.com/v876774538/my-img/raw/master/image-20220104175645829.png)

![image-20220104204713684](https://gitee.com/v876774538/my-img/raw/master/image-20220104204713684.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ToDoList——最简单的待办事项列表</title>
    <link rel="stylesheet" href="css/index.css">
    <script src="js/jquery.min.js"></script>
    <script src="js/index.js"></script>
</head>

<body>
    <header>
        <section>
            <label for="title">ToDoList</label>
            <input type="text" id="title" name="title" placeholder="添加ToDo">
        </section>
    </header>
    <section>
        <h2>正在进行<span id="todocount"></span></h2>
        <ol id="todolist" class="demo-box">

        </ol>

        <h2>已经完成<span id="donecount"></span></h2>
        <ul id="donelist">
            <li>
                <input type="checkbox">
                <p>123</p>
                <a href="#"></a>
            </li>
        </ul>
    </section>
    <footer>
        Copyright &copy: 2022 todolist.cn
    </footer>
</body>

</html>
```

```css
body {
    margin: 0;
    padding: 0;
    font-size: 16px;
    background-color: #cdcdcd;
}

header {
    height: 50px;
    background-color: #333;
}

section {
    margin: 0 auto;
}

label {
    float: left;
    width: 100px;
    line-height: 50px;
    color: #ddd;
    font-size: 24px;
    cursor: pointer;
    font-family: "Helvetica Neue", Arial, Helvetica, sans-serif;
}

header input {
    float: right;
    width: 60%;
    height: 24px;
    margin-top: 12px;
    text-indent: 10px;
    border-radius: 5px;
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    -ms-border-radius: 5px;
    -o-border-radius: 5px;
    box-shadow: 0 1px 0 rgba(255, 255, 255, 0.24), 0 1px 6px rgba(0, 0, 0, 0.45) inset;
    border: none;
    outline: none;
}

h2 {
    position: relative;
}

span {
    position: absolute;
    top: 2px;
    right: 5px;
    display: inline-block;
    height: 20px;
    line-height: 22px;
    text-align: center;
    color: #666;
    font-size: 14px;
    padding: 0 5px;
    border-radius: 20px;
    -webkit-border-radius: 20px;
    -moz-border-radius: 20px;
    -ms-border-radius: 20px;
    -o-border-radius: 20px;
    background-color: #e6e6fa;
    ;
}

ol,
ul {
    padding: 0;
    list-style: none;
}

li {
    position: relative;
    height: 32px;
    line-height: 32px;
    background-color: #fff;
    margin-bottom: 10px;
    padding: 0 45px;
    border-radius: 3px;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    -ms-border-radius: 3px;
    -o-border-radius: 3px;
    border-left: 5px solid #629a9c;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.07);
}

/* 完成勾选框 */
li input {
    position: absolute;
    top: 2px;
    left: 10px;
    width: 20px;
    height: 20px;
    cursor: pointer;
}

/* 删除按钮 */
li a {
    position: absolute;
    top: 4px;
    right: 5px;
    display: inline-block;
    width: 14px;
    height: 12px;
    border-radius: 14px;
    border: 6px double #FFF;
    background: #CCC;
    line-height: 14px;
    text-align: center;
    color: #FFF;
    font-weight: bold;
    font-size: 14px;
    cursor: pointer;
}

ul li {
    /* 已完成中的li调整透明度 */
    opacity: 0.5;
}

footer {
    color: #666;
    font-size: 14px;
    text-align: center;
}

@media screen and (max-device-width: 620px) {
    section {
        width: 96%;
        padding: 0 2%;
    }
}

@media screen and (min-width: 620px) {
    section {
        width: 600px;
        padding: 0 10px;
    }
}
```

```js
$(function () {
    load();
    $('#title').on('keydown', function (event) {
        // console.log(event);
        if (event.key == 'Enter' && $(this).val() != '') {
            // 读取本地存储数据
            var local = getData();
            local.push({
                title: $(this).val(),
                done: false
            });
            // 存储到本地存储
            setData(local);
            // 清空输入框
            $(this).val('');
            // 渲染加载list数据
            load();
        }
    })

    // 删除
    $('#todolist, #donelist').on('click', 'a', function () {
        // 获取本地存储
        var data = getData();

        // 修改数据
        var index = $(this).attr('id');
        data.splice(index, 1);
        console.log(data);

        // 保存到本地存储
        setData(data);
        // 重新渲染
        load();
    })

    // 复选框
    $('#todolist, #donelist').on('click', 'input', function () {
        // 获取本地存储数据
        var data = getData();
        // 修改数据
        var index = $(this).siblings('a').attr('id');
        data[index].done = $(this).prop('checked');
        // 保存到本地存储
        setData(data);
        // 重新渲染
        load();
    })

    // 读取本地存取的数据
    function getData() {
        var data = localStorage.getItem('todolist');
        if (data !== null) {
            // 字符串格式转对象格式
            return JSON.parse(data);
        } else {
            return [];
        }
    }

    // 保存本地存储数据
    function setData(data) {
        localStorage.setItem('todolist', JSON.stringify(data));
    }

    // 加载list
    function load() {
        // 读取本地存储数据
        var data = getData();
        var todoCount = 0; // 未完成事项个数
        var doneCount = 0; // 已完成事项个数
        // console.log(data);
        // 加载前先清空
        $('ol, ul').empty();
        $.each(data, function (i, ele) {
            if (ele.done == false) {
                // 未完成
                $('ol').prepend("<li><input type='checkbox'><p>" + ele.title + "</p><a href='javascript:;' id='" + i + "'></a></li>");
                todoCount++;
            } else {
                // 已完成
                $('ul').prepend("<li><input type='checkbox' checked><p>" + ele.title + "</p><a href='javascript:;' id='" + i + "'></a></li>");
                doneCount++;
            }
        })
        $('#todocount').text(todoCount);
        $('#donecount').text(doneCount);
    }
})
```

file:///G:/%E5%AD%A6%E4%B9%A0/WEB%E5%89%8D%E7%AB%AF/%E9%BB%91%E9%A9%AC%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80/%E6%A1%88%E4%BE%8B/demo25/toDoList/index.html

# 数据可视化项目

## 一、概述

### 1.目的

借助**图形化**手段，清晰有效地传达与沟通信息。

### 2.使用场景

- 通用报表；
- 移动端图标；
- 大屏可视化；
- 图编辑&图分析；
- 地理可视化。

### 3.常见数据可视化库

- D3.js 目前Web端评价最高的Javascript可视化工具库（入手难）；
- **ECharts.js** 百度出品的开源JavaScript数据可视化库；
- **Highcharts.js** 国外的前端数据可视化库，非商用免费；
- AntV 蚂蚁金服全新一代数据可视化解决方案……

## 二、ECharts简介

EChaets是一个使用**JavaScript**实现的开源**可视化库**，可以流畅地运行在PC和移动设备上，兼容目前绝大部分的浏览器。底层依赖矢量图形库ZRender。提供直观、交互丰富、可高度个性化定制的数据可视化图表。

官网：https://echarts.apache.org/zh/index.html

## 三、ECharts基本使用

1. 下载并引入**echarts.js**文件
2. 准备一个具备大小的DOM容器
3. 初始化echarts实例对象
4. 指定配置项和数据（option）：根据具体需求修改配置选项
5. 将配置项设置给echarts实例对象

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <title>ECharts基本使用</title>
    <!-- 引入刚刚下载的 ECharts 文件 -->
    <script src="js/echarts.min.js"></script>
</head>

<body>
    <!-- 为 ECharts 准备一个定义了宽高的 DOM -->
    <div id="main" style="width: 600px;height:400px;"></div>
    <script type="text/javascript">
        // 基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'));

        // 指定图表的配置项和数据
        var option = {
            title: {
                text: 'ECharts 入门示例'
            },
            tooltip: {},
            legend: {
                data: ['销量']
            },
            xAxis: {
                data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
            },
            yAxis: {},
            series: [{
                name: '销量',	// 系列名称 用于tooltip显示legend图例筛选变化
                type: 'bar',	// 图表类型 line 折线 bar 柱形
                data: [5, 20, 36, 10, 10, 20]	// 数据
            }]
        };

        // 使用刚指定的配置项和数据显示图表。
        myChart.setOption(option);
    </script>
</body>

</html>
```

![image-20220106221520612](https://gitee.com/v876774538/my-img/raw/master/image-20220106221520612.png)

相关配置说明：

- title：标题组件
- tooltip：提示框组件（鼠标经过时提示）
- legend：图例组件
- toolbox：工具栏
- grid：直角坐标系内绘图网格
- xAxis：直角坐标系grid中的x轴
- yAxis：直角坐标系grid中的y轴
- series：系列列表，每个系列通过type决定自己的图表类型
- color：调色盘颜色列表（数组）

![image-20220111210716520](https://gitee.com/v876774538/my-img/raw/master/image-20220111210716520.png)

配置项手册：https://echarts.apache.org/zh/option.html#title

# 面向过程与面向对象

## 一、面向过程与面向对象

### 1.面向过程

面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个个依次调用。

### 2.面向对象

面向对象是把事务分解成一个个对象，然后由对象之间分工与合作。

### 3.面向过程与面向对象对比

|      | 面向过程                                                     | 面向多项                                                     |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 优点 | 性能比面向对象好， 适合跟硬件联系很紧密的东西，例如单片机就采用面向过程编程 | 易维护、易服用、易拓展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统更加灵活、易于维护 |
| 缺点 | 不易维护、不易复用、不易拓展                                 | 性能比面向过程差                                             |

## 二、对象与类

### 1.对象

对象是由属性和方法组成的：是一个无序键值对的集合，指的是一个具体的事物。

- 属性：事物的特征，在对象中用属性来表示（常用名词）；
- 方法：事物的行为，在对象中用方法来表示（常用动词）。

#### 1.1 创建对象

```js
// 复习
// 字面量创建对象
var ldh = {
	name: '刘德华',
    age: 18
}
console.log(ldh);

// 构造函数创建对象
function Star(name, age) {
    this.name = name;
    this.age = age;
}
var ldh = new Star('刘德华', 18);	// 对象实例化
console.log(ldh);
```

![](https://gitee.com/v876774538/my-img/raw/master/img3.png)

### 2.类

#### 2.1  创建类

语法：

```js
// 使用class关键字
class name {
	// class body
}
// 使用定义的类创建实例
var xx = new name();
```

```js
class Star {
	// 类的共有属性放到constructor构造函数中
	constructor(name, age) {
		this.name = name;
		this.age = age;
	}
}
// 利用类创建对象
var ldh = new Star('刘德华', 18);
console.log(ldh);
```

![](https://gitee.com/v876774538/my-img/raw/master/img4.png)

#### 2.2 类创建添加属性和方法

```js
// 1. 创建类
class Star {
	// 类的共有属性放到constructor构造函数中
	constructor(name, age) {
		this.name = name;
		this.age = age;
	}
	// 方法与方法之间不需要添加逗号
	sing(song) {
		console.log(this.name + '唱' + song);
	}
}
// 2. 利用类创建对象
var ldh = new Star('刘德华', 18);
console.log(ldh);
ldh.sing('冰雨');	// 刘德华唱冰雨
```

![](https://gitee.com/v876774538/my-img/raw/master/img5.png)

注意：

1. 通过class关键字创建类，类名习惯首字母大写；
2. 类里面的constructor函数，可以接受传递过来的参数，同时返回实例对象；
3. constructor函数只要new生成实例时就会自动调用，即使我们不写这个函数，类也会自动生成这个函数；
4. 多个函数方法之间不需要添加逗号分隔。

#### 2.3 类的继承

语法：

```js
// 父类
class Father {
	// ...
}

// 子类
class Son extends Father {
	// ...
}
```

```js
class Father {
	constructor(surname) {
		this.surname = surname;
	}
	say() {
		console.log('您的姓是' + this.surname);
	}
}

class Son extends Father{
	// 继承父类的属性和方法
}
var damao = new Son('金');
damao.say();	// 您的姓是金
```

子类用super关键字访问父类的方法：

```js
// 父类
class Father {
	constructor(x, y) {
		this.x = x;
		this.y = y;
	}
	sum() {
		console.log(this.x + this.y);
	}
}
// 子类继承父类
class Son extends Father {
	constructor(x, y) {
		super(x, y);	// 使用super调用父类的构造函数
	}
}
var son = new Son(1, 2);
son.sum();	// 3
```

注意：

1. 继承中，若实例化子类输出一个方法，先看子类存不存在该方法，若有就先执行子类的方法，若无，就去父类中查找该方法（就近原则）；

2. 若子类想要继承父类的方法，同时在自己内部脱战自己的方法，就利用super调用父类的构造函数（**super必须在子类this之前调用**）；

   ```js
   // 父类有加法方法
   class Father {
   	constructor(x, y) {
   		this.x = x;
   		this.y = y;
   	}
   	sum() {
   		console.log(this.x + this.y);
   	}
   }
   // 子类继承父类加法方法，同时扩展减法方法
   class Son extends Father {
   	constructor(x, y) {
   		super(x, y);
   		this.x = x;
   		this.y = y;
   	}
   	substract() {
   		console.log(this.x - this.y);
   	}
   }
   var son = new Son(5, 3);
   son.substract();	// 2
   son.sum();	// 8
   ```

3. 时刻注意this的指向问题，类里面的共有的属性和方法一定要加this使用；

   - constructor中的this指向的是new出来的实例对象 
   - 自定义的方法,一般也指向的new出来的实例对象
   - 绑定事件之后this指向的就是触发事件的事件源

4. 在ES6中类没有变量提升，所以**必须先定义类，才能通过类实例化对象**。

   ![](https://gitee.com/v876774538/my-img/raw/master/img2.png)

   ![](https://gitee.com/v876774538/my-img/raw/master/img1.png)

### 3.面向对象版tab栏切换

#### 3.1 insertAdjacentHTML

```js
element.insertAdjacentHTML(position, text);
```

- position是相对于元素的位置，必须是以下字符串之一：

  beforebegin：元素**自身的前面**；

  afterbegin：插入**元素内部的第一个子节点**之前；

  beforeend：插入**元素内部的最后一个子节点**之后；

  afterend：元素自身的后面。

- 以前的做法：动态创建元素creatElement，innerHTML赋值，在appendChild追加到父元素里面。

- 现在的高级做法：利用innerAdjacentHTML()直接把字符串格式元素添加到父元素中。

- appendChild不支持追加字符串的子元素，insertAdjacentHTML支持追加字符串的元素。

#### 3.2 实现

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>面向对象 Tab</title>
    <link rel="stylesheet" href="./styles/tab.css">
    <link rel="stylesheet" href="./styles/style.css">
</head>

<body>

    <main>
        <h4>
            Js 面向对象 动态添加标签页
        </h4>
        <div class="tabsbox" id="tab">
            <!-- tab 标签 -->
            <nav class="fisrstnav">
                <ul>
                    <li class="liactive"><span>测试1</span><span class="iconfont icon-guanbi"></span></li>
                    <li><span>测试2</span><span class="iconfont icon-guanbi"></span></li>
                    <li><span>测试3</span><span class="iconfont icon-guanbi"></span></li>
                </ul>
                <div class="tabadd">
                    <span>+</span>
                </div>
            </nav>

            <!-- tab 内容 -->
            <div class="tabscon">
                <section class="conactive">测试1</section>
                <section>测试2</section>
                <section>测试3</section>
            </div>
        </div>
    </main>

    <script src="js/tab.js"></script>
</body>

</html>
```

```css
* {
    margin: 0;
    padding: 0;
}

ul li {
    list-style: none;
}

main {
    width: 960px;
    height: 500px;
    border-radius: 10px;
    margin: 50px auto;
}

main h4 {
    height: 100px;
    line-height: 100px;
    text-align: center;
}

.tabsbox {
    width: 900px;
    margin: 0 auto;
    height: 400px;
    border: 1px solid lightsalmon;
    position: relative;
}

nav ul {
    overflow: hidden;
}

nav ul li {
    float: left;
    width: 100px;
    height: 50px;
    line-height: 50px;
    text-align: center;
    border-right: 1px solid #ccc;
    position: relative;
}

nav ul li.liactive {
    border-bottom: 2px solid #fff;
    z-index: 9;
}

#tab input {
    width: 80%;
    height: 60%;
}

nav ul li span:last-child {
    position: absolute;
    user-select: none;
    font-size: 12px;
    top: -18px;
    right: 0;
    display: inline-block;
    height: 20px;
}

.tabadd {
    position: absolute;
    /* width: 100px; */
    top: 0;
    right: 0;
}

.tabadd span {
    display: block;
    width: 20px;
    height: 20px;
    line-height: 20px;
    text-align: center;
    border: 1px solid #ccc;
    float: right;
    margin: 10px;
    user-select: none;
}

.tabscon {
    width: 100%;
    height: 300px;
    position: absolute;
    padding: 30px;
    top: 50px;
    left: 0px;
    box-sizing: border-box;
    border-top: 1px solid #ccc;
}

.tabscon section,
.tabscon section.conactive {
    display: none;
    width: 100%;
    height: 100%;
}

.tabscon section.conactive {
    display: block;
}
```

```js
var that;
class Tab {
    constructor(id) {
        that = this;
        // 获取元素
        this.main = document.querySelector(id);
        this.ul = this.main.querySelector('.firstnav ul');
        this.tabscon = this.main.querySelector('.tabscon');
        this.add = this.main.querySelector('.tabadd');
        this.init();
    }
    // 初始化
    init() {
        this.updateNode();
        // 添加绑定事件
        for (var i = 0; i < this.lis.length; i++) {
            this.lis[i].index = i; // 索引号
            this.lis[i].onclick = this.toggleTab;
            this.remove[i].onclick = this.removeTab;
            this.spans[i].ondblclick = this.editTab;
            this.sections[i].ondblclick = this.editTab;
        }
        this.add.onclick = this.addTab;
    }
    // 更新
    updateNode() {
        this.lis = this.main.querySelectorAll('li');
        this.sections = this.main.querySelectorAll('section');
        this.remove = this.main.querySelectorAll('.icon-guanbi');
        this.spans = this.main.querySelectorAll('.firstnav li span:first-child');

    }
    // 清除所有li和section的类
    clearClass() {
        for (var i = 0; i < this.lis.length; i++) {
            this.lis[i].className = '';
            this.sections[i].className = '';
        }
    }
    // 切换
    toggleTab() {
        that.clearClass();
        this.className = 'liactive';
        that.sections[this.index].className = 'conactive';
    }
    // 添加
    addTab() {
        that.clearClass();
        // insertAdjacentHTML() 直接把字符串格式元素添加到父元素中
        var li = '<li class="liactive"><span>新选项卡</span><span class="iconfont icon-guanbi"></span></li>'
        var section = '<section class="conactive">新选项卡</section>';
        that.ul.insertAdjacentHTML('beforeend', li);
        that.tabscon.insertAdjacentHTML('beforeend', section);
        that.init();
    }
    // 删除
    removeTab(e) {
        // 阻止冒泡 防止触发tab切换
        e.stopPropagation();
        var index = this.parentNode.index;
        // console.log(index);
        that.lis[index].remove();
        that.sections[index].remove();
        that.init();
        // 当删除的不是选中状态的tab时 选中状态不改变
        if (document.querySelector('.liactive')) {
            return;
        } else {
            // 当删除的是选中状态的tab时 自动显示前一个tab
            index--;
            that.lis[index] && that.lis[index].click();
        }
    }
    // 修改
    editTab() {
        var str = this.innerHTML;
        // 禁止选中文字
        window.getSelection ? window.getSelection().removeAllRanges() : document.getSelection.empty();
        // 生成文本框
        this.innerHTML = '<input type="text" />'
        var input = this.children[0];
        input.value = str;
        input.select(); // 使文本框的文字处于选定状态
        // 当我们离开文本框（失去焦点）/按下回车 将文本框的值赋给span
        input.onblur = function () {
            this.parentNode.innerHTML = this.value;
        }
        input.onkeyup = function (e) {
            if (e.key == 'Enter') {
                this.blur(); // 不用加on
            }
        }
    }

}
new Tab('#tab');
```

http://localhost:8080/demo27/index.html

## 三、私有属性

```js
class Person {
    // 公有属性
    name;

    // 私有属性
    #age;
    #weight;

    // 构造方法
    constructor(name, age, weight) {
        this.name = name;
        this.#age = age;
        this.#weight = weight;
    }
}

// 实例化
const girl = new Person('小红', 18, '45kg')
console.log(girl)

console.log(girl.name)
console.log(girl.#age)	// 报错
```

![image-20230202111155809](https://gitee.com/v876774538/my-img/raw/master/image-20230202111155809.png)

访问私有属性：

```js
class Person {
    // 公有属性
    name;

    // 私有属性
    #age;
    #weight;

    // 构造方法
    constructor(name, age, weight) {
        this.name = name;
        this.#age = age;
        this.#weight = weight;
    }

    // 访问私有属性
    intro() {
        console.log(this.#age)
    }
}

// 实例化
const girl = new Person('小红', 18, '45kg')
// console.log(girl)

// console.log(girl.name)
// console.log(girl.#age)   // 报错
girl.intro()
```



# 构造函数和原型

## 一、构造函数和原型

### 1.概述

在典型的OOP语言（如Java）中，都存在类的概念。类就是对象的模板，对象就是类的实例。但在ES6之前，JS中并没有引入类的概念。

在ES6之前，对象不是基于类创建的，而是用一种称为**构造函数**的特殊函数来定义对象和他们的特征。

创建对象三种方式：

- 对象字面量

  ```js
  var obj = {};
  ```

- new Object()

  ```js
  var obj = new Object();
  ```

- 自定义构造函数

  ```js
  function Star(uname, age) {
  	this.uname = uname;
  	this.age =age;
  	this.sing = function() {
  		console.log('我会唱歌');
  	}
  }
  var ldh = new Star('刘德华', 18);	// 实例化
  console.log(ldh);
  ldh.sing();
  ```

### 2.构造函数

构造函数是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，总是与new一起使用。

我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数中。

注意：

- 构造函数用于创建某一类对象，其首字母要大写；
- 构造函数要和new一起使用才有意义。

new的执行过程：

- 在内存中创建一个新的空对象；
- 让this指向这个新对象；
- 执行构造函数代码，给新对象添加属性和方法；
- 返回这个新对象（构造函数中不需要return）。

JavaScript构造函数中可以添加一些成员，可以在构造函数本身上添加，也可以在构造函数内部的this上添加。

- **静态成员**：在构造**函数本身上添加**的成员称为静态成员，**只能由构造函数本身来访问**；
- **实例成员**：在构**造函数内部创建的对象**成员称为实例成员，**只能由实例化的对象来访问**。

```js
function Star(uname, age) {
	this.uname = uname;
	this.age =age;
	this.sing = function() {
		console.log('我会唱歌');
	}
}
var ldh = new Star('刘德华', 18);	// 实例化
// uname age sing都是实例成员 只能通过实例化对象来访问
console.log(ldh.uname);
ldh.sing();

Star.sex = '男';	// 静态成员 在构造函数本身上添加的成员
console.log(Star.sex);	// 静态成员只能通过构造函数来访问
// console.log(ldh.sex);	// 错误 不能通过对象来访问
```

### 3.构造函数的问题

构造函数**存在浪费内存的问题**。→ **构造函数原型**

![image-20220116195209132](https://gitee.com/v876774538/my-img/raw/master/image-20220116195209132.png)

同一个方法却开辟了两个不同的存储空间。

### 4.构造函数原型 prototype

构造函数**通过原型分配的函数**是**所有对象所共享**的。

JavaScript规定，每一个构造函数都有一个prototype（原型）**对象**。

我们可以把那些不变的方法，直接定义在prototype对象上，这样所有对象的实例就都可以**共享**这些**方法**。

```js
function Star(uname, age) {
	this.uname = uname;
	this.age =age;
}
Star.prototype.sing = function() {
	console.log('我会唱歌');
}
var ldh = new Star('刘德华', 18);	// 实例化
var zxy = new Star('张学友', 18);
ldh.sing();
zxy.sing();
```

### 5.对象原型  `__proto__`

每个对象都会有一个`__proto__`属性，指向构造函数的prototype原型对象。正是因为对象有`__proto__`存在，我们才可以使用构造函数prototype原型对象的属性和方法。

- `__proto__`对象原型和原型对象prototype是等价的（前者指向后者）；

  ```js
  console.log(ldh.__proto__ == Star.prototype);	// true
  ```

  ![image-20220116201311902](https://gitee.com/v876774538/my-img/raw/master/image-20220116201311902.png)

- `__proto__`对象原型的意义在于为对象的查找机制提供方向，但它是一个非标准属性，在实际开发中，我们不可以使用该属性，它只是内部指向原型对象prototype。

### 6.构造函数 constructor

对象原型（`__proto__`）和构造函数（prototype）原型对象中都有一个constructor属性。constructor我们称为构造函数，因为它指回构造函数本身。

constructor主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数。

```js
function Star(uname, age) {
	this.uname = uname;
	this.age =age;
}
//Star.prototype.sing = function() {
//	console.log('我会唱歌');
//}
//Star.prototyep.movie = function() {
//	console.log('我会演电影')
//}
// 对象形式书写 结构更加清晰
// 但覆盖了原来的对象（没有constructor）
Star.prototype = {
    constructor: Star,	// 手动指回原来的构造函数
    sing: function() {
        console.log('我会唱歌');
    },
    movie: function() {
        console.log('我会演电影');
    }
}
var ldh = new Star('刘德华', 18);	// 实例化
```

### 7.构造函数、实例、原型对象之间的关系

![image-20220116203400930](https://gitee.com/v876774538/my-img/raw/master/image-20220116203400930.png)

### 8.原型链

![image-20220116203622053](https://gitee.com/v876774538/my-img/raw/master/image-20220116203622053.png)

JavaScript成员查找按照原型链进行：

- 当访问一个对象的属性（包括方法）时，首先查找对象自身是否拥有该属性；
- 若没有，则查找它的原型（`__proto__`指向的prototype原型对象）；
- 若还没有就查找原型对象的原型（原型对象`prototype.__proto__`，即Object原型对象prototype）；
- 还没有就查找Object原型对象的原型（返回null）。

### 9.扩展内置对象

可以通过原型对象，对原来的内置对象进行扩展自定义方法。

比如，给数组增加自定义求偶数和的功能。

```js
console.log(Array.prototype);
Array.prototype.sum = function() {
	var sum = 0;
	for (var i = 0; i < this.length; i++) {
		sum += this[i];
	}
	return sum;
}
var arr = [1, 2, 3];
console.log(arr.sum());
var arr1 = new Array(11, 22, 33);
console.log(arr1.sum());
```

注意：数组和字符串内置对象不能通过给原型对象**覆盖**的操作进行（`Array.prototype= {}` ），只能用`Array.prototype.xxx = function() {}` 的方式来追加扩展。

## 二、继承

ES6之前没有提供extends继承。

我们可以通过**构造函数+原型对象**模拟实现继承，称为**组合继承**。

### 1.call()

调用函数，并且修改函数运行时this的指向。

```js
fun.call(thisArg, arg1, arg2, ...);
```

- thisArg：当前调用函数的this的指向对象；
- arg1，arg2，...：传递的其他参数。

### 2.借用构造函数继承父类型属性

核心原理：通过call()把父类型的this指向子类型的this，实现子类型继承父类型属性。

```js
// 父构造函数
function Father (uname, age) {
	this.uname = uname;
	this.age = age;
	// this指向父构造函数的实例对象
}
// 子构造函数
function Son (uname, age) {
	// this指向子构造函数的实例对象
	// 借用父构造函数继承父类型属性
	Father.call(this, uname, age);	// 将this指向Son
}
```

### 3.借用原型对象继承父类方法

```js
// 父构造函数
function Father (uname, age) {
	this.uname = uname;
	this.age = age;
	// this指向父构造函数的实例对象
}
Father.prototype.money = function() {
    console.log(10000000);
}
// 子构造函数
function Son (uname, age) {
	// this指向子构造函数的实例对象
	// 借用父构造函数继承父类型属性
	Father.call(this, uname, age);	// 将this指向Son
}
// 借用原型对象继承父类方法
//Son.prototype = Father.prototype;	// 这样赋值会有问题 （由于是直接修改地址 当我们给Son的原型对象添加方法时，会影响到Father原型对象）
Son.prototype = new Father();
// 利用对象的形式修改了原型对象 别忘了利用constructor指回原来的构造函数
Son.prototype.constructor = Son;
```

![image-20220116212821091](https://gitee.com/v876774538/my-img/raw/master/image-20220116212821091.png)

### 4.类的本质

ES6之前，通过构造函数+原型来实现面向对象编程，而在ES6中，我们可以通过类实现面向对象编程。

## 三、ES5中的新增方法

### 1.数组方法

1. 迭代（遍历）方法
   1. forEach()

      ```js
      array.forEach(function(currentValue, index, arr))
      ```

      - currentValue：数组当前项的值
      - index：数组当前项的索引
      - arr：数组对象本身

   2. map()

   3. filter()

      ```js
      array.filter(function(currentValue, index, arr))
      ```

      filter()方法**创建一个新数组**，新数组中氮元素是通过检查指定数组中**符合条件**的所有元素，**主要用于筛选数组**。

      - currentValue：数组当前项的值
      - index：数组当前项的索引
      - arr：数组对象本身

   4. some()

      ```js
      array.some(function(currentValue, index, arr))
      ```

      some()方法用于监测数组中的元素是否满足指定条件，即**查找数组中是否存在满足条件的元素**。**返回值为布尔值**，若存在，则返回true，反之返回false（找到第一个满足条件的元素就退出循环）。

      - currentValue：数组当前项的值
      - index：数组当前项的索引
      - arr：数组对象本身

   5. every()

### 2.字符串方法

1. trim()

   ```js
   str.trim()
   ```

   trim()方法会**从一个字符串的两端删除空白字符**。trim()方法并不影响字符串本身，它返回的是一个新的字符串。

### 3.对象方法

1. Object.defineProperty()

   定义对象中新属性或修改原有的属性。

   ```js
   Object.defineProperty(obj, prop, descriptor)
   ```

   - obj：必须，目标对象
   - prop：必须，需定义或修改的属性的名字
   - descriptor：必须，目标属性所拥有的的特性

   descriptor说明：以对象形式{}书写

   - value：设置属性的值，默认为undefined
   - writable：值是否可以重写，true | false，默认为false
   - enumerable：目标属性是否可以被枚举，true | false，默认为false（不允许遍历）
   - configurable：目标属性是否可以被删除或是否可以再次修改特性，true | false，默认为false

# 函数进阶

### 一、函数的定义和调用

### 1.函数的定义方式

1. 自定义函数（命名函数）

   ```js
   function fn() {
   	...函数体
   };
   ```

2. 函数表达式（匿名函数）

   ```js
   var fun = function() {
   	...函数体
   }
   ```

3. 利用new Function('参数1', '参数2', ..., '函数体')

   ```js
   var fn = new Function('参数1', '参数2', ..., '函数体')
   ```

   - **所有函数都是Function的实例**（对象）；
   - 函数也属于对象。

   ![image-20220418155746626](https://gitee.com/v876774538/my-img/raw/master/image-20220418155746626.png)

### 2.函数的调用方式

1. 普通函数

   ```js
   function fn() {
   	// 函数体...
   }
   // 调用
   fn();
   fn.call()
   ```

2. 对象的方法

   ```js
   var o = {
   	sayHi: function() {
   		// 函数体...
   	}
   }
   o.sayHi();
   ```

3. 构造函数

   ```js
   function Star() {};
   // 创建实例
   new Star();
   ```

4. 绑定事件函数

   ```js
   btn.onclick = function() {};
   ```

5. 定时器函数

   ```js
   setInterval(function() {},1000);
   ```

6. 立即执行函数

   ```js
   (function() {
   	// 函数体
   })()
   // 立即执行函数将自动调用
   ```

### 二、this

> this的指向，是当我们调用函数的时候确定的。
>
> 调用方式的不同决定了this的指向不同。**一般指向我们的调用者**。

| 调用方式     | this指向                                   |
| ------------ | ------------------------------------------ |
| 普通函数调用 | window                                     |
| 构造函数调用 | 实例对象，原型对象里面的方法也指向实例对象 |
| 对象方法调用 | 该方法所属的对象                           |
| 事件绑定方法 | 绑定事件的对象                             |
| 定时器函数   | window                                     |
| 立即执行函数 | window                                     |

### 1.改变函数内部的this指向

> JavaScript为我们专门提供了一些函数方法来帮我们更优雅地处理函数内部this的指向问题，常用的有bind()、call()、apply()三种。

#### 1.1 call()

call()方法调用一个**对象**。简单理解为调用函数的方式，它还可以改变函数的this指向。

```js
fun.call(thisArg, arg1, arg2, ...);
```

```js
var o = {
	name: 'andy'
}

function fn(a, b) {
	console.log(this);	// 指向o
    console.log(a + b);	// 3
};
fn.call(o, 1, 2);
```

**主要应用**：

```js
// call的主要作用是实现继承
// 核心原谅你：通过call()把父类型的this指向子类型的this，实现子类型继承父类型属性

// 父构造函数
function Father (uname, age) {
	this.uname = uname;
	this.age = age;
	// this指向父构造函数的实例对象
}
// 子构造函数
function Son (uname, age) {
	// this指向子构造函数的实例对象
	// 借用父构造函数继承父类型属性
	Father.call(this, uname, age);	// 将this指向Son
}
```

#### 1.2 apply()

apply()方法调用一个**函数**。单理解为调用函数的方式，它还可以改变函数的this指向。

```js
fun.apply(thisArg, [argsArray]);
```

- thisArg：在fun函数运行时指定的this值
- argsArray：传递的值，必须包含在数组里面
- 返回值就是函数的返回值，因为它就是调用函数

```js
var o = {
	name: 'andy'
}

function fn(arr) {
	console.log(this);	// o
	console.log(arr);	// 'pink'	// 字符串
};
fn.apply(o, ['pink']);	// 参数必须是数组（伪数组）
```

**主要应用**：

```js
// 利用apply借助数学内置对象求数组最大值
var arr = [1, 66, 3, 99, 4];
var max = Math.max.apply(Math, arr);
console.log(max);
```

#### 1.3 bind()

bind()方法不会调用函数，但是能改变函数内部的this指向。

```js
fun.bind(thisArg, arg1, arg2, ...);
```

- thisArg：在fun函数运行时指定的this值
- arg1, arg2, ...：传递的参数
- 返回由指定的this值和初始化参数**改造的原函数拷贝**

```js
var o = {
	name: 'andy'
};
function fn(a, b) {
	console.log(this);
	console.log(a + b);
}
var f = fn.bind(o, 1, 2);
f();	// o	// 3
```

**主要应用**：

```js
// 若有的函数我们不需要立即调用，但是又想改变这个函数内部的this指向，此时使用bind

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

### 2.总结

1. 相同点

   都可以改变函数内部的this指向。

2. 区别点

   - call和apply会调用函数，并且改变函数内部的this指向；
   - call和apply传递的参数不一样，call传递参数采用`arg1, arg2, ...`的形式，apply则必须采用数组`[argArr]`的形式；
   - bind不会调用函数，只是改变函数内部的this指向。

3. 主要应用场景

   - call经常做继承；
   - apply通常跟数组有关，比如借助数学对象实现求数组内最大值/最小值；
   - bind通常用于不想调用函数，但是想改变this指向时，如改变定时器内部的this指向。

### 三、严格模式

### 1.什么是严格模式

> JavaScript除了提供正常模式外，还提供了**严格模式（Strict Mode）**。ES5的严格模式是采用具有限制性JavaScript辩题的一种方式，即在严格的条件下运行JS代码。
>
> 严格模式在IE10以上版本的浏览器中才被支持，旧版本浏览器中会被忽略。

严格模式对正常的JavaScript语义做了一些更改：

1. 消除了JavaScript语法的一些不合理、不严谨之处，减少了一些怪异行为；
2. 消除代码运行的一些不安全之处，保证代码运行的安全；
3. 提高编译器效率，增加运行速度；
4. 禁用了在ECMAScript的未来版本中可能会定义的一些语法，为未来新版本的JavaScript做好铺垫。比如一些保留字，如：class, enum, export, extends, import, super 不能做为变量名。

### 2.开启严格模式

> 严格模式可以应用到整个脚本或个别函数中。
>
> 因此在使用时，我们可以将严格模式分为**为脚本开启严格模式**和**为函数开启严格模式**两种情况。

#### 2.1 为脚本开启严格模式

在所有语句之前放一个特定语句：`"use strict";`或`'use strict';`

```html
<!-- 为整个脚本（script标签）开启严格模式 -->
<script>
	'use strict';
	// 下面的js代码都会按照严格模式执行
	// ...
</script>

<script>
	// 防止代码污染
    // 有的script基本是严格模式，有的script脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样创建一个作用域而不影响其他script脚本文件
	(function() {
		'use strict';
		// 下面的js代码都会按照严格模式执行
		// ...
	})();
</script>
```

#### 2.2 为函数开启严格模式

把`"use strict";`或`'use strict';`生命放在函数体所有语句之前。

```html
<!-- 为某个函数开启严格模式 -->
<script>
	function fn() {
		'use strict';
		// 下面的代码按照严格模式执行
	}
	function fn1() {
		// 里面的代码还按照普通模式执行
	}
</script>
```

### 3.严格模式中的变化

严格模式对JavaScript的语法和行为，都做了一些改变。

#### 3.1 变量规定

1. 在正常模式中，如果一个变量没有声明就赋值，则默认为全局变量。严格模式禁止这种用法，变量都必须先用var进行声明；
2. 严禁删除已经声明的变量。如，`delete x;`这种语法是错误的。

#### 3.2 this指向

1. 以前在全局作用域函数中的this指向window对象；

2. 严格模式下，**全局作用域中函数的this指向是undefined**。

3. 以前构造函数时不加new也可以当普通函数调用，this指向全局对象；

   ```js
   function Star() {
   	this.sex = '男';
   }
   Star();
   console.log(window.sex);
   ```

4. 严格模式下，若构造函数不加new调用，由于this在全局作用域中指向的是undefined，this会报错；

5. new实例化的构造函数指向创建的对象实例。

   ```js
   function Star() {
   	this.sex = '男';
   }
   var ldh = new Star();
   console.log(ldh.sex);
   ```

6. 定时器this还是指向window；

7. 事件、对象还是指向调用者。

#### 3.3 函数

1. 函数不能有重名的参数；

2. 函数必须声明在顶层。新版本的JavaScript会引入“块级作用域”（ES6中已引入），为了与新版本接轨，不允许在**非函数的代码块**内声明函数。

   ```js
   'use strict';
   if (true) {
   	function f() {
   	
   	}	// 语法错误
   	f();
   }
   
   for (var i = 0; i < 5; i++) {
   	function f2() {
   	
   	}	// 语法错误
   	f2();
   }
   
   function f3() {	// 合法
   	function f4() {
   		// 合法
   	}
   }
   ```

### 四、高阶函数

> **高阶函数**是对其他函数进行操作的函数，它**接收函数作为参数**，或**将函数作为返回值输出**。

```html
<!-- 接收函数作为参数 -->
<script>
	// 声明
	function fn(callback) {
		callback && callback();
	}
	// 调用
	fn(function() {
		alert('hi');
	})
</script>
```

```html
<!-- 将函数作为返回值输出 -->
<script>
	function fn() {
		return function() {}
	}
	fn();
</script>
```

函数也是一种数据类型，同样可以作为参数传递给另外一个函数使用。最典型的就是作为**回调函数**。

### 五、闭包

### 1.变量作用域

变量根据作用域的不同分为：全局变量和局部变量。

1. 函数内部可以使用全局变量；
2. 函数外部不可以使用局部变量；
3. 当函数执行完毕，本作用域内的局部变量会销毁。

### 2.什么是闭包

> **闭包**（closure）指**有权访问另一个函数作用域中变量的函数**。
>
> 简单理解就是，一个作用域可以访问另外一个函数内部的局部变量。

```js
function fn() {
	var num = 10;
	function fn1() {
		console.log(num);	// fn1这个函数作用域访问了另一个函数fn里面的局部变量num → 产生了闭包
	}
	fu1();
}
fn();
```

### 3.闭包的作用

> 闭包的主要作用：延伸了变量的作用范围。

```js
function fn() {
	var num = 10;
	// function fun() {
	//	console.log(num);
	//}
	// return fun;
    return function() {
        console.log(num);
    }
}
var f = fn();
f();
```

### 4.闭包的应用

#### 4.1 循环注册点击事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>点击li输出当前li索引号</title>
</head>
<body>
    <ul class="nav">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
    <script>
        // 1. 动态添加属性
        var lis = document.querySelector('.nav').querySelectorAll('li');
        for(var i = 0; i < lis.length; i++) {
            lis[i].index = i;   // 动态添加属性
            lis[i].onclick = function() {
                console.log(this.index);
            }
        }
        // 2. 利用闭包方式得到当前li索引号
        for(var i = 0; i < lis.length; i++) {
            // 利用for循环创建4个立即执行函数
            // 立即执行函数也称为小闭包，因为立即执行函数里面的任何一个函数都可以使用它的i这变量
            (function(i) {
                lis[i].onclick = function() {
                    console.log(i);
                }
            })(i);
        }
    </script>
</body>
</html>
```

#### 4.2 3秒后打印li内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3s后打印所有li元素内容</title>
</head>
<body>
    <ul class="nav">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
    </ul>
    <script>
        // 1. 普通实现
        var lis = document.querySelector('.nav').querySelectorAll('li');
        setTimeout(() => {
            for (var i = 0; i < lis.length; i++) {
                console.log(lis[i].innerHTML);
            }
        }, 3000);
        // 2. 闭包实现
        for(var i = 0; i < lis.length; i++) {
            (function(i) {
                setTimeout(function() {
                    console.log(lis[i].innerHTML);
                }, 3000);
            })(i)
        }
    </script>
</body>
</html>
```

#### 4.3 计算打车价格

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>计算打车价格</title>
</head>
<body>

    <script>
        // 打车起步价13（3公里内），之后每多一公里加5元，用户输入公里数就可以计算打车价格
        // 若有拥堵情况，总价格多收取10元拥堵费
        var car = (function() {
            var start = 13; // 起步价
            var total = 0;  // 总价
            return {
                // 正常的总价
                price: function(n) {
                    if (n <= 3) {
                        total = start;
                    }
                    else {
                        total = start + (n - 3) * 5;
                    }
                    return total;
                },
                // 拥堵费用
                yd: function(flag) {
                    return flag ? total + 10 : total;
                }
            }
        })();
        console.log(car.price(5));  // 23
        console.log(car.yd(true));  // 33

        console.log(car.price(1));  // 13
        console.log(car.yd(false));  // 13
    </script>
</body>
</html>
```

### 六、递归

### 1.什么是递归

> 如果一个函数在内部**调用其本身**，那么这个函数就是递归函数。
>
> 递归函数的作用和循环效果相同。
>
> 由于递归很容易发生“栈溢出”错误（stack overflow），所以**必须要加退出条件return**。

```js
var num = 1;
function fn() {
	console.log('我要打印6句话');
	if (num == 6) {	// 退出条件
		return;
	}
	num++;
	fn();
}
fn();
```

### 2.浅拷贝和深拷贝

#### 2.1 浅拷贝

1. 浅拷贝只是拷贝一层，更深层次对象级别的数据**只拷贝引用（地址）**→修改数据将影响原对象；
2. `Object.assign(target,...source)`ES6新增方法可以进行浅拷贝。

```js
var obj = {
    id: 1,
    name: 'andy',
    msg:{
        age: 18
    }
};
var o = {};
// 浅拷贝
for (var k in obj) {
    // k：属性名 obj[k]：属性值
    o[k] = obj[k];
}
// 或
// Object.assign(o, obj);
console.log(o);
o.msg.age = 20;
console.log(obj);
```

#### 2.2 深拷贝

1. 深拷贝拷贝多层，每一级别的数据都会拷贝。
2. 使用**递归**进行深拷贝：

```js
var obj = {
    id: 1,
    name: 'andy',
    msg:{
        age: 18
    },
    color:['pink','red']
};
var o = {};

// 深拷贝
function deepCopy(newObj, oldObj) {
    for (var k in oldObj) {
        // 判断属性值属于哪种数据类型（简单数据类型/复杂数据类型）
        // 1. 获取属性值 oldObj[k]
        var item = oldObj[k];
        // 2. 判断这个值是否是数组
        // 注意：数组也属于对象，因此要先判断数组！
        if (item instanceof Array) {
            newObj[k] = [];
            deepCopy(newObj[k], item);
        }
        // 3. 判断这个值是否是对象
        else if (item instanceof Object) {
            newObj[k] = {};
            deepCopy(newObj[k], item);
        }
        // 4. 属于简单数据类型
        else {
            newObj[k] = item;
        }
    }
}
deepCopy(o, obj);
console.log(o);
o.msg.age = 20;
console.log(obj);
```

![image-20220419145546997](https://gitee.com/v876774538/my-img/raw/master/image-20220419145546997.png)

# 正则表达式

## 一、概述

### 1.什么是正则表达式

正则表达式（Regular Expression）是用于**匹配字符串中字符组合**的模式。在JavaScript中，正则表达式也是**对象**。

> 正则表达式通常被用来检索、替换那些符合某个模式（规则）的文本，例如验证表单：用户名表单只能输入英文字母、数字或者下划线，昵称输入框中可以输入中文（**匹配**）。此外，正则表达式还常用于过滤掉页面内容中的一些敏感词（**替换**），或从字符串中获取我们想要的特定部分（**提取**）等。

### 2.特点

1. 灵活性、逻辑性和功能性非常强；
2. 可以迅速地用极简单的方式达到字符串的复杂控制；
3. 对于刚接触的人来说，较为晦涩难懂，在实际开发中，一般都是直接复制写好的正则表达式。但还是要求会使用正则表达式并且根据实际情况对其做出修改，如用户名：`/^[a-z0-9_-]{3,16}$/`

## 二、在JavaScript中的使用

### 1.创建正则表达式

在JavaScript中，可以通过两种方式创建正则表达式：

#### 1.1 通过调用RegExp对象的构造函数创建

```js
var 变量名 = new RegExp(/表达式/);
```

#### 1.2 通过字面量创建

```js
var 变量名 = /表达式/;
```

## 三、正则表达式中的特殊字符

### 1.正则表达式组成

一个正则表达式可以由简单的字符构成，比如`/abc/`，也可以是简单和特殊字符的组合，比如`/ab*c/`。

其中，特殊字符也被称为**元字符**，在正则表达式中是具有**特殊意义的专用符号**，如`^`、`$`、`+`等。

特殊字符非常多，可以参考：

- MDN：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions
- jQuery手册：正则表达式部分
- 正则测试工具：https://tool.oschina.net/regex
- 菜鸟正则表达式在线测试工具：https://c.runoob.com/front-end/854/

### 2.边界符

正则表达式中的边界符（位置符）**用来提示字符所处的位置**，主要有两个字符：

| 边界符 | 说明                               |
| ------ | ---------------------------------- |
| ^      | 表示匹配行首的文本（要求以谁开始） |
| $      | 表示匹配行尾的文本（要求以谁结束） |

如果^和$在一起，表示必须是**精确匹配**。

```js
var reg1 = /abc/;	// 正则表达式中不需要加引号 不管是数字型还是字符串型
// 只要包含abc就符合
console.log(reg1.test('abc'));	// true
console.log(reg1.test('abcd'));	// true
console.log(reg1.test('aabcd'));	// true

var reg2 = /^abc/;
// 以abc开头
console.log(reg2.test('abc'));	// true
console.log(reg2.test('abcd'));	// true
console.log(reg2.test('aabcd'));	// false

var reg3 = /^abc$/;
// 精确匹配 要求必须是abc字符串才符合规范
console.log(reg3.test('abc'));	// true
console.log(reg3.test('abcd'));	// false
console.log(reg3.test('aabcd'));	// false
```

### 3.字符类

字符类`[]`表示有一系列字符可供选择，只要匹配其中一个就符合。**所有可供选择的字符都放在方括号内。**

```js
var reg = /[abc]/;
// 只要包含有a/b/c其中一个就符合
console.log(reg.test('andy'));	// true
console.log(reg.test('baby'));	// true
console.log(reg.test('color'));	// true
console.log(reg.test('red'));	// false

var reg1 = /^[abc]$/;
// a/b/c三选一
console.log(reg1.test('aa'));	// false
console.log(reg1.test('a'));	// true
console.log(reg1.test('abc'));	// false
```

`[-]`，方括号内部**范围符**`-`

```js
var reg2 = /^[a-z]$/;
// 26个小写英文字母任意一个
console.log(reg2.test('a'));	// true
console.log(reg2.test('b'));	// true
console.log(reg2.test(1));	// false
console.log(reg2.test('A'));	// false
```

**字符组合**

```js
var reg3 = /^[a-zA-Z]$/;
// 26个英文字母任意一个（大写小写均可）
console.log(reg2.test('a'));	// true
console.log(reg2.test('b'));	// true
console.log(reg2.test(1));	// false
console.log(reg2.test('A'));	// true
```

`[^]`方括号内部`^`为**取反符**

```js
// 中括号内部的^表示取反！
var reg4 = /^[^a-zA-Z]$/;
// 不包含26个英文字母
console.log(reg2.test('a'));	// false
console.log(reg2.test('b'));	// false
console.log(reg2.test(1));	// true
console.log(reg2.test('A'));	// false
```

### 4.量词符

量词符用来**设定某个模式出现的次数**。

| 量词  | 说明             |
| ----- | ---------------- |
| *     | 重复零次或更多次 |
| +     | 重复一次或更多次 |
| ?     | 重复零次或一次   |
| {n}   | 重复n次          |
| {n,}  | 重复n次或更多次  |
| {n,m} | 重复n到m次       |

```js
var reg = /^a$/;

// * 相当于 >=0 可以出现0次或很多次
var reg1 = /^a*$/;
console.log(reg1.test(''));	// true
console.log(reg1.test('a'));	// true
console.log(reg1.test('aaaaaa'));	// true

// + 相当于 >=1
var reg2 = /^a+$/;
console.log(reg2.test(''));	// false
console.log(reg2.test('a'));	// true
console.log(reg2.test('aaaaaa'));	// 

// ? 相当于 1||0
var reg3 = /^a?$/;
console.log(reg3.test(''));	// true
console.log(reg3.test('a'));	// true
console.log(reg3.test('aaaaaa'));	// false

// {n} 相当于 =n
var reg4 = /^a{6}$/;
console.log(reg4.test(''));	// false
console.log(reg4.test('a'));	// false
console.log(reg4.test('aaaaaa'));	// true
console.log(reg4,test('aaaaaaa'));	// false

// {n,} 相当于>=n
var reg5 = /^a{6,}$/;
console.log(reg5.test(''));	// false
console.log(reg5.test('a'));	// false
console.log(reg5.test('aaaaaa'));	// true
console.log(reg5.test('aaaaaaa'));	// true

// {n,m} 相当于>=n <=m
var reg6 = /^a{1,6}$/;
console.log(reg6.test(''));	// false
console.log(reg6.test('a'));	// true
console.log(reg6.test('aaaaaa'));	// true
console.log(reg6.test('aaaaaaa'));	// false
```

### 5.优先级

`()`表示优先级。

```js
var reg = /^(abc){3}$/;
// abc重复3次
console.log(reg.test('abc'));	// false
console.log(reg.test('abcabcabc'));	// true
console.log(reg.test('abcccccccc'));	// false
```

也可以表示对内容的范围选择，捕获等。

`(123|132|321|312)`表示不论123/132/321/312都可以匹配；

`(123)?`表示出现1次或不出现123

### 6.预定义类

预定义类指的是**某些常见模式的简写方式**。

| 预定义类 | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| \d       | 匹配0-9之间的任一数字，相当于`[0-9]`                         |
| \D       | 匹配所有0-9以外的字符，相当于`[^0-9]`                        |
| \w       | 匹配任意的字母、数字和下划线，相当于`[A-Za-z0-9]`            |
| \W       | 除所有字母、数字和下划线以外的字符，相当于`[^A-Za-z0-9_]`    |
| \s       | 匹配空格（包括换行符、制表符、空格符等），相当于`[\t\r\n\v\f]` |
| \S       | 匹配非空格的字符，相当于`[^\t\r\n\v\f]`                      |

```js
// 座机号码验证：两种格式010-12345678	或 0530-1234567
// 正则里面的或者符号→|
var reg = /^\d{3}-\d{8} | \d{4}-\d{7}$/;
```

### 7.通配符

| 表达式 | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| `.`    | 表示匹配除换行符`\n`之外的任何单字符                         |
| `*`    | 表示零次或多次                                               |
| `.*`   | 表示任意字符出现零次或多次                                   |
| `.*?`  | `?`跟在`*`或`+`后面时，表示懒惰模式，也称非贪婪模式，即匹配尽可能少的字符。意味着匹配任意数量的重复，但是在能使整个匹配成功的前提下使用最少的重复<br />例如：`a.*?b`，匹配以a开始b结束的字符串，若将其应用于`aabab`，匹配的结果会是`aab` |
| `.+?`  | `+`表示一次或多次<br/>例如：`a.+?b`，匹配以a开始b结束的字符串，且ab之间至少有一个字符，若将其应用于`ababccaab`。将匹配到`abab` |

```js
let str = 'ababccaab'
let reg1 = /a.+?b/
let reg2 = /a.+b/
let result1 = reg1.exec(str)
let result2 = reg2.exec(str)
// let result = str.match(reg)
console.log(result1)
console.log(result2)
```

![image-20230201162358154](https://gitee.com/v876774538/my-img/raw/master/image-20230201162358154.png)

## 四、常用正则表达式

### 1.校验数字的表达式

- 数字：`^[0-9]\*$`
- n位的数字：`^\d{n}$`
- 至少n位的数字：`^\d{n,}$`
- m-n位的数字：`^\d{m,n}$`
- 零和非零开头的数字：`^(0|[1-9][0-9]\*)$`
- 非零开头的最多带两位小数的数字：`^([1-9][0-9]\*)+(\.[0-9]{1,2})?$`
- 带1-2位小数的正数或负数：`^(\-)?\d+(\.\d{1,2})$`
- 正数、负数、和小数：`^(\-|\+)?\d+(\.\d+)?$`
- 有两位小数的正实数：`^[0-9]+(\.[0-9]{2})?$`
- 有1~3位小数的正实数：`^[0-9]+(\.[0-9]{1,3})?$`
- 非零的正整数：`^[1-9]\d\*$ 或 ^([1-9][0-9]\*){1,3}$ 或 ^\+?[1-9][0-9]\*$`
- 非零的负整数：`^\-[1-9][]0-9"\*$ 或 ^-[1-9]\d\*$`
- 非负整数：`^\d+$ 或 ^[1-9]\d\*|0$`
- 非正整数：`^-[1-9]\d\*|0$ 或 ^((-\d+)|(0+))$`
- 非负浮点数：`^\d+(\.\d+)?$ 或 ^[1-9]\d\*\.\d\*|0\.\d\*[1-9]\d\*|0?\.0+|0$`
- 非正浮点数：`^((-\d+(\.\d+)?)|(0+(\.0+)?))$ 或 ^(-([1-9]\d\*\.\d\*|0\.\d\*[1-9]\d\*))|0?\.0+|0$`
- 正浮点数：`^[1-9]\d\*\.\d\*|0\.\d\*[1-9]\d\*$ 或 ^(([0-9]+\.[0-9]\*[1-9][0-9]\*)|([0-9]\*[1-9][0-9]\*\.[0-9]+)|([0-9]\*[1-9][0-9]\*))$`
- 负浮点数：`^-([1-9]\d\*\.\d\*|0\.\d\*[1-9]\d\*)$ 或 ^(-(([0-9]+\.[0-9]\*[1-9][0-9]\*)|([0-9]\*[1-9][0-9]\*\.[0-9]+)|([0-9]\*[1-9][0-9]\*)))$`
- 浮点数：`^(-?\d+)(\.\d+)?$ 或 ^-?([1-9]\d\*\.\**d\*|0\.\d\*[1-9]\d\*|0?\.0+|0)$`

### 2.校验字符的表达式

- 汉字：`^[\u4e00-\u9fa5]{0,}$`
- 英文和数字：`^[A-Za-z0-9]+$ 或 ^[A-Za-z0-9]{4,40}$`
- 长度为3-20的所有字符：`^.{3,20}$`
- 由26个英文字母组成的字符串：`^[A-Za-z]+$`
- 由26个大写英文字母组成的字符串：`^[A-Z]+$`
- 由26个小写英文字母组成的字符串：`^[a-z]+$`
- 由数字和26个英文字母组成的字符串：`^[A-Za-z0-9]+$`
- 由数字、26个英文字母或者下划线组成的字符串：`^\w+$` 或 `^\w{3,20}$`
- 中文、英文、数字包括下划线：`^[\u4E00-\u9FA5A-Za-z0-9_]+$`
- 中文、英文、数字但不包括下划线等符号：`^[\u4E00-\u9FA5A-Za-z0-9]+$` 或 `^[\u4E00-\u9FA5A-Za-z0-9]{2,20}$`
- 可以输入含有^%&',;=?$\"等字符：`[^%&',;=?$\x22]+`
- 禁止输入含有~的字符：`[^~]+`

### 3.特殊需求表达式

- Email地址：`^\w+([-+.]\w+)\*@\w+([-.]\w+)\*\.\w+([-.]\w+)\*$`
- 域名：`[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(\.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+\.?`
- InternetURL：`[a-zA-z]+://[^\s]\*` 或 `^http://([\w-]+\.)+[\w-]+(/[\w-./?%&=]\*)?$`
- 手机号码：`^(13[0-9]|14[5|7]|15[0|1|2|3|4|5|6|7|8|9]|18[0|1|2|3|5|6|7|8|9])\d{8}$`
- 电话号码("XXX-XXXXXXX"、"XXXX-XXXXXXXX"、"XXX-XXXXXXX"、"XXX-XXXXXXXX"、"XXXXXXX"和"XXXXXXXX)：`^(\(\d{3,4}-)|\d{3.4}-)?\d{7,8}$`
- 国内电话号码(0511-4405222、021-87888822)：`\d{3}-\d{8}|\d{4}-\d{7}`
- 电话号码正则表达式（支持手机号码，3-4位区号，7-8位直播号码，1－4位分机号）: `((\d{11})|^((\d{7,8})|(\d{4}|\d{3})-(\d{7,8})|(\d{4}|\d{3})-(\d{7,8})-(\d{4}|\d{3}|\d{2}|\d{1})|(\d{7,8})-(\d{4}|\d{3}|\d{2}|\d{1}))$)`
- 身份证号(15位、18位数字)，最后一位是校验位，可能为数字或字符X：`(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)`
- 帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：`^[a-zA-Z][a-zA-Z0-9_]{4,15}$`
- 密码(以字母开头，长度在6~18之间，只能包含字母、数字和下划线)：`^[a-zA-Z]\w{5,17}$`
- 强密码(必须包含大小写字母和数字的组合，不能使用特殊字符，长度在 8-10 之间)：`^(?=.\*\d)(?=.\*[a-z])(?=.\*[A-Z])[a-zA-Z0-9]{8,10}$`
- 强密码(必须包含大小写字母和数字的组合，可以使用特殊字符，长度在8-10之间)：`^(?=.\*\d)(?=.\*[a-z])(?=.\*[A-Z]).{8,10}$`
- 日期格式：`^\d{4}-\d{1,2}-\d{1,2}`
- 一年的12个月(01～09和1～12)：`^(0?[1-9]|1[0-2])$`
- 一个月的31天(01～09和1～31)：`^((0?[1-9])|((1|2)[0-9])|30|31)$`
- 钱的输入格式：
  1. 有四种钱的表示形式我们可以接受:"10000.00" 和 "10,000.00", 和没有 "分" 的 "10000" 和 "10,000"：`^[1-9][0-9]\*$`
  2. 这表示任意一个不以0开头的数字,但是,这也意味着一个字符"0"不通过,所以我们采用下面的形式：`^(0|[1-9][0-9]\*)$`
  3. 一个0或者一个不以0开头的数字.我们还可以允许开头有一个负号：`^(0|-?[1-9][0-9]\*)$`
  4. 这表示一个0或者一个可能为负的开头不为0的数字.让用户以0开头好了.把负号的也去掉,因为钱总不能是负的吧。下面我们要加的是说明可能的小数部分：`^[0-9]+(.[0-9]+)?$`
  5. 必须说明的是,小数点后面至少应该有1位数,所以"10."是不通过的,但是 "10" 和 "10.2" 是通过的：`^[0-9]+(.[0-9]{2})?$`
  6. 这样我们规定小数点后面必须有两位,如果你认为太苛刻了,可以这样：`^[0-9]+(.[0-9]{1,2})?$`
  7. 这样就允许用户只写一位小数.下面我们该考虑数字中的逗号了,我们可以这样：`^[0-9]{1,3}(,[0-9]{3})\*(.[0-9]{1,2})?$`
  8. 1到3个数字,后面跟着任意个 逗号+3个数字,逗号成为可选,而不是必须：`^([0-9]+|[0-9]{1,3}(,[0-9]{3})\*)(.[0-9]{1,2})?$`
  9. 备注：这就是最终结果了,别忘了"+"可以用"*"替代如果你觉得空字符串也可以接受的话(奇怪,为什么?)最后,别忘了在用函数时去掉去掉那个反斜杠,一般的错误都在这里
- xml文件：`^([a-zA-Z]+-?)+[a-zA-Z0-9]+\\.[x|X][m|M][l|L]$`
- 中文字符的正则表达式：`[\u4e00-\u9fa5]`
- 双字节字符：`[^\x00-\xff] `(包括汉字在内，可以用来计算字符串的长度(一个双字节字符长度计2，ASCII字符计1))
- 空白行的正则表达式：`\n\s\*\r` (可以用来删除空白行)
- HTML标记的正则表达式：`<(\S\*?)[^>]\*>.\*?|<.\*? />` ( 首尾空白字符的正则表达式：^\s\*|\s\*$或(^\s\*)|(\s\*$) (可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式)
- 腾讯QQ号：`[1-9][0-9]{4,} `(腾讯QQ号从10000开始)
- 中国邮政编码：`[1-9]\d{5}(?!\d) `(中国邮政编码为6位数字)
- IPv4地址：`((2(5[0-5]|[0-4]\d))|[0-1]?\d{1,2})(\.((2(5[0-5]|[0-4]\d))|[0-1]?\d{1,2})){3}`

## 五、RegExp对象方法

### 1.exec()

exec()方法用于检索字符串中正则表达式的匹配，如果字符串中有匹配的值，则**返回该匹配值构成的数组**，且该数组还有继承的属性：

- index：表示第一个匹配的字符在原字符串中的位置
- input：表示原字符串

```js
// 声明一个字符串
let str = '<a href="http://www.atguigu.com">尚硅谷</a>'

// 提取url与标签文本
const reg = /<a href="(.*)">(.*)<\/a>/;

const result = reg.exec(str)   // 检索字符串中正则表达式的匹配
console.log(result)
```

![image-20230201163407073](https://gitee.com/v876774538/my-img/raw/master/image-20230201163407073.png)

说明：

> 数组第一个元素是与正则表达式相匹配的文本；
>
> 第二个元素是与RegExp对象的第一个子表达式（**分组小括号里面的**）相匹配的文本；
>
> 第三个元素是与RegExp对象的第二个子表达式相匹配的文本，以此类推……

获取url参数：

```js
/**
 *   获取url中的参数
 * @param key  待匹配的关键字
 * @param url  被匹配查询的url
 */
export function getUrlQuery(key, url) {
    let str = url || window.location.href //默认获取浏览器地址栏中的url
    let reg = decodeURIComponent((new RegExp('[?|&|/]' + key + '=([^&;]+?)(&|#|;|$)').exec(str) || [, ''])[1].replace(/\+/g, '%20')) || null
    return reg
}
```

### 2.test()

`test()`正则对象方法，用于监测字符串是否符合该规则（**测试正则表达式**），该对象会返回true或false，其参数是测试字符串。

```js
regexObj.test(str);
```

- regexObj：正则表达式；
- str：需要测试的字符串；
- 检测str文本是否符合我们写的正则表达式规范。

**校验手机号**：

```js
let regPhone = /^1[3456789]\d{9}$/;
if (this.utils.isNone(this.account)) {
	this.$Message.info("请输入手机号码");
	return false;
} 
else if (!regPhone.test(this.account)) {
	this.$Message.info("手机号码格式有误");
	return false;
}
```

## 六、支持正则表达式的String对象方法

### 1.replace()

replace()方法可以实现**替换**字符串操作，用来替换的参数可以是一个字符串或是一个正则表达式。

```js
stringObject.replace(regexp/substr, replacement);
```

- regexp/substr：需要被替换的**字符串**或**正则表达式**；
- replacement：替换为的字符串；
- 返回值是一个替换完毕的新字符串。

正则表达式参数：

```js
/表达式/[switch]
```

switch（也称为修饰符），表示按照什么模式来匹配：

- `g`：全局匹配；
- `i`：忽略大小写；
- `gi`：全局匹配且忽略大小写；
- `s`：使`.`可以匹配任意字符，ES9引入了新的修饰符`s`（**dotAll模式**），此先.只能匹配除`\n`以外的任意字符。

**敏感词过滤**

```js
<textarea name="" id="message"></textarea>
<button>提交</button>
<div></div>

<script>
	var text = document.querySelector('textarea');
	bar btn = document.querySelector('button');
	var div = document.querySelecor('div');
	
	btn.onclick = function() {
		div.innerHTML = text.value.replace(/激情|gay/g,'**');
	}
</script>
```

**去除首尾空格**

1. jquery
   
   - `trim()`
2. js
   - 去除首尾空格：`replace(/^\s*|\s*/g, '')`
   
   - 去除首部空格：`replace(/^\s*/g,'')`
   
   - 去除尾部空格：`replace(/\s*$/g,'')`
   
   - `trim() trimStart() trimEnd()`
   
     | 方法      | 说明                                                         |
     | --------- | ------------------------------------------------------------ |
     | trim      | 删除字符串的头尾空白符，空白符包括：空格、制表符tab、换行符等 |
     | trimStart | 删除字符串头部空白符                                         |
     | trimEnd   | 删除字符串尾部空白符                                         |
   
     ```js
     let str = '          i love u       '
     
     console.log(str)
     console.log(str.trim())
     console.log(str.trimStart())
     console.log(str.trimEnd())
     ```
   
     ![image-20230201175235382](https://gitee.com/v876774538/my-img/raw/master/image-20230201175235382.png)

### 2.search()

用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串。→ **判断是否存在某个子串**

若找到任何匹配的子串，则返回**该子串在原字符串中第一次出现的位置**；若没有找到任何匹配的子串，返回-1。

```js
var str1 = 'hello 123 world 456';
var reg1 = /d+/; 
console.log(str1.search(reg1));//6
console.log(str1.search("world"));//10
var str2 = 'hello world';
var reg2 = /d+/;
console.log(str2.search(reg2));//-1
console.log(str2.search("nihao"));//-1
```

### 3.split()

用于把一个字符串按符合匹配条件的方式**分割**成一个字符串数组。**不改变原字符串**。

```js
var str="How 1are 2you 3doing 4today?";
var a=str.split(" ");
var b=str.split(" ",2);
var c=str.split(/d/);
var d=str.split(/d/,3);
console.log(a);//["How", "1are", "2you", "3doing", "4today?"]
console.log(b);//["How", "1are"]
console.log(c);//["How ", "are ", "you ", "doing ", "today?"]
console.log(d);//["How ", "are ", "you "]
```

### 4.match()

match()方法可在字符串内检索指定的值，或找到**一个或多个**正则表达式的匹配。

这个方法的行为在很大程度上有赖于 regexp 是否具有全局标志`g`。

- 如果 regexp 没有标志`g`，那么 match() 方法就只能在 stringObject 中执行一次匹配，**与exce的完全一致。**
- 如果 regexp 有标志`g`，它将找到全部符合正则子字符串，并返回一个数组；如果没有找到任何匹配的文本，无论有没有g，match() 将返回 null。

```js
var str = "Hello45647 123 world!Hello 1423 world! ssfsdf";
var reg1 = /\d+/;
var result1 = str.match(reg1);
console.log(result1)
var reg2 = /\d+/g;
var result2 = str.match(reg2);
console.log(result2)
```

![image-20230201164851320](https://gitee.com/v876774538/my-img/raw/master/image-20230201164851320.png)

### 5.matchAll()

matchAll() 方法返回一个包含所有匹配正则表达式的结果及其分组捕获组的**迭代器**

```js
var str = "Hello45647 123 world!Hello 1423 world! ssfsdf";
var reg = /\d+/g;
var result = str.matchAll(reg);
console.log(result)
// 1. 遍历 -------------------
for(let v of result) {
    console.log(v)
}

// 2. 拓展运算符 --------------
console.log(...result)

// 3. Array.from() -----------
var arr = Array.from(result)    // 将类数组转换为真正的数组
console.log(arr)
```

## 七、断言

断言可以帮助我们查找某些内容时，对内容前和内容后的信息作为判断（但并不包括这些内容）（把内容前或后的信息作为判断依据但结果不包括这些内容，所以也被称为**零宽断言**）

```js
var str = "我是小明我是小王我是小绿"
var reg = /我是(?=)小明/
console.log(str.replace(reg, '我不是')	// 将后面跟着'小明'的'我是'替换为'我不是'
```

1. 断言的写法
   - `VVV(?=XXX)` 零宽正先行断言（正向断言）：只有在**断言XXX在VVV的后边**时，才会继续匹配
   - `VVV(?!XXX)` 零宽负先行断言（正向断言）：只有在**断言XXX不在VVV的后边**时，才会继续匹配
   - `(?<=XX)VVV` 零宽正后发断言（反向断言）：只有在**断言XX在VVV的前边**时，才会继续匹配
   - `(?<!XX)VVV` 零宽负后发断言（反向断言）：只有在**断言XX不在VVV的前边**时，才会继续匹配
2. 注意
   - 断言不占用字符串，不被包括在内容中；
   - 断言一定要写在括号()中

