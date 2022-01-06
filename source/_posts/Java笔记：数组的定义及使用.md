---
title: Java笔记：数组的定义及使用
date: 2019-03-30 15:43:06
tags:
- java基础
copyright: true
categories: Java
mathjax: true
---

**前言**

> **数组**是一组相关数据的集合，一个数组实际上就是一连串的变量，数组按使用可以分为**一维数组**、**二位数组**和**多维数组**。

<!-- more -->

### 一维数组

一维数组可以存放上千万个数据，并且这些数据的类型完全相同。要使用Java的数组，必须经过声明数组和分配内存给数组两个步骤，一维数组的声明与分配内存的语法结构如下：

~~~
数据类型 数组名[] = null;      // 声明一维数组
数组名 = new 数据类型[长度]；  // 分配内存给数组
~~~

对于数组的声明方式也可以用下面的形式：

~~~
数据类型[] 数组名 = null;     // 声明一维数组
~~~

在数组的声明格式中，“数据类型”指的是声明数组元素的数据类型，常见的类型有整型、浮点型与字符型等。“数组名”是用来统一这组相同数据类型的元素的名称，其命名规则和变量相同。数组声明后实际上在内存中保存了此数组的名称（实际上是保存对一堆内存的引用地址），接下来便要在堆内存中配置数组所需的内存。其中，“长度”是告诉编辑器所声明的数组要存放多少个元素，而关键字new则是命令编译器根据括号里的长度在堆内存中开辟一块堆内存供该数组使用，例如：

~~~java
int score[] = null;         // 声明整型数组score
score = new int[3];         // 为整型数组score分配内存空间，其元素个数为3
~~~

当声明一个整型数组score时，score可视为数组类型的变量，此时，这个变量并没有包含任何内容，编译器仅会在栈内存中分配一块内存给它，用来指向数组实体的地址的名称。声明之后，就要做堆内存分配的操作了，也就是上面第二行的语句，这一行会开辟3个可供保存整数的内存空间，并把此内存空间的参考地址赋给score变量。因为数组是引用数据类型，所以数组变量score所保存的并非是数组的实体，而是数组堆内存的参考地址。

> **堆栈内存的解释**
>
> 数组操作中，在栈内存中保存的永远是数组的名称，只开辟了栈内存空间的数组是永远无法使用的，必须有指向的堆内存才可以使用，要想开辟新的堆内存则必须使用关键字new，然后只是将此堆内存的使用权交给了对应的栈内存空间，而且一个堆内存空间可以同时被多个栈内存空间所指向。

另外，可以在声明数组的同时分配内存空间，其格式如下：

~~~
数据类型 数组名[] = new 数据类型[个数]
~~~

例如：

~~~Java
int score[] = new int[10];  //声明一个元素个数为10的整数数组score，同时开辟一块内存空间供其使用
~~~

### 数组中元素的表示方法

若要访问数组中的元素，可以利用索引来完成，Java的数组索引编号由0开始，以score[10]整型数组为例，score[0]代表第一个元素，而score[9]代表第10个元素，也就是最后一个元素。

数组的声明及输出：

~~~java
public class ArrayDemo01 {
    public static void main(String[] args) {
        int score[] = null;                            // 声明数组，但未开辟堆内存空间
        score = new int[3];                            // 为数组开辟堆内存空间
        System.out.println("score[0] = " + score[0]);  // 分别输出每个元素
        System.out.println("score[1] = " + score[1]);  // 分别输出每个元素
        System.out.println("score[2] = " + score[2]);  // 分别输出每个元素
        for (int x = 0; x < 3; x++){                   // 使用循环依此输出数组中的全部内容
            System.out.println("score["+x+"] = " + score[x]);
        }
    }
}
~~~

程序运行结果为：

~~~
score[0] = 0
score[1] = 0
score[2] = 0
score[0] = 0
score[1] = 0
score[2] = 0
~~~

从运行结果可以看出，对于数组的访问采用“数组名称[下标]”的方式，之前一共开辟了3个空间大小的数组，所以下标的取值为0~2，如果超出了这个下标，例如score[3]，则会出现如下错误：`java.lang.ArrayIndexOutOfBoundsException:3`。

此外，可以发现以上数组中的内容都是0，这是因为声明的是整型数组，而此时又没有为整型数组中的内容赋值，所以现在都是默认值，整型的默认值为0。下面的范例将为数组中的元素进行赋值并输出：

