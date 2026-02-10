---
name: sci-translate
description: Translate Chinese scientific manuscripts into submission-ready English for SCI journals. Use when the user asks for Chinese-to-English manuscript translation, section-by-section polishing, terminology consistency checks, or reviewer-facing academic tone refinement.
---

# SCI Translate

## Overview

Use this skill to convert Chinese research writing into clear, accurate, journal-style English.
Prioritize technical fidelity first, then improve readability and academic tone.

## Workflow Decision Tree

- If the user provides full manuscript text, run full workflow from abstract to references.
- If the user provides one section only, run the same workflow on that section and keep global term consistency notes.
- If the user requests "quick translation", still output: translation + key ambiguity list.
- If domain terminology is unclear, ask for or infer a mini glossary before final polishing.

## Core Workflow

1. Classify section type (`Title`, `Abstract`, `Introduction`, `Methods`, `Results`, `Discussion`, `Conclusion`, `Caption`).
2. Extract key terms, symbols, units, abbreviations, and tense constraints.
3. Produce first-pass literal translation (do not optimize style yet).
4. Produce second-pass SCI style rewrite:
   - concise sentence structure
   - explicit logic connectors
   - discipline-appropriate verb tense
   - objective and non-promotional tone
5. Run third-pass consistency checks:
   - terminology consistency
   - number/unit/symbol consistency
   - claim-evidence alignment
6. Output both:
   - final English text
   - editable checklist of risky spots and optional alternatives

## Three-Stage Quality Gate

- `Stage A: Analysis` - identify terminology, section intent, and ambiguity before translating.
- `Stage B: Translation` - complete faithful translation first, then style optimization.
- `Stage C: Validation` - run a strict QA scan; if any hard-constraint risk exists, flag instead of hiding.

If `Stage C` fails, return translation plus explicit fix suggestions and confirmation questions.

## Output Format

Always return in this order:

1. `Final Translation`
2. `Terminology Table` (Chinese -> English -> note)
3. `Potential Issues` (ambiguity, missing subject, logic jumps, tense conflicts)
4. `Author Confirmation Needed` (if any)

## Section-Specific Rules

- `Title`: short, specific, avoid vague words like "study on" unless required by field norm.
- `Abstract`: use structured flow (background -> method -> result -> conclusion), keep quantitative findings.
- `Methods`: prioritize reproducibility wording; avoid rhetorical adjectives.
- `Results`: report observations first, interpretation later.
- `Discussion`: separate what data shows vs what authors infer.
- `Conclusion`: no new claims; focus on contribution and scope.
- `Figure/Table captions`: concise noun phrases; ensure symbol and unit consistency with main text.

## Hard Constraints

- Never invent data, references, or experimental settings.
- Never change numeric values, units, variable names, or equation meaning.
- Keep standard abbreviations stable after first definition.
- Preserve uncertainty language (e.g., "may", "likely", confidence intervals).
- If source Chinese is ambiguous, mark it explicitly instead of guessing silently.

## Non-Translatable Elements

Preserve these elements exactly unless the user explicitly requests normalization:

- equations and inline symbols
- variable names and parameter identifiers
- numbers, ranges, units, confidence intervals, p-values
- citation numbers/keys and reference order
- URLs, DOIs, model/version names, file names

Do not silently reformat decimal precision, minus signs, or unit spacing conventions.

## Terminology Decision Policy

For each key term, choose one mode and keep it stable across the manuscript:

- `Direct Translation`: clear one-to-one domain mapping exists.
- `Term + English Alias`: Chinese term needs international readability support.
- `Keep Original`: code names, standards, or symbols that should remain unchanged.

Always record the choice in `Terminology Table`.

## Default Editing Style

- Prefer active voice where natural, passive voice where process emphasis is needed.
- Keep sentences moderate in length; split overloaded clauses.
- Use field-common terminology over literal word-by-word mapping.
- Remove colloquial or marketing phrasing.
- Avoid over-strong claims unless evidence supports them.

## Reference-Style Adaptation Policy

When users ask to follow a specific paper style (e.g., Kim et al.), treat it as a reusable style reference, not a strict template.

- Priority order: target journal instructions > discipline conventions > reference paper style.
- Prefer `result/action first, reason second` when this improves clarity; do not distort the original causal meaning.
- Default to `one sentence, one primary claim`; allow denser compound sentences only when method detail requires it.
- Do not ban first person absolutely. Use first person only if needed for clarity and accepted by target journal style.
- Match claim strength to evidence:
  - limited evidence: `suggest`, `indicate`
  - consistent patterns: `show`, `demonstrate`
  - strong verification: `confirm`, `validate`
- Use transition markers only at real logic pivots; avoid repetitive connector stacking.
- Follow target journal formatting for numbers, units, percentages, dashes, and symbol spacing.
- Mimic structure and tone, but do not copy long lexical sequences from the reference paper.

## Anti-AI Voice Pass

Before final output, run one extra pass to reduce "AI-translated" style:

- reduce template fillers (e.g., repeated "Moreover", "It is worth noting that")
- vary sentence rhythm; avoid same-length sentence chains
- replace generic high-level words with field-standard collocations
- ensure each paragraph keeps a clear claim-evidence link
- keep cautious scientific tone, but avoid empty and repetitive hedging

If this pass changes wording significantly, re-check terminology and numeric consistency.

## References

- For reusable prompts, see `references/prompt-templates.md`.
- For final QA before submission, see `references/submission-checklist.md`.
