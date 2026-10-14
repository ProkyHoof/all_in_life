---
tags:
  - 知识
类型: 计算机
领域: Java_进阶
来源: "[黑马程序员Java零基础视频教程_上部(Java入门，含斯坦福大学练习题+力扣算法题和大厂java面试题）](https://www.bilibili.com/video/BV17F411T7Ao?vd_source=aae3c81bc41fca87a978ef4700fc0a91)"
日期: 2026-10-08
关联:
---

# 1 IO 流
## 1.1 IO 流的简介
IO 流：存储和读取数据的解决方案。  
I：input  
O：output  
IO 流用于读写文件中的数据（可以读写文件，或网络中的数据）。  
## 1.2 IO 流的分类
流的方向：输入流（文件 -> 程序）和输出流（程序 -> 文件）。  
操作文件类型：字节流（所有类型的文件）和字符流（纯文本文件）。  
## 1.3 IO 流体系

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20d9804c03d4454087.png)  

# 2 FileOutputStream
操作本地文件的字节输出流，可以把程序中的数据写到本地文件中。  
书写步骤：  
1. 创建字符输出流对象。  
2. 写数据。  
3. 释放资源。  

```java
public static void main(String[] args) throws IOException {
    FileOutputStream fos = new FileOutputStream("myio\\a.txt");
    fos.write(97);
    fos.close();
}
```

## 2.1 FileOutputStream 书写细节
1. 创建字节输出流对象。  
2. 写数据。  
3. 释放资源。  

细节一：参数是字符串表示的路径或者是 File 对象都是可以的。  
细节二：如果文件不存在会创建一个新的文件，但是要保证父级路径是存在的。  
细节三：如果文件已经存在，则会清空文件。  
细节四：write 方法的参数是整数，但是实际上写到本地文件中的是整数在 ASCII 上对应的字符。  
细节五：每次使用完流之后都要释放资源。  
## 2.2 FileOutputStream 写数据的 3 种方式

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20af2b809add0eb1b7.png)  

```java
FileOutputStream fos = new FileOutputStream("myio\\a.txt");
byte[] bytes = {97, 98, 99, 100, 101};
fos.write(bytes);
fos.close();
```

```java
fos.write(bytes, 1, 2); //从索引 1 开始,写 2 个字节
fos.close();
```

## 2.3 FileOutputStream 写数据的两个小问题
换行写：  
再次写出一个换行符就可以了。  

```vtable
{"rows":[[{"t":"操作系统","rs":1,"cs":1},{"t":"换行符","rs":1,"cs":1}],[{"t":"windows","rs":1,"cs":1},{"t":"\\r\\n","rs":1,"cs":1}],[{"t":"Linux","rs":1,"cs":1},{"t":"\\n","rs":1,"cs":1}],[{"t":"Mac","rs":1,"cs":1},{"t":"\\r","rs":1,"cs":1}]]}
```

细节：  
在 Windows 操作系统当中，Java 对回车换行进行了优化。  
虽然完整的是 \r\n，但是我们写其中一个 \r 或者 \n，Java 也可以实现换行，因为 Java 在底层会补全。  
建议：不要省略，还是写全了。  
续写：  
如果想要续写，打开续写开关即可。  
开关位置：创建对象的第二个参数。  
默认 false，表示关闭续写，此时创建对象会清空文件。  
手动传递 true，表示打开续写，此时创建对象不会清空文件。  

```java
FileOutputStream fos = new FileOutputStream("myio\\a.txt");
String str = "abc";
byte[] bytes1 = str.getBytes();
fos.write(bytes1);
String wrap = "\r\n";
byte[] bytes2 = wrap.getBytes();
fos.write(bytes2);
String str2 = "666";
byte[] bytes3 = str2.getBytes();
fos.write(bytes3);
fos.close();
```

```java
FileOutputStream fos = new FileOutputStream("myio\\a.txt", true); //打开续写开关
```

# 3 FileInputStream
操作本地文件的字节输入流，可以把本地文件中的数据读取到程序中来。  
书写步骤：  
1. 创建字节输入流对象。  
2. 读数据。  
3. 释放资源。  

```java
FileInputStream fis = new FileInputStream("myio\\a.txt");
int b = fis.read();
System.out.println((char) b);
fis.close();
```

## 3.1 FileInputStream 书写细节
1. 创建字节输入流对象。  
2. 读取数据。  
3. 释放资源。  

