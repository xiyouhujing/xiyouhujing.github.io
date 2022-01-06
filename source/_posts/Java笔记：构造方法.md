---
title: Java笔记：构造方法
date: 2019-05-13 17:36:47
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

**前言**

> 在面向对象程序中，构造方法的主要作用是为类中的属性初始化。在之前的学习过程中可以发现，在程序中只要出现了“()”就表示调用了方法，那么这个方法实际上就是表示要调用构造方法，构造方法可视为一种特殊的方法，它的定义方式与普通方法类似。

<!-- more -->

Java中构造方法的语法结构如下：

~~~
class 类名称{
    访问权限 类名称（类型1 参数1，类型2 参数2，···）{
        程序语句;
        ···     //构造方法没有返回值
    }
}
~~~

在构造方法的声明中，一定要注意一下几点：

1. 构造方法的名称必须与类名称一致。
2. 构造方法的声明处不能有任何返回值类型的声明。
3. 不能在构造方法中使用return返回一个值。

例如，声明一个构造方法：

~~~java
class Person{
    public Person(){         // 声明构造方法
        System.out.println("一个新的Person对象诞生。");
    }
}
public class ConsDemo01 {
    public static void main(String[] args) {
        System.out.println("声明对象：Person per = null;");
        Person per = null;                // 声明对象时不调用构造
        System.out.println("实例化对象：per = new Person();");
        per = new Person();               // 实例化对象时调用构造
    }
}

~~~

程序运行结果：

~~~
声明对象：Person per = null;
实例化对象：per = new Person();
一个新的Person对象诞生。
~~~

需要说明的是，只要是类就必定存在构造方法，在Java中如果一个类中没有明确的声明一个构造方法时，则在编译时会直接生成一个无参数的、什么都不做的构造方法，也就是说，如果以上的Person类中没有明确的声明构造方法，实际上编译之后的类就会为用户自动加上以下形式的构造方法：

~~~java
class Person{
    public Person(){}
}
~~~

下面例子为通过构造方法为类中给属性赋值：

~~~java
class Person02{
    private String name;                           // 声明姓名属性
    private int age;                               // 声明年龄属性
    public Person02(String name, int age){         // 定义构造方法为属性初始化
        this.setName(name);                        // 为name属性赋值
        this.setAge(age);                          // 为age属性赋值
    }
    public void tell(){                            // 取得信息的方法
        System.out.println("姓名：" + getName() + "，年龄：" + getAge());
    }
    public String getName(){                       // 取得姓名
        return name;
    }
    public void setName(String n){                 // 设置姓名
        name = n;
    }
    public int getAge(){                           // 取得年龄
        return age;
    }
    public void setAge(int a){                     // 设置年龄
        if (a >= 0 && a <= 150){
            age = a;
        }
    }
}
public class ConsDemo02 {
    public static void main(String[] args) {
        Person02 per = new Person02("张三", 30);   // 调用构造方法，传递两个参数
        per.tell();
    }
~~~

程序运行结果：

~~~
姓名：张三，年龄：30
~~~

以上就是直接通过构造方法赋值，可以发现，这样赋值比对象实例化之后再单独调用setter方法更方便。需要说明的是，在一个类中如果已经明确地声明了一个构造方法，那么程序在编译时将不会再生成默认的构造方法，即一个类中应保证至少有一个构造方法。

与普通方法一样，构造方法也是可以重载的，只要每个构造方法的参数类型或参数个数不同，即可实现重载。例如：

~~~java
class Person03{
    private String name;                               // 声明姓名属性
    private int age;                                   // 声明年龄属性
    public Person03(){}                                // 定义无参构造
    public Person03(String name){                      // 定义构造，为name属性赋值
        this.setName(name);
    }
    public Person03(String name, int age){             // 定义构造方法为属性初始化
        this.setName(name);                            // 为name属性赋值
        this.setAge(age);                              // 为age属性赋值
    }
    public void tell(){                                // 取得信息的方法
        System.out.println("姓名：" + getName() + "，年龄：" + getAge());
    }
    public String getName(){                           // 取得姓名
        return name;
    }
    public void setName(String n){                     // 设置姓名
        name = n;
    }
    public int getAge(){                               // 取得年龄
        return age;
    }
    public void setAge(int a){                         // 设置年龄
        if (a >= 0 && a <= 150){
            age = a;
        }
    }
}
public class ConsDemo03 {
    public static void main(String[] args) {
        Person03 per = new Person03("张三");     // 调用有一个参数的构造
        per.tell();
    }
}
~~~

程序运行结果：

~~~
姓名：张三，年龄：0
~~~

以上类的构造方法被重载了3次，在主方法中调用的是只有一个参数的构造方法（只设置姓名），因为没有设置年龄，所以年龄默认值为0。