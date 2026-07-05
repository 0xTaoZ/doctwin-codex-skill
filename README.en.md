# DocTwin Translate

English | [简体中文](README.md) | [繁體中文](README.zh-TW.md)

**DocTwin Translate** is an AI Agent Skill for layout-first document translation. It turns PDFs, lecture slides, papers, and handouts into high-fidelity bilingual files, commonly with the **original page on the left and the AI-translated page on the right**.

DocTwin is designed for students, researchers, and multilingual readers who need readable translations without losing formulas, code, diagrams, tables, colors, and page structure.

> Codex is the first-class runtime for DocTwin. Other AI coding agents can use the same workflow if they can read files, run shell/Python commands, and visually inspect rendered PDF pages.

## What It Does

- Creates side-by-side bilingual PDFs.
- Supports many source languages and target languages, depending on the AI model.
- Preserves formulas, code, commands, paths, identifiers, charts, tables, and diagrams as much as possible.
- Uses translation memory and glossary control for consistent terminology.
- Runs render-based QA before final delivery.
- Repairs structured regions such as code blocks, terminals, memory diagrams, tables, and charts when PDF reflow damages them.
- Adds a light attribution watermark to final PDFs by default.

## Best Use Cases

- International students reading foreign-language lecture slides.
- Course PDFs with code, formulas, and diagrams.
- Academic papers and technical notes.
- Documents that need both original text and translated text side by side.
- Simplified Chinese study versions of English, German, French, Japanese, Korean, or other course material.

## Honest Boundary

PDF layout is hard. DocTwin is **layout-first** and optimized for high-fidelity bilingual output, but no workflow can honestly guarantee perfect results for every PDF. The workflow combines layout engines, AI translation memory, post-processing, and visual QA to get as close as possible.

## Install For Codex

```bash
mkdir -p ~/.codex/skills
cp -R skills/doctwin-translate ~/.codex/skills/
```

Install basic Python dependencies:

```bash
python3 -m pip install PyMuPDF PyYAML pillow pdfplumber pypdf reportlab
```

Then invoke it in Codex:

```text
Use $doctwin-translate to turn this PDF into a side-by-side bilingual PDF. Target language: Simplified Chinese. Preserve layout, formulas, code, tables, and diagrams, then render-check the final output.
```

## Use With Other AI Agents

DocTwin can be used by any AI agent that can:

- read local files;
- run shell/Python commands;
- install or call Python PDF tooling;
- render PDF pages and inspect screenshots.

Give the agent `skills/doctwin-translate/SKILL.md` and `docs/UNIVERSAL_AGENT_PROMPT.md`.

Pure chatbots without local execution can use the translation and glossary strategy, but cannot build or verify the final PDF by themselves.

## Output Watermark

DocTwin adds a light footer attribution to final PDFs by default:

```text
Generated with DocTwin Translate © 2026 Haitao Z / 0xTaoZ · github.com/0xTaoZ
```

Users can explicitly request no watermark for private files. Public demos, tutorials, redistributed outputs, and examples should keep the watermark and attribution.

## Upstream Engines

DocTwin may call open-source layout engines when useful, including:

- [BabelDOC](https://github.com/funstory-ai/BabelDOC)
- [PDFMathTranslate](https://github.com/PDFMathTranslate/PDFMathTranslate)

DocTwin is not officially affiliated with those projects. Keep upstream attribution and license notices when distributing modified versions or generated workflows.

## License And Copyright

Copyright (c) 2026 **Haitao Z / 0xTaoZ**.

- GitHub: [https://github.com/0xTaoZ](https://github.com/0xTaoZ)
- Website: [https://0xtaoz.github.io/doctwin-codex-skill](https://0xtaoz.github.io/doctwin-codex-skill)

Released under AGPL-3.0. Redistribution, modification, network deployment, or derivative services must comply with AGPL-3.0 and retain copyright, attribution, and NOTICE files.