细节 1：如果文件不存在，就直接报错。  
细节 2：一次读一个字节，读出来的是数据在 ASCII 上对应的数字。  
细节 3：读到文件末尾了，read 方法返回 -1。  
细节 4：每次使用完流必须要释放资源。  
## 3.2 FileInputStream 循环读取

```java
FileInputStream fis = new FileInputStream("myio\\a.txt");
int b;
while ((b = fis.read()) != -1) {
    System.out.print((char) b);
}
fis.close();
```

## 3.3 文件拷贝
拷贝的核心思想：边读边写。  

```java
FileInputStream fis = new FileInputStream("D:\\movie.mp4");
FileOutputStream fos = new FileOutputStream("myio\\copy.mp4");
int b;
while ((b = fis.read()) != -1) {
    fos.write(b);
}
fos.close();
fis.close();
```

## 3.4 FileInputStream 读取的问题
IO 流：如果拷贝的文件过大，那么速度会很慢。  
FileInputStream 一次读写一个字节。  
## 3.5 FileInputStream 一次读多个字节

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2069eaf31d922e9884.png)  

> 注意：一次读一个字节数组的数据，每次对于读取会尽可能把数组装满。  

```java
FileInputStream fis = new FileInputStream("myio\\a.txt");
byte[] bytes = new byte[2];
int len = fis.read(bytes);
String str = new String(bytes, 0, len);
System.out.println(str);
```

> 注意：len 是读取数据的个数。  

## 3.6 try…catch 异常处理

