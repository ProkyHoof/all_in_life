---
onenote-id: 0-35ef6790fcc748099fa291833fa0106f!1-DBD29CD2C5C95FE5!sf08401c013c344b18cc40c380173894e
---
# Stream流

## Stream流的思想

### Stream流的作用

结合了Lambda表达式，简化集合，数组的操作。

### Stream流的使用步骤

1. 先得到一条Stream流（流水线），并把数据放上去。
2. 使用**中间方法**对流水线上的数据进行操作。
3. 使用**终结方法**对流水线上的数据进行操作。

|   |   |   |
|---|---|---|
|获取方式|方法名|说明|
|单列集合|default Stream\<E\> stream()|Collection中的默认方法|
|双列集合|无|无法直接使用Stream流|
|数组|public static\<T\> Stream\<T\> stream(T[] array)|Arrays工具类中的静态方法|
|一推零散数据|public static\<T\> Stream\<T\> of(T…values)|Stream接口中的静态方法|
 
**单列集合获取数据流**

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8|ArrayList**\<**String**\>** list **=** **new** ArrayList**\<\>();**  <br>Stream**\<**String**\>** stream1 **=** list**.**stream**();**  <br>stream**.**forEach**(****new** Consumer**\<**String**\>() {**  <br>@Override  <br>**public void** accept**(**String s**) {**  <br>System**.**out**.**println**(**s**);**  <br>**}**  <br>**});**|

利用Lambda表达式简写为：

|   |   |
|---|---|
|1|list**.**stream**().**forEach**(**s **-\>** System**.**out**.**println**(**s**));**|

**双列集合获取数据流**

- 第一种方法：

|   |   |
|---|---|
|1  <br>2|HashMap**\<**String**,** String**\>** hm **=** **new** HashMap**\<\>();**  <br>hm**.**keySet**().**stream**().**forEach**(**s **-\>** system**.**out**.**println**(**s**));**|

- 第二种方法：

|   |   |
|---|---|
|1|hm**.**entrySet**().**stream**().**forEach**(**s **-\>** system**.**out**.**println**(**s**));**|

**注意：**  
第一种方法得到的是HashMap中的键属性流，而第二种方法得到的是HashMap中的键值对属性流。
 
**数组获取数据流**

|   |   |
|---|---|
|1  <br>2|**int****[]** arr **= {****1****,** **2****,** **3****,** **4****};**  <br>Arrays**.**stream**(**arr**).**forEach**(**s **-\>** system**.**out**.**println**(**s**));**|
 
**一推零散数据获取数据流（数据必须是同一类型的）**

|   |   |
|---|---|
|1|Stream**.**of**(****1****,** **2****,** **3****,** **4****).**forEach**(**s **-\>** system**.**out**.**println**(**s**));**|

**注意：**  
Stream接口中静态方法of的细节。方法的形参是一个可变参数，可以传递一堆零散的数据，也可以传递数组。但是数组必须是引用数据类型的，如果传递基本数据类型，是会把整个数组当作一个元素，放到Stream流中。
 
## Stream流的中间方法

![](OneNote/JavaNote/Java/%E8%BF%9B%E9%98%B6/Stream%E6%B5%81%20image%201796b27108af6b24.png)  

**注意****1****：**中间方法，返回新的Stream流，原来的Stream流只能使用一次，建议使用链式编程。  
**注意****2**：修改Stream流中的数据，不会影响原来集合或者数组中的数据。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8|ArrayList**\<**String**\>** list **=** **new** ArrayList**\<\>();**  <br>Collections**.**add**(**list**,** "ProkyHoof-1"**,** "ProkyHoof-2"**,** "ProkyHoof-3"**);**  <br>list**.**stream**().**filter**(****new** Predicate**\<**String**\>() {**  <br>@Override  <br>**public boolean** test**(**String s**) {**  <br>**return** s**.**startsWith**(**"Proky"**);**  <br>**}**  <br>**}).**forEach**(**s **-\>** System**.**out**.**println**(**s**));**|

简写为：

|   |   |
|---|---|
|1|list**.**stream**().**filter**(**s **-\>** s**.**startsWith**(**"Proky"**)).**forEach**(**s **-\>** System**.**out**.**println**(**s**));**|

