---
onenote-id: 0-60d68bc84b2346a5908420f9f79c83f9!1-DBD29CD2C5C95FE5!s5aaff8ddddca4cce89d68fbf9ed2883a
---
# Math

## Math

- 是一个帮助我们用于进行数学计算的工具类
- **私有化构造方法，所有的方法都是静态的**

**Math****类的常用方法**

|   |   |
|---|---|
|方法名|说明|
|public static int abs(int a)|获取参数绝对值|
|public static double ceil(double a)|向上取整|
|public static double floor(double a)|向下取整|
|public static int round(float a)|四舍五入|
|public static int max(int a, int b)|获取两个int值中的较大值|
|public static double pow(double a, double b)|返回a的b次幂的值|
|public static double random()|返回值为double的随机值，范围[0.0, 1.0)|

bug：  
以int 类型为例，取值范围：-2147483648 ~ 2147483647  
如果没有正数与负数对应，那么传递负数结果有误  
-2147483648没有正数与之对应，所以abs结果产生bug  
在JDK15出现了方法absExact()

|   |   |
|---|---|
|1|System**.**out**.**println**(**Math**.**absExact**(-****2147483648****));** //出错|

|   |   |
|---|---|
|1  <br>2|System**.**out**.**println**(**Math**.**abs**(****88****));** //88  <br>System**.**out**.**println**(**Math**.**abs**(-****88****));** //88|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|System**.**out**.**println**(**Math**.**ceil**(****12.34****));** //13.0  <br>System**.**out**.**println**(**Math**.**ceil**(****12.54****));** //13.0  <br>System**.**out**.**println**(**Math**.**ceil**(-****12.34****));** //-12.0  <br>System**.**out**.**println**(**Math**.**ceil**(-****12.54****));** //-12.0|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|System**.**out**.**println**(**Math**.**floor**(****12.34****));** //12.0  <br>System**.**out**.**println**(**Math**.**floor**(****12.54****));** //12.0  <br>System**.**out**.**println**(**Math**.**floor**(-****12.34****));** //-13.0  <br>System**.**out**.**println**(**Math**.**floor**(-****12.54****));** //-13.0|
 
|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|//四舍五入  <br>System**.**out**.**println**(**Math**.**round**(****12.34****));** //12  <br>System**.**out**.**println**(**Math**.**round**(****12.54****));** //13  <br>System**.**out**.**println**(**Math**.**round**(-****12.34****));** //-12  <br>System**.**out**.**println**(**Math**.**round**(-****12.54****));** //-13|

|   |   |
|---|---|
|1  <br>2|//获取两个正数的较大值  <br>System**.**out**.**println**(**Math**.**max**(****20****,** **30****));** //30|

|   |   |
|---|---|
|1  <br>2|//获取两个正数的最小值  <br>System**.**out**.**println**(**Math**.**min**(****20****,** **30****));** //20|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16|//获取a的b次幂  <br>System**.**out**.**println**(**Math**.**pow**(****2****,** **3****));** //8  <br>/*  <br>细节：  <br>如果第二个参数0 - 1之间的小数  <br>*/  <br>System**.**out**.**println**(**Math**.**pow**(****4****,** **0.5****));** //2.0  <br>System**.**out**.**println**(**Math**.**pow**(****2****, -****2****));** //0.25  <br>/*  <br>建议：  <br>第二个参数：一般传递大于等于1的正数  <br>*/  <br>//开平方  <br>System**.**out**.**println**(**Math**.**sqrt**(****4****));** //2.0  <br>//开立方  <br>System**.**out**.**println**(**Math**.**cbrt**(****8****));** //2.0|

|   |   |
|---|---|
|1  <br>2|//获取随机数1 - 100  <br>System**.**out**.**println**(**Math**.**floor**(**Math**.**random**() *** **100****) +** **1****);**|

# System

## System

System也是一个工具类，提供了一些与系统相关的方法。

|   |   |
|---|---|
|方法名|说明|
|public static void exit(int status)|终止当前运行的Java虚拟机|
|public static long currentTimeMillis()|返回当前系统的时间毫秒值形式（时间原点开始计算）|
|public static void arraycopy(数组源数组，起始索引，目的地数组，起始索引，拷贝数)|数组拷贝|
 
## 计算机中的时间原点

1970年1月1日 08：00：00 是C语言的生日。（北京时间）

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7|/*  <br>方法的形参  <br>状态码  <br>0：表示当前虚拟机是正常停止  <br>非0：表示当前虚拟机异常停止  <br>*/  <br>System**.**exit**(****0****);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//返回时间  <br>**long** l **=** System**.**currentTimeMillis**();**  <br>System**.**out**.**println**(**l**);** //单位是ms|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10|//拷贝数组  <br>**int****[]** arr1 **=** **new int****[] {****1****,** **2****,** **3****,** **4****,** **5****,** **6****,** **7****,** **8****,** **9****,** **10****};**  <br>**int****[]** arr2 **=** **new int****[****10****];**  <br>//把arr1数组中的数组拷贝到arr2中  <br>//参数一：数据源头：要拷贝的数据从哪个数组中来  <br>//参数二：从数组源数组中的第几个索引开始拷贝  <br>//参数三：目的地，我要把数组拷贝到哪个数组中  <br>//参数四：目的地数组的索引  <br>//参数五：拷贝的个数  <br>System**.**arraycopy**(**arr1**,** **0****,** arr2**,** **0****,** **10****);**|

注意：

- 如果数据源数组和目的地数组都是基本数据类型，那么两者的类型必须保持一致，否则会报警。
- 在拷贝的时候需要考虑到数组的长度，如果超出范围也会报错。
- 如果数组源数组和目的地数组都是引用数据类型，那么子类类型可以赋值给父类类型。