```java
FileInputStream fis = null;
FileOutputStream fos = null;
try {
    fis = new FileInputStream("D:\\movie.mp4");
    fos = new FileOutputStream("myio\\copy.mp4");
    int len;
    byte[] bytes = new byte[1024 * 1024 * 5];
    while ((len = fis.read(bytes)) != -1) {
        fos.write(bytes, 0, len);
    }
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (fos != null) {
        try {
            fos.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    if (fis != null) {
        try {
            fis.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

接口：AutoCloseable。  
特点：特定的情况下，可以自动释放资源。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2056e082a05741e70d.png)  

```java
try (FileInputStream fis = new FileInputStream("D:\\movie.mp4");
     FileOutputStream fos = new FileOutputStream("myio\\copy.mp4")) {
    int len;
    byte[] bytes = new byte[1024 * 1024 * 5];
    while ((len = fis.read(bytes)) != -1) {
        fos.write(bytes, 0, len);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

```java
public static void main(String[] args) throws FileNotFoundException {
    FileInputStream fis = new FileInputStream("D:\\movie.mp4");
    FileOutputStream fos = new FileOutputStream("myio\\copy.mp4");
    try (fis; fos) {
        int len;
        byte[] bytes = new byte[1024 * 1024 * 5];
        while ((len = fis.read(bytes)) != -1) {
            fos.write(bytes, 0, len);
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

# 4 字节流
## 4.1 计算机的存储规则
在计算机中，任一数据都是以二进制的形式来存储的。  
计算机最小的存储单元是字节。  
1. GB2312 字符集：1980 年发布，1981 年 5 月 1 日实施的简体中文汉字编码国家标准。收录 7445 个图形字符，其中包括 6763 个简体汉字。  
2. BIG5 字符集：台湾地区繁体中文标准字符集，共收录 13053 个中文字，1984 年实施。  
3. GBK 字符集：2000 年 3 月 17 日发布，收录 21003 个汉字。包含国家标准 GB13000-1 中的全部中日韩汉字，和 BIG5 编码中的所有汉字。  

   Windows 系统默认使用的就是 GBK，系统显示 ANSI。  
4. Unicode 字符集：国际标准字符集，它将世界各种语言的每个字符定义一个唯一的编码，以满足跨语言、跨平台的文本信息转换。  

# 5 字符集
## 5.1 ASCII 字符集
ASCII 编码规则：前面补 0，补齐 8 位。  
## 5.2 GBK 字符集
汉字：  
规则 1：汉字两个字节存储。  
规则 2：高位字节二进制一定以 1 开头，转成十进制之后是一个负数。  
GBK 汉字编码规则：存储时高位字节二进制以 1 开头，转成十进制后是负数。  
英文：  
规则：英文一个字节存储，兼容 ASCII，二进制前面补 0。  
## 5.3 Unicode 万国码
研发方：统一码联盟（也叫 Unicode 组织）。  
总部位置：美国加州。  
研发时间：1994 年。  
发布时间：1994 年发布 1.0 版本，期间不断添加新的文字，最新的版本是 2022 年 9 月 13 日发布的 15.0 版本。  
联盟组成：世界各地主要的电脑制造商、软件开发商、政府部门、研发机构、国际机构、及个人组成。  
UTF-16 编码规则：用 2 - 4 个字节保存。  
UTF-32 编码规则：固定使用 4 个字节保存。  
UTF-8 编码规则：用 1 - 4 个字节保存。  
英文：1 个字节。  
简体中文：3 个字节。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20faa4ac58d426cb8d.png)  

## 5.4 乱码
原因 1：读取数据时未读完整个汉字。  
原因 2：编码和解码时的方式不统一。  
## 5.5 如何不产生乱码
1. 不要用字节流读取文本文件。  
2. 编码解码时使用同一个码表，同一个编码方式。  

## 5.6 扩展
字节流读取中文会乱码，但是拷贝不会出乱码。  
因为字节流读取中文会使用不同的解码进行读取，但是拷贝不会进行读取操作，只会将数据源进行拷贝，读取数据时使用记事本的解码方式。  
Java 中编码的方法：  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%209da0bfbb66901fba.png)  

Java 中解码的方法：  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20a30c45b8d0b5c855.png)  

编码：  

```java
String str = "ai你";
byte[] bytes1 = str.getBytes();
System.out.println(Arrays.toString(bytes1));
byte[] bytes2 = str.getBytes("GBK");
System.out.println(Arrays.toString(bytes2));
```

解码：  

```java
String str2 = new String(bytes1);
System.out.println(str2);
String str3 = new String(bytes2, "GBK");
System.out.println(str3);
```

# 6 字符流
字符流的底层其实就是字节流。  
字符流 = 字节流 + 字符集。  
特点：  
输入流：一次读一个字节，遇到中文时，一次读多个字节。  
输出流：底层会把数据按照指定的编码方式进行编码，变成字节再写到文件中。  
使用场景：  
对于纯文本文件进行读写操作。  
## 6.1 FileReader
1. 创建字符输入流对象。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%201b67da7cea9b07c6.png)  

细节 1：如果文件不存在，就直接报错。  
2. 读取数据。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20cc756876f965e66c.png)  

细节 1：按字节进行读取，遇到中文，一次读多个字节，读取后解码，返回一个整数。  
细节 2：读到文件末尾了，read 方法返回 -1。  
3. 释放资源。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2075b88b1627a53f2c.png)  

```java
FileReader fr = new FileReader("myio\\a.txt");
```

读取数据 read()：  
字符流的底层也是字节流，默认也是一个字节一个字节的读取的。  
如果遇到中文就会一次读取多个，GBK 一次读两个字节，UTF-8 一次读三个字节。  
read() 细节：  
1. read()：默认也是一个字节一个字节的读取的，如果遇到中文就会读取多个。  
2. 在读取之后，方法的底层还会进行解码并转成十进制。最终将这个十进制作为返回值。这个十进制的数据也表示在字符集上的数字。  

英文：文件里面二进制数据 0110 0001，read 方法进行读取，解码并转成十进制 97。  
中文：文件里面的二进制数据 1100110 10110001 10001001，read 方法进行读取，解码并转成十进制 27721。  

```java
int ch;
while ((ch = fr.read()) != -1) {
    System.out.println((char) ch);
}
fr.close();
```

```java
FileReader fr = new FileReader("myio\\a.txt");
char[] chars = new char[2];
int len;
while ((len = fr.read(chars)) != -1) {
    System.out.print(new String(chars, 0, len));
}
fr.close();
```

read(chars)：读取数据，解码，强转三步合并了，把强转之后的字符放到数组当中。  
空参的 read + 强转类型转换。  
## 6.2 FileWriter 构造方法

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2013918ea20dc426c0.png)  

## 6.3 FileWriter 成员方法

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2023bdbb5389da2651.png)  

## 6.4 FileWriter 书写细节
1. 创建字符输出流对象。  
2. 写数据。  
3. 释放资源。  

细节 1：参数是字符串表示的路径或者 File 对象都是可以的。  
细节 2：如果文件不存在会创建一个新的文件，但是要保证父级路径是存在的。  
细节 3：如果文件已经存在，则会清空文件，如果不想清空可以打开续写开关。  
细节 4：如果 write 方法的参数是整数，但是实际上写到本地文件中的是整数在字符集上对应的字符。  
细节 5：每次使用完流之后都要释放资源。  

```java
FileWriter fw = new FileWriter("myio\\a.txt");
fw.write(25105);
fw.close();
```

根据字符集的编码方式进行编码，把编码之后的数据写到文件中去（默认是 UTF-8）。  

```java
fw.write("你好!");
```

```java
char[] chars = {'a', 'b', 'c', '我'};
fw.write(chars);
```

## 6.5 字符流原理解析
1. 创建字符输入流对象。  
2. 读取数据。  

底层：  
1. 关联文件，并创建缓冲区（长度为 8192 的字节数组）。  
2. 判断缓冲区中是否有数据可以读取。  
3. 缓冲区没有数据：就从文件中获取数据，装到缓冲区中，每次尽可能装满缓冲区。如果文件中没有数据了，返回 -1。  
4. 缓冲区有数据：就从缓冲区中读取。  

空参的 read 方法：一次读取一个字节，遇到中文一次读多个字节，把字节解码并转成十进制返回。  
有参的 read 方法：把读取字节，解码，强转三步合并了，强转之后的字符放到数组中。  
### 6.5.1 flush 和 close 方法

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2098a0c4afa95975af.png)  

flush 刷新：刷新之后，还可以继续往文件中写出数据。  
close 关流：断开通道，无法再往文件中写出数据。  

```java
public static void main(String[] args) throws IOException {
    FileWriter fw = new FileWriter("myio\\a.txt");
    fw.write("夜空中最亮的星");
    fw.write("能否带我前行");
    fw.flush();
    fw.write("那仰望的人");
    fw.write("心底的孤独和叹息");
    fw.close();
}
```

## 6.6 字节流和字符流的使用场景
字节流：拷贝任意类型的文件。  
字符流：读取纯文本文件中的数据；往纯文本文件中写出数据。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20f9110060b7741480.png)  
![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20d9446f4e9a10a61f.png)  
![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2049be835b346c4287.png)  

# 7 高级流
## 7.1 缓冲流

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20c8995741a0ef4f86.png)  

原理：底层自带了长度为 8192 的缓冲区提高性能。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20bfc65a57fc550ce3.png)  

### 7.1.1 字节缓冲流

```java
public static void main(String[] args) throws IOException {
    BufferedInputStream bis = new BufferedInputStream(new FileInputStream("myio\\a.txt"));
    BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("myio\\copy.txt"));
    int b;
    while ((b = bis.read()) != -1) {
        bos.write(b);
    }
    bos.close();
    bis.close();
}
```

```java
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("myio\\a.txt"));
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("myio\\copy.txt"));
byte[] bytes = new byte[1024];
int len;
while ((len = bis.read(bytes)) != -1) {
    bos.write(bytes, 0, len);
}
bos.close();
bis.close();
```

### 7.1.2 字节缓冲流提高效率的原理

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20068b2e45fe0074da.png)  

### 7.1.3 字符缓冲流

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20352a76a6429b94e7.png)  

原理：底层自带了长度为 8192 的缓冲区提高性能。  
### 7.1.4 字符缓冲流的构造方法

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20d7587347bf7577c2.png)  

### 7.1.5 字符缓冲流特有的方法

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20b855372e6e46663c.png)  

```vtable
{"rows":[[{"t":"操作系统","rs":1,"cs":1},{"t":"换行符","rs":1,"cs":1}],[{"t":"Mac","rs":1,"cs":1},{"t":"\\r","rs":1,"cs":1}],[{"t":"Linux","rs":1,"cs":1},{"t":"\\n","rs":1,"cs":1}],[{"t":"Windows","rs":1,"cs":1},{"t":"\\r\\n","rs":1,"cs":1}]]}
```

细节：readLine() 方法在读取的时候，一次读一整行，遇到回车换行结束。但是它不会把回车换行读到内存当中。  

```java
public static void main(String[] args) throws FileNotFoundException {
    BufferedReader br = new BufferedReader(new FileReader("myio\\a.txt"));
    String line = br.readLine();
    System.out.println(line);
    br.close();
}
```

```java
String line;
while ((line = br.readLine()) != null) {
    System.out.println(line);
}
```

```java
public static void main(String[] args) throws IOException {
    BufferedWriter bw = new BufferedWriter(new FileWriter("myio\\a.txt", true));
    bw.write("numb");
    bw.newLine();
    bw.write("prokyhoof");
    bw.newLine();
    bw.close();
}
```

### 7.1.6 缓冲流为什么能提高性能
- 缓冲流自带长度为 8192 的缓冲区。  
- 可以显著提高字节流的读写性能。  
- 对于字符流提升不明显，对于字符缓冲流而言关键点是两个特有的方法：readLine()、newLine()。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20a8956629319027e2.png)  
![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20475fa876b3b33594.png)  
![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%209a9613f35f8e8925.png)  

## 7.2 转换流
转换流是字符流和字节流之间的桥梁。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%209e5a4f4403bd82a6.png)  

作用 1：指定字符集读写。  
作用 2：字节流想要使用字符流中的方法。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2092e09e1acde700ac.png)  

```java
public static void main(String[] args) throws IOException {
    InputStreamReader isr = new InputStreamReader(new FileInputStream("myio\\a.txt"), "GBK");
    int ch;
    while ((ch = isr.read()) != -1) {
        System.out.println((char) ch);
    }
    isr.close();
}
```

```java
FileReader fr = new FileReader("myio\\a.txt", Charset.forName("GBK"));
int ch;
while ((ch = fr.read()) != -1) {
    System.out.println((char) ch);
}
fr.close();
```

```java
public static void main(String[] args) throws IOException {
    OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("myio\\a.txt"), "GBK");
    osw.write("你好你好");
    osw.close();
}
```

```java
FileWriter fw = new FileWriter("myio\\a.txt", Charset.forName("GBK"));
fw.write("你好你好");
fw.close();
```

利用字节流读取文件中的数据，每次读一整行，而且不能出现乱码。  
1. 字节流在读取中文的时候，是会出现乱码的，但是字符流可以搞定。  
2. 字节流里面是没有读一整行的方法的，只有字符缓冲流才能搞定。  

```java
public static void main(String[] args) throws IOException {
    FileInputStream fis = new FileInputStream("myio\\a.txt");
    InputStreamReader isr = new InputStreamReader(fis);
    BufferedReader br = new BufferedReader(isr);
    String str = br.readLine();
    System.out.println(str);
    br.close();
}
```

## 7.3 序列化流

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2041b5810d2c5ab52c.png)  

序列化流可以把 Java 中的对象写到本地文件中。  
### 7.3.1 序列化流（对象操作输出流）

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%206d91a6f3ad8a7bb5.png)  

```java
Student stu = new Student("zhangsan", 23);
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("myio\\a.txt"));
oos.writeObject(stu);
oos.close();
```

### 7.3.2 序列化流的小细节
使用对象输出流将对象保存到文件时会出现 NotSerializableException 异常。  
解决方案：需要让 Javabean 类实现 Serializable 接口。  
Serializable 接口里面是没有抽象方法的，该类接口一般称为标记型接口。  
一旦实现了这个接口，那么就表示当前的 Student 类可以被序列化。  
### 7.3.3 反序列化流（对象操作输入流）
可以把序列化到本地文件中的对象，读取到程序中来。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20907506a28f03c399.png)  

```java
ObjectInputStream ois = new ObjectInputStream(new FileInputStream("myio\\a.txt"));
Student o = (Student) ois.readObject();
System.out.println(o);
ois.close();
```

### 7.3.4 序列化流、反序列化流的细节汇总
1. 使用序列化流将对象写到文件时，需要让 Javabean 类实现 Serializable 接口。否则，会出现 NotSerializableException 异常。  
2. 序列化流写到文件中的数据是不能修改的，一旦修改就无法再次读回来了。  
3. 序列化对象后，修改了 Javabean 类，再次反序列化，会不会有问题？会出问题，会抛出 InvalidClassException 异常。解决方案：给 Javabean 类添加 serialVersionUID（序列号、版本号）。  
4. 如果一个对象中的某个成员变量的值不想被序列化，又该如何实现呢？解决方案：给该成员变量加 transient 关键字修饰，该关键字标记的成员变量不参与序列化过程。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%2021cc524ed7fa9a37.png)  

## 7.4 打印流

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20e2c67ce0189f7557.png)  

分类：打印流一般是指：PrintStream、PrintWriter 两个类。  
特点 1：打印流只操作文件目的地，不操作数据源。  
特点 2：特有的写出方法可以实现，数据原样写出。  
特点 3：特有的写出方法，可以实现自动刷新，自动换行。（打印一次数据 = 写出 + 换行 + 刷新）  
### 7.4.1 字节打印流

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%205ed97ee15bcc0762.png)  

字节流底层没有缓存区，开不开自动刷新都一样。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20484dd28d1978cbc3.png)  

```java
PrintStream ps = new PrintStream(new FileOutputStream("myio\\a.txt"), true, Charset.forName("UTF-8"));
ps.println(97);
ps.close();
```

### 7.4.2 字符打印流

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20e5e7b546ff9d5459.png)  

字符流底层有缓冲区，想要自动刷新需要开启。  

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20a5bd8da2935e14d3.png)  

```java
PrintWriter pw = new PrintWriter(new FileWriter("myio\\a.txt"), true);
pw.println("ProkyHoof");
pw.close();
```

```java
PrintStream ps = System.out;
ps.println("ProkyHoof");
```

获得打印流的对象，此打印流在虚拟机启动的时候，由虚拟机创建，默认指向控制台。  
特殊的打印流，系统中的标准输出流，是不能关闭的，在系统中是唯一的。  
## 7.5 解压缩流、压缩流
### 7.5.1 解压流
解压本质：把每一个 ZipEntry 按照层级拷贝到本地另一个文件夹中。  

```java
public static void main(String[] args) throws IOException {
    File src = new File("D:\\a.zip");
    File dest = new File("D:\\");
    unzip(src, dest);
}