~~~java
public class ArrayDemo02 {
    public static void main(String[] args) {
        int score[] = null;
        score = new int[3];
        for (int x = 0; x < 3; x++){
            score[x] = x * 2 + 1;
        }
        for (int x = 0; x < 3; x++){
            System.out.println("score[" + x + "] = " + score[x]);
        }
    }
}
~~~

程序运行结果为：

~~~
score[0] = 1
score[1] = 3
score[2] = 5
~~~

在Java中取得数组的长度（也就是数组元素的长度）可以利用“数组名称.length”的形式，会返回一个int型数据。例如

~~~java
public class ArrayDemo03 {
    public static void main(String[] args) {
        int score[] = new int[3];
        System.out.println("数组长度为" + score.length);
    }
}
~~~

程序的运行结果为：`数组长度为3`

### 数组的静态初始化

数组的内容分为**动态初始化**和**静态初始化**两种，之前所讲的代码是采用先声明数组之后为数组中的每个内容赋值的方式完成的，所以属于数组的动态初始化，也可以通过数组静态初始化，在数组声明时就指定其具体内容，只要在数组的声明格式后面加上初值的赋值即可，如下：

~~~
数据类型 数组名[] = {初值0，初值1，···，初值n}
~~~

在大括号内的初值会依此指定给数组的第1、···、n个元素。此外，在声明时，并不需要将数组元素的个数列出来，编译器根据所给出的初值个数来判断数组的长度。

~~~java
public class ArrayDemo04 {
    public static void main(String[] args) {
        int score[] = {91, 92, 93, 94, 95, 96};
        for (int x = 0; x < score.length; x++){
            System.out.println("score[" + x + "] = " + score[x]);
        }
    }
}
~~~

程序运行结果为：

~~~
score[0] = 91
score[1] = 92
score[2] = 93
score[3] = 94
score[4] = 95
score[5] = 96
~~~

### 数组应用范例

1. **求出数组中的最大和最小值**

~~~java
public class ArrayDemo05 {
    public static void main(String[] args) {
        int score[] = {67, 89, 87, 69, 90, 100, 75, 90};      // 静态初始化数组
        int max = 0;                                          // 定义变量保存最大值
        int min = 0;                                          // 定义变量保存最小值
        max = min = score[0];                                 // 把第一个元素的内容赋值给max和min
        for (int x = 0; x < score.length; x++){
            if (score[x] > max){                              // 依此判断后续元素是否比max大
                max = score[x];                               // 如果大，则修改max内容
            }
            if (score[x] < min){                              // 依此判断后续的元素是否比min小
                min = score[x];                               // 如果小，则修改min内容
            }
        }
        System.out.println("最高成绩：" + max);               // 输出最大值
        System.out.println("最低成绩：" + min);               // 输出最小值
    }
}
~~~

程序运行结果：

~~~
最高成绩：100
最低成绩：67
~~~

本程序中，首先将数组的最大和最小值都当作数组中的第一个元素，然后用for循环依此和数组后面的元素比较，如果比当前的max值大，则将该值赋给max，如果比当前的min值小，则将该值赋给min，直到数组里的元素都比较完毕，max存储了数组中的最大值，min存储了数组里的最小值。

2. **对整型数组按照由小到大的顺序进行排列**

~~~java
public class ArrayDemo06 {
    public static void main(String[] args) {
        int score[] = {67, 89, 87, 69, 90, 100, 75, 90};   // 声明数组
        for (int i = 1; i < score.length; i++){            // 循环判断
            for (int j = 0; j < score.length; j++){
                if (score[i] < score[j]){                  // 交换位置
                    int temp = score[i];
                    score[i] = score[j];
                    score[j] = temp;
                }
            }
        }
        for (int i = 0; i < score.length; i++){
            System.out.println(score[i] + "\t");
        }
    }
}
~~~

程序运行结果为：`67	69	75	87	89	90	90	100`。

以上程序采用了冒泡算法进行排序。即把数组中的每个元素进行比较，如果第i个元素大于第i+1个元素，那么就要把两个数字进行交换，这样反复的比较就可以将一个数组按照由大到小的顺序进行排序。

3. **修改之前的代码，显示每次的排序结果**

~~~java
public class ArrayDemo07 {
    public static void main(String[] args) {
        int score[] = {67, 89, 87, 69, 90, 100, 75, 90};     // 声明数组
        for (int i = 1; i < score.length; i++){
            for (int j = 0; j < score.length; j++){
                if (score[i] < score[j]){
                    int temp = score[i];
                    score[i] = score[j];
                    score[j] = temp;
                }
            }
            System.out.print("第"+i+"次排序的结果：\t");
            for (int j = 0; j < score.length; j++){          // 循环输出
                System.out.print(score[j] + "\t");
            }
            System.out.println("");                         // 换行
        }
        System.out.print("最终的排序结果为：\t");
        for (int i = 0; i < score.length; i++){
            System.out.print(score[i] + "\t");
        }
    }
}
~~~

