---
name: audience-analyzer
description: >
  Analyze any technical writing draft to identify who is actually reading it, where
  the draft misses its intended audience, and how to fix the mismatch. Use this skill
  whenever a technical writer asks to check their audience fit, calibrate their tone
  or depth, identify who their content is really written for, or get feedback on
  whether their article matches their intended reader. Trigger on phrases like "is
  this written for the right audience," "check my tone," "who is this written for,"
  "does this match my audience," "is this too technical," "is this too basic,"
  "calibrate my depth," "review my article for audience fit," "is this pitched
  correctly," or any request to evaluate whether content matches its reader. Also
  trigger when a writer pastes a draft without context and asks for general feedback,
  since audience fit is the first diagnostic that matters.
---

# Audience Analyzer

A skill for diagnosing who a draft is actually written for, identifying where it
misfires against the intended audience, and delivering targeted rewrites and
calibration guidance that the writer can apply immediately.

---

## When to activate this skill

Use this skill when someone:

- Pastes a draft and asks whether it is pitched at the right level
- Wants to know if their content is "too technical" or "too basic"
- Asks who their article is written for, or whether it matches their target reader
- Requests tone or depth calibration feedback
- Pastes a draft aimed at a specific audience and asks if it delivers
- Provides a brief and a draft and wants to know if the draft serves the brief's
  stated audience
- Asks for general feedback on a draft with no specific focus (run audience analysis
  as the first diagnostic step before anything else)

## When NOT to activate this skill

Do not use this skill when someone:

- Asks a general question about audiences or reader personas without providing a draft
- Only wants style or grammar feedback with no concern about audience calibration
- Explicitly says they know who the audience is and wants a different kind of review
- Pastes a draft in progress and only asks for help with a specific section that
  does not require audience diagnosis
- Asks you to write content for a stated audience from scratch (write it first)

---

## What this skill does

This skill reads a draft the way an experienced content strategist would: not just
for what it says, but for who it assumes is reading. It then compares that inferred
reader against the writer's stated audience (if provided) and surfaces every place
the draft fails to serve them.

The output has four parts:

1. **Audience Profile**: who the draft is actually written for, based on internal evidence
2. **Mismatch Report**: where the draft fails its intended audience, with exact quotes
3. **Rewrite Suggestions**: specific rewrites for each flagged section
4. **Tone and Depth Adjustments**: calibration guidance the writer can apply across
   the whole piece

---

## Primary audience types

This skill is built around four audience types that cover most of what technical
and developer content targets:

- Developer (engineer, architect, DevOps)
- Technical Practitioner (data scientist, ML engineer, researcher)
- Technical Writer and Documentation Consumer
- Non-Technical Reader and Beginner (career changers, business stakeholders,
  students, adjacent professionals learning something new)

Mixed and layered audiences are also handled. See the edge cases section for guidance.

Read the full profiles in `references/audience-profiles.md` before running any analysis.
The profiles include what each audience knows, what they are trying to do, what
frustrates them, and the exact signals that indicate a mismatch. Do not rely on
general assumptions. Use the reference.

---

## Input handling

Writers may provide any of the following combinations. Handle each without asking
for more information unless the draft is under 100 words.

### Draft only

The writer has not said who they are writing for. Your first job is to infer the
intended audience from the draft itself, then evaluate fit.

Clues to look for:

- Topic domain: ML model tuning suggests Technical Practitioner; API integration
  suggests Developer
- Vocabulary level: jargon density, what concepts are assumed versus explained
- Code style: CLI commands suggest Developer; Jupyter-style notebooks suggest
  Technical Practitioner
- Content type: tutorial, how-to, conceptual explainer, reference
- Structure: task-oriented structure suggests Developer; problem-first structure
  suggests Technical Practitioner; concept-then-task suggests Technical Writer

State your inferred audience clearly and explain your reasoning before running
the mismatch report. Be specific about what in the text led you there.

### Draft plus intended audience

The writer has told you who they are targeting. Accept this as ground truth. Your
job is to evaluate how well the draft serves that stated audience, not to question
whether they chose the right one.

### Draft plus intended audience plus content brief

The richest input. Use the brief to understand the goal, the stated audience, and
any constraints. If the brief's audience and the draft's actual calibration diverge,
flag this as the primary finding before anything else.

---

## How to run the analysis

### Step 1: Read the audience profiles

Before starting, read `references/audience-profiles.md` in full. The Mismatch
Signal Library and the Tone and Depth Calibration Matrix are the two sections
you will use most often. Do not skip them.

### Step 2: Identify the actual audience

Read the draft as a content strategist, not a copy editor. Ask:

- What vocabulary level does this draft assume?
- What does it think the reader already knows?
- What does it think the reader is trying to do?
- Does the structure serve a builder, an experimenter, or a craft-focused reader?

Map your observations to the audience profiles. One will fit more cleanly than
the others. If no single profile fits, you are looking at a mixed audience,
which is its own finding.

### Step 3: Compare actual versus intended

If the writer stated their intended audience, compare it to your inferred audience.
Note every place the draft drifts from its stated target. Specific passages with
specific quotes, not vague summary.

If no intended audience was stated, flag the inferred audience and note any internal
inconsistencies. A draft that shifts audiences mid-article is a structural problem,
not just a tone problem.

### Step 4: Run the mismatch scan

Using the Mismatch Signal Library in the profiles reference, scan the draft for
each signal. For every mismatch you find:

- Quote the exact sentence or passage
- Name the signal (from the library, or describe it clearly if it is not in the library)
- Explain why it fails this specific audience
- Offer a rewrite

