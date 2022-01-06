---
title: Java笔记：引用传递及基本应用
date: 2019-05-24 17:19:08
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

**前言**

> 值传递：是指在调用函数时将实际参数复制一份传递到函数中，这样在函数中如果对参数进行修改，将不会影响到实际参数。引用传递：是指在调用函数时将实际参数的地址直接传递到函数中，那么在函数中对参数进行修改，将会影响到实际参数。

<!-- more -->

### 引用传递

所谓引用传递就是指将堆内存空间的使用权交给多个栈内存空间。

#### 引用传递范例一

对象引用传递：

~~~java
class Demo{
    int temp = 30;                    // 此处为了访问方便，属性暂时不封装
}
public class RefDemo01 {
    public static void main(String[] args) {
        Demo d1 = new Demo();
        d1.temp = 50;
        System.out.println("fun()方法调用之前：" + d1.temp);
        fun(d1);
        System.out.println("fun()方法调用之后：" + d1.temp);
    }
    public static  void fun(Demo d2){     // 此处的方法由主方法直接调用
        d2.temp = 1000;
    }
}
~~~

程序运行结果：

~~~
fun()方法调用之前：50
fun()方法调用之后：1000
~~~

从结果中可以发现，在fun()方法中接收了Demo类对象d1，并将temp属性的内容进行了修改，因为是引用传递，所以最终temp的值是1000，此程序可以通过下图进行理解：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E5%BC%95%E7%94%A8%E4%BC%A0%E9%80%92%E5%8F%8A%E5%9F%BA%E6%9C%AC%E5%BA%94%E7%94%A8%EF%BC%89/%E5%BC%95%E7%94%A8%E4%BC%A0%E9%80%92%E8%8C%83%E4%BE%8B%E7%9A%84%E5%86%85%E5%AD%98%E5%88%86%E6%9E%90%E5%9B%BE.png)

#### 引用传递范例二

引用传递：

~~~java
public class RefDemo02 {
    public static void main(String[] args) {
        String str1 = "hello";                 // 实例化字符串对象
        System.out.println("fun()方法调用之前：" + str1);
        fun(str1);                             // 调用fun()方法
        System.out.println("fun()方法调用之后：" + str1);
    }
    public static  void fun(String str2){      // 此处的方法由主方法直接调用
        str2 = "MLDN";                         // 修改字符串内容
    }
}
~~~

程序运行结果：

~~~
fun()方法调用之前：hello
fun()方法调用之后：hello
~~~

从运行结果可以发现，虽然此时传递的是一个String类型的对象，但是结果并没有像之前一样发生给吧，因为字符串的内容一旦声明就是不可改变的，改变的只是其内存地址的指向，如下图所示：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E5%BC%95%E7%94%A8%E4%BC%A0%E9%80%92%E5%8F%8A%E5%9F%BA%E6%9C%AC%E5%BA%94%E7%94%A8%EF%BC%89/%E5%BC%95%E7%94%A8%E4%BC%A0%E9%80%92%E8%8C%83%E4%BE%8B%E7%9A%84%E5%86%85%E5%AD%98%E5%88%86%E6%9E%90%E5%9B%BE2.png)

以上操作并不难理解，因为每个字符串对象都表示一个匿名对象，这样在fun()方法操作中，如果为str2重新设置内容，就相当于改变了str2的引用，而str1本身的内容并不会受到任何影响。

#### 引用传递范例三

~~~java
class Demo2{
    String temp = "hello";              // 此处为了访问方便，属性暂不封装
}
public class RefDemo03 {
    public static void main(String[] args) {
        Demo2 d1 = new Demo2();
        d1.temp = "word";               // 修改对象中的temp属性
        System.out.println("fun()方法调用之前：" + d1.temp);
        fun(d1);
        System.out.println("fun()方法调用之后：" + d1.temp);
    }
    public static void fun(Demo2 d2){
        d2.temp = "MLDN";
    }
}
~~~

程序运行结果：

~~~
fun()方法调用之前：word
fun()方法调用之后：MLDN
~~~

