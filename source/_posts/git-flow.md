title: git开发流
date: 2016-01-07 18:15:43
tags: [git]
categories: develop
thumbnailImage: http://7xkwtq.com1.z0.glb.clouddn.com/git.png
---

规范流程，高效开发

<!-- more -->

![](http://nvie.com/img/git-model@2x.png)

# 流程，分支，环节

* `master` 待上线状态
  * 合并来自`release`或`hotfix`的代码

* `develop` 下一版本功能开发状态
  * 合并来自`feature`,`release`或`hotfix`的代码

* `feature*` 某个功能模块
  * 从`develop`分支切出，完成后合并回`develop`分支

* `release*` 准备发布的版本
  * 该版本所有`feature*`完成后
  * 从`develop`分支切出，完成后合并到`develop`及`master`
  * 打版本tag，用于记录版本迭代，发布更新或回滚代码

* `hotfix*` 修复bug分支
  * 从`master`分支切出，完成后合并到`master`及`develop`
  * 打版本tag，用于记录版本迭代，发布更新或回滚代码

----

# 参考：
* [a successful git branching model](http://nvie.com/posts/a-successful-git-branching-model/)
* [why arent you using git flow](http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/)
* [git flow](https://github.com/nvie/gitflow)