规范书写Stream流的格式：

|   |   |
|---|---|
|1  <br>2  <br>3|list**.**stream**()**  <br>**.**filter**(**s **-\>** s**.**startsWith**(**"Proky"**))**  <br>**.**forEach**(**s **-\>** System**.**out**.**println**(**s**));**|

|   |   |
|---|---|
|1|list**.**stream**().**limit**(****3****);** //就是前三个元素|

|   |   |
|---|---|
|1|list**.**stream**().**skip**(****1****);** //跳过前1个元素|

|   |   |
|---|---|
|1|list**.**stream**().**distinct**();**|

|   |   |
|---|---|
|1|stream**.**concat**(**list1**.**stream**(),** list2**.**stream**()).**forEach**(**s **-\>** System**.**out**.**println**(**s**));**|

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9|list**.**stream**().**map**(****new** Function**\<**String**,** Integer**\>() {**  <br>@Override  <br>**public** Integer apply**(**String s**) {**  <br>String**[]** arr **=** s**.**split**(**"-"**);**  <br>String ageString **=** arr**[****1****];**  <br>**int** age **=** Integer**.**parseInt**(**ageString**);**  <br>**return** age**;**  <br>**}**  <br>**}).**forEach**(**s **-\>** System**.**out**.**println**(**s**));**|

**注意**：  
第一个类型：流中原本的数据类型。  
第二个类型：要转换成的数据类型。  
apply的形参s：依次表示流里面的每一个数据。  
返回值：表示转换之后的数据。  
当map方法执行完毕之后，流上的数据就变成了整数。  
所以在下面forEach当中，s依次表示流里面的每一个数据，这个数据现在就是整数类型。  
简化成Lambda表达式为：

|   |   |
|---|---|
|1  <br>2  <br>3|list**.**stream**()**  <br>**.**map**(**s **-\>** Integer**.**parseInt**(**s**.**split**(**"-"**)[****1****]))**  <br>**.**forEach**(**s **-\>** System**.**out**.**println**(**s**));**|

## Stream流的终结方法

![](OneNote/JavaNote/Java/%E8%BF%9B%E9%98%B6/Stream%E6%B5%81%20image%20567887506c08a9f1.png)  

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|list**.**stream**().**forEach**(****new** Consumer**\<**String**\>() {**  <br>@Override  <br>**public void** accept**(**String s**) {**  <br>System**.**out**.**println**(**s**);**  <br>**}**  <br>**});**|

Consumer的泛型：表示流中数据的类型。  
accept方法的形参s：依次表示流里面的每一个数据。  
方法体：对每一个数据的处理操作（打印）。  
用Lambda表达式简写为：

|   |   |
|---|---|
|1|list**.**stream**().**forEach**(**s **-\>** System**.**out**.**println**(**s**));**|

|   |   |
|---|---|
|1  <br>2|**long** count **=** list**.**stream**().**count**();**  <br>System**.**out**.**println**(**count**);**|

|   |   |
|---|---|
|1  <br>2|Object**[]** arr1 **=** list**.**stream**().**toArray**();**  <br>System**.**out**.**println**(**Arrays**.**toString**(**arr1**));**|

InterFunction的泛型：具体类型的数组。  
apply的形参：流中数据的个数，要跟数组的长度保持一致。  
方法体：就是创建数组。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6|list**.**stream**().**toAraay**(****new** InterFunction**\<**String**[]\>() {**  <br>@Override  <br>**public** String**[]** apply**(****int** value**) {**  <br>**return new** String**[**value**];**  <br>**}**  <br>**});**|

toArray方法的参数的作用：负责创建一个指定类型的数组。  
toArray方法的底层，会依次得到流里面的每一个数据，并把数据放到数组当中。  
toArray方法的返回值：是一个装有流里面所有数据的数组。

|   |   |
|---|---|
|1  <br>2|String**[]** arr1 **=** list**.**stream**().**toArray**(**value **-\>** **new** String**[**value**]);**  <br>System**.**out**.**println**(**Arrays**.**toString**(**arr1**));**|

