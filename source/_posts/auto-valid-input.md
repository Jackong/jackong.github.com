title: 让参数校验自动化
layout: post
date: 2015-08-02 21:31:35
tags:
- node.js
- php
categories:
- backend
---

每次看到其它开发人员，在打一些重复的代码，我都有种深恶痛绝，不想参与进去的想法，隐隐感觉会被对方拖垮我的效率。

<!-- more -->

### 最常见的参数校验

* 我想，这是最常见的做法（我称之为CIERR[Check-If-Error-Return-Repeatedly]）：

``` js
if (!data.account) {
	//...
}
if (data.account.length < 3) {
	//...
}
if (!isEmail(data.account)) {
	//...
}

if (!isMobilePhone(data.account)) {
	//...
}

if (!isXXX(data.account)) {
	//...
}

//do something
```

* 然而，这些其它都可以被自动化，简化，使我们的代码更专注于业务逻辑的开发：

``` js
//It will throw exception if the account is invalid.
//And, the isValidAccount can be reused.
var account  = input(data, 'account', isValidAccount, /*default value*/, error);
//do something
```
> 其中，
data为数据源；
account为data的key；
isValidAccount是一个pattern，支持RegExp|Array|Function|Object|String；
第3个参数是默认值，可用于在校验失败时，给予返回；
error是但校验失败是throw的error信息。

最后，我封装了一个js通用的module：[no-input][no-input-url] 和一个koa的middleware：[koa-input][koa-input-url]。

你会发现，一切都是那么自然，简洁，并强大。

[no-input-url]: https://github.com/Jackong/no-input
[koa-input-url]: https://github.com/Jackong/koa-input