public static void unzip(File src, File dest) throws IOException {
    ZipInputStream zip = new ZipInputStream(new FileInputStream(src));
    ZipEntry entry;
    while ((entry = zip.getNextEntry()) != null) {
        System.out.println(entry);
        if (entry.isDirectory()) {
            File file = new File(dest, entry.toString());
            file.mkdirs();
        } else {
            FileOutputStream fos = new FileOutputStream(new File(dest, entry.toString()));
            int b;
            while ((b = zip.read()) != -1) {
                fos.write(b);
            }
            fos.close();
            zip.closeEntry();
        }
    }
    zip.close();
}
```

### 7.5.2 压缩流
压缩本质：把每一个（文件、文件夹）看成 ZipEntry 对象放到压缩包中。  

```java
public static void main(String[] args) throws IOException {
    File src = new File("D:\\a.txt");
    File dest = new File("D:\\");
    toZip(src, dest);
}

public static void toZip(File src, File dest) throws IOException {
    ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(new File(dest, "a.zip")));
    ZipEntry entry = new ZipEntry("a.txt");
    zos.putNextEntry(entry);
    FileInputStream fis = new FileInputStream(src);
    int b;
    while ((b = fis.read()) != -1) {
        zos.write(b);
    }
    zos.closeEntry();
    zos.close();
}
```

```java
public static void main(String[] args) throws IOException {
    File src = new File("D:\\aaa");
    File destParent = src.getParentFile();
    File dest = new File(destParent, src.getName() + ".zip");
    ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(dest));
    toZip(src, zos, src.getName());
    zos.close();
}

