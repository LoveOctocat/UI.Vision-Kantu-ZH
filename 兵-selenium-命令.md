# 兵部

![兵部](https://github.com/T-Barry-Lu/UI.Vision-Kantu-ZH/blob/master/pictures/%E5%85%B5.png)

## 命令：answerOnNextPrompt (text)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/answeronnextprompt)

该命令用于告诉「提示框」答案，而后确认。

其他：对于「确认提示框」，新版本的 Kantu 不需要点击，因为新版本的 Kantu 默认会自动点击。

| Command            | Target                                       | Pattern/Text |
| ------------------ | -------------------------------------------- | ------------ |
| open               | https://ui.vision/demo/javascript            |              |
| answerOnNextPrompt | Hello world！                                |              |
| click              | //*[@id="content"]/div[2]/div/p[2]/button[2] |              |


## 命令：assertAlert (text), assertConfirmation (text), assertPrompt (text)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/assertalert-assertconfirmation-assertprompt)

assertAlert、assertConfirmation、assertPrompt 用于检查各种 Javascript 的对话框文本是否正确。如果你只需要确认（或点击）一个对话框，这并不需要。它们只对创建 web 测试宏有用，当您需要确认对话框中的文本是否正确时。

### 关于不支持的命令的说明

在传统的 Firefox Selenium IDE 中，还存在相应的 “verify” 版本 verifyAlert，verifyConfirmation，verifyPrompt，UI.Vision RPA 并不支持这三个命令。 原因是在 Firefox IDE 中，如果出现一个对话框而您只想将其关闭，则使用 `verifyAlert` 命令即可。Chrome 的 UI.Vision RPA 默认会自动关闭对话框。 原因是，在所有自动化案例中，有 99％的用户只想关闭对话框然后继续，所以这些命令被砍掉了。

### 为什么 chooseOkOnNextConfirmation 不再需要了

在传统的 Firefox Selenium IDE 中，如果希望 IDE 自动关闭对话框，则需要添加 chooseOkOnNextConfirmation 命令。在 Selenium IDE 的 UI.Vision RPA 实现中，不需要此命令，因为 UI.Vision RPA 会在出现的对话框中自动关闭（点击 OK）。因此换句话说，ChooseOkOnNextConfirmation 是内置的，不需要作为单独的命令。出现这种情况的原因是，在所有自动化案例中，有 99％的用户只想关闭对话框然后继续。相反的命令 selectCancelOnNextConfirmation （取消按钮目前不可用）在 UI.Vision RPA 中尚不可用，因为它似乎很少使用。

「提示对话框」的输入文本可以用 `answerOnNextPrompt` 命令去定义。

### 例子

下面的 Macro 首先打开一个「提示对话框」，然后 UI.Vision RPA 自动关闭它。assertPrompt命令是完全可选的，仅当您希望 assert 对话框确实出现且标题正确时才需要它。

| Command            | Target                                       | Pattern/Text |
| :----------------- | :------------------------------------------- | :----------- |
| open               | https://ui.vision/demo/javascript            |              |
| answerOnNextPrompt | Hello World!                                 | -            |
| click              | //*[@id="content"]/div[2]/div/p[2]/button[2] | -            |
| assertPrompt       | Enter some text!                             | -            |


## 命令：assertChecked (target), verifyChecked (target)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/assertchecked-verifychecked)

`assertChecked` 和 `verifyChecked` 命令用于检查「复选框」和「单项框」的情况。如果「复选框」被选中，命令会成功运行，否则在日志中返回错误：`[error] false`。

您可以使用内部变量 `!LastCommandOK` 确认结果，或者使用 `if/gotoif` 验证命令。

`assert` 和 `verify` 命令都很有用。

- `verify` 命令如果没有匹配到相应条件的话，它只会在日志中返回错误信息，但是 Macro 依旧继续运行。
- `assert` 命令，如果没有匹配到相应条件的话，它将使 Macro 停止运行。

### assertNOTChecked & verifyNOTChecked

这两个命令的工作方式相同，但结果是相反的。如果复选框被选中，它们会返回记错误。

与此命令密切相关的是 `storecheck`。

### 例子

这个 Macro 检查网站的两个复选框的状态。如果没有选中 is18，执行将停止。

| Command       | Target             | Pattern/Text |
| :------------ | :----------------- | :----------- |
| open          | https://ui.vision/ |              |
| verifyChecked | id=firsttimeuser   | is18         |
| assertChecked | id=over18          | is18         |

这些命令有时也用空格拼写:assert Checked、assert Not Checked、verify Checked和verify Not Checked。

## 命令：assertEditable (locator), assertNOTEditable (text)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/asserteditable)

`assertEditable` 用于确认目标元素是可编辑的。如果不可编辑，Macro 则停止运行。

`assertNOTEditable` 与 `assertEditable` 的工作原理相同，但是结果是相反的。因此，当字段不可编辑时，Macro 将停止。

`verifyEditable` 和 `verifyNOTEditable` 都是可用的。verify 和 assert 的区别是：

- `verify` 命令如果没有匹配到相应条件的话，它只会在日志中返回错误信息，但是 Macro 依旧继续运行。
- `assert` 命令，如果没有匹配到相应条件的话，它将使 Macro 停止运行。

### 例子

Available soon

## 命令：assertElementPresent (target, pattern) , verifyElementPresent (locator, text)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/assertelementpresent-verifyelementpresent)

`assertElementPresent` 和 `verifyElementPresent` 用于检查定位器的元素是否存在。

assertElementPresent 在技术上类似于单击命令（click 命令），不过它只是检查元素是否存在。它会根据 `!timeout_wait` 上的时间等待，直到元素出现。

`assert` 和 `verify` 命令都很有用。

- `verify` 命令如果没有匹配到相应条件的话，它只会在日志中返回错误信息，但是 Macro 依旧继续运行。
- `assert` 命令，如果没有匹配到相应条件的话，它将使 Macro 停止运行。

### assertElementNOTPresent

`assertElementNOTPresent` 的工作方式与 `assertElementPresent` 相同，但是结果是相反的。因此当元素在页面上时，Macro 将停止。

### 例子

`gotoIf` 配合 `label`  进行循环，直到找到这个

| Command                  | Target                                                | Pattern/Text  |
| :----------------------- | :---------------------------------------------------- | :------------ |
| store                    | 2                                                     | !timeout_wait |
| open                     | https://yuilibrary.com/yui/docs/node/node-insert.html |               |
| label                    | tryagain                                              |               |
| store                    | true                                                  | !statusOK     |
| verifyElementPresent | xpath=//img[@alt='Lettuce']                       |               |
| gotoIf                   | ${!statusOK} == false                                 | tryagain      |
| echo                     | Lettuce image found!                                  | green         |


## 命令：assertText (target, pattern) , verifyText (locator, text)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/asserttext-verifytext)

`assertText` 和 `verifyText` 用于获取元素的文本（由定位符定义），并检查其是否满足 Pattern/Text 中的要求。这适用于任何包含文本的元素。

`Assert` 和 `verify` 命令都可用于验证条件是否匹配。区别在于：

- `verify` 命令将验证条件，如果不匹配，将在 log 中显示错误消息，并且 Macro 继续运行。
- `Assert` 命令如果条件不匹配，则它将停止 Macro 执行。

UI.Vision RPA Selenium IDE 还支持 `sourceSearch` 命令（不是官方的 Selenium IDE 命令），但是顾名思义，它允许您执行 `assertText`，例如直接检查 HTML 源代码而不是呈现的 DOM。 因此，您可以用于 check/verify/assert 文本。

### 例子

检查文本「Welcome」和「Free Web Automation」是否存在。如果不存在「Welcome」，Macro 将停止（因为我们使用了assert 命令）：

| Command        | Target                                  | Pattern/Text            |
| :------------- | :-------------------------------------- | :---------------------- |
| open           | https://ui.vision/                      |                         |
| ==assertText== | ==//*[@id="title"]==                    | ==Welcome==             |
| ==verifyText== | ==//*[@id="content"]/div[2]/div/h2[1]== | ==Free Web Automation== |

### 在 Selenium 中 verifyTextPresent 和 verifyText 的区别？

verifyTextPresent 命令不用于存储任何目标元素的值，但是可以用来验证指定的目标文本是否在页面的任何地方可用。UI.Vision RPA 不支持这种命令

在storeTextPresent页面上，您可以找到一个使用storeText“模拟”verifyTextPresent的示例，然后检查提取的文本是否正确。如果没有，则抛出一个错误。verifyTextPresent的模拟实际上比原始的更好:旧的verifyTextPresent检查整个页面中的文本是否存在。这经常会导致误报，通常不建议这样做。

## 命令：assertTitle (text), verifyTitle (text)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/asserttitle-verifytitle)

`assertTitle`  用于获取网页的 Title，并做检查。

- `Verify` 命令将验证条件，如果不匹配，Log 区域会给出错误消息，并且 Macro 继续运行。
- `Assert` 命令，如果条件不匹配，则停止

| Command     | Target               | Pattern/Text |
| :---------- | :------------------- | :----------- |
| open        | https://ui.vision/   |              |
| assertTitle | I am the page title! |              |

## 命令：BringBrowserToForeground

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/bringbrowsertoforeground)

