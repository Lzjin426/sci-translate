# Prompt Templates

## 1) Full Manuscript Translation

Use this when the user provides a full Chinese paper draft.

```text
任务：将以下中文学术论文翻译为可投稿 SCI 的英文稿。

要求：
1) 按三阶段执行：Analysis -> Translation -> Validation。
2) 先保证技术准确，再进行学术风格润色。
3) 不改动数据、单位、符号、公式含义与参考文献信息。
4) 对不可翻译元素（公式、变量、DOI、URL、版本号）保持原样。
5) 保持术语一致，首次出现缩写时给出全称。
6) 输出结构必须包含：
   A. Final Translation
   B. Terminology Table (中文 -> 英文 -> 说明)
   C. Potential Issues
   D. Author Confirmation Needed

原文如下：
{{MANUSCRIPT}}
```

## 2) Section-By-Section Polishing

Use this when the user wants iterative translation.

```text
任务：翻译并润色以下“{{SECTION_NAME}}”部分，使其符合 SCI 英文论文风格。

输出：
1) 最终英文文本
2) 术语表（仅列本段新术语）
3) 三条以内的改写说明（为何这样改）
4) 一条“本段最大风险提示”（如歧义、时态或术语不确定）

原文：
{{SECTION_TEXT}}
```

## 3) Final Language Tightening

Use this after a full draft already exists in English.

```text
任务：对以下英文稿做“投稿前语言收紧”，不改变技术含义。

重点：
- 减少冗长句
- 提升逻辑衔接
- 统一术语与时态
- 保持审稿友好、克制、客观语气
- 执行 Anti-AI Voice Pass（去模板套话、打散句长节奏、替换泛化搭配）

输出：
1) Polished Version
2) High-impact Edits (最多10条)
3) Remaining Risks
4) Consistency Verdict (`pass` or `needs-author-review`)

英文稿：
{{EN_DRAFT}}
```
