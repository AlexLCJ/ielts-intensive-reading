---
name: ielts-intensive-reading
description: Use when the user asks to create an IELTS reading teaching/study guide, 精读讲义, or intensive reading document from an IELTS passage. Covers vocabulary bolding in original text, paragraph-by-paragraph analysis, synonym collections, long-sentence breakdowns, reading strategies, and practice exercises.
---

# IELTS Intensive Reading Teaching Document Generator

## When to Use

Invoke when the user:
- Provides an IELTS reading passage and asks for a 精读 (intensive reading) teaching document
- Wants a study guide / 讲义 for IELTS reading practice
- Asks to "teach" or "analyze" an IELTS passage in detail
- Mentions their current IELTS reading band score (e.g., "我现在阅读只有6分")

## Output Format

Generate a Word (.docx) document using python-docx. The document MUST contain these seven sections in order:

### 1. 文章概览与背景知识 (Overview & Background)
- A one-paragraph summary introducing the passage topic and structure
- A "文章结构速览" table with each paragraph's label, English topic name, and Chinese description
- "背景知识补给" with 3-4 bullet points of key background knowledge (historical context, technical terms, etc.)
- A tip box noting common obstacles for the student's current band level

### 2. 逐段精读分析 (Paragraph-by-Paragraph Analysis)
For EACH paragraph (A through final):

**a) Original text header:** `【X段原文】` in bold, colored header

**b) Original English text WITH vocabulary bolded:** 
This is the CRITICAL feature. Display the full original English text in italic. Every word/phrase that appears in the subsequent "核心词汇" (vocabulary) list MUST be rendered in BOLD within this text display. Use case-insensitive regex matching to find and bold each vocab word/phrase within the text. Sort vocab phrases by length (longest first) to avoid partial matches. Handle overlapping matches by keeping the longer one.

Implementation: Use python-docx's Run-level formatting. Split the paragraph into multiple runs — normal italic runs for non-vocab text, bold italic runs for vocab words.

**c) 核心词汇 (Core Vocabulary):**
A list of 10-20 key words/phrases from this paragraph. Each entry MUST include:
- English word/phrase (bold)
- Part of speech abbreviation
- Chinese meaning
- Usage note or etymology hint (in brackets, colored orange)

**d) 长难句拆解 (Long Sentence Breakdown):**
Select 1-2 complex sentences. For each:
- Show the original sentence in italic
- Provide a line-by-line breakdown showing subject, verb, object, modifiers
- Add a summary tip (⚠️ 考点提示) noting why this sentence matters for the exam

**e) 段落主旨与考点 (Main Idea & Exam Points):**
- A colored box with the paragraph's main idea
- A colored box with exam predictions (题型预判), possible question types, and common traps

### 3. 高频学术词汇总表 (High-Frequency Academic Vocabulary)
- A TABLE with 20 general academic words drawn from the passage (not just the paragraph-specific ones)
- Columns: Word, POS & Meaning, Detailed Explanation, Example from Text
- These should be words that appear across many IELTS passages, not just this one

### 4. 同义替换集中整理 (Synonym/Paraphrase Collection)
- IELTS reading is fundamentally about synonym recognition. This section is ESSENTIAL.
- Organized by paragraph (A through F)
- Each entry format: `original expression → synonym/paraphrase` with a brief Chinese note
- Include 4-10 synonym pairs per paragraph
- Cover both vocabulary-level and phrase-level paraphrases

### 5. 长难句专项突破 (Complex Sentence Pattern Training)
- Identify 3-5 recurring complex sentence patterns from the passage
- For each pattern:
  - Give it a name (e.g., "句型1：插入定语从句")
  - Show an example sentence
  - Provide a "破解方法" (decoding method) with step-by-step instructions
- Patterns to look for: embedded relative clauses (to which...), far from...rather... negation-correction, past participle post-modifiers, for-as-because, with-structures

### 6. 雅思阅读技巧点拨 (IELTS Reading Strategy Tips)
- 3-4 practical strategies contextualized to THIS passage
- Include: skimming/scanning approach, information location techniques (数字定位, 专有名词定位, 同义替换定位), TRUE/FALSE/NOT GIVEN judgment rules with concrete examples from the passage
- Show HOW to apply each strategy to the specific passage

### 7. 实战模拟练习 (Practice Exercises)
- 4 exercise types:
  a) 词汇填空 (vocabulary gap-fill): 6-10 sentences using the learned vocabulary in new contexts
  b) 同义替换匹配 (synonym matching): matching exercise
  c) 判断题 (TRUE/FALSE/NOT GIVEN): 6-8 statements based on the passage
  d) 段落主旨匹配 (heading matching): match headings to paragraphs
- Include a complete 参考答案 (answer key) section after the exercises

## Critical Rules

1. **Vocabulary bolding in original text is NON-NEGOTIABLE.** This is the defining feature. Every vocab word listed in 核心词汇 MUST appear bolded in the original text display above it.

2. **Define vocab lists BEFORE the text display call in code.** In the Python script, define `x_vocab = [...]` before calling the paragraph display function, since the display function needs the vocab list as input.

3. **Use Chinese for pedagogical content, English for linguistic examples.** Headings, explanations, strategies, exam tips should be in Chinese. The passage text, vocabulary words, and language examples should be in English.

4. **Target a student 0.5-1.0 band below the content difficulty.** If the passage is a typical academic IELTS passage (Band 7-8 level), write for a Band 6 student. Use simpler Chinese explanations, break down every complex structure, and never assume prior knowledge of academic vocabulary.

5. **Document structure is fixed.** Do not rearrange, skip, or add major sections. The seven-section structure above is mandatory.

6. **Total document should be comprehensive.** Aim for 15-25 pages. This is an intensive study resource, not a quick reference.

## python-docx Implementation Notes

- Use `from docx.shared import Pt, Cm, RGBColor` for styling
- Set East Asian font with `OxmlElement('w:rFonts')` and `qn('w:eastAsia')`
- For the vocabulary-bolding feature: create a helper function that takes (text, vocab_list) as input, uses `re.finditer()` with a pattern built from escaped vocab words (sorted longest-first), and splits the text into normal/bold runs
- Use `doc.styles['Normal']` to set base font and paragraph spacing
- Use `add_page_break()` between major sections
- Colored boxes can be simulated with styled paragraphs — no need for actual borders
- Tables should use `table.style = 'Light Grid Accent 1'`

## Anti-Patterns (Do NOT Do)

- Do NOT use numbered sentences (1., 2., 3.) for the original text — keep it as continuous prose
- Do NOT add sections like "Writing Model", "Grammar Tables", or "Full Translation" unless the user explicitly asks
- Do NOT skip the synonym/paraphrase section — this is what IELTS reading actually tests
- Do NOT display the original text without vocabulary bolding
- Do NOT ask the user clarifying questions during document generation — infer reasonable defaults and proceed
- Do NOT output the document content as chat text — always create the actual .docx file
