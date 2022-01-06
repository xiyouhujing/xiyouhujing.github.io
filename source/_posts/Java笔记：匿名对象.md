---
title: Java笔记：匿名对象
date: 2019-05-15 15:27:00
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

匿名对象就是没有明确给出名称的对象。一般匿名对象只使用一次，而且匿名对象只在堆内存中开辟空间，而不存在栈内存的引用。

<!-- more -->

~~~java
class Person{
    private String name;                        // 声明姓名属性
    private int age;                            // 声明年龄属性
    public Person(String name, int age){        // 定义构造方法，为属性初始化
        this.setName(name);                     // 为name属性赋值
        this.setAge(age);                       // 为age属性赋值
    }
    public void tell(){
        System.out.println("姓名：" + getName() + "，年龄：" + getAge());
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
        if (a >= 0 && a <= 150){
            age = a;
        }
    }
}
public class NonameDemo01 {
    public static void main(String[] args) {
        new Person("张三", 30).tell();            // 匿名对象
    }
}

~~~

程序运行结果：

~~~
姓名：张三，年龄：30
~~~

在以上程序的主方法中可以发现，直接使用了“new Person("张三", "30")”语句，这实际上就是一个匿名对象，与之前声明的对象不同，此处没有任何栈内存引用它，所以使用一次之后就等待被垃圾收集机制回收。