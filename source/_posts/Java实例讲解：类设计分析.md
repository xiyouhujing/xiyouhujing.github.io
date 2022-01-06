---
title: Java实例讲解：类设计分析
date: 2019-05-15 15:53:25
tags:
- java实例
copyright: true
categories: Java
mathjax: true
---

### 题目

定义并测试一个名为Student的类，包括的属性有“学号”、“姓名”以及3门课程“数学”、“英语”和“计算机”的成绩，包括的方法有计算3门课程的“总分”、“平均分”、“最高分”以及“最低分”。

<!-- more -->

### 属性及类型

 序号 |    属性    | 属性类型 | 属性名称 
 :--: | :--------: | :------: | :------: 
  1   |    学号    |  String  |  stuno   
  2   |    姓名    |  String  |   name   
  3   |  数学成绩  |  float   |   math   
  4   |  英语成绩  |  float   | english  
   5   | 计算机成绩 |  float   | computer 

### 需要的方法

| 序号 | 方法名称                                                     | 返回值类型 | 作用                                                         |
| ---- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| 1    | public void setStuno(String s)                               | void       | 设置学生编号                                                 |
| 2    | public void setName(String n)                                | void       | 设置学生姓名                                                 |
| 3    | public void setMath(float m)                                 | void       | 设置数学成绩                                                 |
| 4    | public void setEnglish(float e)                              | void       | 设置英语成绩                                                 |
| 5    | public void setComputer(float c)                             | void       | 设置计算机成绩                                               |
| 6    | public String getStuno()                                     | String     | 取得学生编号                                                 |
| 7    | public String getName()                                      | String     | 取得学生姓名                                                 |
| 8    | public float getMath()                                       | float      | 取得数学成绩                                                 |
| 9    | public float getEnglish()                                    | float      | 取得英语成绩                                                 |
| 10   | public float getComputer()                                   | float      | 取得计算机成绩                                               |
| 11   | public float sum()                                           | float      | 计算成绩总和                                                 |
| 12   | public float avg()                                           | float      | 计算平均成绩                                                 |
| 13   | public float max()                                           | float      | 求出最高成绩                                                 |
| 14   | public float min()                                           | float      | 求出最低成绩                                                 |
| 151  | public Student()                                             | -          | 无参构造方法                                                 |
| 16   | public Student(String stuno, String name, float math, float english, float computer) | -          | 在对象实例化时直接将学号、姓名、数学成绩、英语成绩、计算机成绩设置进去 |

### 代码实现

~~~java
class Student{
    private String stuno;                      // 学生编号
    private String name;                       // 学生姓名
    private float math;                        // 数学成绩
    private float english;                     // 英语成绩
    private float computer;                    // 计算机成绩
    public Student(){                          // 定义无参构造
    }
    // 定义有五个参数的构造方法，为类中的属性初始化
    public Student(String stuno, String name, float math, float english, float computer){
        this.setStuno(stuno);
        this.setName(name);
        this.setMath(math);
        this.setEnglish(english);
        this.setComputer(computer);
    }
    public void setStuno(String s){             // 设置编号
        stuno = s;
    }
    public void setName(String n){              // 设置姓名
        name = n;
    }
    public void setMath(float m){               // 设置数学成绩
        math = m;
    }
    public void setEnglish(float e){             // 设置英语成绩
        english = e;
    }
    public void setComputer(float c){            // 设置计算机成绩
        computer = c;
    }
    public String getStuno(){                   // 取得编号
        return stuno;
    }
    public String getName(){                     // 取得姓名
        return name;
    }
    public float getMath(){                      // 取得数学成绩
        return math;
    }
    public float getEnglish(){                   // 取得英语成绩
        return english;
    }
    public float getComputer(){                  // 取得计算机成绩
        return computer;
    }
    public float sum(){
        return math + english + computer;        // 计算总分
    }
    public float avg(){                          // 计算平均分
        return this.sum() / 3;
    }
    public float max(){                          // 最高成绩
        float max = math;
        max = max > computer ? max : computer;     // 使用三目运算符
        max = max > english ? max : english;       // 使用三目运算符
        return max;
    }
    public float min(){                           // 最低成绩
        float min = math;
        min = math < computer ? math : computer;    // 使用三目运算符
        min = math < english ? math : english;      // 使用三目运算符
        return min;
    }
}

public class ExampleDemo01 {
    public static void main(String[] args) {
        Student stu = null;                       // 声明对象
        // 实例化Student对象，并通过构造方法赋值
        stu = new Student("MLDN-33", "李兴华", 95.0f, 89.0f, 96.0f);
        System.out.println("学生编号：" + stu.getStuno());
        System.out.println("学生姓名：" + stu.getName());
        System.out.println("数学成绩：" + stu.getMath());
        System.out.println("英语成绩：" + stu.getEnglish());
        System.out.println("计算机成绩：" + stu.getComputer());
    }
}
~~~

程序运行结果：

~~~
学生编号：MLDN-33
学生姓名：李兴华
数学成绩：95.0
英语成绩：89.0
计算机成绩：96.0
~~~





