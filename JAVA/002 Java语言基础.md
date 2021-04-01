# 1 常量、变量、数据类型

常量：值不能改变

变量：值可以改变

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

### 3.1.3 提取i作用范围

```java
int i = 0;
for (; i < 2; i++) {}
```



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

# 4 引用数据类型

## 4.1数组

### 4.1.1 定义数组并对数组赋值

```java
int[] srr = {1,2,3,4,5};
数据类型 变量名 = 值
```

数组定义后无法修改数组长度

### 4.1.2 定义空数组

```java
int[] srr = new int[数组长度];
#整数类型数组默认值为0
#flot double默认值为0.0
#char默认为空（不是空格）
#boollean默认为false
```

4.1.3 

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

# 5 方法

+ 方法公开化（用public修饰，代表类外面可调用）

## 5.1 方法的格式

+ 具有某种功能的代码，例如main具有程序入口方法的功能

```
public static void 方法名(数据类型 变量名)   ----- 方法的声明
							^形参
{方法中具有某种功能的代码----方法体} ====== 方法体
```

+ 方法写在class文件中
+ 不能在一个方法中再写一个方法

## 5.2 方法分类

### 5.2.1 是否有参数

+ 有参数

+ 无参数

### 5.2.2 是否有返回值

+ 有返回值（必须使用完成后，使用return返回对应类型值）
+ 无返回值（方法名前是void的方法没有返回值）

```java
	//定义无参带返回值的方法
	public int classSum() {
		int a = 2;
		int b = 55;
		int sum = a + b;
		return sum;
				
	}
```

### 5.2.3 有返回值的方法调用

+ 调用时，方法给了我们数据值，在调用时，可以使用对应的变量接收

如果需要得到方法中的数据，继续做其他操作，该方法需定义成有返回值的方法

## 5.3 定义方法

+ 方法用

```java
    private static void sorts(int[] sorts) {
        //int[] sorts = {34,21,8,49};
        for (int j = 0; j < sorts.length-1; j++) {
            for (int i = 0; i < sorts.length - 1 - j; i++) {
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
<<<<<<< HEAD
```

## 5.3 调用自定义方法

+ jvm调用main方法，main方法调用自己写的代码

方法调用时，观察调用的方法是不是又形参，如果有，形参是什么数据，

```
 public static void main(String[] args) {
        int [] sorts1 = {20,10,0,39};
        int [] sorts2 = {20,10,0,39};
        sorts(sorts1);
        //引用方法时，要注意是否有形参，有的话需要对形参赋值，若有多个形参时，用“，”隔开
    }
```

# 6 二分查找

## 6.1 二分查找



## 6.2 统一输出

在查找时，进行查找数据值的返回，若查找到数据就返回查找到数据的下标，否则返回一个-1

```java
public class find {
    public static void find(int[] arr, int findNum) {
        int start = 0;
        int end = arr.length - 1;
        while (start <= end) {
            //start : 开始查找的数组的最小索引；end：数组结束的索引；half：数组为查找的元素的中间索引
            int half = (start + end) / 2;
            if (findNum == arr[half]) {
                //如果数组中间索引对应的数自是要查找的数字，则查找到值，并返回
                System.out.println(arr[half]);
                return;
            } else if (findNum > arr[half]) {
                //如果查找的数字比数组中间索引的值大，则中间的索引加1
                start = half + 1;
            } else if (findNum < arr[half]) {
                end = half - 1;
                //如果查找的数字比数组中间索引的值小，则结开始的索引减1
            }
        }
        //return -1;
    }


    public static void main(String[] args) {
        int[] arrs = {89,91,97,456};
        find(arrs, 456);
    }
}
```

# 7 类

+ 类中封装了某个方法具体的实现
+ 使用时 通过对象 只是使用了方法 做了方法的调用，此时我们看不到方法的具体实现是什么

## 7.1 JAVA存储数据流程

+ 创建.java的文件

### 7.2 声明类

+ 类是一个数据类型

+ 变量是java存储的数据的特征

```
public class 文件名 {
	String name;
	byte age;
	String type;
}
```

### 7.3 基于类创建数据

```
new 类名() ;
数据类型 变量名 = 值;

```

