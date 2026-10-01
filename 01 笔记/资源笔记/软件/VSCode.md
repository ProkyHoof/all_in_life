---
tags:
  - 资源
类型: 软件
分类: 编辑器
链接:
日期: 2026-09-18
---

# 1 简介
VSCode（Visual Studio Code）是微软开发的一款免费、开源的“代码编辑器”。  
你可以理解为一个超级智能的记事本——专门用来写代码，但本身不像 Pycharm，IDEA 那样复杂。  
# 2 用途
- 插件生态：装 Python 插件就支持 Python，装 Java 插件就支持 Java，装 C++ 插件就支持 C++。
- 内置终端：不用切窗口，直接在 VSCode 里运行命令。
- 内置 Git：可以提交、拉取、查看历史。
- 调试功能：支持断点、单步执行、查看变量。
- 智能提示：补全、跳转定义、查找引用。
- 远程开发：可以连服务器、连 WSL、连 Docker。

# 3 插件推荐  
## 3.1 background  
作用：设置 VSCode 中的背景图片。  
1. 设置 background 的 json 文件。
2. “设置” $\to$ “扩展” $\to$ “background”。
	1. Editor：编辑器，也就是你编写代码的背景。
	2. Fullscreen：全屏，如果应用这个就不能再写其他的设备了，不然会重叠，这个全屏包括了能够看到的全部界面。
	3. Panel：面板区，也就是底边的调式输出等地方。
	4. Sidebar：侧边区，也就是唤出拓展的地方。
3. 编写 CSS 代码。
局部布局的背景设置：

``` json
"background.editor": {
	"useFront": false,  // 决定图片是否显示在代码的前面
	"style": {
		"background-position": "0% 50%",  // 图片对齐位置。0% 50% 表示水平对齐，垂直居中
		"background-size": "auto",  // 图片缩放方式。auto 表示按图片原尺寸显示。
		"opacity": 0.1  // 透明度，数值范围 0 ~ 1。 
	},
	"style": [],  // 留空的数组，用于写额外的自定义 CSS 样式。
	"image": ["file:///E:/documents/wallpaper/vscode.jpg"],  // 图片的绝对路径数组。
	"interval": 0,  // 轮播间隔，0 表示不自动轮播。
	"random": false  // 是否随机切换图片。false 表示按照顺序切换（目前只有一张图，所以没区别）
}
```

> 如果 `"useFront" = true`，图片会覆盖在代码上，可能会影响你看代码。通常建议设为 `false`，让图片作为底层背景。  

全局布局的背景设置：  

``` json
"background.fullscreen": {
    "images": [  // 背景图片的路径。
        "file:///E:/documents/wallpaper/vscode.jpg"
    ],
    "opacity": 0.1,  // 透明度，范围是 0~1。
    "size": "cover",  // 缩放方式。cover 表示等比缩放图片以铺满整个窗口，超出部分会被裁剪。
    "position": "center",  // 图片位置。center 表示居中显示。
    "styles": [],  // 自定义 CSS 数组，目前是空的。如果需要额外调整（比如加模糊效果），可以再这里写 CSS。
    "interval": 0,  // 轮播间隔。0 表示不自动轮播。
    "random": false  // 是否随机切换图片。false 表示按顺序切换。
}
```
# 4 快捷键  

```vtable
{"rows":[[{"t":"快捷键","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1}],[{"t":"Ctrl + ,","rs":1,"cs":1},{"t":"打开设置","rs":1,"cs":1}],[{"t":"<br>","rs":1,"cs":1},{"t":"","rs":1,"cs":1}]]}
```

# 5 使用心得
- 