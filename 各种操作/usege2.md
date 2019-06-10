##### \documentclass[选项]{文档类}
```latex
文档类

article    排版科技期刊、短报告、程序文档、邀请函等。
report    排版多章节的长报告、短篇的书籍、博士论文等。
book    排版书籍。
slides    排版幻灯片。其中使用了较大的 sans serif 字体。也可以考虑使用 FoilTEX 来得到相同的效果。

文档类的选项

纸张大小（a4paper，a5paper，b4paper，letterpaper，legalpaper，executivepaper）：
默认的letterpaper 纸张常见于美国，和国内常用的A4 纸张的大小稍有差别，建议自己指定。

字体大小（10pt，11pt，12pt）：默认为10pt。

纸张方向（portrait，landscape）：默认为portrait（纵向），在屏幕阅读也许landscape（横向）更方便。

草稿定稿（draft，final）：默认为final（定稿）；如果是draft（草稿），页面内容有溢出时会显示粗黑条。

单面双面（oneside，twoside）：对于article 和report 文档类，默认设置为单面，页码总是在右边；对于book 文档类，默认设置为双面，奇数页页码在右边，偶数页页码在左边，这样双面打印时页码总在外侧。

新章开始（openright，openany）：仅对book 文档类有效，默认值为openright，即每章都从奇数页开始；如果设置为openany，则每章仅从新的一页开始，不管奇偶页。
```
##### 段落换行
用一个空行或者\par 命令可以开始新的段落，同时会有默认的首行缩进。用\\ 或者\newline 可以强制换行在下一行继续，且在下一行不会有缩进。
##### 列表环境
列表环境有三种：无序列表（itemize）、有序列表（enumerate）和描述列表（description）。

```latex
\documentclass[UTF8]{ctexart}

\begin{document}

\begin{itemize}
  \item javascript
  \item html
  \item css
\end{itemize}

\begin{enumerate}
  \item javascript
  \item html
  \item css
\end{enumerate}

\begin{description}
  \item[javascript] javascript
  \item[html] html
  \item[css] css
\end{description}

\end{document}
```
###### 标题摘要
用下面的代码可以加入文章的标题、作者、日期信息和内容摘要：
```latex
\documentclass[UTF8]{ctexart}

\begin{document}

\title{Latex与Winedt}
\author{jingwhale}
\date{January 25, 2015}
\maketitle

\begin{abstract}
LATEX是一种基于TEX的排版系统，由美国电脑学家莱斯利•兰伯特在20世纪80年代初期开发，利用这种格式，即使用户没有排版和程序设计的知识也可以充分发挥由TEX所提供的强大功能。对于生成复杂表格和数学公式，这一点表现得尤为突出。因此它非常适用于生成高印刷质量的科技和数学类文档。这个系统同样适用于生成从简单的邮件到完整书籍的所有其他种类的文档。
\end{abstract}

\end{document}
```
如果\date{} 命令的参数为空，则不显示日期信息。如果不出现\date 命令，则默认显示当前的日期。
##### 章节目录
在book 和report 文档类中，可以使用\part、\chapter、\section 、\subsection、\subsubsection、\paragraph、\subparagraph 这些章节命令，在article 文档类中，除了\chapter 不能用，其它的都可以用。

用\tableofcontents 命令可以自动从各章节标题生成目录。

在导言区中用下面的命令载入hyperref 宏包`\usepackage{hyperref}`就可以让生成的文章目录有链接，点击时会自动跳转到该章节。而且也会使得生成的pdf文件带有目录书签。
```latex
\documentclass[UTF8]{ctexart}

\usepackage{hyperref}

\begin{document}

\tableofcontents

\part{部分标题}
%\chapter{章标题}这一章我们介绍这些内容。
\section{节标题}这一节我们介绍这些内容。
\subsection{小节标题}这一小节我们介绍这些内容。
\subsubsection{子节标题}这一子节我们介绍这些内容。
\paragraph{段标题}这一段我们介绍这些内容。
\subparagraph{小段标题}这一小段我们介绍这些内容。

\end{document}
```

