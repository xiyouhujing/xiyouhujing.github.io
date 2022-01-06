---
title: JMeter安装与使用
date: 2019-09-27 16:54:13
tags:
- JMeter
copyright: true
categories: 测试
mathjax: true
---

**前言**
> JMeter是基于Java的测试工具，主要对web应用和软件进行接口测试和压力测试。
<!-- more -->



### 安装前准备

在安装配置JMeter之前，需要确定电脑是否安装有Java环境，可以利用命令提示符查验：

1.ctrl + R，之后输入cmd，在弹出的命令行窗口中输入java -veision，如果出现如下结果，则表明电脑中存在Java环境，接下来便可以进行JMeter的安装：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/cmd%E6%88%AA%E5%9B%BE.png)

2.如果电脑中没有java环境，则首先要下载和配置java的开发工具包JDK，具体步骤参考：[https://xiyouhujing.github.io/2019/09/27/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE/](https://xiyouhujing.github.io/2019/09/27/Java开发环境配置/)

### Jmeter下载

1.进入Jmeter官网http://jmeter.apache.org/，点击如下按钮：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E5%AE%98%E7%BD%91%E4%B8%8B%E8%BD%BD.png)

2.在跳转的页面中选择版本下载，如图我选择下载的为zip压缩文件：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E4%B8%8B%E8%BD%BD%E5%8E%8B%E7%BC%A9%E6%96%87%E4%BB%B6.png)

3.将下载下来的压缩文件解压，记住文件的路径，本文的路径为：D:\Jmeter\apache-jmeter-5.1.1。另外，因为下载下来的是jmeter5.1，需要注意的是对应的jdk版本不能太低。

### Jmeter环境变量配置

1.右键“我的电脑”/“此电脑”，点击“属性”，选择“高级系统设置”：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F1.png)

2.选择“高级”选项卡，点击“环境变量”：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F2.png)

3.在“系统变量”中，分别设置JMETER_HOME和CLASSPATH属性，如果属性不存在，则新建，存在则编辑，具体的参数如下：

|   变量名    | 变量值                                                       |
| :---------: | ------------------------------------------------------------ |
| JMETER_HOME | D:\Jmeter\apache-jmeter-5.1.1   （jmeter的解压路径）         |
|  CLASSPATH  | %JMETER_HOME%\lib\ext\ApacheJMeter_core.jar;%JMETER_HOME%\lib\jorphan.jar;%JMETER_HOME%\lib\logkit-2.0.jar; |

### 测试是否安装配置成功

1.进入jmeter的安装路径，进入bin文件夹，找到jmeter.bat：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%B5%8B%E8%AF%951.png)

2.双击jmeter.bat文件，此时会出现如下命令窗口，在jmeter工作期间，该窗口都不能关闭

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%B5%8B%E8%AF%952.png)

3.以上窗口正常出现后，稍等片刻会出现jmeter的工作界面，如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E5%B7%A5%E4%BD%9C%E7%95%8C%E9%9D%A2.png)

### 优化jmeter的使用

1.我们发现，每次需要使用jmeter的时候必须进入它的安装文件，再进入bin文件，双击jmeter.bat，这么操作比较麻烦。因此我们可以将该文件发送到桌面生成快捷方式：右键jmeter.bat—>发送到—>桌面快捷方式。

2.如果觉得发送到桌面的快捷方式图标不好看，和桌面其他快捷方式格格不入，我们还可以修改该快捷方式的图标：右键该快捷方式，选择属性，在出现的窗口中选择“快捷方式”选项卡，点击下方的“更改图标”按钮，如下：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%9B%B4%E6%94%B9%E5%BF%AB%E6%8D%B7%E6%96%B9%E5%BC%8F.png)

3.在弹出的窗口中可以选择系统自带的图标：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E4%BF%AE%E6%94%B9%E5%9B%BE%E6%A0%87.png)

