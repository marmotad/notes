# 1 函数

## 1.2 函数分类

## 1.2.1 函数定义

```
函数名
函数体（函数内容）
参数
返回值
```

函数签名：函数的参数，参数的数量数量，以及参数对应类型称之为函数的签名

## 1.2.2 无参数无返回值函数

```go
package main
 
import "fmt"
 
//定义函数
 
func syshello() {
    fmt.Print("Hello Word")
}
 
//使用函数
func main() {
    fmt.Printf("%T\n", syshello)
    syshello()
}
```

###### 执行结果：

```
func()
Hello Word
```

### 1.2.3 有参数无返回值函数

```go
package main
 
import "fmt"
 
//有参数无返回值
func sysHI(name string) {
    //     ^ name是形参
    fmt.Println("你好", name)
}
 
func main() {
    sysHI("KK") //KK 是实参
}
```

###### 执行结果

```
你好 KK
```

## 1.2.4 有参数有返回值

```go
package main
 
import "fmt"
 
//有参数有回值
func add(a int, b int) int {
    return a + b
}
 
func main() {
    c := add(6, 9)
    fmt.Println(c)
}
```

###### 执行结果

```
15
```

## 1.3 函数参数类型合并

```go
package main
 
import "fmt"
 
//有参数有回值
func add(a , b int) int {
    return a + b
}
 
func main() {
    fmt.Println(add(9, 11))
}
```

###### 执行结果

```
20
```
## 1.5 可变参数

### 1.5.1 定义可变参数

```go
package main
 
import (
    "fmt"
)
 
//可变参数
func num(a , b int , numbers ...int) (int) {
    fmt.Println(a, b, numbers)
    fmt.Printf( "%T\n", numbers)
    return 0
}
 
 
func main() {
    fmt.Println( num(1, 3) )
    fmt.Println( num(1, 3, 5) )
    fmt.Println( num(1, 3, 5, 7) )
}
```

###### 执行结果

```
1 3 []
[]int
0
1 3 [5]
[]int
0
1 3 [5 7]
[]int
0
```

### 1.5.2 计算可变参数的和

```go
package main
 
import (
    "fmt"
)
 
//可变参数
func num(a , b int , numbers ...int) (int) {
    //                ^ 可变参数必须放在函数最后一个参数
    sum := a + b
    for _,v := range numbers {
        sum += v
    }
    //fmt.Println( a + b + sum)
    return sum
 
}
 
func main() {
    fmt.Println( num(1, 3) )
    fmt.Println( num(1, 3, 5) )
    fmt.Println( num(1, 3, 5, 7) )
}
```

###### 执行结果

```
4
9
16
```

### 1.5.3 将可变参数传递给留一个函数

```
package main
 
import (
    "fmt"
)
 
//可变参数
func num(a , b int , numbers ...int) (int) {
    sum := a + b
    for _,v := range numbers {
        sum += v
    }
    //fmt.Println( a + b + sum)
    return sum
}
 
func clus(op string, a, b int , args ...int ) int {
    switch op {
    case "add" :
         return num(a, b, args... )
    }
    return -1
}
 
 
func main() {
    fmt.Println( clus("add", 1, 3))
    fmt.Println( clus("add", 1, 3, 5))
    fmt.Println( clus("add", 1, 3, 5, 7))
}
```

###### 执行结果

```
4
9
16
```

### 1.6 函数多个返回值

### 1.6.1 显示返回值

```go
package main
 
import (
    "fmt"
)
 
func sum(a, b int) (int, int, int, int) {
    return a + b, a - b, a * b, a / b
}
 
func main() {
    fmt.Println(sum(1, 4))
}
```

###### 执行结果

```
5 -3 4 0
```

### 1.6.2 命名返回值

```go
package main
 
import (
    "fmt"
)
 
func sum(a, b int) (sum, diff,  product, quotient int) {
    sum, diff,  product, quotient = a + b , a - b, a * b , a / b
    return
}
 
func main() {
    fmt.Println(sum(8 , 4))
}
```

###### 执行结果

```
12 4 32 2
```

# 2 递归

## 2.1 求和

```go
package main
 
import "fmt"
 
func addN(n int) int {
        if n == 1 {
            return 1
        }
        return n + addN(n-1)
}
 
func main() {
    fmt.Println(addNt(100))
}
```