BringBrowserToForeground 可以将浏览器于最顶端激活。用户便是很适合用于从「浏览器书签」中启动 Macro。

例如：假设一个 Macro 运行一个登录序列并导航到某个子页面。这样您就可以确保已经激活浏览器，您可以马上开始在这个页面上工作。

| Command                      | Target             | Pattern/Text |
| :--------------------------- | :----------------- | :----------- |
| ==BringBrowserToForeground== | -                  | -            |
| open                         | https://ui.vision/ |              |

## 命令：captureScreenshot (name of screenshot)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/capturescreenshot)

`captureEntirePageScreenshot` 用于截屏整个网页。

`captureScreenshot` 用于截取可见网站部分（viewport）。这个命令的副作用是让运行 Macro 的选项卡激活（可不后台运行）。

如果要捕获 web 元素的屏幕快照，请使用 `storeImage`。

截图保存在在「Screenshot（截图）」选项卡。您可以下载图像文件（PNG），如果需要的话。您可以使用 `LocalStorageExport` 命令自动下载。

### captureEntirePageScreenshot 例子

| Command                         | Target             | Pattern/Text |
| :------------------------------ | :----------------- | :----------- |
| open                            | https://ui.vision/ |              |
| captureEntirePageScreenshot | my screenshot name |           |

## 命令：Check (locator), UnCheck (locator)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/check-uncheck)

`Check` 选中一个切换按钮（复选框/单选）。

`UnCheck` 取消一个切换按钮（复选框/单选）。

## 命令：click (target), clickAndWait (target)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/click)

clickAndWait 和 click 发送一个 Javascript 点击事件给 DOM 元素。区别就是 clickAndWait 多一个等待的过程。

### 如何点击「变化的按钮 ID」

在一些网站上，按钮元素的 ID 在不同的页面加载之间动态变化。也就是说，每刷新一次按钮都有一个新的 ID。