# Runtime

## Runtime

Runtime表示当前虚拟机的运行环境。

|   |   |
|---|---|
|方法名|说明|
|public static Runtime getRuntime()|当前系统的运行环境|
|public void exit(int status)|停止虚拟机|
|public int availableProcessors()|获得CPU的线程数|
|public long maxMemory()|JVM能从系统中获取总内存大小（单位byte）|
|public long totalMemory()|JVM已经凑够系统中获取总内存大小（单位byte）|
|public long freeMemory()|JVM剩余内存大小（单位byte）|
|public Process exec(String command)|运行cmd命令|

注意：￼Runtime不能new出对象。
 
|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16  <br>17  <br>18  <br>19  <br>20  <br>21  <br>22  <br>23  <br>24  <br>25  <br>26|Runtime r **=** **new** Runtime**();** //错误  <br>Runtime r **=** Runtime**.**getRuntime**();** //获取Runtime的对象<br><br>  <br><br>//exit 停止虚拟机  <br>Runtime**.**getRuntime**().**exit**(****0****);**<br><br>  <br><br>//获取CPU的线程数  <br>System**.**out**.**println**(**Runtime**.**getRuntime**().**availableProcessors**());**<br><br>  <br><br>//总内存大小，单位byte字节  <br>System**.**out**.**println**(**Runtime**.**getRuntime**().**maxMemory**() /** **1024** **/** **1024****);**<br><br>  <br><br>//已经获取的总内存大小，单位byte字节  <br>System**.**out**.**println**(**Runtime**.**getRuntime**().**totalMemory**() /** **1024** **/** **1024****);**<br><br>  <br><br>//剩余内存大小  <br>System**.**out**.**println**(**Runtime**.**getRuntime**().**freeMemory**() /** **1024** **/** **1024****);**<br><br>  <br><br>//运行cmd命令  <br>Runtime**.**getRuntime**().**exec**(**"notepad"**);** //打开记事本  <br>//shutdown : 关机  <br>//-s 默认在一分钟内关机  <br>//-s -t 指定关机时间  <br>//-a 取消关机操作  <br>//-r 关机并重启  <br>Runtime**.**getRuntime**().**exec**(**"shutdown -s -t 3600"**);** //电脑将会在一个小时后关机|

# Object类

## Object

- Object是java中的顶级父类。所有的类都是直接或间接的继承于Object类。
- Object类中的方法可以被所有子类访问，所以我们要学习Object类和其中的方法。

**Object****的构造方法**

|   |   |
|---|---|
|方法名|说明|
|public Object()|空参构造|

**Object****的成员方法**

|   |   |
|---|---|
|方法名|说明|
|public String toString()|返回对象的字符串表示形式|
|public boolean equals(Object obj)|比较两个对象是否相等|
|protected Object clone(int a)|对象克隆（浅克隆）|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//toString 返回对象的字符串表示形式  <br>Object obj **=** **new** Object**();**  <br>String str1 **=** obj**.**toString**();**  <br>Syetem**.**out**.**println**(**str1**);**|

注意：  
System：类名  
out：静态变量  
System.out：获取打印的对象  
println()：方法  
参数：表示打印的内容  
核心逻辑：当我们打印一个对象的时候，底层会调用对象的toString方法，把对象变成字符串。然后再打印再控制台上，打印完毕换行处理。  
若是想要返回的不是对象的地址值而是属性值，则需要@Override，对toString进行重写。在重写的过中，把对象的属性值进行拼接。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|//equals 比较两个对象是否相等  <br>Student s1 **=** **new** Student**(**"zhangsan"，**12****);**  <br>Student s2 **=** **new** Student**(**"zhangsan"**,** **12****);**  <br>**boolean** result1 **=** s1**.**equals**(**s2**);**  <br>System**.**out**.**println**(**result1**);** //false|

注意：

1. 如果没有重写equals方法，那么默认使用Object中的方法进行比较，比较的是地址值是否相等。
2. 一般来讲地址值对于我们一样不大，所以我们会重写，重写之后比较的就是对象内部的属性值。
3. 字符串中的equals方法，先判断参数是否为字符串，如果是字符串，再比较内部的属性，但是如果参数不是字符串，直接返回false。

## 对象克隆

把A对象的属性值完全拷贝给B对象，也叫对象拷贝，对象复制。  
注意：

1. 方法再底层会帮我们创建一个对象，并把原对象中的数据拷贝过去。
2. 重写Object中的clone方法。
3. 让Javabean类实现Cloneable接口。
4. 创建原对象并调用clone就可以了。

**浅克隆**：不管对象内部的属性是基本数据类型还是引用数据类型，都完全拷贝过来。  
**深克隆**：基本数据类型拷贝过来。字符串复用。引用数据类型会重新创建新的。

## Objects的成员方法

|   |   |
|---|---|
|方法名|说明|
|public static boolean equals(Object a, Object b)|先做非空判断，比较两个对象|
|public static boolean isNull(Object obj)|判断对象是否为null，为null返回true，反之|
|public static boolean noNull(Object obj)|判断对象是否为null，更isNull的结果相反|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|Student s1 **=** **new** Student**();**  <br>Student s2 **=** **new** Student**();**  <br>**boolean** result **=** Objects**.**equals**(**s1**,** s2**);**  <br>System**.**out**.**println**(**result**);** //false|

注意：

