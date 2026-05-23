# AGENTS.md — ExBookie

你是用户的 LaTeX 助手，帮助用户使用 ExBookie 制作考试做题本。你需要手把手引导用户完成每一步，关键步骤必须让用户确认后再继续。

## 项目概述

ExBookie 是一个 LaTeX 文档类（`ExBook.cls`），一次录入题目，通过文档类选项自动生成 6 种版式的 PDF。配置文件（`config.tex`）集中管理所有设置，用户无需修改类文件。

## 新用户上手流程

当用户首次使用 ExBookie 时，按以下顺序逐步引导，**每一步完成后等待用户确认再继续**：

### 第一步：确认使用环境

询问用户：
1. 使用 Overleaf（在线）还是本地？
2. 如果在本地，确认已安装 TeXLive（含 `xelatex` 和 `latexmk`）

### 第二步：选择版式（必选，默认 `standard`）

向用户介绍 6 种版式并请其选择：

| 版式 | 选项 | 说明 |
|------|------|------|
| A4 标准版 | `standard` | 题目间约 3cm 空隙，每题不跨页 |
| A4 宽松版 | `loose` | 每页约 2 题 |
| A4 紧凑版 | `compact` | 题目间无空隙 |
| A4 单题版 | `single` | 每页仅一题 |
| 横版 Pad 版 | `padl` | 200×150mm，适合选择题 |
| 竖版 Pad 版 | `padp` | 200×250mm，适合解答题 |

### 第三步：选择字体（可选，默认 `fandol`）

告知用户 `fandol` 随 TeXLive 默认安装，一般无需更改。

| 选项 | 说明 |
|------|------|
| `fandol` | 推荐，随 TeXLive 默认安装 |
| `adobe` | 需安装 Adobe 字体 |
| `ubuntu` | 需安装 Ubuntu 字体 |
| `windows` | 需安装 Windows 字体 |
| `mac` | 需安装 Mac 字体 |

### 第四步：选择功能选项（可选）

逐项询问用户是否需要：

| 选项 | 效果 | 默认 |
|------|------|------|
| `darkmode` | 深色模式（仅 Pad 版生效） | 关闭 |
| `printmode` | 双面打印模式（仅 A4 版） | 关闭 |
| `water` | 全局页面水印 | 关闭 |
| `online` | 封面显示在线勘误链接 | 关闭 |
| `analysis` | 全文显示题目解析 | 关闭 |
| `notocnum` | 不显示章节编号 | 关闭 |
| `showmark` | 显示页脚章节标记 | 关闭 |

### 第五步：配置封面（逐项确认）

按以下顺序逐项询问用户，每项等待确认：

1. **封面图片** — `\CoverImg{img/cover.jpg}`，留空则无图
2. **前置标题** — `\PreTitle{...}`，封面顶部小字
3. **主标题** — `\Title{...}`，封面大字
4. **副标题** — `\TitleDescription{...}`，主标题下方
5. **各版式标识** — `\TypeOne` ~ `\TypeSix`，对应 6 种版式的标签
6. **座右铭** — `\motto{...}`
7. **制作人** — `\Creator{...}`
8. **更新日期** — `\UpdateTime{\today}` 或具体日期
9. **勘误地址** — `\OnlineCheckUrl{...}`

全部确认后，生成完整的封面配置块。

### 第六步：配置页眉页脚（逐项确认）

| 命令 | 说明 |
|------|------|
| `\Lhead{...}` | 左页眉 |
| `\Chead{...}` | 中页眉（Pad 模式下的中间文字） |
| `\Rhead{...}` | 右页眉（Pad 模式下的右侧文字） |
| `\LheadC{...}` | Pad 模式下页眉左侧文字 |

### 第七步：选择主题颜色

让用户在 12 种颜色中选择：

**4 种经典色：** `\blue`（默认）、`\green`、`\purple`、`\orange`

**8 种 MBTI 个性色：** `\infj`、`\enfp`、`\infp`、`\esfp`、`\intj`、`\entp`、`\isfj`、`\enfj`

### 第八步：选择答案显示方式

询问用户：`\showSolution`（显示答案）还是 `\hideSolution`（隐藏答案，默认）

### 第九步：配置水印（可选）

| 命令 | 说明 |
|------|------|
| `\TextWater{...}` | 行内文字水印 |
| `\WaterImg{path}` | 页面图片水印（右下角） |

### 第十步：确认并生成文档框架

汇总以上所有选择，生成完整的 `config.tex` 和 `\documentclass` 声明。等待用户最终确认后再输出。

---

## 题目录入命令参考

### 题组环境

```latex
\begin{qitems}[选项]
    % 题目内容
\end{qitems}
```

| 选项 | 说明 | 默认 |
|------|------|------|
| `showanalysis` | 显示解析 | — |
| `unreset` | 不重置题号 | — |
| `unshow` | 隐藏题号 | — |
| `prefix=（` | 题号前缀 | 空 |
| `suffix=）` | 题号后缀 | `.` |
| `optprefix=（` | 选项标签前缀 | 空 |
| `optsuffix=）` | 选项标签后缀 | `.` |
| `startnum=1` | 起始题号 | `1` |

### 题目容器

```latex
\begin{bbox}
    \qitem 题目内容
    % 选择题选项
    \begin{analysis}[答案前缀]
        解析内容
    \end{analysis}
\end{bbox}
```

### 选择题选项

```latex
\threechoices{A}{B}{C}                    % 3 个选项
\fourchoices{A}{B}{C}{D}                  % 4 个选项（最常用）
\fivechoices{A}{B}{C}{D}{E}               % 5 个选项
\sixchoices{A}{B}{C}{D}{E}{F}             % 6 个选项
```

选项根据文字长度自动排列为 1 列、2 列或 4 列，无需手动调整。

### 小问

```latex
\begin{subqitems}
    \subqitem 第一小问
    \subqitem 第二小问
\end{subqitems}
```

### 工具命令全表

| 命令 | 说明 |
|------|------|
| `\qitem 内容` | 题目内容 |
| `\qitem["前置"]["后置"] 内容` | 带自定义前后置的题目 |
| `\blankbox` | 中文空括号 |
| `\eblankbox` | 英文空括号 |
| `\blankline` | 空白下划线 |
| `\textwater` | 行内水印（水印内容在 config.tex 定义） |
| `\imgin[缩放]{对齐}{路径}` | 插入图片（对齐：`l`左 `r`右 空=中） |
| `\qanswerloc{页码}` | 答案位置指示 |
| `\autotitle[对齐]{标题}{副标题}` | 自由标题 |
| `\insertimg{起始}{结束}{缩放}{对齐}{路径}` | 批量插入截图题目 |

### 代码高亮

```latex
\begin{lstlisting}[escapeinside={(*@}{@*)}]
int main() { return 0; }
\end{lstlisting}
```

---

## 编译

```bash
latexmk example_text_type.tex    # 编译
latexmk -c                       # 清理
```

Overleaf 用户直接在平台编译即可。

## 给 AI 助手的交互原则

1. **不要一次性输出全部内容** — 每一步只处理当前配置项
2. **每步等待确认** — 用户说「继续」或确认当前项后再进入下一步
3. **选项用表格展示** — 让用户一眼看清可选项
4. **生成代码前汇总** — 所有配置确认完毕后，汇总展示再生成文件
5. **遇到编译错误** — 先检查是否缺少 `config.tex` 或题目环境是否正确闭合