**解决方法：**通常，ID 的某些部分保持不变。比如：我们要定位 post-123456 和 post-555555 。我们可以使用 XPath 的 starts-with 或者 contains 功能去搜索固定的部分。所以我们可以这样写：//*[contains(@id, 'post-')] 。可以看到 post- 部分是固定的。

**另一个方法是：**使用 visual UI teting 命令 XClick (image) 来识别元素。这就可以准确识别元素，而不用管他是什么 ID。



### FAQ：Contains Example

用户的一个问题：

我想创建一个 `Macro`，当我播放它时，它将打开《纽约时报》网页的第一个标题（该标题始终出现在左上角）。

当你录制 `Macro` 时，它会记录当时出现的文章的 URL，而第二天当我播放相同的 `Macro` 时，它却无法正常工作，因为首页上的标题已更改。

#### 解决方法是：

我们录制 Macro 的时候，我们记录的是：`//*[@id="topnews-100000005713971"]/h2/a` ，这是一个独一无二的 ID。如果你想每天点击相同的链接的话，可以修改成：`//*[contains(@id,"topnews-")]/h2/a`。

……

另一个方法就是使用 XClick。

### FAQ：如何使用 XPath 点击特殊的按钮？

解决方案：您可以使用 XPath 文本功能进行部分文本匹配：

`//*[text()[contains(.,'TEXT HERE')]]`

#### 解释：

- `:` 是一个选择器，能够匹配任何元素 —— 它返回一个节点集。如果您知道包含文本的元素，您可以使用它：`//span[contains(text(),"\*UI.Vision RPA\* IDE")]`，它会快一些，因为它搜索更少的元素。

- `Outer [ ]` 是一个条件语句，它作用于么一个节点——这里指的是文档中的每一个元素。
- `text()` 是一个选择器，它匹配上下文节点的所有子节点——它返回一个节点集（node set）。

- `Inner [ ]` 是一个条件句，作用于该节点集中的每个节点 —— 这里是每个单独的文本节点（individual text node）。
- `.` 每个单独的文本节点是方括号中任何路径的起点，也可以显式地称为 `.` 在括号内。如果它操作的任何单个节点与方括号内的条件匹配，则它将进行匹配。contains是一个操作字符串的函数。在这里，它被传递给一个单独的文本节点（`.`）

### FAQ: 如何找到带有特定文本的第 n 个链接？

这个问题与「如何使用 XPath 来寻找独一无二的按钮（Button）」问题相似。但我们是要找第 n 个，而不是匹配第一个链接。下面有好几种方式可以做到。我们先假设 Link 的文本是 `Download` 然后我们想要点击第六个链接，测试网址是：https://www.7-zip.org/download.html

- `link=Download@POS=6` - 这只能适用于链接（links）。

- `xpath=(//a[text()='Download'])[6]` - 与上述相同，但是使用的是 XPath。

- `xpath=(//*[text()[contains(.,'Download')]])[6]` - 这可以搜索任意元素的文本，不单单是链接（links）。

也可以使用 OCR 识别的方法搜索：https://ui.vision/rpa/docs/xclick#ocr

> 更新：XClick command 可以模拟用户鼠标时间，如果 Click 或者ClickAt 不适合您的话，XClick 是比基于 Javascript 点击命令更加有用的 “click“ 命令。

重点说明：对于桌面自动化，必须使用 XClick。Click 和 ClickAt 命令始终只能在网页中启作用。

| Command      | Target                   | Pattern/Text |
| :----------- | :----------------------- | :----------- |
| open         | https://ui.vision/       |              |
| click        | link=Free Web Automation | -            |
| clickAndWait | link=Go To Next Page     | -            |


## 命令：clickAt(locator, coordString)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/clickat)

`clickAt` 有 locator 和 coordString。由于指定鼠标事件在定位符返回的元素内的 x，y 位置（如 10, 20）

`ClickAt` 在一些复杂的元素中点击更佳方便，如在画布上绘制。

默认情况 UI.Vision RPA 使用的自动录制的是 click，可以去设置中修改为 clickAt。

ClickAt 对于 Visual UI Testing 非常有用，可以和 elementFromPoint 结合使用，以视觉方式查找并单击 canvas 元素内的特定位置。

### 例子

| Command     | Target             | Pattern/Text |
| :---------- | :----------------- | :----------- |
| open        | https://ui.vision/ |              |
|   clickAt   | css=....           | 10,20        |

## 命令：csvRead (file name)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/csvread)

csvRead 用于读取 CSV 文件 📃，Macro 每循环一次读取一行 CSV 文件，用内部变量 `!col1`、`!COL2`  来表示。

> 重要提示：您必须使用 LOOP 按钮启动 Macro。每个循环一次读取一行 CSV。读取的行是基于 `${!LOOP}` 变量的值。比如您运行循环 5（开始）到 10（结束），它将会从 CSV 文件读取第 5 到 10 行。另一个选择是将 CSVRead 命令嵌入带有内部变量 `!csvReadStatus` 和 `!csvReadLineNumber` 的 `while` 循环中，如 DemoCsvReadWithWhile Demo Mcaro 所示。

使用 CSV Tab 可将 CSV 文件导入或者导出（保存）。需要先导入 CSV 文件，因为无法直接从硬盘驱动器读取浏览器扩展。但是使用我们的 XModule，kantu 可以直接读取 CSV，请参见下一段：

### Reading CSV files directly from the hard drive

如果您安装了 UI.Vision RPA FileAccess XModule，则可以将 Macro 存储模式切换为硬盘存储。这还将直接将所有 CSV 读取和写入操作重定向到硬盘驱动器。默认情况下，CSV 文件随后存储在 kantu/datasources 文件夹中。

### FAQ: How can I use commas inside the CSV file text (not as a separator)?