|   |   |
|---|---|
|1  <br>2  <br>3|List**\<**String**\>** newList **=**list**.**stream**()**  <br>**.**filter**(**s **-\>** "男"**.**equals**(**s**.**split**(**"-"**)[****1****]))**  <br>**.**collect**(**Collectors**.**tolist**());**|

收集List集合中

收集Set集合中

|   |   |
|---|---|
|1  <br>2  <br>3|Set**\<**String**\>** newlist2 **=** list**.**stream**()**  <br>**.**filter**(**s **-\>** "男"**.**equals**(**s**.**split**(**"-"**)[****1****]))**  <br>**.**collect**(**Collectors**.**toSet**());**|

收集Map集合中  
参数一  
Function泛型一：表示流中每一个数据的类型。  
Function泛型二：表示Map集合中键的数据类型。  
方法apply形参：依次表示流里面的每一个数据。  
方法体：生成键的代码。  
返回值：已经生成的键。  
参数二  
Function泛型一：表示流中每一个数据的类型。  
Function泛型二：表示Map集合中值的数据类型。  
方法apply形参：依次表示流里面的每一个数据。  
方法体：生成值的代码。  
返回值：已经生成的值。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7  <br>8  <br>9  <br>10  <br>11  <br>12  <br>13  <br>14  <br>15  <br>16|Map**\<**String**,** Integer**\>** map **=** list**.**stream**()**  <br>**.**filter**(**s **-\>** "男"**.**equals**(**s**.**split**(**"-"**)[****1****]))**  <br>**.**collect**(**Collectors**.**toMap**(****new** Function**\<**String**,** String**\>() {**  <br>@Override  <br>**public** String apply**(**String s**) {**  <br>**return** s**.**split**(**"-"**)[****0****];**  <br>**}**  <br>**},**  <br>**new** Funtion**\<**String**,** Integer**\>() {**  <br>@Override  <br>**public** Integer apply**(**String s**) {**  <br>**return** Integer**.**parseInt**(**s**.**split**(**"-"**)[****2****]);**  <br>**}**  <br>**}**  <br>**));**  <br>System**.**out**.**println**(**map**);**|

**注意**：如果我们要收集到Map集合中，键不能重复，否则会报错。

|   |   |
|---|---|
|1  <br>2  <br>3  <br>4  <br>5  <br>6  <br>7|Map**\<**String**,** Integer**\>** map **=** list**.**stream**()**  <br>**.**filter**(**s **-\>** "男"**.**equals**(**s**.**split**(**"-"**)[****1****]))**  <br>**.**collect**(**Collectors**.**toMap**(**  <br>s **-\>** s**.**split**(**"-"**)[****0****],**  <br>s **-\>** Integer**.**parseInt**(**s**.**split**(**"-"**)[****2****])**  <br>**));**  <br>System**.**out**.**println**(**map**);**|

**总结**

1. Stream流的作用

**结合了****Lambda****表达式，简化集合、数组的操作。**

3. Stream的使用步骤
	- **获取****Stream****的流对象。**
	- **使用中间方法处理数据。**
	- **使用终结方法处理数据。**
4. 如何获取Stream流对象。
	- **单列集合：****Collection****中的默认方法****stream****。**
	- **双列集合：不能直接获取。**
	- **数组：****Arrays****工具类型中的静态方法****stream****。**
	- **一推零散的数据：****Stream****接口中的静态方法****of****。**
5. 常见方法
	- **中间方法：****filter****，****limit****，****skip****，****distinct****，****concat****，****map**
	- **终结方法：****forEach****，****count****，****collect**
 
## 练习

![](OneNote/JavaNote/Java/%E8%BF%9B%E9%98%B6/Stream%E6%B5%81%20image%20f4ced89fe48bc55d.png)  
![](OneNote/JavaNote/Java/%E8%BF%9B%E9%98%B6/Stream%E6%B5%81%20image%20693ff91bd8782e3e.png)  
![](OneNote/JavaNote/Java/%E8%BF%9B%E9%98%B6/Stream%E6%B5%81%20image%20060bb5f809a6abd5.png)