---
title: Java笔记：Java新特性对数组的支持
date: 2019-04-05 18:10:19
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

### Java新特性——可变参数

在调用一个方法时，必须根据方法的定义传递指定的参数，但是在JDK 1.5（JAVA SE 5.0）之后产生了新的概念——可变参数，即方法中可以接收的参数不再是固定的，而是随着需要传递的，可变参数的定义格式如下：

<!-- more -->

~~~
返回值类型 方法名称(类型...参数名称){}
~~~

向方法中传递可变参数后，其中的参数是以数组的形式保存下来的。

~~~java
public class NewDemo01 {
    public static void main(String[] args) {
        System.out.print("不传递参数 （fun()）：");
        fun();                                      // 不传递参数
        System.out.print("\n传递1个参数 （fun(1)）：");
        fun(1);                                     // 传递一个参数
        System.out.print("\n传递5个参数 （fun(1, 2, 3, 4, 5)）：");
        fun(1, 2, 3, 4, 5);                         // 传递五个参数
    }
    public static void fun(int...arg){              // 可变参数，可以接收任意多个参数
        for (int i = 0; i<arg.length; i++){
            System.out.print(arg[i] + "、");
        }
    }
}
~~~

程序输出结果为：

~~~
不传递参数 （fun()）：
传递1个参数 （fun(1)）：1、
传递5个参数 （fun(1, 2, 3, 4, 5)）：1、2、3、4、5、
~~~

在使用可变参数的时候，也可以直接向方法中传递一个数组，如下所示：

~~~java
int temp[] = {1, 3, 5};      // 定义数组
fun(temp);                   // 向可变参数中传递数组
~~~

对于以上传递数组的操作，也可以变成以下形式的代码：

~~~java
fun(new int[] {1, 3, 5})
~~~

### Java新特性——foreach输出

数组的输出一般都会使用for循环，但是在JDK 1.5之后为了方便数组的输出，提供了一种foreach语法，此语法的使用格式如下：

~~~java
for(数据类型 变量名称：数组名称){
    ...
}
~~~

例如：

~~~java
public class NewDemo02 {
    public static void main(String[] args) {
        System.out.print("不传递参数 （fun()）：");
        fun();                                 // 不传递参数
        System.out.print("\n传递1个参数 （fun(1)）:");
        fun(1);                                // 传递一个参数
        System.out.print("\n传递5个参数 （fun(1, 2, 3, 4, 5)）：");
        fun(1, 2, 3, 4, 5);                    // 传递五个参数
    }
    public static void fun(int...arg){                // 可变参数，可以接收任意多个参数
        for (int x : arg){                            // 使用foreach输出
            System.out.print(x + "、");
        }
    }
}
~~~

程序运行结果为：

~~~
不传递参数 （fun()）：
传递1个参数 （fun(1)）:1、
传递5个参数 （fun(1, 2, 3, 4, 5)）：1、2、3、4、5、
~~~