用户问题：*UI.Vision RPA* 使用逗号作为分隔符，但有时我需要在文本中使用逗号（而不用作分隔符）；我怎样才能做到这一点？

请将该字段用「引号」引起来，比如：`field1,field2,"fi,e,ld3",field4` ，如果要在字段中包含 `"` 变成这样 `""` ，所以整个字段将是这样的：`""""` 。

### csvRead Example

从 user.csv 中读取数据，然后使用 `${COL1}` 和 `${COL2}` 内部变量将数据填充到表单中。 CSV 文件必须在 CSV Tab 中加载进来才可以。

| Command | Target             | Pattern/Text |
| :------ | :----------------- | :----------- |
| open    | https://ui.vision/ |              |
| csvRead | user.csv           |              |
| type    | id=firstname       | ${!COL1}     |
| type    | id=lastname        | ${!COL2}     |

### !csvReadMaxRow - 读取 CSV 文件的最后一行

在某些情况下，您可能需要了解 CSV 文件中有多少行，或者希望读取 CSV 文件的最后一行（如：最近添加的）.

在这两种情况下，内部变量 `!csvReadMaxRow` 可以提供帮助。在第一个 `csvRead` 之后，将设置 CSV 中的行数。在下面的例子中，我们使用它来从一个名为 user.csv 的 CSV 文件中读取最后一行。为此，我们将 `!csvReadLineNumber` 设置为 `csvReadMaxRow`，然后再次运行 `csvRead`。

| Command | Target            | Pattern/Text       |
| :------ | :---------------- | :----------------- |
| csvRead | user.csv          |                    |
| store   | ${!csvReadMaxRow} | !csvReadLineNumber |
| csvRead | user.csv          |                    |
| type    | id=firstname      | ${!COL1}           |

## 命令：csvSave (file name)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/csvsave)

`csvSave` 的目的是将 `!csvLine` 的值存储到 CSV 文件中。该文件存储在浏览器本地存储中。您可以在 CSV Tab 上查看、导出和删除它。如果您再次调用 csvSave（或第二次运行 Macro），则数据将附加到 CSV 文件之后。

