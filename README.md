![](./README.IMAGE/logo-header.png)

---


<div align="center">
<img src="https://img.shields.io/github/languages/code-size/ExBook/ExBook" alt="code-size" />
    <img src="https://img.shields.io/badge/Author-ExBook-orange" alt="Author" />
    </br>
    <img src="https://img.shields.io/github/languages/top/ExBook/ExBook?color=yellow" alt="languages-top" />
    <img src="https://img.shields.io/github/last-commit/ExBook/ExBook" alt="last-commit" />
    <img src="https://img.shields.io/github/languages/count/ExBook/ExBook" alt="languages-count" />
</div>

<div align="center">
    <a href="https://exbook.github.io/">官方网站</a>
</div>

<div align="center">
<br>微信交流群⬇️（如二维码失效，请添加群主微信`shang_an_001`拉你进群）<br><br>
 <img src="./README.IMAGE/wcqr.png" width="18% alt="wcqr" />
</div>

<!-- toc -->
- [简介](#简介)
- [如何使用](#如何使用)
- [文档类参考](#文档类参考)
  - [文档类选项](#文档类选项)
  - [封面设置](#封面设置)
  - [页眉页脚设置](#页眉页脚设置)
  - [主题颜色设置](#主题颜色设置)
  - [题目录入环境及命令](#题目录入环境及命令)
  - [页面水印设置](#页面水印设置)
- [完整例子](#完整例子)
  - [文字录入型刷题本](#文字录入型刷题本)
  - [截图型刷题本](#截图型刷题本)
- [其他](#其他)


# 简介
**ExBook** 是一个专门制作考研做题本/刷题本的 LaTex 文档类，只录入一次题目，就可以快速生成6种版式的PDF文档（如下图）。

<!-- 
<img src="./README.IMAGE/1.png" width="70%">
<img src="./README.IMAGE/2.png" width="70%"> -->
<div align="center">
    <img src="./README.IMAGE/1.png" width="90%">
    <img src="./README.IMAGE/2.png" width="90%">
</div>

**功能特点：**
1. 录入一次题目，就可以生成6种版式（A4紧凑版、A4标准版、A4宽松版、A4单题版、横版Pad版、竖版Pad版）的PDF文档，无需手动修改任何格式；
2. 支持制作**文字录入型刷题本**以及**截图型刷题本**；
3. 支持选择题选项自动排版，可根据选项的文字长度自动排列选项；
4. 极简自定义封面、页眉、页脚等，极简插入图片，无需关注复杂的 LaTex 代码；
5. 提供12种美观易用的颜色主题，包含4种经典主题以及8种个性主题；
6. 支持自定义添加水印，包含**行内文字水印**以及**全局页面水印**；
7. Pad版（横版Pad版、竖版Pad版）下支持深色模式；
8. 支持成组自定义题目编号和标签样式，并支持组内单个题目编号的重定义；
9. 支持代码高亮。

# 如何使用
1. 在 overleaf 上在线使用 ExBook
2. 在本地使用 ExBook

<!-- 具体教程见：[官方网站](https://exbook.github.io/) -->

注意：使用此项目需要一点 Latex 基础！

本地编译推荐使用 `latexmk`，项目根目录已提供 `.latexmkrc` 配置文件：
```bash
# 编译示例文档
latexmk example_text_type.tex
# 清理辅助文件
latexmk -c
```
也可直接使用 `xelatex`：
```bash
xelatex example_text_type.tex
```

# 文档类参考

## 文档类选项
**字体选项（建议使用 `fandol`）：**
* `adobe`：使用 adobe 字体
* `ubuntu`：使用 ubuntu 字体
* `windows`：使用 windows 字体
* `fandol`：使用 fandol 字体，随 texlive 默认安装
* `mac`：使用 mac 字体

**版式选项：**
* `standard`：A4 标准版。每个题目有一定空隙（大概3cm左右），每道题目的内容会强制在同一页，对于选择题而言，题目和选项不会跨业出现；
* `loose`：A4宽松版。每页会有 2 题，对于较长的题目，会自动占用一页；
* `compact`：A4紧凑版。题目间无任何空隙；
* `single`：A4单题版。一页只会出现一题；
* `padl`：横版Pad版。平板刷题，一页一题，适合小题（选择题和填空题）；
* `padp`：竖版Pad版。平板刷题，一页一题，适合大题。

**其他选项：**
* `printmode`：只在A4版下有效，可生成适合双面打印的文档
* `water`：是否显示全局页面水印（水印图片可在配置文件中自定义，水印将显示在页面右下角）
* `online`：在封面显示在线文档链接
* `darkmode`：深色模式（只在Pad版下生效，其他版式下不要用）
* `notocnum`：不显示章节数字编号
* `showmark`：显示页脚标签（A4版式下显示在左右页脚、Pad版式下显示在页面右上方小字位置）
* `analysis`：全文显示题目解析（如果有解析的话），优先级等于题组环境 `qitems` 的显示解析选项 `showanalysis`（见 [题目录入环境及命令](#题目录入环境及命令)），二者不冲突

## 封面设置
打开 `config.tex`，以下配置项可自定义封面内容：
```latex
% 封面设置
\CoverImg{img/cover.jpg} % 封面图片
\PreTitle{ExBook · 刷题本模板} % 前置标题
\Title{此处填写主标题} % 主标题
\TitleDescription{此处填写副标题} % 副标题
\TypeOne{A4紧凑版} % A4紧凑版下的类型标识
\TypeTwo{A4标准版} % A4标准版下的类型标识
\TypeThree{横版Pad版} % 横版Pad版下的类型标识
\TypeFour{A4宽松版} % A4宽松版下的类型标识
\TypeFive{A4单题版} % A4单题版下的类型标识
\TypeSix{竖版Pad版} % 竖版Pad版下的类型标识
\motto{你这个年龄是怎么睡得着觉的} % 封面座右铭
\Creator{研小布} % 制作人
\UpdateTime{\today} % 更新时间
\OnlineCheckUrl{https://github.com/ExBook/ExBook} % 在线勘误文档地址
```
说明如下：
![](./README.IMAGE/3.png)

## 页眉页脚设置
打开 `config.tex`，以下配置项可自定义页眉页脚：
```latex
% 页眉页脚设置
\Lhead{左侧页眉文本} % 左页眉 
\Chead{中间页眉文本} % 中页眉、平板模式（padl或padp）下页眉中间的文字
\Rhead{右侧页眉文本} % 右页眉、平板模式（padl或padp）下页眉右侧的文字
\LheadC{公众号·研小布·} % 平板模式（padl或padp）下页眉左侧的文字
```

## 主题颜色设置
打开 `config.tex`，以下配置项可自定义颜色主题（默认为`\blue`）：
```latex
\setThemeColor{\blue}
```

ExBook 提供4种经典颜色和8种个性颜色。

1. 4种经典颜色主题

    <img src="./README.IMAGE/classicColor.png" width="70%">

    如果你是一个专门制作做题本/刷题本的博主，那么建议选择这四种经典颜色。

2. 8种个性颜色主题

    <img src="./README.IMAGE/personalColor.png" width="70%">

    这八种个性颜色分别来自八种常见的MBTI人格的代表色，可以选择你自己喜欢的颜色。
## 题目录入环境及命令

1. 题组环境
   ```latex
   \begin{qitems}

   \end{qitems}
   ```
   
   环境选项：
   * `unshow`：环境内不显示题目编号
   * `unreset`：环境内不重置题目编号（默认重置）
   * `startnum`：起始编号（数字）
   * `prefix`：自定义题目编号前缀，比如`prefix=（`
   * `suffix`：自定义题目编号后缀，比如`suffix=）`
   * `optprefix`：自定义环境内选择题选项编号前缀，比如`optprefix=(`
   * `optsuffix`：自定义环境内选择题选项编号后缀，比如`optsuffix=(`
   * `showanalysis`：题组环境内显示题目解析，优先级等于文档类选项 `analysis`（见 [文档类选项](#文档类选项)），二者不冲突
2. 题目环境
   ```latex
   \begin{bbox}

   \end{bbox}
   ```
3. 题目命令
    ```latex
   \qitem 题目内容
   ```
   
   命令选项：
   * `\qitem["text1"][text2]`，`"text1"`会出现在题目编号前缀的前面，`"text2"`会出现在题目编号后缀的后面
  
4. 解析环境
    ```latex
    \begin{analysis}[\underline{答案}：]
        答案内容     
    \end{analysis}
   ```
   
   环境选项：
   * `\begin{analysis}[text1]`，`"text1"`：解析/答案内容的前缀

5. 小问环境
   ```latex
    \begin{subqitems}
            \subqitem 第一小问
            \subqitem 第二小问
    \end{subqitems}
   ```
6. 选择题选项命令
   ```latex
    \threechoices{选项内容}{选项内容}{选项内容}         % 三个选项
    \fourchoices{选项内容}{选项内容}{选项内容}{选项内容}        % 四个选项
    \fivechoices{选项内容}{选项内容}{选项内容}{选项内容}{选项内容}      % 五个选项
    \sixchoices{选项内容}{选项内容}{选项内容}{选项内容}{选项内容}{选项内容}{选项内容}   % 六个选项
   ```
7. 代码高亮环境
   ```latex
   \begin{lstlisting}
    此处输入代码
   \end{lstlisting}
   ```
8. 其他命令
   * 空括号（英文和中文）
    ```latex
    \blankbox % 中文空括号
    \eblankbox % 英文空括号
    ```
   * 空下划线
    ```latex
    \blankline % 空下划线
    ```
   * 文字水印命令
    ```latex
    \textwater % 文字水印的内容在 config.tex 中自定义
    ```
   * 插入题目图片命令
    ```latex
    \imgin[0.2]{l}{fig/img01.png} % 第一个参数为缩放比例，第二个参数为图片位置（不填默认居中，l靠左，r靠右）第二个参数为图片路径
    ```
   * 答案页指示命令
    ```latex
    \qanswerloc{10} % 将会显示 “此部分答案见原书 P10”
    ```
   * 自由标题
    ```latex
    \autotitle[位置（默认居中），l靠左、r靠右]{标题}{后缀} % 将会显示 “此部分答案见原书 P10”
    ```

## 页面水印设置
打开 `config.tex`，以下配置项可自定义全局页面水印：
```latex
\TextWater{【微信公众号·研小布】} % 行内文字水印 
\WaterImg{img/water.png} % 图片水印 出现在页面的右下角
```

# 完整例子

## 文字录入型刷题本
`example_text_type.tex`
```latex
% 使用 ExBook 文档类，并传递选项
\documentclass[standard]{ExBook} 
 
\begin{document}

% 加载配置  
\include{config}

% 加载封面
\maketitle 
 
% 加载声明
\include{contents/pre} 

% 加载广告
\include{contents/print}

\setcounter{page}{1}
\tableofcontents 
    
\clearpage 

\section{文字录入型做题本第一章}
\subsection{文字录入型做题本第一章第1节}\qanswerloc{10}

\begin{qitems}

    \begin{bbox}
        \qitem 设$f(x)$满足$2f(x)+f(1-x)=x^2 abc$，则$ \displaystyle\sum \limits_{n}^{0}f(x)=\blankline.$
    \end{bbox}

    \begin{bbox}
        \qitem   设$f(x)=2x+\sqrt{x^{2}+2x+1}$，$g(x)=
        \begin{cases}
        x+2, & x\geqslant0, \\
        x-1, & x<0,  
        \end{cases}$，则$g[f(x)]= \blankline$.
    \end{bbox}

    \begin{bbox}
        \qitem   设某项目用于 发和宣传 总成本为$a$万元 当 发和宣传所 成本分别为$x$万元和 $y$ 万元时， 收益为$R=2x^{\frac{1}{3}}y^{\frac{1}{2}}$万元,则收 最大时，研发所用成本为\blankline.
    \end{bbox}

    \begin{bbox}
        \qitem   已知 $\lim\limits_{x\to0}\dfrac{f(x)}{x}$ 存在，且函数
        $$f(x)=\ln(1+x)+2x\bullet\lim_{x\to0}\frac{f(x)}{\sin x}$$
        则$\lim\limits_{x\to0}\dfrac{f(x)}{x}=$ \blankline.
    \end{bbox}

    \begin{bbox}
        \qitem  可以用\blankbox 定义一个完整的数据结构。\textwater
        \fourchoices{数据元素}{数据对象}{数据关系}{抽象数据类型}     
    \end{bbox}

    \begin{bbox}
        \qitem   若某算法的空间复杂度为$O(1)$，则表示该算法\blankbox 。
        \fourchoices
        {不需要任何辅助空间}
        {所需辅助空间大小与问题规模$n$无关}
        {不需要任何空间}
        {所需空间大小与问题规模$n$无关}
    \end{bbox}
\end{qitems}

\subsection{文字录入型做题本第一章第2节}
\qanswerloc{15}

\begin{qitems}

    \begin{bbox}
        \qitem   下列关于时间复杂度的函数中，时间复杂度最小的是\blankbox 。
        \fourchoices
        {$T_1(n)=n\log_2n +5000n$}
        {$T_2(n)=n^2 - 800n$}
        {$T_3(n)=n\log_2n - 6000n$}
        {$T_4(n)=20000\log_2n$}
    \end{bbox}

    \begin{bbox}
        \qitem   【2017 统考真题】 下列函数的时间复杂度是 \blankbox 。
        \begin{lstlisting}
    int func(int n){
        int i=0, sum=0;
        while(sum<n) sum += ++i;
        return i; 
    }
        \end{lstlisting}
        \fourchoices{$O(\log n)$}{$O(n^{\frac{1}{2}})$}{$O(n)$}{$O(n\log n)$}
    \end{bbox}

\end{qitems}

\section{文字录入型做题本第二章（长标题测试长标题测试）}
\subsection{文字录入型做题本第二章第1节（长标题测试长标题测试）}
\qanswerloc{20}

\begin{qitems}
    
    \begin{bbox}
        \qitem  已知曲线$L:y=\ln\sqrt{x}(2\leqslant x\leqslant4)$，在$L$ 上的任意点$P(x,y)$作切线，记切线与曲线$L$在 $2\leqslant x\leqslant4$
        时所围成的有界区域的面积为$S$.
        \begin{subqitems}
            \subqitem 求一点$P_0$，使上述面积$S$关于$x$的变化率为零；
            \subqitem 当点$P(x,y)$在曲线上移动至$(\mathrm{e},\dfrac{1}{2})$时，横坐标关于时间的变化率为1，求此时面积关于时间的变化率$\dfrac{\mathrm{d}S}{\mathrm{d}t}.$
        \end{subqitems}
    \end{bbox}

    \begin{bbox}
        \qitem 以 $yOz$ 面上的平面曲线段$y=f(z)(z\geqslant0)$ 绕$z$轴旋转一周所成旋转曲面与xOy 面围成一个无上盖容器(见图)，现以 3 cm$^3/$s 的速率把水注人容器内，水面的面积以$\pi$ c$m^2$/ s 的速率增大.已知容器底面积为 16$\pi$ c$m^2$,求曲线$y=f(z)$的方程.
        \imgin[0.4]{}{fig/fig01.png}
    \end{bbox}

    \begin{bbox}
        \qitem   分析以下各程序段， 求出算法的时间复杂度.
        \begin{lstlisting}[escapeinside={(*@}{@*)}]
    (*@\ding{172}:@*)
    i=1; k=0;
    while(i<n-1){
        k=k+10*i;
        i++;
    }

    (*@\ding{173}:@*)
    y=0;
    while((y+1)*(y+1)<=n)
    y=y+1;

    (*@\ding{174}:@*)
    for(i=0;i<n;i++)
        for(j=0;j<m;j++)
            a[i][j]=0;
    
        
        \end{lstlisting}
    \end{bbox}

    \begin{bbox}
        \qitem   【2011 统考真题】一个长度为 $L$（$L\geqslant 1$ ）的升序序列$ S$, 处在第$\lceil L/2\rceil $个位置的数称为 $S$
        的中位数。例如，若序列 $S_1$=（11,13,15,17,19）, 则 $S_1$的中位数是 15, 两 个序列的中位
        数是含它们所有元素的升序序列的中位数。例如，若 $S_2$ =（2,4,6,8,20）, 则$S_1$和$S_2$的中
        位数是 11。现在有两 个等长升序序列$A$和$B$, 试设计一个在时间和空间两 方面都尽可能
        高效的算法，找出两个序列 $A$和$B$的中位数。要求：
        \begin{subqitems}
            \subqitem 给出算法的基本设计思想
            \subqitem  根据设计思想，采用 C 或 C++或 Java 语言描述算法，关键之处给出注释
            \subqitem 说明你所设计算法的时间复杂度和空间复杂度
        \end{subqitems}
    \end{bbox}

\end{qitems}

\end{document}
```

## 截图型刷题本
`example_image_type.tex`
```latex
% 使用 ExBook 文档类，并传递选项
\documentclass[padl]{ExBook} 

\begin{document} 

% 加载配置
\include{config}

% 加载封面
\maketitle 

% 加载声明
\include{contents/pre} 

% 加载广告
\include{contents/print}

\setcounter{page}{1}
\tableofcontents 
    
\clearpage 

\section{截图型刷题本第一章}
\subsection{截图型刷题本第一章第1节}
\qanswerloc{10}

\begin{qitems}
    \insertimg{1}{3}{0.30}{l}{split-images/}
\end{qitems} 

\subsection{截图型刷题本第一章第2节}
\qanswerloc{20}

\begin{qitems}
    \insertimg{4}{6}{0.30}{l}{split-images/}
\end{qitems}
 
\section{截图型刷题本第二章}
\subsection{截图型刷题本第二章第1节}
\qanswerloc{30}

\begin{qitems}
    \insertimg{7}{8}{0.30}{l}{split-images/}
\end{qitems}

\subsection{截图型刷题本第二章第2节}
\qanswerloc{40}

\begin{qitems}
    \insertimg{9}{10}{0.30}{l}{split-images/}
\end{qitems}

\end{document}
```

# 其他
示例封面图片来自 [https://wallhaven.cc/](https://wallhaven.cc/)，如有侵权，请联系删除！

