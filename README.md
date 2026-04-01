# 深入浅出 Claude Code

> 当前 Claude Code 源码解析是当前技术社区的高热方向。

《深入浅出 Claude Code》是一个面向 `claude-code` 源码分析的中文技术书稿仓库，目标是把复杂系统拆解为可复用的工程知识：源码结构、运行机制、权限与扩展、安全与上下文策略。

本仓库的产出以书稿形式整理，内容可能尚不完美，但可作为 **Claude Code 源码分析的基础版本**，用于继续扩展、校对和迭代。

仓库包含 LaTeX 源码、封面资源、章节内容以及可编译的 PDF 输出。

## 目录结构

- `main.tex`: 主控文件
- `frontmatter/`: 扉页、推荐语、前言、阅读指南
- `chapters/`: 正文章节
- `appendix/`: 附录
- `assets/`: 图片资源，包括封面
- `build/`: 编译输出目录

## 环境要求

- TeX Live 2024+ 或对应版本的 MacTeX
- `latexmk`
- `xelatex`
- `ctex` 宏包

在 Linux 上如果使用最小 TeX Live，通常需要补充安装中文支持相关包，例如：

```bash
sudo apt install texlive-xetex texlive-lang-chinese latexmk
```

## 编译

在仓库根目录执行：

```bash
latexmk -xelatex -interaction=nonstopmode -halt-on-error -output-directory=build main.tex
```

输出文件位于：

```text
build/main.pdf
```

## 封面

- 封面图片文件：`assets/book_cover.png`
- PDF 第 1 页为整页图片封面
- 图片封面后紧跟文字扉页

如果需要替换封面，直接替换 `assets/book_cover.png` 后重新编译即可。

## 字体与可移植性

- 默认使用 `ctexbook` 的标准 `fandol` 字体集
- 不依赖任何机器本地字体绝对路径
- 仓库克隆后应可直接在标准 TeX Live / MacTeX 环境中编译

## AI 书稿生成方案（基于 claude-code 源码）

本仓库配套提供了 `plan.md`（书稿生产方案）。
如果你要复现本书的 AI 生成流程，请按以下方式使用：

1. 以 `plan.md` 为主控文档，先执行 `第2节/第4节` 的目标定义与结构约束，
2. 按 `第7节` 的任务流建立章节/小节任务，
3. 每轮在本地文件体系中落盘输入与输出，再提交审查，
4. 按 `第11-12节` 的标准流程走 `plan -> draft -> review -> tex -> compile`。

可直接复用的系统提示词骨架（来自 `plan.md`）如下：

```text
你正在参与一本基于 Claude Code 源码的技术书写作。
你的首要目标不是“写得像书”，而是“写得可验证、可合并、可复审”。

请严格遵守：
1. 只依据本轮提供的源码范围、既有术语表、已存档资料作答。
2. 若证据不足，明确写“待核实”，不得补全不存在的实现细节。
3. 所有关键论断都要标注 [S]/[I]/[E]/[Q]。
4. 先输出大纲、计划、资料需求、引用点，再输出正文。
5. 正文以工程实现解释为主，不写营销语言，不写空泛赞美。
6. 只对本轮任务目标产出，避免擅自扩写到其他章节。
```

你也可查看 `plan.md` 9.3 的“输出格式模板”，将其作为每轮必输结构。

## License

除非另有说明，本仓库中的书稿正文、LaTeX 源文件、图片资源和示例内容均采用 `CC BY-NC-SA 4.0` 许可发布。详见 [LICENSE](./LICENSE)。
