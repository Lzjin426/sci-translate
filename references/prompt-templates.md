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

## 4) 中文初稿英文化（参考文风迁移版）

Use this when the user wants the translation to align with a reference paper style (for example, Kim et al.) without rigid imitation.

```text
任务：将以下中文初稿改写为可投稿 SCI 的英文稿，并“参考 {{REFERENCE_STYLE}} 的写作风格”。

风格迁移原则（必须遵守）：
1) 优先级：目标期刊规范 > 学科惯例 > 参考文风。
2) 可借鉴句法与论证组织，不可照搬原文措辞。
3) 在不改变技术含义前提下，优先采用“结论/动作在前，原因在后”的英文表达。
4) 默认“一句一个主信息”；如 Methods 需高信息密度，可使用受控复合句。
5) 证据强度与动词匹配：suggest/indicate < show/demonstrate < confirm/validate。
6) 连接词仅用于逻辑转折点，避免每句机械添加 Furthermore/Moreover。
7) 不得改动任何数值、单位、符号、变量名、公式、引用编号、DOI/URL。

章节执行策略：
- Abstract：background -> method -> result -> conclusion，保留关键定量结果。
- Introduction：文献综述句式统一，组末总结不足，再引出“本研究为解决该限制...”。
- Methods：先做什么，再为什么，最后实现细节。
- Results：呈现 -> 观察 -> 解释 -> 意义，不写 “We can see...”，改为 “Fig. X shows...”。
- Discussion/Conclusion：区分“数据支持的事实”与“作者推断”；结论不引入新主张。

输出结构（固定）：
A. Final Translation
B. Terminology Table (中文 -> 英文 -> 决策说明)
C. Style Adaptation Notes（3-8条：说明你如何迁移参考文风）
D. Potential Issues（歧义、术语不确定、逻辑跳跃、时态冲突）
E. Author Confirmation Needed（如有）

原文：
{{CN_DRAFT}}

参考风格来源（可选）：
{{REFERENCE_EXCERPT_OR_PAPER_INFO}}
```
