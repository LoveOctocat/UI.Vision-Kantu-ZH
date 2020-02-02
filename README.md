# 白话 UI.Vision Kantu 插件 | 全平台自动化

浏览器插件 UI.Vision Kantu，我们就叫它看图（Kantu）吧，是一款 RPA（【介绍】）工具。支持 Chrome 和 Firefox 浏览器，正是因为它是一款浏览器插件所以它可以实现全平台（Mac、Windows、Linux）的自动化操作。

![image]https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/pictures/Mac-Windows-Linux.png


Chrome 插件下载地址：[UI.Vision RPA 浏览器自动化工具](https://chrome.google.com/webstore/detail/uivision-rpa/gcbalfbdmfieckjlnblleoemohcganoc?hl=zh-CN)

官方文档：[UI Automation Open-Source Selenium IDE plus additional features, iMacros alternative](https://ui.vision/rpa/docs)

---

## 一、兵（Selenium IDE）

[UI.Vision Kantu Selenium IDE Commands 英文文档](https://ui.vision/rpa/docs/selenium-ide)

### 使用介绍

UI.Vision RPA 的 Selenium IDE 用于网页的自动化。使用方法就是“兵来将挡，水来土掩”，遇到按钮元素，我们就调用 `Click` 命令；遇到输入框，我们就调用 `Type` 命令；遇到下拉选项，我们就调用 `Select` 命令。根据具体的网页情况，调取不同的命令即可。

【全命令链接 🔗】

### UI.Vision RPA 与 Selenium IDE 的区别?

当旧版本的 Selenium IDE for Firefox 停止更新了，UI.Vision 团队就启动了 UI.Vision RPA 的开源项目。目的是创建一个全新的、现代 Web 自动化工具。UI.Vision 团队从头实现了所有重要的 Selenium IDE 命令。几个月后，Sel IDE 团队恢复了旧的 Selenium IDE 项目。所以两者之间的代码是不同的。两者都是开源的，但是 license 不同 [Hi from the Kantu for Chrome / Selenium IDE "Light" team #19](https://github.com/SeleniumHQ/selenium-ide/issues/19)

## 二、军师（运行 Javascript 代码）
[executeScript (JS code, variable) - Selenium IDE command 英文文档](https://www.notion.so/UI-Vision-Kantu-0e620902c985476696258243f1567a48#80f0f633b7d1459c908e61f909d9df6e)

### 使用介绍

军师就是 `executeScript` 和 `executeScript_Sandbox` 这两个命令，后者为前者的升级版本。其实也是 Selenium IDE 中的命令（我特意从中拿了出来说明）一般情况下使用后者这个命令。

- `executeScript` 命令在当前选定的框架或窗口的上下文中执行一段 JavaScript 代码。

- `executeScript_Sandbox` 命令的功能完全相同，不过运行在沙盒中（不在网页内执行），可以避免一些错误发生

“军师”命令用于计算、获取信息等进阶操作。比如随机产生 0 到 10 的数据，比如计算 100 - 20 的算式。



## 三、特种兵（视觉命令）

[XClick (target, click type), XMove (target, mouse event) 英文文档](https://ui.vision/rpa/docs/xclick#vision)
[XType ("text") 英文文档](https://ui.vision/rpa/docs/xtype)

### 使用介绍

「特种兵」模拟真实用户输入、点击等操作。主要用于桌面自动化，以及复杂网页自动化。是基于图像的自动化，模拟的是真人操作。

主要有 XClick、XType、XMove 命令。


## 四、阵法（控制流程）

[Flow Control Commands 英文文档](https://ui.vision/rpa/docs/selenium-ide#flowcontrol)

### 使用介绍

一般情况下，Macro 执行的顺序是从上到下的。而「阵法」命令可以调整执行的顺序，加上判断条件，比如出现 A 我就点击「按钮 1」，要出现的是 B 我就点击「按钮 2」

  
## 五、圣旨（变量，传递信息）

[Internal variables 内部变量英文文档](https://ui.vision/rpa/docs)

### 使用介绍

「圣旨」就是传递信息，分为「内部变量」、「全局变量」以及「普通变量」。

- 「内部变量」可以理解为高祖时期就定下的命令，是带 `!` 的，无法废除，但是解读权在你，比如 `!REPLAYSPEED` 控制的是运行的速度，默认参数是 MEDIUM（中等速度），你可以修改为 FAST（快速）
- 「全局变量（用得较少）」
- 「普通变量（有时需要使用）」