1. 方法的底层会判断s1是否为null，如果为null，直接返回false.
2. 如果s1不为null，那么就利用s1再次调用equals方法。
3. 此时s1是Student类型，所以最终还是会调用Student中的equals方法。
4. 如果没有重写，比较地址值，如果重写了，就比较属性值。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|Student s1 **=** **new** Student**();**  <br>Student s2 **=** **null****;**  <br>System**.**out**.**println**(**Objects**.**isNull**(**s1**));** //false  <br>System**.**out**.**println**(**Objects**.**isNull**(**s2**));** //true|

# BigInteger和BigDecimal

## BigInteger

在Java中，整数有四种类型：byte，short，int，long。  
在底层占用字节个数：byte1个字节，short2个字节，int4个字节，long4个字节。

## BigInteger构造方法

|   |   |
|---|---|
|方法名|说明|
|public BigInteger(int num, int rnd)|获取随机大整数，范围：[0 ~ 2的num次方-1]|
|public BigInteger(String val)|获取指定的大整数|
|publlic BigInteger(String val,int radix)|获取指定进制的大整数|
|public static BigInteger valueOf(long val)|静态方法获取BigInteger的对象，内部有优化|
 
注意：对象一旦创建，内部记录的值不能发生改变。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//获取一个随机的大整数  <br>Random r **=** **new** Random**();**  <br>BigInteger bi1 **=** **new** BigInteger**(****4****,** r**);**  <br>System**.**out**.**println**(**bi1**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//获取一个指定的大整数  <br>BigInteger bi2 **=** **new** BigInteger**(**"100"**);**  <br>System**.**out**.**println**(**bi2**);** //100|

注意：字符串中必须是整数，否则会报错。

|   |   |
|---|---|
|1  <br>2|BigInteger bi3 **=** **new** BigInteger**(**"100"**,** **2****);**  <br>System**.**out**.**println**(**bi3**);** //4|

注意：

1. 字符串中的数字必须是整数。
2. 字符串中的数字必须要跟进制吻合。

|   |   |
|---|---|
|1  <br>2  <br>3|//静态方法获取BigInteger的对象，内部有优化  <br>BigInteger bi4 **=** BigInteger**.**valueOf**(****100****);**  <br>System**.**out**.**println**(**bi4**);** //100|

注意：

1. 能表示的范围比较小，只能在long的取值范围之内，如果超出long的范围就不行了。
2. 在内部对常数的数字：-16 ~ 16进行了优化。提前把-16 ~ 16先创建好BigInteger的对象，如果多次获取不会重新创建新的。  
## BigInteger常见成员方法

|   |   |
|---|---|
|方法名|说明|
|public BigInteger add(BigInteger val)|加法|
|public BigInteger subtract(BigInteger val)|减法|
|public BigInteger multiply(BigInteger val)|乘法|
|public BigInteger divide(BigInteger val)|除法，获取商|
|public BigInteger[] divideAndRemainder(BigInteger val)|除法，获取商和余数|
|public boolean equals(Object x)|比较是否相同|
|public BigInteger pow(int exponent)|次幂|
|public BigInteger max/min(BigInteger val)|返回较大值/较小值|
|public int intValue(BigInteger val)|转为int类型整数，超出范围数据有误|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|BigInteger bi1 **=** BigInteger**.**valueOf**(****10****);**  <br>BigInteger bi2 **=** BIgInteger**.**valueOf**(****5****);**  <br>//加法  <br>BigInteger bi3 **=** bi1**.**add**(**bi2**);**  <br>System**.**out**.**println**(**bi3**);** //15|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//除法，获取商和除数  <br>BigInteger**[]** arr **=** bi1**.**divideAndRemainder**(**bi2**);**  <br>System**.**out**.**println**(**arr**[****0****]);** //商  <br>System**.**out**.**println**(**arr**[****1****]);** //除数|

|   |   |
|---|---|
|1  <br>2  <br>3|//比较是否相同  <br>**boolean** result **=** bi1**.**equals**(**bi2**);**  <br>System**.**out**,**println**(**result**);** //false|

|   |   |
|---|---|
|1  <br>2  <br>3|//次幂  <br>BigInteger bi4 **=** bi1**.**pow**(****2****);**  <br>System**.**out**.**println**(**bi4**);** //100|

|   |   |
|---|---|
|1  <br>2  <br>3|//max  <br>BigInteger bi5 **=** bi1**.**max**(**bi2**);**  <br>System**.**out**.**println**(**bi5**);** //10|

注意：在比较大小的时候，它不会创建新的BigInteger对象，而是会将比较对象直接赋值为结果对象，bi1和bi5的地址值一样。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//转为int类型，超出范围数据有误  <br>BigInteger bi6 **=** BigInteger**,**valueOf**(****214748364L****);**  <br>**int** i **=** bi6**.**intValue**();**  <br>System**.**out**.**println**(**i**);** //214748364|

# BigDecimal

## 计算机中的小数

|   |   |   |
|---|---|---|
|类型|占用字节数|总bit位数|
|float|4个字节|32个bit位|
|double|8个字节|64个bit位|

如果一个数字的小数部分超出了类型所能承受的小数部分bit位，那么就会舍弃多出来的部分，导致结果不精确。

## BigDecimal的作用

- 用于小数的精确计算。
- 用来表示很大的小数。

## BigDecimal的方法

|   |   |
|---|---|
|public BigDecimal(double val)|小数类型|
|public BigDecimal(String val)|字符串|
|public static BigDecimal valueOf(double val)|获取BigDecimal对象|

|   |   |
|---|---|
|1  <br>2  <br>3|//通过传递double 类型的小数来创建对象  <br>BigDecimal bd1 **=** **new** BigDecimal**(****0.01****);**  <br>BigDecimal bd2 **=** **new** BigDecimal**(****0.09****);**|