请注意，将数据赋值给 `!csvLine` ，是分别存储了每个值。因为一旦调用了 `csvSave`，保存在 `!csvLine` 内部数组中的每个值都将在保存之前自动用 “…” 包装，（[见论坛](https://forum.ui.vision/t/why-store-csvline-inserts-double-quotes-no-matter-what/574/4)）

重要提示：`csvSave` 和 `csvRead` 在不同的 CSV 文件上运行。 您可以同时在 Mcaro 中使用两者，但是任何与 `!csvLine` 相加的值都只会修改用于 csvSave 文件。 使用 csvRead 加载的数据是只读的，只能通过只读 `${!COLx}` 变量进行访问。 但是您可以轻松地 “re-use” 一些已加载的数据作为输出日志文件，只需使用 `store | ${COl1} | !csvLine` 即可。 在此示例中，我们将输入 CSV 文件中第一列的值添加到 `!csvLine` 变量中。

使用 CSV Manager Tab 在 UI.Vision RPA 中导入和导出 CSV 文件。在 Macro 中，可以使用 `localStorageExport`命令从 CSV 选项卡导出到硬盘。

如果您安装了 Vision RPA FileAccess XModule，您可以将存储模式切换为「硬盘存储」。这也将重定向所有 CSV 读写操作直接到硬盘驱动器。默认情况下，CSV 文件存储在“kantu/datasources”文件夹中。

### csvSave Example

从网站中提取了两个值，并将它们存储在一个名为 exchangerate.csv 的文件中。

| Command   | Target             | Pattern/Text |
| :-------- | :----------------- | :----------- |
| open      | https://ui.vision/ |              |
| storeText | id=USD             | !csvLine     |
| storeText | id=EURO            | !csvLine     |
| csvSave   | exchangerate.csv   |              |

## 命令：deleteAllVisibleCookies (current domain)

`deleteAllCookies` 清除所有 cookies。与 `selectWindows TAB=CLOSEALLOTHER`（关闭所有打开的选项卡）配合使用，是一个在测试开始时很有用的 clean up 命令。

另一个选项：UI.Vision RPA 支持在 Chrome 隐身模式下运行。「隐身模式」要比 `deleteAllVisibleCookies` 更加有效，因为它还能确保浏览器缓存是空的。只要勾选“允许隐身”。

### 例子

| Command          | Target | Pattern/Text |
| :--------------- | :----- | :----------- |
| deleteAllCookies |        |              |

## 命令：dragAndDropToObject (drop from, drop to)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/draganddroptoobject)

dragAndDropToObject：提供「需要拖动对象的元素定位器」和「拖动目标位置的元素定位器」。不要把 dragAndDrop 这个命令搞错了（该命令不支持）。

dragAndDropToObject 命令在 https://html5demos.com/drag/ 网站中运行良好，但是在 https://jqueryui.com/draggable/ 并不适用。因为它没有目标元素，它依赖于坐标 x，y

### dragAndDropToObject Example

| Command             | Target                       | Pattern/Text |
| :------------------ | :--------------------------- | :----------- |
| open                | https://html5demos.com/drag/ |              |
| dragAndDropToObject | id=one                       | id=bin       |
| dragAndDropToObject | id=two                       | id=bin       |


## 命令：echo (text, color)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/echo)

echo 命令用于在任何 Selenium IDE 软件测试工具的日志区域中显示文本或显示变量的存储值。它通常用于调试，且不会以任何方式影响 Macro 的执行。

### Make automation more colorful

| **Color Name** |
| -------------- |
| white          |
| gray           |
| silver         |
| black          |
| maroon         |
| red            |
| purple         |
| fuchsia        |
| green          |
| lime           |
| olive          |
| yellow         |
| navy           |
| blue           |
| teal           |
| aqua           |
| orange         |

使用  \#shownotification 作为 color 数值，可以开启「通知消息」。

### 例子

| Command  | Target                              | Pattern/Text      |
| :------- | :---------------------------------- | :---------------- |
| open     | https://ui.vision/                  |                   |
| store    | Boston                              | city              |
| echo   | The city variable contains ${city}. | green             |
| echo   | macro done!                         | #shownotification |

## 命令：editContent (target, text in HTML format)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/editcontent)

`editContent` 命令支持编辑「可编辑内容的元素」，如「富文本编辑器」。如果用户使用「自动的 recording（录制）」编辑 content-editable 元素的内容，Kantu 将自动生成相应的 editContent 命令（该命令通过检测元素的焦点移除来触发）这个命令的想法是由来自台湾的 Sideex 团队的，Kantu IDE 现在也很好地支持它。

对于常规输入框，众所周知的 type 命令用于表单填充 editContent，它用于富文本编辑控件（如 TinyMCE、QuillJS 或 RichTextEditor）的命令。

### 例子

注：editContent 支持 HTML 标记，在本例中使用 H1。

| Command     | Target                                  | Pattern/Text                                                 |
| :---------- | :-------------------------------------- | :----------------------------------------------------------- |
| open        | https://quilljs.com/                    |                                                              |
| editContent | //*[@id="snow-container"]/div[2]/div[1] | &lt;h1&gt;&lt;em&gt;UI.Vision RPA&lt;/em&gt; Test Automation&lt;/h1&gt; |

## 命令：mouseOver (target)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/mouseover)

可以使用 `mouseOver` 命令，对目标「页面元素」，鼠标悬停或者滑出进行影像。目标元素可以是按钮、图像、链接或任何其他元素。目标元素可以是按钮（buttom）、图像（image）、链接（link）或其他元素。

注：Selenium IDE 不支持 mouseOverAndWait 和 mouseOutAndWait 命令。

### mouseOver Example

| Command   | Target                   | Pattern/Text |
| :-------- | :----------------------- | :----------- |
| open      | https://ui.vision/       |              |
| mouseOver | link=Free Web Automation | -            |

## 命令：Open (URL)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/open)

最常用的命令，open 命令用于打开 URL。

To do so, the *UI.Vision RPA* IDE separates the URL of the open command into base url and relative path upon export.

UI.Vision RPA Selenium IDE 不支持 `openWindow` 命令 . 您可以使用更加令话的：`selectWindow | TAB=OPEN | https://newurl.com`命令来达到相同的目的。

注意：如果 Open 参数不是以 `http://` 或 `https://` (如 `OPEN | /contact`) 开头的，UI.Vision RPA 会默认假设这个是相对路径，是要附加的现有 URL 后面的。

### 例子

在这个例子中，https://ui.vision/ 是一个 base url，而 docs/selenium-ide 是一个相对路径。

| Command | Target                              | Pattern/Text |
| :------ | :---------------------------------- | :----------- |
| open    | https://ui.vision/docs/selenium-ide |              |
| echo    | This was all...                     | -            |

## 命令：pause (time in milliseconds)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/pause)

`pause` 命令是一个等待命令，用于在指定的时间内延迟自动测试的执行。等待时间的单位是「毫秒」，3 秒就是 3000.

特殊用法：如果您使用 `pause | 0` 或只是 `pause` 没有任何数字，那么执行将暂停，直到用户单击 RESUME 按钮。
![Pause 0 waits until RESUME is clicked](https://ui.vision/Content/Images/pause0.png)

### Pause Example

停止 5000ms

| Command | Target             | Pattern/Text |
| :------ | :----------------- | :----------- |
| open    | https://ui.vision/ |              |
| pause   | 5000               |              |
| open    | https://ocr.space/ |              |

## 命令：Refresh ()

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/refresh)

重新加载当前的页面。

| Command | Target            | Pattern/Text |
| :------ | :---------------- | :----------- |
| open    | https://ui.vision |              |
| Refresh |                   |              |


## 命令：run (macro name)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/run)

通过使用 run(Macro)命令，您可以在一个 Macro 中调用另一个宏。 例如：允许您在多个其他 Macro 中重复使用 “登录 Macro” 作为构建块。

### 主 Macro 和子 Macro 之间的关系

- 「主 Macro 中的变量」在「子 Macro」中可见（不要将此与「全局变量」混淆了，全局变量是所有 Macro 之间也可见的）
- 如果在「子 Macro」中更改了变量的值，则它也将更改「主 Macro」中的值（按引用调用)
- 对于内部变量，适用与变量相同的规则。 但是有一个例外：`!macroname` 始终是「主 Macro」的名称
- `!runtime` 是整体运行时间（主 Macro 和子 Macro 运行时间总和）
- `VisionLimitSearchArea` 命令的限制区域与内部变量一样

### RUN 命令的使用

- `RUN | /reuse/logins/gmail/user1` => 是绝对路径
- `RUN | gmail/user1` (开头没有 `/`) => 当前文件夹的相对路径

总结：绝对路径开头有 `/` 而相对路径没有

### 例子

| Command | Target                | Pattern/Text |
| :------ | :-------------------- | :----------- |
| open    | https://ui.vision/    |              |
| run     | /reuse/login_macro    |              |
| echo    | Now we are logged in! |              |
| run     | /reuse/logout_macro   |              |

## 命令：select (target, pattern), selectAndWait (target, pattern)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/select)

`select` 和 `selectAndWait` 的目的是从下拉 / 组合框或列表框中选择一个值。

