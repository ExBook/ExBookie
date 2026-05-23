# AGENTS.md — ExBookie

## 项目概述

ExBookie 是一个 LaTeX 文档类（`.cls`），用于制作考试做题本 / 习题册。一次录入题目，即可通过文档类选项自动生成 6 种版式的 PDF。

## 文件结构

```
ExBookie/
├── ExBook.cls                # 文档类文件（核心，约 6 万行）
├── config.tex                # 用户配置文件（封面、页眉、颜色、水印）
├── .latexmkrc                # latexmk 编译配置
├── example_text_type.tex     # 文字录入型示例
├── example_image_type.tex    # 截图型示例
├── example_text_type.pdf     # 文字录入型编译结果
├── example_image_type.pdf    # 截图型编译结果
├── contents/
│   ├── pre.tex               # 声明/前言
│   └── print.tex             # 广告/推广页
├── img/                      # 封面图、水印图
├── fig/                      # 题目插图
└── split-images/             # 截图型题目的图片
```

## 文档类选项

调用方式：`\documentclass[选项1, 选项2]{ExBook}`

| 类别 | 选项 | 说明 |
|------|------|------|
| 字体 | `fandol`（推荐）, `adobe`, `ubuntu`, `windows`, `mac` | 中文字体集 |
| 版式 | `standard`, `loose`, `compact`, `single`, `padl`, `padp` | 6 种版式 |
| 功能 | `darkmode`, `printmode`, `water`, `online`, `analysis`, `notocnum`, `showmark` | 深色模式、打印、水印等 |

## 核心环境与命令

### 题目录入
- `\begin{qitems}[选项] ... \end{qitems}` — 题组环境，可选：`showanalysis`, `prefix`, `suffix`, `startnum`, `unreset`, `unshow`
- `\begin{bbox} ... \end{bbox}` — 单个题目容器
- `\qitem 题目内容` — 题目内容
- `\begin{analysis}[前缀] ... \end{analysis}` — 解析/答案
- `\begin{subqitems} \subqitem ... \end{subqitems}` — 小问列表

### 选择题
- `\threechoices{A}{B}{C}` — 三个选项
- `\fourchoices{A}{B}{C}{D}` — 四个选项（最常用）
- `\fivechoices{A}{B}{C}{D}{E}` — 五个选项
- `\sixchoices{A}{B}{C}{D}{E}{F}` — 六个选项

选项会自动根据文字长度排列为 1 列、2 列或 4 列。

### 封面配置（config.tex）
- `\CoverImg{path}` — 封面图片
- `\Title{...}`, `\PreTitle{...}`, `\TitleDescription{...}` — 标题
- `\TypeOne` ~ `\TypeSix` — 各版式的类型标识
- `\motto{...}`, `\Creator{...}`, `\UpdateTime{...}`

### 颜色主题（config.tex）
```latex
\setThemeColor{\blue}   % 经典4色：\blue \green \purple \orange
\setThemeColor{\infj}   % MBTI 8色：\infj \enfp \infp \esfp \intj \entp \isfj \enfj
```

### 工具命令
- `\blankbox` / `\eblankbox` — 中/英文空括号
- `\blankline` — 空白下划线
- `\textwater` — 行内水印
- `\imgin[缩放]{对齐}{路径}` — 插入图片
- `\qanswerloc{页码}` — 答案位置指示
- `\autotitle[对齐]{标题}{副标题}` — 自由标题
- `\insertimg{起始}{结束}{缩放}{对齐}{路径}` — 批量插入截图（截图型刷题本）

## 编译

```bash
# 文字录入型
latexmk example_text_type.tex

# 截图型
latexmk example_image_type.tex

# 清理
latexmk -c
```

## AI 辅助用户的常见任务

1. **帮用户写 config.tex** — 根据用户需求设置封面标题、页眉、主题颜色
2. **帮用户录入题目** — 将用户提供的题目文本转换为 ExBook 的题目环境格式
3. **调试编译错误** — LaTeX 编译报错时，检查语法和命令使用
4. **切换版式** — 修改 `\documentclass` 选项即可在 6 种版式间切换
5. **制作截图型刷题本** — 用户提供题目截图时，用 `\insertimg` 批量导入