### 7.4 对象

+ 对象是类的一个实例
+ 对象在创建时要符合Java的创建语法，与数组相似

```
Cat c = new Cat();
```

### 7.5 赋值和取值

### 7.5.1赋值

+ 在对应的特征的位置上进行数据的输入 

```
name age type
c.name = "sss"
c.age = 1;
c.type = "dddd"
```

### 7.5.2 取值

```
System.out.print(c.name)
```

## 7.6 类的分类

1、含有main方法的类：测试类

2、描述类的特征：特征类

### 7.6.1 给特征赋值

+ 创建后会有默认值，与数组默认值相同

```
public class age {
    int a,age ;
    public void setA(int a){
        if (a > 0) {
            age = a;
        } else {
            age = 1;
        }
    }
}
```

### 7.6.2引用特征类的方法

```java
public class test {
    public static void main(String[] arga) {
        age a = new age();
        a.setA(-1);
        System.out.println(a.age);
    }
}
```

### 7.6.3属性私有化

+ 禁止在测试类中使用.变量名的方式赋值

+ 一个类中写的数据，只能在当前类中使用，出了类不能用

+ private是java中表示私有的一个修饰符，若设置了private，不能在特征类引用，不能在测试类中调用

+ 若要获取特征上的值使用需要设置get方法

```java
public class age {
    private int a,age ;
    public void setA(int a){
        if (a > 0) {
            age = a;
        } else {
            age = 0;
        }
    }
    //在类中获取值,并返回
    public int getA() {
           return age;
    }
}
```

### 7.6.4 获取值的方法

```java
public class test {
    public static void main(String[] arga) {
        age b = new age();
        b.setA(-1);
        System.out.println(b.getA());
    }
}
```

### 7.6.5 类中变量的作用域

如果在当前类中都能生效的变量叫全局变量

如果在方法中定义的变量叫局部变量

若局部变量和全局变量重名，遵循就近原则

### 7.6.7 属性和局部变量区分

this代表当前对象，不是固定的，取决于谁调用了方法

### 7.6.8 给当前对象赋值

```java
public class age {
    private int age ;
    public void setA(int age){
        if (this.age > 0) {
            this.age = age;
        } else {
            this.age = 0;
        }
```

### 7.6.8拼接

+ 类中定义一个方法去调用方法打印
+ 如果在一个类中没有写toSting的方法，打印的是地址，如果写了toString的方法，打印的是返回值

+ 使用toString方法调用

```Java
//打印对象时，默认调用
public String toString() {
        return "年龄" + age;
    }
```

###  7.7 构造对象

在Java中创建了一个类，在类中，存在一个默认的方法，方法名为 类名+（）

只能放在new后进行对象创建，new后也不可以放其他的

类名前不能加返回值类型，否则就不是方法了

### 7.7.1 构造方法

#### 7.7.1.1 默认构造方法：

+ 一个类中只能有一个构造方法，若手动定义了构造方法，默认的会失效

```Java
public 类名() {
	  ^ 不能加返回值类型，否则就不是方法了
//方法体
}
```

#### 7.7.1.2 创建对象并对属性赋值

##### 7.7.1.2.1 在类中定义方法

```java
    public Student () {

    }
//定义无参的方法
    public Student (String name, byte score, short num) {
        this.name = name;
        this.score = score;
        this.num = num;
    }
//定义有参的方法
```

##### 7.7.1.2.2 方法重载

+ 在同一个类中定义多个方法，方法名相同，但是参数列表不同
+ 方法重载只要符合重载的条件就是方法重载，可以是普通的方法，也可以是构造方法
+ 可以根据传入的参数自动的选择要使用现有的方法，还会自动进行大范围的数据转换

> 1、参数个数不同
>
> 2、参数类型不同
>
> 3、类型顺序不同

### 7.7.2 构造方法间调用

#### 7.7.2.1 普通方法间的调用

```java
    public void a () {
        System.out.println("a的无参方法");
        a(2);
    }

    public void a(int a) {
        System.out.println("a的有参方法");

    }
```

#### 7.7.2.2 构造方法间的调用

