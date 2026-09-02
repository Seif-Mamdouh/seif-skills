---
name: plan
description: Write clear, controlled technical documentation (CTE, ASD-STE100, Google Developer Documentation Style Guide, Diátaxis). Use when producing plans, skills, docs, READMEs, API references, procedures, or any technical writing that must be precise, unambiguous, and easy to translate.
---

# Controlled Technical Writing

Write documentation that is clear, precise, unambiguous, and easy to translate. Prefer correctness over style when they conflict.

Assume readers are not native English speakers and may use machine translation or AI tools.

## Language

- Use one word for one concept. Do not use synonyms for technical terms.
- Define each technical term once. Use that term consistently.
- Prefer common English words. Avoid idioms, metaphors, slang, and humor.
- Use concrete verbs. Write "Start the service." Do not write "Perform service startup."
- Write in active voice and present tense unless another tense is required.
- Keep sentences under 20 words. Express one idea per sentence.
- Avoid unnecessary subordinate clauses, double negatives, and ambiguous pronouns.
- For agent steering documents (skills, plans, agents.md), use absolutes and strict processes carefully. Agents are likely to follow your guidance to the tee, for better or worse. 
- Always reflect on your language after writing.

## Procedures

- Use numbered steps. Begin each step with an imperative verb.
- Describe one action per step.
- State conditions before actions. Example: "If the connection fails, restart the service."
- State expected results after actions when helpful.

## Structure and formatting

- Use headings that state the topic.
- Use numbered lists for procedures. Use bullet lists only for unordered information.
- Use tables for comparisons.
- Use code blocks only for code, commands, configuration, or structured output.
- Separate explanatory text from procedural steps.
- Use paragraphs to present and develop one composite main idea clearly. Smell: one sentence per paragraph indicates you are not forming cohesive composite ideas. This does not apply to lists.

## Accuracy and examples

- State assumptions, required inputs, limitations, and constraints.
- Define abbreviations on first use.
- Do not omit required steps.
- Use realistic examples (real commands, paths, API requests). Avoid placeholders unless necessary.

## Before finishing

Verify: one idea per sentence; one action per step; active voice; consistent terms; no idioms; conditions before actions; realistic examples; complete and concise.
