# 1 编程语言

## 1.1 高级语言

+  对于我们 容易理解（单词 ） 对于电脑 不认识 （0和1）

+ 如：JAVA、Go、Python

## 1.2 低级语言

+ 对于我们 不容易理解  电脑认识   
+ 如 ：汇编 机器

# 2 JDK与JRE

## 2.1 JDK

+ （**Java Development Kit**）*称为Java开发包或Java开发工具，

+ JDK是整个Java的核心，包括了Java运行环境*（**Java Runtime Environment**）*，一些

## 2.2 JRE

+ JRE 是支持Java程序运行的标准环境 。
+ JRE是运行环境，JDK是个开发环境。因此写Java程序的时候需要JDK，而运行Java程序的时候就需要JRE。而JDK里面已经包含了JRE，所以只要安装了JDK，就可以编辑Java程序，也可以正常运行Java程序。

## 2.3 JVM 

+ JVM是java虚拟机，用于运行javac编译后端二进制程序

## 3 **Java**语言特点

## 3.1 编译和解释性

### 3.1.1 编译性

+ 文件要执行，直接执行不了 （计算机不认识），需要进行编译，形成字节码文件  形成 计算机直接识别的文件 0和1 

+ 编译性语言 编译后 形成新的文件

### 3.1.2 解释性

+ 编译文件 计算机不认识
+ 中间解释器（解释） 字节码文件解释给计算机
+ 安装了jdk 就包含了jre 包含了解释器（jvm）

# 4 如何写java代码

+ 创建后缀名是.java的文件
+ 写java代码

```java
public class hello {
//public class 文件名
    //写代码内容，声明manin函数
public static void main(String[]  args){
    //java程序的入口地址,java虚拟机运行程序的时候首先找的就是main方法
		System.out.println("hello world");
}
}
```



# 5 执行java代码

## 5.1 编译

+ 通过java自己的编译方式进行文件编译 
  + javac  java文件名.java （新的文件 字节码文件  .class）

```powershell
PS D:\JAVA> javac hello.java
```



## 5.2解释执行

+ java文件名 

```
PS D:\JAVA> java hello
hello world
```

