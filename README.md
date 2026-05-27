# IELTS Intensive Reading Skill

> 雅思阅读精读讲义生成器 — Claude Cowork Skill

An intelligent skill for Claude that automatically generates comprehensive, beautifully formatted IELTS intensive reading study guides (精读讲义) from any IELTS reading passage. One-click generation of professional Word documents with vocabulary bolding, paragraph analysis, synonym collections, and practice exercises.

## What It Does

Give Claude any IELTS reading passage, tell it your current band score, and it produces a complete **15-25 page Word document** containing:

| Section | Content |
|---|---|
| 文章概览与背景知识 | Passage overview, structure map, background knowledge, learning tips |
| 逐段精读分析 | Paragraph-by-paragraph breakdown with **bolded vocabulary in original text**, word lists, long-sentence analysis, exam point predictions |
| 高频学术词汇总表 | 20 general academic words drawn from the passage in a formatted table |
| 同义替换集中整理 | Synonym/paraphrase pairs organized by paragraph — the core IELTS reading skill |
| 长难句专项突破 | 5 recurring complex sentence patterns with decoding methods |
| 雅思阅读技巧点拨 | Practical strategies contextualized to the passage (scanning, T/F/NG rules, etc.) |
| 实战模拟练习 | Vocabulary gap-fills, synonym matching, T/F/NG questions, heading matching — with answer key |

## Key Feature: Vocabulary Bolding

Every core vocabulary word is **bolded directly within the original English text**, so you can see exactly where each word appears in context while reading:

> *This book will provide a detailed **examination** of the Little Ice Age and other climatic shifts, but, before I **embark on** that, let me provide a historical context.*

## Installation

### Prerequisites
- [Claude desktop app](https://claude.ai/download) with Cowork mode
- python-docx (automatically used by the skill — no manual setup needed)

### Install the Skill

1. Clone this repository or download the files
2. In Claude Cowork, use the `/save-skill` command to register the skill, or simply open the `SKILL.md` file and Claude will detect it automatically
3. The skill activates whenever you mention "精读", "IELTS reading", "讲义", or ask for an IELTS passage analysis

### Quick Start (for Skill Developers)

If you're packaging this as a `.skill` file for Cowork:

```bash
# Zip the directory with .skill extension
zip -r ielts-intensive-reading.skill ielts-intensive-reading/
```

Then drag `ielts-intensive-reading.skill` into Claude Cowork to install.

## Usage

### Basic Usage

Just paste an IELTS passage and ask Claude to create a study guide:

```
请帮我精读这篇雅思文章，我目前阅读在6分左右。

[Paste your IELTS passage here]
```

### With Specific Requirements

```
这篇文章是剑桥雅思17 Test 2 Passage 3，我阅读6分，帮我做一份精读讲义，保存为Word文档。
```

### Example Output

Given an IELTS passage, Claude will:
1. Analyze the passage structure and background
2. Generate the complete 7-section document
3. Save it as a `.docx` file to your workspace
4. Bold every vocabulary word within the displayed original text

[View example output](computer:///Users/changjunli/Desktop/Language/剑雅精读/The Little Ice Age 精读讲义.docx)

## Skill Structure

```
ielts-intensive-reading/
├── SKILL.md          # The skill definition (Claude's instruction set)
└── README.md         # This file
```

The `SKILL.md` contains:
- **When to Use** — precise triggers for skill invocation
- **Output Format** — mandatory 7-section document structure
- **Critical Rules** — non-negotiable requirements (vocab bolding, language mixing, etc.)
- **Implementation Notes** — python-docx technical guidance
- **Anti-Patterns** — what NOT to do

## Tips for Best Results

1. **Provide the full passage text** — including paragraph labels (A, B, C...) if present
2. **Mention your current band score** — the skill adjusts explanatory depth accordingly (Band 6 gets simpler Chinese, more detailed breakdowns)
3. **Specify output location** — tell Claude where to save the .docx file
4. **Review and iterate** — you can ask Claude to fix specific sections or add more detail

## License

MIT
