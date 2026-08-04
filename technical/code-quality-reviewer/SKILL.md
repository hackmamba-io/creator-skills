---
name: code-quality-reviewer
description: >
  Review code samples in technical articles, tutorials, and documentation for
  quality, correctness, runnability, security hygiene, and code-prose consistency.
  Use this skill when a technical writer, developer, or editor wants to evaluate
  whether the code in their content is production-appropriate, teachable, and
  accurate. Trigger on phrases like "review the code in my article," "is this
  code correct," "check my code samples," "is this code production-ready,"
  "will this code work for readers," "review my tutorial code," "check my
  snippets," or any request to evaluate code quality in a content context.
  Also trigger when someone pastes an article or tutorial and asks for a general
  review, since code quality is a distinct diagnostic that prose-level feedback
  often misses entirely.
---

# Code Quality Reviewer

A skill for evaluating code samples in technical content. Covers universal
quality rules across all languages and specific conventions for Python,
JavaScript and TypeScript, Bash, SQL, YAML and Dockerfiles, and Go. Reviews
both the code itself and the prose that surrounds it, with heavier weight
on the code.

---

## When to activate this skill

Use this skill when someone:

- Submits an article, tutorial, or guide with code samples and asks for a review
- Asks whether their code is correct, complete, or appropriate for a technical audience
- Wants to know if their code snippets will work when readers copy and run them
- Asks for feedback on code in a documentation or content context specifically
- Submits code samples that appear AI-generated or adapted from personal projects
  and wants them validated for a public audience
- Asks whether their code follows language conventions or best practices
- Wants a readiness verdict on their content before publication

## When NOT to activate this skill

Do not use this skill when someone:

- Wants help debugging code in their own project with no documentation context
- Asks for a code review in a pure engineering context with no mention of
  content, articles, tutorials, or documentation
- Only has prose in their draft with no code blocks
- Asks for style or grammar feedback on prose only
- Wants architecture advice on a system they are building, not writing about

---

## What this skill does

Writers who code and developers who write share a common blind spot: code that
works on their machine, in their environment, with their dependencies, often
fails when a reader tries to run it cold. AI-generated code compounds this
because it is frequently plausible-looking, syntactically correct, and
subtly wrong in ways that are hard to spot without running it.

This skill reviews code samples the way a senior engineer with a documentation
background would: checking not just whether the code is correct, but whether
it is complete enough for a reader to succeed with it, honest about its
limitations, and consistent with what the surrounding prose claims it does.

The output flags issues inline with explanations and rewrites, then delivers
a final readiness verdict the writer can act on before publication.

---

## Language coverage

**Tier 1 (full review, universal plus language-specific conventions):**
Python, JavaScript, TypeScript, Bash, SQL, YAML, Dockerfiles, Go

**Tier 2 (universal rules only):**
All other languages. The universal rules in Section 1 of the reference apply
regardless of language. Flag what can be assessed without language-specific
knowledge and note that the review covers universal standards only.

---

## Input handling

Writers may provide any of the following. Handle each without asking for more
unless there are no code blocks at all.

**Full article or tutorial**
Review all code blocks found in the article. Evaluate both the code itself and
how the surrounding prose integrates with it. Apply the code-prose integration
rules from Section 8 of the reference.

**Code blocks only, no surrounding prose**
Review the code against universal and language-specific rules. Note in the
review that prose integration could not be assessed and offer to review the
full article if available.

**Single code block**
Run the full universal and language-specific review on the block. If context
is missing (no indication of what the article is about, who it is for, or
where this block appears), note the gaps that context would have resolved
and assess what can be assessed.

**Article with stated audience or publication target**
Factor the audience into the review. Code for a beginner tutorial needs
more explanation, more descriptive naming, and simpler error handling than
code in an advanced reference guide. Code for a developer-facing publication
should follow production conventions more strictly than code in a conceptual
explainer.

---

## How to run the review

### Step 1: Read the code rules reference

Before starting, read `references/code-rules.md` in full. The Common Violations
Cheat Sheet in Section 9 is the fastest way to orient before scanning the draft.
Do not rely on general knowledge of best practices. Use the reference.

### Step 2: Identify all code blocks and their languages

Locate every code block in the submission. Note the language for each.
If a block has no language label, that is itself a flag. Infer the language
from context and note what you inferred.

### Step 3: Run the universal review on every block

For each code block, check against Section 1 of the reference:
- Completeness: are imports present, are prerequisites stated, is the code
  scoped appropriately if incomplete?
- Runnability: is it real code or pseudocode, are placeholders correctly
  formatted, are dependencies version-pinned where relevant?
- Error handling: are failure cases handled, especially for network calls,
  file operations, and authentication?
- Security hygiene: are credentials hardcoded, is SQL parameterized, are
  sensitive values handled safely?
- Naming and clarity: are variable names descriptive, do they match the prose,
  are magic numbers explained?
- Comments: do they explain why rather than what, are they consistent with
  the prose?
- Formatting: is the language label present, are input and output separated?

### Step 4: Run the language-specific review

For Tier 1 languages, apply the relevant section from the reference after
the universal review. Language-specific violations are often the most
surprising to writers who learned the language informally or rely on AI
to generate examples.

