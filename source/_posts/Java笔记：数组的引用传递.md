---
title: Java笔记：数组的引用传递
date: 2019-04-05 16:11:43
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

### 传递及返回数组

前面的方法操作中，传递和返回的都是基本数据类型，除此之外，方法中也可以传递和返回数组。如果要向方法中传递一个数组，则方法的接收参数必须是符合其类型的数组。而且数组属于引用数据类型，所以在把数组传递进方法之后，如果方法对数组本身做了任何修改，修改结果也将保存下来。

<!-- more -->

向方法中传递数组：

~~~java
public class ArrayDefDemo01 {
    public static void main(String[] args) {
        int temp[] = {1, 3, 5};                  // 使用静态初始化定义数组
        fun(temp);                               // 传递数组引用
        for (int i = 0; i < temp.length; i++){   // 循环输出
            System.out.print(temp[i] + "、");
        }
    }
    public static void fun(int x[]){             // 接收整型数组引用
        x[0] = 6;                                //修改第1个元素的内容
    }
}
~~~

程序运行结果为：`6、3、5、`

在程序中将第一个整型数组temp传递到了方法中，然后在fun()方法中将此整型数组的第一个元素的内容修改为6，因为数组是引用数据类型，所以，即使方法本身没有任何的返回值，修改后的结果也会被保存下来。一开始声明的temp数组的内容是“1、3、5”，但是将此数组传递到了方法中，并使用数组x接收，也就是说此时temp实际上是将堆内存空间的使用权传递给了方法，为数组的具体内容起了一个别名x，然后在方法中通过x修改数组中的内容，方法执行完毕之后，数组x因为是局部变量所以就失效了，但是对于数组内容的改变却保留了下来，也就是**数组引用传递的过程**。

既然方法可以接收一个数组，那么方法也可以返回一个数组，只需要返回值类型声明处明确地写出返回的数据类型即可。例如：

~~~java
public class ArrayRefDemo02 {
    public static void main(String[] args) {
        int temp[] = fun();                   // 通过方法实例化数组
        print(temp);                          // 向print()方法中传递数组
    }
    public static void print(int x[]){        // 接收数组
        for (int i = 0; i < x.length; i++){   // 循环输出
            System.out.print(x[i] + "、");
        }
    }
    public static int[] fun(){
        int ss[] = {1, 3, 5, 7, 9};          // 定义一个数组
        return ss;                           // 返回数组
    }
}
~~~

程序运行结果：`1、3、5、7、9、`。

### 范例——数组排序

将数组排序程序修改成一个方法的调用形式：

~~~java
public class ArrayDefDemo03 {
    public static void main(String[] args) {
        int score[] = {67, 89, 87, 69, 90, 100, 75, 90};
        int age[] = {31, 30, 18, 17, 8, 9, 1, 39};
        sort(score);                                      // 数组排序
        print(score);                                     // 数组打印
        System.out.println("\n----------------------------------------");
        sort(age);                                      // 数组排序
        print(age);                                     // 数组打印
    }
    public static void sort(int temp[]){
        for (int i = 1; i < temp.length; i++){            // 使用冒泡排序算法
            for (int j = 0; j < temp.length; j++){
                if (temp[i]<temp[j]){
                    int x = temp[i];
                    temp[i] = temp[j];
                    temp[j] = x;
                }
            }
        }
    }
    public static void print(int x[]){
        for (int i = 0; i<x.length; i++){
            System.out.print(x[i] + "\t");
        }
    }
}
~~~

程序运行结果为：

~~~
67	69	75	87	89	90	90	100	
----------------------------------------
1	8	9	17	18	30	31	39	
~~~

以上程序分别把排序和输出的功能定义为方法，然后直接调用这两个方法进行数组的排序和输出。

当然，对于排序操作，Java本身也是有类库支持的，我们可以直接使用“java.util.Arrays.sort(数组名称)”对数组进行排序，例如：

~~~java
public class ArrayDefDemo04 {
    public static void main(String[] args) {
        int score[] = {67, 89, 87, 69, 90, 100, 75, 90};
        int age[] = {31, 30, 18, 17, 8, 9, 1, 39};
        java.util.Arrays.sort(score);                     // 使用Java提供的排序操作
        print(score);                                      // 输出数组
        System.out.println("\n-------------------------------");
        java.util.Arrays.sort(age);
        print(age);
    }
    public static void print(int x[]){
        for (int i = 0; i<x.length; i++){
            System.out.print(x[i] + "\t");
        }
    }
}

~~~

程序运行结果为：

~~~
67	69	75	87	89	90	90	100	
-------------------------------
1	8	9	17	18	30	31	39
~~~

### 范例——数组复制

如果给定两个数组，将其中一个数组指定位置的内容复制给另外一个数组，可以是使用方法来完成，在方法中接收5个参数，分别为“源数组名称”、“源数组开始点”、“目标数组名称”、“目标数组开始点”、“复制长度”。具体操作如下：

~~~java
public class ArrayCopyDemo01 {
    public static void main(String[] args) {
        int i1[] = {1, 2, 3, 4, 5, 6, 7, 8, 9};             // 源数组
        int i2[] = {11, 22, 33, 44, 55, 66, 77, 88, 99};    // 目标数组
        copy(i1, 3, i2, 1, 3);                // 调用复制方法
        print(i2);                                          // 输出数组
    }
    // 参数含义：源数组名称、源数组开始点、目标数组名称、目标数组开始点、复制长度
    public static void copy(int s[], int s1, int o[], int s2, int len){
        for (int i = 0; i < len; i++){
            o[s2+i] = s[s1+i];                             // 修改目标数组内容
        }
    }
    public static void print(int x[]){
        for (int i = 0; i<x.length; i++){
            System.out.print(x[i] + "\t");
        }
    }
}
~~~

程序运行结果为：`11	4	5	6	55	66	77	88	99`。

同样的，在Java中也存在复制的类库支持，直接使用System.arraycopy()方法即可，此方法中也要接收参数，参数的接收顺序及意义与上面的范例中的copy()方法相同。例如：

~~~java
public class ArrayCopyDemo02 {
    public static void main(String[] args) {
        int i1[] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
        int i2[] = {11, 22, 33, 44, 55, 66, 77, 88, 99};
        System.arraycopy(i1, 3, i2, 1,3);
        print(i2);
    }
    public static void print(int x[]){
        for (int i = 0; i<x.length; i++){
            System.out.print(x[i] + "\t");
        }
    }
}
~~~

