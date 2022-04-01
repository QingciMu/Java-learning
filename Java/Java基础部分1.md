# Java基础部分1

Author:**慕清辞**     Time：**2022.03.31**

## Java的基本特性 优势

- 简单性
- 面向对象
- 可移植性
- 高性能
- 分布式
- 多线程
- 安全性

​	……



## Java的三大版本

JavaSE 标准版（桌面程序、控制台开发……）

JavaEE 企业级开发（Web端 、服务器开发……）

JavaME 嵌入式开发(手机、小家电 ……**知道有这么个东西就行，基本不用了**)



##  JRE 、JDK、 JVM

**JDK**：JDK 是 Java Development Kit 缩写，它是功能齐全的 Java SDK。它拥有 JRE 所拥有的一切，还有编译器（javac）和工具（如 javadoc 和 jdb）。它能够创建和编译程序。

**JRE**： JRE 是 Java 运行时环境。它是运行已编译 Java 程序所需的所有内容的集合，包括 Java 虚拟机（JVM），Java 类库，java 命令和其他的一些基础构件。但是，它不能用于创建新程序。

如果你只是为了运行一下 Java 程序的话，那么你只需要安装 JRE 就可以了。如果你需要进行一些 Java 编程方面的工作，那么你就需要安装 JDK 了。但是，这不是绝对的。有时，即使您不打算在计算机上进行任何 Java 开发，仍然需要安装 JDK。例如，如果要使用 JSP 部署 Web 应用程序，那么从技术上讲，您只是在应用程序服务器中运行 Java 程序。那你为什么需要 JDK 呢？因为应用程序服务器会将 JSP 转换为 Java servlet，并且需要使用 JDK 来编译 servlet。

**JVM**: Java 虚拟机（JVM）是运行 Java 字节码的虚拟机。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果。字节码和不同系统的 JVM 实现是 Java 语言“一次编译，随处可以运行”的关键所在。



## 注释

**单行注释**   //

**多行注释**   /* */

**文档注释** /** */



## Java中的数据类型

Java是一种强类型语言：变量的使用要严格符合规定，所有变量必须**先定义后使用**。

Java 的数据类型分为两大类：

- 基本类型
- 引用类型

### 基本类型

​	Java中一共有8种基本类型：

- 整型

|类型|存储需求（字节）|取值范围|
|--|--|--|
|byte|1|-128~127|
|short|2|-2<sup>15</sup>~2<sup>15</sup>-1|
|int|4|-2<sup>31</sup>~2<sup>31</sup>-1|
|long|8|-2<sup>63</sup>~2<sup>63</sup>-1|

- 浮点型

| 类型   | 存储需求（字节） |
| ------ | ---------------- |
| float  | 4                |
| double | 8                |

- char类型

2个字节 char类型的字面量要用**单引号**括起来

- boolean类型

只有两个值  false 和true

### 引用类型

​	类、接口、数组。（后面详细介绍）



### 常见的一些问题

1. 进制的问题

```Java
public class Main{
	public static void main(Stirng args[]){
		int a = 10;//十进制 10
		int b = 010;//八进制 8
		int c = 0x10;//十六进制 16 0-9，A-F
    //二进制0b
    
    //浮点数的问题
    //具体的业务场景 银行业务 float double 会存在问题
    float f = 0.1f;
    double d = 1.0/10;
    System.out.println(f==d); // false
    
    //应该用BigDecimal类，去处理浮点数的运算。避免误差
	}
}
```

```java
//编码相关
//Unicode编码 两个字节
char c = '\u0061'； //a
```

## 变量与常量



**1. 声明变量**

​	每个变量都有一个类型（type），在声明变量之前，先指定变量的类型，然后是变量名。eg:double salary; 大小写敏感

**2. 变量初始化**

​	声明变量后必须用赋值语句对变量进行显式初始化，未初始化的变量会被Java编译器认为是错误的。（变量的声明尽量靠近该变量第一次使用的地方）