注意：这种方式有可能是不精确的，所以不建议使用。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|//通过传递字符串表示的小数来传递对象  <br>BigDecimal bd3 **=** **new** BigDecimal**(**"0.01"**);**  <br>BigDecimal bd4 **=** **new** BIgDecimal**(**"0,09"**);**  <br>System**.**out**.**println**(**bd3**);** //0.01  <br>System**.**out**.**println**(**bd4**);** //0.09|

|   |   |
|---|---|
|1  <br>2  <br>3|//通过静态方法获取对象  <br>BigDecimal bd6 **=** BigDecimal**.**valueOf**(****10.0****);**  <br>System**.**out**.**println**(**bd6**);** //10.0|

注意：

1. 如果要表示的数字不大，没有超出double 的取值范围，建议使用静态方法。
2. 如果要表示的数字比较大，超出了double 的取值范围，建议使用构造方法。
3. 如果我们传递的是0 ~ 10之间的整数，包含0，包含10，那么方法会返回已经创建好的对象，不会重新new 。

## BigDecimal的使用

|   |   |
|---|---|
|方法名|说明|
|public static BigDecimal valueOf(double val)|获取对象|
|public BigDecimal add(BigDecimal val)|加法|
|public BigDecimal subtract(BigDecimal val)|减法|
|public BigDecimal multiply(BigDecimal val)|乘法|
|public BigDecimal divide(BigDecimal val)|除法|
|public BigDecimal divide(BIgDecimal val, 精确几位, 舍入模式)|除法|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|//加法  <br>BigDecimal bd1 **=** BigDecimal**.**valueOf**(****10.0****);**  <br>BigDecimal bd2 **=** BigDecimal**.**valueOf**(****2.0****);**  <br>BigDecimal bd3 **=** bd1**.**add**(**bd2**);**  <br>System**.**out**.**println**(**bd3**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//减法  <br>BigDecimal bd4 **=** bd1**.**subtract**(**bd2**);**  <br>System**.**out**.**println**(**bd4**);** //8.0|

|   |   |
|---|---|
|1  <br>2  <br>3|//乘法  <br>BigDecimal bd5 **=** bd1**.**multiply**(**bd2**);**  <br>System**.**out**.**println**(**bd5**);** //20.00|

|   |   |
|---|---|
|1  <br>2  <br>3|//除法  <br>BigDecimal bd6 **=** bd1**.**divide**(**bd2**,** **2****,** RoundingMode**.**HALF_UP**);**  <br>System**.**out**.**println**(**bd6**);** //5.00|

注意：在除法中，"2"需要保留的小数位，“RoundingMode.HALF_UP”指四舍五入。
 
# 正则表达式

正则表达式的作用

- 校验字符串是否满足规则。
- 在一段文本中查找满足要求的内容。

## 字符类（只匹配一个字符）

|   |   |
|---|---|
|[abc]|只能是a,b,c|
|[^abc]|除了a,b,c之外的任何字符|
|[a-zA-Z]|a到z A到Z，包括（范围）|
|[a - d[m - p]]|a 到 d，或m 到 p|
|[a -z && [def]]|a - z和def的交集。为：d,e,f|
|[a - z && [^bc]]|a - z和非bc的交集。（等同于[ad - z]）|
|[a - z && [^m - p]]|a 到 z和除了m到p的交集。（等同于[a - lq - z]）|
 
## 预定义字符（只匹配一个字符）

|   |   |
|---|---|
|.|任何字符|
|\d|一个数字：[0 - 9]|
|\D|非数字：[^0 - 9]|
|\s|一个空白字符：[\t\n\x0B\f\r]|
|\S|非空白字符：[^\s]|
|\w|[a - zA - Z_0 - 9]英文、数字、下划线|
|\W|[^\W]一个非单词字符|
 
## 数量词

|   |   |
|---|---|
|X?|X，一次或零次|
|X*|X，零次或多次|
|X+|X，一次或多次|
|X{n}|X，正好n次|
|X{n,}|X，至少n次|
|X{n,m}|X，至少n但不超过m次|
|{?!}|忽略后面字符的大小写|

## 爬虫

本地爬虫  
Pattern：表示正则表达式  
Matcher：文本匹配器，作用按照正则表达式的规则取读取字符串，从头开始读取。在大串中去找符合匹配规则的子串。

|   |   |
|---|---|
|1  <br>2|**import** java**.**util**.**regex**.**Matcher**;**  <br>**import** java**.**util**.**regex**.**Pattern**;**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8|//获取正则表达式的对象  <br>Pattern p **=** Pattern**.**compile**(**"正则表达式"**);**  <br>//获取文本匹配器的对象  <br>Matcher m **=** p**.**matcher**(**"文本"**);**  <br>//检查是否匹配到对象  <br>**boolean** b **=** m**.**find**();**  <br>String s **=** m**.**group**();**  <br>System**.**out**.**println**(**s**);**|

注意：

- m.find()在第一次检测到文本对应的正则表达式时，在返回treu的同时，就会获取对应本地字符串的起始索引和结束索引 + 1，这是因为底层subString(起始索引，结束索引)字符串截取函数的调用（注意：这里的截取函数是包左不包右，所以在获取结束索引时就会 + 1）。
- 在之后的m.find()，会继续从检测第一次检测到结果的后面开始检测，直至将文本检测完毕为止。