![image-20200116125446616](/Users/awake/Library/Application%20Support/typora-user-images/image-20200116125446616.png)

如果从下拉菜单中选择标签时页面正在重新加载，则需要使用 `selectAndWait` 命令。 它将选择指定的标签，然后等待页面成功加载。

### 例子

| Command | Target                | Pattern/Text            |
| :------ | :-------------------- | :---------------------- |
| open    | https://ocr.space/    |                         |
| select  | id=ocrLanguage        | label=ChineseSimplified |
| click   | id=SearchableAndLayer |                         |

## 命令：selectFrame (frame identifier)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/selectframe)

当页面包含 iframe 时，您需要使用 `selectFrame` 命令。您需要在 Target 中提供 iframe 元素的名称（name）或 id 属性。同样的命令也适用于 frame，方法完全相同。

SelectFrame values:

- `relative=top` - 回到顶部的 frame（所有 frames 以外）
- `index=0,1,2,3,..`. - 回到第 n-th 个 frame

注意：不要将 selectFrame 与用于选择浏览器选项卡的 selectWindow 混淆了。

### selectFrame Example

第一句的 `relative=top` 不是必要的（因为我们一般默认是在 Top frame 中的），如果已经进入其他 Frame 并想要离开，这就需要使用 `relative=top`。

| Command     | Target                                      | Pattern/Text |
| :---------- | :------------------------------------------ | :----------- |
| open        | https://ui.vision/demo/iframes              |              |
| selectFrame | relative=top                                |              |
| selectFrame | index=0                                     |              |
| click       | css=button.ytp-large-play-button.ytp-button |              |


## 命令：selectWindow (window identifier)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/selectwindow)

`The selectWindow | tab=x and selectWindow | title=y` 命令用于浏览器选项卡切换。 您可以将其与 `title=(title of tab to be selected)` 一起使用，或者使用更方便的 `tab= with number of the tab (比如 0,1,2,...)`。

- `Tab=0` 是主窗口（是 Macro 运行时激活的 Tab，可以称为 start tab）
- `tab=1` 是右侧的第一个 Tab
- `tab=2` 是第二个
- 依此类推
- `tab=-1` 是左侧第一个 Tab（如果左侧有 Tab 的话）
- `tab=-2` 是左侧第二个 Tab

> 这也表明 `selectWINDOW` 的命令名有些过时，它是 Internet Explorer 仍然统治网络时创造的。 如今 `selectTab` 将是更合适的术语（我们继续使用旧术语来实现向后兼容性）。

`selectWindow | TAB=OPEN | https://newwebsiteURL.com` 指定 URL，开启新 Tab

`selectWindow | TAB=CLOSE` 关闭当前 Tab。

- 如果在关闭的 Tab 右边有一个 Tab 的话，UI.Vision PRA 就会把这个 Tab 当作当前激活 Tab
- 如果右边没有的话，左边的 Tab 将成为激活的 Tab
- 如果没有其他 Tab 的话，`TAB=CLOSE` 会关闭浏览器

`selectWindow | TAB=CLOSEALLOTHER` 关闭除了当前 Tab 以外其他所有 Tab。与 `deleteAllCookies` 一起使用，是在测试开始时 “清理” 的有用命

### 例子

| Command          | Target                           | Pattern/Text                          |
| :--------------- | :------------------------------- | :------------------------------------ |
| open             | https://ui.vision/               |                                       |
| click            | link=Open one new browser window |                                       |
| ==selectWindow== | tab=1                            |                                       |
| click            | link=One more tab                |                                       |
| ==selectWindow== | tab=2                            |                                       |
| verifyText       | link=Free Web Automation         | Free Web Automation                   |
| selectWindow     | tab=0                            | (this switches back to the first tab) |
| selectWindow     | tab=open                         | https://ocr.space                     |

## 命令：sendkeys (target, text) and type (target, text)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/sendkeys-type)

`sendkeys` 命令就和 `type` 命令差不多，但是有两个功能 `type` 命令的无法完成。`sendkeys` 命令在自动完成「文本框（text boxes）」或者「组合框（combo boxes）」非常有用。

1. `sendKeys` 命令无法替换文本框中的现有文本内容，而 type 命令能够替换文本框中的现有文本内容。
2. `sendKeys` 命令就如同用户按在键盘上一样，这意味着它的工作原理和用户用键盘输入单词的原理是一样的。因为所有 Selenium IDE 命令是在浏览器的 DOM 中的 Javascript 层级运行的。如果 sendKeys 命令无法使用请使用 XType。

注意：Focus 命令不在支持，Kantu 自动会设置为焦点。请注意，你必须将你的运行窗口放在前台，这样才能使焦点工作。这是 focus 运作原理，您可以使用 BringBrowserToForeground 命令让 Tab 保持在前台

`Sendkey` 支持的特殊按键，就像这样使用：`${KEY_ENTER}`

- KEY_LEFT (Navigation Left)
- KEY_UP (Navigation Up)
- KEY_RIGHT (Navigation Right)
- KEY_DOWN (Navigation Down)
- KEY_PGUP / KEY_PAGE_UP (Page up)
- KEY_PGDN / KEY_PAGE_DOWN (Page down)
- KEY_BKSP / KEY_BACKSPACE (Backspace)
- KEY_DEL / KEY_DELETE (Delete)
- KEY_ENTER (Enter)
- KEY_TAB (Tab)

sendKeys 和 type 命令只可以在网页中运行，桌面自动化必须使用 `XType`。

### type 和 sendKeys 命令的区别

