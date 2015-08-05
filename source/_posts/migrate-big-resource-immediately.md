title: 如何『瞬间』迁移在用大资源 
layout: post
date: 2015-08-05 21:49:56
tags:
- migration 
categories:
- backend
---

> 想像一下，目录/var/www/app/public/upload被用于资源上传存放。
起初，用户量不大，看起来没什么问题。可是用户越来越多了，这里的空间越占越大，慢慢地接近100%。

此时，我们需要将这些资源转移：
* 将资源转移到另一大磁盘，如：/data下（简单，影响小）
* 转移到云存储服务（七牛，阿里云等）（麻烦，牵动大）【其实一开始就应该使用云服务】

现阶段，我选了前者；当然，对于改革，我从未放弃。

考虑到/var和/data是两个不同文件系统。
> 假设使用：
* mv /var/www/app/public/upload /data/resource/upload
* ln -s /data/resource/upload /var/www/app/public/upload
则会在mv会先拷贝，再将原有文件删除，整个过程漫长之极，即便选择访问最少时间段，也容易造成影响。

显然，这方法不靠谱；最后，我的做法是这样的：
```bash
#!/bin/bash
rsync -av /var/www/app/public/upload /data/resource/
rsync -av /var/www/app/public/upload /data/resource/
mv /var/www/app/public/upload /var/www/app/public/upload.bk
ln -s /data/resource/upload /var/www/app/public/upload
```

> 因为前面已经做了第一次rsync，第二次rsync其实速度会非常快（几乎瞬间），此时将mv移动到同目录下（同文件系统），其实是重命名（也是瞬间），最后，ln软链回去（同时也是瞬间完成）

job done!
