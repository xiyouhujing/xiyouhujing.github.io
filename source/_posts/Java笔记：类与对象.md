---
title: Java笔记：类与对象
date: 2019-04-15 19:39:10
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

**前言**

> 在面向对象中，类和对象是最基本、最重要的组成单元。类实际上是表示一个客观世界某类群体的一些基本特征抽象。对象就是表示一个个具体的东西。例如，现实生活中，人可以称为一个类，因为人是一种广义的概念，并不是具体的。而某一个人就可以称为一个对象，某个人可以通过他的各种特征来描述，例如姓名、性别、年龄等。这些信息在面向对象的概念中就称为属性；当然人是可以吃饭、睡觉的，这些人的行为在类中就称为方法。

<!-- more -->

如果要使用一个类，就一定要产生一个对象，每个对象之间是靠属性的不同来进行区分的，而每个对象所具备的操作就是类中规定好的方法。

### 类的定义

类是由属性和方法组成的，属性中定义的是类需要的一个个具体信息，实际上一个属性就是一个变量，而方法是一些操作行为，但是在程序设计中，定义类也是要按照具体的语法要求完成的，类的定义语法如下：

~~~
class 类名称{
    数据类型 属性；
    ···
    public 返回值的数据类型 方法名称（参数1，参数2...）{
        程序语句；
        [return 表达式；]
    }
}
~~~

> **类中定义方法的补充说明**
>
> 可以发现，此处的方法与之前的方法定义有区别，并没有加上static关键字，这是因为此时定义的方法将有对象调用，而不像之前那样与主方法定义在一个类中并且由主方法之间调用。

例如我们定义一个Person类：