public static void toZip(File src, ZipOutputStream zos, String name) throws IOException {
    File[] files = src.listFiles();
    for (File file : files) {
        if (file.isFile()) {
            ZipEntry entry = new ZipEntry(name + "/" + file.getName());
            zos.putNextEntry(entry);
            FileInputStream fis = new FileInputStream(file);
            int b;
            while ((b = fis.read()) != -1) {
                zos.write(b);
            }
            fis.close();
            zos.closeEntry();
        } else {
            toZip(file, zos, name + "/" + file.getName());
        }
    }
}
```

## 7.6 Commons-io
### 7.6.1 Commons-io 简介
Commons-io 是 apache 开源基金组织提供的一组有关 IO 操作的开源工具包。  
作用：提高 IO 流的开发效率。  
### 7.6.2 Commons-io 使用步骤
1. 在项目中创建一个文件夹：lib。  
2. 将 jar 包复制粘贴到 lib 文件夹。  
3. 右键点击 jar 包，选择 Add as Library -> 点击 OK。  
4. 在类中导包使用。  

### 7.6.3 Commons-io 常见方法

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%20ba763828986be6c3.png)  
![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%202304e79408afb445.png)  

```java
File src = new File("myio\\a.txt");
File dest = new File("myio\\copy.txt");
FileUtils.copyFile(src, dest);
```

```java
File src = new File("D:\\aaa");
File dest = new File("D:\\bbb");
FileUtils.copyDirectoryToDirectory(src, dest);
```

## 7.7 Hutool 工具包

![](../../../../../03%20附件/attachments/知识附件/Java/1.%20Java/进阶/IO流%20image%202ace7423dad90004.png)  

```java
File file = FileUtil.file("D:\\", "aaa", "bbb", "a.txt");
System.out.println(file);
```

```java
File touch = FileUtil.touch(file);
System.out.println(touch);
```