<font color="#dd000">注：从Java10开始，对于局部变量，如果可以从初始值推断出类型，就不需要声明类型，用关键字var</font>

```Java
var days = 12;
```

**3. 常量**

​	在Java中，使用关键字**final**指示常量，表示这个变量只能被赋值一次。一旦被赋值就不可再改变。常量名全部大写。

4. 枚举类型（浅谈，后面会详细讲解）

​	变量的取值只在一个有限的集合内。例如服装的尺寸只有S、M、L、X。但是在编程中使用变量保存可能是一个错误的值。使用枚举类型，包含有限个命名的值。

```Java
enum Size {SMALL,MEDIUM,LARGE,EXTRA_LARGE};
Size s = Size.MEDIUM;

//Size类型的变量只能存储这个类型声明中给定的某个枚举值，或者特殊值null，null表示这个变量没有设置任何值
```

**4. 作用域**

​	类变量：使用static修饰。

​	实例变量：不使用static修饰。方法外，类中，从属于对象。

​	局部变量：方法或代码块中定义的变量。使用之前必须声明，初始化值。

## 运算符

**1. 数值类型之间的转换**

​	![1](https://tva1.sinaimg.cn/large/e6c9d24egy1h0teoqiugej20nq0cwt8x.jpg)

​	6个实线箭头表示无信息丢失的转换，三个虚线箭头表示可能有精度损失的转换。

​	例如123456789是一个大整数，它所包含的位数比float类型所能表示的位数多。转换为float时，将会得到正确的大小，但是会损失精度。

```java
int n = 123456789;
float f = n;//f is 1.23456792E8
```

​	当使用二元运算符连接两个值时（eg：n+f，n为整数，f为浮点数），先要将两个数转换为同一种类型，然后计算。（优先级从上到下）

- 有一个是double->double
- 有一个float->float
- 有一个类型为long->long
- 否则为int

```java
public class Main {
    public static void main(String[] args) {
        long a = 1;
        float b = 1.1f;
        Object c = a+b;
        System.out.println(c.getClass().toString()); //class java.lang.Float
    }
}
```



​	**2. 强制类型转换**

​	在必要的时候，int类型会自动转换为double类型，但是有时候也需要将double转换为int类型。在Java中允许这种数值之间的类型转换，即：强制类型转换。

1. **精度问题**

- 截断小数点

```java
double x = 9.997;
int nx = (int)x;//nx=9;
```

- 有舍入

```Java
double x = 9.997;
int nx = (int)Math.round(x);//nx=10;
```

2. **内存溢出问题**

```Java
int i = 128;
byte b = (byte)i;//会转换成一个完全不同的数据
```



**3. 位运算**

位元算  &与、｜或、^ 、~， &&  || 采用短路的方式，即得到结果时不一定两个操作数都要计算。

<< 和>> 左移和右移操作。



## 包机制与Java Doc

### 包

​	包，解决文件重名的问题。包的命名规范，**一般使用公司域名倒置作为包名，eg：com.baidu.www**



### Java Doc

​	Java Doc是用来生成自己的API文档的。

1. 参数

- author：作者
- version：版本号
- since：需要最早使用的jdk版本
- param：参数
- return：返回值情况
- throws：异常抛出情况

```java
/**
 *@author
 *@version
 *@since
 */
public class Main{
	String name;
  /**
   *@parma
   *@return
   */
  public String test(String name){
    return name;
  }
}
```

2. 生成doc文档

```bash
javadoc -encoding UTF-8 -charset UTF-8 Main.java
```



## 流程控制

### Switch

​	一种多选择的实现 方式 switch case 语句。

​	判断一个变量与一系列值中某个值是否相等，每个值称为一个分支。



**switch语句中的变量类型可以是**：

- byte、short、int或者char
- 从Java SE 7 开始 switch支持字符串String类型，同时case标签必须为字符串常量或字面量。

```java
public class Main {
    public static void main(String[] args) {
        char grade = 'C';
        switch (grade){
            case 'A':
                System.out.println("优秀");
                break;
            case 'B':
                System.out.println();
            default:
                System.out.println();
        }
    }
}

```

<font color="#dd000">注：每一句case写完，都要加上break</font>

支持字符串String类型

```java
package com.Seejen.java;

public class Main {
    public static void main(String[] args) {
        String name = "Seejen";
        switch (name){
            case "Seejen":
                System.out.println("Seejen");
                break;
            case "Ycc":
                System.out.println("Ycc");
                break;
            default:
                System.out.println("No Person");
        }
    }
}
```

 **能够支持String类型的底层原理**   查看反编译之后的class文件，其实是通过<font color="#dd000">hashCode()方法和equals()方法</font>来比较。

```java
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package com.Seejen.java;

public class Main {
    public Main() {
    }

    public static void main(String[] args) {
        String name = "Seejen";
        byte var3 = -1;
        switch(name.hashCode()) {
        case -1822358144:
            if (name.equals("Seejen")) {
                var3 = 0;
            }
            break;
        case 88697:
            if (name.equals("Ycc")) {
                var3 = 1;
            }
        }

        switch(var3) {
        case 0:
            System.out.println("Seejen");
            break;
        case 1:
            System.out.println("Ycc");
            break;
        default:
            System.out.println("No Person");
        }

    }
}
```



### Do...While

​	对于while而言，如果不满足条件就不能进入循环，但有时后需要在不满足条件的情况下，最少要执行一次。e

|          | while        | do...while   |
| -------- | ------------ | ------------ |
| 判断顺序 | 先判断后执行 | 先执行后判断 |
| 执行次数 | >=0          | >=1          |



### For循环

**增强for循环**（遍历数组，集合）

- Java5引入了一种主要用于数组或集合的增强型for循环
- 声明语句：声明新的局部变量，该变量的类型必须和数组元素的类型匹配/作用域限定在循环语句块，其值与此时数组元素的值相等。
- 表达式：表达式是要访问的数组名，或者返回值为数组的方法。

```java
package com.Seejen.java;

public class Main {
    public static void main(String[] args) {
        int[] nums = new int[]{1,4,6,20};
        for (int num : nums) {
            System.out.println(nums);
        }
    }
}
```



## 方法

Java方法时语句的集合，它们在一起执行一个功能。

- 方法是解决一类问题的步骤的有序组合
- 方法包含于类或对象中
- 方法在程序中被创建，在其他地方被引用



设计方法的原则：方法的本意是功能块，我们实现方法的时候，最好保持方法的原子性，<font color="#dd000">一个方法只完成一个功能，这样有利于后期的扩展</font>



方法包含一个方法头和一个方法体

- 修饰符：可选
- 返回值类型：
- 方法名
- 参数类型：形参、实参
- 方法体



### 方法的调用

对象名.方法名

静态方法：类名.方法名



### 值传递和引用传递

程序设计语言将实参传递给方法（或函数）的方式分为两种：

- **值传递** ：方法接收的是实参值的拷贝，会创建副本。
- **引用传递** ：方法接收的直接是实参所引用的对象在堆中的地址，不会创建副本，对形参的修改将影响到实参。



### 重载

重载就是在一个类中，有相同的函数名称，但是形参不同的函数。



规则

- 方法名必须相同
- 参数列表必须不同（个数、类型、顺序）
- 返回类型可以相同也可以不同
- 仅仅返回类型不同不足以成为方法的重载



eg：构造方法



### 可变参数

1. JDK1.5开始，Java支持传递同类型的可变参数
2. 在方法声明中，制定参数类型后加一个...
3. 一个方法中只能有一个可变参数，并且必须是方法的最后一个参数，任何的普通参数必须在之前声明



## 数组

### 数组工具类Arrays

方法

- toString()
- sort()
- fill()



