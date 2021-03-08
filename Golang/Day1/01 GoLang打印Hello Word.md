# 01 GoLang打印Hello Word

![image-20210308124616916](01 GoLang打印Hello Word.assets/image-20210308124616916.png)

```
package main
//第一行必须使用package 声明包名
import "fmt"
//使用fmt模块
func main () {
//func 引用包名，包名声明后必须引用  
   fmt.Println("Hello Word")
}
```

在CMD中，使用go build构建包

引用mail库后，go build的文件为可执行文件

  -o ： 指定build后的包名

  -x ：显示详细的build过程