---
title: Java笔记：String
date: 2019-05-16 17:05:40
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

**前言**

> String类定义时单词的首字母大写，所以String本身也是一个类本类，但是此类在使用时却有很多的要求，而且此类在Java中也算是一个比较特殊的类。

<!-- more -->

### 实例化String对象

对于String可以采用直接赋值的方式进行操作，如下面的代码：

~~~java
public class StringDemo01 {
    public static void main(String[] args) {
        String name = "LiXingHua";            // 实例化String对象
        System.out.println("姓名：" + name);  // 输出字符串的内容
    }
}
~~~

在String的使用上还有另外一种形式的实例化方法，就是直接调用String类中的构造方法，在String类存在以下的构造方法：

~~~java
public String(String original)
~~~

所以上面的代码也可以通过如下的代码进行编写：

~~~java
public class StringDemo02 {
    public static void main(String[] args) {
        String name = new String("LiXingHua");        // 实例化String对象
        System.out.println("姓名：" + name);          // 输出字符串的内容
    }
}
~~~

### String的内容比较

对于基本数据类型，可以通过“==”进行内容的比较，如下面的代码：

~~~java
public class StringDemo03 {
    public static void main(String[] args) {
        int x = 30;                            // 声明一个整型变量
        int y = 30;                            // 声明一个整型变量
        System.out.println("两个数字的比较结果：" + (x == y));
    }
}
~~~

程序运行结果：`两个数字的比较结果：true`

下面按照以上的程序思路进行两个字符串的比较操作：

~~~java
public class StringDemo04 {
    public static void main(String[] args) {
        String str1 = "hello";                          // 直接赋值
        String str2 = new String("hello");     // 通过new赋值
        String str3 = str2;                             // 传递引用
        System.out.println("str1 == str2 -->" + (str1 == str2));
        System.out.println("str1 == str3 -->" + (str1 == str3));
        System.out.println("str2 == str3 -->" + (str2 == str3));
    }
}
~~~

程序运行结果为：

~~~
str1 == str2 -->false
str1 == str3 -->false
str2 == str3 -->true
~~~

从程序运行结果中可以发现，虽然以上程序中String的内容都一样，但是比较结果有的相同，有的却不同。主要原因在于堆内存和栈内存。上面每个String对象的内容实际上都保存在堆内存中，而且堆内存中的内容相等。但是对于str1和str2来说，其内容分别保存在了不同的空间，所以即使内容相等，地址的值也是不相等的，“==”是用来进行数值比较的，所以str1和str2不相等。从程序中可以发现str2和str3指向了同一个堆内存空间，是同一个地址，所以最终结果是str2和str3的地址值相等的，同理str1和str3的地址值是不相等的，所以返回了false。栈内存和堆内存的示意图如下：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88String%EF%BC%89/String%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%A3%B0%E6%98%8E.png)

那么既然无法使用“==”进行判断，那该如何去判断两个字符串的内容是否相等呢？此时，即可利用String中专门提供的方法（String是一个类，则会存在各种方法）：

~~~java
public boolean equals(String str)
~~~

例如，使用equals方法对String的内容进行比较：

~~~java
public class StringDemo05 {
    public static void main(String[] args) {
        String str1 = "hello";                         // 直接赋值
        String str2 = new String("hello");             // 通过new赋值
        String str3 = str2;                            // 传递引用
        System.out.println("str1 equals str2 -->" + (str1.equals(str2)));
        System.out.println("str1 equals str3 -->" + (str1.equals(str3)));
        System.out.println("str2 equals str2 -->" + (str2.equals(str3)));
    }
}
~~~

程序运行结果：

~~~
str1 equals str2 -->true
str1 equals str3 -->true
str2 equals str2 -->true
~~~

因为equals()方法的作用是将内容进行比较，所以此处返回的结果都为true。

### String两种实例化方式的区别

String又两种实例化方式，一种是通过直接赋值的方式，另一种是使用标准的new调用构造方式完成实例化。一个字符串就是一个String类的匿名对象，匿名对象就是已经开辟了堆内存空间的并可以直接使用的对象。

验证一个字符串就是String的匿名对象：

~~~java
public class StringDemo06 {
    public static void main(String[] args) {
        System.out.println("\"hello\" equals \"hello\" -->" + ("hello".equals("hello")));
    }
}
~~~

程序运行结果：`"hello" equals "hello" -->true`

从结果可以发现，一个字符串确实可以调用String类中的方法，也就证明了一个字符串就是一个String类的匿名对象。所以对于以下代码：

~~~java
String str1 = "hello";
~~~

实际上就是把一个堆中开辟好的内存空间的使用权给了str1对象，而使用这种方式还有另一个好处，就是如果一个字符串已经被一个名称所引用，则以后再有相同的字符串声明时，就不会重新开辟空间，而是继续使用已经开辟好的堆内存。例如：

