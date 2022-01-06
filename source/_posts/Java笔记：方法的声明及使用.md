---
title: Java笔记：方法的声明及使用
date: 2019-04-04 10:57:34
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

### 方法的定义

方法就是一段可重复调用的代码，在有些地方也把方法叫做函数。方法的定义在Java中可以使用多种方式，以下格式定义的方法可以直接使用主方法（main()）调用，是因为在方法声明处加上了public static关键字。

<!-- more -->

方法暂时使用如下的语句进行定义：

~~~
public station 返回值类型 方法名称（类型 参数1，类型 参数2，···）{
    程序语句；
    [return 表达式]；
}
~~~

要特别注意的是，如果不需要传递参数到方法中，只要将括号写出，不必填入任何类容。此外，如果方法没有返回值，则在返回类型处要明确写出void，此时，在方法中的return语句可以省略，方法执行完成之后无论是否存在返回值都将返回到方法的调用处并向下继续执行。

例如，定义一个方法，在主方法中调用：

~~~java
public class MethodDemo01 {
    public static void main(String[] args) {
        printInfo();                   // 调用printInfo方法
        printInfo();                   // 调用printInfo方法
        printInfo();                   // 调用printInfo方法
        System.out.println("Hello World!");
    }
    // 此处由于此方法是由main()方法直接调用的，所以一定要加上public static
    public static void printInfo(){     // 此处方法没有返回值
        char c[] = {'H', 'e', 'l', 'l', 'o', ',', 'L', 'X', 'H'};
        for (int i =0; i < c.length; i++){
            System.out.print(c[i]);     // 循环输出
        }
        System.out.println("");         // 换行
    }
}
~~~

程序运行结果：

~~~
Hello,LXH
Hello,LXH
Hello,LXH
Hello World!
~~~

从程序中可以发现，因为printInfo()方法本身不需要任何的返回值声明，所以使用了void关键字进行了声明，表示此方法不需要任何的返回值，所以不需要编写return语句。

> **方法命名规范要求**
>
> 在定义类时，全部单词的首字母必须大写，那么在定义方法时也有命名规范要求，即第一个单词的首字母小写，之后每一个单词的首字母大写，如printInfo()方法。

前面介绍了没有返回值的方法，下面是有返回值的方法例子：

~~~java
public class MethodDemo02 {
    public static void main(String[] args) {
        int one = addOne(10, 20);            // 调用整数的加法操作
        float two = addTwo(10.3f, 13.3f);          // 调用浮点数的加法操作
        System.out.println("addOne的计算结果：" + one);
        System.out.println("addTwo的计算结果：" + two);
    }
    // 定义方法，完成两个整数的加法操作，方法返回一个int型数据
    public static int addOne(int x, int y){
        int temp = 0;                             // temp为局部变量，只在此方法中有效
        temp = x + y;                             // 执行加法计算
        return temp;                              // 返回计算结果
    }
    // 定义方法，完成两个浮点数的加法操作，方法返回一个float型数据
    public static float addTwo(float x, float y){
        float temp = 0;                           // temp为局部变量，只在此方法中有效
        temp = x + y;                             // 执行加法计算
        return temp;                              // 返回计算结果
    }
}
~~~

程序运行结果：

~~~
addOne的计算结果：30
addTwo的计算结果：23.6
~~~

另外，在方法中可以定义多个变量，这些变量只在方法的内部起作用，所以也可以把这些变量称为**局部变量**。

### 方法的重载

在面的addOne()和addTwo()两种方法的演示中，我们可以发现，两种方法都是做加法运算，其本质是相同的，应该统一为add()方法才对，为了解决这个问题，Java中引入了**方法重载**的概念。所谓的方法重载就是方法名称相同，但是参数的类型和参数的个数不同。通过传递参数的个数及类型的不同可以完成不同功能方法的调用。

验证方法的重载：

~~~java
public class MethodDemo03 {
    public static void main(String[] args) {
        int one = add(10, 20);              // 调用有两个参数的整型加法
        int two = add(10, 20, 30);          // 调用有三个参数的整型加法
        float three = add(10.3f, 13.3f);    // 调用有两个参数的浮点型加法
        System.out.println("add(int x, int y)的计算结果：" + one);
        System.out.println("add(int x, int y, int z)的计算结果：" + two);
        System.out.println("add(float x, float y)的计算结果：" + three);
    }
    public static int add(int x, int y){
        int temp = 0;
        temp = x + y;
        return temp;
    }
    public static int add(int x, int y, int z){
        int temp = 0;
        temp = x + y + z;
        return temp;
    }
    public static float add(float x, float y){
        float temp = 0;
        temp = x + y;
        return temp;
    }
}

~~~

程序运行结果：

~~~
add(int x, int y)的计算结果：30
add(int x, int y, int z)的计算结果：60
add(float x, float y)的计算结果：23.6
~~~

从程序中可以发现，add()方法被重载了3次，而且每次重载时的参数类型或个数都有不同，所以在调用时，会根据参数的类型和个数自动进行区分。

另外，需要注意的是，**方法的重载一定只是在参数上的类型或个数有所不同**，下面的代码不是方法重载的运用：

~~~java
public static float add(int x, int y){      // 返回floa型，但参数类型及个数一致
    float temp = 0;
    temp = x + y;
    return temp;
}
public static int add(int x, int y){       // 返回int型，但参数类型及个数一致
    int temp = 0;
    temp = x + y;
    return temp;
}
~~~

上面的两个方法的接收参数类型和个数完全一样，但只是方法的返回值类型不同，上面的代码程序也是不可能通过编译通过的，所以不是方法重载。

### 使用return结束一个方法

在Java的方法定义中，可以使用return语句直接结束一个方法的执行，如下所示：

~~~java
public class MethodDemo04 {
    public static void main(String[] args) {
        System.out.println("1、调用fun()方法之前。");
        fun(10);
        System.out.println("2、调用fun()方法之后。");
    }
    public static void fun(int x){
        System.out.println("3、进入fun()方法。");
        if (x==10){
            return;            // 结束方法，返回被调用处
        }
        System.out.println("4、正常执行完fun()方法。");
    }
}
~~~

程序运行结果：

~~~
1、调用fun()方法之前。
3、进入fun()方法。
2、调用fun()方法之后。
~~~

从结果可以看出，虽然return中没有返回任何内容，但是一旦执行到了return语句之后，方法将不再执行，而返回到被调用处继续向下执行。

### 方法的递归调用

递归调用是一种特殊的调用形式，属于方法自身调用，如下图：

![方法的递归调用](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E6%96%B9%E6%B3%95%E7%9A%84%E5%A3%B0%E6%98%8E%E5%8F%8A%E4%BD%BF%E7%94%A8%EF%BC%89/%E6%96%B9%E6%B3%95%E7%9A%84%E9%80%92%E5%BD%92%E8%B0%83%E7%94%A8.png)

例如，要完成一个数字的累加操作，除了可以使用循环方式外，还可以使用递归调用：

~~~java
public class MethodDemo05 {
    public static void main(String[] args) {
        System.out.println("计算结果：" + sum(100));   // 调用操作
    }
    public static int sum(int num){
        if (num == 1){
            return 1;
        }
        else {
            return num + sum(num - 1);     // 递归调用
        }
    }
}
~~~

程序运行结果为：`计算结果：5050`

值得注意的是，递归调用时必须有一个明确的结束条件，然后不断改变传入的数据，才能实现递归调用。

>递归调用在操作时如果处理不好，则有可能出现内存的溢出，所以对于这种方法调用形式使用时要谨慎。