# The four modes

Definitions, recognition tells, boundaries, and a skeleton template for each Diátaxis mode. Read the relevant section fully before scaffolding.

---

## Deciding the mode

Ask two questions:

1. **Is the reader acting or acquiring knowledge?** Acting → tutorial or how-to. Acquiring knowledge → reference or explanation.
2. **Is this for study or for work?** Study (the reader is learning, not yet trying to get a real job done) → tutorial or explanation. Work (the reader has a real task in front of them) → how-to or reference.

Cross the two answers:

- act + study → **tutorial**
- act + work → **how-to guide**
- knowledge + work → **reference**
- knowledge + study → **explanation**

If the request is ambiguous, the fastest disambiguating question is usually: **"Is the reader trying to learn the system, or do they already know it and just need to get something done / look something up?"** Learning → tutorial or explanation. Already competent → how-to or reference.

A common trap: the user says "write a tutorial" but describes a task for someone who already knows the product. That's a how-to guide. Classify by reader need, not by the word the user used.

---

## Tutorial

**Reader need:** "Take me through a learning experience so I gain skills and confidence." The reader is a beginner. Success is measured by what they learn, not by what they produce.

**Tells:** first time using the product; needs hand-holding; the outcome matters less than the understanding gained; the writer is responsible for the reader's success at every step.

**Boundaries — keep out:**
- Full explanation of why things work. One line max, then link to an explanation page.
- Alternatives and options. A tutorial is a single guaranteed-to-work path. No "you could also…".
- Exhaustive reference detail. Link to reference for the full parameter list.
- Anything that can fail unpredictably. Every step must work for every reader.

**Skeleton:**

```
# [Verb-first title: "Build your first …", "Get started with …"]

## What you'll build
One or two sentences on the concrete thing the reader will have made by the end. Show the end result if possible.

## Before you start
Minimal prerequisites — versions, install, an account. Keep this short; a long prereq list scares off beginners.

## Step 1 — [concrete action]
One clear instruction. Show the exact command or code. Show the expected result so the reader knows it worked.

## Step 2 — [concrete action]
Same pattern. Each step builds visibly on the last.

## Step N — [concrete action]
…

## What you've done
Brief recap of the skill gained (not a feature list). Point to the next tutorial or a related how-to.
```

Guidance: every step must produce a visible, correct result. Never leave the reader unsure whether it worked. Resist teaching theory — the reader is here to do, not to understand (yet).

---

## How-to guide

**Reader need:** "I have a specific task; show me the steps to do it." The reader is already competent and knows the basics. Success is the task completed.

**Tells:** goal-oriented; assumes prior knowledge; the reader arrived because they hit a specific need; real-world, so it should adapt to variations.

**Boundaries — keep out:**
- Teaching the basics. Assume competence; don't explain what a "client" is.
- Why it works. Link to explanation instead.
- Full reference tables. Link to reference for exhaustive options.

**Skeleton:**

```
# How to [accomplish specific task]

## Goal
One line: what this guide gets done and the assumed starting point ("You already have the SDK installed and an API key.").

## Steps
Numbered, action-first. Each step is a real action toward the goal. Unlike a tutorial, you may branch: "If you use X, do A; if Y, do B."

1. [action]
2. [action]
3. [action]

## Verify it worked
How the reader confirms success — a command to run, output to expect, a UI state to check.

## Troubleshooting (optional)
Common failure modes and fixes. How-to guides live in the real world; anticipate what breaks.
```

Guidance: cut the noise. The reader wants the task done, not a lesson. Order the steps logically; a series of true statements in the wrong order is a bad how-to.

---

## Reference

**Reader need:** "Tell me the facts so I can look them up while I work." Like a map or dictionary — consulted, not read cover to cover.

**Tells:** API docs, CLI command lists, configuration options, parameter tables, return values, error codes. The reader already knows what they're doing and needs precise, factual detail.

**Boundaries — keep out:**
- Instructional steps. If you're telling the reader how to do a task, that's a how-to.
- Explanation of why. Illustrative examples are fine; digressions into "why it came to be" are not — they obscure the facts.
- Narrative. Reference is structured for lookup, not for reading.

**Skeleton:**

```
# [Thing being documented: "Configuration options", "client.query() API"]

Brief one-line description of what this reference covers.

## [Entry 1 — e.g. a method, a config key, an endpoint]
Consistent, repeatable structure for every entry. For an API method that means:

- **Signature / syntax**
- **Parameters** — table: name, type, required, default, description
- **Returns** — type and meaning
- **Errors** — what it can raise and when
- **Example** — one minimal, illustrative snippet (not a walkthrough)

## [Entry 2]
Identical structure to Entry 1. Consistency is the whole value of reference — the reader learns the pattern once and scans fast after that.

## [Entry N]
…
```

Guidance: describe the machinery accurately and completely. Be terse. Use tables and consistent entry formats so the reader can scan. Every entry follows the same shape.

---

## Explanation

**Reader need:** "Help me understand — the why, the background, the trade-offs." Read when the reader wants to deepen understanding, not while performing a task.

**Tells:** answers "why" questions; discusses design decisions, architecture, trade-offs, history, alternatives; the one mode where narrative and discursion are appropriate.

**Boundaries — keep out:**
- Step-by-step instructions. If the reader can follow it to do something, it belongs in a tutorial or how-to.
- Exhaustive factual tables. That's reference.
- Being written as required reading before action. Explanation is optional deepening, linked from action pages, not a gate in front of them.

**Skeleton:**

```
# [Understanding / About / Why … — e.g. "How the retry model works", "Understanding our auth model"]

## The problem / context
What question this article answers, and why it matters. Set up the "why".

## [Concept or mechanism]
Explain how it works and, more importantly, why it's built this way. You may explore alternatives that were considered and rejected.

## Trade-offs
Where the honest discussion lives — costs, limits, when this approach is the wrong choice. This is the mode's strength; use it.

## Background / history (optional)
How the system came to be designed this way, if it illuminates the present.

## Related
Links to the tutorials, how-tos, and reference pages this explanation supports.
```

Guidance: this is the discursive mode — narrative, context, and opinion belong here. Make connections. Discuss what could be otherwise. Just don't turn it into instructions or a fact table.

---

## Cross-linking

Diátaxis pages work as a set. When you scaffold one, suggest its links:

- **Tutorial** → links out to reference (for full options it deliberately omitted) and explanation (for the theory it deliberately skipped).
- **How-to** → links to reference (full parameter details) and explanation (why this approach).
- **Reference** → links to how-to and tutorial (for readers who need to *do* rather than look up).
- **Explanation** → links to the tutorials, how-tos, and reference it provides context for.

The links are what let each page stay minimal and in-mode. A tutorial can safely omit the full parameter table precisely because it links to the reference page that has it.
