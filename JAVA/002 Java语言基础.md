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



# 2 数据运算

##### 一元运算符

参与运算的数据只有一个：!

##### 二元运算符

参与运算的数据有两个

& | >> <<  + - * /  += -+ *=  /+

##### 三元运算符

参与运算的数据有三个

## 2.1 算数运算符

\+ - \* / % (取余)

+ 参与运算的数据与参与运算的数据类型相同（前提：参与运算的所有数据类型要相同,<font color='red'>**且buye和short的除外，byte + byte,byte+short,short+short的结果都是int**</font>）

int + int == int

long + long == long

... ...

+ 参与运算的类型不同，结果类型为参与运算的数据类型中，大范围的值的类型相同

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

## 2.2 char做算数运算

### 2.2.1 直接打印int类型为字符串的变量值

+ \+ 用的较多，符号和数字用的多

+ 若参加运算的类型的字符，则会用编码集进行运算

```java
public class Bools {
	public static void main (String[] args) {
		int e = '1';
		System.out.println(e);
}}
```

###### 执行结果

```
PS D:\JAVA> java Bools
49
```

+ 若参与运算的是一个变量，结果的类型默认是int

### 2.2.2 定义字符串类型变量

```
public class chars {
	public static void main (String[] args) {
	char a = 'L';
	System.out.println(a);
}
}
```

### 2.2.3 字符串的算数运算

编程常用数据类型：int，long，double

面试常问：short、byte，float、char

#### 2.2.3.1 运算的直接是字符

+ char类型的值对应ASCALL值，与数字相加，得到最终结果对应的值

```
public class chars {
	public static void main (String[] args) {
	char b = '0' + 10;
	System.out.println(b);
}
}
```

| ASCII值 | 控制字符 | ASCII值 | 控制字符 | 控制字符 | ASCII值 | 控制字符 |
| ------- | -------- | ------- | -------- | -------- | ------- | -------- |
| 16      | DLE      | 48      | 0        | P        | 112     | p        |
| 26      | SUB      | 58      | :        | Z        | 122     | z        |

###### 运行结果：

```powershell
PS D:\JAVA> java chars
:
```

#### 2.2.3.2 运算的是保存字符的变量

```java
public class chars {
	public static void main (String[] args) {
	char c = '0';
	int d = c + 1;
//不能用char类型接收，否则会提示类型不兼容
	System.out.print(d);
}
}
```

###### 运行结果：

```powershell
PS D:\JAVA> java chars
49
```

## 2.3 复合运算符

+ 若一个式子中，出现了算数运算符和符合运算符，<font color='red'>优先计算算数运算符。</font>算数运算符优先级大于复合运算符

```java
public class test {
	public static void main (String[] args) {
		int a = 10;
int e = 2;
		a *= e + 1;
		System.out.println(a);
}}
```

###### 运算结果：

```java
PS D:\JAVA> javac .\test.java
PS D:\JAVA> java test
30
```

## 2.4 数据运算

### 2.4.1 数字的符号

+、-可以表示数字的正负

### 2.4.2 结合变量

++、-- ，表示自增、自减，在当前变量的基础上+/-1，可以放在<font color='red'>变量前面</font>，或者<font color='red'>变量后面</font>

#### 2.4.2.1 在变量前面和后面的区别

+ <font color='red'>写在变量前面</font>，先用变量值，后加1

+ <font color='red'>写在变量后面</font>，先加1，后用变量值

```java
public class test {
	public static void main (String[] args) {
		byte a = 120 ;
		System.out.println(a++);
		System.out.println(a);
        System.out.println(a++);
}}
```

```powershell
PS D:\JAVA> java test
120
121
121
```

#### 2.4.2.2 赋值运算符：

= ： int a = 1 ;

将1赋值给int 类型的a 

+= 、-=、 *= 、/=

数字间的运算（关系运算），结果为bool类型

表示数字间关系

<、<=、>=、<=、==、!=

+ 关系运算符一次只能比较一个式子是否成立，若来连续比较需要使用逻辑运算符

#### 2.4.2.3 数据运算：

+ 使用数字运算符和字符运算符

若使用了符合运算符，进行运算，在自己本身的基础上进行的运算，<font color='red'>**数据类型不会发生变化**</font>

```java
public class test { 
	public static void main (String[] args) {
		int a = 10;
		a += a;
		System.out.println(a);
}}
```

## 2.5 关系运算

### 2.5.1 逻辑运算符

用来连接多个关系运算表达式（a + b a + b - 1 a * b a > b）

语句结束表示完成的一句话 赋值

### 2.5.2 表达式

短路与和短路或

#### 2.5.2.1 短路与运算：

当全部结果为true时，结果为true，否则为false

+ 前面的如执行失败，整个表达式是false，后面的不会执行

#### 2.5.2.2 短路或运算：

