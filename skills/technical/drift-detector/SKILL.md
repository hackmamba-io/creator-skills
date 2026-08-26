---
name: drift-detector
description: >
  Compare documentation against a current source of truth and identify sections
  that are outdated, inaccurate, or no longer reflect the product or API. Use
  this skill when a technical writer wants to audit existing documentation for
  drift caused by product updates, API changes, feature removals, or version
  bumps. Trigger on phrases like "check my docs for drift," "is this documentation
  still accurate," "find outdated sections," "compare this against the new spec,"
  "what changed since this was written," "audit my docs against the changelog,"
  "which parts of my docs are wrong," "review my docs against the new version,"
  or any request to validate documentation accuracy against a current source.
  Also trigger when someone says their docs feel stale but they are not sure
  where the problems are.
---

## Before you start: verify this skill is fully installed

This skill depends on its reference file `references/drift-rules.md`. More than half of the skill lives in that file, and the skill cannot produce a correct result without it.

Before doing anything else, attempt to read `references/drift-rules.md`. If you cannot read it, STOP. Do not attempt the task from memory or from general knowledge. Tell the user exactly this:

> This skill is not fully installed. Its reference file could not be read, so I can only produce a degraded result that would look normal but be missing most of the skill. Please reinstall with `npx skills add hackmamba-io/creator-skills --skill drift-detector -g` and confirm the `references/` folder is present next to `SKILL.md` before running this skill again.

Only proceed past this point once the reference file has loaded successfully.

---

# Documentation Drift Detector

A skill for comparing existing documentation against a current source of truth
and identifying every place the documentation no longer accurately reflects
the product, API, or system it describes. Works with OpenAPI and Swagger specs,
changelogs, release notes, newer document versions, and informal update notes.

---

## When to activate this skill

Use this skill when someone:

- Provides existing documentation and a source of truth to compare it against
- Suspects their documentation has become inaccurate after a product update
- Wants to know which sections of their docs need updating before a release
- Is preparing for a documentation audit and needs a starting point
- Has received a changelog or release notes and wants to know what to update
- Has a new version of a spec and wants to validate their existing API docs against it
- Asks whether specific documented behavior is still accurate

## When NOT to activate this skill

Do not use this skill when someone:

- Provides only one document with no source of truth to compare against
- Asks for style, grammar, or clarity feedback with no accuracy concern
- Wants to write new documentation from scratch
- Asks general questions about documentation best practices without providing
  documents to compare
- Provides two documents but neither is clearly the current source of truth
  and they have not clarified which is which

---

## What this skill does

Documentation drift is one of the most insidious problems in technical writing
because it happens silently. An engineer renames a parameter, a product manager
sunsets a feature, a developer changes a default value. The documentation does
not break in any visible way. It just becomes wrong, quietly, and readers start
failing without knowing why.

This skill approaches drift detection the way a careful technical editor with
engineering context would: systematically comparing what the documentation claims
against what the source of truth says is currently true, classifying each
discrepancy by type, and assigning severity so writers know what to fix first.

The output names every drifted section with a specific quote from the documentation,
explains what the source of truth says instead, classifies the drift type, and
assigns a severity level. Writers leave with a prioritized list of what is wrong
and why, not a vague sense that something needs updating.

---

## Frameworks used

This skill uses the drift classification system and severity scoring defined
in `references/drift-rules.md`. Read that reference in full before starting
any analysis. The five drift types (Removed, Renamed, Changed behavior, Added
but undocumented, Structurally stale) and the four severity levels (Critical,
High, Medium, Low) are the vocabulary used throughout the output.

---

## Input handling

### What counts as a valid input pair

This skill requires two inputs: the documentation being reviewed and the source
of truth to compare it against. If only one is provided, ask for the second
before proceeding.

The only exception: if the documentation contains internal inconsistencies
that indicate drift without needing an external source (for example, a page
that references its own changelog and contradicts it, or a README that references
a version number inconsistently), flag those and note that a full drift analysis
requires a current source of truth.

### Identifying which document is which

Before starting the analysis, confirm which document is the existing documentation
and which is the current source of truth. If it is ambiguous, ask. Getting this
backwards produces an inverted analysis.

Label both clearly at the top of the output.

### Input type detection

Identify the source of truth type from Section 2 of the reference and apply
the corresponding comparison rules:

- OpenAPI or Swagger spec: apply Section 3
- Changelog or release notes: apply Section 4
- Newer version of the same document: apply Section 5
- Informal update (Slack message, email, ticket, engineer notes): apply Section 6

If the input type is unclear, describe what you received and state which
comparison approach you are applying and why.

### Scope limitations

Be explicit about what can and cannot be detected from the provided inputs.
A changelog-based comparison can only assess what changed. A spec-based
comparison cannot assess behavioral nuances that are not captured in the spec.
An informal update comparison is limited by the specificity of the update itself.

State the scope limitation once, clearly, at the top of the review. Do not
repeat it for every flag.

---

## How to run the analysis

### Step 1: Read the drift rules reference

Before starting, read `references/drift-rules.md` in full. The drift
classification system in Section 1 and the severity scoring in Section 8
are the two sections to internalize before touching the documents.

### Step 2: Identify and label both inputs

State clearly which document is the existing documentation and which is the
source of truth. Note the input type for the source of truth and which
comparison approach applies.

