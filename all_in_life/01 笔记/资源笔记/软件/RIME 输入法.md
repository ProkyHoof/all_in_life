---
tags:
  - 资源
类型: 软件
分类: 输入法
链接: "[小狼毫输入法](https://rime.im/download/)"
日期: 2026-09-22
---

# 简介
本文档描述了一套小狼毫（Rime for Windows）输入法平台，并采用雾凇拼音（rime-ice）作为核心输入方案的个性化配置。小狼毫是 Rime 在 Windows 上的官方发行版，提供稳定的输入法引擎；雾凇拼音则是运行于 Rime 之上的一套高质量开源方案，包含全拼、双拼、词库、Emoji、符号映射等完整功能。  
本配置不修改雾凇拼音的核心输入逻辑，仅在其基础上进行界面美化、标点行为调整、通知关闭等个性化修改，使其更符合个人使用习惯。成果包括：苹果风格浅色皮肤、中文标点直接上屏、关闭 Shift 切换提示、柔和阴影与圆角、隐藏托盘图标等。  
# 用途
其配置适用于以下场景：  

```vtable
{"rows":[[{"t":"场景","rs":1,"cs":1},{"t":"说明","rs":1,"cs":1}],[{"t":"日常中文输入","rs":1,"cs":1},{"t":"使用雾凇拼音方案，词库丰富，输入准确","rs":1,"cs":1}],[{"t":"个性化界面","rs":1,"cs":1},{"t":"自定义苹果风格皮肤、纯白北京、灰色高亮、圆角、阴影","rs":1,"cs":1}],[{"t":"标点符合中文习惯","rs":1,"cs":1},{"t":"中文模式下直接输出中文标点，英文模式下自动输出英文标点","rs":1,"cs":1}],[{"t":"厌恶切换提示","rs":1,"cs":1},{"t":"关闭中英文切换时的提示窗口，保持界面清爽","rs":1,"cs":1}],[{"t":"隐私保护","rs":1,"cs":1},{"t":"小狼毫完全离线运行，无广告、无云控、不收集数据","rs":1,"cs":1}],[{"t":"低资源占用","rs":1,"cs":1},{"t":"相比商业输入法，内存占用低，适合长期后台运行","rs":1,"cs":1}]]}
```

