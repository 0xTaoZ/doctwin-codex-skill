# DocTwin Translate

[English](README.en.md) | [简体中文](README.md) | 繁體中文

**DocTwin Translate** 是一個面向 AI Agent 的文檔雙語對照 Skill：把 PDF、課件、論文、講義等文件轉換成高保真雙語版本，常見形式是 **左側原文，右側 AI 譯文**。

它特別適合留學生、自學者、研究生和需要啃外語課件的人：保留原文頁面、公式、代碼、表格、圖表和頁面結構，同時生成更容易讀懂的中文譯文。

> Codex 是 DocTwin 的一等適配環境；其他能讀文件、運行 shell/Python、渲染檢查 PDF 的 AI Agent 也可以按同一套流程使用。

## 適合誰

- 留學生閱讀英文、德文、法文、日文等課程 PDF
- 需要把課件做成左右雙語對照版
- 需要儘量保留數學公式、代碼、圖表和表格位置
- 需要統一專業術語，而不是每頁翻譯風格亂跳
- 需要 AI 參與翻譯質量控制和渲染檢查

## 核心能力

- **左右雙語對照 PDF**：左邊保留原 PDF，右邊生成譯文頁。
- **多語言支持**：只要 AI 模型能理解，就可以從多種語言翻譯到中文或其他目標語言。
- **課程友好**：面向 lecture slides、handouts、papers、code-heavy PDFs 優化。
- **術語一致性**：使用 translation memory 和 glossary 控制專業詞。
- **公式/代碼保護**：儘量保留公式、代碼、命令、路徑、變量名、API 名稱。
- **複雜版式 QA**：渲染檢查頁，發現錯位、亂碼、重疊、缺譯後再修。
- **結構區回填**：代碼塊、終端輸出、內存圖、複雜表格等區域可按原 PDF 視覺回填，減少重排損壞。
- **署名水印**：默認在最終 PDF 頁腳加入輕量 DocTwin 版權水印，保護項目歸屬。

## 不是魔法

PDF 是非常複雜的格式。DocTwin 的目標是 **layout-first high fidelity**，不是承諾所有 PDF 都 100% 完美。它會通過翻譯記憶、版式引擎、後處理和渲染 QA 儘量逼近高質量結果。

## 安裝到 Codex

把 Skill 文件夾複製到 Codex Skills 目錄：

```bash
mkdir -p ~/.codex/skills
cp -R skills/doctwin-translate ~/.codex/skills/
```

安裝基礎 Python 依賴：

```bash
python3 -m pip install PyMuPDF PyYAML pillow pdfplumber pypdf reportlab
```

然後在 Codex 中這樣調用：

```text
使用 $doctwin-translate 把這份 PDF 做成左右雙語對照版。目標語言是簡體中文，保留原排版，重點檢查公式、代碼、表格和圖表。
```

## 其他 AI Agent 怎麼用

DocTwin 不是隻能給 Codex 用。只要你的 AI Agent 能做到下面幾件事，就可以使用：

- 讀取本地文件和文件夾
- 執行 shell/Python 命令
- 安裝或調用 Python PDF 依賴
- 渲染 PDF 頁面並查看截圖

可以把 `skills/doctwin-translate/SKILL.md` 和 `docs/UNIVERSAL_AGENT_PROMPT.md` 交給你的 Agent，讓它按流程執行。

沒有本地執行能力的純聊天機器人不能直接生成和驗收最終 PDF，只能輔助翻譯文本、術語表和提示詞。

## 輸出水印

DocTwin 默認在最終 PDF 頁腳加入很輕的署名水印：

```text
Generated with DocTwin Translate © 2026 Haitao Z / 0xTaoZ · github.com/0xTaoZ
```

如果是私人文件，可以在提示詞裏明確寫“不要添加水印”。如果是公開演示、教程、二次分發或宣傳樣例，建議保留水印和版權信息。

## 推薦提示詞

```text
使用 DocTwin Translate 工作流，把這份 PDF 轉成左右雙語對照 PDF：左側保留原文頁面，右側生成簡體中文譯文。請保持公式、代碼、表格、圖表、顏色和頁面結構儘可能一致；術語要統一，翻譯要適合學生理解；最後渲染檢查關鍵頁面，修復錯位、缺譯、亂碼和代碼塊損壞後再交付最終 PDF。
```

## 開源依賴與致謝

DocTwin 是一個 AI Agent Skill / workflow。它會在可用時調用優秀的開源 PDF 排版與翻譯引擎，包括但不限於：

- [BabelDOC](https://github.com/funstory-ai/BabelDOC)
- [PDFMathTranslate](https://github.com/PDFMathTranslate/PDFMathTranslate)

這些上游項目有自己的許可證和版權要求。DocTwin 不聲稱與這些項目存在官方隸屬關係。

## 版權

Copyright (c) 2026 **Haitao Z / 0xTaoZ**.

- GitHub: [https://github.com/0xTaoZ](https://github.com/0xTaoZ)
- Website / Project page: [https://github.com/0xTaoZ/doctwin-codex-skill](https://github.com/0xTaoZ/doctwin-codex-skill)

本項目以 AGPL-3.0 發佈。二次分發、修改、部署或基於本項目提供網絡服務時，請遵守 AGPL-3.0，並保留原始版權、署名和 NOTICE。