### Step 3: Run the cross-cutting signal check

Before comparing document-specific content, scan the documentation for the
cross-cutting drift signals in Section 7 of the reference:
- Hardcoded version numbers
- Deprecated patterns
- Broken cross-references
- Date-sensitive claims
- Screenshot and diagram dependencies

Flag any found here before moving to the structured comparison. These often
reveal drift that the document-specific comparison might miss.

### Step 4: Run the structured comparison

Apply the comparison rules from the relevant section of the reference based
on the source of truth type. Work systematically through the documentation,
checking each claim against the source of truth.

For each discrepancy found:
- Quote the exact text from the documentation that is wrong
- State what the source of truth says instead
- Classify the drift type from the five categories
- Assign a severity level

Do not flag stylistic differences, additional explanation in the docs that
the spec does not contain, or prose that describes the same thing in different
words. Focus on factual discrepancies.

### Step 5: Check for undocumented additions

After flagging what is wrong in the existing docs, scan the source of truth
for anything new that has no corresponding documentation. Flag these as drift
of type Added but undocumented.

### Step 6: Compile and prioritize

Group all flags by severity. Critical items first, then High, Medium, Low.
Within each severity group, order by the section of the documentation where
they appear so the writer can work through the document linearly.

---

## Output format

```
## Documentation Drift Report

**Documentation reviewed:** [Title or description of the existing docs]
**Source of truth:** [Title, type, and version if available]
**Comparison type:** [Spec / Changelog / Document version / Informal update]
**Scope note:** [One sentence on what this comparison can and cannot assess]

---

### Drift Summary

**Critical:** [N items]
**High:** [N items]
**Medium:** [N items]
**Low:** [N items]
**Total flags:** [N]

[2 to 3 sentences on the overall drift pattern. Is drift concentrated in one
area of the docs or distributed? Is it mostly naming drift from a rename, or
behavioral drift from changed defaults? Is there a single product change driving
most of the flags?]

---

### Flagged Items

Organized by severity, then by location in the document.

---

#### Critical

**Flag [N]: [Short label, e.g., "Removed endpoint still documented"]**

**Location in docs:** [Section title or page where this appears]
**Drifted content:**
> [Exact quote from the documentation that is now wrong]

**Drift type:** [Removed / Renamed / Changed behavior / Added but undocumented /
Structurally stale]
**What the source of truth says:** [Specific description of the current state,
quoted from the source of truth where possible]
**Reader impact:** [What happens when a reader relies on this documentation]

---

[Repeat for each Critical flag]

---

#### High

[Same structure as Critical]

---

#### Medium

[Same structure as Critical]

---

#### Low

[Same structure as Critical]

---

### What is still accurate

[2 to 4 sentences on the sections of the documentation that the comparison
confirmed are still accurate. This gives writers confidence about what does
not need touching and prevents unnecessary rewrites of correct content.
If the documentation is largely accurate with only isolated drift, say so.]

### Recommended update order

[A prioritized sequence for addressing the flags. Not just "fix Critical first"
but a practical order that accounts for dependencies between fixes. For example,
if a parameter was renamed and that name appears in 6 places, fixing the
reference definition first makes the other five easier. Maximum 5 to 7 steps.]
```

---

## Tone of the report

Documentation drift is rarely the writer's fault. It happens because products
move faster than documentation cycles, because engineers do not always notify
the docs team, and because no one has time to re-audit documentation after
every sprint. The report should be direct about what is wrong without implying
negligence.

- Lead with the specific discrepancy, not a general statement about the docs
  being outdated.
- Quote the exact drifted text so the writer can find it immediately without
  searching.
- State what the source of truth says instead, specifically enough that the
  writer can make the fix without needing to re-read the source of truth.
- Be clear about severity. A renamed parameter and a removed endpoint are
  both drift but they are not equally urgent. The writer needs to know which
  one to fix before the next release.
- Acknowledge what is still accurate. A drift report that only lists problems
  leaves the writer not knowing how much of the document to distrust.

---

## Edge cases

**Documentation is significantly more detailed than the source of truth**
A spec or changelog will almost never capture every nuance documented in a
well-written set of docs. Do not flag additional explanation, examples, or
context in the documentation as drift just because the source of truth does
not contain it. Flag only factual discrepancies.

**Source of truth has errors**
If the source of truth appears to contain errors (a spec field that is clearly
mislabeled, a changelog entry that contradicts itself), note this in the report
and do not treat it as ground truth for that specific item. Flag it as something
the writer should verify with the engineering team before updating the docs.

**Massive drift across the entire document**
If nearly every section of the documentation has drifted, note this in the
summary and recommend a full rewrite from the source of truth rather than
attempting to patch individual items. Provide the drift report as a guide
for what the rewrite needs to address, but flag that incremental patching
may be less efficient than starting fresh from the current spec.

**No clear drift found**
If the comparison reveals no meaningful drift, say so directly. State which
comparison was run, confirm that the documentation appears to accurately
reflect the source of truth, and note any caveats about the scope of the
comparison. Do not manufacture flags to appear thorough.

**Writer provides a very large document**
For very large documentation sets, note that the analysis covers the content
provided and that sections not included in the submission could not be assessed.
Recommend the writer prioritize submitting sections most likely to have drifted
based on what changed in the source of truth.
