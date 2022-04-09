# LaTeX使用指南


# 前言

最近在尝试入坑 LaTeX，然后发现网上的教程大多停留在18年以前，甚至有14年的，对现在的最新版软件非常的不适用，尤其是 vscode 的部分，故整理此文，适用于2022年4月的最新软件。

## 什么是LaTeX？

LaTeX 是一种基于 ΤeΧ 的排版系统，由美国计算机学家莱斯利·兰伯特（Leslie Lamport）在20世纪80年代初期开发，利用这种排版系统，即使使用者没有排版和程序设计的知识也可以充分发挥由 TeX 所提供的强大功能，这是一种用于高质量排版的文档准备系统。常用于大中型技术或科学文档，但它几乎可以用于任何形式的出版。

如果你使用过 Markdown，你应该知道 Markdown 可以让写作者更专注于写作，而不是文字的排版上。LaTeX 和它相似，它使用精准的语法让文档的格式统一而高效，尤其是生成复杂表格与数学公式。但在轻格式写作这一领域，最近被 Markdown 抢去半壁江山（因为 Markdown 的入门更简单），如果你只是厌倦了 Microsoft Word 重复性的更改字体、字号、格式这些工作，想要专注于写作，那建议你去用 Markdown，此外  本网站所有文档都是用 Markdown 写的。

注：LaTeX 发音为 «Lah-tech» 或 «Lay-tech»（与 «blech» 或 «Bertolt Brecht» 押韵，不要像我一样一直把 "X" 的读音读出来丢人）

## 我是否需要使用 LaTeX ？

### 如果你符合以下条件，建议你花一些时间学习并使用 LaTeX ：

- 我需要写书或者写毕业论文这种巨型文档，涉及大量的图片、公式与文献引用
- 我需要写计算机领域的论文
- 我已经，并且长期身处学术界
- 我对 Microsoft Word 莫名其妙的排版崩坏、程序崩溃与内容丢失感到厌倦
- 我认为 Microsoft Word 对图片与公式的支持无法满足我的需求
- 我需要与别人协同完成文档，我希望有版本控制并且在最后合并工作时省心高效
- 我需要在在 Linux 和 Mac 下写文章


### 如果你符合以下条件，建议你不要浪费时间学习 LaTeX ：

- 我只是想编辑一些简单的文档，尽管需要图文并茂并且有格式要求，但很少超过五千字
- 我仅进行写作工作，或者进行一些简单的文字记录，对于格式完全不在意
- 我无法接受 “非所见即所得”，即我必须立即马上立刻看到我的编辑后的最终效果
- 我对于计算机一窍不通或者自己的电脑上安装了三个及其以上的 “杀毒软件”

## 如何安装 LaTeX 编译环境

看到这里说明你已经决定入坑 LaTeX 了，首先要告诉你一个好消息和一个坏消息，

坏消息是，如果你并没有计算机的背景知识，那你必须要经历一段繁琐且晦涩难懂的配置过程，你将接触一种你从未接触过的文档生成方式——编写源码并用编译器编译生成文档。

好消息是，配置过程你只需要进行一次，一劳永逸，并且完全不懂每一步在干什么也没关系，只需要照做即可。

## 安装 TeX Live

之后的所有教程都默认你是一个 Windows 用户，Mac 用户建议另寻网络上其他的详细教程。Linux 用户默认不用教。

