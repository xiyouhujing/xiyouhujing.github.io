---
title: Java笔记：封装性
date: 2019-04-18 16:49:12
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

**前言**

> 封装是指隐藏对象的属性和实现细节，仅对外提供公共访问方式。封装可以被认为是一个保护屏障，防止该类的代码和数据被外部类定义的代码随机访问。要访问该类的代码和数据，必须通过严格的接口控制。

<!-- more -->

封装性是面向对象的第一大特性，所谓的封装性就是指对外部不可见，那么为什么要有封装性呢，首先观察以下程序：

~~~java
class Person06{
    String name;
    int age;
    public void tell(){
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
}
public class EncDemo01 {
    public static void main(String[] args) {
        Person06 per = new Person06();        // 声明并实例化对象
        per.name = "张三";                    // 为name属性赋值
        per.age = -30;                        // 为age属性赋值
        per.tell();                           // 调用方法
    }
}
~~~

程序运行结果：

~~~
姓名：张三，年龄：-30
~~~

年龄赋值为-30在程序中是正确的，因为int可以取负值，但是在实际中没有人的年龄是负的。之前所列举的程序都是用对象直接访问类中的属性，这在面向对象法则中是不允许的，所以为了避免程序中这种错误的发生，在一般的开发中往往要将类中的属性封装，封装的格式如下：

~~~
属性封装： private 属性类型 属性名称；
方法封装： private 方法返回值 方法名称（参数列表）{}
~~~

例如，为程序加上封装属性：

~~~java
class Person07{
    private String name;             // 声明姓名属性
    private int age;                 // 声明年龄属性
    public void tell(){
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
}
public class EncDemo02 {
    public static void main(String[] args) {
        Person07 per = new Person07();
        per.name = "张三";
        per.age = -30;
        per.tell();
    }
}
~~~

程序会编译出错，本程序与上面的程序除了在声明属性上有些区别外，并没有其他的区别，而就是一个小小的关键字private，使程序连编译都无法通过，而所提示的错误为“属性（name、age）为私有的”，所以不能由对象直接进行访问，这样就可以保证对象无法直接去访问类中是属性，从而保证堆入口处有所限制，可是这样以来又该如何访问此属性呢？为了解决属性必须封装且必须访问的矛盾，在Java开发中对于私有属性的访问有了以下的明确定义：“只要是被封装的属性，则必须通过setter和getter方法设置和取得”。

为前面类中的私有属性加上setter和getter方法：

~~~java
class Person08{
    private String name;
    private int age;
    public void tell(){
        System.out.println("姓名：" + getName() + "，年龄：" + getAge());
    }
    public String getName(){
        return name;                  // 取得姓名
    }
    public void setName(String n){    // 设置姓名
        name = n;
    }
    public int getAge(){              // 取得年龄
        return age;
    }
    public void setAge(int a){        // 设置年龄
        age = a;
    }
}
public class EncDemo03 {
    public static void main(String[] args) {
        Person08 person = new Person08();      // 声明并实例化对象
        person.setName("张三");                // 调用setter设置姓名
        person.setAge(-30);                    // 调用setter设置年龄
        person.tell();                         // 输出信息
    }
}

~~~

程序运行结果：

~~~
姓名：张三，年龄：-30
~~~

观察程序的结构，可以发现通过setter和getter方法可以设置和取得属性，而在主方法调用时，也是调用了setter()方法进行内容的赋值，也就是说如果想要堆设置进去的值进行检查，则只需要在setter()方法中加入检查代码即可。

~~~java
class Person09{
    private String name;
    private int age;
    public void tell(){
        System.out.println("姓名：" + name + "，年龄：" + age);
    }
    public String getName(){
        return name;
    }
    public void setName(String n){
        name = n;
    }
    public int getAge(){
        return age;
    }
    public void setAge(int a){
        if (a>=0 && a<150){             // 在此处加上验证代码
            age = a;
        }
    }
}
public class EncDemo04 {
    public static void main(String[] args) {
        Person09 per = new Person09();
        per.setName("张三");
        per.setAge(-30);
        per.tell();
    }
}

~~~

程序运行结果：

~~~
姓名：张三，年龄：0
~~~

因为程序中的setter方法处加入了验证代码，所以如果年龄数值不正确，则不会把值赋给age属性，所以程序的运行结果为0。

> **关于private的补充说明**
>
> （1）类中的属性都必须封装，封装之后的属性必须通过setter和getter进行访问。
>
> （2）面向对象的封装性本身并不是单单指private关键字，用private声明的属性或方法只能在其类的内部被调用，而不能在类的外部被调用。
>
> （3）正常情况下，类中的方法直接写上方法名称就可以完成本类中的方法调用，如果在此时非要枪带哦时本类中的方法，也可以在调用时按“this.方法名称()”的形式编写。

程序中的属性进行封装后，在使用类图表示封装属性时就必须按照如下的风格：

~~~
-属性名称：数据类型
~~~

其中“-”表示private。