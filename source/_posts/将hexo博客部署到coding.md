---
title: 将hexo博客部署到coding
date: 2019-11-25 10:31:51
tags:
- hexo
- coding
copyright: true
categories: 工具
mathjax: true
---

**前言**

> 在将hexo博客部署到coding之前，我已经在github上部署过，但是考虑到github是国外网站，每次打开博客访问较慢，而coding是国内网站，速度肯定快一些。所以，在部署到github的基础上，我又将hexo博客部署到coding上。coding pages是国内有名的软件研发管理平台coding旗下的一个功能，可以实时发布在coding.net里托管的代码。

<!-- more -->

#### 注册Coding账号

进入[coding官网](https://coding.net/)，点击右上角的注册按钮，注意不要点个人版登陆来注册，我试过个人版，部署到个人版之后，页面会显示404，所以直接注册就行，团队名称自己随意设置。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/%E6%B3%A8%E5%86%8C1.png)

#### 创建项目

注册后登陆，在项目页面点新建项目：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE1.png)

创建项目页面，项目名称随便填，项目地址格式为：你的域名.coding.me。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE2.png)

#### 配置SSH公钥

点击coding页面右上角的头像，选择个人设置，点击SSH公钥，再点击右上角的新增公钥：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/%E6%96%B0%E5%A2%9E%E5%85%AC%E9%92%A51.png)

如果之前没有部署到github，可以点击上面图片中的“点击查看SSH公钥使用办法”来生成公钥。我这里之前部署到github了，可以使用同一个公钥，在本地文件夹C:\Users\你的user名\\.ssh中，找到id_rsa.pub文件，并将其内容复制到如下页面，记得勾选上永久有效，最后点添加：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/%E6%96%B0%E5%A2%9E%E5%85%AC%E9%92%A52.png)

#### 配置站点配置文件

打开coding中的你的项目，右下角选择SSH，复制SSH后面的地址：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/SSH%E5%9C%B0%E5%9D%80.png)

打开站点配置文件_config.yml（注意非主题配置文件），搜索deploy，在后面添加coding: 你的项目SSH地址。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/%E7%AB%99%E7%82%B9%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E4%BF%AE%E6%94%B9.png)

配置完成后，在git中依次执行以下命令：

```
hexo clean
hexo g
hexo s
```

显示如下表示成功：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/push%E5%92%8Cdeploy.png)

部署成功之后，coding项目中可以查看部署成功的代码：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/%E6%9F%A5%E7%9C%8B%E6%88%90%E5%8A%9F%E9%83%A8%E7%BD%B2%E7%9A%84%E4%BB%A3%E7%A0%81.png)

#### 构建静态网站

进入项目页面-构建与部署-静态网站，点击新建（这里我之前已经为我的博客新建了静态网站，所以，下面会有一个静态网站）：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/pages%E6%9C%8D%E5%8A%A11.png)

在新建静态网站页面，填写网站名称，触发机制默认自动部署，选择推送到master时触发构建，填写完成后点保存：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/pages%E6%9C%8D%E5%8A%A12.png)

新建完成后回到静态网站页面，点击右下角的立即部署：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/%E5%B0%86hexo%E5%8D%9A%E5%AE%A2%E9%83%A8%E7%BD%B2%E5%88%B0coding/pages%E6%9C%8D%E5%8A%A13.png)

最后可以点击上面图片中的[访问地址](http://qtuuy5.coding-pages.com)来访问自己的博客。