~~~java
public class StringDemo07 {
    public static void main(String[] args) {
        // 声明3个字符串变量，每个变量的内容都是一样的
        String str1 = "hello";
        String str2 = "hello";
        String str3 = "hello";
        System.out.println("str1 == str2 -->" + (str1 == str2));
        System.out.println("str1 == str3 -->" + (str1 == str3));
        System.out.println("str2 == str3 -->" + (str2 == str3));
    }
}
~~~

程序运行结果：

~~~
str1 == str2 -->true
str1 == str3 -->true
str2 == str3 -->true
~~~

三种比较都是true，说明3个字符串指向的堆内存地址空间都是同一个，所以，当String使用直接赋值的方式之后，只要是声明的字符串内容相同，则都不会再开辟新的内存空间。

> **在Java中会提供一个字符串池来保存全部的内容**
>
> 对于String的以上操作，在Java中称为共享设计，这种设计思路是，在Java中形成一个对象池，在这个对象池中保存多个对象，新实例化的对象如果已经在池中定义了，则不再重新定义，而是从池中直接取出继续使用。String就是因为采用了这样的设计，所以当内容重复时，会将对象指向已存在的实例空间。

下面为使用new String()的方式实例化String对象的例子：

~~~java
public class StringDemo08{
    public static void main(String[] args){
        String str = new String("hello");
    }
}
~~~

一个字符串就是一个String类的匿名对象，而如果使用new关键字，不管如何都会再开辟一个新的空间，但是此时，此空间的内容还是hello，所以上面的代码实际上是开辟了两个内存空间，但真正使用的只是一个使用关键字new开辟的空间，另外一个就是垃圾空间了，如图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88String%EF%BC%89/new%E5%8A%A0String%E6%96%B9%E5%BC%8F%E5%AE%9E%E7%8E%B0%E5%AE%9E%E4%BE%8B%E5%8C%96%E5%AF%B9%E8%B1%A1.png)

通过以上两种实现方式比较可以知道那种方式更合适，对于字符串的操作就采用直接赋值的方式完成，而不要采用构造方法传递字符串的方式完成，这样可以避免产生垃圾空间，当然，在String类中也存在一些其他的构造方法。

### 字符串的内容不可改变

在使用String类进行操作时还有一个特性是特别重要的，那就是字符串的内容一旦声明则不可以改变。例如：

~~~java
public class StringDemo09 {
    public static void main(String[] args) {
        String str = "hello";        // 声明字符串
        str = str + " world!";        // 修改字符串
        System.out.println("str = " + str);
    }
}
~~~

程序运行结果：`str = hello world!`。

从结果来看，String对象的内容确实已经修改了，但是其实String对象内容的改变是通过内存地址的“断开-连接”变化完成的，而本身字符串中的内容并没有任何变化，具体如下图：

![](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88String%EF%BC%89/%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%86%85%E5%AE%B9%E7%9A%84%E4%BF%AE%E6%94%B9.png)

### String类中常用的方法

#### 字符串与字符数组的转换

字符串可以使用toCharArray()方法变成一个字符数组，也可以使用String类的构造方法把一个字符数组变成一个字符串。

~~~java
public class StringAPIDemo01 {
    public static void main(String[] args) {
        String str1 = "hello";                    // 定义字符串
        char c[] = str1.toCharArray();            // 将字符串变为字符数组
        for (int i = 0; i < c.length; i++){       // 循环输出
            System.out.print(c[i] + "\t");
        }
        System.out.println("");
        String str2 = new String(c);              // 将全部字符数组变为String
        String str3 = new String(c, 0, 3);        // 将部分字符数组变为String
        System.out.println(str2);                 // 输出字符串
        System.out.println(str3);                 // 输出字符串
    }
}

~~~

程序运行结果：

~~~
h	e	l	l	o	
hello
hel
~~~

程序一开始将一个字符串变成一个字符数组，字符串的长度就是转换之后字符数组的长度，也可以把一个字符数组的全部或者部分转换为字符串。

#### 从字符串中取出指定位置的字符

可以使用String类中的charAt()方法去除字符串指定位置的字符。

~~~java
public class StringAPIDemo02 {
    public static void main(String[] args) {
        String str1 = "hello";                 // 声明String对象
        System.out.println(str1.charAt(3));    // 取出字符串中的第4个字符
    }
}
~~~

程序最终取出的字符为“l”，因为字符从0开始编号，编号为3的字符为“l”。

#### 字符串与byte数组的转换

字符串可以通过getBytes()方法将String变为一个byte数组，然后可以通过String的构造方法将一个字节数组重新变为字符串。

~~~java
public class StringAPIDemo03 {
    public static void main(String[] args) {
        String str1 = "hello";
        byte b[] = str1.getBytes();                  // 将字符串变为byte数组
        System.out.println(new String(b));           // 将全部byte数组变为字符串
        System.out.println(new String(b, 1, 3));     // 将部分byte数组变为字符串
    }
}
~~~

程序运行结果：

~~~
hello
ell
~~~

#### 取得一个字符串的长度

在String中使用length()方法取得字符串的长度。

~~~java
public class StringAPIDemo04 {
    public static void main(String[] args) {
        String str1 = "hello LiXingHua";          // 定义字符串变量
        System.out.println("\"" + str1 + "\" 的长度为：" + str1.length());
    }
}
~~~

