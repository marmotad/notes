# 1 什么是ruby

Ruby是一种纯粹的面向对象编程语言。

## 2 ruby运行

### 2.1 查看ruby版本

```shell
ruby --version
```

### 2.2 ruby 控制台

```powershell
C:\Users\范杨>irb
irb(main):001:0> 5*5
=> 25
irb(main):002:0>
```

### 2.3 打印Hello Word

### 2.3.1 代码

```ruby
pusb "Hello Word"
```

### 2.3.2 执行结果

```powershell
D:\Coder\Ruby>ruby hello.rb
Hello Word
```

## 3 定义函数

```ruby
def printHello
  #定义一个函数打印Hello
  puts "Hello"
end

printHello
#引用函数打印Hello


def printHi(name)
  #定义一个可接收参数的函数打印Hi $name
  puts "Hi #{name}."
  #引用一个函数
end
# 用函数打印Hi $name

printHi("tom")


def printage(age = 20)
  #定义一个带有末日参数的函数打印my age $age
  puts "my age #{age}"
end

printage
# 使用默认值打印
printage(23)
# 使用指定值打印
```