TeX Live 是一个全面的 TeX 系统，它包括所有主要的 TeX 相关程序、宏包和免费软件字体。宏包是TeX系统的一个重要概念，不同的宏包提供了对不同文档格式或者功能的支持，安装 TeX Live 预计会占用4~5个GB的磁盘空间。如果你嫌它太大，还可以尝试另一个主要的（免费软件）TeX 发行版 [MiKTeX](https://miktex.org/)，它会检测你用到的包，然后在使用中仅安装你需要的包，但实际上经过我的测试，即便是满足基本功能 MiKTeX 也会占用3个GB左右的空间，如果你不想为了这节省的一点点空间去承受可能的各种奇奇怪怪的问题，那建议你还是老老实实去安装 TeX Live。

### 下载并安装 TeXLive ISO 镜像

[TeXLive官网](https://www.tug.org/texlive/)上提供了多种 TeXLive 的安装方式，包括在线安装与 ISO 镜像安装。在线安装会逐个下载并安装宏包，如果你对你的网络没有信心，那我建议还是使用 ISO 镜像，镜像包含了所有所需的文件，下载镜像等同于把下载过程一次性完成。

从[这里](https://mirror.las.iastate.edu/tex-archive/systems/texlive/Images/texlive.iso)下载最新的 ISO 文件，完成下载后，双击该文件将其挂载为虚拟光驱，之后你会在电脑的资源管理器中看到该光盘，一般盘符为E，双击进入该光盘看到如下文件目录，如果无法成功挂载可以用压缩软件将其解压，解压后的文件夹等同于挂载。

![image](Pasted%20image%2020220407201358.png "挂载的虚拟光驱盘符")

双击盘符或者运行其中的`install-tl-windows.bat`打开安装程序

![image](Pasted%20image%2020220407201445.png "安装界面")
取消选择“安装TeXworkds前端”，这是一个比较老旧的Tex编辑器，有很多更好的选择，点击右下角的`Advanced`进入更详细的配置
![image](Pasted%20image%2020220407201501.png "详细配置页")

点击左下的`Customize`

![image](Pasted%20image%2020220407201535.png "左侧语言安装选项")

点前面的勾去掉你不需要的语言，节省磁盘空间占用，一般来说保留中英文即可，你要是嫌以后安装麻烦就不取消选择。完成后点确定，然后点开始安装，等待安装完成，耗时30分钟到两个小时左右。

### 升级各个包到最新

在开始菜单栏中找到 TeX Live 2022，运行其中的 TLShell TeX Live Manager，即包管理器

![image](Pasted%20image%2020220407214158.png "运行 TLShell TeX Live Manager")

打开后如图所示，注意每次打开后软件需要联网加载信息，打开后不要操作，等待加载完成，首先可以在上方菜单中的 GUI language 中更改默认语言

![image](Pasted%20image%2020220407201632.png "界面")

然后点击选项菜单，点击 `Repository` 更改源，将其更改为中国任意一个镜像源，更换后下载速度会显著提升

![image](Pasted%20image%2020220407201710.png "更换源")

等待更新完成

![image](Pasted%20image%2020220407201803.png "源更新完成后")

然后点击左侧的 `Updatable` 等待加载完成，此时会在下面显示可以更新的包，然后点右侧，更新全部。

![image](Pasted%20image%2020220407201819.png "加载可更新包")

![image](Pasted%20image%2020220407212550.png "更新完成后")

完成更新，关闭包管理器，此时 LaTeX 后端已完成配置。接下来配置 vscode 前端

# 使用vscode搭建LaTeX写作环境

## 安装 vscode

### 下载安装包

打开[官网](https://code.visualstudio.com/)

点击 Download for Windows 下载

![image](Pasted%20image%2020220407220049.png "点击下载")

### 开始安装

双击下载后的可执行文件，安装

勾选同意，然后点击下一步

![image](Pasted%20image%2020220407215812.png "同意")

选择安装位置，我这里选择的是D盘

![image](Pasted%20image%2020220407215818.png "修改安装位置")

选择后安装位置后 然后点击下一步

下一步，不创建开始菜单可以不勾选

![image](Pasted%20image%2020220407215825.png "下一步")

勾选创建快捷方式，下一步

![image](Pasted%20image%2020220407215833.png "快捷方式")

点击安装，开始安装

![image](Pasted%20image%2020220407215838.png "开始安装")

等待安装结束

![image](Pasted%20image%2020220407215843.png "安装结束" )

可勾选运行，此时点击完成后会直接运行 Visual Studio Code 代码编辑器

### 安装 LaTeX Workshop

vscode 功能强大的重要原因是拥有丰富的社区插件，其中就包括 LaTeX Workshop。

为方便使用，可先把界面改为中文，点击 vscode 左侧像俄罗斯方块一样的图标，然后在输入框中输入`chinese`，安装第一个简体中文包，然后点击重新加载软件。

![image](Pasted%20image%2020220407220529.png "安装中文")

然后界面就变成了中文。

然后安装 LaTeX Workshop，在输入框中输入LaTeX Workshop，点击安装

![image](Pasted%20image%2020220407220722.png "安装LaTeX Workshop插件")

然后你就拥有了一个 vscode 下的 LaTeX 编辑器，这个插件提供了相当丰富的功能。

### 配置 LaTeX Workshop

安装完成后，在左侧找到`TEX`图标，点击进入 LaTeX Workshop

![image](Pasted%20image%2020220407220929.png "LaTeX Workshop入口图标")

进入如下界面，左侧是功能区，右侧是编辑区

![image](Pasted%20image%2020220407221000.png "LaTeX Workshop")

在左上角依次选择 `文件-新建文件` ，点击`选择编程语言`
输入`latex`，选择为 LaTeX 文件

![image](Pasted%20image%2020220407221222.png "选择编程语言")

![image](Pasted%20image%2020220407221320.png "选择为 LaTeX 文件")

然后复制粘贴进如下内容

```latex
\documentclass[fontset=windows]{article}
\usepackage[zihao=-4]{ctex}
\usepackage[a4paper]{geometry}
\begin{document}
``Hello world!'' from balababla123测试呀！ \LaTeX.
\end{document}
```

如图所示：

![image](Pasted%20image%2020220407221656.png "测试代码")

然后进行编译测试，点击左侧的`Recipe: latexmk 🔁`，然后会发现软件左下角出现了一个 `↻`

![image](Pasted%20image%2020220407221745.png "点击进行编译")

等待其编译完成，变成 `√`，

![image](Pasted%20image%2020220407222131.png "编译完成")

然后点击右上角的绿色箭头旁边的符号，预览

![image](Pasted%20image%2020220407222123.png "编译完成")

然后你就可以看到你编译完成的第一个 LaTeX 文档了

![image](Pasted%20image%2020220407222256.png "编译成功")

至此安装配置已完成，但是这只是 LaTeX 学习的开始，语法部分自行 Google 学习。

### 其他配置

这里包含了如何最快在完成上面工作后进入产出，如果你不想学复杂的语法，或者你直接想开始写论文，就看下面的内容。

以 [武汉大学毕业论文 LaTeX 模板](https://github.com/whutug/whu-thesis)为例，进入到GitHub页面，点击[下载](https://github.com/whutug/whu-thesis/archive/refs/heads/master.zip)，然后解压压缩包。

得到模板与实例文件：

![image](Pasted%20image%2020220410020222.png "压缩包内容")

阅读模板的文档(whu-thesis-doc.pdf)

![image](Pasted%20image%2020220410020200.png "模板说明")

发现该模板仅支持仅支持 XELATEX 或 LuaLATEX 引擎，其他编译方式会直接报错

进入vscode，打开 LaTeX Workshop，在左侧的菜单的编译项中可以发现两种编译方式都支持，但是使用的是 latexmk 里的参数， LaTeX Workshop仅仅是帮你自动运行了编译命令来进行编译，调用的是你之前安装的 TeXLive 中的 latexmk 引擎。

注意到模板的文档中有使用多行`xelatex` 或`lualatex`命令来进行编译或者一行`latexmk`，这里只需要知道 latexmk 会自动帮你解决引用问题，无需重复编译，所以优先使用`latexmk`即可，这也是官方推荐的方式。

在vscode中打开 `whu-thesis-demo.tex` ，点击左侧的菜单的编译项中的`latexmk (xelatex)`，LaTeX Workshop 会自动运行下面的命令进行编译：

```shell
latexmk -xelatex 你现在的文档名
```

编译状态与预览同上

![image](Pasted%20image%2020220410021902.png "编译完成")

需要注意的一点是，LaTeX Workshop 默认会在你每次保存后启动编译，实时刷新预览视图，但是默认会运行编译项中的第一个，也就是 `latexmk 🔃`，这个编译方法由于没有使用`-xelatex`参数，所以编译这个模板的文档会失败。所以我们要进行一些设置。

按`F1`，输入`打开设置`，点击`首选项：打开设置(json)`

![image](Pasted%20image%2020220410022122.png "打开设置")

在新打开的文件中加入下列键：

```json
 "latex-workshop.view.pdf.viewer": "tab",    //设置默认pdf阅读方式为侧栏pdf阅读器
 "latex-workshop.latex.recipe.default": "lastUsed",    //设置每次编译时默认使用上一次的编译方式
 "latex-workshop.latex.autoClean.run": "onBuilt",    //设置编译进行后自动清理中间文件
 "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",    //设置双击预览pdf中的文字可以定位到源文件中的段落，方便修改
 "latex-workshop.texcount.autorun": "onSave",    //设置每次保存后统计字数，可以不加
```

如图：

![image](Pasted%20image%2020220410022648.png "添加设置项")

按下快捷键`Ctrl + s`保存设置，关闭 json 文件，你的设置 json 文件中可能与我的有出入，这是因为我还用了其他插件，只要粘贴后格式正确即可。

第一次使用了`latexmk (xelatex)`后，之后每次编译都会自动使用这个编译方式。

### 双向搜索

由于 LaTeX 是从源文件编译为 PDF 进行预览，有时候在阅读 PDF 时发现需要修改某些部分，就得去源文件中找到该段落，或者需要从源文件中找到 PDF 中的位置，都很不方便，所以需要进行双向搜索。

LaTeX Workshop 支持这一功能，如果你加入了我上面的设置项，那么你双击 PDF 中的段落（默认是`Ctrl+单击`），左侧的源文件会自动定位到这一行：

![image](Pasted%20image%2020220410023341.png "双击右侧需要修改的文字，左侧源文件自动定位")

然后左键单击左侧的源文件中的一行，按下快捷键`Ctrl + Alt + j`,右侧会定位到 PDF 中的位置，并用红点标记。

以上就是安装配置 LaTeX，并使用模板进行写作的基本内容，请从网络教程中获取更多使用方法，练习使用。

[Begin-Latex-in-minutes](https://github.com/luong-komorebi/Begin-Latex-in-minutes/blob/master/Translation-Chinese.md)

[武汉大学毕业论文 LaTeX 模板](https://github.com/whutug/whu-thesis) 模板 Demo 中有常见文章格式示例

