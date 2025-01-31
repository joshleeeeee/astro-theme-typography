---
title: 如何在个人博客(hexo)中放入图片
tags:
  - 杂谈
categories:
  - 常用工具
pubDate: 2023-09-13 15:12:47
---

这个问题的本质其实是在讨论如何将本地的图片上传到服务器中，并在 markdown 写作中引用已上传的图片。最理想的方式当然是：截图工具一截图，然后就直接把图片 `Ctrl V` 进文章中啦。那么具体如何做呢？本文将介绍两种方法

## 方法 1. Github + Typora

第一种方法是直接将图片存入 Github 的仓库中，这种方法最大的优点就是免费和可靠了，访问的速度也很快。缺点是 Repository 的存储空间不能太大，官方推荐是小于 1GB，如下面我从 [Github Docs](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#limits-on-use-of-github-pages) 中截的图。

![](https://josh-blog-images.oss-cn-shenzhen.aliyuncs.com/202309131331788.png)

如果一张图 1MB，那么大约可以放 1000 张图到 Repository 中， emmm这么算下来的话，其实大部分人使用肯定是戳戳有余了

众所周知，在用 hexo 写博客的时候，可以将图片放在 `source` 的文件夹内，然后用相对路径进行引用，比如将图片都放在 `./source/images` 中，如果你的文章是 `./source/_posts/xxx.md` 的话，可以在文章中使用类似于 `![](../images/xxx.png)` 的方式引用图片。最终 `hexo generate` 的时候会将你的 `images` 文件夹原封不动的放入 `./build` 文件夹，部署的时候也会将这些图片部署到 Github Repository 中。

利用这个hexo 的特性，我们就可以将 github 作为我们自己放文章图片的地方了。但这样的问题是，使用起来很是麻烦，要在文章中插入图片，首先要将截的图存入博客中专门放图片的文件夹如 `./source/images` ，还要将图片归个类...还要在 markdown 中写上插入图片的语法...这可太麻烦了。

于是我们可以使用 Typora 图片上传的特性完美解决这个痛点。打开 Typora 的 Setting，Image，选择 `Copy image to custom folder`，意思就是当插入图片的时候会将图片复制到指定的文件夹中，指定的那个文件夹我们用相对路径表示就行，如下图（请务必按照你自己的实际情况来配置）

![](https://josh-blog-images.oss-cn-shenzhen.aliyuncs.com/202309131442115.png)

最后大功告成啦，截个图，然后直接粘贴到 Typora 里就行。


## 方法 2. 阿里云 OSS + PicGo

第二种方法就是图床 + 图片上传工具啦，市面上的图床有很多，但免费的一些野鸡图床一般都很不稳定，比如随便谷歌或百度搜`免费图床`，会出来一大堆，具体稳定性如何，就需要大家自己去甄别了。

这里我只介绍我用的：阿里云 OSS 当图床，PicGo 当图片上传工具。

---

前往 [阿里云 OSS官网](https://www.aliyun.com/product/oss)，点击立即购买。然后按照下图购买方案即可，一年 9 块钱，也不算很贵

![](https://josh-blog-images.oss-cn-shenzhen.aliyuncs.com/202309131349982.png)

---

然后点击 Bucket 列表，创建 Bucket，填写 `Bucket 名称`、`地域`还有`读写权限`(改成公共读)，如下图

![](https://josh-blog-images.oss-cn-shenzhen.aliyuncs.com/202309131358364.png)

---

阿里云OSS 创建完之后，我们需要下载个图片上传的软件，[PicGo下载链接](https://github.com/Molunerfinn/PicGo/releases/)


如果 mac 下载安装完 PicGo，打开后提示「文件已损坏」的情况，可以按照以下方式操作：

---

信任开发者，会要求输入密码:

``` bash
sudo spctl --master-disable
```

然后放行 PicGo :

``` bash
xattr -cr /Applications/PicGo.app
```

然后就能正常打开。


---

打开PicGo 的主窗口，图床设置，阿里云 OSS

这里需要填入 `设定KeyId` 和 `设定KeySecret`，可以在「阿里云 -> 右上角头像 -> AccessKey 管理」中创建 `AccessKey`。

![](https://josh-blog-images.oss-cn-shenzhen.aliyuncs.com/202309131409613.png)

然后分别把刚刚在阿里云中创建的 `AssessKey ID`和 `AssessKey Secret` 填入PicGo中的 `设定KeyId` 和 `设定KeySecret` 。

> 记得把你自己的 `AssessKey ID`和 `AssessKey Secret` 妥善保管好

然后 `设定Bucket` 和 `设定存储区域` 根据自身情况填，可参考下图，最后按确定即可

![](https://josh-blog-images.oss-cn-shenzhen.aliyuncs.com/202309131258387.png)

使用起来就非常方便了，用微信、Snipaste 等一些截图工具，截图后直接在状态栏中点 PigGo 的图标就能上传啦~上传成功后会自动将 markdown 格式的图片复制到你的剪贴板，直接粘贴进你 `.md` 即可

软件具体的操作细节可以自己探索，很简单的

![](https://josh-blog-images.oss-cn-shenzhen.aliyuncs.com/202309131414529.png)

