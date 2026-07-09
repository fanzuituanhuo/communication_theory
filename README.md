# 通信原理笔记 · Communication Theory Notes

这里是通信原理课程的 LaTeX 手写风格笔记，使用 [Loom](https://github.com/Polaris-Aeterna/loom-notes) 文档类排版。

## 目录结构

```
communication_theory/
├── source_coding/              # 当前主要笔记：信源编码的统计基础
│   ├── src/                    # 源代码
│   │   ├── main.tex            # 学生版主文件（填空模式）
│   │   ├── main-answers.tex    # 答案版主文件（显示答案）
│   │   ├── main-body.tex       # 正文内容，被上面两个文件共享
│   │   ├── loom.cls            # 本地 Loom 文档类（支持答案模式）
│   │   ├── sections/           # 分章节源文件
│   │   │   ├── 01-overview.tex
│   │   │   ├── 02-source-types.tex
│   │   │   ├── 03-sequence-source.tex
│   │   │   ├── 04-memoryless-example.tex
│   │   │   ├── 05-entropy.tex
│   │   │   ├── 06-conditional-joint-entropy.tex
│   │   │   └── 07-mutual-information.tex
│   │   └── assets/             # 图片等辅助资源
│   └── pdf/                    # 编译输出的 PDF
│       ├── main.pdf            # 学生版
│       └── main-answers.pdf    # 答案版
├── loom-notes-main/            # Loom 仓库完整副本（参考用，只读）
│   ├── loom.cls
│   ├── template/
│   ├── examples/
│   ├── skill/
│   └── ...
└── loom-notes.zip              # Loom 仓库原始压缩包
```

## 当前进度

`source_coding/src/sections/` 已覆盖：

1. 通信系统与信源编码（有效性 / 可靠性）
2. 信源分类：离散 / 连续、单符号 / 序列
3. 离散消息序列信源的联合分布与链式分解
4. 无记忆信源与等概 / 不等概二进制例子
5. 信息熵：定义、二进制熵函数、最大熵
6. 条件熵与联合熵：链式法则、Shannon 不等式
7. 互信息：定义、概率形式、性质

## 双版本机制

本笔记使用 **fill-in study notes** 风格：

- **学生版** `src/main.tex`：关键定义条款、计算步骤、证明空隙留空，供主动回忆填写。
- **答案版** `src/main-answers.tex`：通过 `\showanswerstrue` 开关，把所有填空显示为红色答案。

两个版本共享同一份正文内容 `src/main-body.tex`，只需改一个文件即可同步更新。

## 编译

需要 XeLaTeX + Libertinus 字体（随 TeX Live 或 MacTeX 安装）。

```bash
cd source_coding/src

# 学生版
latexmk -xelatex main

# 答案版
latexmk -xelatex main-answers

# 把生成的 PDF 移到 pdf/ 目录
mv main.pdf main-answers.pdf ../pdf/
```

编译后 `src/` 里会出现 `.aux`、`.log`、`.xdv` 等中间文件，这些属于编译产物；真正的输出 PDF 建议放到 `pdf/`。

## 依赖

- `loom.cls`：基于 `libertinus-otf`、`xeCJK`、`tcolorbox`、`titlesec` 等宏包
- 字体：`Libertinus Serif/Math`、`Songti SC`、`PingFang SC`、`Optima`、`Avenir Next`

## 笔记方法

参考 Loom 的 fill-in method：

| 元素 | 命令 | 作用 |
|---|---|---|
| 核心直觉 | `strand` 环境 | 每节主线 |
| 定义/定理/例子 | `definition` / `theorem` / `example` | 知识点盒子 |
| 填空 | `\answerin[width]{answer}` | 学生版空白，答案版显示答案 |
| 证明空隙 | `\answertodo{hint}{answer}` | 学生版显示提示，答案版显示答案 |
| 主动练习 | `yourturn` + `\workspace` | 练习区 |
| 页边复习 | `\recall{question}` | 复习钩子 |
| 未决问题 | `\loose{...}` | 下一章钩子 |

## 新增章节的步骤

1. 在 `source_coding/src/sections/` 新建 `08-xxx.tex`
2. 用 `\input{sections/08-xxx}` 添加到 `src/main-body.tex`
3. 用 `\answerin` 和 `\answertodo` 设计填空与答案
4. 分别编译 `main.tex` 和 `main-answers.tex`，检查输出
5. 把生成的 PDF 移到 `source_coding/pdf/`

## 许可证

笔记内容个人学习使用。Loom 文档类及其仓库遵循原仓库 [MIT 许可证](loom-notes-main/LICENSE)。