Target 4 to 10 mismatch flags. Fewer than 3 may mean the draft is well-calibrated
(say so clearly). More than 10 overwhelms the writer and buries the most important findings.
Use the higher end of the range for longer drafts or when multiple audience dimensions
are clearly off. Use the lower end for short drafts or when the issues cluster around
one or two root causes.

### Step 5: Calibrate tone and depth

Using the Tone and Depth Calibration Matrix, assess the draft against all relevant
dimensions for the intended audience:

- Jargon level
- Code presence
- Math and theory
- Structure preference
- Tone
- Benchmark and claims standard
- Length preference

Flag any dimension where the draft is significantly off. Give a concrete adjustment
for each gap, not just a label.

---

## Output format

```
## Audience Analysis

**Draft:** [Title or opening line]
**Input type:** [Draft only / Draft + audience / Draft + audience + brief]
**Intended audience (stated):** [What the writer said, or "Not stated"]
**Actual audience (inferred):** [Your assessment, be specific, not just a label]

---

### Audience Profile Match

[2 to 3 sentences explaining who this draft is actually written for, based on
specific evidence from the text. If it matches the stated audience, say so
directly. If it does not, name the gap clearly. Do not hedge.]

**Confidence:** [High / Medium / Low, and briefly why]

---

### Mismatch Report

**Mismatch [N]: [Short label, e.g., "Theory-first opening" or "Benchmark without methodology"]**

> [Exact quote from the draft]

**Signal:** [Name from the Mismatch Signal Library, or a clear description]
**Who is being failed:** [Developer / Technical Practitioner / Technical Writer]
**Why it misfires:** [1 to 2 sentences on the specific reader impact]
**Suggested rewrite:**
> [Rewritten version]

---

[Repeat for each mismatch]

---

### Tone and Depth Calibration

For each dimension where the draft is off-target:

| Dimension | Target | Current | Adjustment |
|---|---|---|---|
| [Only include rows with a meaningful gap] | | | |

If a dimension is well-calibrated, omit the row or note "On target" briefly
at the end.

---

### Overall Verdict

[3 to 4 sentences. Is this draft serving its audience? What is the single
biggest gap? What one structural or tonal shift would have the most impact?
Be direct. This is a diagnostic, not a performance review.]

### One rewrite priority

[The single most impactful change the writer can make to improve audience fit.
Framed as a specific action, not a principle. For example: "Move the code
example from paragraph 6 to paragraph 2. Your Developer audience is already
skimming to find it."]
```

---

## Tone of the analysis

This is a diagnostic. The writer is not bad. The calibration is off.
Keep that framing throughout.

- Be specific. "The tone is too academic" is useless. "The sentence 'The
  utilization of embeddings facilitates semantic retrieval' reads like a paper
  abstract, not a tutorial" is useful.
- Be direct. Do not soften findings to the point of obscuring them.
- Be constructive. Every flag comes with a path forward.
- Do not mock the draft or imply the writer should have known better.
  The goal is to raise the work, not to grade the writer.

---

## Edge cases

### Mixed or layered audiences

If the draft clearly targets multiple audience types, note this explicitly as
the primary structural finding. Evaluate each section against the audience it
appears to target. Flag missing or abrupt transitions. Use the Mixed Audience
guidance in Section 4 of the profiles reference when giving rewrite direction.

### Draft with no audience mismatch

Some drafts are genuinely well-calibrated. If that is the case, say so clearly
in the Overall Verdict. Flag the 1 to 2 highest-impact improvements anyway,
because there is almost always something. But do not manufacture mismatches
to seem thorough. A verdict of "This draft is well-calibrated for a Technical
Practitioner audience" is a valid and useful output.

### Very short drafts (under 100 words)

Audience signals are harder to read from short samples. Run the analysis but
note the limitation. Offer to review a longer section or the full article.

### Audience type outside the four primary profiles

If the draft targets an executive, a policy maker, a journalist, or another
audience not explicitly covered in the profiles, note this and run the analysis
using first principles: what does this audience know, what are they trying to do,
what frustrates them. The Non-Technical and Beginner profile is often the closest
analog for executive and business audiences, though adjust for the fact that
executives are not necessarily beginners, they are specialists in a different domain.
Apply the same output format regardless.

### Writer disagrees with the inferred audience

Do not immediately concede. If the evidence in the draft supports your inference,
say so clearly and show your work. Quote the specific signals you read and explain
why they pointed to the audience you identified. A good diagnostic is only useful
if it is honest, and agreeing reflexively when you have a well-grounded reading
does not serve the writer.

That said, hold your position proportionally to your confidence. If your inference
was High confidence, push back with evidence. If it was Medium or Low, be more
open to the writer's correction.

The response to disagreement should follow this structure:

1. Acknowledge the writer's stated audience directly.
2. Show the specific signals in the draft that led to your original inference.
   Quote the passages. Name the patterns. Explain what a reader from the inferred
   audience would make of them.
3. Acknowledge that the writer knows their audience context better than you do,
   and that there may be context you cannot see in the draft alone (publication
   platform, companion content, prior knowledge of the reader base).
4. State clearly that you will recalibrate to their stated audience and re-run
   the analysis from that lens.
5. Re-run the mismatch scan against the corrected audience type.

Example framing that balances honesty with respect:

"Based on what I read in the draft, particularly [specific passage], I inferred
[audience type] because [specific reason]. That said, you know the context I
cannot see. I will recalibrate to [writer's stated audience] and re-run the
analysis from there."

Do not capitulate so quickly that the writer loses the diagnostic value of your
original reading. Sometimes the most useful thing you can surface is that the
draft is not yet serving the audience the writer thinks it is, even if they
ultimately know better who that audience is.
