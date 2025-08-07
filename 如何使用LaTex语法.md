# LaTeX】新手教程：从入门到日常使用

[![Dylaaan](https://pic1.zhimg.com/v2-a311a345bd36bdec995af633beba52bc_l.jpg?source=32738c0c&needBackground=1)](https://www.zhihu.com/people/dylan-dong-233)[Dylaaan](https://www.zhihu.com/people/dylan-dong-233)[​](https://www.zhihu.com/question/48509984)[​![知乎知识会员](https://picx.zhimg.com/v2-57fe7feb4813331d5eca02ef731e12c9.jpg?source=88ceefae)](https://www.zhihu.com/kvip/purchase)

北京大学 概率论与数理统计博士在读
6072 人赞同了该文章

---

> 本份教程适合**完全没有用过LaTeX**的读者使用，学习完后**应该能写出能跑的代码**。如果之前已经使用过LaTeX的话，也可以参考本文学习，但是**在一些地方可能不是最规范的写法**。  
> 如果本份教程有没有讲清楚的地方、可以改进的地方或者错误，欢迎大家在评论区指出。  
> 另外，这篇文章也被上传到了我的个人网站：[LaTeX：从入门到日常使用](https://link.zhihu.com/?target=https%3A//dylandong.top/posts/e480/)。

## 前言：排版工具与书写工具的讨论

LaTeX是一种“非所见即所得”的排版系统，用户需要输入特定的代码，保存在后缀为.tex的文件中，通过编译得到所需的pdf文件，例如以下代码：

```tex
\documentclass{article}

\begin{document}

Hello, world!

\end{document}
```

最后输出的结果是一个pdf文件，内容是”Hello, world!“。

如何理解“非所见即所得”呢？在这里举个“所见即所得”的例子：Word。Word的界面就是一张A4纸，输入的时候是什么样子，最后呈现出来就是什么样子。这给了我们极高的**自由度**，也非常容易上手，但是有如下问题： - 对于对细节不敏感的用户，Word的排版常常会在细节存在问题，比如两段话之间行间距不同、字体不同、标题样式不同等； - 对于撰写论文的用户，Word的标题、章节、图表、参考文献等无法自动标号，也很难在正文中引用； - 对于有公式输入需求的用户，Word自带的公式不稳定，而公式插件效果常常不好。

相比之下，使用LaTeX进行排版，就像是在铺好的轨道上驾驶火车一样。使用LaTeX没有办法像Word一样非常自由，但是可以保证**规范性**，这使得LaTeX非常适合用于论文的排版。在学习的过程中，也将会感受到这一点。

无论是LaTeX还是Word，其归根结底都只是**排版工具**，用Word也可以排出LaTeX的效果，用LaTeX也可以排出Word的效果。另外，笔者最建议的**书写工具**是Markdown，其书写的过程中可以不在意排版，也支持使用LaTeX语法输入公式，与LaTeX之间的转换非常方便。

## 准备工作：安装LaTeX与配置环境

### 安装Tex Live

官方的地址是[http://mirror.ctan.org/systems/texlive/Images/](https://link.zhihu.com/?target=http%3A//mirror.ctan.org/systems/texlive/Images/)，点开之后会随机跳转到国内的镜像站。

其中的iso文件可以使用压缩软件解压，或者加载到光盘，接下来直接安装就行了。对于其他操作系统的用户（如MacOS），可以参考[TeX Live 下载及安装说明 | 始终 (liam.page)](https://link.zhihu.com/?target=https%3A//liam.page/texlive/)中的方法。

### 选择TeX编辑器

对于新手，最推荐的编辑器是[TeXworks](https://zhida.zhihu.com/search?content_id=189476676&content_type=Article&match_order=1&q=TeXworks&zhida_source=entity)，非常适合用来上手，也避免了配置环境带来的问题。如果想要提高效率的话，可以选用：

- TeXstudio，安装地址为[TeXstudio - A LaTeX editor (sourceforge.net)](https://link.zhihu.com/?target=http%3A//texstudio.sourceforge.net/)；
- 宇宙第一的Visual Studio Code，这是笔者最建议的TeX编辑器，不过需要手动配置LaTeX，较为麻烦；
- 另外，也有在线的编辑器，如[Overleaf, 在线LaTeX编辑器](https://link.zhihu.com/?target=https%3A//cn.overleaf.com/)。

### 选择pdf阅读器和编辑器

LaTeX编译的结果是pdf文件，建议选用专业的pdf阅读器或pdf编辑器。特别是在阅读beamer类型的文件时，不同的阅读器效果差别极大。在这里推荐Acrobat：

- Adobe Acrobat Reader，免费，可用于查看、签署、协作处理和批注 PDF 文件，安装地址为[Adobe Acrobat Reader (中国)](https://link.zhihu.com/?target=https%3A//www.adobe.com/cn/acrobat/pdf-reader.html)；
- Adobe Acrobat Pro，付费，可用于创建、保护、转换和编辑 PDF文件，安装地址为[Adobe Acrobat | Adobe Document Cloud](https://link.zhihu.com/?target=https%3A//www.adobe.com/cn/acrobat.html)。

## 利用LaTeX编写文档

### 文档类型

TeX有多种文档类型可选，笔者较常用的有如下几种类型：

- 对于英文，可以用`book`、`article`和`beamer`；
- 对于中文，可以用`ctexbook`、`ctexart`和`ctexbeamer`，这些类型自带了对中文的支持。

不同的文件类型，编写的过程中也会有一定的差异，如果直接修改文件类型的话，甚至会报错。以下统一选用`ctexart`。在编辑框第一行，输入如下内容来设置文件类型：

```tex
\documentclass{ctexart}
```

另外，一般也可以在`\documentclass`处设置基本参数，笔者通常设置默认字体大小为12pt，纸张大小为A4，单面打印。需要将第一行的内容替换为：

```tex
\documentclass[12pt, a4paper, oneside]{ctexart}
```

文件的正文部分需要放入document环境中，在document环境外的部分不会出现在文件中。

```tex
\documentclass[12pt, a4paper, oneside]{ctexart}

\begin{document}

这里是正文. 

\end{document}
```

### 宏包

为了完成一些功能（如定理环境），还需要在导言区，也即document环境之前加载宏包。加载宏包的代码是`\usepackage{}`。本份教程中，与数学公式与定理环境相关的宏包为`amsmath`、`amsthm`、`amssymb`，用于插入图片的宏包为`graphicx`，代码如下：

```tex
\usepackage{amsmath, amsthm, amssymb, graphicx}
```

另外，在加载宏包时还可以设置基本参数，如使用超链接宏包`hyperref`，可以设置引用的颜色为黑色等，代码如下：

```tex
\usepackage[bookmarks=true, colorlinks, citecolor=blue, linkcolor=black]{hyperref}
```

### 标题

标题可以用`\title{}`设置，作者可以用`\author`设置，日期可以用`\date{}`设置，这些都需要放在导言区。为了在文档中显示标题信息，需要使用`\maketitle`。例如：

```tex
\documentclass[12pt, a4paper, oneside]{ctexart}
\usepackage{amsmath, amsthm, amssymb, graphicx}
\usepackage[bookmarks=true, colorlinks, citecolor=blue, linkcolor=black]{hyperref}

% 导言区

\title{我的第一个\LaTeX 文档}
\author{Dylaaan}
\date{\today}

\begin{document}

\maketitle

这里是正文. 

\end{document}
```

### 正文

正文可以直接在document环境中书写，没有必要加入空格来缩进，因为文档默认会进行首行缩进。相邻的两行在编译时仍然会视为同一段。在LaTeX中，另起一段的方式是使用一行相隔，例如：

```tex
我是第一段. 

我是第二段.
```

这样编译出来就是两个段落。在正文部分，多余的空格、回车等等都会被自动忽略，这保证了全文排版不会突然多出一行或者多出一个空格。另外，另起一页的方式是：

```tex
\newpage
```

笔者在编写文档时，为了保证美观，通常将中文标点符号替换为英文标点符号（需要注意的是英文标点符号后面还有一个空格），这比较适合数学类型的文档。

在正文中，还可以设置局部的特殊字体：

|字体|命令|
|---|---|
|直立|\textup{}|
|意大利|\textit{}|
|倾斜|\textsl{}|
|小型大写|\textsc{}|
|加宽加粗|\textbf{}|

### 章节

对于`ctexart`文件类型，章节可以用`\section{}`和`\subsection{}`命令来标记，例如：

```tex
\documentclass[12pt, a4paper, oneside]{ctexart}
\usepackage{amsmath, amsthm, amssymb, graphicx}
\usepackage[bookmarks=true, colorlinks, citecolor=blue, linkcolor=black]{hyperref}

% 导言区

\title{我的第一个\LaTeX 文档}
\author{Dylaaan}
\date{\today}

\begin{document}

\maketitle

\section{一级标题}

\subsection{二级标题}

这里是正文. 

\subsection{二级标题}

这里是正文. 

\end{document}
```

### 目录

在有了章节的结构之后，使用`\tableofcontents`命令就可以在指定位置生成目录。通常带有目录的文件需要编译两次，因为需要先在目录中生成.toc文件，再据此生成目录。

```tex
\documentclass[12pt, a4paper, oneside]{ctexart}
\usepackage{amsmath, amsthm, amssymb, graphicx}
\usepackage[bookmarks=true, colorlinks, citecolor=blue, linkcolor=black]{hyperref}

% 导言区

\title{我的第一个\LaTeX 文档}
\author{Dylaaan}
\date{\today}

\begin{document}

\maketitle

\tableofcontents

\section{一级标题}

\subsection{二级标题}

这里是正文. 

\subsection{二级标题}

这里是正文. 

\end{document}
```

### 图片

插入图片需要使用`graphicx`宏包，建议使用如下方式：

```tex
\begin{figure}[htbp]
    \centering
    \includegraphics[width=8cm]{图片.jpg}
    \caption{图片标题}
\end{figure}
```

其中，`[htbp]`的作用是自动选择插入图片的最优位置，`\centering`设置让图片居中，`[width=8cm]`设置了图片的宽度为8cm，`\caption{}`用于设置图片的标题。

### 表格

LaTeX中表格的插入较为麻烦，可以直接使用[Create LaTeX tables online – TablesGenerator.com](https://link.zhihu.com/?target=https%3A//www.tablesgenerator.com/%23)来生成。建议使用如下方式：

```tex
\begin{table}[htbp]
    \centering
    \caption{表格标题}
    \begin{tabular}{ccc}
        1 & 2 & 3 \\
        4 & 5 & 6 \\
        7 & 8 & 9
    \end{tabular}
\end{table}
```

### 列表

LaTeX中的列表环境包含无序列表`itemize`、有序列表`enumerate`和描述`description`，以`enumerate`为例，用法如下：

```tex
\begin{enumerate}
    \item 这是第一点; 
    \item 这是第二点;
    \item 这是第三点. 
\end{enumerate}
```

另外，也可以自定义`\item`的样式：

```tex
\begin{enumerate}
    \item[(1)] 这是第一点; 
    \item[(2)] 这是第二点;
    \item[(3)] 这是第三点. 
\end{enumerate}
```

### 定理环境

定理环境需要使用`amsthm`宏包，首先在导言区加入：

```text
\newtheorem{theorem}{定理}[section]
```

其中`{theorem}`是环境的名称，`{定理}`设置了该环境显示的名称是“定理”，`[section]`的作用是让`theorem`环境在每个section中单独编号。在正文中，用如下方式来加入一条定理：

```tex
\begin{theorem}[定理名称]
    这里是定理的内容. 
\end{theorem}
```

其中`[定理名称]`不是必须的。另外，我们还可以建立新的环境，如果要让新的环境和`theorem`环境一起计数的话，可以用如下方式：

```tex
\newtheorem{theorem}{定理}[section]
\newtheorem{definition}[theorem]{定义}
\newtheorem{lemma}[theorem]{引理}
\newtheorem{corollary}[theorem]{推论}
\newtheorem{example}[theorem]{例}
\newtheorem{proposition}[theorem]{命题}
```

另外，定理的证明可以直接用`proof`环境。

### 页面

最开始选择文件类型时，我们设置的页面大小是a4paper，除此之外，我们也可以修改页面大小为b5paper等等。

一般情况下，LaTeX默认的页边距很大，为了让每一页显示的内容更多一些，我们可以使用`geometry`宏包，并在导言区加入以下代码：

```tex
\usepackage{geometry}
\geometry{left=2.54cm, right=2.54cm, top=3.18cm, bottom=3.18cm}
```

另外，为了设置行间距，可以使用如下代码：

```tex
\linespread{1.5}
```

### 页码

默认的页码编码方式是阿拉伯数字，用户也可以自己设置为小写罗马数字：

```tex
\pagenumbering{roman}
```

另外，`aiph`表示小写字母，`Aiph`表示大写字母，`Roman`表示大写罗马数字，`arabic`表示默认的阿拉伯数字。如果要设置页码的话，可以用如下代码来设置页码从0开始：

```tex
\setcounter{page}{0}
```

## 数学公式的输入方式

### 行内公式

行内公式通常使用`$..$`来输入，这通常被称为公式环境，例如：

```tex
若$a>0$, $b>0$, 则$a+b>0$.
```

公式环境通常使用特殊的字体，并且默认为斜体。需要注意的是，只要是公式，就需要放入公式环境中。如果需要在行内公式中展现出行间公式的效果，可以在前面加入`\displaystyle`，例如

```tex
设$\displaystyle\lim_{n\to\infty}x_n=x$.
```

### 行间公式

行间公式需要用`\[..\]`或者`$$..$$`来输入，推荐使用`\[..\]`，输入方式如下：

```tex
若$a>0$, $b>0$, 则
\[
a+b>0.
\]
```

关于具体的输入方式，可以参考[在线LaTeX公式编辑器-编辑器 (latexlive.com)](https://link.zhihu.com/?target=https%3A//www.latexlive.com/)，在这里只列举一些需要注意的。

### 上下标

上标可以用`^`输入，例如`a^n`，效果为  ；下标可以用`_`来输入，例如`a_1`，效果为  。上下标只会读取第一个字符，如果上下标的内容较多的话，需要改成`^{}`或`_{}`。

### 分式

分式可以用`\dfrac{}{}`来输入，例如`\dfrac{a}{b}`，效果为  。为了在行间、分子、分母或者指数上输入较小的分式，可以改用`\frac{}{}`，例如`a^\frac{1}{n}`，效果为  。

### 括号

括号可以直接用`(..)`输入，但是需要注意的是，有时候括号内的内容高度较大，需要改用`\left(..\right)`。例如`\left(1+\dfrac{1}{n}\right)^n`，效果是  。

在中间需要隔开时，可以用`\left(..\middle|..\right)`。

另外，输入大括号{}时需要用`\{..\}`，其中`\`起到了转义作用。

### 加粗

对于加粗的公式，建议使用`bm`宏包，并且用命令`\bm{}`来加粗，这可以保留公式的斜体。

### 大括号

在这里可以使用`cases`环境，可以用于分段函数或者方程组，例如

```tex
$$
f(x)=\begin{cases}
    x, & x>0, \\
    -x, & x\leq 0.
\end{cases}
$$
```

效果为

### 多行公式

多行公式通常使用`aligned`环境，例如

```tex
$$
\begin{aligned}
a & =b+c \\
& =d+e
\end{aligned}
$$
```

效果为

### 矩阵和行列式

矩阵可以用`bmatrix`环境和`pmatrix`环境，分别为方括号和圆括号，例如

```tex
$$
\begin{bmatrix}
    a & b \\
    c & d
\end{bmatrix}
$$
```

效果为  。如果要输入行列式的话，可以使用`vmatrix`环境，用法同上。

## 最后的话

这个教程比较简短，涉及到的东西也比较少，耐心学习完后，应该能满足日常使用的需求。

LaTeX的使用还需要一定的熟练度，仍有时间的读者还可以考虑：

- 试着用LaTeX抄几页书籍或者写几页文章，增加熟练度；
- 配置Visual Studio Code上的LaTeX，探索效率更高的编辑器；
- 研究如何美化排版，或是使用网络上的精美模板，让排版的效果更好。

编辑于 2024-09-17 12:21・北京

LaTeX
(https://www.zhihu.com/topic/19568710)

LaTeX 排版与设计
(https://www.zhihu.com/topic/19773080)

数学
(https://www.zhihu.com/topic/19554091)