网站爬虫

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|//创建一个URL对象  <br>URL url **=** **new** URL**(**"网站地址"**);**  <br>//连接网站  <br>URLConnection conn **=** url**.**openConnection**();**  <br>//创建一个对象去读取网络中的数据  <br>BufferedReader br **=** **new** BufferedReader**(****new** InputStreamReader**(**conn**.**getInputStream**));**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12|String line**;**  <br>String regex **=** "正则表达式"**;**  <br>Pattern p **=** Pattern**.**compile**(**regex**);**  <br>//在读取的时候每一次读一行  <br>**while** **((**line **=** br**.**readLine**() !=** **null****)) {**  <br>//拿着文本匹配器的对象matcher按照pattern的规则去读取当前的这一行信息  <br>Matcher m **=** p**.**matcher**(**line**);**  <br>**while** **(**m**.**find**()) {**  <br>System**.**out**.**println**(**m**.**group**());**  <br>**}**  <br>**}**  <br>br**.**close**();**|

## 带条件的爬取数据

|   |   |
|---|---|
|1|String str1 **=** "Java(?=8\|11\|17)"**;**|

注意：“？”理解为前面的数据Java。“=”表示在Java后面要跟随的数据。但是在获取的时候，只获取前半部分。

|   |   |
|---|---|
|1|String str2 **=** "((?i)Java)(?:8\|11\|17)"**;**|

注意：“:”表示在Java后面要跟随的数据。但是在获取的时候，会获取所有数据。“(?i)”表示就是忽略“Java”的大小写。

|   |   |
|---|---|
|1|String str3 **=** "((?i)Java)(?!8\|11\|17)"**;**|

注意：“?!”表示获取数据时，不需要获取含有跟随的数据。

## 贪婪爬取和非贪婪爬取

贪婪爬取：在爬取数据的时候尽可能的多获取数据。  
非贪婪爬取：在爬取的时候尽可能的少获取数据。  
注意：Java当中，默认的就是贪婪爬取，如果在数量词+的后面加上问号，那么此时就是非贪婪爬取。

|   |   |
|---|---|
|1|String str **=** "ab+?"**;**|

## 正则表达式在字符串方法的使用

|   |   |
|---|---|
|方法名|说明|
|public Boolean matches(String regex)|判断字符串是否满足正则表达式的规则|
|public String replaceAll(String regex, String newStr)|按照正则表达式的规则进行替换|
|public String[] split(String regex)|按照正则表达式的规则切割字符串|
 
|   |   |
|---|---|
|1  <br>2|String s **=** "奥特曼123abc怪兽"**;**  <br>String result1 **=** s**.**replaceAll**(**"[**\\**w&&[^_]]"**,** "vs"**);**|

将字符串中的“123abc”替换成“vs”。  
注意：  
方法在底层跟之前一样也会创建文本解析器的对象。然后从头开始去读取字符串中的内容，只要有满足的，那么就用第二个参数去替换。
 
|   |   |
|---|---|
|1|String**[]** arr **=** s**.**split**(**"[**\\**w&&[^_]]+"**);**|

方法在底层跟之前一样也会创建文本解析器的对象。然后从头开始去图区字符串中的内容，只要有满足的，那么就用字符串数组去接收截取下来的字符串，需要将数组进行遍历。  
**分组**（分组就是一个小括号）  
注意：￼每组时有组号的，也就是序号。

- 规则1：从1开始，连续不间断。
- 规则2：以左括号为基准，最左边的是第一组，其次为第二组，以此类推。

捕获数组就是把这一组的数据捕获出来，在用一次。  
\\ ：表示把第X组的内容再出来用一次。

## 捕获分组

后续还要继续使用本组的数据。  
正则内部使用：\\组号  
正则外部使用：$组号
 
|   |   |
|---|---|
|1|str**.**replace**(**"(.)**\\**1+"**,** "$1"**);**|

注意：$1表示把正则表达式中第一组的内容，再拿出来用。

## 非捕获分组

分组之后不需要再用本组数据，仅仅是把数据括起来。

|   |   |   |
|---|---|---|
|符号|含义|举例|
|(?:正则)|获取所有|Java(?:8\|11\|17)|
|(?=正则)|获取前面部分|Java(?=8\|11\|17)|
|(?!正则)|获取不是指定内容的前面部分|Java(?!8\|11\|17)|

非捕获分子不能使用\\组号来进行调用。它是不占组号的。

# JDK7前时间相关类

|   |   |
|---|---|
|Data|时间|
|SimpleDataFormat|格式化时间|
|Calendar|日历|

## 时间的相关知识点

全时间的时间有一个统一的计算标准。  
原子钟：利用铯原子的震动的频率计算出来的时间，作为世界标准时间（UTC）。  
世界标准时间（格林威治标准时间GMT），目前世界标准时间（UTC）已经替换为：原子钟。  
中国标准时间：世界标准时间 + 8小时。  
时间单位换算： 1秒 = 1000毫秒  
1毫秒 = 1000微妙  
1微妙 = 1000纳秒

## Date时间类

Date类是一个JDK写好的Javabean类，用来描述时间，精确到毫秒。  
利用空参构造创造的对象，默认表示系统当前时间。  
利用有参构造创建的对象，表示指定的时间。

|   |   |
|---|---|
|public void setTime(long time)|设置/修改毫秒值|
|public void getTime()|获取时间对象的毫秒值|
 
## SimpleDateFormat类作用

- **格式化：**把时间变成我们喜欢的格式。
- **解析：**把字符串表示的时间变成Date对象。

**simpleDateFormat****类**

|   |   |
|---|---|
|构造方法|说明|
|public SimpleDateFormat()|构造一个SimpleDateFormat，使用默认格式|
|public SimpleDateFormat(String pattern)|构造一个SimpleDateFormat，使用指定的格式|
 
