---
title: Java开发实战经典习题3.7
date: 2019-03-21 14:59:47
tags:
- Java练习
copyright: true
categories: Java
mathjax: true
---

**前言**

> Java开发实战经典第三章习题：java基础程序设计。掌握java中数据类型的划分方法、掌握八种基本数据类型的使用方法、掌握数据类型的转换方式、掌握java中的运算位、掌握各个运算符和表达式的运用、掌握判断和循环语句的使用方法、掌握break及continue关键字的作用。
>

<!-- more -->

#### 打印出1\~10000范围中所有的“水仙花数”，所谓“水仙花数”是指一个3位数，其各位数字立方和等于该数本身。例如，153就是一个“水仙花数”，因为153=（1的三次方+5的三次方+3的三次方）。

~~~java
/**
首先“水仙花数”是一个三位数，所以题目给的1~10000的范围是比较大的，可以缩小为100~999，另外需要明白这题需要用到循环结构，一次验证范围内的3位数是为“水仙花数”，我们可以采用while、do···while以及for循环中的任意一种，这里采用的是for循环。本题 一个难点是如何提取个十百位的数，我们可以采用取余算法（%）。然后用if语句判断该数是否为“水仙化数”，是就打印，不是就再执行for循环验证下一个数。
*/
public class test3_1 {
    public static void main(String[] args) {
        for (int i = 100; i < 1000; i++){
            int m = i % 10;            // 取个位数
            int n = (i / 10) % 10;     // 取十位数
            int h = i / 100;           // 取百位数
            if (i == m * m * m + n * n * n + h * h * h){    // 验证是否为水仙花数
                System.out.println(i + "是水仙花数");
            }
        }
    }
}

~~~

程序运行结果为：

~~~
153是水仙花数
370是水仙花数
371是水仙花数
407是水仙花数
~~~

#### 通过代码完成两个整数内容的交换

~~~java
public class test3_2 {
    public static void main(String[] args) {
        int a = 10, b = 5;
        System.out.println("交换之前的内容：" + "a = " + a + "，b = " + b);
        a = a + b;
        b = a - b;
        a = a - b;
        System.out.println("交换之后的内容：" + "a = " + a + "，b = " + b);
    }
}
~~~

程序运行结果为：

~~~
交换之前的内容：a = 10，b = 5
交换之后的内容：a = 5，b = 10
~~~

#### 给定3个数字，求出这3个数字中的最大值，并将最大值输出

~~~java
public class test3_3 {
    public static void main(String[] args) {
        int a = 3, b = 5, c = 4;
        int max = 0;
        max = a > b ? (a > c ? a : c) : (b > c ? b : c);
        System.out.println("最大值为：" + max);
    }
}
~~~

程序运行结果为：

~~~
最大值为：5
~~~

#### 判断某数能否被3、5、7同时整除

~~~java
public class test3_4 {
    public static void main(String[] args) {
        int num = 105;
        if (num%3==0 && num%5==0 && num%7==0) {
            System.out.println(num + "能被3、5、7同时整除");
        }else {
            System.out.println(num + "不能被3、5、7同时整除");
        }
    }
}
~~~

程序运行结果为：

~~~
105能被3、5、7同时整除
~~~

#### 编写程序，分别利用while循环、do···while循环和for循环求出100~200的累加和。

~~~java
/**
while循环求100~200的累加和
*/
public class test3_5_1 {
    public static void main(String[] args) {
        int i = 100;
        int sum = 0;
        while (i <= 200){
            sum += i;
            i++;
        }
        System.out.println("100~200的累加和为：" + sum);
    }
}

/**
do···while循环求100~200的累加和。
*/
public class test3_5_2 {
    public static void main(String[] args) {
        int i = 100;
        int sum = 0;
        do {
            sum += i;
            i++;
        }while (i <= 200);
        System.out.println("100~200的累加和为：" + sum);
    }
}

/**
for循环求100~200的累加和。
*/
public class test3_5_3 {
    public static void main(String[] args) {
        int sum = 0;
        for (int i = 100; i <= 200; i++){
            sum += i;
        }
        System.out.println("100~200的累加和为：" + sum);
    }
}
~~~

#### 编写程序Java程序，求13-23+33-43+···+973-983+993-1003的值

~~~java
public class test3_6 {
    public static void main(String[] args) {
        int count = 1;
        int sum = 0;
        int x = 13;
        while (x <= 1003){
            if (count % 2 == 1){
                sum += x;
            }else {
                sum -= x;
            }
            x += 10;
            count++;
        }
        System.out.println("3-23+33-43+···+973-983+993-1003 = " + sum);

    }
}
~~~

程序运行结果为：

~~~
3-23+33-43+···+973-983+993-1003 = -500
~~~

#### 编写一个程序，实现两个数字的交换。

~~~java
/**
这一题我理解为交换两位数的个位和十位。
*/
public class Test3_7 {
    public static void main(String[] args) {
        int a = 35;
        int n = a % 10;
        int m = a / 10;
        System.out.println("交换后的数字为：" + (n*10+m));
    }
}
~~~

#### 编写一个程序求3个数中的最大值

~~~
参考第三题
~~~

#### 编写一个程序，实现1~100的累加

~~~java
public class Test3_9 {
    public static void main(String[] args) {
        int sum = 0;
        for (int i = 1; i <= 100; i++){
            sum += i;
        }
        System.out.println("1~100的累加和为：" + sum);
    }
}
~~~

#### 求1~1000之间可以同时被3、5、7整除的数字。

~~~java
public class Test3_10 {
    public static void main(String[] args) {
        for (int i = 1; i <= 1000; i++){
            if (i%3==0 && i%5==0 && i%7==0){
                System.out.println(i);
            }
        }
    }
}
~~~

#### 编程求1!+2!+3!+···+20!的值。

~~~java
/**
此处需要注意，阶乘是很大的数，所以不能按常规设定阶乘pro和阶乘累加和sum为int型，范围可能不够大，所以设为long型数据。
*/
public class Test3_11 {
    public static void main(String[] args) {
        long sum = 0;
        long pro = 1;
        for (int i = 1; i <= 20; i++){
            pro *= i;     // 计算每项的阶乘
            sum += pro;   // 计算每项阶乘的累加和
        }
        System.out.println("1!+2!+3!+...+20! = " + sum);
    }
}
~~~

程序运行结果为：

~~~
1!+2!+3!+...+20! = 2561327494111820313
~~~

#### 使用for循环打印由*组成的三角形，三角形每行的星数和行数相等

~~~java
public class Test3_12 {
    public static void main(String[] args) {
        for (int i = 0; i < 5; i++) {
            for (int j = 0; j <= 4-i; j++) {
                System.out.print(" ");      // 注意print为不换行输出
            }
            for (int k = 0; k <= i; k++) {
                System.out.print("* ");     // print不换行输出，注意星号后面还需要打印一个空格，不然三角形不对称
            }
            System.out.println("  ");       // println换行输出
        }
    }
}
~~~

程序运行的结果如图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E5%BC%80%E5%8F%91%E5%AE%9E%E6%88%98%E7%BB%8F%E5%85%B8%E4%B9%A0%E9%A2%983-7/%E4%B8%89%E8%A7%92%E5%BD%A2.png)