该例子运行在 Google 搜索页面，使用 Type 在输入框输入关键词，然后使用 sendkeys 命令键入「回车」进行搜索。如果您在输入框使用 Type 命令键入 `${KEY_ENTER}`，它只会输入这几个字符，而不会执行回车搜索操作。

| Command  | Target                   | Pattern/Text               |
| :------- | :----------------------- | :------------------------- |
| open     | https://google.com/      |                            |
| Type     | id=lst-ib                | Solar Cells Web Automation |
| sendkeys | link=Free Web Automation | ${KEY_ENTER}               |

## 命令：Search and extract page source code

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/sourceextract-sourcesearch)

`sourceSearch` 和 `sourceExtract` 命令是用于查看页面源代码的，而不是查看文档对象模型（DOM）。 因此 `sourceSearch` / `sourceExtract` 可以用于验证（verify）。

比如：可以检查 / 提取页面源代码中的注释。可以查看 `storeText` 命令不可见的 Javascript 代码部分（例如：Google Analytics ID）。

- 这两个命令都可以在纯文本模式（plain text mode）下使用。 `*` 通配符表示变化的部分。
- 对于专家来说，这两个命令都支持标准的正则表达式（通常称为 regex 或 regexp）
- 使用 `sourceExtract`，如果找不到匹配项，则将变量设置为 `#nomatchfound`（不会触发错误）

### 例子

下面 👇 这几个文字，例子中的代码将对文字进行操作。

- Coffee $2.95
- Tea $1.95
- Milk $2.10

Another test string: width: 11, width: 22, width: 33

| Command       | Target                              | Result (stored in the variable)                              |
| :------------ | :---------------------------------- | :----------------------------------------------------------- |
| sourceSearch  | $*</li>                             | 3 (= 3 matches found)                                        |
| sourceSearch  | regex=[\$\£\€](\d+(?:\.\d{1,2})?)   | 3 (= 3 matches found, same as before, but now with regular expressions) |
| sourceSearch  | Tea $*</li>                         | 1 (= 1 match found)                                          |
| sourceSearch  | Beer $*</li>                        | 0 (no match found)                                           |
| sourceExtract | $*</li>                             | $2.95</li> (the coffee, without @ the first match (@1) is assumed) |
| sourceExtract | $*</li>@2                           | $1.95</li> (the tea)                                         |
| sourceExtract | $*</li>@5                           | #nomatchfound                                                |
| sourceExtract | regex=[\$\£\€](\d+(?:\.\d{1,2})?)@2 | 1.95 (the tea)                                               |
| sourceExtract | regex=width: (\d+)@2                | width: 22                                                    |
| sourceExtract | regex=width: (\d+)@2,1              | 22 (the 2,1 means the first group of the second match)       |

## 命令：store (value, variable)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/store)

Selenium 函数中的 `store`，`storeValue` 和 `storeText` 存储一些数据以供以后访问。

- 变量格式：`${varaiable_name}`
- 要显示存储变量：请使用 `echo`

UI.Vision RPA IDE 包含有用的「内部变量」，这些变量控制运行并提供状态信息。 可以从您的 Macro 中访问它们。 一些是只读的（例如 `!URL`），其他的比如 `!TIMEOUT_WAIT` 是可以进行设置。内部变量始终以 `!` 开头，因此您自己的变量不得以 `!` 开头。

### 例子

当您将某些内容存储在 var 中时，不需要使用 `${...}`。但是，当您需要 var 的值时，可以通过 `${...}` 来访问它。

| Command   | Target             | Pattern/Text |
| :-------- | :----------------- | :----------- |
| open      | https://ui.vision/ |              |
| ==store== | 12345              | myvar        |
| echo      | ${myvar}           |              |
| type      | id=phone           | ${myvar}     |

## 命令：storeAttribute (locator@attribute, variable)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/storeattribute)

> 类似于抓取代码行中的内容

`storeAttribute` 将指定元素的属性值存储到给定变量中。 您可以使用 `storeAttribute` 命令存储任何属性的值。

### 用法

输入元素的定位符（后跟 `@` 符号），然后是 Selenium IDE 的目标列中的属性名称。

例如：`css=img.sensitive-img@href` ，`css=img.responsive-img` 是元素的定位符，`href` 是我们要存储的属性名（attribute name）。

`storeAttribute` 不适用于输入框（input boxes）。但是可以使用：

```
storeEval | window.document.getElementsByName('Phone')[0].value; | value
```

作为替代。这与旧版本 IDE 中的 storeValue 相同。

V5.3.3 版本：如果 locator 无法找到，是不会报错。`#LNF` 将会保存在 Variable。LNF → Locator not found。

- 论坛相关的链接，how-to-copy-and-paste-mp3-hyperlink：https://forum.ui.vision/t/how-to-copy-and-paste-mp3-hyperlink/1763/
- 爬虫相关命令的网站地址：https://ui.vision/rpa/docs/selenium-ide/web-scraping

### storeAttribute Example

该例子从图像中提取链接和 ALT 文本：

| Command        | Target                                                       | Pattern/Text |
| :------------- | :----------------------------------------------------------- | :----------- |
| open           | https:/ui.vision/demo/storeeval                              |              |
| storeAttribute | css=img.responsive-img@href                                  | mylink       |
| storeAttribute | css=img.responsive-img@alt                                   | myalttext    |
| echo           | `The image links to ${mylink} and its ALT text is ${myalttext}` |              |

## 命令：storeChecked (target, variable)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/storechecked)

`storeChecked` 命令将标识复选框或单选按钮的状态，并将值 true 或 false 存储在变量中。如果选中元素，它将在变量中存储  `true`，如果未选中或未选中元素，则将存储  `false`。

与该命令密切相关的是 `AssertChecked` 和 `VerifyChecked` 这两个命令。

