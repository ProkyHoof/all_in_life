---
onenote-id: 0-ed6570e96e1a475aa5b84c7adde90a02!1-DBD29CD2C5C95FE5!s5aaff8ddddca4cce89d68fbf9ed2883a
---
# API

**API**（Application Programming Interface）：应用程序编程接口。  
**简单理解：**API就是别人已经写好的东西，我们不需要自己编写，直接使用即可。  
**Java API****：**指的就是JDK中提供的各种功能的Java类。  
这些类将底层的实现封装起来，我们不需要关心这些类是如何实现的，指学习这些类如何使用即可。
 
## API和API帮助文档

**API****：**目前是JDK中提供的各种功能的Java类。  
**API****帮助文档：**帮助开发人员更好的使用API和查询API的一个工具。
 
# 字符串

## String概述

java.lang.String类代表字符串，Java程序中的所有字符串文字（例如"abc"）都为此类的对象。  
字符串的内容是不会发生改变的，它的对象在创建后不能被更改。  
String是Java定义好的一个类。定义在Java.lang包中，所以使用的时候不需要导包。
 
## 创建String对象的两种格式

1. 直接赋值

String name = "猪脚";

3. new

|   |   |
|---|---|
|构造方法|说明|
|public String()|创建空白字符串，不含任何内容|
|public String(String original)|根据传入的字符串，创建字符串对象|
|public String(char[] chs)|根据字符数组，创建字符串对象|
|public String(byte[] chs)|根据字节数组，创建字符串对象（通过ASCII字码表将数数字进行转换，然后拼接）|

注：如果将字符串变成字符数组，可以使用toCharArray()，返回值为char[]。
 
## Java的内存模型

StringTable（串池）在JDK7版本开始，从方法区中挪到了堆区域（以前是在方法区（用来临时存储.class文件））。

1. 直接赋值

**当使用双引号直接赋值时，系统会检查该字符串在串池中是否存在。不存在：创建新的。存在：复用地址值。**

3. 手动new

**字符串不会复用，会在堆区中重新开辟地址值。**
  
## Java的常用方法（比较）

**==****号的比较**  
基本数据类型比较的是数据值。引用数据类型比较的是地址值。  
**字符串内容的比较**

|   |   |
|---|---|
|boolean equals方法（要比较的字符串）|全部一样结果才是true，否则为false|
|boolean equalslgnoreCase（要比较的字符串）|忽略大小写的比较|

**注意：键盘录入的字符串是在堆区域中****new****出来的地址值。**
 
## 遍历字符串

|   |   |
|---|---|
|public char charAt(int index)|根据索引返回字符|
|public int length()|返回此字符串的长度|
|数组的长度|数组名.length|
|字符串的长度|字符串对象.length()|
 
## 截取字符串

String substring(int beginIndex, int endIndex) 截取  
注意点：包头不包尾，包左不包右。只有返回值才是截取的小串。  
String substring(int beginIndex) 截取到末尾
 
## 替换字符串

string replace(旧值,新值) 替换
 
# StringBuilder

## StringBuilder概述

StringBUilder可以看成是一个容器，创建之后里面的内容是可变的。  
**作用：**提高字符串的操作效率。
 
## StringBuilder构造方法

|   |   |
|---|---|
|方法名|说明|
|public StringBuilder()|创建一个空白可变字符串对象，不含有任何内容。|
|public StringBuilder(String str)|根据字符串的内容，来创建可变字符串对象。|
 
## StringBuilder常用方法

|   |   |
|---|---|
|方法名|说明|
|public StringBuilder append(任意类型)|添加数据，并返会对象本身。|
|public StringBuilder reverse()|反转容器中的内容。|
|public int length()|返回长度（字符出现的个数）。|
|public String toString()|通过toString()就可以实现把StringBuilder转换为String。|
 
**注意：**因为StringBuilder是Java已经写好的类，java在底层对他做了一些特殊处理，打印对象不是地址值。
 
**链式编程：**当我们在调用一个方法的时候，不需要用变量接收他的结果，可以继续调用其他方法。
 
# StringJoiner

## StringJoiner 概述

- StringJoiner跟StringBuilder一样，也可以看成是一个容器，创建之后里面的内容是可变的。
- 作用：提高字符串的操作效率，而且代码编写特变简介，但是目前市场上很少有人用。
- **JDK8****出现的**
 
## StringJoiner的构造方法

|   |   |
|---|---|
|方法名|说明|
|public StringJoiner(间隔符号)|创建一个StringJoiner对象，指定拼接时的间隔符号|
|public StringJoiner(间隔符号, 开始符号, 结束符号)|创建一个StringJoiner对象，指定拼接时的间隔符号|
 
## StringJoiner的成员方法

|   |   |
|---|---|
|方法名|说明|
|public StringJoiner(添加内容)|添加数据，并返回对象本身|
|public int length()|返回长度（字符出现的个数）|
|public String toString()|返回一个字符串（该字符串就是拼接之后的结果）|
 
# 字符串原理

## 字符串拼接的底层原理

**注意：**拼接的时候没有变量，都是字符串。除法字符串的优化机制。在编译的时候就已经时最终的结果了。  
JDK8之前，串池中的内容都是""内的内容，底层逻辑会通过StringBuilder对象中的append()和toString()方法在堆内存中的创建一个拼接的字符串，此字符串不在串池内。
 
## JDK8字符串拼接的底层原理

**注意：**将字符串中要被拼接的字符串，创建一个字符串数组，然后进行字符串的拼接操作。
 
**结论：如果很多字符串变量拼接，不要直接****+****。在底层会创建多个对象，浪费时间，浪费性能。建议利用****StringBuilder****或者****StringJoiner****。**  
**字符串拼接的底层原理（使用”****+****“号进行拼接）**

- 如果没有变量参与，都是字符串直接相加，编译之后就是拼接之后的结果，会复用串池中的字符串。
- 如果有变量参与，每一行拼接的代码，都会在内存中创建新的字符串，浪费内存。

**StringBuilder****提高效率原理图**

- 所有要拼接的内容都会往StringBuilder中放，不会创建很多无用的空间，节约内存。

**StringBuilder****源码分析**

- 默认创建一个长度为16的字节数组。
- 添加的内存长度小于16，直接存。
- 添加的内容大于16会扩容（原来的容量 * 2 + 2）。
- 如果扩容之后还不够，以实际长度为准。
 
# 综合练习