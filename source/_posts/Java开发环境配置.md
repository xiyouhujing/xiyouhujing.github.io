---
title: Java开发环境配置
date: 2019-09-27 17:17:36
tags:
- JDK
- eclipse
copyright: true
categories: Java
mathjax: true
---

**前言**

> 下载安装java开发工具JDK，以及进行环境的配置，下载安装java开发的ide，因为eclipse是使用较为广泛的java开发ide，所以这里安装的是eclipse。另外，也可以了解一下IntelliJ IDEA（收费的），我觉得IDEA用得更顺手。当然了，都只是开发工具，看拿个更适合自己吧，用得开心就行。

<!-- more -->

### 下载安装JDK

1.JDK是Java开发工具，下载地址为：https://www.oracle.com/technetwork/java/javase/downloads/index.html ，点击如下图片中的按钮：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/JDK%E4%B8%8B%E8%BD%BD1.png)

2.在跳转的页面中选择接受许可，之后根据自己的系统选择对应的安装程序，本文window 64为例，如下：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/JDK%E4%B8%8B%E8%BD%BD2.png)

3.双击安装文件，然后提示的安装步骤进行安装即可，可以修改JDK的安装路径，例如我的安装路径为：D:\JDK，记住安装路径，在接下来配置环境变量中需要用到。

### 配置环境变量

1.安装完成后，邮件“我的电脑”/“此电脑”，点击“属性”，选择“高级系统设置”，如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F1.png)

2.选择“高级”选项卡，点击“环境变量”，如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F2.png)

3.在“系统变量”中分别设置JAVA_HOME、CLASSPATH、PATH三个属性，如果三个属性不存在，则新建，存在则选定后编辑，变量参数设置如下：

|  变量名   | 变量值                                                       |
| :-------: | :----------------------------------------------------------- |
| JAVA_HOME | D:\JDK      (根据自己的安装路径选择)                         |
| CLASSPATH | .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;   （注意最前面有.; 符号用英文） |
|   PATH    | %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin  （win10中双击PATH后分条添加，否则无法识别） |

### 测试JDK是否安装成功

1.ctrl+R，在弹出的对话框中输入cmd，回车。

2.在弹出的命令框中，输入java -version命令，如果出现如下结果，则说明java环境配置成功：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/%E6%B5%8B%E8%AF%951.png)

### 安装Eclipse

目前市场上用于java开发的IDE比较多，比较推荐Eclipse和IntelliJ IDEA，IDEA功能很强大，但是要收费，Eclipse是免费开源的java开发工具，也是目前使用较多的开发工具，所以这里推荐安装Eclipse。

1.下载eclipse的安装文件，下载地址为：https://www.eclipse.org/downloads/packages/ ，选择Eclipse IDE for Committers，并根据自己的电脑系统选择相应的版本，本次选择windows 64：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/%E4%B8%8B%E8%BD%BDeclipse.png)

2.在跳转的界面中，默认的下载地址是日本一所大学，此时点击“select another mirror”，然后将页面往下拉，选择中国的镜像，这样下载速度较快，这里选择大连东软信息学院或者中国科技大学镜像，如下：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/%E9%80%89%E6%8B%A9%E9%95%9C%E5%83%8F.png)

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/%E9%80%89%E6%8B%A9%E9%95%9C%E5%83%8F2.png)

3.选择镜像之后，开始下载，下载完成后的文件名为eclipse-committers-2019-09-R-win32-x86_64.zip，解压，运行eclipse.exe。按照步骤安装。