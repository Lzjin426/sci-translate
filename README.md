# sci-translate

将中文科研文本翻译为可投稿 SCI/Top 期刊风格英文的技能说明。

## 适用场景

- 中文论文整篇翻译（从题目到图表说明）
- 分章节翻译与润色（Abstract/Methods/Results 等）
- 术语一致性检查（术语、缩写、变量、单位）
- 投稿前语言收紧（审稿友好、客观、克制语气）

## 核心能力

本技能遵循三阶段流程：

1. Analysis：先识别章节类型、关键术语、歧义和时态约束  
2. Translation：先忠实翻译，再进行 SCI 风格重写  
3. Validation：一致性与风险扫描，不确定项显式标注

默认输出顺序：

1. Final Translation  
2. Terminology Table（中文 -> 英文 -> 说明）  
3. Potential Issues  
4. Author Confirmation Needed（如有）

## 硬约束

- 不得编造数据、实验设置、参考文献或结论
- 不得改动数值、单位、变量名、公式语义
- DOI/URL/版本号/引用编号等不可翻译元素保持原样
- 源文有歧义时必须显式标注，不可静默猜测

## 使用方式

### 1) 整篇翻译

请直接提供全文中文草稿，并说明目标期刊（如有）。

### 2) 分段翻译

请提供章节名 + 文本，例如：`Methods` + 对应中文内容。

### 3) 英文终稿收紧

请提供现有英文稿，要求只做语言与结构优化，不改变技术含义。

## 目录结构

```text
sci-translate/
├── SKILL.md
└── references/
    ├── prompt-templates.md
    └── submission-checklist.md
```

## 参考文件

- `references/prompt-templates.md`：整篇翻译 / 分段翻译 / 终稿收紧模板
- `references/submission-checklist.md`：投稿前一致性与风险检查清单