### 例子

| Command      | Target                     | Pattern/Text |
| :----------- | :------------------------- | :----------- |
| open         | https://ui.vision/         |              |
| storeChecked | id=over18                  | is18         |
| echo         | User is over 18 is ${is18} |              |

## 命令：storeText (target, pattern)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/storetext)

`storeText` 命令将页面元素的文本值存储到变量中以供将来使用。 因此，它是从 HTML 文本和表格中进行网络抓取信息的推荐命令。

V5.3.3：如果找不到定位器，则不会触发任何错误。 而是将文本 `#LNF`（Locator not found）存储在变量中

请注意，对于输入框（input boxes）、请选择框（select boxes）、复选框（checkboxes）、单选按钮（radiobuttons）或文本区域（textareas），因为这些文本在技术上是字段值（field value）。 因此，`storeText` 在设计上不适用于这些元素，如果用 storeText 抓取的话，将会返回 `""`。 可以使用 `storeValue` 从输入元素中提取文本。

如果您需要从 HTML 源代码中提取文本，请直接使用 `sourceExtract`。

### 例子

| Command   | Target                              | Pattern/Text |
| :-------- | :---------------------------------- | :----------- |
| open      | https://ui.vision/                  |              |
| storeText | //*[@id="content"]/div[2]/div/h2[1] | name         |
| echo      | Name var = ${name}                  |              |

## 命令：storeTitle (target, pattern)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/storetitle)

`storeTitle` 命令用于存储当前网页的 Title 到一个变量中。

Firefox（浏览器）有一个命令是 storeLocation，可以用于保存当前网页的 URL。在 UI.Vision 中可以用这个语句达到相同的作用：`store | ${!URL} | myurl`，或者直接使用内部变量 `!URL`。 

### 例子

| Command    | Target                       | Pattern/Text |
| :--------- | :--------------------------- | :----------- |
| open       | https://ui.vision/           |              |
| storeTitle |                              | mytitle      |
| echo       | The page title is ${mytitle} |              |

## 命令：storeValue (target, pattern)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/storevalue)

`storeValue` 命令用于将元素的值赋值给变量。 网站的输入框（input boxes）可以使用 `storeValue` 命令从中获取文本。 换句话说，`storeValue` 可以用于「输入框（input boxes）」、「选择框（select boxes）」或「文本区域（textareas）」信息的抓取。

V5.3.3 版本更新：如果找不到定位器，不会触发错误。 而是将文本 `#LNF` 存储在变量中。 `#LNF` 代表 `Locator not found` 。

重要：要从复选框（checkboxes）和单选按钮（radiobuttons）获取状态，必须使用 `storeChecked`。 要从通常的 HTML 中提取文本，请使用 `storeText`。

### 例子

| Command    | Target                                         | Pattern/Text |
| :--------- | :--------------------------------------------- | :----------- |
| open       | https://ui.vision/docs/selenium-ide/storevalue |              |
| storeValue | id=Readonlytask_Description                    | mytext       |
| echo       | Extracted Text = ${mytext}                     |              |

## 命令：ThrowError

| **Command** | **Target**         | **Comment**                                                  |
| ----------- | ------------------ | ------------------------------------------------------------ |
| ThrowError  | Your error message | This command triggers an error. It stops the macro execution and displays "your error message" in the log file. Together with if/endif it allows you to create your own error conditions. |

## 命令：WaitForPageToLoad (max. time to wait in milliseconds)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/waitforpagetoload)

`WaitForPageToLoad` 用于告诉 IDE 页面的加载时间，通常不是所有情况都要使用 `...andWait` 命令的。

比如：`ClickandWait`，你只需要用在一些特殊的情况即可，比如当一个网站触发多个页面加载事件。

### 例子

| Command           | Target                   | Pattern/Text        |
| :---------------- | :----------------------- | :------------------ |
| open              | https://ui.vision/       |                     |
| assertText        | link=Free Web Automation | Free Web Automation |
| WaitForPageToLoad | 3000                     |                     |

## 命令：waitForVisible (locator)

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/waitforvisible)

`waitForVisible` 用于告诉 IDE 等待元素可见的时间。如果使用了这个命令，它会等待到元素出现。一旦该元素出现了，Macro 会继续运行。

### 例子

| Command        | Target                                | Pattern/Text |
| :------------- | :------------------------------------ | :----------- |
| open           | https://ui.vision/demo/waitforvisible |              |
| waitForVisible | css=#div1 > h1                        |              |
| echo           | The text is now visible               |              |



### waitForNotVisible 例子（不支持）

[该命令英文链接](https://ui.vision/rpa/docs/selenium-ide/waitforvisible)

等到元素不可见为止，这是很少使用的命令，可以很容易地用现有的命令进行模拟，所以不支持。

您可以使用 `while / endWhile` 循环来模拟。循环通过内部变量 `!statusOK` 和 WaitForVisible 一起使用。如果元素可见，`!statusOK` 的值则为 true，循环仍然继续。不过一旦元素消失 `!statusOK` 为 FALSE，循环结束，Macro 继续运行。

你需要把 `!errorIgnore = TRUE`，这样如果元素消失了，Macro 不会报错。

| Command        | Target                                                       | Pattern/Text |
| :------------- | :----------------------------------------------------------- | :----------- |
| open           | https://www.w3schools.com/howto/howto_js_toggle_hide_show.asp |              |
| store          | true                                                         | !errorignore |
| while          | ${!statusOK}                                                 |              |
| waitForVisible | id=myDIV                                                     |              |
| endWhile       |                                                              |              |
| echo           | The text is now hidden!                                      |              |
| store          | false                                                        | !errorignore |