程序运行结果：`"hello LiXingHua" 的长度为：15`。

> **length和length()的区别**
>
> 在数组操作中，使用length取得数组的长度，但是操作的最后没有“()”，而字符串调用length是一个方法，只要是方法后面都有“()”。

#### 查找一个指定的字符串是否存在

在String中使用indexOf()方法，可以返回指定的字符串的位置，如果不存在则返回-1，例如：

~~~java
public class StringAPIDemo05 {
    public static void main(String[] args) {
        String str1 = "abcdefgcgh";
        System.out.println(str1.indexOf("c"));        // 查到返回位置
        System.out.println(str1.indexOf("c", 3));       // 查到返回位置，从第4个开始查找
        System.out.println(str1.indexOf("x"));        // 没有查到返回-1
    }
}
~~~

程序运行结果：

~~~
2
7
-1
~~~

#### 去掉左右空格

使用trim()方法可以去掉字符串左、右空格，例如：

~~~java
public class StringAPIDemo06 {
    public static void main(String[] args) {
        String str1 = "     hello           ";
        System.out.println(str1.trim());           // 去掉左右空格后输出
    }
}
~~~

程序运行结果为：`hello`

从程序运行的结果来看，字符串左右两边的空格都被清除掉了。

#### 字符串截取

在String中提供了两个substring()方法，一个是从指定位置截取到字符串结尾i，另一个是截取指定范围的内容。例如：

~~~java
public class StringAPIDemo07 {
    public static void main(String[] args) {
        String str1 = "hello world";
        System.out.println(str1.substring(6));       // 从第7个位置开始截取
        System.out.println(str1.substring(0, 5));    // 截取0~5个位置的内容
    }
}
~~~

程序运行结果：

~~~
world
hello
~~~

需要注意的是，当截取指定范围的字符串时，截取的内容包括空号中前一个数字指定的位置，不包括括号中后一个数字指定的位置。

#### 按照指定的字符串拆分字符串

在String中通过split()方法可以进行字符串的拆分操作，拆分的数据将以字符串数组的形式返回。例如：

~~~java
public class StringAPIDemo08 {
    public static void main(String[] args) {
        String str1 = "hello world";
        String s[] = str1.split(" ");        // 按空格进行字符串的拆分
        for (int i = 0; i < s.length; i++){
            System.out.println(s[i]);
        }
    }
}
~~~

程序运行结果：

~~~
hello
world
~~~

#### 字符串的大小写转换

在用户输入信息时，有时需要统一输入数据的大小写，此时就可以使用toUpperCase()和toLowerCase()两个方法完成字符串大小写的转换操作。

~~~java
public class StringAPIDemo09 {
    public static void main(String[] args) {
        System.out.println("将\"hello world\"转换成大写：" + "hello world".toUpperCase());
        System.out.println("将\"HELLO WORLD\"转换成小写：" + "HELLO WORLD".toLowerCase());
    }
}
~~~

程序运行结果：

~~~
将"hello world"转换成大写：HELLO WORLD
将"HELLO WORLD"转换成小写：hello world
~~~

#### 判断是否以指定的字符串开头或结尾

在String中使用startsWith()方法可以判断字符串是否以指定的内容开头，使用endsWith()方法可以判断字符串是否以指定的内容结尾。

~~~java
public class StringAPIDemo10 {
    public static void main(String[] args) {
        String str1 = "**HELLO";
        String str2 = "HELLO**";
        if (str1.startsWith("**")){
            System.out.println("(**HELLO)以 ** 开头");
        }
        if (str2.endsWith("**")){
            System.out.println("(HELLO**)以 ** 结尾");
        }
    }
}
~~~

程序运行结果：

~~~
(**HELLO)以 ** 开头
(HELLO**)以 ** 结尾
~~~

#### 不区分大小写进行字符串笔记

在String中可以通过equals()方法进行字符串内容的比较，但是这种比较方法是区分大小写的比较，如果要完成不区分大小写的比较则可以使用equalsIgnoreCase()方法。

~~~java
public class StringAPIDemo11 {
    public static void main(String[] args) {
        String str1 = "HELLO";
        String str2 = "hello";
        System.out.println("\"HELLO\" equals \"hello\": " + str1.equals(str2));        // 区分大小写比较
        System.out.println("\"HELLO\" equalsIngoreCase \"hello\": " + str2.equalsIgnoreCase(str2));         // 区分大小写比较
    }
}
~~~

程序运行结果：

~~~
"HELLO" equals "hello": false
"HELLO" equalsIngoreCase "hello": true
~~~

#### 将一个指定的字符串替换成其他的字符串

使用String的replaceAll()方法可以将字符串的指定内容进行替换。

~~~java
public class StringAPIDemo12 {
    public static void main(String[] args) {
        String str = "hello";
        String newStr = str.replaceAll("l", "x");    // 将所有的l替换成x
        System.out.println("替换之后的结果：" + newStr);
    }
}
~~~

程序运行结果为：`替换之后的结果：hexxo`

