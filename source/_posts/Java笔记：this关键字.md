---
title: Java笔记：this关键字
date: 2019-06-05 15:43:55
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---
**前言**

> this是Java中的关键字，除了可以用来强调调用的是本类中的方法，this还有以下作用：
> 1. 表示类中的属性
> 2. 可以使用this调用本类的构造方法
> 3. this表示当前对象

<!-- more -->

### 使用this调用本类中的属性

在程序中可以使用this调用本类属性，例如：

~~~java
class Person{
    private String name;
    private int age;
    public Person(String n, int a){
        name = n;
        age = a;
    }
    public String getInfo(){
        return "姓名：" + name + "，年龄：" + age;
    }
}
~~~

该类中的构造方法意在为类中的属性赋值，但是其实从构造方法传递的参数名称上很难看出n或者a表示的意义，所以进行如下的修改：

~~~java
class Person{
    private String name;
    private int age;
    public Person(String name, int age){
        name = name;
        age = age;
    }
    public String getInfo(){
        return "姓名：" + name + "，年龄：" + age;
    }
}
~~~

这个时候就能看出构造方法中两个参数表示的意思了，但是同时也出现了新的问题，构造方法的本意是要将参数传递的name赋值给类中的name属性，把age的值赋给age属性，但是实际运行出来的结果却和我们想像的并不一样，例如：

~~~java
class Person01{
    private String name;
    private int age;
    public Person01(String name, int age){
        name = name;
        age = age;
    }
    public String getInfo(){
        return "姓名：" + name + "，年龄：" + age;
    }
}
public class ThisDemo01 {
    public static void main(String[] args) {
        Person01 per1 = new Person01("张三",33);
        System.out.println(per1.getInfo());
    }
}
~~~

程序运行结果为：`姓名：null，年龄：0`

从结果来看，程序并没有将构造方法传递进去的参数赋值给属性，也就是说，现在的构造方法并不能将传递进去的参数值赋给类中的熟悉你个，这是由于在赋值时，属性并没有被明确的指出，而这种错误可以利用this关键字来结果，例如进行如下的修改：

~~~java
class Person02{
    private String name;
    private int age;
    public Person02(String name, int age){
        this.name = name;                     // 明确表示为类中的name属性赋值
        this.age = age;                       // 明确表示为类中的age属性赋值
    }
    public String getInfo(){
        return "姓名：" + name + "，年龄：" + age;
    }
}
public class ThisDemo02 {
    public static void main(String[] args) {
        Person02 per2 = new Person02("张三", 33);
        System.out.println(per2.getInfo());
    }
}
~~~

程序运行结果：`姓名：张三，年龄：33`

> 实际上上面程序中的“name = name”、“age = age”中的两个name和两个age都是构造方法中的参数。更实际中的就近原则相似，在程序的构造方法中，已经存在了name和age属性，那么在构造方法中如果要使用name或age属性，则肯定按照就近取用的原则，所以上面的name和age使用都是构造方法中的参数。

### 使用this调用构造方法

如果一个类中有多个构造方法，也可以利用this关键字互相调用。

假设现在要求不管类中有多少个构造方法，只要对象一被实例化，就打印一行“一个新的对象被实例化”信息出来，很明显，如果在每个构造方法中编写此输出语句肯定不是最佳方法，所以可以利用this关键字完成，如下：

~~~java
class Person03{
    private String name;
    private int age;
    public Person03(){
        System.out.println("一个新的Person对象被实例化");
    }
    public Person03(String name, int age){
        this();                                            // 在此处调用Person类中的无参构造方法
        this.name = name;                                  // 为name属性赋值
        this.age = age;                                    // 为age属性赋值
    }
    public String getInfo(){
        return "姓名：" + name + "，年龄：" + age;
    }
}
public class ThisDemo03 {
    public static void main(String[] args) {
        Person03 per1 = new Person03("张三", 33);
        System.out.println(per1.getInfo());
    }
}
~~~

程序运行结果：

~~~
一个新的Person对象被实例化
姓名：张三，年龄：33
~~~

该程序中提供了两个构造方法，其中有两个参数的构造方法中使用this()的形式调用该类中的无参构造方法，所以即使是通过有两个参数的构造方法实例化，最终结果还是会把无参构造方法中的内容打印出来。

另外需要注意的是，在使用this()调用构造方法的时候，由于构造方法是在实例化对象时被自动调用，也就是说在类中的所有方法中，只有构造方法是被优先调用的，所以使用this调用构造方法必须也只能放在构造方法的首行，下面就是一个错误的例子：

~~~java
class Person{
    private String name;
    private int age;
    public Person(){
        system.out.println("一个新的Person对象被实例化。");
    }
    public Person(String name, int age){
        this.name = name;
        this.age = age;
        this();                                          // 错误的调用，只能放在构造方法的首行
    }
    public String getInfo(){
        this();                                          // 错误的调用，只能放在构造方法的首行
        return "姓名：" + name + "，年龄：" + age;
    }
}
~~~

另外，this调用构造方法时一定要留一个构造方法作为出口，即程序中至少有个构造方法是不使用this调用其他构造方法的。一般都会将无参构造方法作为出口，即在无参构造方法中最好不要再去调用其他构造方法。

### this表示当前对象

this最重要的特点就是表示当前对象，在Java中当前对象就是指当前正在调用类中方法的对象。

~~~java
class Person04{
    public String getInfo(){
        System.out.println("Person类 --> " + this);         // 直接打印this
        return null;                                        // 此处返回null，为的是让语法不出错
    }
}
public class ThisDemo06 {
    public static void main(String[] args) {
        Person04 per1 = new Person04();
        Person04 per2 = new Person04();
        System.out.println("MAIN方法 --> " + per1);         // 直接打印对象
        per1.getInfo();
        System.out.println("----------------------------");
        System.out.println("MAIN方法 --> " + per2);         // 直接打印对象
        per2.getInfo();
    }
}
~~~

程序运行结果：

~~~
MAIN方法 --> ThisDemo.Person04@21bcffb5
Person类 --> ThisDemo.Person04@21bcffb5
----------------------------
MAIN方法 --> ThisDemo.Person04@380fb434
Person类 --> ThisDemo.Person04@380fb434
~~~

从结果来看，直接打印对象和调用getInfo()方法打印的结果是一样的，而且在getInfo()方法中打印的永远是this关键字，也就是说哪个对象调用了类中的方法，this就表示哪个对象。

这样一个特性有什么用处呢？通过下面一个例子来理解：

~~~

~~~