从结果可以看出，fun()方法中将属性的内容修改了，内存操作如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E5%BC%95%E7%94%A8%E4%BC%A0%E9%80%92%E5%8F%8A%E5%9F%BA%E6%9C%AC%E5%BA%94%E7%94%A8%EF%BC%89/%E5%BC%95%E7%94%A8%E4%BC%A0%E9%80%92%E8%8C%83%E4%BE%8B%E7%9A%84%E5%86%85%E5%AD%98%E5%88%86%E6%9E%90%E5%9B%BE3.png)

本程序的分析方法与第一个范例完全一样，因为String是作为一个Demo2类的属性存在的，而在操作时更改的只是Demo2类中属性的内容。

### 接收本类的引用

以上为引用传递的基本形式，实际上，在对象引用传递上也可以在一个类中接收自己本类对象的实例，而且接受完之后，可以方便地通过此对象直接进行本类中封装属性的访问，如下：

~~~java
class Demo3{
    private int temp = 30;                     // 声明temp属性并封装
    public void fun(Demo3 d2){                 // 接收本类的引用
        d2.temp = 50;                          // 直接通过对象调用本类的私有属性
    }
    public int getTemp(){                      // getter方法
        return temp;
    }
    public void setTemp(int t){                // setter方法
        temp = t;
    }
}
public class RefDemo04 {
    public static void main(String[] args) {
        Demo3 d1 = new Demo3();               // 实例化Demo对象
        d1.setTemp(50);                       // 修改temp内容
        d1.fun(d1);                           // 此处把Demo对象传回到自己的类中
        System.out.println("temp = " + d1.getTemp());
    }
}
~~~

程序运行结果为：`temp = 50`

此种引用方式的传递在关于对象比较操作时才会经常使用，其他时候基本上都很少使用。

### 范例——一对一关系

使用引用传递还可以表示出生活中的以下一种场景：一个人有一本书，一本书属于一个人。因而可以得出这样的结论：人应该是一个具体的类，书也应该是一个具体的类，在人的类中应该存在一个属性表示书，在书的类中也应该存在一个属性表示人。

~~~java
class Person{
    private String name;                            // 姓名
    private int age;                                // 年龄
    private Book book;                              // 一个人有一本书
    public Person(String name, int age){            // 通过构造方法设置内容
        this.setName(name);
        this.setAge(age);
    }
    public void setName(String n){                  // 设置姓名
        name = n;
    }
    public String getName(){                        // 返回姓名
        return name;
    }
    public void setAge(int a){                      // 设置年龄
        age = a;
    }
    public int getAge(){                            // 返回年龄
        return age;
    }
    public void setBook(Book b){                    // 设置本人的书
        book = b;
    }
    public Book getBook(){                          // 得到本人的书
        return book;
    }
}
class Book{
    private String title;                          // 标题
    private float price;                           // 价格
    private Person person;                         // 一本书属于一个人
    public Book(String title, float price){        // 通过构造方法设置属性内容
        this.setTitle(title);
        this.setPrice(price);
    }
    public void setTitle(String t){
        title = t;
    }
    public String getTitle(){
        return title;
    }
    public void setPrice(float p){
        price = p;
    }
    public float getPrice(){
        return price;
    }
    public void setPerson(Person person){
        this.person = person;
    }
    public Person getPerson(){
        return person;
    }
}
public class RefDemo05 {
    public static void main(String[] args) {
        Person per = new Person("张三", 30);                  // 实例化Person对象
        Book bk = new Book("JAVA SE 核心开发", 90.0f);        // 实例化Book对象
        per.setBook(bk);                                     // 设置两个对象间的关系，一个人有一本书
        bk.setPerson(per);                                  // 设置两个对象间的关系，一本书属于一个人
        System.out.println("从人找到书 --> 姓名：" + per.getName() + "；年龄："
        + per.getAge() + "；书名：" + per.getBook().getTitle() + "；价格："
        + per.getBook().getPrice());
        System.out.println("从书找到人 --> 书名：" + bk.getTitle() + "；价格："
        + bk.getPrice() + "；姓名：" + bk.getPerson().getName() + "；年龄："
        + bk.getPerson().getAge());
    }
}
~~~