+ 通过this进行构造方法间的调用
+ this必须放在构造方法里，且必须是构造方法体第一句
+ this可以自己调自己，但是必须加条件，否则会溢出、
+ 构造方法可以调用普通方法，但普通方法不能调用构造方法
+ 多个参数的构造方法可以调用少个参数的构造方法，在多个参数里书写逻辑
+ 少参数的构造方法可以调用多参数的构造方法

```java
    public Student (String name, byte score, short num) {
        this();//调用当前类中的构造方法
    }
```

## 7.8 继承

### 7.8.1 继承

+ 继承发生在类和类之间
+ 通过extens指定父类。若没有指定父类，默认继承Object
+ 父类

```java
package git.cncf.online.day10;

public class publicClass {
    protected String name;
    protected byte age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

+ 子类

```java
public class Student extends publicClass {
    //子类中的代码
}
```

### 7.8.2 super

#### 7.8.2.1 super 关键字

+ 就近原则

> 调用方法时，先在自己的类中找需要执行的方法，找不到去父类中查找
>
> 实际执行时，先加载父类，再加载子类，子类是父类的扩展

+ 如果在子类中调用和父类中同名的方法 ，需要使用super去调用父类中的方法
+ 如果子类中没有这个方法，底数父类中有，可用省略super

#### 7.8.2.2 super()

+ 用于调用父类中的构造方法
+ super必须放在构造方法体的第一句
+ super无法和this同时存在

```java
public Student (String name, byte score, short num) {
	super();
}

public xxx() {
    super();
}
```

#### 7.8.2.2 父类和子类

+ 拥有的共同特征，父类表示的数据范围大
+ 子类是在父类基础上的扩展，做了具体类型的指定

#### 7.8.2.3 范围转换

+ 父类的范围比子类的范围大

##### 7.8.2.3.1 向上转型（隐藏子类中扩展的功能）

+ 子类转父类（直接转换）
+  向上转型后<font color="red">子类的特征依然存在，但是父类不能调用</font>
+ 子类扩展的特征对父类来说是隐藏的

```java
Cat cat = new();
Animal animal = cat;
//或者
Animal animal = new cat();
```

##### 7.8.2.3.2 向上转型的应用

###### 7.8.2.3.2.1 赋值的向上转型

+ 逻辑相同但参数不同的代码多次出现，参数都是同一个父类

```java
方法 (父类类型 变量名名) {
}
```

###### 7.8.2.3.2.2 传参的向上转型

+ 通过传参的方式，用父类接受子类对

```
package git.cncf.online.day11;

import git.cncf.online.day11.homewark.Animal;

public class test11 {
    public static void main(String[] args) {
        b(new Cat("tom",88,"白色"));
        b(new dog("来福",55,"白色")); 
        }

    private static void b(Animal cat) {
        System.out.println("================");
        System.out.println(cat);
        System.out.println("================");

    }
}
```



##### 7.8.2.3.3 动态绑定

+ 程序运行时，识别变量中存放的数据的实际类型，找到实际类型中的方法做方法调用

![image-20210321212442507](002 Java语言基础.assets/image-20210321212442507.png)

##### 7.8.2.3.4 方法重写

+ @override会标识方法重写

+ 类是具有相同特征和行为的一类事物 

+ 子类和父类拥有相同的方法，但方法体不同

+ 子类<font color="red">继承父类，参数列表相同，返回值相同</font>访问权限修饰符不同，<font color="red">称为方法重写</font>
+ 向上转型后，方法调用时，会进行动态绑定，都是子类特征中符合自己的特征行为，而不会执行父类的方法体（父类的方法体多余，执行不到）
+ 子类必须手动写方法才能实现重写（使用抽象方法提示子类需要方法重写）

```java
####cat
package git.cncf.online.day11;

public class Cat extends Animal {
        private String type ;
        public void run(){
                System.out.println("cat可以跑");
        }
}

####dog
import git.cncf.online.day11.Animal;

public class dog extends Animal {
    private String type ;
    public void run(){
        System.out.println("dog跑的很快");;
    }
}

####animal
package git.cncf.online.day11;

public class Animal {
    private String name;
    private int age;

    public Animal () {
    }

