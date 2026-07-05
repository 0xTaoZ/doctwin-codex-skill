# DocTwin Translate

[English](README.en.md) | 简体中文 | [繁體中文](README.zh-TW.md)

**DocTwin Translate** 是一个面向 AI Agent 的文档双语对照 Skill：把 PDF、课件、论文、讲义等文件转换成高保真双语版本，常见形式是 **左侧原文，右侧 AI 译文**。

它特别适合留学生、自学者、研究生和需要啃外语课件的人：保留原文页面、公式、代码、表格、图表和页面结构，同时生成更容易读懂的中文译文。

> Codex 是 DocTwin 的一等适配环境；其他能读文件、运行 shell/Python、渲染检查 PDF 的 AI Agent 也可以按同一套流程使用。

## 适合谁

- 留学生阅读英文、德文、法文、日文等课程 PDF
- 需要把课件做成左右双语对照版
- 需要尽量保留数学公式、代码、图表和表格位置
- 需要统一专业术语，而不是每页翻译风格乱跳
- 需要 AI 参与翻译质量控制和渲染检查

## 核心能力

- **左右双语对照 PDF**：左边保留原 PDF，右边生成译文页。
- **多语言支持**：只要 AI 模型能理解，就可以从多种语言翻译到中文或其他目标语言。
- **课程友好**：面向 lecture slides、handouts、papers、code-heavy PDFs 优化。
- **术语一致性**：使用 translation memory 和 glossary 控制专业词。
- **公式/代码保护**：尽量保留公式、代码、命令、路径、变量名、API 名称。
- **复杂版式 QA**：渲染检查页，发现错位、乱码、重叠、缺译后再修。
- **结构区回填**：代码块、终端输出、内存图、复杂表格等区域可按原 PDF 视觉回填，减少重排损坏。
- **署名水印**：默认在最终 PDF 页脚加入轻量 DocTwin 版权水印，保护项目归属。

## 不是魔法

PDF 是非常复杂的格式。DocTwin 的目标是 **layout-first high fidelity**，不是承诺所有 PDF 都 100% 完美。它会通过翻译记忆、版式引擎、后处理和渲染 QA 尽量逼近高质量结果。

## 安装到 Codex

把 Skill 文件夹复制到 Codex Skills 目录：

```bash
mkdir -p ~/.codex/skills
cp -R skills/doctwin-translate ~/.codex/skills/
```

安装基础 Python 依赖：

```bash
python3 -m pip install PyMuPDF PyYAML pillow pdfplumber pypdf reportlab
```

然后在 Codex 中这样调用：

```text
使用 $doctwin-translate 把这份 PDF 做成左右双语对照版。目标语言是简体中文，保留原排版，重点检查公式、代码、表格和图表。
```

## 其他 AI Agent 怎么用

DocTwin 不是只能给 Codex 用。只要你的 AI Agent 能做到下面几件事，就可以使用：

- 读取本地文件和文件夹
- 执行 shell/Python 命令
- 安装或调用 Python PDF 依赖
- 渲染 PDF 页面并查看截图

可以把 `skills/doctwin-translate/SKILL.md` 和 `docs/UNIVERSAL_AGENT_PROMPT.md` 交给你的 Agent，让它按流程执行。

没有本地执行能力的纯聊天机器人不能直接生成和验收最终 PDF，只能辅助翻译文本、术语表和提示词。

## 输出水印

DocTwin 默认在最终 PDF 页脚加入很轻的署名水印：

```text
Generated with DocTwin Translate © 2026 Haitao Z / 0xTaoZ · github.com/0xTaoZ
```

如果是私人文件，可以在提示词里明确写“不要添加水印”。如果是公开演示、教程、二次分发或宣传样例，建议保留水印和版权信息。

## 推荐提示词

```text
使用 DocTwin Translate 工作流，把这份 PDF 转成左右双语对照 PDF：左侧保留原文页面，右侧生成简体中文译文。请保持公式、代码、表格、图表、颜色和页面结构尽可能一致；术语要统一，翻译要适合学生理解；最后渲染检查关键页面，修复错位、缺译、乱码和代码块损坏后再交付最终 PDF。
```

## 开源依赖与致谢

DocTwin 是一个 AI Agent Skill / workflow。它会在可用时调用优秀的开源 PDF 排版与翻译引擎，包括但不限于：

- [BabelDOC](https://github.com/funstory-ai/BabelDOC)
- [PDFMathTranslate](https://github.com/PDFMathTranslate/PDFMathTranslate)

这些上游项目有自己的许可证和版权要求。DocTwin 不声称与这些项目存在官方隶属关系。

## 版权

Copyright (c) 2026 **Haitao Z / 0xTaoZ**.

- GitHub: [https://github.com/0xTaoZ](https://github.com/0xTaoZ)
- Website: [https://0xtaoz.github.io/doctwin-codex-skill](https://0xtaoz.github.io/doctwin-codex-skill)

本项目以 AGPL-3.0 发布。二次分发、修改、部署或基于本项目提供网络服务时，请遵守 AGPL-3.0，并保留原始版权、署名和 NOTICE。
