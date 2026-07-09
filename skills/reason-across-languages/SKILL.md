---
name: reason-across-languages
description: Enhance complex reasoning and professional writing across Chinese, English, and mixed-language prompts by privately clarifying intent in precise English when useful, selecting appropriate international concepts or frameworks, and answering in the user's requested or contextually appropriate language. Use for business strategy, research synthesis, technical architecture, academic analysis, decision analysis, professional writing, bilingual drafting, high-quality Chinese output from English-heavy knowledge domains, or requests mentioning cross-language thinking, English-first reasoning, terminology alignment, or Chinese/English output control.
---

# Reason Across Languages

## Core Rule

Improve answer quality by using the strongest available conceptual language for reasoning, while making the final answer match the user's requested output language and task context.

Do not expose private scratch work, intermediate translations, hidden framework selection, or step-by-step internal reasoning. When explanation is useful, provide a concise, user-facing rationale instead.

## Workflow

1. Determine the target output language before reasoning.
2. Privately clarify the user's intent, domain, constraints, audience, and success criteria.
3. When useful, normalize ambiguous Chinese or mixed-language input into precise English concepts, terminology, and problem structure.
4. Select only the frameworks that materially improve the answer. Avoid name-dropping frameworks that do not affect the result.
5. Reason through options, trade-offs, assumptions, and risks.
6. Produce the final answer directly in the target language with clear structure, natural phrasing, and appropriate technical terms.

## Output Language Routing

Explicit user instructions override all defaults.

- If the user asks for English, all-English, "answer in English", "write this in English", "全英文", or a deliverable whose artifact language is English, output in English. Do not add a Chinese finalization step.
- If the user asks for Chinese, output in Chinese.
- If the user asks for bilingual output, provide both languages in the requested order or, if unspecified, use Chinese first and English second for Chinese-dominant prompts.
- If the user asks for translation, rewriting, polishing, localization, or a document in a specific language, output the artifact in that target language.
- If the user asks to preserve the original language, preserve it.

When no output language is specified:

- Chinese-dominant input: answer in Chinese.
- English-dominant input: answer in English.
- Mixed Chinese-English input: answer in the dominant instruction language, while preserving quoted text, code, names, and domain terms.
- If the user writes Chinese instructions for an English artifact, make the artifact English. Use Chinese only for brief surrounding notes when helpful.

## Terminology

- Preserve canonical English terms when translation would reduce precision, such as PMF, LTV, CAC, moat, idempotency, latency, Game Theory, CAP, SLO, or Zero Trust.
- For Chinese output, use `中文（English）` on first mention when the audience may benefit from both forms, then use the clearer term thereafter.
- Do not translate code, commands, API names, filenames, product names, legal names, citations, or quoted source text unless the user explicitly asks.
- Avoid ornamental jargon. Use professional terms only when they carry real explanatory value.

## Framework Selection

Use domain frameworks as tools, not decorations.

- Business strategy: competitive moat, network effects, switching costs, Porter's Five Forces, value chain, unit economics, GTM, CAC/LTV.
- Product and growth: PMF, Jobs To Be Done, user segmentation, activation/retention loops, funnel analysis, growth loops.
- Technical architecture: requirements, constraints, trade-offs, failure modes, observability, SLOs, idempotency, scalability, security boundaries.
- Academic or research tasks: problem framing, literature map, hypothesis, methodology, evidence quality, limitations.
- Decision analysis: options, criteria, trade-offs, reversibility, expected value, risk matrix.
- Writing and communication: audience, purpose, tone, narrative arc, information hierarchy, call to action.
- Logic and debate: premises, definitions, hidden assumptions, counterexamples, burden of proof.

## Freshness And Evidence

For facts that may have changed, such as laws, prices, product capabilities, market data, public roles, standards, or recent events, use available browsing or source-checking tools according to the host environment's rules before making current claims.

When sources are used, cite or link them as required by the environment. When no source is available, distinguish inference from verified fact.

## Clarification Policy

Ask a brief clarifying question only when missing information would materially change the answer or create risk. Otherwise, state reasonable assumptions and proceed.

For high-stakes domains such as legal, medical, financial, safety, compliance, or hiring decisions, be explicit about uncertainty, scope, and the need for professional review where appropriate.

## Final Answer Style

- Start with the answer, recommendation, or key judgment.
- Use headings, bullets, tables, or examples only when they improve scanability.
- For Chinese output, write natural professional Chinese rather than translationese.
- For English output, do not include Chinese summaries unless requested.
- Do not mention that the response was translated, aligned, routed, or reasoned in another language unless the user asks about process.
- Preserve the user's desired tone, such as concise, executive, academic, persuasive, casual, or technical.

## Examples

User: `帮我看看这个新项目怎么建立商业壁垒。`

Behavior: Answer in Chinese by default. Use relevant strategy concepts such as moat, network effects, switching costs, and data advantage only where useful.

User: `Answer in English. 帮我分析这个 AI SaaS 的 GTM 策略。`

Behavior: Answer entirely in English. Do not add a Chinese version.

User: `帮我写一封英文邮件，语气礼貌但坚定。`

Behavior: Produce the email in English. Add Chinese notes only if necessary and brief.

User: `中英双语解释一下 idempotency 为什么重要。`

Behavior: Provide both Chinese and English explanations, keeping the technical term `idempotency`.

User: `用中文解释这段英文论文摘要。`

Behavior: Explain in Chinese, preserving key English terms where they are standard or hard to translate precisely.

## Avoid

- Forcing Chinese output when the user explicitly requested English.
- Showing intermediate translations or hidden reasoning traces.
- Adding framework labels without using them to improve the answer.
- Translating technical identifiers, commands, code, or proper nouns incorrectly.
- Treating Chinese instruction language as the artifact language when the requested artifact is English.
