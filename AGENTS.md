# Agent Notes for communication_theory

## 项目目标

用 Loom 手写风 LaTeX 类编写通信原理课程的 **fill-in study notes**。笔记要同时满足：

1. **可读**：概念陈述完整、条理清晰；
2. **可填**：关键定义条款、计算过程、结论判据等留空，供主动回忆；
3. **可出答案**：同一份源码能生成学生版（挖空）和答案版（填红）。

当前聚焦章节：**信源编码的统计基础**（source coding）。

## 目录约定

- `source_coding/`：唯一活跃工作目录。
  - `src/`：所有源代码和编译输入
    - `main.tex`：学生版入口，只设置宏和文档类，然后 `\input{main-body}`
    - `main-answers.tex`：答案版入口，在 `\input{main-body}` 前设置 `\showanswerstrue`
    - `main-body.tex`：共享正文，包含封面、总览地图、所有 `\input{sections/...}`
    - `sections/*.tex`：分节内容
    - `loom.cls`：本地 Loom 文档类（已扩展答案模式）
    - `assets/`：图片等辅助资源
  - `pdf/`：编译输出的 PDF
    - `main.pdf`：学生版
    - `main-answers.pdf`：答案版
- `loom-notes-main/`：Loom 仓库只读参考，包含模板、示例和 skill。
- `source-statistics-loom/`：**已删除**。

## 技术栈

- 引擎：XeLaTeX
- 文档类：`src/loom.cls`（本地副本，已扩展答案模式）
- 加载方式：`\documentclass[cjk]{loom}`
- 双版本机制：由 `\ifshowanswers` 条件控制

## 填空与答案命令

本地 `loom.cls` 新增了两个核心命令，**优先使用它们**而不是旧的 `\fillin` / `\TODO`：

### `\answerin[width]{answer}`

- 学生版：显示为空白下划线（宽度可省略，默认 `2.2cm`）
- 答案版：显示红色答案，居中在下划线上

```tex
\answerin[3cm]{信源统计特性}
```

### `\answertodo{hint}{answer}`

- 学生版：显示 `[fill in: hint]`
- 答案版：显示红色 `[answer]`

```tex
\answertodo{用 Jensen 不等式}{由 Jensen 不等式，...}
```

## 编辑规范

1. **只在 `source_coding/src/` 里改**。
2. **共享正文在 `main-body.tex`**：新增章节时，在 `main-body.tex` 里加 `\input{sections/xx-xxx}`，不要同时改 `main.tex` 和 `main-answers.tex`。
3. **保持 fill-in 比例**：约 70% 阅读、30% 填空。不要把所有细节填死，也不要空得读不懂。
4. **定理与证明处理**：
   - 定理、引理、命题、推论的陈述默认完整给出，不挖空。
   - 证明默认不挖空，保持推导连贯可读；不要按 skill 示例把证明机械改成 proof skeleton。
   - 证明后适合加一个简短 `yourturn`，让学生复述关键动作、关键等式或一句话直觉。
   - 主动回忆优先放在定义关键条款、对照表、例题计算、结论判据、`yourturn`，或证明后的简短“关键思想回忆”中。
   - 只有特别适合训练的一步短证明，才可少量用 `\answertodo` 挖一个核心动作。
5. **符号一致性**：
   - 概率质量函数用 `\pmf`（定义为 `p`）
   - 单符号取值集合优先用 `\Xcal`（`\mathcal{X}`）
   - 互信息用 `\info`（定义为 `I`）
   - 序列用 `X^L` 或 `(X_1,\dots,X_L)`
6. **中文字体**：正文和数学环境中的中文都已通过 `xeCJK` + `CJKmath=true` 支持，直接写中文即可。
7. **每节固定节奏**：
   - `\section{标题}`
   - `\warmth{0}\quad\whisper{...}`
   - `\begin{strand} ... \end{strand}`
   - 知识点盒子 + 表格 + `\answerin` / `\answertodo` + `yourturn`
   - `\recall{...}`

## 编译检查

修改后必须两个版本都能编译通过：

```bash
cd source_coding/src
latexmk -xelatex main
latexmk -xelatex main-answers
mv main.pdf main-answers.pdf ../pdf/
```

编译中间文件（`.aux`、`.log`、`.xdv` 等）默认留在 `src/`；最终 PDF 放到 `pdf/`。

如果出现字体或宏包错误，先检查是否使用了系统未安装的字体，再检查是否漏了 `[cjk]` 选项。

## 与 Loom skill 的关系

`loom-notes-main/skill/` 是一份 Kimi Code CLI 可用的 fill-in-notes skill，已安装到：

```
~/.config/agents/skills/fill-in-notes/
```

新会话中若用户说「把这一章做成 fill-in notes」或类似触发语，会自动加载该 skill。注意：skill 里的示例使用的是旧的 `\fillin` / `\TODO`，而本项目实际使用的是本地扩展的 `\answerin` / `\answertodo`。请按本项目规范执行。

## 注意事项

- 不要修改 `loom-notes-main/` 里的官方文件，除非是要同步更新 Loom 版本。
- 新增图片统一放在 `source_coding/src/assets/`。
- 最终 PDF 输出到 `source_coding/pdf/`，不要把 `.aux`、`.log` 等中间文件误提交到那里。
