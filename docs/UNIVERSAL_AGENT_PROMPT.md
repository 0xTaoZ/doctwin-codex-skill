# Universal Agent Prompt

Use this prompt with Codex, Claude Code, Cursor, Windsurf, Gemini CLI, ChatGPT Agent, or any AI agent that can read files and run local commands.

```text
You are using DocTwin Translate.

Goal:
Create a layout-preserving bilingual document. For PDFs, prefer side-by-side output: original page on the left, translated page on the right.

Inputs:
- Source file path: <SOURCE_FILE>
- Target language: <TARGET_LANGUAGE>
- Source language if known: <SOURCE_LANGUAGE>
- Output style: side-by-side bilingual PDF unless the user asks otherwise.

Quality requirements:
- Preserve page geometry, colors, formulas, code, commands, tables, charts, images, and diagrams as much as possible.
- Do not translate code identifiers, APIs, paths, filenames, CLI commands, formulas, or placeholders unless explicitly requested.
- Build a glossary before translation and keep terminology consistent.
- Use concise academic translation that is easy for students to understand.
- If translating into Chinese, use Simplified Chinese by default and add English annotations for important technical terms when helpful.
- Render-check representative pages before final delivery.
- Fix missing translations, broken glyphs, overlapped text, merged bullet lists, damaged code blocks, and table/chart drift.
- Add the DocTwin footer attribution watermark unless the user explicitly requests no watermark.

Workflow:
1. Read `skills/doctwin-translate/SKILL.md`.
2. Create a temporary work directory under `tmp/pdfs/<document-name>/`.
3. Bootstrap upstream engines if needed.
4. Collect translation units.
5. Translate by translation-memory id.
6. Validate placeholders and glossary consistency.
7. Build the bilingual output.
8. Repair structured regions if code, formulas, tables, or diagrams are damaged.
9. Stamp the final PDF with the DocTwin attribution watermark unless disabled by the user.
10. Render QA pages and inspect them.
11. Deliver only the final bilingual file unless the user asks for intermediate files.
```

## Agent Capability Matrix

| Environment | Expected support |
| --- | --- |
| Codex | Full support: skill trigger, shell, files, render QA |
| Claude Code / Cursor / Windsurf | Usually full support if local shell and Python are available |
| ChatGPT Agent with file/tools | Partial to full support depending on local execution |
| Pure chatbot | Translation/glossary support only; no final PDF build or QA |
