---
title: Java开发实战经典习题4-6
date: 2019-04-05 18:36:08
tags:
- Java练习
copyright: true
categories: Java
mathjax: true
---

**前言**

> Java开发实战第四章习题：数组与方法。掌握数组的定义及使用方法、掌握数组的应用传递、掌握方法及方法的重载、使用方法接收和返回一个数组、了解Java对数组的操作支持。

<!-- more -->

#### 编写程序求1!+2!+···+30!的和并显示，要求使用方法完成。

~~~java
public class Test4_1 {
    public static void main(String[] args) {
        float sum = 0;
        for (int i = 1; i<31; i++){
            sum = sum + Factorial(i);
        }
        System.out.println("1!+2!+...+30! = " + sum);
    }
    public static float Factorial(int x){
        float temp = 1;
        for (int i = 1; i<=x; i++){
            temp = temp*i;
        }
        return temp;
    }
}
~~~

也可以利用递归的方法：

~~~java
public class Test4_1 {
    public static void main(String[] args) {
        float sum = 0;
        for (int i = 1; i<31; i++){
            sum = sum + Factorial(i);
        }
        System.out.println("1!+2!+...+30! = " + sum);
    }
    public static float Factorial(int x){
        if (x==1){
            return 1;
        } else {
            return x * Factorial(x-1);
        }
    }
}
~~~

程序运行结果为：`1!+2!+...+30! = 2.7441084E32`。

#### 定义一个由整数组成的数组，要求求出其中的奇数个数和偶数个数。

~~~java
public class Test4_2 {
    public static void main(String[] args) {
        int arr[] = {45, 32, 66, 77, 98};
        oddEven(arr);
    }
    public static void oddEven(int temp[]){
        int odd = 0;
        int even = 0;
        for (int i = 0; i<temp.length; i++){
            int n = temp[i] % 2;
            if (n==0){
                even = even + 1;
            }else {
                odd = odd +1;
            }
        }
        System.out.println("奇数个数为：" + odd);
        System.out.println("偶数个数为：" + even);
    }
}

~~~

#### 现在有如下的一个数组`int oldArr[]={1,3,4,5,0,0,6,6,0,5,4,7,6,7,0,5};`，要求将以上数组中值为0的项去掉，将不为0的值存入一个新的数组，生成新数组为`int newArr[]={1,3,4,5,6,6,5,4,7,6,7,5}`。

~~~java
public class Test4_3 {
    public static void main(String[] args) {
        int oldArr[] = {1, 3, 4, 5, 0, 0, 6, 6, 0, 5, 4, 7, 6, 7, 0, 5};
        int newArr[]= new int[oldArr.length];
        int j = 0;
        for (int i = 0; i<oldArr.length; i++){
            if (oldArr[i] != 0){
                newArr[j] = oldArr[i];
                j++;
            }
        }
        for (int i = 0; i<j; i++){
            System.out.print(newArr[i] + "\t");
        }
    }
}

~~~

#### 定义一个整型数组，求出数组元素的和、数组元素的最大值和最小值，并输出所求的结果。

~~~java
public class Test4_4 {
    public static void main(String[] args) {
        int arr[] = {1, 5, 6, 3, 8};
        print(arr);
    }
    public static void print(int temp[]){
        int sum = 0;
        int max = temp[0];
        int min = temp[0];
        for (int i = 0; i < temp.length; i++){
            sum = sum + temp[i];
            if (max < temp[i]){
                max = temp[i];
            }
            if (min > temp[i]){
                min = temp[i];
            }
        }
        System.out.println("数组元素之和为：" + sum);
        System.out.println("数组中的最大值为：" + max);
        System.out.println("数组中的最小值为：" + min);
    }
}
~~~

#### 给出10个整数（int型），然后任意查询一个数字是否存在再该10个数字内。

