# React

## 一、React简介

1. 简介

   > React是一个将数据渲染为HTML视图的开源**JavaScript库**。

2. 历史

   由Facebook开发，且开源。

   - 期初由Facebook的软件工程师Jordan Walke创建；
   - 于2011年部署于Facebook的newsfeed；
   - 随后在2012年部署于Instagram；
   - 2013年5月宣布开源
   - ……

3. 必要性

   - 原生JavaScript操作DOM繁琐、效率低；

     ```js
     document.getElementById('app')
     document.querySelector('#app')
     document.getElementsByTagName('span')
     ```

   - 使用JavaScript直接操作DOM，浏览器会进行大量的**重绘重排**；

   - 原生JavaScript没有**组件化**编码方案，代码复用率低

4. 特点

   - 采用**组件化**模式、**声明式编码**，提高开发效率及组件复用率；
   - 在React Native中可以使用React语法进行**移动端开发**；
   - 使用**虚拟DOM**和优秀的**Diff算法**，尽量减少与真实DOM的交互。



