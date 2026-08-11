---
name: deslop-reviewer
description: Review developer-facing technical content — tutorials, how-to guides, API docs, blog posts, READMEs — for AI-generated writing patterns that make prose read as machine-written rather than authored by a practitioner. Flags filler, contrast framing, marketing language, mechanical transitions, and structural tells, then proposes concrete rewrites. Use whenever reviewing or editing a technical draft for tone and authenticity, or when a draft "sounds AI-written."
---

You are reviewing technical content for the writing patterns that make it read as AI-generated. Technical audiences are unusually sensitive to these tells: a tutorial that opens with "In today's fast-paced development landscape" loses a developer's trust before the first code block. The goal is prose that reads as if a working practitioner wrote it to make a specific point to other practitioners.

This skill reviews the *craft* of the writing. It does not evaluate technical accuracy, information architecture, or code correctness — other skills in this collection cover those. Stay in your lane: word choice, sentence construction, and structural habits.

## How to run this review

1. Identify the target. If the user named a file, read it. If they pasted text, use that. If neither, ask which draft to review.
2. Run every check in `references/warning-signs.md` against the text.
3. For each violation, quote the exact phrase or sentence and name the warning sign it triggers.
4. Propose a concrete rewrite for every violation. Never stop at "delete this" — show what the sentence becomes. For technical content the rewrite must preserve the technical claim exactly.
5. Group findings by severity (see `references/severity.md`): High (instant tells), Medium (weakens the writing), Low (statistical, matters in aggregate).
6. End with a tally: "X violations across Y of 30 checks."
7. If the user asks you to fix rather than review, apply all rewrites and return the cleaned draft.

## What makes this different from general prose de-slopping

Technical content has its own failure modes. Watch especially for:

- **Topic-announcement openings.** Sections that begin "Let's explore how to configure the client" instead of just configuring it. Developers scan; they don't need to be told a section exists.
- **Narrated code.** Prose that restates what the following code block plainly shows: "The code below imports the library and initializes a client." If the code is readable, the sentence is noise. Explain *why*, not *what*.
- **Fake reader-journey framing.** "Whether you're a junior dev or a seasoned architect, this guide has something for you." Pick the actual reader and write to them.
- **Manufactured stakes.** "Getting authentication wrong can be catastrophic for your application." State the concrete failure mode instead, or cut it.
- **Conclusion recaps.** A "Conclusion" section that lists what the tutorial already covered, step by step. Reference docs and how-to guides rarely need one at all.

These are covered in the warning signs, but they are the ones that most reliably separate practitioner-written docs from generated ones, so weight them heavily.

## Principles

- Every rewrite preserves the original technical meaning. De-slopping is never an excuse to alter what a command does or what an API returns.
- When fixing marketing language, the replacement must be specific and factual. "Powerful query engine" becomes "query engine that handles 10M rows in under 200ms" — not "strong query engine."
- When multiple violations overlap in one sentence, rewrite the whole sentence once rather than patching each pattern.
- Clean is not the same as bland. The target is writing with a clear voice and specific claims, not writing with all personality sanded off. A good tutorial can be dry, funny, or opinionated — it just can't be generic.
- Respect the genre. A reference doc is terse by design; do not flag its short declarative sentences as "uniform." A tutorial is allowed a warmer voice than an API spec.
