---
tags:
  - knowledge
introduction: Python 基础
start_date: 2026-10-15
---
# 1 环境安装

Python 官网地址：[Welcome to Python.org](https://www.python.org/)  

> 1. 勾选 `Use admin privileges when installing py.exe`。  
> 2. 勾选 `Add python.exe to PATH`。

Pycharm 官网地址：[PyCharm，您需要的唯一 Python IDE](https://www.jetbrains.com/zh-cn/pycharm/)  
傻瓜式安装即可。

PyCharm 创建新项目“python_basic”时，在项目根目录下面会出现 `.idea`、`.venv` 两个文件夹。  
`.idea`：存放的是 PyCharm 的一些配置文件。  
`.venv`：存放的是 PyCharm 当前项目的虚拟环境。  
## 1-1 快捷键

```vtable
{"rows":[[{"t":"&lt;b&gt;快捷键&lt;/b&gt;","rs":1,"cs":1},{"t":"&lt;b&gt;对应操作&lt;/b&gt;","rs":1,"cs":1}],[{"t":"<code>Ctrl + Alt L</code>","rs":1,"cs":1},{"t":"代码格式化","rs":1,"cs":1}],[{"t":"<code>Ctrl + /</code>","rs":1,"cs":1},{"t":"行注释（可选中多行）","rs":1,"cs":1}],[{"t":"<code>Ctrl + C</code>","rs":1,"cs":1},{"t":"复制当前行 / 复制选定的代码","rs":1,"cs":1}],[{"t":"<code>Ctrl + D</code>","rs":1,"cs":1},{"t":"重复当前行 / 重复选定的代码","rs":1,"cs":1}],[{"t":"<code>Ctrl + Z</code>","rs":1,"cs":1},{"t":"撤销","rs":1,"cs":1}],[{"t":"<code>Ctrl + Y</code>","rs":1,"cs":1},{"t":"删除当前行 / 反撤销（重做）","rs":1,"cs":1}],[{"t":"<code>Ctrl + X</code>","rs":1,"cs":1},{"t":"复制当前行 / 剪切选定的代码","rs":1,"cs":1}],[{"t":"<code>Ctrl + = / -</code>","rs":1,"cs":1},{"t":"展开 / 折叠当前代码块","rs":1,"cs":1}],[{"t":"<code>Ctrl + Backspace / Delete</code>","rs":1,"cs":1},{"t":"向前 / 向后删除一个单词","rs":1,"cs":1}],[{"t":"<code>Ctrl + Shift + 上箭头/下箭头</code>","rs":1,"cs":1},{"t":"将当前行上移 或 下移","rs":1,"cs":1}],[{"t":"`Ctrl + F / R`","rs":1,"cs":1},{"t":"查找 / 替换","rs":1,"cs":1}],[{"t":"`Tab / Shift + Tab`","rs":1,"cs":1},{"t":"缩进 / 反向缩进","rs":1,"cs":1}],[{"t":"`Shift + Enter`","rs":1,"cs":1},{"t":"换行（光标不在结尾处也可换行）","rs":1,"cs":1}],[{"t":"`Ctrl + P`","rs":1,"cs":1},{"t":"查看方法传参","rs":1,"cs":1}],[{"t":"`Shift + Esc`","rs":1,"cs":1},{"t":"关闭命令行","rs":1,"cs":1}]]}
```


# 2 Python 核心基础

## 2-1 字面量
1. 所谓**字面量**，就是直接写在代码中的**具体值**。
2. Python 的字符串中可以包含**任意字符**，且必须使用**引号**包起来。
3. 字符串的引号，可以是：**单**引号、**双**引号、**三个单**引号、**三个双**引号。
4. 写在 Python 文件**头部的**字符串，会被自动识别成 **docstring**（文档字符串）
5. 文档字符串的主要作用是：对当前 Python 文件进行一些**说明**，且文档字符串必须用**三个双引号**。

\# 2 变量  

``` python
print("张三的体重是", 65.2)  # 张三的体重是 65.2
```

> 打印语句输出中有一个空格。  

在 Python 中，变量其实就是一个**代号**，用来和某个值建立**绑定关系**。  
当我们想**读取**或**修改**某个值的时候，可以**通过变量**去完成读取和修改操作。  
之所以叫**变量**，是一位它和某个值的绑定关系，可以**随时改变**。  
语法：`变量名 = 值`。  示例：`name = "张三"`  

``` python
weight = 65.2
print("张三的体重是", weight)  # 张三的体重是 65.2
```

在数学书中，`1 + 1 = 2` 叫**等式**，其含义是：`1 + 1` 是具体的**运算**，`2` 是运算**结果**。  
代码中的 `age = 18` 并**不是等式**，其含义是：把右边的**值**，和左边的**变量**，建立一个**绑定关系**。此操作也叫赋值操作，把 18 这个值吗，赋值给了 qge 这个变量。  
在 Python 中，当一个**新的变量**出现时，他必须**立即**与某个值建立**绑定关系**。  
	变量名不能过于随意，而且要遵守一定·的命名规则。  
\# 3 标识符  
标识符的**命名规则**：
1. 只能包含：**数字**、**字母**、**下划线**，且**不能**以**数字开头**，不能包含**空格**。
2. 标识符**区分大小写**，例如 `Name` 和 `name` 是两个不同的标识符。
3. 标识符**不能**使用**关键字**。
4. 标识符**尽量不要**与内置函数同名。
5. 标识符虽然没有长度限制，但应追求：**简洁清晰**，**具有描述性**。
\# 4 常量  
1. 什么是**常量**，一旦被赋值，就**不希望**被修改的量（区别于变量）。
2. Python 中一般约定使用**全大写变量名**来表示常量，涉及到多个单词时，用**下划线**做分隔。
3. Python 中**没有**强制的常量机制，Python 中所谓的常量，其**本质**其实还是**变量**，只不过我们**约定好**不去修改。
\# 5 注释  
1. **注释**是对代码的**备注**和**解释**，在代码执行时，通常不起任何作用。
2. 注释的分类：
	1. 单行注释：`#` 后的一行内容，会被视为注释。
	2. 多行注释：使用**三个单引号**，或**三个引号**的方式编写。
	3. 文件编码注释：写在 Python 文件开头，用于指定当前文件的**字符编码**。

``` python
#coding=utf-8
```

> 备注：Python 中其实**并没有**真正的多行注释语法，上述方式编写的多行注释，本质是一个字符串字面量。

\# 6 字符编码  
1. `utf-8` 又称万国码，全球语言通吃，可以对任意语言进行编码。
2. Python3 中默认的编码方式是 `utf-8`，Python3 中无需编写文件编码注释。
\# 7 数据类型  

```vtable
{"rows":[[{"t":"<b>类型名称</b>","rs":1,"cs":1},{"t":"<b>英文名</b>","rs":1,"cs":1}],[{"t":"字符串","rs":1,"cs":1},{"t":"string","rs":1,"cs":1}],[{"t":"整型","rs":1,"cs":1},{"t":"int","rs":1,"cs":1}],[{"t":"浮点型","rs":1,"cs":1},{"t":"float","rs":1,"cs":1}]]}
```

> Python 中可以使用 `type()`，来查看数据类型。  
> 注意：在 Python 中：**变量无**类型，**数据有**类型。  

\# 8 整型  
所谓整型，就是没有小数点的数字，可以是正数，也可以是负数，也可以是 0.  

``` python
age = 18
temp = -15
score = 0
```

当数很大时，我们可以使用下划线将数字进行分组，来让数字变得更易读。  

``` python
salary = 300_000
house_price = 3_200_000
graduates = 12_000_000
```

Python 中整数的上限值，取决于执行代码的计算机的内存和处理能力。  

> 在 `print` 打印数字时，内部会把数字转换成字符串，再打印。Python 中数字在转换字符串的过程中，默认的限制是：数字不能超过 4300 位。  

\# 9 浮点数  

``` python
# 浮点型就是带有小数点的数字。
weight = 65.2
balance = 1425.58
out_temp = -25.2
price = 120.0

# 浮点型的科学计数法表示。
speed_of_sound = 3.4e+2  # 3.4乘以10的2次方。
world_population = 7.8e9  # 7.8乘以10的9次方。
distance_sun_earth = 1.496E8  # 1.496乘以10的8次方。
speed_of_light = 2.998E+8  # 2.998乘以10的8次方。

one_ml = 1e-3  # 1乘以10的-3次方。
one_mg = 1E-3  # 1乘以10的-3次方。
```

\# 10 字符串  
### 2-10-1 四种定义方式

``` python
# 单引号和双引号的写法是等价的，二者都不能直接换行（要用圆括号才能换行），单引号用的多。
name1 = 'ProkyHoof'
name2 = "ProkyHoof"

# 三个单引号的写法，可以直接换行，并且可以作为多行注释使用
name3 = '''ProkyHoof'''

# 三个双引号的写法，可以直接换行，也可以作为多行注释使用，还能作为文档字符使用。
name4 = """ProkyHoof"""
```

### 2-10-2 格式化输出
按照预先定义的**格式**，将**变量**或**计算结果**，**插入**到字符串中并输出。  

``` python
name = "张三"
gender = "男"
weight = 65.2
age = 12

# 写法一：直接用加号进行拼接，写起来很麻烦且代码很乱，而且只能是字符串之间拼接。
info1 = "我叫" + name + "我是" + gender + "生"

# 写法二：使用占位符
# %s占位字符串，%f占位浮点数，%i占位整数，%d占位十进制的整数，%s是万能的
info2 = "我叫%s，我是%s生，我的体重是%f，我的年龄是%i" % (name, gender, weight, age)
info2 = "我叫%s，我是%s生，我的体重是%f，我的年龄是%d" % (name, gender, weight, age)
info2 = "我叫%s，我是%s生，我的体重是%s，我的年龄是%s" % (name, gender, weight, age)

# 写法三：使用f-string，是目前Python最推荐的方式。
info3 = f"我叫{name}，我是{gender}生，我的体重是{weight}，我的年龄是{age}"
```

### 2-10-3 占位符精度控制
`%m.ns`：  
`m` 的含义：
1. 字符串的**最小宽度**，位数**不够**会自动使用**空格**补全，位数**小于**字符串长度则**不起作用**。
2. **正数**是**右**对齐，**负数**是**左**对齐。

`.n` 的含义：**精度**控制，**最多**输出 **n 个**字符（若 **n 大于**实际字符长度，则不起作用）。  

``` python
name = "张三"
gender = "男"
weight = 65.2
age = 12

info = "我叫%4s，我是%s生，我的体重是%f，我的年龄是%d" % (name, gender, weight, age)
info = "我叫%.1s，我是%s生，我的体重是%f，我的年龄是%d" % (name, gender, weight, age)
```

`%m.nf`：  
`.n` 的含义：**精度**控制，保留 **n 位**小数（n 的**默认**值为 **6**），不够 **0** 来补，截断时会**四舍五入**。  
`m`的含义：  
1. 控制**整体宽度**（整体宽度=**整数**宽度+**小数点**+**小数**宽度）。
2. 位数**不够**空格来补，位数**小于整体宽度**，则自动**失效**。
3. **正数**是**右**对齐，**负数**是**左对齐**。

``` python
info = "我叫%.1s，我是%s生，我的体重是%.1f，我的年龄是%d" % (name, gender, weight, age)
```

`%m.nd`：  
`m` 的含义：  
1. **最小宽度**，位数**不够**会使用**空格**补齐，位数**小于**整数位数，则自动**失效**。
2. **正数**是**右**对齐，**负数**是**左**对齐。

`.n` 的含义：  
1. **精度**控制，含义用 **n 位**显示数字。
2. 位数**不够**用 **0** 来补，位数**小于**整数位，则自动失效。

### 2-10-4 转义字符
是一种在**字符串中**用于表示**特殊含义**的字符组合，通常以**反斜杠**开头，通常用于表示那些在字符串中**不能直接写出**的字符。  

``` python
# 使用 \' 输出 '
print('在Python中，可以使用\'包裹一个字符串')

# 使用 \" 输出 "
print("在Python中，可以使用\"包裹一个字符串")

# 使用 \n 进行换行
print("注册会员需要以下信息：\n姓名\n年龄\n手机号")

# 使用 \\ 输出 \
print("D:\\ProkyHoof")

# 使用 \b 删除前一个字符
print("helloo\b")

# 使用 \r 使光标回到本行开头，覆盖输出
print("67%\r68%")

# 使用 \t 表示水平制表符（让光标跳转到下一个制表位）Pycharm 制表位就是 4 位
print("123\t4".expandtabs(4))
```

> `expandtabs()` 表示使得制表位不论在任何环境下，就是 4 位。  
> 中文占用两位。

\# 11 数据类型转换  
**数据类型转换**：把**一种**类型的数据，变成**另一种**类型。  
为什么要进行数据类型转换：  
1. **用户输入**的内容是都是**字符串**，若需要进行**数学运算**，就必须进行**数据类型转换**。
2. 对**文件**进行**写入操作**时，要将**其他类型**的数据转为**字符串**。
3. 从**数据库**中**读取**出的内容都是**字符串**，若需要进行**数学运算**，也需要**数据类型转换**。

把指定数据转为**字符串**：`str()`  
把指定数据转为**整数**：`int()`  

``` python
int(15.6)  # 不会四舍五入，输出 15
int("79")  # 输出 79
int(" 79 ")  # 输出 79
int(15)  # 输出 15

# 错误案例
int(" 7 9 ")
int("你好")
int("79个")
int("15.6")
```

把指定数据转为**浮点数**：`float()`  

``` python
float(18)
float("15.6")
float(" 5.7 ")
float(14.8)
float("48")

float(" 5. 7 ")
float("你好")
float("5.7元")
float("5.23.12")
```

\# 12 算数运算符  
### 2-12-1 数学运算符


```vtable
{"rows":[[{"t":"运算符","rs":1,"cs":1},{"t":"说明","rs":1,"cs":1},{"t":"示例","rs":1,"cs":1},{"t":"结果","rs":1,"cs":1}],[{"t":"+","rs":1,"cs":1},{"t":"加","rs":1,"cs":1},{"t":"9 + 7","rs":1,"cs":1},{"t":"16","rs":1,"cs":1}],[{"t":"-","rs":1,"cs":1},{"t":"减","rs":1,"cs":1},{"t":"7 - 2","rs":1,"cs":1},{"t":"5","rs":1,"cs":1}],[{"t":"*","rs":1,"cs":1},{"t":"乘","rs":1,"cs":1},{"t":"3 * 4","rs":1,"cs":1},{"t":"12","rs":1,"cs":1}],[{"t":"/","rs":1,"cs":1},{"t":"除","rs":1,"cs":1},{"t":"9 / 6","rs":1,"cs":1},{"t":"1.5","rs":1,"cs":1}],[{"t":"//","rs":1,"cs":1},{"t":"取整数（取整）","rs":1,"cs":1},{"t":"9 // 6","rs":1,"cs":1},{"t":"1","rs":1,"cs":1}],[{"t":"%","rs":1,"cs":1},{"t":"取余（取模）","rs":1,"cs":1},{"t":"9 % 6","rs":1,"cs":1},{"t":"3","rs":1,"cs":1}],[{"t":"**","rs":1,"cs":1},{"t":"指数","rs":1,"cs":1},{"t":"2 ** 3","rs":1,"cs":1},{"t":"8","rs":1,"cs":1}]]}
```

### 2-12-2 赋值运算符

``` python
age = 18
age = age + 1
print(age)
```

### 2-12-3 复合赋值运算符

``` python
# 加法复合运算符
age = 18
age += 1  # 等价于：age = age + 1
print(age)

# 减法复合运算符
age -= 1  # 等价于：age = age - 1
print(age)

# 乘法复合运算符
price = 100
discount = 0.8
price *= discount  # 等价于：price = price * discount
print(price)

# 除法复合运算符
pay = 100
num = 5
pay /= num  # 等价于：pay = pay / num
print(pay)

# 取整赋值运算符
apple = 31
num = 14
apple //= num  # 等价于：apple = apple // num
print(apple)

# 取模赋值运算符
seconds = 336
minutes = 60
seconds %= minutes  # 等价于：seconds = seconds % minutes

# 指数赋值运算符
a = 2
b = 3
a **= b  # 等价于：a = a ** b
```

### 2-12-4 比较运算符

```vtable
{"rows":[[{"t":"运算符","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1}],[{"t":"==","rs":1,"cs":1},{"t":"判断左右两侧是否相等","rs":1,"cs":1}],[{"t":"!=","rs":1,"cs":1},{"t":"判断左右两侧是否不等","rs":1,"cs":1}],[{"t":"&gt;","rs":1,"cs":1},{"t":"判断左侧是否大于右侧","rs":1,"cs":1}],[{"t":"&lt;","rs":1,"cs":1},{"t":"判断左侧是否小于右侧","rs":1,"cs":1}],[{"t":"&gt;=","rs":1,"cs":1},{"t":"判断左侧是否大于等于右侧","rs":1,"cs":1}],[{"t":"&lt;=","rs":1,"cs":1},{"t":"判断左侧是否小于等于右侧","rs":1,"cs":1}]]}
```

``` python
a = 5
b = 7
c = "5"
print(a == c)  # False，数据类型不同
print(a != c)  # True
print(a > b)  # False，大于号左右必须是同一种类型，否则报错
print(a >= b)  # False，大于等于号左右必须是同一种类型，否则报错
print(a < b)  # True
print(a <= b)  # False
```

> 以上这些比较运算符，同样适用于字符串。  
> Python 中**字符串**进行**比较**时，是**依次**比较每个**字符**的 **Unicode 编码**。  
> 注意：Unicode 编码不是 Python 特有的，而是全世界通用的标准。  

Python 中可以使用如下方式进行**字符**与 **Unicode 编码**之间的转化。  
使用 `ord()` 查看字符 Unicode 码。  
使用 `chr()` 将 Unicode 码转为字符。  

``` python
ord("a")  # 97
ord("我")  # 25105
chr(97)  # a
chr(25105)  # 我
```

> 字符串比较：  
> 1. 字符串比较为逐字比较，如果第一个字符比较大小之后，不相等，则直接返回结果 `True` 或 `False`。  
> 2. 字符串如果都相等时，就会比较字符串的长度，长度长就大于，长度小就小于，长度相等就相等。  

### 2-12-5 布尔类型（Boolean）

``` python
a = True
b = False
print(type(a), a)  # bool，True
print(type(b), b)  # bool，False
```

> 布尔类型是 `int` 类型的子类型，底层的本质是用 1 表示 `True`，用 0 表示 `False`。  

``` python
print(int(True))  # 1
print(int(False))  # 0
print(True + True)  # 2
print(True - False)  # 1
print(1 + True)  # 2
print(7 > True)  # True
print(False <= 0)  # True
```

使用 `bool()` 将指定内容转为布尔类型。  

``` python
print(bool(1))  # True
print(bool(0))  # False

# Python中除0意外的任何数，转为布尔值都为True
print(bool(300))  # True
print(bool(-1))  # True

# Python中除空字符意外的任何字符串，转为布尔值都是True
print(bool("ProkyHoof"))  # True
print(bool(""))  # False
```

### 2-12-6 逻辑运算符

```vtable
{"rows":[[{"t":"运算符","rs":1,"cs":1},{"t":"名称","rs":1,"cs":1},{"t":"功能描述","rs":1,"cs":1}],[{"t":"and","rs":1,"cs":1},{"t":"逻辑与","rs":1,"cs":1},{"t":"判断其两侧的值，是否都为True","rs":1,"cs":1}],[{"t":"or","rs":1,"cs":1},{"t":"逻辑或","rs":1,"cs":1},{"t":"判断其两侧的值，是否至少有一个为True","rs":1,"cs":1}],[{"t":"not","rs":1,"cs":1},{"t":"逻辑非","rs":1,"cs":1},{"t":"用于对一个值取反","rs":1,"cs":1}]]}
```

`and` 用于判断其两侧，是否都为 `True`（只要都是 `True`，那就返回 `True`）。

> `and` 具备“逻辑短路”能力。  

``` python
print(False and 3 / 0)  # 3 / 0 一定报错，但是 and 检测到 False 就会直接返回 False
```

> `and` 返回的不一定是布尔值，它返回的是某个参与计算的值本身。  
> 规则：`and` 会先看左边，如果左边是“假”，就直接返回左边，否则返回右边。  
> 备注：若参与 `and` 运算的值不是布尔值，那 Python 会自动转为布尔值，然后再进行逻辑操作。  

``` python
print(2 - 2 and True)  # 0
print("" and True)  # ""
print(True and 8 / 2)  # 4.0
print(3 + 3 and 3 * 4)  # 12
```

`or` 用于判断其两侧，是否至少有一个为 `True`（只要有一个是 `True`，那就返回 `True`）。

> `or` 同样也具备“逻辑短路”的能力。  

``` python
print(True or 3 / 0)  # True
```

> `or` 返回的也不一定是布尔值，它返回的是参与计算的值本身。  
> 规则：`or` 会先看左边，如果左边是“真”，就直接返回左边，否则返回右边。  
> 备注：若参与 `or` 运算的值不是布尔值，那 Python 会自动转为布尔值，然后再进行逻辑操作。  

``` python
print(7 - 2 or False)  # 5
print("你好" or "ProkyHoof")  # "你好"
print(False or 8 / 2)  # 4.0
print(2 - 2 or 3 * 4)  # 12
```

`not` 用于取反。  

> 备注：若参与 `not` 运算的值不是布尔值，那 Python 会自动转为布尔值，然后再进行逻辑操作。  
> `not` 返回的值，一定是布尔值！  

``` python
print(not 0)  # True
print(not 3 > 2)  # False
print(not 9 // 4)  # False
print(not "abc")  # False
```

\# 13 进制  

``` python
# 0b 开头表示二进制
num1 = 0b11001  # 25
# 0o 开头表示八进制
num2 = 0o1034  # 540
# 0x 开头表示十六进制
num3 = 0x1cf  # 463
```

> Python 中所有的非十进制数字，只是代码层面的编写方式，是给程序员看的。  
> Python 再对上面的 `num1`、`num2`、`num3` 进行计算、打印等操作时，会自动将其转为十进制。  

``` python
print(num1 + 1)  # 26
print(str(num2))  # 540
print(num3 > 400)  # True
```

### 2-13-1 Python 中的进制转换

```vtable
{"rows":[[{"t":"写法","rs":1,"cs":1},{"t":"功能","rs":1,"cs":1},{"t":"示例","rs":1,"cs":2},{"t":"","rs":0,"cs":0}],[{"t":"`bin()`","rs":1,"cs":1},{"t":"十进制转二进制字符串","rs":1,"cs":1},{"t":"`bin(25)`  # 0b11001","rs":1,"cs":2},{"t":"","rs":0,"cs":0}],[{"t":"`oct()`","rs":1,"cs":1},{"t":"十进制转八进制字符串","rs":1,"cs":1},{"t":"`oct(540)`  # 0o1034","rs":1,"cs":2},{"t":"","rs":0,"cs":0}],[{"t":"`hex()`","rs":1,"cs":1},{"t":"十进制转十六进制字符串","rs":1,"cs":1},{"t":"`hex(463)`  # 0x1cf","rs":1,"cs":2},{"t":"","rs":0,"cs":0}],[{"t":"`int()`","rs":3,"cs":1},{"t":"其他进制转十进制数字","rs":3,"cs":1},{"t":"二进制转十进制","rs":1,"cs":1},{"t":"`int(\"0b11001\", 2)`  # 25","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"","rs":0,"cs":0},{"t":"八进制转十进制","rs":1,"cs":1},{"t":"`int(\"0o1034\", 8)`  # 540","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"","rs":0,"cs":0},{"t":"十六进制转十进制","rs":1,"cs":1},{"t":"`int(\"0x1cf\", 16)`  # 463","rs":1,"cs":1}]]}
```

> 注意：`bin()`、`oct()`、`hex()` 返回的值类型都是字符串。  

\# 14 输入语句  

``` python
print("请输入你的年龄")
age = input()  # 输入类型都是字符串类型 str
age = int(age)
print(f"你今年的年龄是{age}")
print(f"你明年的年龄是{age + 1}")
input("请输入你的姓名")
```


# 3 流程控制语句

## 3-1 分支
### 3-1-1 单分支

``` python
age = 18
if age >= 18:
	print("你是成年人") 
```

### 3-1-2 双分支

``` python
age = 18
if age >= 18:
	print("你是成年人")
else:
	print("你不是成年人")
```

### 3-1-3 多分支

``` python
age = 18
if age <= 10:
	print("你是幼儿")
elif age <= 18:
	print("你是青少年")
elif age <= 30:
	print("你是青年")
elif age <= 50:
	print("你是中年")
elif age <= 60:
	print("你是中年人")
else:
	print("你是老年")
```

> 分支之间是互斥的。  

### 3-1-4 嵌套分支
e.g. 为长跑俱乐部，设计一个马拉松比赛报名审核程序，具体规则如下：  
1. 参赛年龄必须是：18~45 岁之间。
2. 参赛前必须提交体验报告，否则不能比赛。
3. 比赛结束后，根据会员的等级，领取不同礼物。
	1. 1 级会员礼物为：纪念 T 恤。
	2. 2 级会员礼物为：专业跑鞋。
	3. 3 级会员礼物为：运动耳机。

``` python
age = int(input("请输入你的年龄"))
is_submit_report = int(input("是否提交体检报告（1 表示提交，0 表示未提交）"))
grade = int(input("请输入你的会员等级，等级分别是1，2，3"))
if age >= 18 and age <= 45:  # 简写：18 <= age <= 45
	if is_submit_report == 1:
		if grade == 1:
			print("纪念 T 恤一件")
		elif grade == 2:
			print("专业跑鞋一双")
		elif grade == 3:
			print("运动耳机一副")
	else:
		print("未提交体检报告不能参赛")
else:
	print("不符合年纪要求")
```

\# 2 循环  
### 3-2-1 while 循环

``` python
n = 1
while n <= 10:
	print("我是ProkyHoof")
	n += 1
```

> 1. 循环条件为 `True` 会继续循环，为 `False` 会终止循环。  
> 2. 要设计好循环条件，避免死循环。  

### 3-2-2 while 循环案例
e.g. 模拟一个密室逃脱场景：  
1. 用户必须正确的回答问题，才能“逃脱密室”。
2. 若回答错误，系统就会不断**循环提问**，直到答对为止。
3. 若回答正确，控制台打印逃脱成功，并结束循环。

``` python
print("您现在身处密室，需要正确回答问题之后，才能掏出密室")
riddle = "你是什么人"
answer = "你的心上人"
guess = ""
while guess != answer:
	print(f"问题：{riddle}")
	guess = input("请输入答案")
	if guess == answer:
		print("回答正确，逃脱成功")
	else:
		print("回答失败，请再想想")
```

### 3-2-3 for 循环

``` python
for n in range(10):
	print("hello")
```

`range`：循环范围（此处含义是：循环 10 次，0~9）。  
`n`：当前这次循环，所取出的值。  

> **可迭代对象**中的元素有多少个，循环就执行多少次。  
> 只要不在循环内部修改可迭代对象，`for` 循环通常是不会出现死循环的。  

``` python
# 使用 for 循环便利 range() 所指定的数字范围
n = 0
for n in range(1, 11):
	print(f"第{n}次你好啊")
print(f"我是for循环以外的代码，执行到这里时，循环已经结束了，此时的n是：{n}")
```

如果 `n` 在循环外使用到，建议定义变量 `n`。如果循环外部没有使用，则不需要定义。

``` python
# 使用 for 循环遍历字符串
for m in "ProkyHoof":
	print(m)  # 依次打印字符串
```

``` python
# 演示由于误操作造成的死循环
nums = [1, 2, 3]
for i in nums:  # 死循环
	nums.append(4)
	print(i)
```

### 3-2-4 for 循环案列
e.g. 需求：设计一个字符串加密程序。  

``` python
# 加密代码
text = input("请输入要加密的文字")
secret = ""
for t in text:
	unicode = ord(t)
	secret += chr(unicode + 1)
print(f"经过加密后的内容为：{secret}")

# 解密代码
word = input("请输入要解密的文字")
answer = ""
for w in word:
	unicode = ord(w)
	answer += chr(unicode - 1)
print(f"经过解密后的内容为：{answer}")
```

### 3-2-5 while 和 for 之间的区别

```vtable
{"rows":[[{"t":"`while`","rs":1,"cs":1},{"t":"`for`","rs":1,"cs":1}],[{"t":"条件驱动循环（只要条件为`True`就继续循环）。","rs":1,"cs":1},{"t":"迭代驱动循环（遍历一个**可迭代对象**的每一项。","rs":1,"cs":1}],[{"t":"写法灵活，尤其适合处理不确定循环次数的场景。","rs":1,"cs":1},{"t":"语法简洁，处理可迭代对象的首选，不易发生死循环。","rs":1,"cs":1}],[{"t":"但需要手动维护循环条件，维护不好容易死循环。","rs":1,"cs":1},{"t":"只适合一开始就知道要循环几次的场景。","rs":1,"cs":1}]]}
```

e.g.   
提示用户输入密码，若密码不正确就反复提示，直到密码正确。  while  
遍历字符串“Python”，逐个输出每个字符。  for  
让用户不断输入数字，直到输入的是一个偶数为止。  while  
让用户依次输入 5 个名字，最终把 5 个名字拼接到一起。 for  
### 3-2-6 嵌套循环
e.g. 打印一个为期 30 天的健身计划  

``` python
# for 循环实现
day = 1
for day in range(1, 31):
	print(f"第{day}天")
	for group in range(1, 4):
		print(f"这是第{group}组仰卧起坐")
	print(f"第{day}天任务已完成，明天继续\n")
print(f"为期{day}天的健身任务完成")

# while 循环实现
day = 1
while day < 31:
	print(f"第{day}天")
	group = 1
	while group < 4:
		print(f"这是第{group}组仰卧起坐")
		group += 1
	print(f"第{day}天任务已完成，明天继续\n")
	day += 1
print(f"为期{day - 1}天的健身任务完成")
```

### 3-2-7 九九乘法表

前序知识  
`print` 打印出的结果都会进行换行操作。  

``` python
# 不换行
print("你好", end = "!")
print("猪脚", end = "@")  # 你好!猪脚@
```

``` python
# for 循环实现
for row in range(1, 10):
	for item in range(1, row + 1):
		print(f"{row} * {item} = {row * item}", end = "\t")
	print()
```

### 3-2-8 continue 与 break
`continue`：跳出本次循环剩余语句，随后进入下一次循环。  
`break` ：立即终止循环，不再执行后续循环。  

``` python
for day in range(1, 5):
	print(f"第{day}天")
	print("吃饭")
	if day == 2:
		continue  # 第二天的“睡觉”不会进行打印
	print("睡觉")
	
for day in range(1, 5):
	print(f"第{day}天")
	print("吃饭")
	if day == 2:
		break  # 进行到第二天的“吃饭”，以后的内容不会被打印
	print("睡觉")
```

> `continue` 和 `break` 只会影响所在循环的进行。  

### 3-2-9 综合案例
e.g. 一共 3 个关卡（每个关卡只有一道题），答对进入下一关，3 关都通过则挑战成功。  
1. 答错可重试，每道题都有 3 次回答机会，若 3 次均答错，则挑战失败，游戏自动结束。
2. 如果用户输入为空，则提示重新作答，且不浪费回答机会。
3. 如果用户输入字母 q，则直接退出游戏。

``` python
print("欢迎来到：答题闯关挑战赛（输入 q 可随时退出）")

# 题目与答案
ques1 = "Python 中用于输出的函数是"
ans1 = "print"
ques2 = "Python 中用于表示逻辑“并且”的关键字是"
ans2 = "and"
que3 = "Python 属于编译型还是解释型"
ans3 = "解释型"

# 最多可尝试次数
max_tries = 3
# 总关卡数
total_levels = 3
# 是否处于可游戏状态
is_playing = True

# 根据题目数量开始循环
for level in range(1, total_levels + 1):
	# 打印当前是第几关
	print(f"第{level}关")
	# 取出当前关卡所对应的题目和答案
	if level == 1:
		question, answer = ques1, ans1
	elif level == 2:
		question, answer = ques2, ans2
	elif level == 3:
		question, answer = ques3, ans3
	# 记录当前关卡的尝试次数
	tries = 1
	# 若已经尝试的次数，小于等于最大尝试次数，则进入循环
	while  tries <= max_tries:
		# 想用户提问
		user_input = input(question)
		# 根据用户的输入，来决定做什么
		if user_input == answer:
			print("回答正确\n")
			break
		elif user_input == "":
			print("您的输入为空，请重新作答\n")
			continue
		elif user_input == "q"
			print("你已退出游戏\n")
			is_playing = False
			break
		else:
			# 计算剩余次数
			leave = max_tries - tries
			# 判断是否还有剩余次数
			if leave > 0:
				print(f"回答错误，您还剩{leave}次机会\n")
				tries += 1
				continue
			else:
				print(f"挑战失败，本体的正确答案是：{answer}，游戏结束")
				is_playing = False
	# 每次进入下一关之前，都要看一下is_playing，如果is_playing为False就要结束游戏
	if is_playing == False:  # not is_playing
		break
# 如果到了这里，is_playing的值依然为True，那就意味着用户已经通关了
if is_playing:
	print("恭喜您！全部通关")
```


# 4 函数

## 4-1 概念及分类
### 4-1-1 什么是函数
定义：函数（function）是**组织好**的、可**重复使用**的，用于执行**特定任务**的代码块。  
函数就像是**智能家居**中的**一个场景**，**提前配置**好场景中要**执行的操作**，**呼唤场景**，场景中的操作就会**执行**。  
Python 中的函数是一段**有名字**的**代码块**，**提前编写**好函数中要**执行的代码**，**调用函数**，函数中的代码就会**执行**。  
### 4-1-2 函数的作用
1. **代码复用**；提高代码复用性，减少重复代码。  
2. **结构清晰**：让程序更易读、更易维护。  
3. **模块化开发**：把程序分成若干个小功能，便于团队合作。  

```vtable
{"rows":[[{"t":"分类","rs":1,"cs":1},{"t":"说明","rs":1,"cs":1}],[{"t":"内置函数","rs":1,"cs":1},{"t":"无需任何操作，直接就能使用","rs":1,"cs":1}],[{"t":"模块提供的函数","rs":1,"cs":1},{"t":"需要导入指定的模块后，才能使用","rs":1,"cs":1}],[{"t":"自定义函数","rs":1,"cs":1},{"t":"程序员自己定义的函数（先定义再使用）","rs":1,"cs":1}]]}
```

[内置函数 — Python 3.14.7 文档](https://docs.python.org/zh-cn/3/library/functions.html)  
[6. 模块 — Python 3.14.7 文档](https://docs.python.org/zh-cn/3/tutorial/modules.html)  
[Python 标准库 — Python 3.14.7 文档](https://docs.python.org/zh-cn/3/library/index.html)

\# 2 基本使用
e.g. 定义一个名为 welcome 的函数，函数中**打印两句**欢迎语。  

``` python
# 定义函数
def welcome():
	print("欢迎光临")
	print("这里是Python学习笔记")

# 调用函数（让函数中的代码运行起来）
welcome()
```

`def` 是定义函数的关键字 define。  
`welcome()`：`welcome` 是函数名，`()` 是写参数的地方。
`:` 之后的内容就称为函数体。  

> Python 中的函数必须先定义再调用。  

\# 3 参数的使用  
e.g. 定义一个名为 order 的函数，函数中打印用户的点餐信息。  

``` python
def order(num, dish):
	print(f"您点的是：{num}份{dish}")

order(1, "辣椒炒肉")
order(2, "辣子鸡")
```

`num`、`dish`：形参。  
`1` 、`辣椒炒肉` 、`2`、`辣子鸡`：实参。

> 形参 `num` 与 `dish` 的使用范围，仅限函数内。 
> 实参参数必须与函数中的形参参数保持一致，否则就会报错。  

\# 4 位置参数  
**位置参数**：调用函数时，根据参数在函数定义中出现的顺序，把实参的值依次传递给对应的形参。  

``` python
# 定义函数（接受位置参数）
def greet(name, gender, age, height):
	print(f"我叫{name}，性别{gender}，年龄{age}，身高{height}")

# 调用函数
greet("张三", "男", 18, 172)  # 位置参数
```

> 注意：使用位置参数时，不能跳过某个位置的参数，去给后面的形参赋值。
> 位置参数是按照实参的顺序对形参进行赋值。  

\# 5 关键字参数  
**关键字参数**：调用函数时，通过形参名 = 值的形式传递实参。  

``` python
# 定义函数
def greet(name, gender, age, height):
	print(f"我叫{name}，性别{gender}，年龄{age}，身高{height}")

# 调用函数
greet(name = "张三", gender = "男", age = 18, height = 172)  # 关键字参数
greet("张三", "男", height = 172, age = 18)  # 位置参数与关键字参数混用
```

> 关键字参数无需顺序按照实参的顺序对形参进行赋值。 
> 注意：使用关键字参数时，位置参数必须在关键字参数之前。  

\# 6 限制传参方式  
**具体规则**：`/` 前边只能用**位置**参数，`*` 后面只能用**关键字**参数。  

``` python
# 定义函数（接受位置参数）
def greet(name, /, gender, *, age, height):
	print(f"我叫{name}，性别{gender}，年龄{age}，身高{height}")

# 调用函数
greet("张三", gender = "男", age = 18, height = 172)
greet("张三", "男", height = 172, age = 18)
```

> `/` 和 `*` 同时使用时，`/` 必须在 `*` 的前面。

\# 7 参数默认值  
**参数默认值**：定义函数时，通过形参名 = 值的形式，为参数指定一个默认值。  

``` python
# 定义函数
def greet(name, gender, age, height, msg = "你好"):
	print(f"我叫{name}，性别{gender}，年龄{age}，身高{height}")
	print(f"我想说：{msg}")

# 调用函数
greet("张三", "男", 18, 172)  # msg使用默认值：你好
greet("张三", "男", 18, 172, "hello")  # msg使用hello
```

在调用 `greet` 时：  
* 如果没传 `msg`，那就使用默认值。
* 如果传了 `msg`，那就使用传入的值覆盖默认值。

> 注意：默认参数必须放在必选参数的后面，或者说：某个形参，一旦设置了默认值，那它后面的所有形参，也必须要写默认值。  

\# 8 可变参数  
### 4-8-1 可变位置参数
**定义函数**时，在形参名前加 `*`，可以接收**任意数量**的**位置**参数，并打包成一个**元组**。  

``` python
def test(*args):
	print(args)
```

* `args` 只是一个形参名，arguments，可以**随意更改**。
* `args` 中存放的是：函数调用时，所传入的**所有位置实参**。
* `args` 的**数据类型**是**元组**。

### 4-8-2 可变关键字参数
**定义函数**时，在形参名前加 `**`，可以接收**任意数量**的**关键字**参数，并打包成一个**字典**。  

``` python
def test2(**kwargs):
	print(kwargs)
```

* `kwargs` 只是一个形参名，keyword arguments 可以**随意更改**。
* `kwargs` 中存放的是：函数调用时，所传入的**所有关键字实参**。
* `kwargs` 的**数据类型**是**字典**。

> 可变位置参数、可变关键字参数，可以同时使用，但必须先写可变位置参数。  

``` python
def test3(*args, **kwargs)；
	print(args)
	print(kwargs)
	
test3("张三", "男", age = 18, height = 172)
```

> 可变位置参数、可变关键字参数，也能与其他类型的参数一起使用。  

``` python
def test4(a, b, *args, c = "猪脚", **kwargs):
	print(a)
	print(b)
	print(args)
	print(c)
	print(kwargs)

test4("张三", "男", "抽烟", "喝酒", c = "ProkyHoof", age = 18, height = 172)
```

> 总结  

正确的书写顺序（五段式）  
1. 普通位置参数（如果 `a, b`）——必须写在最前面。
2. 默认值参数（如 `c = 1`）——紧跟在普通参数后面。
3. 可变位置参数（收集剩余的位置参数）（如 `*args`）——只能有一个，放在默认参数后面。
4. 仅限关键字参数（如 `d = 2` 或 `e`）——必须写在 `*args` 后面，调用时只能用 `形参名 = 值` 传参。
5. 可变关键字参数（收集剩余的关键字参数）（如 `**kwargs`）——必须放在最后，且只能有一个。

标准模板：  

``` python
def func(a, b, c = 1, *args, d = 2, **kwargs):
	pass
```

> 有默认值的参数，绝对不能排在“没有默认值的普通参数”前面。  

调用函数时，正确的传递顺序：  
1. 所有位置参数（不带参数名的值）必须写在最前面。
2. 所有关键字参数（带参数名的值）必须跟在所有位置参数的后面。

`*args` 和 `**kwargs` 的“区域隔离原理”  
* `*args` 前面的参数：既可以接受位置传参，也可以接受关键字传参。
* `*args` 后面的参数（仅限关键字参数）：只能接受关键字传参，绝对不能位置传参。无论它带不带默认值，这个限制都存在。

\# 9 特殊的字面量——None  
NoneType 类型：`None`  
1. `None` 是一个特殊的字面量，它表示：空值/无值/无意义。

`msg = None`  
定义了 `msg` 变量，但目前还不知道它的具体类型。  
不写 `None`，写：0 或"或 False 不行吗，最好不写。  
`None` 更中立，更开放，`None` 是不暗示类型的。  
如果确定 `msg` 以后是字符串类型，那就可以写"。  

2. `None` 的类型是 NoneType。
3. `None` 转为布尔值是 `False`。
4. `None` 不能参与数学运算，也不能与字符串拼接。
5. 不给函数设置返回值，函数会默认返回 `None`。

\# 10 返回值  
函数返回值：函数执行完毕后，会把执行结果交给调用者，这个执行结果就是返回值。  
`return` 关键字：`return` 会结束函数执行，并把 `return` 后的值，作为函数的返回值。

``` python
# 定义一个add函数
def add(n1, n2):
	print(f"我收到了：{n1}、{n2}，二者相加是：{n1 + n2}")
	answer = n1 + n2
	return answer
	print("add函数执行完毕")  # 无法执行

# 调用add函数，并用result变量接收其返回值
result = add(100, 200)
```

> 如果一个函数返回值是 `None`，我们也经常说这个函数没有返回值。  

\# 11 全局作用域与局部作用域  
1. 全局作用域：整个 `.py` 文件最外层的范围，就是全局作用域。
2. 局部作用域：函数的内部范围，就是局部作用域。

``` python
# 全局作用域与局部作用域，以及global的使用
a = 100  # 全局变量
b = 200  # 全局变量

def test():
	c = "ProkyHoof"  # 局部变量
	d = "hello"  # 局部变量
	global a = 300
	print("函数中的打印(a)", a)  # 300
	print("函数中的打印(b)", b)  # 200
	print("函数中的打印(c)", c)  # ProkyHoof
	print("函数中的打印(d)", d)  # hello
test()

# print(c)  # 错误
# print(d)  # 错误
```

> 局部作用域和局部变量，会在函数调用时创建，在函数执行结束后销毁。  
> 全局作用域和全局变量，会在程序开始时创建，在程序结束后销毁。  

\# 12 嵌套调用  
嵌套调用：在一个函数的执行过程中，去调用了另外一个函数。  

``` python
def speak(msg):
	print("------")
	print(msg)
	print("------")

def greet(name, msg):
	print(f"我叫{name}，我想说的话在下面：")
	speak(msg)
	print("嗯，我想说的结束了")
	
greet("张三", "你好呀")
```

\# 13 递归调用  
递归调用（简称：递归）：是指函数自己调用自己的一种操作。  

``` python
def welcome():
	print("hello")
	welcome()
	
welcome()
```

``` python
# 从大到小打印
def welcome(n):
	print(f"hello{n}")
	if n > 1:
		welcome(n - 1)

welcome(5)

# 从小到大打印
def welcome(n):
	if n > 1:
		welcome(n - 1)
	print(f"hello{n}")

welcome(5)
```

> **特别注意**：这两段代码在递归时，其实都需要逐层压栈，二者调用深度完全相同，只是打印的时机不同。  

1. 我们之前说“待执行收集器”只是为了大家好理解，其实最准确的说法，其实应该叫：函数调用栈。
2. 每一次递归调用，都会在调用栈里压入对应的信息，因此递归必然涉及到：多次压栈和出栈。

\# 14 递归的应用  
递归的应用举例：使用递归求一个数的阶乘。  

``` python
def factorial(num):
	if num == 0:
		return 1
	else:
		return num * factorial(num - 1)
	
result = factorial(5)
```

\# 15 说明文档  
说明文档：写在函数里的文字说明，用来描述：函数的功能、需要哪些参数、返回什么结果。  

``` python
def add(n1, n2):
	"""
	计算两个数相加的结果
	:param n1: 第一个数
	:param n2: 第二个数
	:return: 二者相加的结果
	"""
	return n1 + n2

result = add(1, 2)
```

\# 16 综合案例  
需求：完成一个健身挑战赛程序。  
1. 定义 `calc_total` 函数，用于统计总运动量（参数：多天的运动数据）。
2. 定义 `calc_avg` 函数，用于统计平均运动量（参数：总运动量和天数）。
3. 定义 `check_success` 函数，用于反馈挑战是否成功（参数：总运动量和目标运动量）。
4. 定义 `main` 函数，用于启动一场挑战赛（参数：比赛标题和比赛持续天数）。

``` python
def calc_total(*nums):
	# 计算总运动量（个）
	"""
	:param nums: 每一天的运动量（可变参数）
	:result: 总运动量（个）
	"""
	return sum(nums)

def calc_avg(total, days = 7):
	"""
	计算平均值
	:param total: 总运动量（个）
	:param days: 天数（默认值是7）
	:result: 平均值
	"""
	return total/days

def check_success(total, goal = 120):
	"""
	判断本次挑战是否成功
	:param total: 总运动量
	:param goal: 成功数量（默认值为120）
	:return: 成功或失败的具体信息
	"""
	if total >= goal:
		return "恭喜，挑战成功"
	else:
		return "抱歉，挑战失败"

def main(title, duration, goal):
	"""
	主函数，用于开始一场挑战赛
	:param title: 比赛标题
	:param duration: 比赛持续天数
	:param goal: 目标运动量
	:return: None
	"""
	print(f"{title}{duration}挑战赛（请输入每天的数量）")
	num1 = int(input(“第1天：”))
	num2 = int(input(“第2天：”))
	num3 = int(input(“第3天：”))
	num4 = int(input(“第4天：”))
	num5 = int(input(“第5天：”))
	num6 = int(input(“第6天：”))
	num7 = int(input(“第7天：”))
	# 计算总数
	total = calc_total(num1, num2, num3, num4, num5, num6, num7)
	# 计算平均值
	avg = calc_avg(total)
	# 判断挑战是否成功
	result = = check_success(total, goal)
	# 打印相关信息
	print(f"{title}{duration}天健身总结")
	# print("总数：%d，平均值：%.1f" %(total, avg))
	print(f"总数：{total}，平均值：{avg:.1f}")
	print(result)
main("仰卧起坐", 7, 40)
```


# 5 数据容器

## 5-1 数据容器
数据容器：一种能存放多个数据的数据类型。  
数据容器可以更高效的管理成批的数据，且便于存储、访问。  
1. 容器中的每一个数据，又称：每一个元素。
2. Python 中有很多种数据容器。

不同的数据容器，有不同的特点，和不同的语法，但都有一个共性，就是都可以存储多个元素。  
\# 2 列表（list）  
### 5-2-1 定义列表
`[元素0, 元素1, 元素2, 元素3, ...]`  
定义空列表：列表中的数据，后期会通过特定写法填充。  

``` python
# 定义有内容的变量
list1 = [34, 56, 21, 56, 11]
list2 = ["合肥", "猪脚", "你好"]
list3 = ["23", "猪脚", True, None]
list4 = ["23", "猪脚", True, None, [100, 200, 300]]

# 定义空列表（列表中的数据，后期会通过特定写法填充）
list5 = []
list6 = list()

print(list1)
print(list2)
print(list3)
print(list4)
```

### 5-2-2 下标（索引值）
下标（索引值）：列表中元素的位置编号。  
**正索引**：从左往右数，起始元素是 0，随后是 1，依次类推。  
**负索引**：从右往左数，起始元素是-1，随后是-2，依次类推。  
通过：列表[下标]的形式，取出对应元素。  

``` python
# 定义一个列表
nums = [10, 20, 30, 40, 50]

# 测试正索引
print(nums[0])

# 测试负索引
print(nums[-1])

# 测试错误索引
print(nums[5])  # 索引超出范围，也就是下标越界了

# 定义一个嵌套列表
nums2 = [10, 20, ["你好", "猪脚"], 40, 50]

# 去除“猪脚”
print(nums2[2][1])
```

### 5-2-3 增删改查
#### 5-2-3-1 新增
`列表.append(元素)`：调用列表的 `append` 方法。  
当一个函数隶属于某个对象时，那该函数就是该对象的一个方法。  

``` python
# 新增操作
# 方法一：通过列表的append方法，在列表尾部追加一个元素
nums = [10, 20, 30, 40]
nums.append(50)
print(nums)

# 方法二：通过列表的insert方法，在列表的指定下标处添加一个元素
nums = [10, 20, 30, 40]
nums.insert(2, 666)
print(nums)

# 方法三：通过列表的extend方法，将可迭代对象中的内容依次取出，追加到列表尾部
nums = [10, 20, 30, 40]
nums.extend("猪脚")
```

#### 5-2-3-2 删除

``` python
# 删除操作
# 方式一：通过列表的app方法，删除指定位置的元素，并返回该元素
nums= [10, 20, 10, 40, 50]
result = nums.pop(1)
print(nums)  # [10, 10, 40, 50]
print(result)  # 20

# 方式二：通过列表的remove方法，删除列表中第一次出现的指定值
nums = [10, 20, 10, 40, 50]
nums.remove(10)  # [20, 10, 40, 50]
print(nums)

# 方式三：通过列表的clear方法，删除列表中所有的元素（清空列表）
nums = [10, 20, 10, 40, 50]
nums.clear()
print(nums)  # []

# 方式四：通过del关键字，删除指定元素
nums = [10, 20, 10, 40, 50]
del nums[3]
print(nums)  # [10, 20, 10, 50]
```

#### 5-2-3-3 修改

``` python
nums = [10, 20, 10, 40, 50]
nums[2] = 66
print(nums)  # [10, 20, 66, 40, 50]
```

#### 5-2-3-4 查询

``` python
nums = [10, 20, 10, 40, 50]
print(nums[3])  # 40
```

#### 5-2-3-5 总计

```vtable
{"rows":[[{"t":"操作","rs":1,"cs":1},{"t":"写法","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1}],[{"t":"新增","rs":3,"cs":1},{"t":"`列表.append(元素)`","rs":1,"cs":1},{"t":"在列表尾部追加一个元素","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`列表.insert(下标, 元素)`","rs":1,"cs":1},{"t":"在列表指定下标处添加一个元素","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`列表.extend(可迭代对象)`","rs":1,"cs":1},{"t":"将可迭代对象中的内容依次取出，追加到列表尾部","rs":1,"cs":1}],[{"t":"删除","rs":4,"cs":1},{"t":"`列表.pop(下标)`","rs":1,"cs":1},{"t":"删除指定位置的元素，并将删除的元素返回","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`列表.remove(值)`","rs":1,"cs":1},{"t":"删除列表第一次出现的指定值","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`列表.clear()`","rs":1,"cs":1},{"t":"删除列表中的所有元素（清空列表）","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`del 列表[下标]`","rs":1,"cs":1},{"t":"删除指定位置的元素","rs":1,"cs":1}],[{"t":"修改","rs":1,"cs":1},{"t":"`列表[下标] = 值`","rs":1,"cs":1},{"t":"通过下标修改指定位置的元素","rs":1,"cs":1}],[{"t":"查询","rs":1,"cs":1},{"t":"`列表[下标]`","rs":1,"cs":1},{"t":"通过下标获取指定位置的元素","rs":1,"cs":1}]]}
```

### 5-2-4 常用方法

``` python
# 1. 使用index方法，查找指定元素在列表中第一次出现的下标，返回值是：元素下标
fruits = ["香蕉", "苹果", "橙子", "香蕉"]
result = fruits.index("苹果")
print(result)  # 1

# 2. 使用count方法，统计某个元素在列表中出现的次数，返回值是：元素出现的次数
nums = [10, 20, 10, 30, 10, 40]
result = nums.count(10)
print(result)  # 3

# 3. 使用reverse方法，对列表进行反转（会改变原列表）
nums = [23, 11, 32, 30, 17]
nums.reverse()
print(nums)  # [17, 30, 32, 11, 23]

# 4. 使用sort方法，对列表排雷（默认从小到大），若想从大到小，可以将reverse参数设为True
# 4.1 若列表中的元素：都是数字，则按照数字的大小顺序进行排序。
nums = [23, 11, 32, 30, 17]
nums.sort()  # nums.sort(reverse = True) 关键字传参，从大到小
print(nums)  # [11, 17, 23, 30, 32]

# 4.2 若列表中的元素：既有数字，又有字符串，那就会报错
nums = [23, 11, 32, 30, 17, "猪脚"]
nums.sort()
print(nums)  # [11, 17, 23, 30, 32]  # 报错

# 4.3 若列表中的元素：都是字符串，则按照字符串的Unicode编码大小进行排序
msg_list = ["北京", "上海", "广州", "深圳"]
msg_list.sort()
print(msg_list)
```

> `index` 方法中是无法进入嵌套列表中进行查找。 
> `count` 方法无法对嵌套列表中的信息进行统计。  
> `reverse` 方法无法将嵌套列表中的信息进行反转。  
> 注意：所有的列表方法，都只作用于“当前层”的元素（浅层操作），不会自动进入嵌套的“里层”结构中。  

```vtable
{"rows":[[{"t":"写法","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1},{"t":"返回值","rs":1,"cs":1}],[{"t":"`列表.index(值)`","rs":1,"cs":1},{"t":"查找指定元素中第一次出现的下标","rs":1,"cs":1},{"t":"元素下标","rs":1,"cs":1}],[{"t":"`列表.count(值)`","rs":1,"cs":1},{"t":"统计某个元素在列表中出现的次数","rs":1,"cs":1},{"t":"元素出现的次数","rs":1,"cs":1}],[{"t":"`列表.reverse()`","rs":1,"cs":1},{"t":"反转列表，无需参数，直接操作原列表","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"`列表.sort(reverse = 布尔值)`","rs":1,"cs":1},{"t":"对列表排序（默认从小到大排序），会改变原列表，reverse参数用于控制排序方式","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}]]}
```

### 5-2-5 常用内置函数

``` python
# 1. 使用内置的sorted函数，返回一个排序后的新容器（不改变原容器，默认顺序：从小到大）
# 1.1 若列容器中的元素：都是数字，则按照数字的大小顺序进行排序。
nums = [23, 11, 32, 30, 17]
result = sorted(nums, reverse=True)
print(nums)  # [23, 11, 32, 30, 17]
print(result)  # [32, 30, 23, 17, 11]

# 1.2 若列容器中的元素：既有数字，又有字符串，那就会报错。
nums = [23, 11, 32, 30, 17, "猪脚"]
sorted(nums)  # 报错

# 1.3 若列容器中的元素：都是字符串，则按照字符串的Unicode编码大小进行排序。
msg_list = ["合肥", "猪脚", "你好"]
result = sorted(msg_list)
print(smg_list)
print(result)

# 2. 使用内置的len函数，获取容器中元素的总数量，返回值是：元素总数量。
nums = [10, 20, 10, 30, 10, 40]
result = len(nums)
print(result)  # 6

# 3. 使用内置的max函数，获取容器中的最大值，返回值是：最大值。
# 3.1 如果容器中的元素：都是数字，那max返回的是最大的数。
nums = [23, 11, 32, 30, 17]
result = max(nums)
print(result)  # 32

# 3.2 如果容器中的元素：既有数字又有字符串，那max会报错。
nums = [23, 11, 32, 30, 17, "猪脚"]
result = max(nums)  # 报错

# 3.3 如果容器中的元素：都是字符串，那max会返回：Unicode编码最大的字符。
msg_list = ["合肥", "猪脚", "你好"]
result = max(msg_list)
print(msg_list)  # ['合肥', '猪脚', '你好']
print(result)  # 猪脚

# 3.4 max 函数也可以接受多个值，并筛选出最大值
result = max(33, 45, 12, 78, 99)
print(result)  # 99

# 4. 使用内置的min函数，获取容器中的最小值，返回值是：最小值。
# 备注：min函数的使用方式与注意点与max函数一样，只不过min函数返回的是最小值
nums = [23. 11, 32, 30, 17]
result = min(nums)
print(result)  # 11

# 5. 使用内置的sum函数，对容器中的数据进行求和（元素只能是数值）。
sums = [10, 20, 30, 40, 50]
result = sum(sums)
print(result)  # 150
```

```vtable
{"rows":[[{"t":"操作","rs":1,"cs":1},{"t":"写法","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1},{"t":"返回值","rs":1,"cs":1}],[{"t":"内置函数","rs":5,"cs":1},{"t":"`sorted(数据容器, reverse=布尔值)`","rs":1,"cs":1},{"t":"对容器排序（默认从小到大排列）不会改变原列表，`reverse`参数用于控制排序方式","rs":1,"cs":1},{"t":"排序后的新容器","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`len(数据容器)`","rs":1,"cs":1},{"t":"获取容器中元素的总数量","rs":1,"cs":1},{"t":"元素总数量","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`max(数据容器)`","rs":1,"cs":1},{"t":"获取容器中的最大值","rs":1,"cs":1},{"t":"最大值","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`min(数据容器)`","rs":1,"cs":1},{"t":"获取容器中的最小值","rs":1,"cs":1},{"t":"最小值","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`sum(数据容器)`","rs":1,"cs":1},{"t":"获取容器中所有元素的和","rs":1,"cs":1},{"t":"所有元素的和","rs":1,"cs":1}]]}
```

### 5-2-6 循环遍历
遍历：把容器中的元素依次取出，并对它们进行处理的过程。  
### 5-2-7 while 循环遍历
``` python
# 定义一个成绩列表
score_list = [62, 50, 60, 48, 80, 20, 95]

# 使用while循环遍历列表
index = 0
while index < len(score_list):
	print(score_list[index])
	index += 1
```

### 5-2-8 for 循环遍历

``` python
# 定义一个成绩列表
score_list = [62, 50, 60, 48, 80, 20, 95]

# 使用for循环遍历列表
for item in score_list:
	print(item)

# 使用for循环遍历列表（通过range函数和len函数按照索引遍历）
for index in range(len(scoer_list)):
	print(score_list(index))

# 使用for循环遍历列表（通过enumerate函数，同时获取下标（索引值）和元素）
# enumerate 的 strat 参数，可以让计数从指定值开始（改变的是循环时的“编号”，不是真正的索引值）
for index, item in enumerate(score_list, start=5):
	print(index, item)
```

### 5-2-9 练习
需求：实现一个成绩统计小程序，可以对多名学生的成绩，进行统计和分析。  
备注：用户可以连续输入学生成绩，直到用户输入“结束”字符串。  

``` python
print("请输入学生成绩，输入“结束”停止录入")
score_list = []

# 持续循环，让用户输入学生成绩
while True:
	data = input("请输入成绩：")
	if data == "结束":
		break
	else:
		score_list.append(int(data))
	
# 如果score_list中有数据，则开始统计
if score_list:  # 列表中有内容就为 True，如果列表中没有内容就为 False
	# 统计平均分
	avg = sum(score_list) / len(score_list)
	# 合格人数
	pass_count = 0
	# 优秀人数
	excellent_count = 0
	# 遍历列表，开始统计
	for item in score_list:
		if item >= 60:
			pass_count += 1
		if item >= 90:
			excellent_count += 1
	# 合格率
	pass_rate = pass_count / len(score_list) * 100
	# 优秀率
	excellent_rate = excellent_count / len(score_list) * 100
	# 打印信息
	print("信息统计如下")
	print(f"总人数为：{len(score_list)}")
	print(f"最高分为：{max(score_list)}")
	print(f"最低分为：{min(score_list)}")
	print(f"合格人数：{pass_count}人")
	print(f"合格率为：{pass_rate:.1f}%")
	print(f"优秀人数：{excellent_count}人")
	print(f"优秀率为：{excellent_rate:.1f}%")
	print(f"平均分数：{avg:.1f}")
else:
	print("您没有输入任何成绩")
```

### 5-2-10 特点总结
1. 可存放不同类型的元素。
2. 元素是有序存储的（正索引、负索引）。
3. 列表中的元素允许重复。
4. 元素是允许修改的（增、删、改、查、其他操作）。
5. 长度不固定，可以随着操作自动调正大小。

列表是最常用的数据容器，当遇到要“存储一批数据”的场景时，首选列表。  
\# 3 元组（tuple）  
元组是一种和列表类似的数据容器，它和列表的区别是：元组中的元素不可修改。  

``` python
# 定义元组
t1 = (28, 67, 21, 67, 11)
t2 = ("合肥", "猪脚", "你好")
t3 = (100, True, "你好", None)
t4 = (100, True, "你好", None, (50, 60, 70))

# 元组的下标
t1 = (28, 67, 21, 67, 11)
print(t1[3])  # 67
print(t1[-1])  # 11
```

> 元组中的元素不可修改。  

``` python
# 元组中的元素，不可修改
t1 = (28, 67, 21, 67, 11)
t1[0] = 100  # 报错

# 元组中的元素，不可修改，但元组中如果存放了可变类型（列表），那可变类型中的内容仍可修改
t2 = (28, 67, 21, 67, 11, [100, 200, 300, ("你好", "猪脚")])
# t2[5] = 400 报错
t2[5][2] = 400
print(t2)
```

``` python
# 定义空元组
t1 = ()
t2 = tuple()

# 定义只有一个元素的元组
t1 = ("你好",)
t2 = (18,)
```

### 5-3-1 元组的常用方法

``` python
# index 方法：获取指定元素在元组中第一次出现的下标。
t1 = (28, 67, 21, 67, 11)
result = t1.index(67)
print(result)  # 1

# count 方法：统计指定元素在元组中出现的次数
t1 = (28, 67, 21, 67, 11)
result = t1.count(67)
print(result)  # 2
```

### 5-3-2 元组常用的内置函数

``` python
# max 函数，返回元组中的最大值
t1 = (23, 11, 32, 30, 17)
result = max(t1)
print(result)  # 32

# min 函数，返回元组中的最小值
t1 = (23, 11, 32, 30, 17)
result = min(t1)
print(result)  # 11

# len 函数，返回元组中元素的个数（元组长度）
t1 = (23, 11, 32, 30, 17)
result = len(t1)
print(result)  # 5

# sorted 函数，对元组进行排序（不修改原元组，返回一个新的列表）
t1 = (23, 11, 32, 30, 17)
result = sorted(t1)
print(result)  # [11, 17, 23, 30, 32]

result = sorted(t1, reverse=True)
print(result)  # [32, 30, 23, 17, 11]
print(tuple(result))  # (32, 30, 23, 17, 11)

# sum 函数，统计元组中所有元素的和（元素必须是纯数字）
t1 = (23, 11, 32, 30, 17)
result = sum(t1)
print(result)  # 113
```

> 实际开发中的元组，不一定是我们自己定义的，比如函数的可变参数 `*args` 就是一个元组。  

``` python
def demo(*args):
	return sum(args)
result = demo(100, 200, 300)
print(result)  # 600
```

``` python
# 元组的循环遍历
t1 = (23, 11, 32, 30, 17)
# while 循环遍历
index = 0
while index < len(t1):
	print(t1[index])
	index += 1

# for 循环遍历
for item in t1:
	print(item)
```

### 5-3-3 函数_解包列表或元组传参
``` python
# 定义函数时，使用*args（变量不一定非要用args，比如写：*data也可以），将收到的多个参数。打包成一个元组
def test(data):
	print(f"我是test函数，我收到的参数是：{data}")

list1 = [100, 200, 300, 400]
tuple1 = ("你好", "合肥", "猪脚")

# 函数调用时，正常传参：列表或元组
test(list1)  # 我是test函数，我收到的参数是：[100, 200, 300, 400]
test(tuple1)  # 我是test函数，我收到的参数是：('你好', '合肥', '猪脚')

# 函数调用时，使用*对:列表或元组进行解包后，再传递参数。
def test1(*args):
	print(f"我是test函数，我收到的参数是：{args}")
test1(*list1)  # 此种写法相当于：test1(100, 200, 300, 400)
test1(*tuple1)  # 此种写法相当于：test1(“你好”, “合肥”, “猪脚”)
```

### 5-3-4 特点总结
1. 可存放不同类型的元素。
2. 元素是有序存储的（正索引、负索引）。
3. 元组中的元素允许重复。
4. 元素不允许修改（不能：增删改、只能：查）。
5. 长度固定（一旦创建，元素个数不能增减）。

> 元组是一种“只读”的数据容器，想保存一批“不会变的数据”时，首选元组。  

\# 4 字符串（str）  
数据容器的角度：字符串就是存放多个字符的容器。  
字符串支持（索引值）。  
字符串不能嵌套（字符串中的每一个元素都是单一字符）。  

``` python
# 字符串的下标
msg = "welcome to prokyhoof"
print(msg[3])  # c
print(msg[-1])  # f

# 字符串中的字符，不可修改
msg = "welcome to prokyhoof"
msg[0] = "a"  # 报错

# 字符串不能嵌套
msg = "welcome to "hello" prokyhoof"  # 报错
msg = "welcome to 'hello' prokyhoof"  # welcome to 'hello' prokyhoof
msg = "welcome to \"hello\" prokyhoof"  # welcome to "hello" prokyhoof
```

### 5-4-1 常用方法
`index` 方法：获取指定字符在字符串第一次出现的下标。  
`split` 方法：将字符串按照指定字符进行分隔，并返回一个列表。  
`replace` 方法：将字符串中的某个字符串片段，替换成目标字符串。  
`count` 方法：统计指定字符在字符串中出现的次数。  

``` python
# index
msg = "welcome to prokyhoof"
result = msg.index("t")
print(result)  # 8

# split
msg = "welcome to prokyhoof"
result = msg.split(" ")
print(result)  # ['welcome', 'to', 'prokyhoof']

# replace
msg = "welcome to prokyhoof"
result = msg.replace("prokyhoof", "猪脚")
print(result)  # welcome to 猪脚

# count
msg = "welcome to prokyhoof"
result = msg.count("p")
print(result)  # 1
```

`strip` 方法：从某个字符串中删除指定字符串中的任意字符。  
规则：从字符串两端开始删除，直到遇到第一个不在指定字符串中的字符就停下。  

``` python
msg = "666猪6脚666"
result = msg.strip("6")
print(result)  # 猪6脚

msg = "   猪脚   "
result = msg.strip()
print(result)  # 猪脚
```

### 5-4-2 常用内置函数
`len` 函数：统计字符串中，字符的个数（字符串长度）  

``` python
# len
msg = "welcome to prokyhoof"
result = len(msg)
print(result)  # 20
```

### 5-4-3 循环遍历

``` python
# 字符串的循环遍历
msg = "welcome to prokyhoof"
# while 循环遍历
index = 0
while index < len(msg):
	print(msg[index])
	index += 1

# for 循环遍历
for item in msg:
	print(item)
```

\# 5 序列
### 5-5-1 切片操作
#### 5-5-1-1 序列、切片
序列：能连续存放元素的数据容器，元素有先后顺序，且可以通过下标访问。  

> 列表、元组、字符串都是序列。  

切片：从序列中按照指定范围，取出一部分元素，形成一个新的序列的操作。  
#### 5-5-1-2 语法
`序列[起始索引:结束索引:步长]`
`步长`：步长为 `n`：每次跳过 `n - 1` 位取出。  

``` python
# 对列表进行切片
list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[0:5:1]
print(list2)  # [10, 20, 30, 40, 50]

list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[1:8:2]
print(list2)  # [20, 40, 60, 80]

list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[1:8:3]
print(list2)  # [20, 50, 80]

list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[0:10:1]
print(list2)  # [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[::]
print(list2)  # [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[:999:]
print(list2)  # [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[3::]
print(list2)  # [40, 50, 60, 70, 80, 90, 100]

list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[:5:]
print(list2)  # [10, 20, 30, 40, 50]

list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[::4]
print(list2)  # [10, 50, 90]
```

>  注意：当其实索引大于结束索引时，步长必须是负数，否则结果是空列表。  

``` python
list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[7:2:-1]
print(list2)  # [80, 70, 60, 50, 40]

# 一个特殊情况：当同时省略其实索引和结束索引时，如果步长为负数，那Python会自动对调：起始位置和结束位置
list1 = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
list2 = list1[::-1]
print(list2)  # [100, 90, 80, 70, 60, 50, 40, 30, 20, 10]
```

``` python
# 对元组进行切片
tuple1 = (10, 20, 30, 40, 50, 60, 70, 80, 90, 100)
tuple2 = tuple1[0:5:1]
print(tuple2)  # (10, 20, 30, 40, 50)

# 对字符串进行切片
msg1 = "welcome to prokyhoof"
msg2 = msg1[2:9:2]
print(msg2)  # loet
```

### 5-5-2 序列的其他操作
#### 5-5-2-1 相加

> 注意：两个同类型的序列才能相加（字符串 + 字符串、列表 + 列表、元组 + 元组）。  

``` python
# 序列相加
list1 = [10, 20, 30, 40]
list2 = [50, 60, 70, 80]
list3 = list1 + list2
print(list3)  # [10, 20, 30, 40, 50, 60, 70, 80]

tuple1 = (10, 20, 30, 40)
tuple2 = (50, 60, 70, 80)
tuple3 = tuple1 + tuple2
print(tuple3)  # (10, 20, 30, 40, 50, 60, 70, 80)

str1 = "hello, "
str2 = "ProkyHoof"
str3 = str1 + str2
print(str3)  # hello, ProkyHoof

# 错误示例
list1 = [10, 20, 30, 40]
str1 = "hello"
print(list1 + str1)  # 报错
```

#### 5-5-2-2 相乘（重复）

> 注意：`n` 必须是整数，不能是浮点数。  

``` python
list1 = [10, 20, 30, 40]
list2 = list1 * 3
print(list2)  # [10, 20, 30, 40, 10, 20, 30, 40, 10, 20, 30, 40]
```

\# 6 集合  
### 5-6-1 定义集合
集合的特点：内部的元素无序（不保证顺序）、不能通过下标访问元素、会自动去除重复元素。  

``` python
# 定义有内容的【可变集合】
s1 = {10, 20, 20, 30, 40, 40, 50, 60, 70, 80, 90, 100}
s2 = {"你好", "hello", "你好", "prokyhoof", "合肥"}
s3 = {10, "你好", 1, True, 12.4}
print(type(s1), s1)  # <class 'set'> {100, 70, 40, 10, 80, 50, 20, 90, 60, 30}
print(type(s2), s2)  # <class 'set'> {'你好', 'hello', '合肥', 'prokyhoof'}
print(type(s3), s3)  # <class 'set'> {'你好', 10, 1, 12.4}

s2.add("猪脚")
print(s2)  # {'猪脚', '合肥', 'prokyhoof', '你好', 'hello'}

# 定义有内容的【不可变集合】
s1 = frozenset({10, 20, 20, 30, 40, 40, 50, 60, 70, 80, 90, 100})
s2 = frozenset({"你好", "hello", "你好", "prokyhoof", "合肥"})
s3 = frozenset({10, "你好", 1, True, 12.4})
print(type(s1), s1)  # <class 'frozenset'> frozenset({100, 70, 40, 10, 80, 50, 20, 90, 60, 30})
print(type(s2), s2)  # <class 'frozenset'> frozenset({'你好', 'hello', '合肥', 'prokyhoof'})
print(type(s3), s3)  # <class 'frozenset'> frozenset({'你好', 10, 1, 12.4})
```

> `frozenset` 接收的参数，可以是任意可迭代对象，但最终返回的一定是【不可变集合】

``` python
s1 = frozenset([10, 20, 30, 40, 50])
s2 = frozenset((10, 20, 30, 40, 50))
s3 = frozenset("hello")
print(type(s1), s1)  # <class 'frozenset'> frozenset({40, 10, 50, 20, 30})
print(type(s2), s2)  # <class 'frozenset'> frozenset({40, 10, 50, 20, 30})
print(type(s3), s3)  # <class 'frozenset'> frozenset({'e', 'l', 'o', 'h'})
```

``` python
# 定义空集合（可变集合）
s1 = set()
print(type(s1), s1)  # <class 'set'> set()

# 不能直接写{}来定义空结合，因为直接写{}定义的是：空字典
s2 = {}
print(type(s2), s2)  # <class 'dict'> {}

# 定义空集合（不可变集合）
s3 = frozenset()
print(type(s3), s3)  # <class 'frozenset'> frozenset()

# 集合中不能嵌套【可变集合】，但可以嵌套【不可变集合】
# 通俗理解：只有“不可变”的东西，才能安全的放进集合里
s1 = {10, 20, 30, 40, 50}
s2 = frozenset({100, 200, 300, 400, 500})
l1 = [666, 777, 888]
t1 = ("hello", "prokyhoof", "合肥")

s3 = {11, 22, 33, s1}  # 报错
s3 = {11, 22, 33, s2}  # 没问题
s3 = {11, 22, 33, l1}  # 报错
s3 = {11, 22, 33, t1}  # 没问题
print(s3)
```

> 集合中不能嵌套【可变集合】，但可以嵌套【不可变集合】  

### 5-6-2 增删改查
#### 5-6-2-1 增

``` python
# add方法：向集合中添加元素
s1 = {10, 20, 30, 40, 50}
s1.add(60)
print(s1)  # {50, 20, 40, 10, 60, 30}

# update方法：向集合中添加元素（必须传递可迭代对象，例如“列表、元组、集合等”）
s1 = {10, 20, 30, 40, 50}
s1.update([60, 70])
s1.update((80, 90))
s1.update({100, 200})
s1.update(range(300, 308))
print(s1)
```

#### 5-6-2-2 删
``` python
# remove方法：从集合中移除元素（移除不存在的元素，会报错）
s1 = {10, 20, 30, 40, 50}
s1.remove(20)
print(s1)  # {50, 40, 10, 30}

# discard方法：从集合中移除元素（移除不存在的元素，不会报错）
s1 = {10, 20, 30, 40, 50}
s1.discard(80)
print(s1)  # {50, 20, 40, 10, 30}

# pop方法：从集合中移除一个任意元素，返回值是移除的那个元素
s1 = {10, 20, 30, 40, 50}
s2 = {"你好", "合肥", "猪脚", "hello"}
result = s1.pop()
print(s1)  # {20, 40, 10, 30}
print(result)  # 50
result = s2.pop()
print(s2)  # {'hello', '合肥', '你好'}
print(result)  # 猪脚

# clear方法：清空集合
s1 = {10, 20, 30, 40, 50}
s1.clear()
print(s1)  # set()
```

#### 5-6-2-3 改
集合没有下标，也不支持 replace 方法，所以集合没有专门用于“改”的方法。  

``` python
# 使用 add + remove 的组合，来实现修改的效果
s1 = {10, 20, 30, 40, 50}
s1.remove(20)
s1.add(66)
print(s1)  # {50, 66, 40, 10, 30}
```

#### 5-6-2-4 查
由于集合没有下标，也不支持切片操作，所以结合不具备按位置访问的能力。  

``` python
s1 = {10, 20, 30, 40, 50}
result = 20 in s1
print(result)  # True
```

### 5-6-3 总结
```vtable
{"rows":[[{"t":"操作","rs":1,"cs":1},{"t":"写法","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1},{"t":"返回值","rs":1,"cs":1}],[{"t":"新增","rs":2,"cs":1},{"t":"`集合.add(元素)`","rs":1,"cs":1},{"t":"向集合中添加单个元素（若已存在则忽略）","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`集合.update(可迭代对象)`","rs":1,"cs":1},{"t":"将可迭代对象中的内容逐个取出，批量添加到集合","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"删除","rs":4,"cs":1},{"t":"`集合.remove(元素)`","rs":1,"cs":1},{"t":"删除指定元素，不存在会报错","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`集合.discard(元素)`","rs":1,"cs":1},{"t":"删除指定元素，不存在不会报错","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`集合.pop(元素)`","rs":1,"cs":1},{"t":"随机删除并返回一个元素","rs":1,"cs":1},{"t":"被移除的元素","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`集合.clear(元素)`","rs":1,"cs":1},{"t":"删除集合中的所有元素（清空集合）","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"修改","rs":1,"cs":1},{"t":"`remove` + `add`","rs":1,"cs":1},{"t":"集合不能直接修改，通过“删 + 增”实现修改效果","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"查询","rs":1,"cs":1},{"t":"集合没有下标，也不支持切片操作，所以不具备按位置访问的能力，但可以使用成员运算符。","rs":1,"cs":3},{"t":"","rs":0,"cs":0},{"t":"","rs":0,"cs":0}]]}
```

### 5-6-4 常用方法

``` python
# 集合A.difference(集合B)：
# 作用：找出集合A中，不同于集合B的元素（集合 A 与集合 B 都不变，返回的是一个新的集合）
s1 = {10, 20, 30, 40, 50}
s2 = {30, 40, 50, 60, 70}
result = s1.difference(s2)
print(s1)  # {50, 20, 40, 10, 30}
print(s2)  # {50, 70, 40, 60, 30}
print(result)  # {10, 20}

# 集合A.difference_update(集合B)：
# 作用：从集合 A 中，删除集合 B 中存在的元素（集合 A 会被修改，集合 B 不会）
s2.difference_update(s1)
print(s1)  # {50, 20, 40, 10, 30}
print(s2)  # {70, 60}

# 集合A.union(集合B):
# 作用：合并两个集合，集合 A 和集合 B 都不变，返回的是一个新的集合
result = s1.union(s2)
print(result)  # {50, 20, 70, 40, 10, 60, 30}

# 集合A.issubset(集合B)：
# 作用：判断集合 A 是否为集合 B 的子集
# 如果集合 A 的所有元素都在集合 B 中，那就返回 True，否则返回 False
s3 = {30, 40, 50}
result = s3.issubset(s1)
print(result)  # True

# 集合A.issuperset(集合B)：
# 作用：判断集合A是否是集合 B 的超集
# 如果集合 A 中，包含了集合 B 中的所有元素，那就返回 True，否则返回 False
s1 = {10, 20, 30, 40, 50}
s2 = {30, 40, 50, 60, 70}
s3 = {30, 40, 50}
result = s1.issuperset(s3)
print(result)  # True

# 集合A.isdisjoint(集合B)：
# 作用：判断集合 A 和集合 B 是否没有交集
# 如果没有交集，返回 True，只要有一个公共元素。就返回 False
s1 = {10, 20, 30, 40, 50}
s2 = {30, 40, 50, 60, 70}
s3 = {30, 40, 50}
result = s1.isdisjoint(s3)
print(result)  # False
```

### 5-6-5 常用方法总结

```vtable
{"rows":[[{"t":"方法","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1},{"t":"返回值","rs":1,"cs":1}],[{"t":"`集合A.difference(集合B）`","rs":1,"cs":1},{"t":"找出集合A中，不同于集合B的元素","rs":1,"cs":1},{"t":"一个新的集合","rs":1,"cs":1}],[{"t":"`集合A.difference_update(集合B)`","rs":1,"cs":1},{"t":"从集合 A 中，删除集合 B 中存在的元素","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"`集合A.union(集合B)`","rs":1,"cs":1},{"t":"合并两个集合，集合 A 和集合 B 都不变，返回的是一个新的集合","rs":1,"cs":1},{"t":"一个新的集合","rs":1,"cs":1}],[{"t":"`集合A.issubset(集合B)`","rs":1,"cs":1},{"t":"判断集合 A 是否为集合 B 的子集","rs":1,"cs":1},{"t":"布尔值","rs":1,"cs":1}],[{"t":"`集合A.issuperset(集合B)`","rs":1,"cs":1},{"t":"判断集合A是否是集合 B 的超集","rs":1,"cs":1},{"t":"布尔值","rs":1,"cs":1}],[{"t":"`集合A.isdisjoint(集合B)`","rs":1,"cs":1},{"t":"判断集合 A 和集合 B 是否没有交集","rs":1,"cs":1},{"t":"布尔值","rs":1,"cs":1}]]}
```

### 5-6-6 数学运算

``` python
s1 = {10, 20, 30, 40, 50, 60}
s2 = {40, 50, 60, 70, 80, 90}

# 并集
result = s1 | s2
print(result)  # {70, 40, 10, 80, 50, 20, 90, 60, 30}

# 交集
result = s1 & s2
print(result)  # {40, 50, 60}

# 差集
result = s1 - s2
print(result)  # {10, 20, 30}

# 对称差集
result = s1 ^ s2
print(result)  # {70, 10, 80, 20, 90, 30}
```

#### 5-6-6-1 数学运算总结

```vtable
{"rows":[[{"t":"写法","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1}],[{"t":"`集合A | 集合B`","rs":1,"cs":1},{"t":"并集（找出集合 A 中，不同于集合 B 的元素）","rs":1,"cs":1}],[{"t":"`集合A &amp; 集合B`","rs":1,"cs":1},{"t":"交集（找出集合 A 和集合 B 中，共有的元素）","rs":1,"cs":1}],[{"t":"`集合A - 集合B`","rs":1,"cs":1},{"t":"差集（得到属于集合 A，但不属于集合 B 的元素）","rs":1,"cs":1}],[{"t":"`集合A ^ 集合B`","rs":1,"cs":1},{"t":"对称差集（排除两个集合的交集，然后合并剩下的元素）","rs":1,"cs":1}]]}
```

#### 5-6-6-2 循环遍历

> 集合不能使用 `while` 循环直接遍历，但可以使用 ` for ` 循环进行遍历。  
> 原因：`while` 循环需要通过下标访问元素，而集合是无序的、没有下标。  

``` python
s1 = {1, 2, 3, 4, 5, 6, 7, 8, 9}
for item in s1:
	print(item, end=" ")  # 1 2 3 4 5 6 7 8 9 
```

### 5-6-7 特点总结
1. 无序：集合中的元素没有固定顺序，无法通过下标访问。
2. 不重复：集合会自动去重，同一个元素只会保留一份。
3. 分为两种：可变集合（set）和不可变集合（forzenset）。
4. 集合中的元素必须是不可变类型（如：字符串、数字、元组）。
5. 集合支持：并集、交集、差集、对称差集等数字操作。

> 集合是可以去重的数据容器，当只关心元素是否存在，而不在乎顺序时，首选集合。  

\# 7 字典（dict）  
### 5-7-1 定义字典
对应关系：键（key）与值（value）的对应关系。  

> 字典中的 key 不能重复，若出现重复，则后写的会覆盖之前写的。  

``` python
# 定义有内容的字典
d1 = {"张三": 72, "李四": 60, "王五": 85}
print(type(d1), d1)  # <class 'dict'> {'张三': 72, '李四': 60, '王五': 85}


# 字典中的 key 不能重复，若出现重复，则后写的会覆盖之前写的
d1 = {"张三": 72, "李四": 60, "王五": 85, "张三": 99}
print(d1)  # {'张三': 99, '李四': 60, '王五': 85}

# 定义空字典
d1 = {}
d2 = dict()
print(type(d1), d1)  # <class 'dict'> {}
print(type(d2), d2)  # <class 'dict'> {}
```

> 字典中的键（key）必须是不可变类型，但值（value）可以是任意类型。  

``` python
d1 = {("抽烟", "喝酒"): 72, "李四": 60, "王五": 85}
d2 = {["抽烟", "喝酒"]: 72, "李四": 60, "王五": 85}
```

``` python
# 字典可以嵌套
student_dict = {
	2026001: {
	"姓名": "张三", 
	"年龄": 18, 
	"成绩": 72
	},
	2026002: {
	"姓名": "李四", 
	"年龄": 19, 
	"成绩": 60
	},
	2026003: {
	"姓名": "王五", 
	"年龄": 20, 
	"成绩": 85
	}
}
```

### 5-7-2 增删改查

``` python
# 查询
d1 = {"张三": 72, "李四": 60, "王五": 85}

# 直接取值，若键（key）不存在，会报错
result = d1["张三"]
print(result)  # 72

# 安全取值，若键（key）不存在，会返回默认值（若没有设置默认值，则会返回 None）
result = d1.get("ProkyHoof", "抱歉，不存在")
print(result)  # 抱歉，不存在

# 新增
d1 = {"张三": 72, "李四": 60, "王五": 85}
d1["赵六"] = 100
print(d1)  # {'张三': 72, '李四': 60, '王五': 85, '赵六': 100}

# 修改
d1 = {"张三": 72, "李四": 60, "王五": 85}
# 修改的写法，与新增的写法一样，若字典中有对应的 key，就是修改；若没有，就是新增
d1["张三"] = 100
print(d1)  # {'张三': 100, '李四': 60, '王五': 85}
# 批量修改
d1.update({"李四": 40, "王五": 67})
print(d1)  # {'张三': 100, '李四': 40, '王五': 67}

# 删除
d1 = {"张三": 72, "李四": 60, "王五": 85}

# 删除指定 key 所对应的那组键值对
del d1["张三"]
print(d1)  # {'李四': 60, '王五': 85}

# 删除指定 key 所对应的那组键值对，并返回这个 key 所对应的值
result = d1.pop("张三")
print(result)  # 72

# pop 方法可以设置默认值
# 默认可以保证：当要删除的 key 不存在的情况下，程序不会报错，并且返回这个默认值
result = d1.pop("ProkyHoof", "删除失败")
print(result)  # 删除失败

# 清空字典
d1.clear()
print(d1)  # {}
```


```vtable
{"rows":[[{"t":"操作","rs":1,"cs":1},{"t":"写法","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1},{"t":"返回值","rs":1,"cs":1}],[{"t":"新增","rs":1,"cs":1},{"t":"`字典[key] = 值`","rs":1,"cs":1},{"t":"新增一组键值对（若键已存在则变为修改）","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"删除","rs":2,"cs":1},{"t":"`del 字典[key]`","rs":1,"cs":1},{"t":"删除指定键值对的那组键值对（键不存在会报错）","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`字典.pop(key, 默认值)`","rs":1,"cs":1},{"t":"删除指定键对应的那组键值对，并返回该键对应的值；若键不存在且设置了默认值，则返回默认值","rs":1,"cs":1},{"t":"被删除键的值活默认值","rs":1,"cs":1}],[{"t":"修改","rs":2,"cs":1},{"t":"`字典[key] = 新值`","rs":1,"cs":1},{"t":"修改指定键对应的值（若键不存在则变为新增）","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`字典.update(其他字典)`","rs":1,"cs":1},{"t":"批量修改或合并多个键值对","rs":1,"cs":1},{"t":"无","rs":1,"cs":1}],[{"t":"查询<br><br>","rs":2,"cs":1},{"t":"`字典[key]`","rs":1,"cs":1},{"t":"根据键取值，若键不存在会报错","rs":1,"cs":1},{"t":"键对应的值","rs":1,"cs":1}],[{"t":"","rs":0,"cs":0},{"t":"`字典.get(key, 默认值)`","rs":1,"cs":1},{"t":"安全取值，若键不存在返回默认值（未设置则返回 None 值","rs":1,"cs":1},{"t":"键对应的值活 None","rs":1,"cs":1}]]}
```

### 5-7-3 常见方法
  
``` python
# keys 方法：用于获取字典中所有的键
d1 = {"张三": 72, "李四": 60, "王五": 85}

# keys 方法的返回值不是 list，而是一种叫做 dict_keys 的类型
result = d1.keys()
print(result)  # dict_keys(['张三', '李四', '王五'])
print(type(result))  # <class 'dict_keys'>

# dict_keys 的列表类似，可以被遍历，但要注意的是：它不能通过下标访问元素
for item in result:
	print(item, end = " ")  # 张三 李四 王五

# 借助内置的 list 函数，可以将 dict_keys 转换成 list
l1 = list(result)
print(l1)  # ['张三', '李四', '王五']
print(type(l1))  # <class 'list'>
```

``` python
# values 方法，获取字典中所有的值
d1 = {"张三": 72, "李四": 60, "王五": 85}
result = d1.values()
print(result)  # dict_values([72, 60, 85])
print(type(result))  # <class 'dict_values'>
```

``` python
# items 方法：获取字典中所有的键值对（每组键值对以元组的形式呈现）
d1 = {"张三": 72, "李四": 60, "王五": 85}
# items 方法返回的类型是：dict_items，它的特点也和 dict_keys 一样
result = d1.items()
print(result)  # dict_items([('张三', 72), ('李四', 60), ('王五', 85)])
print(type(result))  # <class 'dict_items'>
```

```vtable
{"rows":[[{"t":"方法","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1},{"t":"返回值类型","rs":1,"cs":1}],[{"t":"`字典.keys()`","rs":1,"cs":1},{"t":"用于获取字典中所有的键","rs":1,"cs":1},{"t":"dict_keys","rs":1,"cs":1}],[{"t":"`字典.values()`","rs":1,"cs":1},{"t":"获取字典中所有的值","rs":1,"cs":1},{"t":"dict_values","rs":1,"cs":1}],[{"t":"`字典.items()`","rs":1,"cs":1},{"t":"获取字典中所有的键值对（每组键值对以元组的形式呈现）","rs":1,"cs":1},{"t":"dict_items","rs":1,"cs":1}]]}
```

### 5-7-4 循环遍历

``` python
# 字典不能使用 while 循环遍历，但可以使用 for 循环遍历
d1 = {"张三": 72, "李四": 60, "王五": 85}
for key in d1:
	print(f"{key}的成绩是{d1[key]}")
	
for key in d1.keys():
	print(f"{key}的成绩是{d1[key]}")
```

### 5-7-5 特点总结
1. 键值对结构：字典中的数据以 `key:value` 的形式存在，每个键都对应一个值。
2. 键唯一：字典中的键（key）不能重复，若重复则后写的会覆盖前写的。
3. 键不可变：键必须是不可变类型（如数字、字符串、元组等），而值可以是任意类型。
4. 不支持下标：字典中的元素不能通过下标取值。
5. 支持增删改查，支持 `for` 循环遍历。

> 字典是一种以“键”找“值”的映射型容器，当需要唯一标识 $\to$ 对应信息的结构时，首先字典。  

\# 8 通用操作  

``` python
# 以下这五个函数：既能定义对应的【空容器】，又能将【其它类型】转换为对应的数字类型

# 1. list 函数：1. 定义空列表。2. 将【可迭代对象】转换为列表。
res1 = list(range(8))
res2 = list("欢迎来到猪脚的世界")
res3 = list({10, 20, 30, 40, 50})
res4 = list({"张三": 72, "李四": 60, "王五": 85})
print(type(res1), res1)  # <class 'list'> [0, 1, 2, 3, 4, 5, 6, 7]
print(type(res2), res2)  # <class 'list'> ['欢', '迎', '来', '到', '猪', '脚', '的', '世', '界']
print(type(res3), res3)  # <class 'list'> [50, 20, 40, 10, 30]
print(type(res4), res4)  # <class 'list'> ['张三', '李四', '王五']

# 2. tuple 函数：1. 定义空元组。2. 将【可迭代对象】转换为元组。
res1 = tuple(range(8))
res2 = tuple("欢迎来到猪脚的世界")
res3 = tuple({10, 20, 30, 40, 50})
res4 = tuple({"张三": 72, "李四": 60, "王五": 85})
print(type(res1), res1)  # <class 'tuple'> (0, 1, 2, 3, 4, 5, 6, 7)
print(type(res2), res2)  # <class 'tuple'> ('欢', '迎', '来', '到', '猪', '脚', '的', '世', '界')
print(type(res3), res3)  # <class 'tuple'> (50, 20, 40, 10, 30)
print(type(res4), res4)  # <class 'tuple'> ('张三', '李四', '王五')

# 3. set 函数：1. 定义空集合。2. 将【可迭代对象】转换为集合。
res1 = set(range(8))
res2 = set("欢迎来到猪脚的世界")
res3 = set({10, 20, 30, 40, 50})
res4 = set({"张三": 72, "李四": 60, "王五": 85})
print(type(res1), res1)  # <class 'set'> {0, 1, 2, 3, 4, 5, 6, 7}
print(type(res2), res2)  # <class 'set'> {'来', '的', '界', '欢', '世', '猪', '迎', '脚', '到'}
print(type(res3), res3)  # <class 'set'> {50, 20, 40, 10, 30}
print(type(res4), res4)  # <class 'set'> {'李四', '张三', '王五'}

# 4. str 函数：1. 定义空字符串。2. 将【任意类型】转换为空字符串。
res1 = str(range(8))
res2 = str("欢迎来到猪脚的世界")
res3 = str({10, 20, 30, 40, 50})
res4 = str({"张三": 72, "李四": 60, "王五": 85})
print(type(res1), res1)  # <class 'str'> range(0, 8)
print(type(res2), res2)  # <class 'str'> 欢迎来到猪脚的世界
print(type(res3), res3)  # <class 'str'> {50, 20, 40, 10, 30}
print(type(res4), res4)  # <class 'str'> {'张三': 72, '李四': 60, '王五': 85}

# 5. dict 函数：1. 定义空字典。2. 将【可迭代对象】转换为字典。
# 备注：交给 dict 函数的内容必须是键值对才可以，否则就会报错
res1 = dict([("张三", 75), ("李四", 60), ("王五", 85)])
res2 = dict((("张三", 75), ("李四", 60), ("王五", 85)))
res3 = dict({("张三", 75), ("李四", 60), ("王五", 85)})
print(type(res1), res1)  # <class 'dict'> {'张三': 75, '李四': 60, '王五': 85}
print(type(res2), res2)  # <class 'dict'> {'张三': 75, '李四': 60, '王五': 85}
print(type(res3), res3)  # <class 'dict'> {'李四': 60, '张三': 75, '王五': 85}

# 所有的数据容器，都支持成员运算符：in / not in 作用：判断某个“元素”是否在于容器中。
hobby = ["抽烟", "喝酒", "探头"]
nums = (10, 20, 30, 40, 50)
message = "hello, ProkyHoof"
citys = {"北京", "天津", "上海", "重庆"}
score = {"张三": 75, "李四": 60,  "王五": 85}
print("喝酒" in hobby)  # True
print(20 in nums)  # True
print("hoof" in message)  # False
print("上海" in citys)  # True
print("猪脚" in score)  # False
```

\# 9 练习  
### 5-9-1 练习一：水果清单
需求 1：打印所有的水果。  
需求 2：找到最贵的水果。  

``` python
fruits = {
	"苹果": 4.5,
	"香蕉": 3.2,
	"橙子": 5.8,
	"草莓": 12.0,
	"哈密瓜": 8.8
}

for key in fruits:
	print(f"水果：{key}，价格：{fruits[key]}")
key = max(fruits, key=fruits.get)
print(f"最贵的水果是{key}，其价格是{fruits.get(key)}")  # 最贵的水果是草莓，其价格是12.0
```

### 5-9-2 练习二：学生成绩单
需求 1：计算每位学生的平均分。  
需求 2：找到总分最高的学生。  

``` python
students = [
	{
		"name": "张三",
		"scores": {"语文": 88, "数学": 92, "英语": 95}
	},
	{
		"name": "李四",
		"scores": {"语文": 75, "数学": 83, "英语": 80}
	},
	{
		"name": "王五",
		"scores": {"语文": 92, "数学": 95, "英语": 88}
	}
]

# 计算每位学生的平均值
for student in students:
	# 获取当前学生的成绩列表
	score_list = list(student["scores"].values())
	# 计算平均值
	avg = sum(score_list) / len(score_list)
	print(f"{student["name"]}的平均分是{avg:.1f}")

# 找到总分最高的学生
def find_best():
	# 记录分数最高的学生
	best_student = list()
	# 记录最高分
	best_score = 0
	# 循环遍历
	for student in students:
		# 获取学生的总成绩
		total = sum(student["scores"].values())
		# 当前学生的成绩如果大于 best_score 就会更新数据
		if total > best_score:
			best_score = total
			best_student = [student["name"]]
		elif total == best_score:
			best_student.append(student["name"])
	print(f"最高分为{best_score}，取得最高分的学生有：{best_student}")

find_best()
```

### 5-9-3 练习三：评论内容
需求 1：统计“好喝”出现的次数。  
需求 2：将字符串中的“贵”替换为“略高”。  
需求 3：是否包含“推荐”两个字。  

``` python
comment = "这家奶茶真好喝，环境也不错，就是价格有点贵，好喝好喝好喝！强烈推荐！"
print(comment.count("好喝"))
res = comment.replace("贵", "略高")
print(res)
print("推荐" in comment)
```

\# 10 总结  
有序与无序：  
* 有序：列表（list）、元组（tuple）、字符串（str）——元素有顺序，可通过下标访问元素。
* 无序：集合（set）、字典（dict）——元素没有固定位置，不能用下标访问。

可修改：  
* 可变：列表、集合、字典——可以对内容进行增、删、改操作。
* 不可变：元组、字符串——内容固定，创建后无法修改。

可修复：  
* 允许重读：列表、元组、字符串。
* 不允许重复；集合、字典。备注：字典的 key 是唯一的，但 value 可重复。

```vtable
{"rows":[[{"t":"对比项","rs":1,"cs":1},{"t":"列表 list","rs":1,"cs":1},{"t":"元组 tuple","rs":1,"cs":1},{"t":"字符串 str","rs":1,"cs":1},{"t":"集合 set","rs":1,"cs":1},{"t":"字典 dict","rs":1,"cs":1}],[{"t":"是否支持多个元素","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1}],[{"t":"元素类型","rs":1,"cs":1},{"t":"任意","rs":1,"cs":1},{"t":"任意","rs":1,"cs":1},{"t":"仅字符","rs":1,"cs":1},{"t":"任意\n（元素应为不可变类型）","rs":1,"cs":1},{"t":"key：不可变类型\nvalue：任意的类型","rs":1,"cs":1}],[{"t":"是否支持重复","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"否","rs":1,"cs":1},{"t":"key：不能重复\nvalue：可以重复","rs":1,"cs":1}],[{"t":"是否有序","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"否","rs":1,"cs":1},{"t":"否","rs":1,"cs":1}],[{"t":"是否支持下标","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"否","rs":1,"cs":1},{"t":"否（可以通过 key 访问 value）","rs":1,"cs":1}],[{"t":"是否可修改","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"否","rs":1,"cs":1},{"t":"否","rs":1,"cs":1},{"t":"是","rs":1,"cs":1},{"t":"是","rs":1,"cs":1}],[{"t":"定义符号","rs":1,"cs":1},{"t":"[]","rs":1,"cs":1},{"t":"()","rs":1,"cs":1},{"t":"\"\"或''","rs":1,"cs":1},{"t":"{}","rs":1,"cs":1},{"t":"{key: value}","rs":1,"cs":1}],[{"t":"使用场景","rs":1,"cs":1},{"t":"可增删改查、可重复的多个数据","rs":1,"cs":1},{"t":"不可修改、可重复的多个数据","rs":1,"cs":1},{"t":"文本处理","rs":1,"cs":1},{"t":"去重、集合运算","rs":1,"cs":1},{"t":"通过 key 查找 value 的映射数据","rs":1,"cs":1}]]}
```


# 6 面向对象

## 6-1 概述
对象：一个拥有【属性】和【行为】的个体，是构成现实世界和程序世界的基本单位。  
面对对象：一种以对象为中心去思考和组织代码的方式，它更关注：“谁来做这件事”  
类（class）：用来描述一类事物的“模板”，它规定了一类事物所具有的【属性】和【行为】。  
实例（instance）：根据【类】创建出来一个具体的【对象】就是【实例】（实例对象）。

> 类是抽象的，实例是具体的。  

实例化：根据类“制作出”对象的过程，就叫实例化。  

\# 2 类的定义  

``` python
# 定义一个 Person 类（类名通常使用：大驼峰写法）
class Person:
	# 说明：当一个函数被定义在了类中时，那这个函数就被称为：方法。
	# __init__ 方法：初始化方法，主要作用：给当前正在创建的实例对象添加属性。
	# __init__ 方法收到的参数：当前正在创建的实例对象（self）、其他的自定义参数。
	# 当我们以后编写代码去创建 Person 类实例的时候，Python 会自动调用 __init__
	def __init__(self, name, age, gender):
		# 给实例添加属性（语法为：self.属性名 = 值）
		self.name = name
		self.age = age
		self.gender = gender
```

\# 3 创建实例  

``` python
# 创建 Person 类的实例对象
p1 = Person("bot", 18, "male")
p2 = Person("anay", 18, "female")

# 如果直接打印一个实例的化，我们是看不到实例身上的属性的
print(p1)  # <__main__.Person object at 0x1123908>
print(p2)  # <__main__.Person object at 0xb6ecf0>

# 通过点语法可以访问或修改实例身上的属性
print(p1.name)  # bot
print(p1.age)  # 18
print(p1.gender)  # male
print("-" * 20)  # --------------------
print(p2.name)  # anay
print(p2.age)  # 18
print(p2.gender)  # female

# 通过实例.__dict__ 可以查看实例身上的所有属性
print(p1.__dict__)  # {'name': 'bot', 'age': 18, 'gender': 'male'}
print(p2.__dict__)  # {'name': 'anay', 'age': 18, 'gender': 'female'}

# 实例创建完毕后，依然可以通过 实例.属性名 = 值 去给实例追加属性
p1.address = "猪脚世界"
print(p1.__dict__)  # {'name': 'bot', 'age': 18, 'gender': 'male', 'address': '猪脚世界'}

# 通过 type 函数，可以查看某个实例对象，是由哪个类创建出来的
print(type(p1))  # <class '__main__.Person'>
print(type(p2))  # <class '__main__.Person'>
```

\# 4 自定义方法  

``` python
# 定义一个 Person 类
class Person:
	# 初始化方法（给实例添加属性）
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender
	
	# 自定义方法（给实例添加行为）
	# speak 方法收到的参数是：调用 speak 方法的实例对象{self}、其他参数
	# speak 方法只有一份，保存在 Person 类身上的，所有 Person 类的实例对象，都可以调用 speak 方法
	def speak(self, msg):
		print(f"我叫{self.name}，年龄是{self.age}，性别是{self.gender}，我想说：{msg}")

p1 = Person("Bot", 18, "male")
p2 = Person("Anay", 18, "female")

# {'__module__': '__main__', '__init__': <function Person.__init__ at 0x10cd2e0>, 'speak': <function Person.speak at 0xf01c08>, '__dict__': <attribute '__dict__' of 'Person' objects>, '__weakref__': <attribute '__weakref__' of 'Person' objects>, '__doc__': None}
print(Person.__dict__)

print(p1.__dict__)  # {'name': 'Bot', 'age': 18, 'gender': 'male'}
print(p2.__dict__)  # {'name': 'Anay', 'age': 18, 'gender': 'female'}
p1.speak("我是猪脚")  # 我叫Bot，年龄是18，性别是male，我想说：我是猪脚
p2.speak("我是ProkyHoof")  # 我叫Anay，年龄是18，性别是female，我想说：我是ProkyHoof
```

> 方法保存在类身上，实例对象无法查找到方法，但是所有类的实例对象都是可以调用类的方法。  
> 当实例对象调用类方法时，查找方法的过程：  
> 1. 实例对象自身去寻找方法。如果有就调用该方法。  
> 2. 实例对象如果在自身没有寻找到方法，就去实例的“缔造者”的身上进行寻找。  

\# 5 实例属性  
通过【实例.属性名 = 值】给实例添加的属性，就叫实例属性。
实例属性只能通过实例访问，不能通过类访问。  

``` python\
class Person:
	def __init__(self, name, age, gender):
		# 实例属性
		self.name = name
		self.age = age
		self.gender = gender

print(Person.name)  # 错误
```

> 每个实例都有自己【独一份的】实例属性，各个实例之间是互不干扰的。   

\# 6 类属性  
类属性是保存在类身上的。  
类属性可以通过类访问，也可以通过实例访问。  
类属性通常用于保存：公共数据。

``` python
class Person:
	# 类属性
	max_age = 120
	planet = "地球"
	# 给实例添加属性
	def __init__(self, name, age, gender):
		self.name = name
		# 限制 age 的最大值
		if age <= Person.max_age:
			self.age = age
		else:
			print(f"年龄超出范围了，已经将年龄设置为最大值：{Person.max_age}")
			self.age = Person.max_age
		self.gender = gender
		
p1 = Person("Bot", 121, "male")  # 年龄超出范围了，已经将年龄设置为最大值：120
p1.planet = "火星"
print(Person.__dict__)  # {'__module__': '__main__', 'max_age': 120, 'planet': '地球', '__init__': <function Person.__init__ at 0xeac9c8>, '__dict__': <attribute '__dict__' of 'Person' objects>, '__weakref__': <attribute '__weakref__' of 'Person' objects>, '__doc__': None}
print(p1.__dict__)  # {'name': 'Bot', 'age': 120, 'gender': 'male', 'planet': '火星'}
print(Person.planet)  # 地球
print(p1.planet)  # 火星
```

> 进行【实例.属性名 = 值】操作时，只会对实例自身的属性起作用，不会影响类属性。  

\# 7 实例方法  
实例方法都是保存在类身上的，但是都需要实例去调用。  

``` python
class Person:
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender

	def speak(self, msg):
		print(f"我叫{self.name}，年龄是{self.age}，性别是{self.gender}，我想说：{msg}")
		
	def run(self, distance):
		print(f"{self.name}疯狂的奔跑了{distance}米")
		
p1 = Person("Bot", 18, "male")
p2 = Person("Anay", 18, "female")

# 通过实例调用实例方法
p1.speak("你好")  # 我叫Bot，年龄是18，性别是male，我想说：你好
p1.run(100)  # Bot疯狂的奔跑了100米

# 通过类去调用实例方法(能调用，但不推荐)
Person.run(p2, 100)  # Anay疯狂的奔跑了100米
```

\# 8 类方法  
使用 `@classmethod` 装饰过的方法，就叫类方法。  
类方法收到的参数：当前类本身（`cls`）、自定义的参数。  
因为收到了 `cls` 参数，所以类方法中是可以访问类属性的。  
类方法通常用于实现：与类相关的逻辑，例如：操作类级别的信息，一些工厂方法。

``` python
from datetime import datetime

class Person:
	max_age = 120
	planet = "地球"
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender

	def speak(self, msg):
		print(f"我叫{self.name}，年龄是{self.age}，性别是{self.gender}，我想说：{msg}")
		
	def run(self, distance):
		print(f"{self.name}疯狂的奔跑了{distance}米")
	
	@classmethod
	def change_planet(cls, planet):
		cls.planet = planet
	
	@classmethod
	def create(cls, info_str):
		# 从 info_str 中获取到有效信息
		name, year, gender = info_str.split("-")
		# 获取当前年份
		current_year = datetime.now().year
		# 计算年龄
		age = current_year - int(year)
		# 创建并返回一个 Person 类的实例对象
		return cls(name, age, gender)
		
# 类方法需要通过类调用
Person.change_planet("月球")
print(Person.__dict__)  # {'__module__': '__main__', 'max_age': 120, 'planet': '月球', '__init__': <function Person.__init__ at 0xf68898>, 'speak': <function Person.speak at 0x10df220>, 'run': <function Person.run at 0xe216d0>, 'change_planet': <classmethod(<function Person.change_planet at 0xae3b08>)>, 'test2': <classmethod(<function Person.test2 at 0x1219228>)>, '__dict__': <attribute '__dict__' of 'Person' objects>, '__weakref__': <attribute '__weakref__' of 'Person' objects>, '__doc__': None}

p3 = Person.create("jack-2004-male")
print(p3.__dict__)  # {'name': 'jack', 'age': 22, 'gender': 'male'}
```

> 类方法，也能通过实例调用到，但是非常不推荐。

``` python
info_str = "bot-2004-male"
name, year, gender = info_str.split("-")
print(name, year, gender)  # bot 2004 male
```

\# 9 静态方法  
使用 `@staticmethod` 装饰过的方法，就叫：静态方法，静态方法也是保存在类身上的。  
静态方法只是单纯的定义在类中，它不会收到：`self`、`cls` 参数，它收到的参数都是自定义参数。  
由于静态方法没有收到：`self`、`cls` 参数，所以其内部不会访问任何、类和实例相关的内容。 静态方法通常用于定义：与类相关的工具方法。  
 


``` python
from datetime import datetime

class Person:
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender

	# 静态方法
	@staticmethod
	def is_adult(year):
		# 获取当前的年份
		current_year = datetime.now().year
		# 计算年龄
		age = current_year - year
		# 返回结果（成年 True，未成年 False）
		return age >= 18

	@staticmethod
	def mask_idcard(idcard):
		return idcard[:6] + "********" + idcard[-4:]

res = Person.is_adult(2011)
print(res)  # False

res2 = Person.mask_idcard("340881200406060722")
print(res2)  # 340881********0722
```

> 注意点：通过实例也能调用到静态方法，但是非常不推荐。

\# 10 继承  

``` python
class Person:
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender

	def speak(self, msg):
		print(f"我叫{self.name}，年龄是{self.age}，性别是{self.gender}，我想说：{msg}")

# 定义一个 Student 类（子类、派生类），继承自 Person 类（父类、超类、基类）
class Student(Person):
	def __init__(self, name, age, gender, stu_id, grade):
		# 在子类中，有两种方式去调用父类的初始化方法，来实现对继承属性：name, age, gender
		# 方法一：
		# super().__init__(name, age, gender)
		# 方法二
		Person.__init__(self, name, age, gender)
		
		# 子类独有的属性，需要自己动手完成初始化
		self.stu_id = stu_id
		self.grade = grade
		
s1 = Student("bot", 18, "male", "2022001", "大一")
print(s1.__dict__)  # {'name': 'bot', 'age': 18, 'gender': 'male', 'stu_id': '2022001', 'grade': '大一'}
print(type(s1))  # <class '__main__.Student'>

s1.speak("我是猪脚")  # 我叫bot，年龄是18，性别是male，我想说：我是猪脚
```

查找 `speak1` 方法的过程：  
1. 查找实例对象有没有方法。
2. 查找实例对象的类有没有方法。
3. 查找实例对象的类的父类有没有方法。

\# 11 方法重写  
方法重写是当子类中定义了一个与父类中相同的方法，那么子类中的方法就会“覆盖”父类的方法。  

``` python
class Person:
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender

	def speak(self, msg):
		print(f"我叫{self.name}，年龄是{self.age}，性别是{self.gender}，我想说：{msg}")

# 定义一个 Student 类，继承自 Person 类
class Student(Person):
	def __init__(self, name, age, gender, stu_id, grade):
		super().__init__(name, age, gender)
		self.stu_id = stu_id
		self.grade = grade
	
	def speak(self, msg):
		super().speak(msg)
		print(f"我是学生，我的学号是{self.stu_id}，我正在读{self.grade}，我想说：{msg}")

s1 = Student("bot", 18, "male", "2022001", "freshman")
s1.speak("好好学习")  
# 我叫bot，年龄是18，性别是male，我想说：好好学习
# 我是学生，我的学号是2022001，我正在读freshman，我想说：好好学习
```

\# 12 两个常用方法  
方法 1：`isinstance(instance, Class)`，作用：判断某个对象是否为指定类或其子类的实例。  
方法 2：`issubclass(Class1, Class2)`，作用：判断某个类是否是另一个类的子类。  

``` python
class Person:
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender

	def speak(self, msg):
		print(f"我是{self.name}，我的年龄是{self.age}，我是{self.gender}生，我想说：{msg}")

class Student(Person):
	def __init__(self, name, age, gender, stu_id, grade):
		super().__init__(name, age, gender)
		self.stu_id = stu_id
		self.grade = grade

p1 = Person("bot", 18, "male")
s1 = Student("lisi", 18, "male", "2022001", "freshman year")

res1 = isinstance(s1, Student)
res2 = isinstance(s1, Person)
res3 = isinstance(p1, Student)
print(res1, res2, res3)  # True True False

print(issubclass(Student, Person))  # True
print(issubclass(Person, Student))  # False
```

\# 13 多重继承  
概念：多重继承指一个类同时继承多个父类，从而拥有多个父类的属性和方法。  

``` python
class Person:
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender

	def speak(self, msg):
		print(f"我是{self.name}，我的年龄是{self.age}，我是{self.gender}生，我想说：{msg}")

class Worker:
	def __init__(self, company):
		self.company = company
	
	def do_work(self):
		print(f"我在{self.company}做兼职")

class Student(Person, Worker):
	def __init__(self, name, age, gender, company, stu_id, grade):
		Person.__init__(self, name, age, gender)
		Worker.__init__(self, company)
		self.stu_id = stu_id
		self.grade = grade
	
	def study(self):
		print(f"我在努力的学习，争取做{self.grade}年级的第一名")

s1 = Student("bot", 18, "male", "McDonald", "2025001", "freshman year")
print(s1.__dict__)  # {'name': 'bot', 'age': 18, 'gender': 'male', 'company': 'McDonald', 'stu_id': '2025001', 'grade': 'freshman year'}
s1.speak("我是猪脚")  # 我是bot，我的年龄是18，我是male生，我想说：我是猪脚
s1.do_work()  # 我在McDonald做兼职
s1.study()  # 我在努力的学习，争取做freshman year年级的第一名

print(Student.__mro__)  # (<class '__main__.Student'>, <class '__main__.Person'>, <class '__main__.Worker'>, <class 'object'>)
```

类的 `__mro__` 属性：用于记录属性和方法的查找顺序。  
通过实例去查找属性或方法时，会先在实例自身上去查找，如果没有，就按找 `__mro__` 记录的顺序去查找。  

\# 14 三种访问权限  

``` python
class Person:
	def __init__(self, name, age, gender):
		self.name = name  # 共有属性：当前类中、子类中、类外部，都可以访问
		self._age = age  # 受保护的属性：当前类中，子类中，都可以访问
		self.__gender = gender  # 私有属性：仅能在当前类中访问
		
		def speak(self, msg):
			print(f"我是{self.name}，我的年龄是{self.age}，我是{self.gender}生，我想说：{msg}")
```

> 在类的外部，如果强制访问【受保护的属性】也能访问到，但十分不推荐。
> 在类的外部，如果强制访问【私有属性】不能访问到，而且会报错。  
> Python 底层是通过重命名的方式，实现私有属性。  

```vtable
{"rows":[[{"t":"权限类型","rs":1,"cs":1},{"t":"定义方式","rs":1,"cs":1},{"t":"在当前类内部访问","rs":1,"cs":1},{"t":"在子类内部访问","rs":1,"cs":1},{"t":"在类外部访问","rs":1,"cs":1}],[{"t":"公有属性","rs":1,"cs":1},{"t":"`属性名`","rs":1,"cs":1},{"t":"能","rs":1,"cs":1},{"t":"能","rs":1,"cs":1},{"t":"能","rs":1,"cs":1}],[{"t":"受保护属性","rs":1,"cs":1},{"t":"`_属性名`","rs":1,"cs":1},{"t":"能","rs":1,"cs":1},{"t":"能","rs":1,"cs":1},{"t":"能（但不推荐）","rs":1,"cs":1}],[{"t":"私有属性","rs":1,"cs":1},{"t":"`__属性名`","rs":1,"cs":1},{"t":"能","rs":1,"cs":1},{"t":"不能","rs":1,"cs":1},{"t":"不能","rs":1,"cs":1}]]}
```

\# 15 getter 与 setter  
`@property`：注册属性 `getter` 方法，当访问类实例的属性时，`getter` 方法就会被自动调用。  
`@属性.setter`：注册属性 `setter` 方法，当修改类实例的属性时，`setter` 方法就会被自动调用。

``` python
class Person:
	def __init__(self, name, age, gender):
		self.name = name  # 共有属性：当前类中、子类中、类外部，都可以访问
		self._age = age  # 受保护的属性：当前类中，子类中，都可以访问
		self.__gender = gender  # 私有属性：仅能在当前类中访问
	
	# 注册 age 属性 getter 方法，当访问 Person 实例的 age 属性时，下面的 age 方法就会被自动调用
	@property
	def age(self):
		return self._age
	
	# 注册 age 属性 setter 方法，当修改 Person 实例的 age 属性时，下面的 age 方法就会被自动调用
	@age.setter
	def age(self, value):
		self._age = value

p1 = Person("bot", 18, "340881200406060722")
print(p1.age)  # 18
p1.age = 19
print(p1.age)  # 19
```

\# 16 魔法方法（魔术方法）
概念：以__xxx__ 命名的特殊方法（双下划线开头和结尾）。  
特点：不需要我们手动调，我们只要准备好这些方法，Python 会在特定场景下，去自动调取。  

``` python
class Person:
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender
	
	# 当执行 print(Person 的实例对象)或 str(Person 的实例对象)时调用
	def __str__(self):
		return f"{self.name}-{self.age}-{self.gender}"
	

p1 = Person("bot", 18, "male")
print(p1)
```

> 当 `print(p1)` 时，Python 会调用 `__str__` 方法，先去查找实例对象是否有 `__str__` 方法，如果没有就会在 `Person` 父类中查找，如果还是没有就会在 `object` 类中进行查找。

### 6-16-1 常见的魔法方法

```vtable
{"rows":[[{"t":"方法","rs":1,"cs":1},{"t":"调用时机","rs":1,"cs":1}],[{"t":"`__str__`","rs":1,"cs":1},{"t":"当调用`print(对象)`或`str(对象)`时","rs":1,"cs":1}],[{"t":"`__len__`","rs":1,"cs":1},{"t":"当调用`len(对象)`时","rs":1,"cs":1}],[{"t":"`__lt__`","rs":1,"cs":1},{"t":"当执行`对象1 &lt; 对象2`时","rs":1,"cs":1}],[{"t":"`__gt__`","rs":1,"cs":1},{"t":"当执行`对象1 &gt; 对象2`时","rs":1,"cs":1}],[{"t":"`__eq__`","rs":1,"cs":1},{"t":"当执行`对象1 == 对象2`时","rs":1,"cs":1}],[{"t":"`__getattr__`","rs":1,"cs":1},{"t":"当访问不存在的属性时","rs":1,"cs":1}]]}
```

\# 17 object 类  
Python 中，所有的类都继承了 object 类，即：object 类是所有类的顶层父类。  
因为 object 是所有类的父类，所以 Python 中的所有对象，都间接是 object 类的实例。  

``` python
print(issubclass(int, object))  # True
print(issubclass(list, object))  # True

print(isinstance(100, object))  # True
print(isinstance("猪脚", object))  # True
```

> 所有对象都继承了 object 类所提供的：各种属性和方法，从而保证了每个对象都具备统一的基本能力。  

``` python
print(p1.__dict__)  # 对象身上自己的东西
print(dir(p1))  # 对象可以访问到的东西（继承的东西）
```

\# 18 多态  
概念：同一个方法名，在不同的对象上调用时，呈现出不同的行为。
### 6-18-1 标准多态

``` python
class Animal:
	def speak(self):
		print("动物正在发出声音")

class Dog(Animal):
	def speak(self):
		print("汪汪汪")
	
class Cat(Animal):
	def speak(self):
		print("喵喵喵")	

def make_sound(animal:Animal):  # 类型注解
	# 多态的体现
	animal.speak()

# 创建实例对象
a1 = Animal()
d1 = Dog()
c1 = Cat()

make_sound(a1)  # 动物正在发出声音
make_sound(d1)  # 汪汪汪
make_sound(c1)  # 喵喵喵
```

### 6-18-2 鸭子多态
核心理念：如果一个东西看起来像鸭子，叫起来像鸭子，那它就是鸭子。  
鸭子类型是一种编程分割，它不检查对象的类型，只关注对象能否“做某件事”（是否有对应的方法）。  

``` python
class Animal:
	def speak(self):
		print("动物正在发出声音")

class Dog:
	def speak(self):
		print("汪汪汪")
	
class Computer:
	def speak(self):
		print("滋滋滋")

def make_sound(animal):
	animal.speak()

d1 = Dog()
c1 = Computer()

make_sound(d1)  # 汪汪汪
make_sound(c1)  # 滋滋滋
```

\# 19 抽象类  
【抽象类】是一种不能直接实例化的类，它通常作为“规范”，让子类去继承，并实例其中定义的【抽象方法】。  

``` python
from abc import ABC, abstractmethod

# Must 类一旦继承了 ABC 类，那么 MustRun 类就是抽象类了
class MustRun(ABC):
	@abstractmethod
	def run(self):
		pass

class Person(MustRun):
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender
	
	def run(self):
		print(f"{self.name}在努力的奔跑")

p1 = Person("bot", 18, "male")
p1.run()  # bot在努力的奔跑
```

> 1. 抽象类无法实例化，实例化抽象类的子类必须重写抽象方法。  
> 2. 抽象类中可以出现正常方法（实例方法，类方法，静态方法）。  

\# 20 小练习  
学生管理：  
1. 添加学生。
2. 删除学生。
3. 查看所有学生。
4. 录入成绩。
5. 退出。

``` python
from datetime import datetime

class Person:
	def __init__(self, name, age, gender):
		self.name = name
		self.age = age
		self.gender = gender

class Student(Person):
	count = 0
	
	def __init__(self, name, age, gender):
		super().__init__(name, age, gender)
		Student.count += 1
		self.stu_id = f"{datetime.now().year}{Student.count:03d}"
		self.scores = {}
	
	# 给当前学生添加成绩
	def add_score(self, subject, score):
		self.score[subject] = score
		
	# 计算平均分
	def calcu_avg(self):
		if self.scores:
			avg = sum(self.score.values()) / len(self.score)
			return float(f"{avg:.1f}")
		else:
			return 0
	
	# 魔法方法
	def __str__(self):
		return f"{self.name}({self.age}-{self.gender})，成绩：{self.scores}，平均分：{self.calcu_avg()}"

class Manager:
	def __init__(self):
		self.stu_list = []
	
	# 添加学生
	def add_student(self):
		name = input("请输入姓名：")
		age = int(input("请输入年龄："))
		gender = input("请输入性别：")
		stu = Student(name, age, gender)
		self.stu_list.append(stu)
		print(f"添加成功，学号是{stu.stu_id}")
	
	# 删除学生
	def del_student(self):
		sid = input("请输入学号：")
		target = None
		for stu in self.stu_list:
			if stu.stu_id == sid:
				target = stu
		if target:
			self.stu_list.remove(target)
			print("删除成功")
		else:
			print("学号有误，删除失败")
	
	# 展示所有学生
	def show_all_student(self):
		if self.stu_list:
			for stu in self.stu_list:
				print(stu)	
		else:
			print("暂无学生")
	
	# 给指定学生设置成绩
	def set_score(self):
		sid = input("请输入学号：")
		for stu in self.stu_list:
			if sid == stu.stu_id:
				score_str = input("请输入成绩（学科-分数，学科-分数）")
				score_list = score_str.replace("，", ",").split(",")
				for item in score_list:
					subject, score = item.split("-")
					score = float(score.strip())
					stu.add_score(subject, score)
				print("添加成功")
				return
		print("学号有误")

	def run(self):
		while True:
			print("------学生管理----")
			print("1. 添加学生")
			print("2. 删除学生")
			print("3. 查看所有学生")
			print("4. 录入成绩")
			print("5. 退出")

			option = input("请输入操作编号：")
			if option == "1":
				self.add_student()
			elif option == "2":
				self.del_student()
			elif option == "3":
				self.show_all_student()
			elif option == "4":
				self.set_score()
			elif option == "5":
				print("再见")
				break
			else:
				print("输入有误")
			
m1 = Manager()
m1.run()
```

\# 21 内存分析  

![1. 内存分析](../../../../03%20附件/Excalidraw/1.%20Python/1.%20内存分析.md)

``` python
a = 123
print(hex(id(a)))  # id() 输出变量的存储位置（十进制），hex() 将十进制转换为 十六进制
```

Python 中常见的不可变对象有：int、float、bool、str、tuple、frozenset、None。  
Python 中常见的可变对象有：list、dict、set、自定义类的实例对象。  

> 不可变对象只能进行重新创建，可变对象可以自身修改不改变地址。


# 7 函数进阶

## 7-1 重新认识函数
1. 函数也是对象。
2. 函数可以动态添加属性。
3. 函数可以赋值给变量。
4. 函数也可以作为参数。
5. 不可变参数和可变参数。
6. 函数也可以作为返回值。

``` python
# 函数也是对象
a1 = 100  # int 类的实例对象
a2 = "Hello"  # str 类的实例对象
a3 = [10, 20, 30]  # list 的实例对象

def welcome():
	print("你好")  # welcome 函数是 function 类的实例对象

print(type(welcome))  # <class 'function'>

# 函数可以动态添加属性
welcome.desc = "这是一个打招呼的函数"
welcome.version = 1.0
print(welcome.desc)  # 这是一个打招呼的函数
print(welcome.version)  # 1.0

# 函数可以赋值给变量
say_hello = welcome
say_hello()  # 你好
print(say_hello.desc)  # 这是一个打招呼的函数

# 可变参数和不可变参数的区别
# 不可变参数
a = 666
def welcome(data):
	print("data 修改前", data, id(data))  # data 修改前 666 15365680
	data = 888
	print("data 修改后", data, id(data))  # data 修改后 888 16461360

print("函数调用前", a, id(a))  # 函数调用前 666 15365680
welcome(a)
print("函数调用后", a, id(a))  # 函数调用后 666 15365680

# 可变参数
a = [10, 20, 30]
def welcome(data):
	print("data修改前", data, id(data))  # data修改前 [10, 20, 30] 16557032
	data[2] = 99
	print("data修改后", data, id(data))  # data修改后 [10, 20, 99] 16557032
print("函数调用前", a, id(a))  # 函数调用前 [10, 20, 30] 16557032
welcome(a)  # [10, 20, 30]
print("函数调用后", a, id(a))  # 函数调用后 [10, 20, 99] 16557032

# 函数也可以作为参数
def welcome():
	print("你好呀")

# 函数也可以作为返回值
def caller(f):
	print("caller函数调用了")
	f()

caller(welcome)  # caller函数调用了  你好呀

# 函数也可以作为返回值
def welcome():
	print("你好啊")
	def show_msg(msg):
		print(msg)
	return show_msg

result = welcome()
result("猪脚")  # 你好啊  猪脚
```

\# 2 多返回值  
### 7-2-1 参数的打包与解包
1. 打包接受参数：
`*args`：打包所有的位置参数（会形成一个元组）。  
`**kwargs`：打包所有的关键字参数（会形成一个字典）。  
2. 解包传递参数：
`*变量名`：将元组拆解成一个一个独立的位置参数。  
`**变量名`：将字典拆解一个一个 `key = value` 形式的关键字参数。  

``` python
# 函数的多返回值
def calculate(x, y):
	res1 = x + y
	res2 = x - y
	return res1, res2

result = calculate(30, 10)
print(result)  # (40, 20)

r1, r2 = calculate(30, 10)
print(r1, r2)  # 40 20

# 参数的打包与解包
def show_info(*args, **kwargs):
	print(args)
	print(kwargs)

show_info(10, 20, 30, name="张三", age=18, gender="男")
# (10, 20, 30)
# {'name': '张三', 'age': 18, 'gender': '男'}

# 解包传递参数
def show_info(num1, num2, num3, name, age, gender):
	print(num1, num2, num3)
	print(name, age, gender)
nums = (10, 20, 30)
person = {"name": "张三", "age": 18, "gender": "男"}

show_info(*nums, **person)

# 打包接受参数和解包传递参数一起使用
def show_info(*args, **kwargs):
	print(args)
	print(kwargs)
nums = (10, 20, 30)
person = {"name": "张三", "age": 18, "gender": "男"}
show_info(*nums, **person)
```

\# 3 高阶函数  
高阶函数：当一个函数的【参数是函数】或者【返回值是函数】那该函数就是【高阶函数】  
高阶函数的意义：  
1. 代码复用性高：可以把行为“独立出来”，传入不同函数实现不同逻辑。
2. 能让函数更灵活，更通用。
3. 高阶函数是：装饰器、闭包的基础。

``` python
def info(msg):
	return "[提示]：" + msg

def warn(msg):
	return "[警告]：" + msg

def error(msg):
	return "[错误]：" + msg

def log(func, text):
	print(func(text))

log(info, "文件保存成功")  # [提示]：文件保存成功
log(warn, "磁盘空间不足")  # [警告]：磁盘空间不足
log(error, "该用户不存在")  # [错误]：该用户不存在
```

\# 4 条件表达式  
表达式：执行后能得到值的代码，就是表达式（表达式最终会形成一个值，可以写在任何需要值的地方）。  
条件表达式：根据条件的真假，在两个结果中二选一的表达式（又称：三元表达式、三目运算符）。  

``` python
# 表达式
a1 = 3 + 5
a2 = "abc" * 3
a3 = 5 > 3
a4 = "y" in "python"
a5 = len("hello")

# 条件表达式
age = 18
res = "成年" if age >= 18 else "未成年"
print(res)  # 成年
```

条件表达式的使用场景：简单的二选一场景。  

\# 5 匿名函数  
概念：所谓【匿名函数】，就是没有名字的函数，它无需使用 def 关键字去定义。  
语法：Python 中使用 lambda 关键字来定义【匿名函数】，格式为：lambda 参数：表达式。  
使用场景：当一个函数只用一次，只做一点点小事，使用匿名函数会更简洁。  

``` python
# 使用普遍函数实现计算结果
def calculate(func, a, b):
	print(f"计算结果为：{func(a, b)}")

calculate(lambda x, y: x + y, 30, 20)  # 计算结果为：50
calculate(lambda x, y: x - y, 30, 20)  # 计算结果为：10
```

>注意点：    
>1. 只能写一行，不能写多行代码。  
>2. 不能写代码块（`if`、`for`、`while`）。  
>3. 冒号右边必须是表达式，且只能写一个表达式。  
>4. 表达式结果自动作为返回值。

``` python
is_adult = lambda age: "成年" if age >= 18 else "未成年"
print(is_adult(13))  # "未成年"
print(is_adult(18))  # "成年"
```

\# 6 数据处理  
### 7-6-1 map 函数
map 函数：对一组数据中的每一个元素，统一执行某种操作（加工），并生成一组新数据。  
语法格式：map（操作函数，可迭代对象）  

``` python
# 统一数据处理
nums = [10, 20, 30, 40]

# map 函数的返回值是一个迭代器对象，需要我们自己手动便利，或者手动类型转换
res = map(lambda x: x * 2, nums)
print(list(res))  # [20, 40, 60, 80]

# 字符串转换
names = ("python", "java", "js")
res = map(lambda x: x.upper(), names)
print(list(res))  # ['PYTHON', 'JAVA', 'JS']

# 类型转换
str_number = {"1", "2", "3"}
res = map(int, str_number)
print(set(res))  # {1, 2, 3}
```

> 注意点：  
> 1. 延迟执行：`map` 不会立即计算，只有在“需要结果”时才执行计算。  
> 2. 返回的是迭代器对象，且一旦遍历完成，就会被“耗尽”。  
> 3. `map` 不会影响元素数量。  

### 7-6-2 filter 函数
`filter` 函数：从一组数据中，筛选出符合条件的元素（过滤），并组成一组新数据。  
语法格式：`filter(过滤函数，可迭代对象)`。  

``` python
# 筛选数值
nums = [10, 20, 30, 40, 50]
res = filter(lambda n: n > 30, nums)
print(list(res))  # [40, 50]

# 过滤一下非法字符串
names = ["张三", "", "李四", None, "王五"]
res = filter(lambda name: name, names)
print(list(res))  # ['张三', '李四', '王五']
```

> 注意点：
> 1, `filter` 不会立刻筛选，只有在“需要结果”时才执行。  
> 2. 返回的是迭代器对象，且一旦遍历完成就会被“耗尽”。  
> 3. `filter` 可能会影响元素数量。  

`filter` 函数的特殊用法：如果不传递过滤函数，那么自动会过滤掉“假值”。  

``` python
data = [0, 1, "", "hello", [], (), 5]
res = filter(None, data)
print(list(res))  # [1, 'hello', 5]
```
### 7-6-3 sorted 函数
`sorted` 函数：对一组数据进行排序，返回一组新数据。  
语法格式：`sorted(可迭代对象, key=xxx, reverse=xxx)`  

``` python
# 数据排序
nums = [30, 40, 20, 10]
res = sorted(nums)
print(res)  # [10, 20, 30, 40]

# 按照字符串的长度去排序
names = ["python", "sql", "java"]
res = sorted(names, key=lambda n: len(n))
print(res)  # ['sql', 'java', 'python']
res2 = sorted(names, key=len, reverse=True)
print(res2)  # ['python', 'java', 'sql']
```

### 7-6-4 reduce 函数
reduce 函数：将一组数据不断“合并”，最终归并成一个结果。  
语法格式：`reduce(合并函数, 可迭代对象, 初始值)`  
备注：`reduce` 函数需要从 `functools` 模块中引入才能使用。  

``` python
# 从 functools 模块中引入 reduce
from functools import reduce

# 数据统计
nums = [1, 2, 3, 4, 5]
def count(a, b):
	return a + b

res = reduce(count, nums)
print(res)  # 15

# 字符串拼接
str_list = ["ab", "cd", "ef"]
res = reduce(lambda a, b: a + b, str_list)
print(res)  # abcdef
```

\# 7 列表推导式  
列表推导式：用一条简洁语句，从可迭代对象中，生成新列表的语法结构。  
备注：列表推导式本质上是对 `for` 循环 + `append()` 的一种简写形式。  
语法格式：`[表达式 for 变量 in 可迭代对象]`  

``` python
# 需求：让列表中每个元素，都变为原来的 2 倍，得到是一个新的结果。
nums = [10, 20, 30, 40]
res = [n * 2 for n in nums]
print(res)  # [20, 40, 60, 80]

# 带条件的列表推导式
nums = [10, 20, 30, 40]
res = [n * 2 for n in nums if n > 20]
print(res)  # [60, 80]
```

``` python
# 字典推导式
names = ["张三", "李四", "王五"]
scores = [60, 70, 80]
res = {names[i]: scores[i] for i in range(len(names))}
print(res)  # {'张三': 60, '李四': 70, '王五': 80}

# 集合推导式
names = ["张三", "李四", "王五"]
res = {name + "!" for name in names}
print(res)  # {'张三!', '李四!', '王五!'}
```

> Python 中没有元组推导式。  

\# 8 常用内置函数  
### 7-8-1 输入与输出
`print()`：输出指定内容。  

``` python
# 完整参数：print(*object, sep=" ", end="\n", file=sys.stdout, flush=False)
# 参数详解：
# 1. object：要输出的内容。
# 2. sep：分隔符。
# 3. end：结束符。
# 4. file：输出位置。
# 5. flush：是否立即刷新。
from time import sleep

for index in range(1, 101):
	print(f"\r已加载{index}%", end="", flush=True)
	sleep(0.1)
```
`input()`：获取用户输入。  
### 7-8-2 类型转换
`int()`：转为整数。  
`float()`：转为浮点数。  
`str()`：转为字符串。  
`bool()`：转为布尔值。
`list()`：转为列表。
`tuple()`：转为元组。
`set()`：转为集合。
`dict()`：转为字典。
### 7-8-3 数学相关
`abs()`：取绝对值。  
`round()`：四舍五入。  

> 注意：`round` 函数的四舍五入，是银行家舍入法：小于 5 就舍，大于 5 就入，等于 5 看奇偶（奇入偶舍）。  

`pow()`：次方。  
`divmod()`：商和余数。  
`max()`：最大值（支持 key 函数）。  
`min()`：最小值（支持 key 函数）。  
`sum()`：求和。  
`map()`：加工一组数据。  
`filter()`：按条件过滤数据（支持 key 函数）。  
`reduce()`：合并计算（需导入 functools）。  
`sorted()`：排序（支持 key 函数）。  
### 7-8-4 数据容器相关
`len()`：获取容器中元素的个数。  
`range()`：给序列添加索引。  
`sorted()`：对序列进行排序。返回新列表。  
`enumerate()` ：给序列添加索引。
`zip()`：将多个序列一一配对。  
### 7-8-5 类型判断与对象相关
`type()`：查看类型。  
`isinstance()`：判断类型。  
`issubclass()`：判断两个类的继承关系。  
`id()`：查看对象的内存地址。  
### 7-8-6 逻辑判断相关
`all()`：全为真返回 `True`。  
`any()`：有一个为真即可。  
### 7-8-7 字符床辅助相关
`ord`：获取字符的 Unicode 编码值。  
`chr()`：将 Unicode 编码值转为字符。  
\# 9 浅拷贝和深拷贝  
直接赋值：两个变量指向同一个对象，修改其中一个，就会影响另一个（互相影响）。  

``` python
import copy

nums1 = [10, 20, 30, 40]
nums2 = nums1
nums2[3] = 99
print(nums1)  # [10, 20, 30, 99]
```

浅拷贝：创建一个新的外层容器，但内部元素仍然引用原来的对象.  

``` python
nums1 = [10, 20, 30, 40]
nums2 = copy.copy(nums1)
print(id(nums1))  # 14568848
print(id(nums2))  # 17730576
```

> 浅拷贝存在的问题：
> 嵌套数据仍然是共享的，修改嵌套数据会相互影响。  

深拷贝：创建一个新的外层容器，并对其内部所有的可变对象进行递归复制。  

``` python
nums1 = [10, 20, 30, [40, 50]]
nums2 = copy.deepcopy(nums1)

print(id(nums1))  # 11901320
print(id(nums2))  # 14568848
```

> 备注：  
> 1. 深拷贝可以彻底消除数据之间的相互影响。  
> 2. 深拷贝遇到【不可变对象】不会复制，会直接引用。  

> 注意点：  
> 1. 深拷贝只复制可变对象，不可变对象会直接引用。  
> 2. 元组中如果只包含不可变对象，则深拷贝没有效果。  

\# 10 四种作用域  

``` python
a = 100

def test(b):
	print("我是test函数")
	print("test中打印的a是", a)  # 100
	print("test收到的参数b是", b)  # 66
	
	c = 200
	d = 300
	print("test中的c和d分别是", c, d)  # 200 300
	
	def inner():
		e = 400
		nonlocal c
		c = 999
		print("inner 中的 e 是", e)  # 400
		print("inner 中打印的是", c)  # 999
	
	inner()

print("全局打印的 a 是", a)  # 100
test(66)
```

* python 中有四种作用域，分别是：Local、Enclosing、Global、Built-in。  
* 当访问一个变量时，Python 会按一下顺序查找：Local $\to$ Enclosing $\to$ Global $\to$ Built-in。
### 7-10-1 局部作用域（Local）
定义：函数的内部就是局部作用域，局部作用域中的变量，只能在该函数内部可见。  
特点：  
* 每次调用函数都会创建一个新的局部作用域。
* 函数运行结束后，局部作用域随之销毁。
* 局部作用域优先级最高（LEGB 中的 L）。

### 7-10-2 外部作用域（Enclosing）
定义：如果函数中又定义了函数，那么外层函数的作用域，就是内层函数的 Enclosing 作用域。  
特定：  
* 只有当函数“嵌套定义”时才会出现。
* 内层函数可以读取外层函数变量。
* 想修改外层变量必须使用 `nonlocal`。

### 7-10-3 全局作用域（Global）
定义：`.py` 文件就是全局作用域，全局作用域中的变量，在当前 `.py` 文件的任何位置都可以访问。  
特点：  
* 全局变量只在当前 `.py` 文件中可见。
* 函数内部可以使用 `global` 关键字修改全局变量。

### 7-10-4 内建作用域（Built-in）
定义：Python 预先定义好的东西，会放在内建作用域中，所有 `.py` 文件都可以直接使用。  
特点：  
* 所有 `.py` 文件都能直接使用其中的名称。
* 例如：`print`、`len`、`range`、`sum`、`max` 等。
* 查找优先级最低（LEGB 中的 B）。

\# 11 闭包  
1. 每次调用函数时，Python 都会为函数创建一个新的局部作用域。
2. 函数执行完毕后，这个局部作用域会被销毁，其中的局部变量也会随之被释放。

``` python
def outer():
	num = 10
	num += 1
	print(num)

outer()  # 11
outer()  # 11
```

1. 在 Python 中，【内层函数】可以访问其【外层函数】作用域中的变量。
2. 访问外层函数变量无需使用 nonlocal；但修改外层变量时要使用 nonlocal。

``` python
def outer():
	num = 10
	
	def inner():
		nonlocal num
		num = 99
		print(1, num)  # 1 99
	
	inner()
	print(2, num)  # 2 99

outer()
```

``` python
# 闭包
def outer():
	num = 10
	
	def inner():
		nonlocal num
		num += 1
		print(num)
		
	return inner

f = outer()
f()  # 11
f()  # 12
f()  # 13

# 打印 __closure__ 元组
print(f.__closure__)  # (<cell at 0x1060b68: int object at 0x319528>,)

# 打印 __closure__ 元组中的某一项
print(f.__closure__[0])  # <cell at 0x1060b68: int object at 0x319528>

# 打印 __closure__ 元组中的某一项的具体值
print(f.__closure__[0].cell_contents)  # 13
```

> 结论：  
> 1. `outer` 函数中，被 `inner` 所使用到的那些变量，会被封存到【闭包单元（cell）】中。  
> 2. 这些 cell 会组成一个 `__closure__` 元组，最终放在了 `inner` 函数身上。  

什么是闭包：闭包 = 内层函数（`inner`） + 被内层函数所引用的外层变量（`inner.__closure__`）。  
闭包产生的条件：  
1. 要有函数嵌套。
2. 在【内层函数】中，要访问【外层函数】的变量。
3. 并且【外层函数】要返回【内层函数】。——只有返回了内层函数，闭包才能“活下来”。

> 注意点：  
> 1. 调用 n 次外层函数，就会得到 n 个不同的闭包，并且这些闭包之间互不影响。  
> 2. 内层函数中用到的外层变量是可变对象，多个闭包之间依然互不影响。  

闭包的优点：  
1. 可以“记住”状态：不用全局变量，也不用写类，就能在多次调用之间保存数据。
2. 可以做“配置过的函数”：先传一部分参数，把环境固定住，得到一个定制版函数。
3. 可以实现简单的“数据隐藏”：外层变量对外不可见，只能通过内层函数访问。
4. 是装饰器（`decorator`）等高级用法的基础。

闭包的缺点：  
1. 理解成本较高：对初学者不太友好，滥用会让代码难读。
2. 如果闭包里引用了很大的对象，又长期不释放，可能会增加内存占用。
3. 很多场景下，其实用【类 + 实例属性】会更清晰，闭包不一定是最优解。

\# 12 装饰器  
装饰器：  
1. 装饰器是一种【可调用对象】（通常是函数），它能接受一个函数作为参数，并且会返回一个新函数。
2. 装饰器可以在不修改原函数代码的前提下，增强或改变原函数的功能。

### 7-12-1 函数装饰器

``` python
def say_hello(func):
	def wrapper(*args, **kwargs):
		print("你好，我要开始计算了")
		return func(*args, **kwargs)
	return wrapper

@say_hello  # = add = say_hello(add)
def add(x, y, z):
	res = x + y + z
	print(f"{x}和{y}和{z}相加的结果是：{res}")
	return res

# add = say_hello(add)
res = add(10, 20, 30)
# 你好，我要开始计算了
# 10和20和30相加的结果是：60
print(res)  # 60
```

关键点：  
1. 接收被装饰的函数，同时返回新函数（`wrapper`）。
2. 装饰器“吐出来”的是 `wrapper` 函数，以后别人调用的也是 `wrapper` 函数。
3. 为了保证参树的兼容性，`wrapper` 函数要通过 `*args` 和 `**kwargs` 接收参数。
4. `wrapper` 函数中主要做的是：调用原函数（被装饰的函数）、执行其他逻辑，但要记得将原函数的返回值 `return` 出去。

``` python
# 进阶：带参数的装饰器（三层嵌套：外层接收配置、中间层接收函数，内层接收具体参数）
def say_hello(msg):
	def outer(func):
		def wrapper(*args, **kwargs):
			print(f"你好，我要开始做{msg}计算了")
			return func(*args, **kwargs)
		return wrapper
	return outer

@say_hello("加法")
def add(x, y):
	print(f"{x} + {y} = {x + y}")
	
@say_hello("减法")
def sub(x, y):
	print(f"{x} - {y} = {x - y}")

add(10, 20)
# 你好，我要开始做加法计算了
# 10 + 20 = 30

sub(20, 10)
# 你好，我要开始做减法计算了
# 20 - 10 = 10
```

``` python
# 进阶：多个装饰器一起使用
def test1(func):
	print("我是test1装饰器")
	def wrapper(*args, **kwargs):
		print("我是test1追加的逻辑")
		return func(*args, **kwargs)
	return wrapper

def test2(func):
	print("我是test2装饰器")
	def wrapper(*args, **kwargs):
		print("我是test2追加的逻辑")
		return func(*args, **kwargs)
	return wrapper

@test1
@test2
def add(x, y):
	print(f"{x} + {y} = {x + y}")

add(10, 20)
# 我是test2装饰器
# 我是test1装饰器
# 我是test1追加的逻辑
# 我是test2追加的逻辑
# 10 + 20 = 30
```

> 实际应用：在不改变原函数的前提下，给函数统一加上：日志、计时、校验、 缓存等功能。  

\## 12. 2 类装饰器  
类装饰器：  
1. 包含 `__call__` 方法的类，就是类装饰器。
2. 像调用函数一样，去调用类装饰器的实例对象，就会触发 `__call__` 方法的调用。
3. `__call__` 方法通常接收一个函数作为参数，并且会返回一个新函数。

``` python
class SayHello:
	def __call__(self, func):
		def wrapper(*args, **kwargs):
			print("你好，我要开始计算了")
			return func(*args, **kwargs)
		return wrapper

# 使用@符语法糖使用类装饰器
@SayHello()
def add(x, y):
	print(f"{x} + {y} = {x + y}")

# 使用 SayHello 去装饰 add 函数（手动装饰）
say = SayHello()
add_pro = say(add)
add_pro(10, 20)
# 你好，我要开始计算了
# 10 + 20 = 30

# 使用 SayHello 去装饰 add 函数（@符）
add(10, 20)
# 你好，我要开始计算了
# 10 + 20 = 30
```

``` python
# 带参数的类装饰器
class SayHello:
	def __init__(self, msg):
		self.msg = msg

	def __call__(self, func):
		def wrapper(*args, **kwargs):
			print(f"你好，我要开始{self.msg}计算了")
			return func(*args, **kwargs)
		return wrapper

@SayHello("加法")
def add(x, y):
	print(f"{x} + {y} = {x + y}")

add(10, 20)
# 你好，我要开始加法计算了
# 10 + 20 = 30
```

``` python
# 多个类装饰器的使用
class Test1:
	def __call__(self, func):
		def wrapper(*args, **kwargs):
			print("我是Test1追加的逻辑")
			return func(*args, **kwargs)
		return wrapper

class Test2:
	def __call__(self, func):
		def wrapper(*args, **kwargs):
			print("我是Test2追加的逻辑")
			return func(*args, **kwargs)
		return wrapper

@Test1()
@Test2()
def add(x, y):
	print(f"{x} + {y} = {x + y}")

add(10, 20)
# 我是Test1追加的逻辑
# 我是Test2追加的逻辑
# 10 + 20 = 30
```

\# 13 类型注解  
### 7-13-1 变量类型注解
变量类型注解：给变量加上类型说明，可增强代码的可读性、让 IDE 的提示更友好。  

``` python
num: int = 100
price: float = 12.5
message: str = "你好呀"
is_vip: bool = True
result: None = None  # 语法上没有问题，但这么写没有意义

# 注意：可以先写变量的类型注解，以后再赋值
school: str
school = "ProkyHoof"

# hobby 是列表，并且列表中的所有元素必须是 str 类型
hobby: list[str] = ["抽烟", "喝酒", "烫头"]

# hobby 是列表，并且列表中的元素，可以是：str 或者 int 类型
hobby: list[str | int] = ["抽烟", "喝酒", 100]

# persons 是字典，键是 str 类型，值是 int 类型
persons: dict[str, int] = {"猪脚": 18, "张三": 16}

# 元组的类型声明有点特殊
scores: tuple[int] = (10,)
scores: tuple[int, int] = (10, 20)
scores: tuple[int, ...] = (10, 20, 30)
scores: tuple[int | str, ...] = ("猪脚", 19, 29, 30)
```

Python 会根据初始赋值推导变量的类型：  
1. 对于普通变量：后续如果改变类型，不会警告。
2. 对于容器变量：要求内部元素类型必须与推导出来的一致，否则就会警告。

### 7-13-2 函数类型注解
函数类型注解：给函数的【参数】和【返回值】添加类型说明。  
语法格式：`函数名(参数1: 类型, 参数2: 类型) -> 返回值类型:`。  

``` python
# 设置参数类型注解、设置返回值类型注解
def add(x: int, y: int) -> int:
	return x + y

add(10, 20)

# 参数有默认值（Python可以推导出参数的类型）、设置返回值类型
def add(x=1, y=1) -> int:
	return x + y
	
# 设置多个返回值的类型注解
def show_nums_info(nums: list[int]) -> tuple[int, int, float]:
	max_value = max(nums)
	min_value = min(nums)
	res = max_value / min_value
	return max_value, min_value, res

# 设置 *args 的类型注解，要求 args 中的每个参数都必须是 int 类型
def add(*args: int) -> int:
	return sum(args)

# 设置 **kwargs 的类型注解，需求 kwargs 中的每组参数的值，必须是 str 或 int 类型
def show_info(**kwargs: str | int):
	print(kwargs)

show_info(name="张三", age=18, gender="男")

# 获取函数的注解信息
print(add.__annotations__)
```


# 8 错误与异常

## 8-1 错误与异常
错误：代码本身有语法错误，解释器无法执行代码。——无法通过异常处理机制解决。  
异常：代码在语法上没问题，但执行过程中出现了问题。——可以通过异常处理机制解决。  

``` python
# 一些开发中常见的异常：
# 1. ZeroDivisionError：当除数为 0 时触发。
num1 = 100
num2 = 0
res = num1 / num2  # ZeroDivisionError: division by zero

# 2. TypeError：当操作的数据类型不正确或不兼容时触发。
res = "10" + 5  # TypeError: can only concatenate str (not "int") to str

# 3. AttributeError：当对象没有指定的属性活方法时触发。
class Person:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	
p1 = Person("张三", 18)
print(p1.gender)  # AttributeError: 'Person' object has no attribute 'gender'

nums = [10, 20, 30]
nums.add(40)  # AttributeError: 'list' object has no attribute 'add'

# 4. IndexError：当索引超出范围（索引越界）时触发。
nums = [10, 20, 30, 40]
print(nums[4])  # IndexError: list index out of range

# 5. NameError：当使用了不存在的变量时触发。
print(school)  # NameError: name 'school' is not defined

# 6. KeyError：当访问字典中不存在的 key 时触发。
person = {"name": "张三", "age": 18}
print(person["gender"])  # KeyError: 'gender'

# 7. ValueError：当值不合法，但类型正确时触发。
int("hello")  # ValueError: invalid literal for int() with base 10: 'hello'
```

异常层级关系文档：
[Built-in Exceptions — Python 3.13.15 文档](https://docs.python.org/zh-cn/3.13/builtins/exceptions.html#exception-hierarchy)  

\# 2 异常处理  
### 8-2-1 为什么要进行异常处理：
- 程序运行过程中出现的异常，如果得不到处理，那程序就会立即崩溃，导致后续代码无法执行。
- 异常处理不是让异常消失，而是将异常捕获到，随后根据异常的具体情况，来执行指定的逻辑。

### 8-2-2 异常处理（初级）：
1. 将可能出现异常的代码放在 `try` 中，出现异常后的处理代码写在 `except` 中。
2. 如果 `try` 中的代码出现异常，那 `try` 中的后续代码将不会执行，并自动跳转到 `except` 中处理异常。
3. 如果 `try` 中的代码没有异常，那 `except` 中的代码就不会执行。
4. 无论是否发生异常，`try-except` 后面的代码都会继续执行。

``` python
print("欢迎使用本程序")
try:
	a = int(input("请输入第一个数："))
	b = int(input("请输入第二个数："))
	res = a / b
	print(f"{a}除以{b}的结果是：{res}")
except:
	print("抱歉，程序出现了异常")
print("我是后续的其他逻辑1")
print("我是后续的其他逻辑2")
```

### 8-2-3 异常处理（捕获指定的类型的异常）

``` python
print("欢迎使用本程序")
try:
	a = int(input("请输入第一个数："))
	b = int(input("请输入第二个数："))
	res = a / b
	print(f"{a}除以{b}的结果是：{res}")
except ZeroDivisionError:
	print("程序异常：0不能作为除数")
except ValueError:
	print("程序异常：您输入的必须是数字")
print("我是后续的其他逻辑1")
print("我是后续的其他逻辑2")
```

### 8-2-4 验证一下异常之间的继承关系

``` python
print(issubclass(ZeroDivisionError, ArithmeticError))  # True
print(issubclass(ZeroDivisionError, Exception))  # True
print(issubclass(ValueError, Exception))  # True
print(issubclass(KeyboardInterrupt, Exception))  # False
print(issubclass(KeyboardInterrupt, BaseException))  # True
```

### 8-2-5 多个 except 从上往下匹配，匹配成功后不再向下匹配

``` python
print("欢迎使用本程序")
try:
	a = int(input("请输入第一个数："))
	b = int(input("请输入第二个数："))
	res = a / b
	print(f"{a}除以{b}的结果是：{res}")
except Exception:
	print("程序异常")
except ZeroDivisionError:
	print("程序异常：0不能作为除数")
except ValueError:
	print("程序异常：您输入的必须是数字")
print("我是后续的其他逻辑1")
print("我是后续的其他逻辑2")
```

### 8-2-6 获取异常的具体信息

``` python
print("欢迎使用本程序")
try:
	a = int(input("请输入第一个数："))
	b = int(input("请输入第二个数："))
	res = a / b
	print(f"{a}除以{b}的结果是：{res}")
except ZeroDivisionError:
	print("程序异常：0不能作为除数")
except ValueError:
	print("程序异常：您输入的必须是数字")
except Exception as e:
	print(f"程序异常，异常信息：{e}")
	print(f"程序异常，异常类型：{type(e)}")
	print(f"程序异常，异常参数：{e.args}")
	print(f"程序异常，异常的文件：{e.__traceback__.tb_frame.f_code.co_filename}")
	print(f"程序异常，异常的具体行数：{e.__traceback__.tb_lineno}")
	
	# 通过 traceback 来回溯异常
	import traceback
	print(traceback.format_exc())
print("我是后续的其他逻辑1")
print("我是后续的其他逻辑2")
```

### 8-2-7 一个 except，也可以捕获不同的异常

``` python
print("欢迎使用本程序")
try:
	a = int(input("请输入第一个数："))
	b = int(input("请输入第二个数："))
	res = a / b
	print(f"{a}除以{b}的结果是：{res}")
except (ZeroDivisionError, ValueError, Exception) as e:
	if isinstance(e, ZeroDivisionError):
		print("程序异常：0不能作为除数")
	elif isinstance(e, ValueError):
		print("程序异常：您输入的必须是数字")
	else:
		print(f"程序异常：{e}")
print("我是后续的其他逻辑1")
print("我是后续的其他逻辑2")
```

### 8-3-8 异常处理的完整写法
1. `try`：尝试去做可能会出现异常的事情。
2. `except`：出现异常时的处理（出现异常时怎么补救）。
3. `else`：如果一切顺利（没有异常出现）要做的事。
4. `finally`：无论有没有异常，都要做的事。

``` python
print("欢迎使用本程序")
try:
	a = int(input("请输入第一个数："))
	b = int(input("请输入第二个数："))
	res = a / b
	print(f"{a}除以{b}的结果是：{res}")
except (ZeroDivisionError, ValueError, Exception) as e:
	if isinstance(e, ZeroDivisionError):
		print("程序异常：0不能作为除数")
	elif isinstance(e, ValueError):
		print("程序异常：您输入的必须是数字")
	else:
		print(f"程序异常：{e}")
else:
	print("try 中的代码没有任何异常！")
finally:
	print("无论有没有异常，我的计算都结束了")
print("我是后续的其他逻辑1")
print("我是后续的其他逻辑2")
```

\# 3 异常的拓展  
### 8-3-1 手动抛出异常
当程序遇到不符合预期情况时，可以使用 `raise` 语句手动触发（抛出）异常。  

``` python
print("欢迎使用年龄判断系统")
try:
	age = int(input("请输入你的年龄："))
	if 18 <= age <= 120:
		print("成年")
	elif 0 <= age < 18:
		print("未成年")
	else:
		raise ValueError("年龄应该为0 - 120 的整数")
except Exception as e:
	print(f"程序异常：{e}")
```

### 8-3-2 异常的传递机制
1. 如果异常没有被当前代码块所捕获处理，那该异常就会沿着调用链，逐层传递给其调用者。
2. 如果所有调用者，都没有捕获该异常，那最终程序将因【未处理异常】而意外中止。

``` python
def test1():
	print("test1开始")
	res = "100" + 100
	print("test1结束")

def test2():
	print("test2开始")
	try:
		test1()
	except Exception as e:
		print(f"程序异常：{e}")
	print("test2结束")

def test3():
	print("test3开始")
	test2()
	print("test3结束")

test3()
"""
test3开始
test2开始
test1开始
程序异常：can only concatenate str (not "int") to str
test2结束
test3结束
"""
```

### 8-3-3 自定义异常类
1. 自由开发人员自己定义一个异常类，用来表示代码中“更具体、更有业务含义”的异常。
2. 具体规则：定义一个类（类名通常以 `Error` 结尾），继承 `Exception` 类或其他的子类。

``` python
class SchoolNameError(Exception):
	def __init__(self, msg):
		super().__init__("[校名异常]", msg)

def check_school_name(name):
	if len(name) > 10:
		raise SchoolNameError("学校名过长")
	else:
		print("学校名是合法的")

check_school_name("we are prokyhoof")  # SchoolNameError: ('[校名异常]', '学校名过长')
```


# 9 模块与包

## 9-1 模块
### 9-1-1 模块的概述与分类
模块概述：  
1. 在 Python 中，一个 `.py` 文件就是一个模块（Module）。
2. 模块中可以包含：变量、函数、类等很多内容。
3. 通常把能够实现某一特定功能的代码，集中放在一个模块中（模块就类似于一个工具箱）。
4. 模块可以提高代码的可维护性与可复用性，还可以避免命名冲突。

模块的分类：  
Python 中的模块分为三类，分别是：标准库模块、自定义模块、第三方模块。  
模块命名注意点：  
1. 要符合标识符命名规则。
2. 模块名（`.py` 文件名）区分大小写。
3. 不要与标准库模块同名（一旦同名，Python 会优先引入标准库模块）。

### 9-1-2 定义一个模块

``` python
# order.py
# 订单最大金额
max_order_amount = 1000000

# 创建订单
def create_order():
	print("订单创建成功")

# 关闭订单
def cancel_order():
	print("订单关闭成功")

# 提示函数
def show_info()：
	print("我是来自【订单】模块的提示")

__all__ = ("cancel_order", "show_info")
```

``` python
# pay.py
# 支付超时时间
timeout = 1800

# 微信支付
def wechat_pay():
	print("我是微信支付")

# 支付宝支付
def ali_pay():
	print("我是支付宝支付")

# 提示函数
def show_info():
	print("我是来自【支付】模块的提示")
```

### 9-1-3 引入模块的多种方式
常见的模块导入方式：  
1. `import 模块名` 。
2. `import 模块名 as 别名`。
3. `from 模块名 import 具体内容1, 具体内容2, ...`。
4. `from 模块名 import 具体内容1 as 别名1, 具体内容2 as 别名2, ...`。
5. `from 模块名 import *`。

``` python
# 1
import order
import pay

# 2
import order as dd
import pay as zf

# 3
from order import max_order_amount, show_info
from pay import wechat_pay, ali_pay

# 4
from order import max_order_amount as max_order, show_info as show
from pay import wechat_pay as wechat, ali_pay as ali

# 5
from order import *
from pay import *
```

> 对于同名方法，后引入的模块将会覆盖之前引入的模块。  

关于 `__all__`：  
- 在 Python 模块中，可通过 `__all__` 来控制【`from 模块名 import *`】能导入哪些内容。
- `__all__` 的值可以是：列表、元组。

关于 `__name__`：  
- `__name__` 是每个 Python 模块（`.py` 文件）都拥有的一个内置变量。
- 它的具体值取决于模块的运行方式：
	- 作为主程序直接运行，`__name__` 的值是 `__main__`。
	- 作为模块被导入到其他程序中运行，`__name__` 的模块的文件名（不带 `.py `）。

\# 2 标准库模块  
标准库模块：随着 Python 一起安装在我们电脑上的那些模块。  
有一些标准库模块是用 C 语言实现的，这些用 C 语言实现的模块，又称：【内置模块】

``` python
import copy		# 拷贝对象（浅拷贝，深拷贝）
import os		# 操作系统相关操作（文件、文件夹、路径系统层面的操作）
import random	# 随机数相关（生成随机数、随机选择、洗牌）

# 内置模块（无法看到具体实现，也没有__file__属性）
import time		# 时间相关操作（获取时间、延时、格式化时间等）
import math		# 数学相关
import sys		# Python 解释器相关操作
```

\# 3 包  
### 9-3-1 包的概述
1. 在 Python 中，【包含 `__init__.py` 的文件夹】就是一个包（Package）。
2. 我们通常会把【某个特定功能相关的所有模块】放入一个包中。
3. 使用包可以进一步提升代码的：可维护性、可复用性，便于管理大型项目。

包与模块的关系：
1. 一个模块就是一个 `.py` 文件，包是用来“管理模块”的目录（文件夹）。
2. 一个包中可以有多个模块，也可以有多个子包。

包的分类：Python 中的包分为三类，分别是：标准库包、自定义包、第三方包。  
包命名注意点：  
1. 要符合标识符命名规范。
2. 包名区分大小写（建议全部使用小写字母）。
3. 不要与标准库包同名。

### 9-3-2 包的多种导入方式
包（文件夹 trade）  ：  
	- `__init__.py`  
	- `order.py`  
	- `pay.py`  

``` python
# 1. import 包名.模块名
import trade.order
import trade.pay

# 2. import 包名.模块名 as 别名
import trade.order as dd
import trade.pay as zf

# 3. from 包名.模块名 import 具体内容1, 具体内容2, ...
from trade.order import max_order_amount, create_order
from trade.pay import timeout, wechat_pay

# 4. from 包名.模块名 import 具体内容1 as 别名1, 具体内容2 as 别名2, ...
from trade.order import max_order_amount as max_amt, create_order
from trade.pay import timeout, wechat_pay as w_pay

# 5. from 包名.模块名 import *
from trade.order import *
from trade.pay import *

# 6. from 包名 import 模块名
from trade import order
from trade import pay

# 7. from 包名 import 模块名 as 别名
from trade import order as dd, pay as zf

# 8. from 包名 import *
from trade import *
```

关于 `__init__.py` 文件：  
1. `__init__.py` 是包的初始化文件，在包被导入时，`__init__.py` 会被自动调用。
2. `__init__.py` 中可以编写一些包的初始化逻辑。
3. `__init__.py` 中所定义的内容，会被【`from 包名 import *`】形式全部引入。
4. `__init__.py` 中也可以使用 `__all__` 来控制包中的哪些模块可以被【`from 包名 import *`】引入。

``` python
import trade
trade.order.create_order()
trade.pay.wechat_pay()
```

\# 4 第三方包  
### 9-4-1 安装一个包
`pip` 是 Python 自带的包管理工具，它相当于 Python 世界的“应用商店”或“依赖管理器”。
  
``` bash
pip install numpy
```

### 9-4-2 全局环境和虚拟环境
#### 9-4-2-1 全局环境（系统环境）
Python 安装目录：`E:\Program Files\python`。  
-- Lib：
	-- 标准库（模块/包）
	-- 第三方 模块/包（site-packages）  
-- Scripts：  
	-- pip.exe  
-- python.exe（python 解释器）  
#### 9-4-2-2 虚拟环境
当前工程里的 `.venv` 文件夹。  

> 全局环境与虚拟环境只共用标准库。虚拟环境无法使用全局环境中的第三方包。  

### 9-4-3 常用 pip 命令

```vtable
{"rows":[[{"t":"命令","rs":1,"cs":1},{"t":"说明","rs":1,"cs":1}],[{"t":"`pip install 包名`","rs":1,"cs":1},{"t":"安装指定的包","rs":1,"cs":1}],[{"t":"`pip install -i 镜像地址 包名`","rs":1,"cs":1},{"t":"临时使用镜像地址安装指定包。","rs":1,"cs":1}],[{"t":"`pip config set global.index-url 地址`","rs":1,"cs":1},{"t":"设置 pip 所使用的镜像地址。","rs":1,"cs":1}],[{"t":"`pip config list`","rs":1,"cs":1},{"t":"查看当前环境的 pip 配置。","rs":1,"cs":1}],[{"t":"`pip config unset global.index-url`","rs":1,"cs":1},{"t":"让 pip 恢复使用官方默认的地址。","rs":1,"cs":1}],[{"t":"`pip list`","rs":1,"cs":1},{"t":"列出当前环境中，已安装的所有第三方包。","rs":1,"cs":1}],[{"t":"`pip uninstall 包名`","rs":1,"cs":1},{"t":"从当前环境中卸载指定的第三方包。","rs":1,"cs":1}]]}
```

### 9-4-4 使用虚拟环境
1. 使用项目根目录。
打开终端，进入项目跟目录，进入 `.venv\Scripts`，输入 `activate`。 输入 `deactivate` 推出虚拟环境。 
2. 使用 PyCharm 自带的终端。
3. 解释器设置安装虚拟环境包。

![](../../../../03%20附件/attachments/知识附件/Python/1.%20Python/1.%20python_20260929_1.png  )


# 10 迭代器与生成器

## 10-1 迭代器
### 10-1-1 可迭代对象
1. 能被 `for` 循环遍历的对象，被称为：可迭代对象（iterable）。

``` python
names = ["张三", "李四", "王五"]
citys = ("北京", "上海", "深圳")
msg = "ProkyHoof"
```

### 10-1-2 迭代器
2. 可迭代对象（iterable）能调用到 `__iter__` 方法。

``` python
names = ["张三", "李四", "王五"]
print(hasattr(names, "__iter__"))  # True
```

3. 调用 `__iter__` 方法会得到：迭代器（iterator）。
	1. `__iter__` 是一个魔法方法，当调用 `iter` 函数时，`__iter__` 会自动调用。
	2. 可迭代对象，`__iter__()` 等价于 `iter(可迭代器对象)`。
	3. 如果 `iter(obj)` 能得到一个迭代器（iterator），那 `obj` 就是可迭代对象。

``` python
names = ["张三", "李四", "王五"]
msg = "ProkyHoof"

print(msg.__iter__())  # <str_ascii_iterator object at 0xf93bd8>
print(iter(names))  # <list_iterator object at 0xe681a8>
```

4. 迭代器（iterator）拥有 `__next__` 方法，每次调用都会根据当前的状态，返回下一个元素。
	1. `迭代器.__next__()` 等价于 `next(迭代器)`。
	2. 当所有元素全都取出后，若继续调用 `__next__` 方法，Python 会抛出 `StopIteration` 异常。

``` python
msg = "ProkyHoof"
it = iter(msg)

print(next(it))  # P
```

#### 10-1-2-1 for 循环背后的工作逻辑

``` python
names = ["张三", "李四", "王五"]

for item in names:
	print(item)

it = iter(可迭代对象)
while True:
	try:
		item = next(it)
		print(item)
	except StopIteration:
		break;
```

5. 迭代器（iterator）也拥有 `__iter__` 方法，并且其返回值是迭代器自身。
	这么设计的原因如下：让 for 循环也能遍历迭代器（即：为了让 iter （迭代器）不出错）。

``` python
it = iter(names)
print(it)  # <list_iterator object at 0xdb0f68>

res = iter(it)
print(res)  # <list_iterator object at 0xdb0f68>
```

6. 迭代器协议。
	1. 能被 `iter()` 接受。
	2. 能被 `next()` 一步一步取值。

\# 2 手写迭代器  
### 10-2-1 迭代器的一个特点
迭代器是一次性的，状态只会向前推进，且不会自动重置（迭代器在遍历的过程中会被“消耗”）。  

``` python
names = ["张三", "李四", "王五"]
it1 = iter(names)
it2 = iter(names)

print(it1)  # <list_iterator object at 0xf8cb68>
print(it2)  # <list_iterator object at 0xd61408>

for item in it1:
	print(item)

for item in it2:
	print(item)
```

### 10-2-2 实现方式 1

``` python
class Person:
	def __init__(self, name, age, gender, address):
		self.name = name
		self.age = age
		self.gender = gender
		self.address = address
	
	def __iter__(self):
		return PersonIterator(self)

class PersonIterator:
	def __init__(self, p):
		# 将外部传进来的数据保存好
		self.p = p
		# 设置迭代器的初始化状态（指针位置）
		self.index = 0
		# 配置好要遍历的内容
		self.attrs = [p.name, p.age, p.gender, p.address]

	# 迭代器的 __iter__ 方法会返回迭代器自身
	def __iter__(self):
		return self

	# 每次调用 __next__ 方法，会根据当前的状态，返回下一个元素
	def __next__(self):
		# 如果指针的位置超出范围，那就抛出 StopIteration 异常
		if self.index >= len(self.attrs):
			raise StopIteration
		# 获取要返回的内容
		value = self.attrs[self.index]
		# 跟新迭代器状态（指针位置）
		self.index += 1
		# 返回 value
		return value

p1 = Person("张三", 18, "男", "安徽合肥")

for item in p1:
	print(item, end=" ")  # 张三 18 男 安徽合肥 
```

### 10-2-3 实现方法 2

``` python
class Person:
	def __init__(self, name, age, gender, address):
		self.name = name
		self.age = age
		self.gender = gender
		self.address = address
		# 设置迭代器的初始化状态（指针位置）
		self.__index = 0
		# 配置好要遍历的内容
		self.__attrs = [name, age, gender, address]
	
	def __iter__(self):
		return self

	def __next__(self):
		# 如果指针的位置超出范围，那就抛出 StopIteration 异常
		if self.__index >= len(self.__attrs):
			raise StopIteration
		# 获取要返回的内容
		value = self.__attrs[self.__index]
		# 将字符串转为大写
		if isinstance(value, str):
			value = value.upper()
		# 跟新迭代器状态（指针位置）
		self.__index += 1
		# 返回 value
		return value

p1 = Person("张三", 18, "男", "安徽合肥")

for item in p1:
	print(item, end=" ")  # 张三 18 男 安徽合肥 
```

\# 3 迭代器的优势  
1. 迭代器是惰性计算，不会一次性生成所有结果，所以能显著降低内存占用。
2. 当数据量很大，不确定要用多少结果时，推荐使用迭代器。

``` python
# 使用迭代器实现
class Fibo:
	def __init__(self, total):
		# 要生成多少个数
		self.total = total
		# 当前生成到第几个了（计数器，指针）
		self.index = 0
		# 初始的两个值
		self.pre = 1
		self.cur = 1
	
	def __iter__(self):
		return self
	
	def __next__(self):
		# 当生成足够数量后，抛出 StopIteration 异常
		if self.index >= self.total:
			raise StopIteration
		# 前两项都是1
		if self.index < 2:
			value = 1
		else:
			# 新的结果等于前两项的和
			value = self.pre + self.cur
			# 更新一下 pre 和 cur
			self.pre = self.cur
			self.cur = value
		# 计数器 + 1
		self.index += 1
		# 返回
		return value

f1 = Fibo(10)
for item in f1:
	print(item, end=" ")  # 1 1 2 3 5 8 13 21 34 55 

# 不用迭代器实现
def fibo(total):
	if total <= 0:
		return []
	if total == 1:
		return [1]
	nums = [1, 1]
	for i in range(2, total):
		nums.append(nums[-1] + nums[-2])
	return nums

f2 = fibo(10)
for item in f2:
	print(item, end=" ")  # 1 1 2 3 5 8 13 21 34 55 
```

\# 4 生成器  
### 10-4-1 生成器函数与生成器对象
1. 生成器：  
	1.  生成器函数：函数体中如果出现了 `yield` 关键字，那该函数是【生成器函数】。  
	2. 生成器对象：调用【生成器函数】时，其函数体不会立刻执行，而是返回一个【生成器对象】。

> 备注：不管能否执行到 `yield` 所在的位置，只要函数中有 `yield` 关键字，那该函数，就是【生成器函数】。  

2. 写在【生成器函数】中的代码，需要通过【生成器对象】来执行。
	1. 调用【生成器对象】的 `__next__` 方法，会让【生成器函数】中的代码开始执行。
	2. 当【生成器函数】中的代码开始执行后，遇到 `yield` 会“暂停”执行，并且其内部会记录“暂停”的位置。
	3. 后续调用 `__next__` 方法时，都会从上一次“暂停”的位置，继续运行，直到再次遇到 `yield`。
	4. 遇到 `return` 会抛出 `StopIteration` 异常，并将  `return` 后面的表达式，作为异常信息。
	5. yield 后面所写的表达式，会作为本次 `__next__` 方法的返回值。

``` python
def demo():
	print("demo 函数开始执行了")
	print(100)
	yield
	a = 200
	print(a)
	yield "我是第二个 yield 返回的数据"
	b = 300
	print(b)
	return "ProkyHoof"

d = demo()
print(d)  # <generator object demo at 0xddc670>
res1 = next(d)
# demo 函数开始执行了
# 100
print(res1)  # None
res2 = next(d)
# 200
print(res2)  # 我是第二个 yield 返回的数据

try:
	next(d)
except StopIteration as e:
	print(e)  # ProkyHoof
```

### 10-4-2 生成器对象的几个细节
3. 生成器对象是一种特殊的迭代器（本质是通过 `yield` 自动实现了迭代器协议）。

``` python
def demo():
	print("demo 函数开始执行了")
	print(100)
	yield
	a = 200
	print(a)
	yield "我是第二个 yield 返回的数据"
	b = 300
	print(b)
	return "ProkyHoof"

d = demo()
print(hasattr(d, "__iter__"))  # True
print(hasattr(d, "__next__"))  # True

for item in d:
	print(item)
# demo 函数开始执行了
# 100
# None
# 200
# 我是第二个 yield 返回的数据
# 300

# for 循环背后的逻辑
gen = iter(d)
while True:
	try:
		value = next(gen)
		print(value)
	except StopIteration:
		break
```

4. `yield` 也可以写在循环里。

``` python
def create_car(total):
	for index in range(1, total + 1):
		yield f"我是第{index}台车"

# cars 是生成器对象
cars = create_car(5)

for car in cars:
	print(car)
# 我是第1台车
# 我是第2台车
# 我是第3台车
# 我是第4台车
# 我是第5台车
```

5. `yield from` 能把一个【可迭代对象】里的东西依次 `yield` 出去。（替代：for + yield）。

``` python
def create_car():
	cars = [1, 2, 3, 4, 5]
	yield from cars

for item in create_car():
	print(item, end=" ")  # 1 2 3 4 5 
```

6. 使用：`生成器.send(值)` 可以让生成器继续执行的同时，给上一次 `yield` 传值。
	1. `next` 只能取值，`send` 既能取值，也能送值。
	2. 第一次启动生成器，不能传值。

``` python
def demo():
	print("demo 函数开始执行了")
	print(100)
	a = yield "我是第二个 yield 返回的数据"
	print(a)
	yield
	return "ProkyHoof"

d = demo()
r1 = next(d)
print(r1)
d.send("猪脚")
# demo 函数开始执行了
# 100
# 我是第二个 yield 返回的数据
# 猪脚
```

### 10-4-3 用生成器实现两个效果

``` python
# 用生成器实现遍历 Person 类的实例对象
class Person:
	def __init__(self, name, age, gender, address):
		self.name = name
		self.age = age
		self.gender = gender
		self.address = address
		self.__attr = [name, age, gender, address]
	
	def __iter__(self):
		yield from self.__attr

p1 = Person("猪脚", 18, "男", "安徽安庆")
for attr in iter(p1):
	print(attr, end=" ")  # 猪脚 18 男 安徽安庆 
```

``` python
# 
def fibo(total):
	pre = 1
	cur = 1

	for index in range(total):
		if index < 2:
			yield 1
		else:
			value = pre + cur
			pre = cur
			cur = value
			yield value

for attr in fibo(10):
	print(attr, end=" ")  # 1 1 2 3 5 8 13 21 34 55 
```

> 无论是迭代器，还是生成器对象，都可以用 `list`、`tuple`、`set` 等直接拿到其里面的所有内容（注意：容易挤爆内存）。  

### 10-4-4 生成器表达式
生成器表达式：一种用类似列表推导式的语法，快速创建生成器对象的方式。  
语法格式：`(表达式 for 变量 in 可迭代对象)`  。  

``` python
nums = [10, 20, 30, 40]
res = (n * 2 for n in nums)
print(res)  # <generator object <genexpr> at 0xd56e98>
for n in res:
	print(n, end=" ")  # 20 40 60 80 
```

> 什么时候适合用生成器表达式：当【每个结构，只依赖当前这一个元素】时。


# 11 文件操作

## 11-1 前序知识
### 11-1-1 文件分类
1. 纯文本文件：
	1. 读取和存储时，要遵循某种【字符编码】规范（如：UTF-8 等）进行编码和解码，最终以【二进制】的形式存储。
	2. 【纯文本文件】最终会呈现为：可以直接阅读的文本信息。
	3. 常见的【纯文本文件】有：`.txt`、`.py`、`.md`、`.html` 等。

2. 二进制文件：
	1. 读取和存储时，不涉及字符编码，会按照某种【文件格式规范】把内容转为【二进制】数据进行存储。
	2. 二进制文件需要由【能够识别其格式的软件】进行解析，最终的呈现形式多种多样（音频、视频、图像、幻灯片等）。
	3. 常见的二进制文件有：`.mp3`、`.mp4` 、`.doc`、`.ppt`、`.jpg`、`.png` 等。

### 11-1-2 路径分类
1. 绝对路径：从文件系统的【根目录】开始，完整描述文件活目录所在的位置。
2. 相对路径：以当前【工作目录】为参照，描述目标文件或目录相对于它的位置。

\# 2 读取文件  
### 11-2-1 open 方法
Python 中操作文件的标准流程：  
1. 创建【文件对象】。
2. 操作文件（读取、写入等）。
3. 关闭文件。

文件操作的核心 —— `open` 函数：它可以打开或创建文件，且支持多种操作模式，返回值是【文件对象】。  
`open` 函数最常用的三个参数如下：  
1. `file`：要操作的文件路径。
2. `mode`：文件的打开模式。
	`r` ：读取（默认值）。
	`w`：写入，并先截断文件。
	`x`：排它性创建，如果文件已存在，则创建失败。
	`a`：打开文件用于写入，如果文件存在，则在文件末尾追加内容。
	`b`：二进制模式。
	`t`：文本模式（默认值）。
	`+`：打开用于更新（读取与写入）。
3. `encoding`：字符编码。

``` python
# 创建【文件对象】
file = open(file="a.txt", mode="rt", encoding="utf-8")

# 操作文件（读取）
res = file.read()
print(res)

# 关闭文件
file.close()
```

### 11-2-2 read 方法
`read` 方法说明：  
1. `read(size)` 中的 `size` 是可选参数。
	1. 若不传递 `size` 参数，表示：读取文件中所有的内容（注意内存占用）。
	2. 若传递了 `size` 参数，表示：读取文件中指定个数的字符，或指定大小的字符。
2. `read` 会从上一次 `read` 的位置继续读取（指针思想），若到达文件末尾后继续读取，将返回空字符串。

``` python
# 创建【文件对象】
file = open(file="a.txt", mode="rt", encoding="utf-8")

# 操作文件（读取）
res = file.read(2)
print(res)

# 用循环配合多次read （对内存友好）
while True:
	result = file.read(10)
	if result == "":
		break
	print(result, end=" ")

# 关闭文件
file.close()
```

### 11-2-3 readline 方法
`readline` 方法说明：   
1. `readline(size)` 中的 `size` 是可选参数。
	1. 若不传递 `size` 参数，表示：读取当前这一行所有的内容。
	2. 若传递了 `size` 参数，表示：表示读取当前行时，最多能读取的字符串，或字节数（`size` 不是行数）。
2. `readline` 方法，也是从上一次位置继续读取，若到达文件末尾后继续读取，也是返回空字符串。

``` python
# 使用文件对象的 readline 方法，读取文件中的一行
file = open(file="a.txt", mode="rt", encoding="utf-8")

res = file.readline()
print(repr(res))
print(res.strip())

# 通过循环配合 readline 逐行读取
while True:
	line = file.readline()
	if line == "":
		break
	print(line)

file.close()
```

### 11-2-4 readlines 方法
`readlines` 方法说明：  
1. `readlines(hint)` 中的 `hint` 是可选参数。
	1. 若不传递 `hint` 参数，表示：读取当前文件的所有行。
	2. 若传递了 `hint` 参数，表示：期望读取的【字符个数 或 字节数的上限】（`hint` 不是行数）。
2. 注意：由于 `readlines` 是一次性读取文件的所有内容，所以不适合读取体积较大的文件。

``` python
# 使用 for 循环直接遍历文件对象
file = open(file="a.txt", mode="rt", encoding="utf-8")

for line in file:
	print(line, end="")

file.close()
```

``` python
# 使用文件对象的 readlines 方法，一次性按“行”读完，返回一个列表
file = open(file="a.txt", mode="rt", encoding="utf-8")

res = file.readlines()
print(res)

file.close()
```

### 11-2-5 with 的使用
最佳实践：使用 `with` 上下文管理器，集合 `for` 循环遍历，逐行读取文件。  

``` python
with open(file="a.txt", mode="rt", encoding="utf-8") as file
	for line in file:
		print(line, end="")
```

\# 3 关于 with  
1. Python 中的 `with` 主要用于程序中“需要成对出现的操作”，例如：
	1. 上锁 / 解锁。
	2. 打开 / 关闭。
	3. 借用 / 归还。
2. 最终目标：编码者只管做具体的事，“进入”和“离开”的事，让 Python 自动处理。
3. 语法格式如下：

``` python
with 能得到一个上下文管理器的表达式 as 变量:
	具体的事1
	具体的事2
	具体的事3
```

4. 上下文管理器协议：
	1. `__enter__` 方法：`with` 中的代码执行【之前】调用，其返回值会赋值给 `as` 后的变量。
	2. `__exit__` 方法：`with` 中的代码执行【结束后】调用（无论是 `with` 中是否出现异常都会调用）。

``` python
# 定义一个 Person 类，让其他实例对象遵循：上下文管理器协议
class Person:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	
	def speak(self):
		print(f"我叫{self.name}，年龄是{self.age}")
		
	def __enter__(self):
		print("进入的逻辑")
		return self
	
	def __exit__(self, exc_type, exc_val, exc_tb):
		print("离开的逻辑")

with Person("猪脚", 18) as p1:
	p1.speak()
# 进入的逻辑
# 我叫猪脚，年龄是18
# 离开的逻辑
```

`exc_type`：异常信息。  
`exc_val`：异常对象。  
`exc_tb`：异常追踪信息。  
当 `with` 中的代码发生异常时，`__exit__` 方法的返回值规则如下：  
- 返回“真”：表示异常【已经】被处理，异常【不会】被继承抛出。
- 返回“假”：表示异常【没有】被处理，异常【会】被继承抛出。

`with` 执行流程：  
1. 计算 `with` 后面的表达式，得到一个【上下文管理器】。
2. 调用【上下文管理器】的 `__enter__()` 方法，并将其返回值赋给 `as` 后面的变量。
3. 执行 `with` 所管理的代码。
4. 无论 `with` 中的代码，是正常结束，还是发生异常，都会自动调用【上下文管理器】的 `__exit__` 方法。

\# 4 写入文件  
### 11-4-1 w 模式、x 模式、a 模式
`w`：写入，并先截断文件（清空文件中的所有内容）。  
`x`：排它性创建，如果文件已存在，则创建失败。
`a`：打开文件用于写入，如果文件存在，则在文件末尾追加内容。
### 11-4-2 flush 方法的使用
在 Python 中文件写入时，并不是没写一次就立刻落盘，而是：先写到“缓冲区”里。  
文件对象的 `flush` 方法：把缓冲区中的数据，立刻写入到文件中。

``` python
with open(file="demo.txt", mode="at", encoding="utf-8") as file:
	file.write("你好")
	file.write("再见")
	file.flush()  # 这时候的 demo 文件夹就会出现 “你好 再见”
	time.sleep(10000000)
	file.write("我上早8")
```

### 11-4-3 rt+ 模式和 seek 方法

``` python
with open(file="demo.txt", mode="rt+", encoding="utf-8") as file:
	file.seek(0, 2)
	file.write("你好")
```

`seek(offset, whence)` 方法：用于改变文件对象指针的位置，参数说明如下：  
	`offset`：偏移量，要移动多少距离。  
	`whence`：参考点，从哪里开始计算偏移，有三种取值。  
		`0`：从文件开头计算（默认值）。  
		`1`：从当前位置计算。  
		`2`：从文件末尾计算。  

> 注意：在文本模式下，不要随意去定位中文字符位置，否则可能破坏文件编码。  

\# 5 目录操作  

> 文件路径可以使用 `/` 也可以使用 `\\`。

1. `os.mkdir(path)`：创建“单级”目录（如果目录已经存在，则会抛出异常）。

``` python
import os  # os 是一个模块
os.mkdir("./demo")  # 当前文件夹创建一个 demo 的文件夹
```

2. `os.makedirs(path)`：创建“多级”目录（如果路径中的所有目录都已经存在，则会抛出异常）。

``` python
os.makedirs("D:/demo/aa/bb")  # demo 文件夹已经存在，创建一个多级文件夹 aa\bb
```

3. `os.rmdir(path)`：删除空目录（如果目录不存在，或目录非空，都会抛出异常）。

``` python
os.rmdir("D:/demo/aa/bb")
```

4. `os.removedirs(path)`：递归删除空目录，在成功删除末尾一级目录后，会“向上”尝试把父级目录也删除（直到父目录不是空目录）。

``` python
os.removedirs("D:/demo/aa/bb")
```

> `os.removedirs()` 一次只能处理“一条路径”，不会主动去删除同级目录下的其他空文件夹。  
> 它的规则是：  
> 1. 先删除你指定的那个叶子目录（必须为空）。  
> 2. 然后沿着父级录链一层层往上删。  
> 3. 一旦遇到非空目录，就停止，不会继续删。  

5. `os.path.exists(path)`：判断路径是否存在（文件/目录都算）。

``` python
res = os.path.exists("D:/demo/aa/bb")  # 这里的 bb 是文件或者文件夹都是可以的
print(res)
```

6. `os.path.isdir(path)`：用于判断路径，具体规则如下：
	1. 路径不存在（返回 False）。
	2. 路径存在，但指向的是文件（返回 False）。
	3. 路径存在，并且是目录（返回 True）。

``` python
res = os.path.isdir("D:/demo/aa/bb")  # 若 bb 是文件则返回 False，若 bb 是目录则返回 True
print(res)
```

7. `os.path.isfile(path)`：判断是否为文件。

``` python
res = os.path.isfile("D:/demo/aa/bb")  # bb 必须是文件返回 True
print(res)
```

8. `os.scandir(path)`：扫描指定目录。

``` python
res = os.scandir("D:/demo")  # 返回的是一个 iterator 迭代器对象，只会扫描 demo 单一文件夹，不会深入文件夹
for item in res:
	print("文件" if item.is_file() else "目录", item.name)
```

9. `os.walk(path)`：按层级，递归地遍历指定目录下，所有的子目录和文件。

``` python
res = os.walk("D:/demo")  # 返回的是一个 generator 生成器
for item in res:
	print(item)  # 一个元组，("目录路径", [文件夹], [文件])
```

10. 危险操作：删除有内容的目录内的所有目录。

``` python
shutil.rmtree("D:/demo")
```

\# 6 小练习  
### 11-6-1 练习 1
将一个二进制文件复制到指定位置。  

``` python
import os

# 源文件
source = "music.mp3"  # 相对文件路径
# 目标目录
target = "D:/media"

# 如果目标目录不存在，就创建目录
if not os.path.isdir(target):
	os.makedirs(target)

with open(file=source, mode="rb") as f1, open(file=target + "/" + "my_music.mp3", mode = "wb") as f2:
	while True:
		# 每次只读取 1 KB
		data = f1.read(1024)  # 每次读取 1024 个字节，就是 1KB
		# 如果文件读取完毕了，就跳出循环
		if data:
			break
		# 向目标文件中写入数据
		f2.write(data)
	print("复制完毕")
```

> 对于二进制的读取，当二进制文件读取完之后，再次读取，由于指针指向文件末尾，所以返回的是一个空字节 `b""`。  

### 11-6-2 练习 2
日志记录:  
1. 用户输入用户名和密码后，程序进行校验。
2. 用户名不存在，提示“用户名未注册”，并记录日志。
3. 用户名存在，但密码错误，提示“密码错误”，并记录日志。
4. 用户名和密码均正确，提示“登录成功”，并记录日志。

``` python
import time

users = {
	"张三": "123456",
	"李四": "888888",
	"王五": "abc123"
}

# 获取当前的时间
now = time.strftime(%Y-%m-%d %H:%M:%S)

# 提示输入信息
username = input("请输入用户名")
password = input("请输入密码")

# 如果用户名不在 user 中
if username not in users:
	print("用户名未注册")
	with open(file="log.txt", mode="at", encoding="utf-8") as file:
		file.write(f"{now}\t{username}\t登录失败（用户未注册）\n")

# 如果密码不正确
elif users[username] != password:
	print("密码不正确")
	with open(file="log.txt", mode="at", encoding="utf-8") as file:
		file.write(f"{now}\t{username}\t密码错误\n")

# 登录成功
else:
	print("登录成功")
	with open(file="log.txt", mode="at", encoding="utf-8") as file:
		file.write(f"{now}\t{username}\t登录成功\n")
```

> `mode="rt"` 不会自动创建文件，`open()` 方法中只能创建文件，不能创建不存在的目录（文件夹）。


# 12 多进程 多线程

## 12-1 概念
### 12-1-1 并发与并行
1. 并发：
	- 概念：在一段时间内，当 CPU 面对多个任务时，会将每个任务交替着执行一段时间。
	- 特点：
		- 对于某个瞬间，CPU 实际上只在执行一个任务。
		- CPU 通过高频切换不同的任务，让每个任务都能得到推进，仿佛多个任务在“同时执行”。
2. 并行：
	- 概念：并行依赖于多个 CPU，或多核的 CPU，在同一时刻，每个核心都在执行不同的任务。
	- 特点：
		- 对于某个瞬间，每个 CPU（或每个核心）都在执行不同的任务。
		- 通过多个 CPU（或多个核心）同时工作的方式，让多个任务真的在同时执行。

> 在现代操作系统，并发与并行通常都是同时存在的。  

![2. 并行与并发](../../../../03%20附件/Excalidraw/1.%20Python/2.%20并行与并发.md)

``` python
import os
print(os.cpu_count())  # 查看当前 cpu 的核数
```

### 12-1-2 同步与异步
1. 同步（sync）
	- 概念：发起一个任务之后，需要等该任务完成后，才能继续执行后续任务。
	- 表现：当前执行流会被【阻塞】。
2. 异步（async）
	- 概念：发起一个任务之后，不必等该任务完成，就可以继续执行其他任务。
		备注：虽然不必等待任务完成，但任务完成后，仍然可以通过特定方式获取结果。
	- 表现：当前执行流不会被【阻塞】。

> 注意区分概念：  
> 	并发 / 并行：描述的是任务如何被执行，即：多个任务在执行时，CPU 要如何处理。  
> 	同步 / 异步：描述的是任务如何被组织和等待，即：要不要等当前发起的任务执行完，再进行下一个任务。  

> 注意点：CPU 的核心数和执行速度，不会改变任务之间的逻辑依赖关系！例如：  
> 一旦任务 1、任务 2、任务 3 之间被设计为同步关系，那么：即便 CPU 切换任务的速度再快，核心数量再多，也不会在【任务 1】没完成的情况下去启动【任务 2】。

### 12-1-3 进程与线程
1. 进程：
	1. 一个正在运行的程序或软件，背后就对应着一个或多个进程。
	2. 进程是操作系统进行资源分配的基本单位。
	3. 每个进程都有自己独立的一块内容空间。
2. 线程：
	1. 线程是进程内部的执行单元（一个进程中可以有多个线程）。
	2. 线程是操作系统进行 CPU 调度的基本单位。
	3. 同一进程内的线程共享进程资源。

\# 2 主进程与子进程  
在 Windows 操作系统中，查看：进程名、父进程 pid、进程 pid 的命令如下：  

``` bash
wmic process get Name,ParentProcessId,ProcessId
```

``` python
import os

print(f"当前的进程 pid:{os.getpid()}")
print(f"当前进程的父进程 pid:{os.getppid()}")
```

\# 3 使用 Process 创建进程  

``` python
import os
import time
from multiprocessing import Process

# 定义一个 speak 函数，功能是：每个一秒说话一次（一共说话10次）
def speak():
    for index in range(10):
        print(f"我在说话{index}，进程 pid 是：{os.getpid()}")
        time.sleep(1) 

# 定义一个 study 函数，功能是：每隔一秒学习一次（一共学习15次）
def study():
    for index in range(15):
        print(f"我在学习{index}，进程 pid 是：{os.getpid()}")
        time.sleep(1) 

if __name__ == "__main__":
    # 创建两个 Process 类的实例对象（进程对象），分别是 p1 和 p2
    p1 = Process(target=speak)
    p2 = Process(target=study)  

    # 调用进程对象的 start 方法，会立刻向操作系统申请一个进程，并且会将进程交由操作系统进行调度。
    p1.start()
    p2.start()
```

> 注意点 1: `p1` 和 `p2` 就对应着以后的两个子进程，在创建它们的时候，就要指定它们要执行的任务。  
> 注意点 2:此时的 `p1` 和 `p2` 只是代码层面的两个进程对象，操作系统还没有真的创建 `p1` 和 `p2` 两个进程。  

> 注意：一定要写 `if __name__ == "__main__"` 这个判断，原因如下：  
> 1. 当创建子进程时，Python 并不会把父进程内存里的 `speak` 函数直接交给子进程。  
> 2. Python 会启动一个全新的 Python 解释器进程，重新执行当前的 `.py` 文件（作为模块）。  
> 3. 在执行过程中，重新定义出一个 `speak` 函数，交给子进程。  

\# 4 关于 Process 参数  
`Process` 的参数：  
- `group`：默认值是 `None`（应当始终为 `None`）。
- `target`：子进程要执行的可调用对象，默认值为 `None`。
- `name`：进程名称，默认为 `None`，如果设置为 `None`,Python 会自动分配名字。
- `args`：给 `target` 传的位置参数（元组）。
- `kwargs`：给 `target` 传的关键字参数（字典）。
- `daemon`：标记进程是否为守护进程，取值为布尔值（默认为 `None`，表示从创建方进程继承）。

``` python
import os
import time
from multiprocessing import Process, current_process

# 定义一个 speak 函数，功能是：每个一秒说话一次（一共说话10次）
def speak(a, b, msg):
    for index in range(10):
        print(f"{msg}-{a}-{b}-{current_process().name}我在说话{index}，进程 pid 是：{os.getpid()}")
        time.sleep(1)

# 定义一个 study 函数，功能是：每隔一秒学习一次（一共学习15次）
def study():
    for index in range(15):
        print(f"{current_process().name}我在学习{index}，进程 pid 是：{os.getpid()}")
        time.sleep(1)

if __name__ == "__main__":
    # 创建两个 Process 类的实例对象（进程对象），分别是 p1 和 p2
    p1 = Process(target=speak, name="猪脚", args=(666, 888), kwargs={"msg": "demo"})
    p2 = Process(target=study, name="ProkyHoof")

    # print(p1.name)
    # print(p2.name)
    # 调用进程对象的 start 方法，会立刻向操作系统申请一个进程，并且会将进程交由操作系统进行调度。
    p1.start()
    p2.start()
```

\# 5 Lock（锁）  

```python
import os
import time
from multiprocessing import Process, Lock, RLock

# 定义一个 speak 函数，功能是：每个一秒说话一次（一共说话10次）
def speak(lock):
    for index in range(10):
        # 上锁：如果锁是空闲的，立刻上锁，继续往下执行；如果锁被别人拿着：当前进程会阻塞等待（原地等）
        lock.acquire()
        print("好好", end="")
        print("学习", end="")
        print("天天", end="")
        print("向上")
        # 释放锁：acquire 和 release 必须成对出现爱你，否则会永远卡住（死等）
        lock.release()
        time.sleep(1)

# 定义一个 study 函数，功能是：每隔一秒学习一次（一共学习15次）
def study(lock):
    for index in range(15):
        with lock:
            # with lock：会自动完成两件事：
            # 1. 进入前：自动执行 lock.acquire() 上锁
            # 2. 离开后：自动执行 lock.release() 释放锁
            # 好处：即使代码块里发生异常，也能保证释放锁，避免“卡死”
            # 备注：RLock 可以多次上锁
            print("A", end="")
            print("B", end="")
            print("C", end="")
            print("D")
        time.sleep(1)

if __name__ == "__main__":
    print("我是主进程中的【第一行】打印")
    
    lock = RLock()

    p1 = Process(target=speak, args=(lock,))
    p2 = Process(target=study, args=(lock,))
    p1.start()
    p2.start()
    print("我是主进程中的【最后一行】打印")
```

> `Lock` 和 `RLock` 的核心区别：
> `Lock` 不可重入，同一线程重复 `acquire` 会死锁；`RLock` 可重入，同一线程可以多次 `acquire`，但必须对应次数 `release` 才真正释放。
\# 6 join 方法  
`join` 方法的作用：阻塞当前进程，等 join 前面的进程执行完，再继续往下执行。  
`join(timeout)`，其中 `timeout` 是可选参数，表示等多久，单位是秒。  

```python
import os
import time
from multiprocessing import Process

# 定义一个 speak 函数，功能是：每个一秒说话一次（一共说话10次）
def speak():
    for index in range(10):
        print(f"我在说话{index}，进程 pid 是：{os.getpid()}")
        time.sleep(1)

# 定义一个 study 函数，功能是：每隔一秒学习一次（一共学习15次）
def study():
    for index in range(15):
        print(f"我在学习{index}，进程 pid 是：{os.getpid()}")
        time.sleep(1)

if __name__ == "__main__":
    # 创建两个 Process 类的实例对象（进程对象），分别是 p1 和 p2
    p1 = Process(target=speak)
    p2 = Process(target=study)

    p1.start()
    # 让主进程等 p1 进程执行完毕后，主进程再继续执行。
	p1.join()

    p2.start()
    # 让主进程等 p2 进程执行完毕后，主进程再继续执行。
	p2.join()
```

> 注意点：
> 1. `p.join()` 不是让进程 `p` 等，而是让“执行这行 `join` 代码的那个进程”去等，等的是 `p` 这个进程。  
> 2. 当达到了 `timeout` 所指定的时间后，进程并不会终止，只是“不再等”了。  
> 3. `join` 必须在 `start` 之后。  

\# 7 terminate  

```python
import os
import time
from multiprocessing import Process

# 定义一个 speak 函数，功能是：每个一秒说话一次（一共说话10次）
def speak():
    try:
        for index in range(10):
            print(f"我在说话{index}，进程 pid 是：{os.getpid()}")
            time.sleep(1)
    # 注意：使用 terminate 终止进程，不会引起 finally 执行
    finally:
        print("我是 finally 里的逻辑")

# 定义一个 study 函数，功能是：每隔一秒学习一次（一共学习15次）
def study():
    for index in range(15):
        print(f"我在学习{index}，进程 pid 是：{os.getpid()}")
        time.sleep(1)

if __name__ == "__main__":
    # 创建两个 Process 类的实例对象（进程对象），分别是 p1 和 p2
    p1 = Process(target=speak)
    p2 = Process(target=study)
    p1.start()
    p2.start()

    time.sleep(3)
    print("我是主进程，我准备强制终止p1进程")
    # 向操作系统申请强制终止 p1 进程
    p1.terminate()
    # 等操作系统彻底终止掉了 p1 进程
    p2.join()
    # 看一下 p1 进程是否“活着”
    print(p1.is_alive())

    print("我是主进程中的【最后一行】打印")
```

\# 8 守护进程  
什么是守护进程：  
1. 一种“依附于主进程存在的子进程”，一旦主进程结束，它就会被自动终止。
2. 简言之：主进程一死，守护进程必跟着死。

守护进程的使用场景：
1. 后台监控类任务。
2. 日志 / 统计 / 采样 类任务。
3. 辅助型“陪跑任务”。

注意点：  
1. 守护进程必须是子进程。
2. 主进程结束，守护进程也会随之结束。
3. 守护进程中，不允许再创建新的子进程。
4. 必须在 `start` 之前，`start()` 之后，不能再设置 `daemon`。

```python
import os 
import time
from multiprocessing import Process

def monitor():
    while True:
        try:
            with open(file="./files/log.txt", mode="rt", encoding="utf-8") as f:
                lines = sum(1 for line in f)
        except FileNotFoundError as e:
            lines = 0
        print(f"我是【守护进程({os.getpid()})】中的代码，当前文件中【有{lines}行数据】")
        time.sleep(1)

if __name__ == '__main__':
    print(f"我是主进程({os.getpid()})中的【第一行】代码")

    p = Process(target=monitor, daemon=True)
    p.start()

    # 向文件中写入数据
    with open(file="./files/log.txt", mode="at", encoding="utf-8") as f:
        for index in range(10):
            f.write(f"我是主进程中的代码{index}\n")
            f.flush()
            time.sleep(1)
    
    print(f"我是主进程({os.getpid()})中的【最后一行】代码")
```

\# 9 进程之间不共享变量  
进程之间不共享内容，因此也就不共享任何变量。  

```python
from multiprocessing import Process
num = 100

def test1():
    global num
    num += 10
    print(f"我是 test1 进程，num = {num}")

def test2():
    global num
    num -= 10
    print(f"我是 test2 进程，num = {num}")

if __name__ == '__main__':
    print(f"主进程中的【第一行】代码")
    p1 = Process(target=test1)
    p2 = Process(target=test2)

    p1.start()
    p2.start()

    p1.join()
    p2.join()

    print(num)
    print(f"主进程中的【最后一行】代码")
```

\# 10 Queue（队列）  
队列（Queue）：一种“先进先出”的数据结构（先放进去的数据，一定会先取出来）。  

```python
from multiprocessing import Queue

# 创建一个队列（不限制大小，即：不设置容量上限）
q1 = Queue()

# 创建一个队列（限制大小为3）
q2 = Queue(3)

# 1. put方法：向队列中添加元素，如果队列已满，则阻塞，直到队列有空间
q2.put(10)
q2.put(20)
q2.put(30)

# 2. get方法：从队列中取出元素，如果队列为空，则阻塞，直到队列有元素
value1 = q2.get()
value2 = q2.get()
value3 = q2.get()
print(value1, value2, value3)  # 10 20 30

# 3. empty方法：判断队列是否为空
print(q2.empty())  # True

# 4. full方法：判断队列是否已满
print(q2.full())  # False

# 5. qsize方法：获取队列中元素的个数q
print(q2.qsize())  # 0

# 6. 队列具备等待模式
q2.put(40)
q2.put(50)
q2.put(60)

# 6.1 当队列已满时，继续向队列中添加元素会进入等待模式，直到队列有空间
# q2.put(70)  # 阻塞，直到队列有空间

# 6.2 当队列已满时，执行：put(元素, timeout=3) 方法，如果在3秒内队列有空间，则添加元素成功，否则抛出异常
# q2.put(70, timeout=3)  # 阻塞，直到队列有空间，或者超时

# 6.3 当队列已满时，执行：put_nowait(元素) 方法，如果队列有空间，则添加元素成功，否则抛出异常
# 备注：put_nowait() 方法是 put(block=False) 方法的别名
# q2.put_nowait(80)  # 抛出异常

# get 读多了，也会进入等待模式
q2.get()
q2.get()
q2.get()

# 6.1 当队列已空时，继续从队列中取出元素会进入等待模式，直到队列有元素
# q2.get()  # 阻塞，直到队列有元素

# 6.2 当队列已空时，执行：get(timeout=3) 方法，如果在3秒内队列有元素，则取出元素成功，否则抛出异常
# q2.get(timeout=3)  # 阻塞，直到队列有元素，或者超时

# 6.3 当队列已空时，执行：get_nowait() 方法，如果队列有元素，则取出元素成功，否则抛出异常
# 备注：get_nowait() 方法是 get(block=False) 方法的别名
# q2.get_nowait()  # 抛出异常
```

\# 11 使用 Queue 实现进程通信  

```python
import time
from multiprocessing import Process, Queue

# 子进程1：往队列里放数据
def test1(q):
    for index in range(5):
        print(f"【test1】放入数据：{index}")
        q.put(index)
        time.sleep(1)

# 子进程2：从队列里取数据
def test2(q):
    while True:
        data = q.get()
        print(f"【test2】取出数据：{data}")
        if data == 4:
            break

if __name__ == '__main__':
    q = Queue()
    p1 = Process(target=test1, args=(q,))
    p2 = Process(target=test2, args=(q,))
    p1.start()
    p2.start()
    p1.join()
    p2.join()
```

\# 12 使用 Pipe 实现进程通信  

```python
from multiprocessing import Process, Pipe
import time

def test1(con1):
    time.sleep(2)
    con1.send("hello")
    print("子进程1发送消息")


def test2(con2):
    msg = con2.recv()
    print(f"子进程2接收到消息: {msg}")

if __name__ == '__main__':
    print("主进程开始")
    # 创建管道
    con1, con2 = Pipe(duplex=True)  # duplex=True表示管道是双向的
    # 创建进程
    p1 = Process(target=test1, args=(con1,))
    p2 = Process(target=test2, args=(con2,))

    # 启动进程
    p1.start()
    p2.start()

    # 等待进程结束
    p1.join()
    p2.join()

    print("主进程结束")
```

\# 13 继承 Process 类创建进度  

```python
from multiprocessing import Process
import time, os

class SpeakProcess(Process):
    def __init__(self, a, b):
        super().__init__()
        self.a = a
        self.b = b

    def run(self):
        for index in range(10):
            print(f"我在说话{index}，进程 pid 是：{os.getpid()}，父进程 pid 是：{os.getppid()}")
            time.sleep(1)

class StudyProcess(Process):
    def __init__(self, a, b):
        super().__init__()
        self.a = a
        self.b = b

    def run(self):
        for index in range(10):
            print(f"我在学习{index}，进程 pid 是：{os.getpid()}，父进程 pid 是：{os.getppid()}")
            time.sleep(1)

if __name__ == '__main__':
    speak_process = SpeakProcess(1, 2)
    study_process = StudyProcess(3, 4)

    speak_process.start()
    study_process.start()

    speak_process.join()
    study_process.join()

    print("主进程结束")
```

\# 14 进程池  

```python
# 1. 创建一个进程池执行器，使用 submit 方法提交任务、使用 shutdown 方法等待任务完成
from concurrent.futures import ProcessPoolExecutor
import os

def work(n):
    print(f"子进程({os.getpid()})正在执行任务，参数是：{n}")

if __name__ == '__main__':
    # 创建进程池执行器
    executor = ProcessPoolExecutor(max_workers=3)
    # 使用 submit 方法提交任务
    executor.submit(work, 1)
    executor.submit(work, 2)
    executor.submit(work, 3)
    executor.submit(work, 4)
    executor.submit(work, 5)
    executor.submit(work, 6)
    executor.submit(work, 7)
    # 使用 shutdown 方法等待任务完成
    # shutdown 作用是：不再接收新的任务。
    # wait=True 的作用：阻塞主进程，等待进程池中所有任务执行完毕。
    executor.shutdown(wait=True)
```

```python
# 2. 获取子进程执行后的返回结果（Future 类的实例对象 + result 方法）
import os, time
from concurrent.futures import ProcessPoolExecutor

def work(n):
    print(f"子进程({os.getpid()})正在执行任务，参数是：{n}")
    time.sleep(1)
    return f"我是任务{n}的结果"

if __name__ == '__main__':
    # 创建进程池执行器
    executor = ProcessPoolExecutor(max_workers=3)
    # 使用 submit 方法提交任务
    # future1 = executor.submit(work, 1)
    # future2 = executor.submit(work, 2)
    # future3 = executor.submit(work, 3)
    # future4 = executor.submit(work, 4)
    # future5 = executor.submit(work, 5)
    # future6 = executor.submit(work, 6)
    # future7 = executor.submit(work, 7)
    futures = [executor.submit(work, index) for index in range(1, 8)]
    # print(future1.result())
    # print(future2.result())
    # print(future3.result())
    # print(future4.result())
    # print(future5.result())
    # print(future6.result())
    # print(future7.result())
    for future in futures:
        print(future.result())
    # 使用 shutdown 方法等待任务完成
    # shutdown 作用是：不再接收新的任务。
    # wait=True 的作用：阻塞主进程，等待进程池中所有任务执行完毕。
    executor.shutdown(wait=True)
    print(future1.result())
```

```python
# 3. 使用 as_completed：按“完成顺序”获取结果
import os, time
from concurrent.futures import ProcessPoolExecutor, as_completed

def work(n):
    print(f"子进程({os.getpid()})正在执行任务，参数是：{n}")
    time.sleep(1)
    return f"我是任务{n}的结果"

if __name__ == '__main__':
    print(f"主进程({os.getpid()})正在执行任务")
    # 创建进程池执行器
    executor = ProcessPoolExecutor(max_workers=3)
    # 使用 submit 方法提交任务（submit 只负责“提交任务”，不会阻塞主进程）
    futures = [executor.submit(work, index) for index in range(1, 8)]

    # 准备一个 result_list 列表去收集任务的具体结果
    result_list = []

    # 收集每个任务的结果
    for future in as_completed(futures):
        result_list.append(future.result())

    # 阻塞主进程，等待进程池中所有任务执行完毕
    executor.shutdown(wait=True)

    # 打印结果
    for result in result_list:
        print(result)
```

```python
# 4. 使用 add_done_callback() 方法，为任务添加完成时的回调函数
import os, time
from concurrent.futures import ProcessPoolExecutor

def work(n):
    print(f"子进程({os.getpid()})正在执行任务，参数是：{n}")
    time.sleep(1)
    return f"我是任务{n}的结果"

if __name__ == '__main__':
    print("start")
    # 创建一个进程池执行器
    executor = ProcessPoolExecutor(max_workers=3)

    # 准备一个 result_list 列表去收集任务的结果
    result_list = []

    # 任务完成后的回调函数
    def done_func(future):
        result_list.append(future.result())

    # 开启7个任务，并指定回调函数
    for index in range(1, 8):
        f = executor.submit(work, index)
        f.add_done_callback(done_func)

    # 关闭进程池
    executor.shutdown(wait=True)
    print(result_list)
    print("end")
```

```python
# 5. 使用 map 方法批量提交任务（注意：map方法是阻塞的，并且得到结果的顺序，与任务分配的顺序是一致的）
import os, time
from concurrent.futures import ProcessPoolExecutor

def work(n):
    print(f"子进程({os.getpid()})正在执行任务，参数是：{n}")
    time.sleep(1)
    return f"我是任务{n}的结果"

if __name__ == '__main__':
    print("start")
    # 创建一个进程池执行器
    executor = ProcessPoolExecutor(max_workers=3)

    # 开启7个任务，并指定回调函数
    results = executor.map(work, [1, 2, 3, 4, 5, 6, 7])
    print(list(results))

    # 关闭进程池
    executor.shutdown(wait=True)

    print("end")
```

```python
# 6. 使用 with：进程池的“自动回收”写法，离开 with 代码块时自动执行 shutdown(wait=True)
import os, time
from concurrent.futures import ProcessPoolExecutor

def work(n):
    print(f"子进程({os.getpid()})正在执行任务，参数是：{n}")
    time.sleep(1)
    return f"我是任务{n}的结果"

if __name__ == '__main__':
    print("start")
    # 创建一个进程池执行器
    with ProcessPoolExecutor(max_workers=3) as executor:
        # 开启7个任务，并指定回调函数
        results = executor.map(work, [1, 2, 3, 4, 5, 6, 7])
        print(list(results))

    print("end")
```

\# 15 使用 Thread 创建线程  

```python
import os
import time
# from multiprocessing import Process
from threading import get_native_id, Thread, RLock

def speak(lock):
    for index in range(5):
        with lock:
            print(f"我在说话{index}，进程 pid 是：{os.getpid()}，线程 id 是：{get_native_id()}")
            time.sleep(1)

def study(lock):
    for index in range(5):
        with lock:    
            print(f"我在学习{index}，进程 pid 是：{os.getpid()}，线程 id 是：{get_native_id()}")
            time.sleep(1)

if __name__ == "__main__":
    print("start")
    
    lock = RLock()

    t1 = Thread(target=speak, args=(lock,))
    t2 = Thread(target=study, args=(lock,))

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    print("end")
```

> 注意点 1: `t1` 和 `t2` 就对应着以后的两个子线程，在创建它们的时候，就要指定它们要执行的任务。  
> 注意点 2:此时的 `t1` 和 `t2` 只是代码层面的两个线程对象，操作系统还没有真的创建 `t1` 和 `t2` 两个进程。  

> 注意：一定要写 `if __name__ == "__main__"` 这个判断，原因如下：  
> 1. 当创建子进程时，Python 并不会把父进程内存里的 `speak` 函数直接交给子进程。  
> 2. Python 会启动一个全新的 Python 解释器进程，重新执行当前的 `.py` 文件（作为模块）。  
> 3. 在执行过程中，重新定义出一个 `speak` 函数，交给子进程。  

`Thread` 的参数：  
- `group`：默认值是 `None`（应当始终为 `None`）。
- `target`：子进程要执行的可调用对象，默认值为 `None`。
- `name`：进程名称，默认为 `None`，如果设置为 `None`,Python 会自动分配名字。
- `args`：给 `target` 传的位置参数（元组）。
- `kwargs`：给 `target` 传的关键字参数（字典）。
- `daemon`：标记进程是否为守护进程，取值为布尔值（默认为 `None`，表示从创建方进程继承）。

\# 16 继承 Thread 类创建线程  

```python
import os
import time
# from multiprocessing import Process
from threading import get_native_id, Thread, RLock

class SpeakThread(Thread):
    def __init__(self, lock, **kwargs):
        super().__init__(**kwargs)
        self.lock = lock

    def run(self):
        for index in range(5):
            with self.lock:
                print(f"我在说话{index}，进程 pid 是：{os.getpid()}，线程 id 是：{get_native_id()}")
                time.sleep(1)

class StudyThread(Thread):
    def __init__(self, lock, **kwargs):
        super().__init__(**kwargs)
        self.lock = lock

    def run(self):
        for index in range(5):
            with self.lock:    
                print(f"我在学习{index}，进程 pid 是：{os.getpid()}，线程 id 是：{get_native_id()}")
                time.sleep(1)

if __name__ == "__main__":
    print("start")

    lock = RLock()

    t1 = SpeakThread(lock)
    t2 = StudyThread(lock)

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    print("end")
```

\# 17 线程池  
参考 ![13. 多进程 多线程](#14%20进程池)  

```python
# 加载线程池模块
from concurrent.futures import ThreadPoolExecutor
```

\# 18 GIL（Global Interpreter Lock）全局解释器锁  
无论 CPU 有多少个核心，在某一时刻，只允许进程中的**一个线程**去执行 Python 代码。  

> CPython 解释器中的多线程模型，本质上是并发，而不是并行！（是快速切换，而不是同时进行）  
> 可以使用多进程利用 CPU 的多核性能。  


```vtable
{"rows":[[{"t":"对比维度","rs":1,"cs":1},{"t":"GIL 全局解释器锁","rs":1,"cs":1},{"t":"Lock / RLock","rs":1,"cs":1}],[{"t":"核心本质","rs":1,"cs":1},{"t":"解释器级别的强制限制","rs":1,"cs":1},{"t":"代码级别的逻辑约定","rs":1,"cs":1}],[{"t":"谁来控制","rs":1,"cs":1},{"t":"Python 解释器：解释器自动加锁、遇到 IO 或 超时自动释放","rs":1,"cs":1},{"t":"程序员：需要写代码 `lock.acquire()` 和 `lock.release()`","rs":1,"cs":1}],[{"t":"保护对象","rs":1,"cs":1},{"t":"保护“解释器不崩“维护引用计数、垃圾回收等底层结构的线程安全","rs":1,"cs":1},{"t":"保护”数据不算错“，维护用户定义的变量、操作顺序等业务逻辑的完整性","rs":1,"cs":1}],[{"t":"作用范围","rs":1,"cs":1},{"t":"全局唯一：一个进程里只有一个 GIL，管理所有线程","rs":1,"cs":1},{"t":"按需创建：可以创建 100 把不同的锁，分别保护 100 个不同的业务逻辑","rs":1,"cs":1}],[{"t":"如果没有","rs":1,"cs":1},{"t":"Python 解释器可能会崩溃","rs":1,"cs":1},{"t":"售票场景下，两个人可能买到同一张车票","rs":1,"cs":1}]]}
```

关于 GIL（Global Interpreter Lock）
	1. GIL 锁是 CPython 解释器中的一把互斥锁。
	2. GIL 锁的作用：无论 CPU 有多少个核心，在某一时刻，值允许同一个进程中的一个线程去执行 Python 代码。

\# 19 多进程和多线程  

```vtable
{"rows":[[{"t":"维度","rs":1,"cs":1},{"t":"多线程","rs":1,"cs":1},{"t":"多进程","rs":1,"cs":1}],[{"t":"执行单元","rs":1,"cs":1},{"t":"线程","rs":1,"cs":1},{"t":"进程","rs":1,"cs":1}],[{"t":"内存","rs":1,"cs":1},{"t":"共享同一进程内存","rs":1,"cs":1},{"t":"各自独立内存","rs":1,"cs":1}],[{"t":"GIL","rs":1,"cs":1},{"t":"受 GIL 限制","rs":1,"cs":1},{"t":"每个进程独立 GIL","rs":1,"cs":1}],[{"t":"真正并行","rs":1,"cs":1},{"t":"纯 Python CPU 任务：否","rs":1,"cs":1},{"t":"是","rs":1,"cs":1}],[{"t":"创建开销","rs":1,"cs":1},{"t":"小","rs":1,"cs":1},{"t":"大","rs":1,"cs":1}],[{"t":"通信方式","rs":1,"cs":1},{"t":"共享变量、锁、队列","rs":1,"cs":1},{"t":"队列、管道、共享内存","rs":1,"cs":1}],[{"t":"数据共享","rs":1,"cs":1},{"t":"容易，但需同步","rs":1,"cs":1},{"t":"难，需序列化","rs":1,"cs":1}],[{"t":"崩溃影响","rs":1,"cs":1},{"t":"一个线程崩可能拖垮进程","rs":1,"cs":1},{"t":"一个子进程崩不影响其他","rs":1,"cs":1}],[{"t":"适合场景","rs":1,"cs":1},{"t":"I/O 密集","rs":1,"cs":1},{"t":"CPU 密集","rs":1,"cs":1}]]}
```

### 12-19-1 GIL 是关键
CPython 里：  
- 同一进程内，同一时刻只有一个线程在执行 Python 字节码；
- 所以纯 Python 计算任务，多线程**不能真正并行**；
- 但 I/O 阻塞时会释放 GIL，其他线程可以跑；
- 多进程各自有独立 GIL，所以可以真正并行。

### 12-19-2 I/O 密集型：选多线程或 asyncio
典型任务：  
- 网络请求、爬虫、API 调用。
- 文件读写。
- 数据库查询。
- 消息队列收发。
- WebSocket。

#### 12-19-2-1 多线程

```python
from concurrent.futures import ThreadPoolExecutor
import requests

urls = [...]  # 很多 URL

def fetch(url):
    return requests.get(url).status_code

with ThreadPoolExecutor(max_workers=20) as ex:
    results = list(ex.map(fetch, urls))
```

优点：  
- 写法简单，同步代码直接丢进去。
- 适合已有阻塞库（`requests`、`pymysql` 等）。
- 线程切换开销小。

缺点：  
- 线程太多会上下文切换开销大。
- 共享数据要加锁。
- 不适合 CPU 密集。

#### 12-19-2-2 asyncio
```python
import asyncio
import aiohttp

async def fetch(session, url):
    async with session.get(url) as resp:
        return resp.status

async def main():
    async with aiohttp.ClientSession() as session:
        tasks = [fetch(session, url) for url in urls]
        return await asyncio.gather(*tasks)

asyncio.run(main())
```

优点：  
- 单线程内可支撑成千上万并发。
- 没有线程切换开销。
- 资源占用低。

缺点：  
- 必须用异步库（`aiohttp`、`asyncpg`、`httpx` 等）。
- 一旦混入同步阻塞调用，整个事件循环卡死。
- 编程模型更复杂。

#### 12-19-2-3 选择建议

```vtable
{"rows":[[{"t":"情况","rs":1,"cs":1},{"t":"推荐","rs":1,"cs":1}],[{"t":"已有同步阻塞库，改造成本高","rs":1,"cs":1},{"t":"多线程","rs":1,"cs":1}],[{"t":"高并发、连接数很多","rs":1,"cs":1},{"t":"asyncio","rs":1,"cs":1}],[{"t":"简单脚本、任务量不大","rs":1,"cs":1},{"t":"多线程","rs":1,"cs":1}],[{"t":"需要精细控制并发","rs":1,"cs":1},{"t":"asyncio","rs":1,"cs":1}]]}
```

\## 4. CPU 密集型：选多进程
典型任务：  
- 数值计算、矩阵运算。
- 图像 / 视频处理。
- 加密解密。
- 数据压缩。
- 大量纯 Python 循环。

```python
from concurrent.futures import ProcessPoolExecutor

def cpu_task(n):
    return sum(i * i for i in range(n))

if __name__ == "__main__":
    with ProcessPoolExecutor(max_workers=4) as ex:
        results = list(ex.map(cpu_task, [10**7] * 8))
```

优点：  
- 绕过 GIL，真正并行。
- 充分利用多核。 

缺点：  
- 进程创建开销大。
- 参数和返回值要 pickle。
- 内存不共享，通信成本高。
- 不能直接改共享变量。

> **I/O 密集用多线程或 asyncio；CPU 密集用多进程；混合场景用多进程 + 进程内异步 / 线程。**  
> **Python 里选择的第一依据是 GIL：纯 Python CPU 任务多线程无法并行，必须多进程。**


# 13 协程

## 13-1 什么是协程

**概念**：协程（Coroutine），是一种线程内部的任务调度机制，它通过事件循环，在用户态中实现任务的挂起与恢复执行，从而在遇到 IO 操作时，不让 CPU 等待，而是继续执行其它需要 CPU 的任务。  
协程的本质就是：在一个线程里，趁着某些任务在等 IO，把 CPU 交给其它任务去用。

![](../../../../03%20附件/attachments/知识附件/Python/1.%20Python/1.%20Python_20261012_1.png)

**关键点 1：协程不是线程，也不是进程**

- 协程不是操作系统提供的，并且 CPU 看不见协程。
- 操作系统不知道协程的存在。
- 协程是程序员在用户态，用代码“设计出来”的任务切换机制。

**关键点 2：协程发生在一个线程内部**

- 协程不是线程之间的切换。
- 而是线程内部多个任务之间的切换。
- 本质是一个线程里，写了很多任务，由事件循环统一调度。

**关键点 3：协程的核心能力：挂起与恢复**

- 当任务遇到 IO 操作时：任务会被挂起。
- 当 IO 操作完成后：任务会被恢复执行。

**关键点 4：协程依赖一个关键角色：事件循环**

- 事件循环负责：调度任务、判断是否该挂起、决定何时恢复执行，事件循环是协程系统的“大脑”。

**关键点 5：协程的目标是尽量减少线程切换**

- 在单线程场景下，最大化 CPU 利用率，特别适合 IO 密集型任务

\# 2 协程函数 vs 协程对象

- **协程函数（coroutine Function）**：使用『async 关键字』修饰的函数，就是协程函数。
- **协程对象（coroutine Object）**：调用『协程函数』，就会得到『协程对象』。

> 注意：调用『协程函数』，并不会执行『协程函数』中的代码。  

```python
# 定义一个协程函数
async def work():
    print('work开始')
    print('work执行中......')
    print('work结束')
    return '工作结果'

# 调用协程函数，会得到协程对象
coroutine_object = work()
```

将协程对象交给 `asyncio.run()`，`asyncio.run()` 会将协程对象包装成一个任务交给事件循环。

```python
# asyncio.run 方法做了3件事：
#   1.创建一个事件循环。
#   2.将收到的协程对象，包装成一个任务（task），交给事件循环。
#   3.启动事件循环。
# 注意：asyncio.run 会阻塞当前线程，直到任务执行完毕，并返回该任务 return 的最终结果。
result = asyncio.run(coroutine_object)
print(result)
```

\# 3 await 关键字

await 关键字有三个作用：

1. **挂起**：await 会暂停当前协程的执行。
2. **等待**：遇到 await 关键字，事件循环会立即安排 await 后面的对象去执行，并等待该对象执行完成，并且可以拿到执行结果。

**关键点**：在执行 await 后面的对象时，会出现两种情况：

- **情况一**：如果在执行该对象中的代码时，遇到了【await I/O 操作】（需要等待外部资源返回结果的操作）例如：网络请求、文件读写等，那 CPU 的控制权就会交给事件循环。事件循环会去调度循环中的其他任务（如果有的话）。
- **情况二**：如果该对象中的代码，不包含任何【await I/O 操作】。例如：print 打印、数学计算、逻辑计算等。此时事件循环拿不到 CPU 控制权，无法调度循环中的其他任务，不会发生任务切换。

3. **恢复**：当 await 后的对象执行完毕，事件循环会恢复之前被挂起的协程，该协程会从当时挂起的位置继续执行，并拿到返回值。

> **注意**：await 后面只能写『可等待对象』，常见可等待对象有：协程对象、Future 对象、Task 对象。  

```python
import asyncio

async def work():
    print('work开始')
    print('work执行中......')
    # await去等待一个协程对象（靠asyncio.sleep方法，返回一个协程对象）
    res = await asyncio.sleep(2)
    print(res)
    print('work结束')
    return '工作结果'

async def main():
    print('main开始')
    # await去等待一个协程对象（靠自己去编写协程函数，随后调用该函数来得到协程对象）
    res = await work()
    print(res)
    print('main结束')
    return 'main的返回值'

result = asyncio.run(main())
print(result)
```

\# 4 多个任务同步执行

使用 await 实现多个任务同步执行。

```python
import asyncio
import time

# 定义一个协程函数
async def work(n, delay):
    print(f'work{n}开始')
    print(f'work{n}执行中......')
    # 模拟一个IO等待
    await asyncio.sleep(delay)
    print(f'work{n}结束')
    return f'work{n}的返回值'

async def main():
    print('main开始')
    start = time.time()

    # 调用三次work函数，分别得到三个协程对象
    coroutine1 = work(1, 2)
    coroutine2 = work(2, 2)
    coroutine3 = work(3, 2)

    # 此处会等待coroutine1执行完成
    res1 = await coroutine1
    print(res1)

    # 等待上面的coroutine1完成后，再等待coroutine2完成
    res2 = await coroutine2
    print(res2)

    # 等待上面的coroutine2完成后，再等待coroutine3完成
    res3 = await coroutine3
    print(res3)

    print('main结束', time.time() - start)
    return '我是main的返回值'

# 将协程对象交给事件循环
result = asyncio.run(main())
print(result)
```

\# 5 多个任务异步执行

使用 `asyncio.create_task()` 方法向事件循环中添加任务，从而实现多个任务异步执行。

```python
import asyncio
import time

# 定义一个协程函数
async def work(n, delay):
    print(f'work{n}开始')
    print(f'work{n}执行中......')
    # 模拟一个IO等待
    await asyncio.sleep(delay)
    print(f'work{n}结束')
    return f'work{n}的返回值'

async def main():
    print('main开始')
    start = time.time()

    # asyncio.create_task 会把一个协程对象包装成一个可被事件循环调度的任务，并注册到事件循环中
    task1 = asyncio.create_task(work(1, 2))
    task2 = asyncio.create_task(work(2, 2))
    task3 = asyncio.create_task(work(3, 2))

    # 此处会等待task1执行完成
    res1 = await task1
    print(res1)

    # 等待上面的task1完成后，再等待task2完成
    res2 = await task2
    print(res2)

    # 等待上面的task2完成后，再等待task3完成
    res3 = await task3
    print(res3)

    print('main结束', time.time() - start)
    return '我是main的返回值'

# 将协程对象交给事件循环
result = asyncio.run(main())
print(result)
```

\# 6 asyncio.gather

`asyncio.gather` 方法可以把多个协程对象丢给事件循环，并在全部执行完后，一次性拿到所有结果。

```python
import asyncio
import time

# 定义一个协程函数
async def work(n, delay):
    print(f'work{n}开始')
    print(f'work{n}执行中......')
    # 模拟一个IO等待
    await asyncio.sleep(delay)
    print(f'work{n}结束')
    return f'work{n}的返回值'

async def main():
    print('main开始')
    start = time.time()

    # 把多个协程对象同时丢给事件循环，并在全部执行完后，一次性拿到所有结果。
    result = await asyncio.gather(work(1, 2), work(2, 2), work(3, 2))
    print(result)

    print('main结束', time.time() - start)
    return '我是main的返回值'

# 将协程对象交给事件循环
result = asyncio.run(main())
print(result)
```

\# 7 下载图片案例

### 13-7-1 传统方式下载图片（同步）

如下代码的特点：图片是一张一张下载的，当前图片没有下载完成，后一张图片的下载就不能开始，这属于典型的同步下载。

```python
import requests

def download_picture(url):
    print(f'开始下载：{url}')
    # 发送网络请求，获取这张图片
    response = requests.get(url)
    print('下载完毕')
    # 保存图片到本地
    with open(url[-10:], 'wb') as file:
        file.write(response.content)

def main():
    url_list = [
        'https://n.sinaimg.cn/spider20260129/217/w600h417/20260129/3e26-917ee55a8a42b8626807c332c24981de.png',
        'https://n.sinaimg.cn/finance/transform/97/w630h267/20260129/97c4-b211cc51784830f09ee19e450475c93b.png',
        'https://n.sinaimg.cn/spider20260129/539/w1439h700/20260129/e09a-cc2ca319e00f701ccfca3ebc62aa8772.png'
    ]
    for url in url_list:
        download_picture(url)

main()
```

### 13-7-2 协程方式下载图片（并发）

如下代码的特点：多张图片会几乎同时发起下载请求，当某一张图片在等待网络数据返回时，其它图片的下载任务并不会被阻塞，而是可以继续执行，这属于典型的协程并发下载。

```python
import aiohttp
import asyncio

async def download_picture(session, url):
    print(f'开始下载：{url}')
    # 发送网络请求，获取这张图片，请求发出去后，要等待服务器把数据返回，等的这段时间就是IO等待
    response = await session.get(url)
    # 等待数据（图片数据可能分多次传输，需要等待数据全部读完，等的这段时间也是IO等待）
    content = await response.read()
    print('下载完毕')
    # 保存图片到本地
    with open(url[-10:], 'wb') as file:
        file.write(content)
    # 释放连接资源（告诉 aiohttp，这个连接我不用了，你可以回收了）
    await response.release()

async def main():
    url_list = [
        'https://n.sinaimg.cn/spider20260129/217/w600h417/20260129/3e26-917ee55a8a42b8626807c332c24981de.png',
        'https://n.sinaimg.cn/finance/transform/97/w630h267/20260129/97c4-b211cc51784830f09ee19e450475c93b.png',
        'https://n.sinaimg.cn/spider20260129/539/w1439h700/20260129/e09a-cc2ca319e00f701ccfca3ebc62aa8772.png'
    ]
    # 创建会话对象（发请求的工具）
    session = aiohttp.ClientSession()
    # 创建多个协程对象
    coroutine_list = [download_picture(session, url) for url in url_list]
    # 将多个协程对象交给事件循环
    await asyncio.gather(*coroutine_list)
    # 关闭会话
    await session.close()

asyncio.run(main())
```