程序运行结果为：

~~~
第1次排序的结果：	67	100	87	69	89	90	75	90	
第2次排序的结果：	67	87	100	69	89	90	75	90	
第3次排序的结果：	67	69	87	100	89	90	75	90	
第4次排序的结果：	67	69	87	89	100	90	75	90	
第5次排序的结果：	67	69	87	89	90	100	75	90	
第6次排序的结果：	67	69	75	87	89	90	100	90	
第7次排序的结果：	67	69	75	87	89	90	90	100	
最终的排序结果为：	67	69	75	87	89	90	90	100	
~~~

### 二维数组

二维数组的声明方式和一维数组类似，内存的分配也要使用关键字new完成，其声明与分配内存的格式如下：

~~~
数据类型 数组名[][];
数组名 = new 数据类型[][];
~~~

与一维数组不同的是，二维数组在分配内存时，必须告诉编译器二维数组的行与列的个数，例如：

~~~java
int score[][];           // 声明整型数组score
score = new int[4][3];   // 配置一块内存空间，供4行3列的整型数组score使用
~~~

同样的，也可以利用较为简洁的声明和分配内存语句：

~~~
数据类型 数组名[][] = new 数据类型[行的个数][列的个数]
~~~

二维数组的定义及使用：

~~~java
public class ArrayDemo08 {
    public static void main(String[] args) {
        int score[][] = new int[4][3];         // 声明并实例化二维数组
        score[0][1] = 30;
        score[1][0] = 31;
        score[2][2] = 32;
        score[3][1] = 33;
        score[1][1] = 30;
        for (int i = 0; i < score.length; i++){
            for (int j = 0; j < score[i].length; j++){
                System.out.print(score[i][j] + "\t");
            }
            System.out.println("");
        }
    }
}

~~~

程序运行结果为：

~~~
0	30	0	
31	30	0	
0	0	32	
0	33	0	
~~~

可以看出，一维数组输出只需要使用一层循环，而二维数组全部输出则需要使用两层循环，同理，对于N维数组，则要使用N+1层循环。

二维数组也可以利用大括号进行静态初始化，只要在数组的声明格式后面再加上所赋的初值即可，格式如下：

~~~
数组类型 数组名[][] = {
    {第0行初值}，
    {第1行初值}，
    ···
    {第n行初值}
}；
~~~

要特别注意的是，用户不必定义数组的长度，因此，在数组名后面的中括号中不必填入任何内容。下面是二维数组声明及赋初值的例子：

~~~java
public class ArrayDemo09 {
    public static void main(String[] args) {
        // 静态初始化一个二维数组，每行的数组元素个数都不一样
        int score[][] = {{67, 61}, {78, 89, 83}, {99, 100, 98, 66, 95}};
        for (int i = 0; i < score.length; i++){
            for (int j = 0; j < score[i].length; j++){
                System.out.print(score[i][j] + "\t");
            }
            System.out.println("");
        }
    }
}
~~~

程序运行结果如下：

~~~
67	61	
78	89	83	
99	100	98	66	95	
~~~

### 多维数组

想要提高数组的维数，只要在声明数组时将索引与中括号再加一组即可，即三维数组的声明为`int score[][][]`，而四维数组的声明为`int score[][][][]`···，依此类推。使用多维数组时，输入、输出的方式和一维、二维数组相同，但是每多一维，嵌套循环的层数就必须多一层，所以维数越高的数组其复杂度也就越高。例如下面是三维数组的使用：

~~~java
public class ArrayDemo10 {
    public static void main(String[] args) {
        // 定义一个三维数组，使用静态初始化的方式
        int score[][][] = {{{5, 1}, {6, 7}}, {{9, 4}, {8, 3}}};
        for (int i = 0; i < score.length; i++){
            for (int j = 0; j < score[i].length; j++){
                for (int k = 0; k < score[i][j].length; k++){
                    System.out.println("score[" + i + "][" + j + "][" + k +"]=" + score[i][j][k]);
                }
            }
        }
    }
}
~~~

程序运行结果为：

~~~
score[0][0][0]=5
score[0][0][1]=1
score[0][1][0]=6
score[0][1][1]=7
score[1][0][0]=9
score[1][0][1]=4
score[1][1][0]=8
score[1][1][1]=3
~~~