~~~java
class Person{
    String name;             // 声明姓名属性
    int age;                 // 声明年龄属性
    public void tell(){      // 取得信息的方法
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
}
~~~

类定义完成后，我们可以通过下图所示的图形样式来表示出类的定义：

|     Person      |
| :-------------: |
|  name : String <br> age : int  |
| + tell() : void |

1. 第一层表示类的名称，类的名称要求开头首字母大写。
2. 第二层表示属性的定义，按照“访问权限 属性名称：属性类型”的格式定义，在本类中因为声明属性处没有写任何的访问权限，所以前面暂时不加任何的符号。
3. 第三层表示类中方法的定义，按照“访问权限 方法名称():方法返回值”的格式定义，在本类中，方法的声明处加上了public（此为访问权限，表示任何地方都可以访问），所以使用“+”表示，另外，如果方法中由传递的参数，则此方法定义格式为“访问权限 方法名称(参数名称: 参数类型, 参数名称: 参数类型, ...): 方法返回值”

### 对象的创建及使用

要想使用一个类则必须由对象，下面给出了对象的创建格式：

~~~
类名 对象名称 = null;                 // 声明对象
对象名称 = new 类名();                // 实例化对象
~~~

以上格式产生对象分为声明对象和实例化对象两步。

当然也可以直接通过以下方式一步完成：

~~~
类名 对象名称 = new 类名();
~~~

> 以上格式与之前数组定义的格式相似，因为类和数组都属于引用数据类型，只要引用数据类型的使用格式都可以使用如上的定义样式。

创建对象的具体范例：

~~~java
class Person{
    String name;                    // 声明姓名属性
    int age;                        // 声明年龄属性
    public void tell(){             // 取得信息的方法
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
}
public class ClassDemo02{
    public static void main(String args[]){
        Person per = new Person();   // 创建并实例化对象
    }
}
~~~

如果要使用对象访问类中的某个属性或方法可以使用如下的语法实现：

~~~
访问属性：对象名称.属性名
访问方法：对象名称.方法名()
~~~

例如：

~~~java
class Person2{
    String name;                // 声明姓名属性
    int age;                    // 声明年龄属性
    public void tell(){
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
}

public class ClassDemo03 {
    public static void main(String[] args) {
        Person2 per = null;            // 声明对象
        per = new Person2();           // 实例化对象
        per.name = "张三";            // 为name属性赋值
        per.age = 30;                 // 为age属性赋值
        per.tell();                   // 调用类中的方法
    }
}

~~~

程序运行结果：

~~~
姓名：张三，年龄：30
~~~

### 创建多个对象

前面介绍过创建一个对象的方法，可以按照同样的格式同时创建多个对象，每个对象会分别占据自己的堆、栈空间。

创建两个对象：

~~~java
class Person3{
    String name;          // 声明姓名属性
    int age;              // 声明年龄属性
    public void tell(){
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
}
public class ClassDemo04 {
    public static void main(String[] args) {
        Person3 per1 = null;              // 声明per1对象
        Person3 per2 = null;              // 声明per2对象
        per1 = new Person3();             // 实例化per1对象
        per2 = new Person3();             // 实例化per2对象
        per1.name = "张三";               // 设置per1对象的name属性内容
        per1.age = 30;                    // 设置per1对象的age属性内容
        per2.name = "李四";               // 设置per2对象的name属性内容
        per2.age = 33;                    // 设置per2对象的age属性内容
        System.out.print("per1对象中的内容 -->");
        per1.tell();                      // per1调用方法
        System.out.print("per2对象中的内容 -->");
        per2.tell();                      // per2调用方法
    }
}
~~~

程序运行结果：

~~~
per1对象中的内容 -->姓名：张三，年龄：30
per2对象中的内容 -->姓名：李四，年龄：33
~~~

类属于引用数据类型，而且从数组的使用上也可以发现，引用数据类型就是指一段堆内存空间可以同时被多个栈内存指向。下面来看一个引用传递的例子：

~~~java
class Person4{
    String name;
    int age;
    public void tell(){
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
}
public class ClassDemo05 {
    public static void main(String[] args) {
        Person4 per1 = null;
        Person4 per2 = null;
        per1 = new Person4();
        per2 = per1;                 // 把per1的堆内存空间使用权给per2
        per1.name = "张三";
        per1.age = 30;
        // 设置per2对象的内容，实际上就是设置per1对象的内容
        per2.age = 33;
        System.out.print("per1对象中的内容 -->");
        per1.tell();
        System.out.print("per2对象中的内容 -->");
        per2.tell();
    }
}
~~~

程序运行结果：

~~~
per1对象中的内容 -->姓名：张三，年龄：33
per2对象中的内容 -->姓名：张三，年龄：33
~~~

从程序运行结果可以发现，两个对象的输出内容是一样的，实际上所谓的引用传递就是将一个堆内存空间的使用权给多个栈内存空间，每个栈内存空间都可以修改堆内存的内容。

~~~java
class Person5{
    String name;
    int age;
    public void tell(){
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
}
public class ClassDemo06 {
    public static void main(String[] args) {
        Person5 per1 = null;
        Person5 per2 = null;
        per1 = new Person5();
        per2 = new Person5();
        per1.name = "张三";
        per1.age = 30;
        per2.name = "李四";
        per2.age = 33;
        per2 = per1;
        System.out.print("per1对象中的内容 -->");
        per1.tell();
        System.out.print("per2对象中的内容 -->");
        per2.tell();
    }
}
~~~

程序运行结果为：

~~~
per1对象中的内容 -->姓名：张三，年龄：30
per2对象中的内容 -->姓名：张三，年龄：30
~~~

因为per2本身有堆内存空间，所以如果要想再指向per1对应的空间，则必须先断开已有的连接。而per2原来的空间没有任何的栈内存空间所引用，就形成了垃圾空间，等待垃圾收集机制进行回收。

> **关于垃圾空间的释放**
>
> Java本身提供垃圾收集机制（Garbage Collection, GC），会不定期地释放不用的内存空间，只要对象不使用了，就会等待GC释放空间。

从上面的程序中明确的一点，即一个栈内存空间只能指向一个堆内存空间，如果要想再指向其他的堆内存空间，则必须先断开已有的指向才能分配新的指向。