~~~java
public class Test4_5 {
    public static void main(String[] args) {
        int arr[] = {2, 3, 4, 5, 6};
        int num1 = 3;
        int num2 = 7;
        print(num1, arr);
        print(num2, arr);
    }
    public static void print(int x, int temp[]){
        int count = 0;
        for (int i = 0; i<temp.length; i++){
            if (x == temp[i]){
                count++;
            }
        }
        if (count>0){
            System.out.println(x + "在这十个数中");
        }else {
            System.out.println(x + "不在这十个数中");
        }
    }
}
~~~

#### 定义一个包含10个元素的数组，对其进行赋值，使每个元素的值等于其下标，然后输出；最后将这个数组倒置（即首尾交换）后输出。

~~~java
public class Test4_6 {
    public static void main(String[] args) {
        int arr[] = new int[10];
        for (int i = 0; i<arr.length; i++){
            arr[i] = i;
        }
        for (int j = arr.length-1; j>=0; j--){
            System.out.print(arr[j] + "\t");
        }
    }
}
~~~

#### 给出10个老师的打分，对10个老师的打分找到最高分。

~~~java
public class Test4_7 {
    public static void main(String[] args) {
        int score[] = {67, 88, 78, 69, 100, 57, 81, 89, 94, 91};
        int max = 0;
        for (int i = 0; i<score.length; i++){
            if (max<score[i]){
                max = score[i];
            }
        }
        System.out.println("10个老师打分中最高分为：" + max);
    }
}
~~~

#### 有30个0\~9之间的数字，分别统计0~9这10个数字分别出现了多少次。

~~~java
public class Test4_8 {
    public static void main(String[] args) {
        int arr[] = {0,1,2,3,1,3,2,5,3,8,9,1,4,2,0,5,7,3,5,3,7,9,0,2,3,5,7,8,9,2};
        for (int i = 0; i<10; i++){
            int num = count(i, arr);
            System.out.println(i + "在数组中出现的次数为：" + num);
        }
    }
    public static int count(int x, int temp[]){
        int num = 0;
        for (int i = 0; i<temp.length; i++){
            if (x==temp[i]){
                num++;
            }
        }
        return num;
    }
}
~~~

#### 定义一个整型数组，保存10个数据，利用程序完成将最大值保存在数组中的第一个元素的操作。

~~~java
public class Test4_9 {
    public static void main(String[] args) {
        int arr[] = {9, 45, 11, 22, 33, 44, 51, 65, 21, 200};
        int max = arr[0];
        int num = 0;
        System.out.println("原数组为：");
        for (int i = 0; i<arr.length; i++){
            System.out.print(arr[i] + "\t");
        }
        for (int j = 0; j<arr.length; j++){
            if (max<arr[j]){
                max = arr[j];
                num = j;
            }
        }
        int temp = arr[0];
        arr[0] = max;
        arr[num] = temp;
        System.out.println(" ");
        System.out.println("最大值保存在数组中的第一个元素后:");
        for (int i = 0; i<arr.length; i++){
            System.out.print(arr[i] + "\t");
        }
    }
}
~~~

#### 在排序号的数组中添加一个数字，将添加后的数组插入到数组合适的位置。

~~~java
public class Test4_10 {
    public static void main(String[] args) {
        int num = 10;
        int arr[] = {2, 5, 9, 11, 13};
        insert(num, arr);
    }
    public static void insert(int x, int arr[]){
        int newArr[] = new int[arr.length+1];
        int temp = 0;
        for (int i = 0; i<arr.length; i++){
            if (x<arr[i]){
                temp = i;
                newArr[temp] = x;
                break;
            }else {
                temp = arr.length;   //如果要插入的数字是否比数组中最后一个数字大
                newArr[temp] = x;
            }
        }
        for (int j = 0; j<temp; j++){
            newArr[j] = arr[j];
        }
        for (int j = temp+1; j<newArr.length; j++){
            newArr[j] = arr[j-1];
        }
        for (int i = 0; i<newArr.length; i++){
            System.out.print(newArr[i] + "\t");
        }
    }
}
~~~