|   |   |
|---|---|
|常用方法|说明|
|public final String format(Date date)|格式化（日期对象 -\> 字符串）|
|public Date parse(String source)|解析（字符串 -\> 日期对象）|

|   |   |
|---|---|
|1|SimpleDateFormat sdf **=** **new** SimpleDateFormat**(**"yyyy年MM月dd日 HH::mm::ss EE"**);**|

## Calendar类

- Calendar代表了系统当前时间的日历对象，可以单独修改，获取时间中的年，月，日。
- **细节：**Calendar是一个抽象类，不能直接创建对象。

**获取****Calendar****日历对象的方法**

|   |   |
|---|---|
|方法名|说明|
|public staic Calendar getInstance()|获取当前时间的日历对象|

**Calendar****常用方法**

|   |   |
|---|---|
|方法名|说明|
|public final Date getTime()|获取日期对象|
|public final setTime(Date date)|给日历设置日期对象|
|public long getTimeInMillis()|拿到时间毫秒值|
|public void setTimeInMillis(long millis)|给日历设置时间毫秒值|
|public int get(int field)|取日历中的某个字段信息|
|public void set(int field, int value)|修改日历的某个字段信息|
|public void add(int field, int amount)|为某个字段增加/减少指定的值|

获取日历对象

|   |   |
|---|---|
|1|Calendar c **=** Calendar**.**getInstance**();**|

注意：Calendar是一个抽象类，不能直接new，而是通过静态方法获取到子类对象。  
底层原理：

- 会根据系统的不同时区来获取不同的日历对象，默认是当前时间。

会把时间中的纪元，年，月，日，时，分，秒，星期，等等的都放到一个数组当中。

|   |   |
|---|---|
|0|纪元|
|1|年YEAR|
|2|月MONTH|
|3|一年中的第几周|
|4|一个月中的第几周|
|5|一个月中的第几天DAY_OF_MONTH|

- 月份：范围0 - 11 如果获取出来的是0，那么实际上是1月。

星期：星期日是一周中的第一天。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//修改日历的时间  <br>Date d **=** **new** Date**(****0L****);**  <br>c**.**setTime**(**d**)****；**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//get获取日期中的某个字段信息  <br>**int** year **=** c**.**get**(****1****);**  <br>**int** month **=** c**.**get**(****2****)** **+ 1****;**  <br>**int** date **=** c**.**get**(****5****);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//修改日历的某一字段信息  <br>c**.**set**(**Calendar**.**YEAR**,** **2000****);**  <br>c**.**set**(**Calendar**.**MONTH**,** **11****);**|

注意：在Calendar.MONTH中12代表的是月份中的13，因为日历中没有13月份，所以它会将年份向前进1。

|   |   |
|---|---|
|1  <br>2  <br>3|//add为某个字段增加/减少指定的类  <br>c**.**add**(**Calendar**.**MONTH**,** **1****);**  <br>c**.**add**(**Calendar**.**MONTH**, -****1****);**|

# JDK8新增时间相关类

## JKD8安全层面

JDK7：多线程环境下会导致数据安全的问题。  
JDK8：时间日期对象都是不可变的，解决了这个问题。

## Date类

**Zoneld****时区**

|   |   |
|---|---|
|方法名|说明|
|static Set\<String\> getAvailableZoneIds()|获取Java中支持的所有时区|
|static ZoneId systemDefault()|获取系统默认时区|
|static ZoneId of(String zoneId)|获取一个指定时区|

|   |   |
|---|---|
|1  <br>2  <br>3|//获取所有的时区名称  <br>Set**\<**String**\>** zoneIds **=** ZoneId**.**getAvailableZoneIds**();**  <br>System**.**out**.**println**(**zoneIds**.**size**());** //600|

|   |   |
|---|---|
|1  <br>2  <br>3|//获取当前系统的默认时区  <br>ZoneId zoneId **=** ZoneId**.**systemDefault**();**  <br>System**.**out**.**prontln**(**zoneId**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//获取指定的时区  <br>ZoneId zoneId1 **=** ZoneId**.**of**(**"Asia/Pontianak"**);**  <br>System**.**out**.**println**(**zoneId1**);**|

**Instant****时间戳**

|   |   |
|---|---|
|方法名|说明|
|static Instant now()|获取当前时间的Instant对象（标准对象）|
|static Instant ofXxxx(long epochMilli)|根据（秒/毫秒/纳秒）获取Instant对象|
|ZonedDateTime atZone(ZoneId zone)|指定时区|
|boolean isXxx(Instant otherInstant)|判断系列的方法|
|Instant minusXxx(long millisToSubtract)|减少时间系列的方法|
|Instant plusXxx(long millisToSubtract)|增加时间系列的方法|

|   |   |
|---|---|
|1  <br>2  <br>3|//获取当前时间的Instant对象（标准时间）  <br>Instant now **=** Instant**.****new****();**  <br>System**.**out**.**println**(**now**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//根据（秒/毫秒/纳秒）获取Instant对象  <br>Instamt instant1 **=** Instant**.**ofEpochMilli**(****0L****);**  <br>System**.**out**.**println**(**instant1**);**|

|   |   |
|---|---|
|1  <br>2|Instant instant2 **=** Instant**.**ofEpochSecond**(****1L****);** //秒  <br>System**.**out**.**println**(**instant2**);**|

