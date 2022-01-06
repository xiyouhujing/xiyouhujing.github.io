---
title: Java笔记：选择和循环语句
date: 2019-03-18 11:14:09
categories: Java
tags: java基础
mathjax: true
---

一般来说程序的结构可以分为**顺序结构**、**选择结构**以及**循环结构**三种，这三种结构只有一个共同点，就是它们只有一个入口，也只有一个出口，这些单一的入、出口可以让程序易读、好维护，也可以减少调试时间。

<!-- more -->

## 程序的结构

### 顺序结构

顺序结构下的程序至上而下的逐条执行，一条语句执行完之后继续执行下一条语句，一直到程序的末尾，其结构如下图所示：

![顺序结构流程图](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E9%80%89%E6%8B%A9%E5%92%8C%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5%EF%BC%89/%E7%A8%8B%E5%BA%8F%E7%9A%84%E9%A1%BA%E5%BA%8F%E7%BB%93%E6%9E%84%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

### 选择结构

选择结构的流程图如下，这种结构可以依据判断条件的结构来决定要执行的语句，当判断条件的值为真时，就运行语句1；当判断的条件为假，则执行语句2。不论执行哪一句，最后都会回到语句3继续执行。选择结构的流程图如下：

![选择结构流程图](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E9%80%89%E6%8B%A9%E5%92%8C%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5%EF%BC%89/%E7%A8%8B%E5%BA%8F%E7%9A%84%E9%80%89%E6%8B%A9%E7%BB%93%E6%9E%84%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

验证选择结构：

~~~java
public class IfDemo {
    public static void main(String[] args) {
        int x = 3;
        int y = 10;
        System.out.println("======比较开始=====");
        if (x > y){
            System.out.println("x比y大！");
        }
        if (x < y){
            System.out.println("x比y小！");
        }
        System.out.println("=====比较完成=====");
    }
}
~~~

程序运行结果：

~~~
======比较开始=====
x比y小！
=====比较完成=====
~~~

选择结构包括if、if···else及switch语句。

#### if语句

要根据判断的结果来执行不同的语句时，使用if语句是一个很好的选择，它会准确地判断条件成立与否，再决定是否要执行后面的语句。if语句的格式如下：

~~~
if (判断条件) {
    语句1;
    ···
    语句2;
}
~~~

当判断条件的值不满足时（true），就会逐一执行大括号里面所有的语句，否则执行大括号外的语句。

#### if···else语句

当程序中存在含有分支的判断语句时，就可以用if···else语句处理，当判断条件成立时，即执行if语句主题；判断条件不成立时，则会执行else后面的语句主题。if···else语句的格式如下：

~~~
if (判断条件) {
    语句主体1;
}else {
    语句主体2;
}
~~~

例如，通过if···else语句判断一个数字是奇数还是偶数：

~~~java
public class IfElseDemo {
    public static void main(String[] args) {
        int x = 3;
        if (x % 2 == 1) {
            System.out.println("x是基数！");
        }else {
            System.out.println("x是偶数！");
        }
    }
}
~~~

#### 三目运算符

三目运算符可以等价于使用if···else进行变量赋值的语句。如下表所示：

| 三目运算符 |                          意义                          |
| :--------: | :----------------------------------------------------: |
|     ?:     | 根据条件的成立与否来决定结果为“：”前或者“：”后的表达式 |

三目运算符的使用格式如下：

~~~
变量 = 条件判断?表达式1:表达式2
~~~

该语句的意思是，当条件成立时执行表达式1，否则执行表达式2，通常会将这两个表达式之一的运算结果指定给某个变量，用if···else表示为：

~~~
if (条件判断){
    变量x = 表达式1;
}else{
    变量x = 表达式2；
}
~~~

例如，使用三目运算符求出两个数字中的最大值：

~~~java
public class MaxDemo {
    public static void main(String[] args) {
        int max = 0;
        int x = 3;
        int y = 10;
        max = x > y ? x:y;
        System.out.println("最大值为：" + max);
    }
}
~~~

#### if···else if···else语句

如果需要在if···else中判断多个条件时，就需要if···else if···else语句了，其格式如下：

~~~
if (条件判断1) {
    语句主体1;
}else if (条件判断2) {
    语句主体2;
}
···     // 多个else if()语句
else{
    语句主体3;
}
~~~

例如：

~~~java
public class MoreIfElseDemo {
    public static void main(String[] args) {
        int x = 3;
        if (x ==1) {
            System.out.println("x的值是1！");
        }else if (x == 2) {
            System.out.println("x的值是2！");
        }else if (x == 3) {
            System.out.println("x的值是3！");
        }else {
            System.out.println("x的值不是1、2、3中的一个！");
        }
    }
}
~~~

#### switch语句

switch语句可以将多选一的情况简化，使程序简洁易懂，使用嵌套if···else语句最常发生的状况就是容易将if与else配对混淆，从而造成阅读及运行上的错误，而使用switch语句则可以避免这种错误发生，switch语句的格式如下：

~~~
switch (表达式) {
    case 选择值1:	语句主体1;
                   break；
    case 选择值2:	语句主体2：
                   break;
    ……
    case 选择值n:	语句主体n;
                   break;
    default:       语句主体;
}
~~~

特别注意的是，在switch语句中选择值只能是字符或常量，在JDK 1.5之后，switch也支持枚举类的判断。

switch语句执行的流程如下：

（1） switch语句先计算括号内的表达式结果，结果是数字、字符或者枚举。

（2）根据表达式的值检测是否符合case后面的选择值，若是所有case的选择值皆不符合，则执行default所包含的语句，执行完毕即离开switch语句。

（3）如果某个case的选择值符合表达式的结果，就会执行该case所包含的语句，一直遇到break语句后才离开switch语句

（4）如果没有在case语句结尾处加上break语句，则会一直执行到switch语句的尾端才离开switch语句。

（5）若是没有定义default执行语句，则什么都不会执行，直接退出switch语句。

根据以上描述，绘制如下的switch语句的流程图：

![switch语句的流程图](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E9%80%89%E6%8B%A9%E5%92%8C%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5%EF%BC%89/switch%E8%AF%AD%E5%8F%A5%E7%9A%84%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

以下程序验证了switch语句的作用：

~~~java
public class SwitchDemo01 {
    public static void main(String[] args) {
        int x = 3;
        int y = 6;
        char oper = '+';
        switch (oper){
            case '+':{
                System.out.println("x + y =" + (x + y));
                break;
            }
            case '-':{
                System.out.println("x - y = " + (x - y));
                break;
            }
            case '*':{
                System.out.println("x * y = " + (x * y));
                break;
            }
            case '/':{
                System.out.println("x / y = " + (x / y));
                break;
            }
            default:{
                System.out.println("未知操作！");
                break;
            }
        }
    }
}
~~~

程序的运行结果为：`x + y = 9`

> **break语句的作用**
>
> 从以上程序可以发现，在每一个case语句后面都加上了break语句，如果不加，则switch语句会从第一个满足条件的case开始依此执行操作，例如：
>
> ~~~java
> public class SwitchDemo02 {
>     public static void main(String[] args) {
>         int x = 3;
>         int y = 6;
>         char oper = '+';
>         switch (oper){
>             case '+':{
>                 System.out.println("x + y =" + (x + y));
>             }
>             case '-':{
>                 System.out.println("x - y =" + (x - y));
>             }
>             case '*':{
>                 System.out.println("x * y =" + (x * y));
>             }
>             case '/':{
>                 System.out.println("x / y =" + (x / y));
>             }
>             default:{
>                 System.out.println("未知操作！");
>             }
>         }
>     }
> }
> ~~~
>
> 最后得到的结果如下：
>
> ~~~
> x + y =9
> x - y =-3
> x * y =18
> x / y =0
> 未知操作！
> ~~~
>
> 从运行的结果可以发现，程序在满足第一个条件后，由于没有设置break语句，所以从第一个满足条件的语句case开始依此向后继续执行，知道最后一个条件执行完毕。

### 循环结构

#### while循环

while是循环语句，也是判断语句，当事前不知道循环执行多少次时，就要用while循环，其格式如下：

~~~
while (循环条件判断){
    语句1;
    语句2;
    ···
    语句n;
    循环条件改变；
}
~~~

在while循环语句中，只有一个判断条件，当判断条件为真时，循环就会执行一次，再重复测试判断条件，执行循环主体，知道判断条件为假，才会跳出while循环。下面是while循环的流程及流程图：

（1）第一次进入while循环前，必须先为循环控制变量（或表达式）赋起始值。

（2）根据判断条件的内容决定是否要继续执行循环，如果条件判断值为真（true），继续执行循环主体，若条件判断值为假（false），则跳出循环执行其他语句。

（3）执行完循环主体内的语句后，重新为循环控制变量（或表达式）赋值（增加或者减少），由于while循环不会自动更改循环控制变量（或表达式）的内容，所以while循环中为循环控制变量赋值的工作要自己来做，完成后再回到步骤（2）重新判断是否继续执行循环。

![while循环流程图](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E9%80%89%E6%8B%A9%E5%92%8C%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5%EF%BC%89/while%E5%BE%AA%E7%8E%AF%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

使用while循环进行累加操作：

~~~java
public class WhileDemo {
    public static void main(String[] args) {
        int x = 1;
        int sum = 0;
        while (x <= 10) {
            sum += x;
            x++;
        }
        System.out.println("1-->10累加结果为：" + sum);
    }
}
~~~

程序运行结果为：`1-->10累加结果为：55`

如果程序中没有修改循环条件（x++），那么程序将出现“死循环”的情况。

#### do···while循环

do···while循环也是用于未知循环执行次数的情况，而while循环及do···while循环最大的不同就是进入while循环前，while语句会先测试判断条件的真假，再决定是否执行循环主体，而do···while循环则是每次都是先执行一次循环主体，然后再测试判断条件的真假，**所以无论循环成立的条件是什么，使用do···while循环时，至少都会执行一次循环主体**。do···while循环的格式如下：

~~~
do{
    语句1;
    语句2;
    ···
    语句n;
    循环条件改变;
}while(循环条件判断)
~~~

下面描述的do···while循环的流程及流程图：

（1）进入do···while循环前，要先为循环控制变量（或表达式）赋起始值。

（2）直接执行循环主体，循环主体执行完毕，才开始根据判断条件的内容决定是否继续执行循环，条件为真（true）时，继续执行循环主体；条件为假（false）时，则跳出循环，执行其他语句。

（3）执行完循环主体内的语句后，重新为循环控制变量（或表达式）赋值（增加或减少），由于do···while循环和while循环一样，不会自动更改循环控制变量（或表达式）的内容，所以在do···while循环中赋值循环控制变量的工作要由自己来做，然后再回到步骤（2）重新判断是否继续执行循环。

![dowhile循环流程图](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E9%80%89%E6%8B%A9%E5%92%8C%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5%EF%BC%89/dowhile%E5%BE%AA%E7%8E%AF%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

使用while循环进行累加操作：

~~~java
public class DoWhileDemo {
    public static void main(String[] args) {
        int x = 1;
        int sum = 0;
        do {
            sum += x;
            x++;
        }while (x <= 10);
        System.out.println("1-->10累加结果为：" + sum);
    }
}
~~~

程序的运行结果为：`1-->10累加结果为：55`

从程序的运行结果来看，while和do···while的结果是一样的，但是do···while与while循环不同的是do···while操作中就算条件不满足，也至少会执行一次，而while如果条件不满足，则一次也不会被执行。

#### for循环

对于while和do···while两种循环来讲，操作时并不一定要明确地知道循环次数，而如果开发者已经明确地知道了循环次数，那么就可以使用另一种循环语句——for循环。for循环的格式如下：

~~~
for(赋值初值；判断条件；赋值增减量){
    语句1;
    ···
    语句n;
}
~~~

下面是for循环的流程和流程图：

（1）第一次进入for循环时，要为循环控制变量赋起始值。

（2）根据判断条件的内容检查是否继续执行循环，当判断条件为真（true）时，继续执行循环主体内的语句；判断条件为假（false）时，则会跳出循环，执行其他语句。

（3）执行完循环主体内的语句后，循环控制变量会根据增减量的要求更改循环控制变量的值，然后再回到步骤（2）重新判断是否继续执行循环。

![for循环流程图](https://raw.githubusercontent.com/xiyouhujing/TyporaPic/master/Java%E7%AC%94%E8%AE%B0%EF%BC%88%E9%80%89%E6%8B%A9%E5%92%8C%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5%EF%BC%89/for%E5%BE%AA%E7%8E%AF%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

使用for循环进行累加操作：

~~~java
public class ForDemo {
    public static void main(String[] args) {
        int sum = 0;
        for (int x = 1; x <= 10; x++){
            sum += x;
        }
        System.out.println("1-->10累加结果为：" + sum);
    }
}
~~~

程序的运行结果依旧如下：`1-->10累加结果为：55`

#### 循环的嵌套

多个循环语句是可以嵌套操作的，例如下面要打印一个九九乘法表：

~~~java
public class ForNestedDemo {
    public static void main(String[] args) {
        for (int i = 1; i <= 9; i++){
            for (int j = 1; j <= 9; j++){
                System.out.println(i + "*" + j + "=" + (i * j) + "\t");   // “\t”制表
            }
            System.out.println("\n");      // 换行
        }
    }
}
~~~

程序说明：

（1）i为外层循环的循环控制变量，j为内层循环的循环控制变量。

（2）当i为1时，符合外层for循环的判断条件（i<9），进入另一个内层for循环体，由于是第一次进入内层循环，所以j的初值为1，符合内层for循环的判断条件（j<=i）进入循环主体，输入i*j的值（1\*1=1），如果最后j的值任符合内层for循环的判断条件（j<=i），则再次执行计算与输出的工作，直到j的值大于i时，离开内层for循环，回到外层循环。此时，i会加1成为2，符合外层for循环的判断条件，继续执行内层for循环主体，直到i的值大于9时离开嵌套循环。

## 循环的中断

### break语句

break语句可以强迫程序中断循环，当程序执行到break语句时，即会离开循环，继续执行循环外的下一个语句，如果break语句出现在嵌套循环中的内层循环，则break语句只会跳出当前层的循环。下面用for循环为例，描述break语句的格式：

~~~
for (初值赋值；判断条件；设增减量){
    语句1；
    语句2；
    	···
    	break；
    ···      // 若执行break语句，则此块的语句将不会被执行
    语句n；
}
~~~

例如：

~~~java
public class BreakDemo {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++){
            if (i == 3){
                break;
            }
            System.out.println("i =" + i);
        }
    }
}
~~~

程序运行结果如下：

~~~
i =0
i =1
i =2
~~~

从结果可以看出，当i=3时，判断语句满足，则执行了break语句跳出了整个循环，因此没有输出i=3。

### continue语句

continue语句可以强迫程序跳到循环的起始处，当程序运行到continue语句时，会停止运行剩余的循环主体，而是回到循环的开始处继续运行。下面以for循环为例，描述continue语句的用法：

~~~
for (初值赋值；判断条件；设增减量){
    语句1；
    语句2；
    ···
    continue
    	···   // 若执行continue语句，则此处将不会被执行
    语句n；
}
~~~

例如：

~~~java
public class ContinueDemo {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            if (i == 3){
                continue;
            }
            System.out.println("i = " + i);
        }
    }
}
~~~

程序运行结果为：

~~~
i = 0
i = 1
i = 2
i = 4
i = 5
i = 6
i = 7
i = 8
i = 9
~~~

从结果中可以发现，当i的值为3时，程序并没有输出，而是退回了循环判断处继续向下执行，所以continue只是中断了一次的循环操作。

> 另外，在循环语句中定义的变量属于局部变量，所谓的局部变量是指此变量只能在循环语句中使用，而在循环语句之外则无法使用。

