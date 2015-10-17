layout: post
date: 2015-07-31 15:54:58
title: 使用React构建Web App
tags: [react, web-app]
category: frontend
thumbnailImage: https://www.codementor.io/assets/tutorial_icon/reactjs.png
---

### 从Angular到React
> 在使用React之前，我兴奋地使用着Angular。

<!-- more -->

* 它们的区别
	* Angular是一个全能框架。（MVVM）
	* 而React则不是，它只是一个View，一个模块。
	* 使用它，你还有依赖其它第三方模块。如：HTTP请求模块[Axios][Axios-url]，Flux单向数据流模块[Reflux][Reflux-url]等等。

[Axios-url]: https://github.com/mzabriskie/axios
[Reflux-url]: https://github.com/spoike/refluxjs

* 看中React的理由
	* 移动开发（[React-Native][React-Native-url] 一处编码，到处运行；一门语言，全端开发）
	* 廉价的渲染能力（[virtual-dom][virtual-dom-url]）
	* 模块化（像写Node.js写前端代码，在我的经历中，前端的代码总是看起来很混乱，缺少后端开发者的思想）
	* 职责单一（一个模块做一件事，插件式开发，专业灵活）
	* 组件化（实现view层的可复用性）

[React-Native-url]: https://facebook.github.io/react-native
[virtual-dom-url]: https://github.com/Matt-Esch/virtual-dom

-----

### React的『坑』，一个萝卜一个坑
> 没有无坑的『萝卜』，也没有填不了的坑。

* 优点也会是『坑』
	* 因为render太廉价，所以在使用[react-route][react-route-url]时，只要url一变化，React都会re-render。
	这就导致了当浏览器back历史的时候，也会被重新渲染！
	数据会重新请求，页面位置被重置（当数据请求没那么快时），完全没有cache。

* but，换一种思维开发，那不算坑
	* 你是否知道AMD，CMD，Gulp，Webpack，SASS，DI，Promise，Data-Flow，Generator-Function 这些利器？
	* 如果你还停留在JQuery的年代，那是你给自己挖的坑。哦，不，是井。

[react-route-url]: https://github.com/rackt/react-router

-----

### 路在哪，走出来
> 路是人走出来的。

将React应用在微信公众号项目上，已快上线了。
然而，这只是第一步。