###### 执行结果

```
5050
```

## 2.2 求商

```go
package main
 
import "fmt"
 
func product(n int) int {
    if n == 1 {
        return 1
    } else if n < 0 {
        return -1
    }
        return  n * product(n - 1)
}
 
func main() {
    fmt.Println(product(10))
}
```

###### 执行结果

```
3628800
```

## 2.3 函数类型

函数赋值给变量

```
package main
 
import "fmt"
 
func add1(a, b int) int {
    return a + b
}
 
func main()  {
    fmt.Printf("%T\n",add1)
 
    f := add1
    fmt.Printf("%T\n",f)
 
    fmt.Println(f(1, 5))
}
```

###### 执行结果

```
func(int, int) int
func(int, int) int
6
```

## 2.4 函数传递给函数

+ 通过函数定义形参的函数类型，并通过函数将形参和实参传递到函数内部

```go
package main
 
import "fmt"
 
//callback  格式化  将传递的数据按照每行打印还是按照一行按|分割打印
func print(callback func(...string), args ...string){
    fmt.Println("print函数输出：")
    callback(args...)
}
 
func lit(arggs ...string) {
    for i,v := range  arggs {
        fmt.Println(i, ":", v)
    }
}
 
func main()  {
    print(lit, "A", "B", "C")
}
 
```

###### 执行结果

```
print函数输出：
0 : A
1 : B
2 : C
```

## 2.5 匿名函数

### 2.5.1 定义变量方式声明匿名函数

```go
package main
 
import "fmt"
 
func main()  {
    syaHello := func(name string) {
        fmt.Println("Hello ", name)
    }
    syaHello("kk")
}
```

###### 执行结果

```
Hello  kk
```

### 2.5.2 直接定义匿名函数并直接调用

```go
package main
 
import "fmt"
 
func main()  {
 
    func(name string) {
        fmt.Println("Hi ", name)
    }("AA")
}
```

###### 执行结果

```
Hi  AA
```

# 3 值类型和引用类型

+ 值类型：将变量赋值给新的一个变量，并修改新的变量的值，若对旧变量无影响为：值类型

+ 引用类型：将变量赋值给新的一个变量，并修改新的变量的值，若对旧变量有影响为：引用类型

+ 值类型的特点是：变量直接存储值，内存通常在栈中分配

+ 引用类型的特点是：变量存储的是一个地址，这个地址对应的空间里才是真正存储的值，内存通常在堆中分配

>值类型： int bool float array 指针
>引用类型： slice map

 

```go
package main
 
import (
    "fmt"
)
 
func main() {
    /*
    值类型    引用类型
    将变量赋值给新的一个变量，并修改新的变量的值，若对旧变量有影响为：引用类型，无影响为：值类型
    */
    array := [3]string{"A", "B", "C"}
    slice := [3]string{"A", "B", "C"}
 
    arrayA := array
    sliceA := slice
 
    arrayA[0] = "Z"
    sliceA[0] = "Z"
    fmt.Println(arrayA, array)
    fmt.Println(sliceA, slice)
 
    int1 := 3
    int2 := int1
    int2 = 4
    fmt.Println("int1:", int1, "int2:", int2)
 
    bool1 := true
    bool2 := bool1
    bool2 = false
    fmt.Println("bool1:", bool1, "bool2:", bool2)
 
    var (
        float32A float32 = 1.1
        float64A float64 = 1.2
    )
    float32B := float32A
    float32B = 2.1
    fmt.Println("float32A:", float32A, "float32B:", float32B )
 
    float64B := float64A
    float64B = 2.2
    fmt.Println("float64A:", float64A, "float64B:", float64B )
 
    map1 := map[string]int{"A":1, "B":2}
    map2 := map1
    map2["A"] = 2
    fmt.Println("map1:", map1)
    fmt.Println("map2:", map2)
}
```
###### 执行结果

```
 
[Z B C] [A B C]
[Z B C] [A B C]
int1: 3 int2: 4
bool1: true bool2: false
float32A: 1.1 float32B: 2.1
float64A: 1.2 float64B: 2.2
map1: map[A:2 B:2]
map2: map[A:2 B:2]
m: 0xc00000a158
m1: 0xc00000a160
```

# 4 指针传递值传递

https://www.jianshu.com/p/759b28a2552c

