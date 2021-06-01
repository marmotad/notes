# 03 JAVA 中的集合

> 集合：可以取代数组的存储类型

+ 数组：数组的长度是固定的。数组中占用连续的存储空间
+ 集合：集合长度不是固定的。元素的个数可变。集合还提供了很多可操作元素成员的方法

## 1 集合的概述

+ 集合的分类
  + 单列集合：Colletion
    + List接口:
      + 对应实现类：
        + ArrayList、LinkedList...
    + Set接口:
      + 对应实现类：
        + HashSet\Tree

  
## 2 ArrayList

+ `ArrayList<E>`

  + ArrayList 是一个实现类的类名

  + `<E>`是一个特殊的数据类型，泛型！（集合中想存储什么类型数据，泛型就写什么）

    + ArrayList<String> / ArratList<Integer> / ArrayList(student)

### 2.1 ArrayList 的构造方法和添加方法

| 方法名                             | 说明                         |
| ---------------------------------- | ---------------------------- |
| public ArrayList<E> ()             | 创建一个空的集合             |
| public boolean  add (E e)          | 向集合的末尾添加一个元素     |
| public void add (int index ,  E e) | 向集合的指定位置添加一个元素 |

```java
package git.cncf.online.day18;

import java.util.ArrayList;

public class ArraylistTest {
    public static void main(String[] args) {
        //通过ArrayList 实现类实例化一个对象，获取了一个空集合
        ArrayList<String>  list = new ArrayList<>();

        //向集合添加元素
        list.add("sss");
        list.add("bbb");
        //打印集合中内容
        System.out.println(list);
        //第一个参数是索引，集合的索引和数组也是从0开始
        list.add(1,"ccc");
        System.out.println(list);
        //使用索引进行插入时，索引的最大取值范围不超过集合元素的个数
        list.add(4,"ddd");
    }
}
```

###### 运行结果

```
[sss, bbb]
[sss, ccc, bbb]
Exception in thread "main" java.lang.IndexOutOfBoundsException: Index: 4, Size: 3
	at java.util.ArrayList.rangeCheckForAdd(ArrayList.java:667)
	at java.util.ArrayList.add(ArrayList.java:479)
	at git.cncf.online.day18.ArraylistTest.main(ArraylistTest.java:20)
```

### 2.2 ArrayList 常用方法

| 方法名                           | 说明                                     |
| -------------------------------- | ---------------------------------------- |
| public boolean remove (object o) | 删除指定的元素，成功返回true             |
| public E remove （int index）    | 删除指定索引对应的元素，返回贝删除的元素 |
| public E set (int index , E e)   | 修改指定索引对应的元素，返回修改前的元素 |
| public E get (int index)         | 获取指定索引对应的元素                   |
| public int size ()               | 返回大小                                 |

```java
package git.cncf.online.day18;

import java.util.ArrayList;

public class ArraylistTest {
    public static void main(String[] args) {
        //通过ArrayList 实现类实例化一个对象，获取了一个空集合
        ArrayList<String>  list = new ArrayList<>();

        //向集合添加元素
        list.add("sss");
        list.add("bbb");
        //打印集合中内容
        System.out.println(list);
        //第一个参数是索引，集合的索引和数组也是从0开始
        list.add(1,"ccc");
        System.out.println(list);
        //使用索引进行插入时，索引的最大取值范围不超过集合元素的个数
        list.add(3,"ddd");
        //删除指定内容的索引，并返回true/false
        System.out.println(list.remove("sss"));
        System.out.println(list.remove("sss"));
        System.out.println(list);
        //修改指定索引内容并返回修改前的内容
        System.out.println(list.set(0,"aaa"));
        System.out.println(list);
        //集合的遍历
        for (int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }
        //增强for遍历
        for (String name : list) {
            System.out.println(name);
        }
    }
}

```

###### 运行结果

```
[sss, bbb]
[sss, ccc, bbb]
true
false
[ccc, bbb, ddd]
ccc
[aaa, bbb, ddd]
aaa
bbb
ddd
aaa
bbb
ddd
```