    public Animal (String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void run(){
        System.out.println("动物可以跑");
    }

}

####test


package git.cncf.online.day11;

public class test11 {
    public static void main(String[] args) {
        b(new Cat());
        b(new dog());
    }

    private static void b(Animal animal) {
        System.out.println("================");
        animal.run();
        System.out.println("================");

    }
}
```

###### 运行结果

```powershell
================
cat可以跑
================
================
dog跑的很快
================
```

##### 7.8.2.3.5 向下转型

ClassCatException类型转换的异常

+ 做向下转型前必须先做向上转型

```java
Animal a = new Cat();
Cat c = (cat) a;
c.a();
```



instanceof 

对象 instanceof 数据类型

判断前面的对象是否是后面的数据类型，如果是返回ture，不是返回false

```java
Animal animal = a (-1);
if (animal instanceof Cat) {
    Cat c = (Cat) animal;
    System.out.println(c);
    c.run();
} else {
    Dog d = (Dog) animal;
    System.out.print(d);
    d.run();
}
```



#### 7.8.2.4 抽象方法

+ 只有方法声明没有方法体
+ 需要使用abstract修饰
+ <font color="red">抽象方法必须在抽象类中</font>，但是抽象类中不影响有抽象方法
+ 通过子类对父类进行标识

```java
# 父类定义抽象方法
package git.cncf.online.day11;

public abstract class Animal {
    private String name;
    private int age;

    public Animal () {
    }

