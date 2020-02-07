# 白话 UI.Vision Kantu 插件 | 全平台自动化

## 目录

- [UI.Vision Kantu 插件介绍](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH#uivision-kantu-%E6%8F%92%E4%BB%B6%E4%BB%8B%E7%BB%8D)
- [一、兵（Selenium IDE）](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH#%E4%B8%80%E5%85%B5selenium-ide)
- [二、军师（运行 Javascript 代码）](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH#%E4%BA%8C%E5%86%9B%E5%B8%88%E8%BF%90%E8%A1%8C-javascript-%E4%BB%A3%E7%A0%81)
- [三、特种兵（视觉命令）](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH#%E4%B8%89%E7%89%B9%E7%A7%8D%E5%85%B5%E8%A7%86%E8%A7%89%E5%91%BD%E4%BB%A4)
- [四、阵法（控制流程）](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH#%E5%9B%9B%E9%98%B5%E6%B3%95%E6%8E%A7%E5%88%B6%E6%B5%81%E7%A8%8B)
- [五、下旨（变量，传递信息）](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH#%E4%BA%94%E4%B8%8B%E6%97%A8%E5%8F%98%E9%87%8F%E4%BC%A0%E9%80%92%E4%BF%A1%E6%81%AF)

## UI.Vision Kantu 插件介绍

浏览器插件 UI.Vision Kantu，我们就叫它看图（Kantu）吧，是一款 RPA 工具。支持 Chrome 和 Firefox 浏览器，正是因为它是一款浏览器插件所以它可以实现全平台（Mac、Windows、Linux）的自动化操作。

![Mac、Windows、Linux 系统图标](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/pictures/Mac-Windows-Linux.png)

[UI.Vision RPA Chrome 浏览器插件下载地址](https://chrome.google.com/webstore/detail/uivision-rpa/gcbalfbdmfieckjlnblleoemohcganoc?hl=zh-CN)

[UI.Vision RPA 火狐浏览器插件下载地址](https://addons.mozilla.org/en-US/firefox/addon/rpa/?src=search)

[官方英文文档](https://ui.vision/rpa/docs)

要想完全掌握 UI.Vision Kantu 插件，就应该知道下面五个方面的知识。为了更好地学习和记忆，我把它归纳为「兵」、「军师」、「特种兵」、「阵法」、「下旨」。想象一下，你就是部落冲突的君主，你的对手就是“网页怪”，通过调动下方的这五个方面的命令从而达到目的。

![汇总](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/pictures/%E6%B1%87%E6%80%BB1.png)

## 一、兵（Selenium IDE）

[UI.Vision Kantu Selenium IDE Commands 英文文档](https://ui.vision/rpa/docs/selenium-ide)

### 使用介绍

![兵](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/pictures/%E5%85%B5.png)

UI.Vision 的 Selenium IDE 用于网页的自动化。使用方法就是“兵来将挡，水来土掩”，比如遇到按钮元素，我们就调用 `Click` 命令；遇到输入框，我们就调用 `Type` 命令；遇到下拉选项，我们就调用 `Select` 命令。根据不同的网页情况，调取不同的命令。

**👉 👉 👉 👉 👉 👉 [点击此处查看兵部](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/%E5%85%B5-selenium-%E5%91%BD%E4%BB%A4.md) 👈 👈 👈 👈 👈 👈**


## 二、军师（运行 Javascript 代码）
[executeScript (JS code, variable) - Selenium IDE command 英文文档](https://www.notion.so/UI-Vision-Kantu-0e620902c985476696258243f1567a48#80f0f633b7d1459c908e61f909d9df6e)

### 使用介绍

![军师](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/pictures/%E5%86%9B%E5%B8%88.png)

军师就是 `executeScript` 和 `executeScript_Sandbox` 这两个命令，后者为前者的升级版本。其实也是 Selenium IDE 中的命令（我特意从中拿了出来说明）一般情况下使用后者这个命令。

- `executeScript` 命令在当前选定的框架或窗口的上下文中执行一段 JavaScript 代码。

- `executeScript_Sandbox` 命令的功能完全相同，不过运行在沙盒中（不在网页内执行），可以避免一些错误发生

“军师”命令用于计算、获取信息等进阶操作。比如随机产生 0 到 10 的数据，比如计算 100 - 20 的算式。

**👉 👉 👉 👉 👉 👉 [点击此处查看军师命令](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/%E5%86%9B%E5%B8%88.md) 👈 👈 👈 👈 👈 👈**

## 三、特种兵（视觉命令）

[XClick (target, click type), XMove (target, mouse event) 英文文档](https://ui.vision/rpa/docs/xclick#vision)

[XType ("text") 英文文档](https://ui.vision/rpa/docs/xtype)

### 使用介绍

![特种兵](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/pictures/%E7%89%B9%E7%A7%8D%E5%85%B5.png)

「特种兵」模拟真实用户输入、点击等操作。主要用于桌面自动化，以及复杂网页自动化。是基于图像的自动化，模拟的是真人操作。

主要有 XClick、XType、XMove 命令。


## 四、阵法（控制流程）

[Flow Control Commands 英文文档](https://ui.vision/rpa/docs/selenium-ide#flowcontrol)

### 使用介绍

![阵法](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/pictures/%E9%98%B5%E6%B3%95.png)

### 使用介绍

一般情况下，Macro 执行的顺序是从上到下的。而「阵法」命令可以调整执行的顺序，加上判断条件，比如出现 A 我就点击「按钮 1」，要是 B 我就点击「按钮 2」

  
## 五、下旨（变量，传递信息）

[Internal variables 内部变量英文文档](https://ui.vision/rpa/docs)

### 使用介绍

![下旨](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/pictures/%E4%B8%8B%E6%97%A8.png)

「圣旨」就是传递信息，分为「内部变量」、「全局变量」以及「普通变量」。

- 「内部变量」可以理解为高祖时期就定下的命令，是带 `!` 的，无法废除，但是解读权在你，比如 `!REPLAYSPEED` 控制的是运行的速度，默认参数是 MEDIUM（中等速度），你可以修改为 FAST（快速）
- 「全局变量（用得较少）」
- 「普通变量（有时需要使用）」
