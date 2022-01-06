---
title: Typora主题美化
date: 2019-11-26 15:18:37
tags:
- Typora
copyright: true
categories: 工具
mathjax: true
---

**前言**

> Typora是一款非常好用的makedown文本编辑器，界面简单干净，所见即所得，所以在记笔记写博客时是一款非常好用的工具。当然了，一个好看的适合自己的主题，会让自己在写作时赏心悦目。这篇文章是根据我自己的风格和喜好，在typora官网night主题的基础上，结合catfish主题的优点，进行的一些调整，注意是字体上的调整。

<!-- more -->

### 偏好设置

首先我们打开typora，选择【文件】-【偏好设置】-【外观】

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/typora%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96/%E5%81%8F%E5%A5%BD%E8%AE%BE%E7%BD%AE1.png)

点击上面图片的【打开主题文件夹】，会直接跳到本地你的typora主题文件夹，包括各个主题的文件夹，和各个主题的css文件：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/typora%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96/%E4%B8%BB%E9%A2%98%E6%96%87%E4%BB%B6%E5%A4%B9.png)

点击偏好页面的【获取主题】，将会跳转到[typora主题官网](http://theme.typora.io/)，我们可以在这个网站上找到我们心仪的主题：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/typora%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96/%E4%B8%BB%E9%A2%98%E7%BD%91%E7%AB%99.png)

### night和catfish主题

我比较喜欢night的全黑界面，但是nigth默认的字体是宋体，不是很好看，例如：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/typora%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96/night%E4%B8%BB%E9%A2%98.png)

官网上的另一个主题catfish，其官方说明是：

> 无衬线字体，衬线字体和等宽字体分别采用思源黑体，思源宋体， mononoki ，在 Windows 下有良好的中文呈现效果。

但是，catfish的页面是白色的，我不喜欢白色，看长了时间眼睛会累，另外，它的代码块字体我也不是很喜欢，还是比较喜欢night主题的代码块，而且，catfish主题的表格样式没有竖线，我也不喜欢，所以，综上来看，除了catfish主题的正文字体，我还是比较喜欢night主题的风格，所以，我决定在night主题的基础上进行修改，这样修改的幅度较小。

### 修改night主题

由于只需要catfish主题中的字体，而catfish中自带了思源黑体、思源宋体、mononoki字体文件，我们可以直接下载这些字体，这里我为了方便就直接下载catfish主题了：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/typora%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96/catfish%E4%B8%BB%E9%A2%98%E4%B8%8B%E8%BD%BD.png)

解压下载下来的catfish主题文件，打开catfish文件夹，可以看到下面有很多字体文件：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/typora%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96/%E5%AD%97%E4%BD%93%E6%96%87%E4%BB%B6.png)

依次右键ttc和otf文件，并点击安装，至于woff字体文件，我也不知道在win10上怎么安装（恕我无能-_-），不过也没关系，我们在catfish中发现，也只有一处用到了这个字体，所以就直接忽略吧。安装完字体后，我们可以在C:\Windows\Fonts这个路径中发现多了思源黑体和思源宋体文件。

最后，我们打开night主题的样式文件night.css，这里我建议复制该样式文件，重命名为“my-night.css”,为了防止我们将该样式文件改崩了，然后我们在my-night.css中进行修改，搜索“font-family”，将每个font-family后面的字体都替换成“Source Han Sans SC, sans-serif”，例如，修改正文字体：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/typora%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96/%E5%AD%97%E4%BD%93%E6%9B%BF%E6%8D%A2.png)

### 主题选择

重启typora，在菜单栏点击【主题】，可以发现，在下拉菜单中会多出一个“my night”的主题，选择改主题，可以发现在night主题的基础上，字体变好看了：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/typora%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96/mynight%E4%B8%BB%E9%A2%98.png)

当然了，如果在这个主题样式中，依旧有不满意的，可以继续修改，比如字体大小、代码块样式等，本人没学过css，所以就不继续瞎改了。