4.如果想自定义一个图标，可以网上下载一个自己喜欢的图标，**保存为ico格式**，点击“更改图标”窗口的浏览按钮，选择自己想要的图标，点击确定，图标修改完成。

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E4%BF%AE%E6%94%B9%E6%88%90%E8%87%AA%E5%B7%B1%E5%96%9C%E6%AC%A2%E7%9A%84%E5%9B%BE%E6%A0%87.png)

5.如果使用默认的jmeter.bat启动的话，会出现一个CMD命令窗口之后再启动jmeter。如果不想每次点击jmeter的快捷方式都要打开命令窗口，可以进行如下修改：

右键jmeter.bat快捷方式，点击属性，修改目标和启始位置（**根据实际的jmeter解压路径填写**）：

目标：D:\Jmeter\apache-jmeter-5.1.1\bin\ApacheJMeter.jar

起始位置：D:\Jmeter\apache-jmeter-5.1.1\bin

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%9B%B4%E6%94%B9%E8%B7%AF%E5%BE%84.png)

**注意：默认ApacheJMeter.jar的打开方式是解压工具winrar，这里需要更改打开方式**

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%89%93%E5%BC%80%E6%96%B9%E5%BC%8F.png)

### 使用Jmeter进行测试

#### 更改JMeter默认语言

点击【options】>【choose language】变为简体中文，方便操作，如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%9B%B4%E6%94%B9%E8%AF%AD%E8%A8%80.png)

#### 创建线程组

1、在“测试计划”上右键，依次选择【添加】>【线程（用户）】>【线程组】

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E8%AE%BE%E7%BD%AE%E7%BA%BF%E7%A8%8B.png)

2、在线程组界面设置线程数和循环次数，我这里设置线程数为100，循环一次

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E8%AE%BE%E7%BD%AE%E7%BA%BF%E7%A8%8B2.png)

#### 添加HTTP请求默认值

1、在刚刚创建的线程组上右键，依次选择【添加】>【配置元件】>【HTTP请求默认值】

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E9%85%8D%E7%BD%AE%E5%85%83%E4%BB%B6.png)

2、在配置元件界面填写我们需要测试的程序协议、地址和端口，如下图所示：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E9%85%8D%E7%BD%AE%E5%85%83%E4%BB%B62.png)

#### 构造HTTP请求

1、在线程组上右键，依次选择【添加】>【取样器】>【HTTP请求】,如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%B7%BB%E5%8A%A0http%E8%AF%B7%E6%B1%82.png)

2、由于我们刚才在HTTP默认值中设置了默认路径，我们这里使用默认路径的话，就在http请求界面的路径中输入反斜杠“/”就行，如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%B7%BB%E5%8A%A0http%E8%AF%B7%E6%B1%822.png)

其中消息体数据根据实际情况填写，可以无参数。

#### 添加HTTP请求头

1、在线程组上右键，依次选择【添加】>【配置元件】>【HTTP信息头管理器】，如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/HTTP%E4%BF%A1%E6%81%AF%E5%A4%B4.png)

2、因为HTTP请求中没有传输数据，所以，这里设置为Content-Type:application/text（如果在HTTP请求中传入了数据，并且为json格式的数据，则可以设置为Content-Type:application/json）

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/HTTP%E4%BF%A1%E6%81%AF%E5%A4%B42.png)

#### 添加断言

1、在线程组上右键，依次点击【添加】>【断言】>【响应断言】，如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%96%AD%E8%A8%80.png)

2、根据响应的数据来判断请求是否正常。这里只判断的响应代码是否为200。还可以配置错误信息，如下图所示：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E6%96%AD%E8%A8%802.png)

#### 察看结果树

1、在线程组上右键，依次选择【添加】>【监听器】>【察看结果树】

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/JMeter%E5%AE%89%E8%A3%85%E4%B8%8E%E4%BD%BF%E7%94%A8/%E5%AF%9F%E7%9C%8B%E7%BB%93%E6%9E%9C%E6%A0%91.png)

2、点击运行按钮便可查看结果

