---
onenote-id: 0-e66fa6ac3c160f6d026bd12844ec17d9!1-DBD29CD2C5C95FE5!se4e140a7c9e643aeac1c77b25db7eb21
---
# 什么是AJAX

1 AJAX = Asynchronous JavaScript and XML（异步的JavaScript和XML）  
2 AJAX不是新的编程语言，而是一种使用现有标准的新方法  
3 AJAX最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容  
4 AJAX不需要任何浏览器插件，但需要用户允许JavaScript在浏览器上执行  
5 XMLHttpRequest只是实现AJAX的一种方式
 
```HTML  
\<script\>  
function getMessage() {  
// 实例化一个XMLHttpRequest  
var request = new XMLHttpRequest();  
// 设置XMLHttpRequest对象的回调函数  
// request.readyState 1 2 3 4  
// request.status 响应状态码 响应行状态码  
request.onreadystatechange=function() {  
if (request.readyState == 4 && request.status == 200) {  
// 接收响应结果，处理结果  
// request.responseText 后端响应回来的响应体中的数据  
console.log(request.responseText);  
// 将信息放到指定的位置  
var inputEle = document.getElementById("message");  
inputEle.value = request.responseText;  
}  
}  
// 设置发送请求的方式和请求的资源路径  
request.open("GET", "/hello?username=prokyhoof");  
// 发送请求  
request.send();  
}  
\</script\>
 
\<body\>  
\<button onclick="getMessage()"\>button\</button\>  
\<input type="text" id="message"\>  
\</body\>  
```
 
## 问题

1 响应乱码问题  
2 响应信息格式不规范，处理方式不规范  
后端响应回来的信息应当有一个统一的格式，前后端共同遵守  
响应一个JSON串  
code 业务状态码 本次请求的业务是否成功？如果失败了，是什么原因失败的？不是响应报文中的响应码  
message 业务状态码的补充说明/描述  
data 本次响应的数据  
3 校验不通过，无法阻止表单提交问题