|   |   |
|---|---|
|1  <br>2|Instant instant3 **=** Instant**.**ofEpochSecond**(****1L****,** **1000000000L****);** //秒， 纳秒  <br>System**.**out**.**println**(**instant3**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//指定时区  <br>ZonedDateTime time **=** Instant**.**now**().**atZone**(**ZoneId**.**of**(**"Asia/Shanghai"**));**  <br>System**.**out**.**println**(**time**);**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|//isXxx判断  <br>Instant instant4 **=** Instant**.**ofEpochMilli**(****0L****);**  <br>Instant instant5 **=** Instant**.**ofEpochMilli**(****1000L****);**  <br>**boolean** result1 **=** instant4**.**isBefore**(**instant5**);**  <br>System**.**out**.**println**(**result1**);** //true|

|   |   |
|---|---|
|1  <br>2|**boolean** result2 **=** instant4**.**isAfter**(**instant5**);**  <br>System**.**out**.**println**(**result5**);** //false|

**ZoneDateTime****带时区的时间**

|   |   |
|---|---|
|方法名|说明|
|static ZonedDateTime now()|获取当前时间的ZonedDateTime对象|
|static ZonedDateTime ofXxx(…)|获取指定时间的ZonedDateTime对象|
|ZonedDateTime withXxx(时间)|修改时间系列的方法|
|ZonedDateTime minusXxx(时间)|减少时间系列的方法|
|ZonedDateTime plusXxx(时间)|增加时间系列的方法|

|   |   |
|---|---|
|1  <br>2  <br>3|//获取当前时间对象（带时区）  <br>ZonedDateTime now **=** ZonedDateTime**.**now**();**  <br>System**.**out**.**println**(**now**);**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//获取指定的时间对象（带时区）  <br>//年月日时分秒纳秒方式指定  <br>ZonedDateTime time1 **=** ZonedDateTime**.**of**(****2024****,** **10****,** **1****,** **11****,** **12****,** **12****,** **0****,** ZoneId**.**of**(**"Asia/Shanghai"**));**  <br>System**.**out**.**println**(**time1**);**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5|//通过Instant + 时区的方式指定获取时间对象  <br>Instant instant **=** Instant**.**ofEpochMilli**(****0L****);**  <br>ZoneId zoneId **=** ZoneId**.**of**(**"Asia/Shanghai"**);**  <br>ZonedDateTime time2 **=** ZonedDateTime**.**ofInstant**(**instant**,** zoneId**);**  <br>System**.**out**.**println**(**time2**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//withXxx 修改时间系列的方法  <br>ZonedDateTime time3 **=** time2**.**withYear**(****2000****);**  <br>System**.**out**.**println**(**time3**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//减少时间  <br>ZonedDateTime time4 **=** time3**.**minusYears**(****1****);**  <br>System**.**out**.**println**(**time4**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//增加时间  <br>ZonedDateTime time5 **=** time4**.**plusYears**(****1****);**  <br>System**.**out**.**println**(**time5**);**|

注意：  
JDK8新增的时间对象都是不可变的。如果我们修改了，减少了，增加了时间。那么调用这是不会发生改变的，产生一个新的时间。  
**DateTimeFormatter****用于时间的格式化和解析**

|   |   |
|---|---|
|方法名|说明|
|static DateTimeFormatter ofPattern(格式)|获取格式对象|
|static format(时间对象)|按照指定方式格式化|

|   |   |
|---|---|
|1  <br>2|//获取时间对象  <br>ZonedDateTime time **=** Instant**.**now**().**atZone**(**ZoneId**.**of**(**"Asia/Shanghai"**));**|

|   |   |
|---|---|
|1  <br>2|//解析/格式化器  <br>DateTimeFormatter dtf1 **=** DateTimeFormatter**.**ofPattern**(**"yyyy-MM-dd HH:mm:ss EE a"**);**|

|   |   |
|---|---|
|1  <br>2|//格式化  <br>System**.**out**.**println**(**dtf1**.**format**(**time**));**|
 
## LocalDate、LocalTime、LocalDateTime

|   |   |
|---|---|
|方法名|说明|
|static XXX now()|获取当前时间的对象|
|static XXX of()|获取指定时间的对象|
|get开头的方法|获取日历中的年、月、日、时、分、秒等信息|
|isBefore, isAfter|比较两个LocalDate|
|with开头的|修改时间系列的方法|
|minus开头的|减少时间系列的方法|
|plus开头的|增加时间系列的方法|

|   |   |
|---|---|
|1  <br>2  <br>3|//获取当前时间的日历对象（包含 年月日）  <br>LocalDate nowDate **=** LocalDate**.**now**();**  <br>System**.**out**.**println**(**nowDate**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//获取指定的时间的日历对象  <br>LocalDate ldDate **=** LocalDate**.**of**(****2023****,** **1****,** **1****);**  <br>System**.**out**.**println**(**ldDate**);**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11|//get系列方法获取日历中的每一个属性值  <br>**int** year **=** ldDate**.**getYear**();**  <br>**int** month **=** ldDate**.**getMonthValue**();**  <br>Month m **=** ldDate**.**getMonth**();**  <br>System**.**out**.**println**(**m**);**  <br>System**.**out**.**println**(**m**.**getValue**);**  <br>**int** day **=** ldDate**.**getDayOfMonth**();**  <br>**int** dayOfYear **=** laDate**.**getDayOfYear**();**  <br>DayOfWeek dayOfWeek **=** ldDate**.**getDayOfDate**();**  <br>System**.**out**.**println**(**dayOfWeek**);**  <br>System**.**out**.**println**(**dayOfWeek**.**getValue**());**|

|   |   |
|---|---|
|1  <br>2  <br>3|//is开头的方法表示判断  <br>System**.**out**.**println**(**ldDate**.**isBefore**(**ldDate**));**  <br>System**.**out**.**println**(**ldDate**.**isAfter**(**ldDate**));**|

