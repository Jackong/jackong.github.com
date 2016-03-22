title: 集成React Native到已有项目
date: 2016-03-21 11:16:51
tags: [react, iOS, android]
categories: [frontend]
thumbnailImage: http://7xkwtq.com1.z0.glb.clouddn.com/reactjs.png
---

问题与方案

<!-- more -->

# 吐糟

吾至转客户端已近一月，每每见开发时，需次次build来以见效果，深感此中低效。
又见App Store审核漫长，上版未过，下版即出，而android与iOS各分阵营，更是人力浪费。
痛定思痛，决意试引React Native，以便解决以上问题。
此行途中坑洼，随记一二，望能交流。

# 模块

因为是集成到已有项目，所以希望是先挑几个功能模块试点切入。
便有了分多模块开发的需要，首先想到的方案是使用多个bundle作为不同的模块（activity）。

* 问题

实践过程中却发现android上多个bundle时，开发模式下有个缓存的bug，导致无法正常使用多个bundle。
> 从服务端拉取的bundle缓存于本地同一文件。

* 方案：
  * 提交PR（已提）。
  * 临时处理（在开发模式下`onCreate`和`onDestory`时`mv/cp`缓存文件）。
  * 使用一个bundle（其实一个bundle就可以实现不同模块划分，而且对于同一APP更方便开发、管理和发布）。

# 升级

为了能够动态升级，我尝试了[CodePush](codepush.tools)。
CodePush操作简便（命令行模式），而且实用。

# 性能

* 问题
在android下，切换activity时，迅速滑动或点击等交互，可以明显感觉到有几百毫秒的`交互无响应`，推测是渲染期导致的。

* 方案
  * 避免使用过于复杂的界面
  * 性能优化（需具体分析）


# 结语

总之，坑不会少，但好处也很明显。看来，又免不了一场`恶战`，想想又该兴奋起来了。