至少有一个表达式成立，结果为true，否则为false

+ 前面的如执行成功，整个表达式是true，后面的不会执行

### 2.5.3 全路与和全路或

+ & | 是全路运算符，无论前面表达式是否可以决定整个表达式结果，都继续执行后面语句

#### 2.5.3.1 全路与

+ 取决于参与运算的数据类型

#### 2.5.3.2 运算结果

运算结果取决于全路运算符

+ 若链接的是关系表达式，无论前面的表达式是否能决定整个表达式的结果，后边都执行、
+ 若连接的是数字，则对数字进行位运算

### 2.5.4 移位

<<：左移 ，左移一位，值变为原来的一倍

\>>：右移，右移一位，值变为原来的一半

```
public class test1 {
	public  static void main (String[] args) {
	int a = 5;
	System.out.println(a >> 1);
	System.out.println(a << 1);
}
}
```

### 2.5.5 三目运算符

格式：结果是boolean类型的表达式？

参与运算的结果取决于前两个值

判断前面的表达式是否成立，若成立表达式结果为值1，不成立则为值2

```java
public class test1 {
    public static void main (String[] args) {
        int a = 10;
        int b = 20;
        System.out.print(a>b?20:true);
        System.out.print(a<b?20:true);
    }
}
```

希望实现若前面的表达式成立，则执行前一部分 的代码，并把值赋给结果，否则执行第二部分的代码，赋给表达式的结果

流程控制语句

## 2.6 字符串类型

String ,值需要使用“”赋值

### 2.6.1 String与字符的拼接

+ 使用+ 是字符串拼接

```java
public class test1 {
	public  static void main (String[] args) {
	String b = "a" + "b";
	System.out.print(b);
}
}
```

###### 运行结果：

```
PS D:\JAVA> java test1
ab
```

## 2.7 分支语句

### 2.7.1 if

#### 2.7.1.1 一个条件

```java
if (条件 boolean类型) {
    若条件成立，执行{
        
    } 
}    
```

#### 2.7.1.2 两个条件

```java
if (条件 boolean类型) {
    若条件成立，执行{
        
    } else {
        代码
    }
}    
```

#### 2.7.1.3多个条件

```java
if (条件 boolean类型) {
    若条件成立，执行{
        
    } else if (条件) {
        代码
    } else {
    }
}    
```

### 2.7.2 swich case 

+ <font color='red'>case穿透：忘记写break会导致case一直向下执行，直到遇到break，或者switch</font>

  和 case 后的值比较

值只可以为byte，short，int，char，String

```java
switch (值) {
    case 值:
         代码
    break:
  }
```

+ case比default优先级高
+ default可以放在case前，但是还是会先执行case

```java
switch 变量a {
    case a == 1:
         代码
    break:
    //强制终止当前循环
    default:
    //若值都不相等，执行default代码
  }
```

# 3 循环

循环三要素:初始值、循环条件、更新初始值

## 3.1 for循环

### 3.1.1 循环格式

```java
for (初始值; 循环条件; 更新初始值)   {
	循环语句
	}
```

#### 3.1.2 for循环执行过程

初始化值--> 判断循环条件-->执行循环语句--->更新初始值

变量的作用域：定义变量的范围

### 3.2 while 循环

#### 3.2.1 循环格式

```java
while (循环条件) {
    执行的内容
    更新条件
}
```

## 3.3 do while循环

### 3.3.1 循环格式

```java
do {
    循环体
} while {
    循条件
```

### 3.3.2 do while 循环特点

+ 无论条件是否满足都会执行至少循环

## 3.4 中断循环

continue：跳过当前循环，进行下一次循环

break：结束循环

return：结束方法，执行后退出该方法，每个方法最后都会执行return

# 4 数据类型

## 4.1数组

### 4.1.1 定义数组

```java
int[] srr = {1,2,3,4,5};
数据类型 变量名 = 值
```

数组定义后无法修改数组长度

## 4.2 修改数组中某个元素的值

```java
arr[4] = 10;
```

## 4.3 查看数组的值

打印数组时，显示是内存地址，根据内存中的地址数组下标查找对应值

获取数组长度：数组名.length

查看所有的值：使用for循环打印

数组定义后数据不能添加

## 4.4 冒泡排序

判断第一个位置和第二个位置的值的大小，

```java
    public static void main(String[] args) {
        int[] sorts = {1, 20, 0, 80};
        for (int j = 0; j < sorts.length-1; j++) {
            for (int i = 0; i < sorts.length - 1; i++) {
                if (sorts[i] > sorts[i + 1]) {
                    int temp = sorts[i];
                    sorts[i] = sorts[i + 1];
                    sorts[i + 1] = temp;
                }
            }
        }

        for (int i = 0; i < sorts.length; i++) {
            System.out.println(sorts[i]);

        }

    }
}
```