For Tier 2 languages, note that the review covers universal standards only
and does not assess language idioms.

### Step 5: Review code-prose integration

Using Section 8 of the reference, evaluate whether the prose before and
after each code block does its job. Specifically:
- Does the prose before the block explain what the code does, when to use it,
  and what the reader needs before running it?
- Does the prose after the block address output, side effects, and next steps?
- Are all terms and names in the prose consistent with what appears in the code?

Weight this section less heavily than the code review itself. Flag the highest
impact integration issues, not every prose-level imperfection.

### Step 6: Determine the readiness verdict

After completing all flags, assess the overall readiness of the code for
publication using three levels:

**Ready with minor fixes**
The code is fundamentally sound. Issues are cosmetic or low-risk (missing
language label, variable naming, minor prose inconsistency). The writer can
publish after addressing the flagged items.

**Needs revision before publication**
The code has issues that would cause real problems for readers (missing imports,
no error handling on network calls, hardcoded credentials, placeholder format
inconsistency). These must be fixed before the article goes live.

**Not publication-ready**
The code has fundamental problems (does not run, teaches insecure patterns
without warning, contains incorrect logic, major completeness gaps). Significant
revision is required.

---

## Output format

```
## Code Quality Review

**Article / content:** [Title or description]
**Languages found:** [List all code block languages, e.g., "Python (3 blocks),
Bash (1 block), YAML (1 block)"]
**Prose integration reviewed:** [Yes / Code blocks only]
**Readiness verdict:** [Ready with minor fixes / Needs revision / Not publication-ready]

---

### Summary

[3 to 4 sentences on the overall state of the code. What is the most common
category of issue? Are the problems concentrated in one block or distributed
across the article? Is this AI-generated code that passed a surface check
but has runnability gaps, or is it personal code that works in one environment
but makes too many assumptions? Be specific about the pattern, not just
the presence of issues.]

---

### Flagged Issues

**Issue [N]: [Short label] -- [Block reference, e.g., "Block 2, Python"]**

> [Exact code excerpt showing the problem]

**Category:** [Completeness / Runnability / Error Handling / Security /
Naming / Comments / Formatting / Code-Prose Integration / Language-Specific]
**What is wrong:** [Plain explanation of the problem]
**Reader impact:** [What happens when a reader copies and runs this as-is]
**Suggested fix:**
```[language]
[Corrected version of the flagged code]
```
**Note:** [Any additional context the writer needs, e.g., "This is a PEP 8
requirement" or "This is a security concern, not just a style one"]

---

[Repeat for each issue]

---

### What is working

[2 to 4 specific things the code does well. If the error handling is thorough,
say so. If the placeholder format is consistent throughout, say so. If the
code-prose integration is clear and the variables match the prose, say so.
Do not manufacture praise.]

### Before you publish

[A short, prioritized list of the fixes that must happen before this goes live,
separate from the nice-to-haves. Frame it as a checklist the writer can action
immediately. Maximum 5 items. If the verdict is "Ready with minor fixes," this
section can be brief.]
```

---

## Tone of the review

Code feedback in a content context lands differently than a pull request review.
Writers who are not primarily engineers can be defensive about code feedback
in a way that developers are not. The goal is to help them ship content that
does not fail their readers, not to audit their engineering skills.

- Lead with the reader impact, not the rule. "A reader who runs this will hit
  an authentication error before they see any output" lands better than
  "you violated error handling best practices."
- Be specific. Vague feedback ("this code needs improvement") leaves the writer
  with no path forward.
- Separate must-fix from nice-to-have. Not every violation has the same urgency.
  A writer preparing to publish needs to know which issues will hurt readers and
  which are polish.
- If the code appears to be AI-generated, name it directly and without judgment.
  AI-generated code has a recognizable failure mode: it looks complete, passes
  a surface read, but makes assumptions about the environment that cause readers
  to fail silently. Flag that pattern when you see it.

---

## Edge cases

**All code blocks are intentionally incomplete (e.g., a conceptual article
that uses code to illustrate a point rather than teach a workflow)**
Apply the universal rules but lower the bar for completeness and runnability.
A code block that exists to illustrate a concept does not need to be runnable.
Note this in the review and scope the flags accordingly. Flag any block that
looks like it is meant to be runnable but is not.

**Mixed language articles**
Review each block against the appropriate tier. Note in the summary which
blocks received a full Tier 1 review and which received universal rules only.

**Code that is correct but teaches bad habits**
Flag it. The question for tutorial code is not just "does this work" but
"should a reader learn this pattern." A `SELECT *` query works. It also
teaches a habit that causes real problems in production. That distinction
matters in a content context.

**Security issues in demo code**
Never leave a security issue unflagged just because the article frames it as
a demo. State the issue, explain why it matters, and provide the safer pattern.
If the article is specifically demonstrating a vulnerability (e.g., a security
tutorial showing what not to do), confirm that the article makes that framing
explicit and flag it if it does not.

**AI-generated code**
Do not refuse to review it or treat it differently in principle. Review it
against the same standards. AI-generated code tends to cluster around specific
failure modes: missing error handling, plausible-but-wrong placeholder formats,
version assumptions that are silently stale, and variable names that are generic
rather than domain-appropriate. Look for those patterns specifically and flag
them when present.
