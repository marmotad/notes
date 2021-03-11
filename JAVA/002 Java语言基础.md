# 1 常量、变量、数据类型

常量：值不能改变

常量：值可以改变

数据类型：变量值的类型，如整数、小数、字母... ...

## 1.1 基本数据类型

整数、小数

## 1.2 整数类型：

byte、short、int、long

不同的整数类型大小范围不同，占用的空间也不同


|类型|占用空间|位数 |数值范围|
|---|-------|----|-------|
|byte|1个字节 |8位|-128到127|
|short|2个字节	|16位|-32768 到 32767|
|int |4字节|32位|-2147483648到2147483647|
|log|8字节|64位|-9223372036854775808到9223372036854775807|

### 1.2.1 long类型

定义时long类型时和其他类型不同，定义时需要和int类型区分，long类型的值后需要使用l或者L的后缀做标识（建议使用L）

```java
public class long_test {
	public static void main (String[] args) {
	long a = 2888888888888888L;
	System.out.println(a);

}
}
```

### 1.2.2 数字符号

写在变量值的前面

## 1.3 小数

### 1.3.1 float

+ float占4个字节,只保留四位小数，超过后会四舍五入

+ 定义float数据类型时，需要声明类型是float（添加f或F后缀），否则默认是double类型
  + 若float类型的变量有小数点时需要添加f/F的后缀
  + 若float类型的变量没有小数点时可以不添加f/F的后缀
  + 当数值过大时，会自动使用科学计数法表示

```java
public class float_test {
	public static void main (String[] args) {
	float a = 288.8881f;
	//当存储的小数位大于4位时，后面的位
	System.out.println(a);

}
}
```

### 1.3.2 double

+ 通过float和double表示小数类型

+ double占八位，表示双精度，可表示15-16位小数

### 1.5 字符类

ASCII码表

每个国家都有自己的编码集，表示自己的编码（我国GBK2312）

Unicode 所有编码集（占用空间较大）  

Utf-8 ----编码集

#### 1.5.1 定义字符串类型变量

```
public class chars {
	public static void main (String[] args) {
	char a = 'L';
	System.out.println(a);
}
}
```



### 1.6 bool值

#### 1.6.1 定义bool类型变量

boolean = true/false

变量命名规范

1、变量名只能由数字、字母、下划线及$符组成

2、不能以数字开头

3、不能以Java中关键字开头

4、尽量见名知意

5、建议使用驼峰命名法

### 1.7 变量定义

```
byte a = 1;
//变量类型 变量名 = 变量值
```

### 1.8 程序的执行顺序

+ 从上到下依次执行
+  变量没有零值，且定义后不一定要引用

```java
public class test {
	public static void main (String[] args) {
	byte a,b;
	a = 1;
	b = 1;
	System.out.println(a);
}
}
```

### 1.9 数据类型转换

#### 1.9.1 小范围数据转大范围的数据

<font color='red'>**小范围转大范围直接转换**</font>

```java
public class SmallToMax {
	public static void main (String[] args) {
	byte a = 20;
	long b = a;
	System.out.println(b);
}
}
```

#### 1.9.2 大范围数据转下范围的数据

<font color='red'>**大范围转小范围需要强制转换**</font>

```java
public class MaxToSmall {
	public static void main (String[] args) {
	long a = 20L;
	byte b = (byte)a;
	System.out.println(b);
}
}
```



## 2、数据运算

### 2.1 算数运算符

\+ - \* / % (取余)

参与运算的数据与参与运算的数据类型相同（前提：参与运算的所有数据类型要相同）

int + int == int

long + long == long

... ...

参与运算的类型不同，结果类型为参与运算的数据类型中，大范围的值的类型相同

long + byte == long

short ，byte，char在做运算的时候会转成int，运算时需要强制转换类型

```java
public class homework {
    	public static void main (String[] args) {
		short e = 128;
		System.out.println(e / 100);
		short f = (short)(e%100);
//强制转换数据类型
		System.out.println(f / 10);
}
}
```





char做算数运算

+ \+ 用的较多，符号和数字用的多

+ 若参加运算的类型的字符，则会用编码集进行运算

```java
public class Bools {
	public static void main (String[] args) {
		int e = '1';
		System.out.println(e);
}}
```

执行结果

```
PS D:\JAVA> java Bools
49
```

+ 若参与运算的是一个变量，结果的类型默认是int

编程常用数据类型：int，long，double

面试常问：short、byte，float、char

赋值运算符：

= ： int a = 1 ;

将1赋值给int 类型的a 



数据运算：

+ 使用数字运算符和字符运算符

复合运算符

+= 、-=、 *= 、/=

若一个式子中，出现了算数运算符和符合运算符，优先计算算数运算符。算数运算符优先级大于复合运算符

```java
public class test {
	public static void main (String[] args) {
		int a = 10;
int e = 2;
		a *= e + 1;
		System.out.println(a);
}}
```

运算结果：

```java
PS D:\JAVA> javac .\test.java
PS D:\JAVA> java test
30
```



若使用了符合运算符，进行运算，在自己本时的基础上进行的运算，<font color='red'>**数据类型不会发生变化**</font>

```java
public class test {
	public static void main (String[] args) {
		int a = 10;
		a += a;
		System.out.println(a);
}}
```



### 数据范围

数字符合

+、-可以表示数字的正负

结合变量

++、-- ，表示自增、自减，在当前变量的基础上+/-1，可以放在<font color='red'>变量前面</font>，或者<font color='red'>变量后面</font>

在变量前面和后面的区别

在变量前面，先用变量值，后加1

在变量后面，先加1，后用变量值

```java
public class test {
	public static void main (String[] args) {
		byte a = 120 ;
		System.out.println(a++);
		System.out.println(a);
}}
```

```powershell
PS D:\JAVA> java test
120
121
```



数字间的运算（关系运算），结果为bol类型

表示数字间关系

<、<=、>=、<=、==、!=

+ 关系运算符一次只能比较一个式子是否成立，若来连续比较需要使用逻辑运算符

逻辑运算符

用来连接多个关系运算表达式（a + b a + b - 1 a * b a > b）

语句结束表示完成的一句话 赋值

#### 表达式

短路与运算：当全部结果为true时，结果为true，否则为false

+ 前面的如执行失败，整个表达式是false，后面的不会执行

短路或运算：

至少有一个表达式成立，结果为true，否则为false

+ 前面的如执行成功，整个表达式是true，后面的不会执行