# 使用
## 安装小狼毫和雾凇拼音
1. 从 [下載及安裝 | RIME | 中州韻輸入法引擎](https://rime.im/download/) 下载最新版并安装。  
2. 从 [GitHub - iDvel/rime-ice: Rime 配置：雾凇拼音 | 长期维护的简体词库 · GitHub](https://github.com/iDvel/rime-ice) 下载 `main.zip`。  
3. 复制到用户文件夹：
	解压后，将所有文件复制到小狼毫用户文件夹，覆盖同名文件夹。
4. 重新部署。
	右键任务栏小狼毫图标 $\to$ 重新部署。首次部署时间较长，请耐心等待。
5. 启用雾凇拼音。
	右键小狼毫图标 $\to$ 输入法设定，勾选“雾凇拼音”，点击确定。
## 核心配置文件清单  

```vtable
{"rows":[[{"t":"文件/文件夹","rs":1,"cs":1},{"t":"作用","rs":1,"cs":1}],[{"t":"`rime_ice.schema.yaml`","rs":1,"cs":1},{"t":"雾凇拼音主方案文件","rs":1,"cs":1}],[{"t":"`rime_ice.dict.yaml`","rs":1,"cs":1},{"t":"雾凇拼音词库汇总文件","rs":1,"cs":1}],[{"t":"`cn_dicts/`","rs":1,"cs":1},{"t":"中文词库文件夹","rs":1,"cs":1}],[{"t":"`en_dicts/`","rs":1,"cs":1},{"t":"英文词库文件夹","rs":1,"cs":1}],[{"t":"`rime_ice.yaml`","rs":1,"cs":1},{"t":"雾凇拼音方案的个人补丁（标点、快捷键等）","rs":1,"cs":1}],[{"t":"`weasel.yaml`","rs":1,"cs":1},{"t":"全局界面皮肤、配色、字体、布局、阴影、通知等","rs":1,"cs":1}],[{"t":"`default.yaml`","rs":1,"cs":1},{"t":"全局快捷键、方案列表等","rs":1,"cs":1}],[{"t":"`build/`","rs":1,"cs":1},{"t":"部署后生成的编译文件夹。可清理后重新部署","rs":1,"cs":1}]]}
```

## 自定义苹果风格皮肤  
编辑 `weasel.yaml`，修改或添加以下内容：  

``` yaml
patch:
  # 启用苹果风格配色
  "style/color_scheme": macos_style

  # 全局字体（优先苹方，无则回退微软雅黑）
  "style/font_face": "PingFang SC, Microsoft YaHei UI"
  "style/font_point": 14
  "style/label_font_point": 12
  "style/comment_font_point": 12
  "style/inline_preedit": true
  "style/horizontal": true

  # 布局
  "style/layout/border_width": 0
  "style/layout/corner_radius": 8
  "style/layout/round_corner": 6
  "style/layout/shadow_radius": 8
  "style/layout/shadow_offset_x": 0
  "style/layout/shadow_offset_y": 2
  "style/layout/margin_x": 10
  "style/layout/margin_y": 8
  "style/layout/hilite_padding": 6
  "style/layout/hilite_spacing": 6
  "style/layout/candidate_spacing": 20

  # 定义苹果风格配色
  "preset_color_schemes/+":
    macos_style:
      name: "苹果风格 / macOS Style"
      author: "Custom"
      back_color: 0xffffffff
      border_color: 0x00000000
      shadow_color: 0x20000000
      text_color: 0xff333333
      label_color: 0xff999999
      comment_text_color: 0xffaaaaaa
      candidate_text_color: 0xff333333
      hilited_text_color: 0xff000000
      hilited_back_color: 0x00000000
      hilited_candidate_back_color: 0xffe5e5e5   # 选中项灰色高亮
      hilited_candidate_text_color: 0xff000000
      hilited_candidate_label_color: 0xff333333
      hilited_comment_text_color: 0xff666666
```

## 自定义中文标点  
在 `rime_ice.yaml` 或 `default.yaml` 中添加 `punctuator` 配置，让中文模式下标点直接上屏，不弹候选框。推荐配置如下（以 `rime_ice.yaml` 为例）：  

``` yaml
patch:
  punctuator:
    half_shape:
      "\\": "、"
      "`": "·"
      ",": "，"
      ".": "。"
      ";": "；"
      ":": "："
      "?": "？"
      "!": "！"
      "\"": "“"
      "'": "‘"
      "<": "《"
      ">": "》"
      "(": "（"
      ")": "）"
      "[": "【"
      "]": "】"
      "{": "｛"
      "}": "｝"
      "/": "/"
      "-": "-"
      "_": "——"
      "+": "+"
      "=": "="
      "*": "*"
      "&": "&"
      "%": "%"
      "$": "$"
      "#": "#"
      "@": "@"
      "~": "～"
      "|": "|"
      "^": "……"
    full_shape:
      "\\": "、"
      "`": "·"
      ",": "，"
      ".": "。"
      ";": "；"
      ":": "："
      "?": "？"
      "!": "！"
      "\"": "“"
      "'": "‘"
      "<": "《"
      ">": "》"
      "(": "（"
      ")": "）"
      "[": "【"
      "]": "】"
      "{": "｛"
      "}": "｝"
      "/": "／"
      "-": "－"
      "_": "——"
      "+": "＋"
      "=": "＝"
      "*": "＊"
      "&": "＆"
      "%": "％"
      "$": "￥"
      "#": "＃"
      "@": "＠"
      "~": "～"
      "|": "｜"
      "^": "……"
```

> 注意：雾凇拼音自带一套标点配置，如果直接覆盖可能影响其他符号输入。建议在补丁文件中以 `patch` 方式合并，保留雾凇的其他符号映射。  

## 关闭切换提醒于托盘图标  
在 `weasel.yaml` 中添加：  

``` yaml
patch:
  show_notifications: false
  show_notifications_when: never
```

在 `style:` 部分添加：  

``` yaml
style:
  display_tray_icon: false
```

## 重新部署  
所有配置修改后，必须右键小狼毫图标 $\to$ **重新部署**。若部署失败，检查 YAML 缩进（只能用空格）、文件编码（UTF-8 无 BOM）、路径是否正确。
# 使用心得  
## 标点配置要谨慎  
雾凇拼音自带丰富的符号映射（如 `v` 模式、Emoji 等），直接覆盖 `punctuator` 可能导致部分功能失效。建议只修改基础标点，保留雾凇的其他符号配置。如果发现某些符号打不出来，优先检查是否与雾凇的 `symbols_v.yaml` 冲突。  
## 词库不是越大越好  
雾凇拼音默认启用了 `tencent.dict.yaml`（约 16.9 MB），加载后内存占用会明显上升，首次部署也很慢。若感觉卡顿，可在 `rime_ice.dict.yaml` 中注释掉 `cn_dicts/tencent` 和 `cn_dicts/41448`。仅保留 `base`、`ext`、`en` 已能满足绝大多数日常输入。  
## 图片背景容易失败  
小狼毫支持 `background_image`，但常见失败原因有：  
- 路径包含空格或中文。  
- 图片放在 `Program Files` 等受保护目录，后台进程无权限读取。  
- 背景色不透明遮住图片。  
- 配置层级错误。  

推荐将图片放在用户文件夹下的 `bg/` 子目录，使用相对路径 `bg/logo.png`，并确保 `back_color` 为完全透明（`0x00ffffff`）或半透明。  
## 阴影效果需同时设置半径与颜色  
仅设置 `shadow_radius` 不够，还必须在配色方案中设置非透明的 `shadow_color`。例如：  

``` yaml
"style/layout/shadow_radius": 8
"preset_color_schemes/macos_style/shadow_color": 0 x 20000000
```

颜色格式为 `0xAARRGGBB`，`AA` 表示透明度。  
## 关闭 Shift 切换提示  
`show_notifications: false` 可关闭所有切换提示，`show_notifications_when: never` 进一步确保。若想隐藏托盘图标，设置 `display_tray_icon: false`。  
## 方案列表里选择“雾凇拼音”  
安装完整雾凇拼音后，在“输入法设定”中应勾选“雾凇拼音”，而不是“明月拼音·简化字”。这样所有雾凇的词库、符号、Emoji 功能才会完整生效。  
## 备份与恢复  
建议定期备份整个用户文件夹。可使用 Git 管理，或直接压缩成 zip。重装系统或更换电脑时，可快速恢复配置。  
## 游戏兼容性  
在部分游戏中，小狼毫可能被反作弊系统拦截，导致无法切换或卡顿。若常玩游戏，建议保留一个系统输入法作为备用。  
# 常见问题排查  

| 问题      | 可能原因                            | 解决方法                                      |
| ------- | ------------------------------- | ----------------------------------------- |
| 皮肤不生效   | YAML 缩进错误 / 配色名不对               | 检查缩进；确保 `color_scheme` 与定义的方案名一致          |
| 标点仍弹候选框 | 配置写成了数组                         | 改为单值字符串，如 `",": "，"`                      |
| 标点冲突    | 雾凇自带符号映射拦截                      | 检查 `rime_ice.yaml` 中是否覆盖了雾凇的 `punctuator` |
| 图片背景不显示 | 路径含空格/权限不足                      | 移至用户文件夹下 `bg/`，使用相对路径                     |
| 切换提示未关闭 | 版本不支持 `show_notifications_when` | 只保留 `show_notifications: false`           |
| 部署失败    | 编码错误 / Tab 缩进                   | 使用 VS Code 检查编码与缩进                        |

# 维护建议  
1. 定期更新雾凇拼音，更新后重新部署。  
2. 升级小狼毫前，备份 `*.custom.yaml` 及词库文件。  
3. 若配置混乱，可删除 `build/` 文件夹内容，再重新部署。  
4. 保持用户文件夹路径简单，避免空格、中文和系统保护目录。  
5. 如需添加新方案，在 `default.yaml` 的 `schema_list` 中列出。  

# 总结  
本配置基于 **小狼毫（Rime）输入法平台**，采用 **雾凇拼音方案** 作为核心输入引擎，并在此基础上进行界面美化、标点行为调整、通知关闭等个性化修改。通过补丁文件实现，既保留了雾凇拼音强大的词库和功能，又获得了干净、安静、美观的输入体验。适合愿意折腾、重视隐私和定制的人长期使用。  