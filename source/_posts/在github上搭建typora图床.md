---
title: 在github上搭建typora图床
date: 2019-11-27 09:03:22
tags:
- typora
copyright: true
categories: 工具
mathjax: true
---

**前言**

> 图床是指存储图片的服务器，简单来说，就是一个保存图片的仓库，将图片上传到这个仓库后，我们可以用一个URL地址来查看这张图片。

<!-- more -->

### 为何要使用图床

最近用typora写博客，需要插入大量的截图，使用这些截图时，一般有两种方式，一是将截图先保存到本地，然后在typora中出插入图片的本地路径，另外一种是将图片放在我写的博客的相同路径下，在拖到相应的md文件中。但是，本地路径获取图片不太靠谱，一旦我的图片改变路径了，博客中就没法显示，我用的是第二种，但是这种会造成增加文件的体积，博客越来越多时，上传到博客的速度也会变慢。所以我开始考虑选择使用图床。

国内有很多免费图床，但是我都不太放心，毕竟一旦这些图床挂掉了，我博客里的图片就无法显示了。所以，我选择自己在github上自己搭建图床，比较靠谱。

### 在GitHub中创建项目

在前言中提到图床起始就是一个保存图片的库，所以，首先我们需要用github创建一个图片库来保存我们的图片。

没有使用过github的首先需要在注册[GitHub账号](https://github.com/)，很简单，就部介绍了。登陆后点击主页面右上角的加号，选择“New repository”:

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/%E5%88%9B%E5%BB%BArepository.png)

在建库页面，进行相关的设置：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/%E5%BB%BA%E5%BA%93%E9%A1%B5%E9%9D%A2%E8%AE%BE%E7%BD%AE.png)

建好的页面是这个样子的：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/%E5%88%9B%E5%BB%BA%E5%A5%BD%E7%9A%84%E4%BB%93%E5%BA%93.png)

创建好后，需要在GitHub上生成一个token以便PicGo来操作我们的仓库。点击GitHub页面右上角的头像，选择“settings”，在跳转的页面中选择左侧栏的“Developer settings”：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/DeveloperSettings.png)

在跳转的页面中选择“Personal access tokens”，然后点击右上角的“Generate new token”创建一个新的token：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/PersonalAccessTokens.png)

填写Note，勾选上的repo，然后点击最下方的“Generate token”绿色按钮：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/%E5%88%9B%E5%BB%BAtoken.png)

下面就是生成的token，记得点击红框中右侧的按钮，复制保存到其他地方，这个token只显示一次。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/%E5%A4%8D%E5%88%B6token.png)

### 安装配置PicGo

PicGo是一款简易的图床上传工具，可以通过拖拽或者复制粘贴的方式将图片上传至图床，下载地址：https://github.com/Molunerfinn/PicGo/releases/tag/v2.1.2：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/%E4%B8%8B%E8%BD%BDPicGo.png)

正常安装下载好的PicGo，打开后界面如下：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/picgo%E7%95%8C%E9%9D%A2.png)

点击左边栏的【图床设置】-【GitHub图床】，将我们在GitHub上建的图片仓库与之绑定，如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/picgo%E8%AE%BE%E7%BD%AE.png)

设置完成后点击确定即可完成绑定，然后点击【设为默认图床】。

### 使用

点击PicGo左侧的上传，然后点击【上传区】，将本地图片拖上去，或者在截图之后，点击剪贴板图片上传，然后会默认生成链接，直接在typora中复制链接就行。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/%E4%B8%8A%E4%BC%A0%E5%9B%BE%E7%89%87.png)

上传完成后，可以在PicGo的相册和GitHub的仓库中看到上传的照片了。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/GitHub%E7%9B%B8%E5%86%8C.png)

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/GitHub%E5%9B%BE%E5%BA%93%E7%95%8C%E9%9D%A2.png)

另外，直接上传截图的话，是没有命名的，我们可以在相册里给图片重新命名：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/%E6%88%AA%E5%9B%BE%E5%91%BD%E5%90%8D.png)

另外，我们也可以在【PicGo设置】中，设置图片上传前重命名：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%9C%A8git2ub%E4%B8%8A%E6%90%AD%E5%BB%BAtyporpm%E5%9B%BE%E5%BA%8A/picgo%E9%87%8D%E5%91%BD%E5%90%8D%E8%AE%BE%E7%BD%AE.png)

同时，还可以选中多张图片批量上传。