要调整章节标题在目录页中的格式，可以用titletoc 宏包。该宏包的基本命令参数如下:
```latex
\titlecontents{标题层次}[左间距]{整体格式}{标题序号}{标题内容}{指引线和页码}[下间距]
```
##### 参考文献
引用文献的基本环境是：
```latex
\begin{thebibliography}{}
\bibitem[显示符号]{引用标签} Book Title, Author
\end{thebibliography}
```
其中`\begin{thebibliography}{}`的大括号内填入的数字表示最大标号值。
\bibitem表示一条文献记录。其中[显示符号]表示在参考文献区域显示的标号，可不填，默认使用数字1,2,3进行编号。引用标签则是在正文中引用的标签。参考文献的引用和其他的引用有点不同，需要用\cite{引用标签}来引用。

```
\documentclass[UTF8]{ctexart}

\begin{document}

\begin{thebibliography}{123456}
\bibitem {JW1}Jingwhale, T.A.O.C.P. , Yunlong Zhang , 2015,Vol. 1.
\bibitem {JW2}Jingwhale, T.A.O.C.P. , Yunlong Zhang , 2015,Vol. 6.
\bibitem {JW2}Jingwhale, T.A.O.C.P. , Yunlong Zhang , 2015,Vol. 8.
\end{thebibliography}

\end{document}
```
TIPS：
- 默认thebibliography会自动添加标题Reference，所以无需重复添加
- 默认参考文献的行间距为一行，这有时候显得太大了。可以在`\begin{thebibliography}{}`后添加`\addtolength{\itemsep}{-1.5ex}`来缩小行间距。-1.5ex表示每行缩小1.5ex。其实细心观察可以发现，thebibliography其实是一个枚举环境，因此对于itemize和enumerate，可以用同样的方法缩小行间距。
- thebibliography是十分繁琐的。因为你还需要把作者等信息一个个地填上去。有没有什么更好的方法呢？答案是：有的。那就是bibtex！bibtex是一个引用数据库，一般以bib后缀结尾。各大论文网站都会提供bibtex格式的文献引用。这里不做详解，可以到网上搜所一下。
##### 数学公式
###### 折行公式
一个公式太长需要拆为几行，这种折行公式应该只需要一个编号，可以使用equation 环境中的\split 环境。例如：
```latex
\begin{equation}
\begin{split}
(3+3)\cdot111 &= 3\cdot111 + 3\cdot111 \\
&= 666
\end{split}
\end{equation}
```
###### 复杂公式
```latex
\documentclass{article}

\usepackage{amsmath}

\begin{document}

\begin{equation}
\left.
\begin{aligned}
x+y &> 5 \\
y-y &> 11
\end{aligned}
\ \right\}\Rightarrow x^2 - y^2 > 55
\end{equation}

\end{document}
```
##### 排版
```latex
\documentclass{article}
\usepackage{CJK}
%\begin{document}
\begin{CJK}{GBK}{song}
CTeX里中文默认用宋体！
\CJKfamily}{GBK}{hei} 这是CTeX里的黑体！
\CJKfamily{fs} 这是CTeX里的仿宋体！
\CJKfamily{kai} 这是CTeX里的楷体！
\CJKfamily{li} 这是CTeX里的隶书！
\CJKfamily{you} 这是CTeX里的幼圆体！
\end{CJK}
\end{document}
```
```latex
\begin{center}//段落居中对齐
啦啦啦
\end{center}

\begin{flushleft}//段落向左对齐
啦啦啦
\end{flushleft}

\begin{flushright}//段落向右对齐
啦啦啦
\end{flushright}
```
####### 调整页面布局
现在我们来说说如何定制页面的布局，比如正文区域的宽度和高度，和各个边距的大小。LATEX 中一般推荐用geometry 宏包来调整页面的布局。例如本文档（页面为B5 纸张大小）的页面布局就是用如下的代码设定的：
```latex
\usepackage[text={125mm,195mm},centering]{geometry}
```
其中的geometry 包的`text={width,height}` 选项指明了页面正文区域的宽度和高度大小，而后面的centering 选项表示将正文区域自动居中（即上下边距相等，而且左右边距也相等）。

`\clearpage`令起一页，与前页格式相同
`\newpage`令起一页，无格式