程序运行结果：

~~~
从人找到书 --> 姓名：张三；年龄：30；书名：JAVA SE 核心开发；价格：90.0
从书找到人 --> 书名：JAVA SE 核心开发；价格：90.0；姓名：张三；年龄：30
~~~

### 范例——进一步深入一对一关系

现在有一个新的要求，一个人有一个孩子，每个孩子还会有一本书。因为一个孩子也是一个人，所以并不需要单独建立一个孩子类，只需要简单的修改Person类，在类中增加一个自己的引用即可。

~~~java
class Person1{
    private String name;                            // 姓名
    private int age;                                // 年龄
    private Book1 book;                             // 一个人有一本书
    private Person1 child;                           // 一个人有一个孩子
    public Person1(String name, int age){            // 通过构造方法设置内容
        this.setName(name);
        this.setAge(age);
    }
    public void setName(String n){                  // 设置姓名
        name = n;
    }
    public String getName(){                        // 返回姓名
        return name;
    }
    public void setAge(int a){                      // 设置年龄
        age = a;
    }
    public int getAge(){                            // 返回年龄
        return age;
    }
    public void setBook(Book1 b){                    // 设置本人的书
        book = b;
    }
    public Book1 getBook(){                          // 得到本人的书
        return book;
    }
    public void setChild(Person1 child){             // 设置孩子
        this.child = child;
    }
    public Person1 getChild(){                       // 得到孩子
        return child;
    }
}
class Book1{
    private String title;                          // 标题
    private float price;                           // 价格
    private Person1 person;                         // 一本书属于一个人
    public Book1(String title, float price){        // 通过构造方法设置属性内容
        this.setTitle(title);
        this.setPrice(price);
    }
    public void setTitle(String t){
        title = t;
    }
    public String getTitle(){
        return title;
    }
    public void setPrice(float p){
        price = p;
    }
    public float getPrice(){
        return price;
    }
    public void setPerson(Person1 person){
        this.person = person;
    }
    public Person1 getPerson(){
        return person;
    }
}
public class RefDemo06 {
    public static void main(String[] args) {
        Person1 per = new Person1("张三", 30);            // 实例化Person对象
        Person1 cld = new Person1("张草", 10);            // 定义一个孩子
        Book1 bk = new Book1("JAVA SE 核心开发", 90.0f);        // 实例化Book对象
        Book1 b = new Book1("一千零一夜", 30.3f);               // 定义孩子的书
        per.setBook(bk);                                    // 设置对象间的关系，一个人有一本书
        bk.setPerson(per);                                  // 设置对象间的关系，一本书属于一个人
        cld.setBook(b);                                     // 设置对象间的关系，一个孩子有一本书
        b.setPerson(cld);                                   // 设置对象间的关系，一本书属于一个孩子
        per.setChild(cld);                                  // 设置对象间的关系，一个人有一个孩子
        System.out.println("从人找到书 --> 姓名：" + per.getName() + "；年龄："
                + per.getAge() + "；书名：" + per.getBook().getTitle() + "；价格："
                + per.getBook().getPrice());
        System.out.println("从书找到人 --> 书名：" + bk.getTitle() + "；价格："
                + bk.getPrice() + "；姓名：" + bk.getPerson().getName() + "；年龄："
                + bk.getPerson().getAge());
        System.out.println(per.getName() + "的孩子 --> 姓名：" + per.getChild().getName()
        + "；年龄：" + per.getChild().getAge() + "；书名：" + per.getChild().getBook().getTitle()
        + "；价格：" + per.getChild().getBook().getPrice());
    }
}
~~~

程序运行结果：

~~~
从人找到书 --> 姓名：张三；年龄：30；书名：JAVA SE 核心开发；价格：90.0
从书找到人 --> 书名：JAVA SE 核心开发；价格：90.0；姓名：张三；年龄：30
张三的孩子 --> 姓名：张草；年龄：10；书名：一千零一夜；价格：30.3
~~~