+ 严格地说，go方法或函数只有一种传递方式，那就是`值传递`。每次将一个变量作为参数传递时，都会创建一个新的变量副本并将其传递给所调用的函数或方法。副本分配在不同的内存地址。

+ 在指针传递变量的情况下，将创建指向相同内存地址的新副本。

## 4.1 值传递

```go
package main
 
import "fmt"
 
func changeInt(a int) {
    a = 100
}
 
func changeSlic(s []int) {
    s[0] = 100
}
 
func main() {
//值类型在传递时，值不变
    num := 1
    changeInt(num)
    fmt.Println(num)
 
// 引用类型改函数内数据对函数外有影响
    nums := []int{1, 2, 3}
    changeSlic(nums)
    fmt.Println(nums)
}
```

###### 执行结果

```
1
[100 2 3]
```

## 4.2 指针传递

+ 函数main中的变量num在函数changeIntByPoint中被修改。发生这种情况是因为＆name和p是存储在相同内存地址的相同结构的两个不同指针。

```go
package main
 
import "fmt"
 
func changeInt(a int) {
    a = 100
}
func changeIntByPoint(p *int) {
    *p = 100
}
 
func changeSlic(s []int) {
    s[0] = 100
}
 
func main() {
//值类型在传递时，值不变
    num := 1
    changeInt(num)
    fmt.Println(num)
 
// 引用类型改函数内数据对函数外有影响
    nums := []int{1, 2, 3}
    changeSlic(nums)
    fmt.Println(nums)
 
    changeIntByPoint(&num)
    fmt.Println(num)
}
```

###### 执行结果

```
1
[100 2 3]
100
```

## 4.3 错误处理

```go
package main
 
//返回值：error（错误类型）
//创建错误类型的值： errors.New ,fmt.Errorf()
//无错误为nil
 
import (
    "errors"
    "fmt"
)
 
func division(a, b int ) (int, error){
    if b == 0 {
        return -1 , errors.New("division by zero")
    }
    return a / b, nil
}
 
func main() {
    fmt.Println(division(1, 4))
    if v, err := division(1, 0); err == nil {
        fmt.Println(v)
    } else {
        fmt.Println(err)
    }
 
    e := fmt.Errorf("Error: %s", "division by zero")
    fmt.Printf("&T, &v\n", e, e)
}
```

###### 执行结果

```
0 <nil>
division by zero
&T, &v
%!(EXTRA *errors.errorString=Error: division by zero, *errors.errorString=Error: division by zero)
```

## 4.4 延迟处理

+ defer是一个栈（先定义的后执行）defer在函数其他内容执行完成后执行
+ 常用来做资源释放和记录日志

```
package main
 
import "fmt"
 
func main() {
    func () {
        fmt.Println("defer")
    }()
    defer func () {
        fmt.Println("defer01")
    }()
 
    defer func () {
        fmt.Println("defer02")
    }()
 
    fmt.Println("main over")
}
```

###### 执行结果

```
defer
main over
defer02
defer01
```

# 5 panic与recover函数

go语言提供panic和recover函数用于处理运行时错误，当调用panic抛出错误，中断原有的控制流程，常用于不可修复性错误。recover函数用于终止错误处理流程，仅在defer语句的函数中有效，用于截取错误处理流程，recover只能捕获到最后一个错误

## 5.1 panic

```
package main
 
import "fmt"
 
func main() {
    fmt.Println("main start")
    panic("error")
 
    fmt.Println("over")
}
```

###### 执行结果

```
main start
panic: error
 
goroutine 1 [running]:
main.main()
    D:/GoLang/day3/panic.go:7 +0x9c
```

## 5.2 recover

+ 只能定义在defer内

```go
package main
 
import "fmt"
 
func main() {
    defer func() {
        if err := recover(); err  != nil {
            fmt.Println(err)
        }
    }()
    fmt.Println("main start")
    panic("error xxxxx")
 
    fmt.Println("over")
}
```

###### 执行结果

```
main start
error xxxxx
```

## 5.1 函数内使用recover

```go
package main
 
import "fmt"
 
func test() (err error) {
    defer func() {
        if err := recover(); err  != nil {
            fmt.Println(err)
        }
    }()
 
    panic("error")
    return
}
 
func main() {
    fmt.Println(test())
}
```

###### 执行结果

```
error
<nil>
```

 