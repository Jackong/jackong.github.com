title: 在react中使用css
description: inline styles
date: 2015-09-17 10:46:39
tags: [react, css]
categories: frontend
---

## 传统的css
---

* 一般是在html里面引入一个.css文件，或者写入一段
```html
<style>...</style>
```

* 它没有变量，没有什么function，总之，够用，但不够强大、高效

## 进化的css
---

* 为了给css赋予更强大的力量，就有了[less](http://lesscss.org/), [sass/scss](http://sass-lang.com/)

* 这显然已经足够强大了，但依然没有解决另外一些问题
    * 全局命名空间
    * css名称不好压缩，一般css的压缩也只是去掉空格注释，而class，id之类的命名还是被保留
    * 在组件化的时代，把css单独开来不好管理，维护和复用
    * ...

## inline styles
---

* facebook的解决方法[react-css-in-js](https://speakerdeck.com/vjeux/react-css-in-js)

* 于是，在react的世界里，便有了这些优秀的开源项目来尝试解决这些问题
    * [react-style](https://github.com/js-next/react-style)
    * [radium](https://github.com/FormidableLabs/radium)
    * [reactcss](https://github.com/casesandberg/reactcss)

> WEB的世界很精彩，WEB的世界很惊人