    public abstract void run();
}

# 子类中创建抽象方法
package git.cncf.online.day11;

public class Cat extends Animal {
        private String type ;
        @Override
        public void run(){
                System.out.println("cat可以跑");
        }
}
```

#### 7.8.2.5 访问权限修饰符

+ 设定变量的有效作用范围
+ <font color="red">子类的权限要大于等于父类的权限</font>

|            | 不同的包 | 不同包下的子类 | 相同的包 | 当前类 |
| ---------- | -------- | -------------- | -------- | ------ |
| public     | 可以     | 可以           | 可以     | 可以   |
| protected  | 不可以   | 可以           | 可以     | 可以   |
| 默认修饰符 | 不可以   | 不可以         | 可以     | 可以   |
| private    | 不可以   | 不可以         | 不可以   | 可以   |

实现

implements

类实现另一个类中的抽象方法

子类继承了抽象类，实现逻辑

## 8 接口类型

+ 接口注重的是方法

## 8.1接口定义

+ 接口中的方法，默认是抽象方法，默认使用public abstract修饰

```java
public interface 接口名 {
    void per ();
    //接口名
}
```

+ 接口中都是抽象方法，通过类进行具体实现

## 8.2 接口的实现

+ 类（实现类）实现接口（父接口）

+ 一个类可以实现多个接口

+ 接口和接口间是多继承的关系

```java
pbulic class 类名 implements 接口名 () {
    public void 
}
```



|      | 类       | 接口       |
| ---- | -------- | ---------- |
| 类   | 单根继承 | 类实现接口 |
| 接口 | 多实现   | 多继承     |

## 8.3 方法体

+ JDK1、8 以上可以在接口中定义方法体，但是需要使用default修饰

```java
public interface A {
    public static void a(){

    };
    public default void a(int a){

    }
}
```

## 8.4 接口和抽象类

### 8.4.1 相同点

+ 都有常量和抽象方法
+ jdk1.8后都可以定义普通方法
+ 都可以使用匿名内部类完成功能

### 8.4.2 不同点

+ jdk1.8 前不可以在接口中定义普通方法
+ 类和类单根继承
+ 类和接口 多实现
+ 类中有属性和方法、构造方法、set/get方法、toString、代码块，接口中没有
+ 接口可以通过lambda表达式实现

```java
package git.cncf.online.day13;

public interface shape1 {
    void a();
}




package git.cncf.online.day13;

public class test {
    public static void mian(String[] args) {
        new shape1() {

            @Override
            public void a() {
                
            }
        };
    }
}
```



# 9 static 和final

+ 加载类-->创建对象-->分配内存-->使用

static 优先加载，被static修饰的内容会被优先加载

static会优先分配内存，随着类的加载就进行了内存的分配

当在main方法中，通过变量指向了对象的地址，对象分配好了内存空间，就可以使用了

只有一个对象分片好了内存空间，才可以进行使用

static修饰的内容需要通过类进行调用，通过类调用的方法称为类方法，变量称为类变量

如果调用的是本类的方法，类可以省略，调用的是其他类中的方法，类不可以省略

![image-20210321165613836](002 Java语言基础.assets/image-20210321165613836.png)



## 9.1 static 可以修饰的内容

static可以修饰全局变量

static不可以修饰局部变量

构造方法

getset方法

抽象方法

自己定义的方法

static修饰的方法不可以被重写



类只能调用static的方法

对象可以调用static方法和普通方法

static {} static可以修饰代码块   静态代码块，随着类加载而执行，只会执行一次

## 9.2 静态代码块

+ 先加载父类代码块---->子类静态代码块------>父类的构造代码块------>父类的构造方法------->子类的构造代码块-------->子类的构造方法 

```java
ststic {
    
}
```



## 9.3 构造代码块

+ 在构造方法前执行的代码块叫构造代码块

```
{}
//随构造方法的执行而执行
```

## 9.4 final

final可以修饰类，<font color="red">但final修饰的类不能被继承</font>

final不可以修饰抽象类

final可以修饰局部变量，也可以修饰get/set方法，但不这么用

final不可以修饰抽象方法

final可以修饰普通方法，但是<font color="red">final修饰的方法不能被重写</font>

+ final可以修饰全局变量，但必须赋值

```java
final int a = 10;
```

+ final修饰的变量是只读的普通变量

+ 在使用final修饰的变量前对final修饰的变量赋值就不会影响使用
+ 构造代码块中进行赋值

## 9.5 static final 修饰

+ 用大写字母表示

+ 优先加载的一个不能变的值
+ static final 修饰基本数据类型 当前这个变量的值不能变
+ static final 修饰引用数据类型 地址不能变（值不能变），但是可以对其中值的内容重新赋值

```java 
static final int A = 10;
//static修饰的基本数据类型代表当前修饰的变量值不能变
static final int[] = A{};
A[1 = 10;
```

# 10 单例

+ 一个类只有一个对象
  + 优点：节省内存空间

## 10.1 单例的实现

a. 不能随便的调用构造方法进行对象创建

限制对象的创建，不要在测试类中随便创建，出了类不能使用

b. static修饰的方法可以通过类进行调用，提供对象

c. 不能随便创建，一个类只能有一个，不能在static方法中创建

### 10.1.1 饿汉模式

+ 无论是否调用方法

```java
package git.cncf.online.day14;

public class cat2 {
    private String name;
    private byte age;
    private String type;
    private static cat2 cat = new cat2();

    public static cat2 getInstance() {
        return cat;
    }
}
```

### 10.1.2 懒汉模式

```java
package git.cncf.online.day14;

public class cat2 {
    private String name;
    private byte age;
    private String type;
    private static cat2 cat;
    
public static cat2 getInstance() {
        if (cat == null) {
            cat = new cat2();
        }
        return cat;
    }
}
```

# 11 String

## 11.1 构造方法赋值

```java
public class teststring {
    public static void main(String[] args) {
        //字符串创建对象的方式  1 构造方法赋值-----------存在于堆中
//        空的字符串
        String str = new String();
        System.out.println(str);
//        字符串的构造方法
        String str1 = new String("fdjfkd");
        System.out.println(str1);
    }
}    
```

###### 运行结果

```java

fdjfkd
```

## 11.2 类型转换

### 11.2.1 字符数组转成字符串

```java
        char[] chs = {'2','f','c'};
//        字符数组转成字符串
        String str2 = new String(chs);
        System.out.println(str2);
        System.out.println(new String(chs,1,2));
```

###### 运行结果

```java
2fc
fc
```

### 11.2.2 byte数组转字符串

```java
//  byte数组转字符串
        byte[] bytes = new byte[10];
        for (int i = 0; i < bytes.length; i++) {
            bytes[i]=(byte)(i+97);
        }
        System.out.println(new String(bytes));
//        调用的方法加了删除线 方法不推荐使用
        System.out.println(new String(bytes,2,5));
```

###### 运行结果

```java
abcdefghij
cdefg
```

### 11.2.3 获取指定索引位置上的数据

```
        String s = "++++http:/  /abcdefa.txt+++";
//        调用方法 查看方法功能
//        可以获取指定索引位置上的数据
        char a = s.charAt(0);
        System.out.println(a);
```

###### 运行结果

```powershell
+
```

### 11.2.4 字符串长度

```java
        String s = "++++http:/  /abcdefa.txt+++";
//        调用方法 查看方法功能
//        可以获取指定索引位置上的数据
        char a = s.charAt(0);
//        获取字符串长度
        System.out.println(s.charAt(s.length()-1));
```

###### 运行结果

```powershell
+
+
```

### 11.2.5 获取数字对应的字符索引

#### 11.2.5.1 从左往右查找

```java
//        找到了 就返回索引位置  没找到 返回-1
        System.out.println(s.indexOf(98));
        System.out.println(s.indexOf(98,2));
        System.out.println(s.indexOf("ab"));
        System.out.println(s.indexOf("b",2));
```

###### 运行结果

```powershell
14
14
13
14
```

11.2.5.1 从右往左查找

```java
//   从后向前找
        System.out.println(s.lastIndexOf("a"));
        System.out.println(s.lastIndexOf("a",5));
        System.out.println(s.lastIndexOf(98));
        System.out.println(s.lastIndexOf(98,5));
```

###### 运行结果

```powershell
19
-1
14
-1
```

#### 11.2.5.2 从指定开始位置取到结尾

```java
        System.out.println(s.substring(4));
```

###### 运行结果

```powershell
http:/  /abcdefa.txt+++
```

#### 11.2.5.3 从指定开始位置取到指定位置

```java
        System.out.println(s.substring(4,6));
```

###### 运行结果

```
ht
```

#### 11.2.5.4 获取后缀

```java
        System.out.println(s.substring(s.indexOf(".")+1));
```

###### 运行结果

```powershell
txt+++
```

#### 11.2.5.5 判断文件后缀

```java
        System.out.println(s.endsWith("txt"));
```

###### 运行结果

```powershell
false
```

#### 11.2.5.6 判断文件前缀

```java
        System.out.println(s.startsWith("http://"));
```

###### 运行结果

```
false
```

#### 11.2.5.7 大小写转换

```java
        System.out.println(s.toLowerCase());
        System.out.println(s.toUpperCase());
```

###### 运行结果

```
++++http:/  /abcdefa.txt+++
++++HTTP:/  /ABCDEFA.TXT+++
```

#### 11.2.5.8 判断字符串是否为空

```java
        System.out.println(s.isEmpty());
```

###### 运行结果

```java
false
```

#### 11.2.5.9 去掉字符串前后空白

```java
        System.out.println(s.trim());
```

###### 运行结果

```
++++http:/  /abcdefa.txt+++
```

#### 11.2.5.10 字符串转byte数组

```java
        System.out.println(s.getBytes());
```

###### 运行结果

```
[B@1b6d3586
```

#### 11.2.5.11 字符串转char数组

```java
        System.out.println(s.toCharArray());
```

###### 运行结果

```
++++http:/  /abcdefa.txt+++    
```

#### 11.2.5.12 替换指定字符

```
        System.out.println(s.replace('a','X'));
```

###### 运行结果

```
++++http:/  /XbcdefX.txt+++  
```

#### 11.2.5.13 指定规则拆分字符串

```java
String[] strs = s.split("a",2);
for (String s1:strs
) {
    System.out.println(s1);
}
```

###### 运行结果

```
++++http:/  /
bcdefa.txt+++  
```

#### 11.2.5.14 替换所有指定字符串

```java
        System.out.println(s.replaceAll("a","QQ"));
```

###### 运行结果

```
++++http:/  /QQbcdefQQ.txt+++  java
```

#### 11.2.5.14 替换结尾的指定字符串

```java
System.out.println(s.replaceFirst("a","QQ"));
```

###### 运行结果

```
++++http:/  /QQbcdefa.txt+++  
```