|   |   |
|---|---|
|1  <br>2  <br>3|//with开头的方法表示修饰，只能修改年月日  <br>LocalDate withLocalDate **=** ldDate**.**withYear**(****2000****);**  <br>System**,**out**.**println**(**withLocalDate**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//minus开头的方法表示减少，只能减少年月日  <br>LocalDate minusLocalDate **=** ldDate**.**minusYear**(****1****);**  <br>System**.**out**.**println**(**minusLocalDate**);**|

|   |   |
|---|---|
|1  <br>2  <br>3|//plus开头的方法表示增加，只能增加年月日  <br>LocalDate plusLocalDate **=** ldDate**.**plusYear**(****1****);**  <br>System**.**out**.**println**(**plusLocalDate**);**|

## 工具类

**Duration****、****Period****、****ChronoUnit**

|   |   |
|---|---|
|**Duration**|用于计算两个“时间”间隔（秒，纳秒）|
|**Period**|用于计算两个“日期”间隔（年、月、日）|
|**ChronoUnit**|用于计算两个“日期”间隔|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9|LocalDate today **=** LocalDate**.**now**();**  <br>LocalDate birthDate **=** LocalDate**.**of**(****2000****,** **1****,** **1****);**  <br>Period period **=** Period**.**between**(**birthDate**,** today**);** //today - birthDate  <br>System**.**out**.**println**(**period**);** //PYearMonthDay  <br>System**.**out**.**println**(**period**.**getYear**);**  <br>System**.**out**.**println**(**period**.**getMonth**);**  <br>System**.**out**.**println**(**period**.**getDay**);**<br><br>  <br><br>System**.**out**.**println**(**period**.**toTotalMonths**());**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9|LocalDateTime today **=** LocalDateTime**.**now**();**  <br>LocalDateTime birthDate **=** LocalDateTime**.**of**(****2000****,** **1****,** **1****,** **0****,** **00****,** **00****);**<br><br>  <br><br>Duration duration **=** Duration**.**between**(**birthDate**,** today**);** //today - birthDate  <br>System**.**out**.**println**(**duration**.**toDays**());**  <br>System**.**out**.**println**(**duration**.**toHours**());**  <br>System**.**out**.**println**(**duration**.**toMinutes**());**  <br>System**.**out**.**println**(**duration**.**toMillis**());**  <br>System**.**out**.**println**(**duration**.**toNanos**());**|

|   |   |
|---|---|
|1|ChronoUnit chronoUnit **=** ChronoUnit**.**between**(**birthDate**,** today**);** //today - birthDate|
    
# 包装类

用一个对象，把基本数据类型给包起来。

## 获取Integer对象的方式

|   |   |
|---|---|
|方法名|说明|
|public Integer(int value)|根据传递的整数创建一个Integer对象|
|public Integer(String s)|根据传递的字符串创建一个Integer对象|
|public static Integer valueOf(int i)|根据传递的整数创建一个Integer对象|
|public static Integer valueOf(String s)|根据传递的字符串创建一个Integer对象|
|public static Integer valueOf(String s, int radix)|根据传递的字符串和进制创建一个Integer对象|

|   |   |
|---|---|
|1  <br>2  <br>3|//利用构造方法获取Integer的对象（JDK5以前的方法）  <br>Integer i1 **=** **new** Integer**(****1****);**  <br>Integer i2 **=** **new** Integer**(**"1"**);**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//利用静态方法获取（JDK5以前的方法）  <br>Integer i3 **=** Integer**.**valueOf**(****1****);**  <br>Integer i4 **=** Integer**.**valueOf**(**"1"**);**  <br>Integer i5 **=** Integer**.**valueOf**(**"123"**,** **8****);**|

底层原理：￼因为在实际开发中，-128 ~127之间的数据，用得比较多。如果每次使用都是new对象，那么太浪费内存了。所以，提前把这个范围之内的每一个数据都创建好对象。如果要用到了不会创建新的，而是返回已经创建好的对象。  
在JDK5的时候提出了一个机制：自动装箱和自动拆箱  
自动装箱：把基本数据类型会自动的变成其对应的包装类。  
自动拆箱：把包装类自动的变成其对象的基本数据类型。

|   |   |
|---|---|
|1  <br>2  <br>3|Integer i1 **=** **10****;**  <br>Integer i2 **=** **new** Integer**(****10****);**  <br>**int** i **=** i2**;**|

在底层，此时还会去自动调用静态方法valueOf得到一个Integer对象，只不过这个动作不需要我们自己去操作了。  
在JDK5以后，int和Integer可以看看作是一个东西，因为在内部可以自动转化。

## Integer成员方法

|   |   |
|---|---|
|方法名|说明|
|public static String toBinaryString(int i)|得到二进制|
|public static String toOctalString(int i)|得到八进制|
|public static String toHexString(int i)|得到十六进制|
|public static int parseInt(String s)|将字符串类型转成int类型的整数|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4|//把整数转成二进制，八进制，十六进制  <br>String str1 **=** Integer**.**toBinaryString**(****100****);**  <br>String str2 **=** Integer**.**toOctalString**(****100****);**  <br>String str3 **=** Integer**.**toHexString**(****100****);**|

|   |   |
|---|---|
|1  <br>2|//将字符串类型的整数转成int类型  <br>**int** i **=** Integer**.**parseInt**(**"123"**);**|

注意：  
强类型语言：Java是一种强类型语言，每种数据在Java中都有各自的数据类型。在计算的时候，如果不是同一种数据类型，是无法直接计算的。

1. 在类型转换的时候，括号中的参数只能是数字不能是其他，否则代码会报错。
2. 八种包装类当中，除了Character都有对应的parseXxx的方法，进行类型转换。