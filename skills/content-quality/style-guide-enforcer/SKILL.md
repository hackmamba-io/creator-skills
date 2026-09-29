---
name: style-guide-enforcer
description: >
  Enforce technical writing style standards on any draft and return inline corrections,
  principle explanations, and suggested rewrites. Use this skill whenever a technical
  writer asks to check, review, audit, or improve a piece of writing for style,
  consistency, clarity, tone, or grammar. Trigger on phrases like "check my draft,"
  "review this article," "is this well-written," "fix my tone," "clean up my writing,"
  "does this follow best practices," "give me feedback on this," "check this against
  style standards," "review this for consistency," or "edit this draft."
---

## Before you start: verify this skill is fully installed

This skill depends on its reference file `references/style-rules.md`. More than half of the skill lives in that file, and the skill cannot produce a correct result without it.

Before doing anything else, attempt to read `references/style-rules.md`. If you cannot read it, STOP. Do not attempt the task from memory or from general knowledge. Tell the user exactly this:

> This skill is not fully installed. Its reference file could not be read, so I can only produce a degraded result that would look normal but be missing most of the skill. Please reinstall the skill. In Claude Code or another agent, run `npx skills add hackmamba-io/creator-skills --skill style-guide-enforcer -g`. In the Claude app, go to Settings > Capabilities > Skills, delete this skill, and upload it again as a zip that contains both `SKILL.md` and the `references/` folder. Then run this skill again.

Only proceed past this point once the reference file has loaded successfully.

---

# Style Guide Enforcer

A skill for reviewing technical writing drafts against a consolidated set of
industry-standard style rules. Returns inline corrections, the principle behind
each flag, and suggested rewrites.

---

## When to activate this skill

Use this skill when someone:

- Pastes a draft and asks for feedback, a review, or a "check"
- Asks whether their writing is clear, consistent, or follows best practices
- Wants their tone corrected or their draft cleaned up
- Asks if a piece is ready to publish or submit
- Requests a line edit or copy edit on technical content
- Pastes a paragraph and asks "does this sound right?" or "is this too formal?"
- Asks you to compare their draft against a style guide

## When NOT to activate this skill

Do not use this skill when someone:

- Asks a general question about writing principles without providing a draft
- Wants structural or strategic feedback on content architecture
- Asks you to write something from scratch
- Submits a draft but explicitly says they only want feedback on something unrelated to style
- Pastes code only, with no prose to review

---

## What this skill does

This skill draws on four major style guides: the Google Developer Documentation
Style Guide, the Microsoft Writing Style Guide, the Chicago Manual of Style,
and the Apple Style Guide. For every flagged issue, it quotes the exact sentence
or phrase, names the principle being violated, explains why it matters to the
reader, and offers a specific rewrite.

---

## Input handling

Writers may provide any of the following. Handle each case without asking for
more unless the draft is under 80 words.

**Draft only**
Proceed using the consolidated base rules. Note at the top of the review that no
company-specific overrides were provided.

**Draft plus company style rules**
The writer pastes their organization's specific conventions alongside the draft.
Company rules take precedence over the base layer. Note any conflicts between
company rules and the base guides so the writer understands the tradeoff.
For example: "Your company uses title case for headings, which differs from the
Google and Microsoft recommendation of sentence case. Both are internally valid.
What matters is consistent application throughout."

**Draft plus audience context**
The writer describes who they are writing for. Factor this into the review.
A piece for senior engineers needs different calibration than one for new users.
Do not apply feedback mechanically regardless of audience.

If company overrides conflict with base rules, apply the company override and note
the conflict once. Do not repeat it for every flagged instance.

---

## How to run the review

### Step 1: Read the style rules reference

Before starting, read `references/style-rules.md` in full. Use it as the working
reference throughout the review. The reference is the source of truth for this skill.

### Step 2: Understand the writer's context

Check whether company overrides or audience context were provided. If not, proceed
with base rules and note it briefly in the review header.

### Step 3: Scan the draft systematically

Work through the draft section by section, checking against each rule category:

1. Voice and Tone
2. Grammar and Sentence Structure
3. Word Choice
4. Punctuation
5. Headings and Structure
6. Lists (if present)
7. Code and Technical Elements (if present)
8. Inclusive and Global Language

Prioritize violations that affect clarity, reader trust, and consistency. For a
typical article-length draft, 5 to 12 flags is the right range. More than 15
buries what actually matters.

### Step 4: Calibrate to writer level

Writer level affects how you deliver the review, not what you flag.

- **Aspiring or beginner writers**: Explain the principle behind each flag in plain
  terms. Show the fix and explain why it works.
- **Mid-level writers**: Assume familiarity with basics. Focus on nuance, pattern
  recognition, and reader experience.
- **Senior writers**: Flag edge cases and subjective calls. Offer alternative
  framings where relevant.

If writer level is not known, default to mid-level.

### Step 5: Format and deliver the review

Use the output format below. If there are no issues in a category, note it briefly
rather than omitting the section.

---

## Output format

```
## Style Review

**Draft:** [Title or opening line, for reference]
**Base standards:** Google Developer Docs, Microsoft Writing Style Guide,
Chicago Manual of Style, Apple Style Guide
**Company overrides:** [List them, or "None provided"]
**Writer level assumed:** [If known, state it. If unknown: "Mid-level (default)"]

---

### Summary

[2 to 3 sentences on the overall state of the draft. What is working? What
pattern appears most often? Be specific. "The voice is inconsistent" is vague.
"Most instructions use second person, but the setup section shifts into third
person throughout" is specific.]

---

### Flagged Issues

**Issue [N]: [Short label, e.g., "Passive voice" or "Undefined acronym"]**

> [Exact quote from the draft]

**What is wrong:** [Plain explanation of the violation]
**Which guide:** [Google / Microsoft / Chicago / Apple / All four]
**Why it matters:** [1 to 2 sentences on the reader impact]
**Suggested rewrite:**
> [Rewritten version of the flagged sentence or passage]

---

[Repeat for each issue]

---

### What is working

[2 to 4 specific things the writer did well. Be genuine. Do not manufacture
praise. If the code examples are clean and runnable, say so. If the structure
is logical, say so. Vague compliments are not useful here.]

### One thing to focus on next

[The single most impactful improvement this writer can make, based on the
patterns in this draft. Frame it as a habit to build rather than a mistake
to avoid.]
```

---

## Tone of the review

The review should come from a sharp, experienced editor who respects the writer's
intelligence and gives them something actionable.

- Name the issue clearly. Do not soften it until it becomes meaningless.
- Give the fix. Do not make the writer guess what the corrected version looks like.
- Explain why it matters. Reader impact is more persuasive than rule citation.
- End with something genuine that is working. Every draft has something.
- Do not give feedback that could apply to any draft ever written.

---

## Edge cases

**Very short drafts (under 80 words)**
Run the review but note that patterns are harder to assess from short samples.
Offer to review a longer section if available.

**Near-perfect drafts**
Flag the 1 to 3 highest-impact improvements even in strong drafts. If a draft
is genuinely excellent, say so and explain what makes it work. Do not manufacture
flags to appear thorough.

**Non-native English writers**
Flag clarity issues that affect comprehension. Do not penalize stylistic patterns
that do not confuse the reader. Prioritize reader impact over grammatical
perfectionism.

**Drafts with code samples**
Check code samples against Section 7 of the style rules. Missing language labels
and unexplained code blocks are the most common violations in technical drafts,
and they carry more weight with developer audiences than most prose-level issues.

**Company overrides that conflict with base rules**
Apply the company override. Note the conflict once so the writer understands the
tradeoff. Do not repeat it for every instance.
