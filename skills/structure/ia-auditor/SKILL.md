---
name: ia-auditor
description: >
  Evaluate a table of contents, heading structure, or sitemap and recommend
  logical restructurings based on Diátaxis content types and task-oriented IA
  principles. Use this skill when a writer, documentation lead, or content
  strategist wants to audit or improve the structure of their documentation.
  Trigger on phrases like "audit my docs structure," "is my table of contents
  logical," "my users can't find anything," "review my sitemap," "help me
  restructure my docs," "my navigation is a mess," "is this organized well,"
  "does this ToC make sense," "how should I restructure this," or any request
  to evaluate or improve documentation organization, hierarchy, or navigation.
  Also trigger when someone pastes a table of contents or heading list and asks
  for feedback with no further context.
---

## Before you start: verify this skill is fully installed

This skill depends on its reference file `references/ia-principles.md`. More than half of the skill lives in that file, and the skill cannot produce a correct result without it.

Before doing anything else, attempt to read `references/ia-principles.md`. If you cannot read it, STOP. Do not attempt the task from memory or from general knowledge. Tell the user exactly this:

> This skill is not fully installed. Its reference file could not be read, so I can only produce a degraded result that would look normal but be missing most of the skill. Please reinstall the skill. In Claude Code or another agent, run `npx skills add hackmamba-io/creator-skills --skill ia-auditor -g`. In the Claude app, go to Settings > Capabilities > Skills, delete this skill, and upload it again as a zip that contains both `SKILL.md` and the `references/` folder. Then run this skill again.

Only proceed past this point once the reference file has loaded successfully.

---

# Information Architecture Auditor

A skill for diagnosing structural problems in technical documentation and
proposing a reorganized structure grounded in Diátaxis content classification
and task-oriented IA principles. Covers all technical documentation types:
API docs, developer portals, product documentation, user guides, tutorial
sites, and learning hubs.

---

## When to activate this skill

Use this skill when someone:

- Pastes a table of contents, sitemap, heading list, or navigation structure
  and asks for feedback or a review
- Says their users cannot find what they need in the docs
- Wants to restructure documentation that has grown organically and become
  hard to navigate
- Asks whether their documentation hierarchy is logical or well-organized
- Wants to audit navigation depth, section naming, or content groupings
- Is planning a documentation rewrite or migration and wants an IA foundation
  before writing begins
- Asks how to organize a new documentation set for a product or feature

## When NOT to activate this skill

Do not use this skill when someone:

- Asks about prose quality, tone, or writing style within individual pages
- Wants feedback on the content of a single page, not the structure across pages
- Asks about SEO structure without any documentation IA context
- Wants help creating a single article outline (use a content outline skill instead)
- Asks a general question about documentation best practices without providing
  a structure to audit

---

## What this skill does

Documentation structure is one of those problems that everyone feels before
anyone can articulate it. Users submit support tickets for things the docs
already cover. Writers add pages that duplicate existing content because they
could not find the original. Navigation sections accumulate children until
no single person can describe what the section is for.

This skill gives that structural feeling a name and a fix. It reads a table
of contents or heading structure the way an experienced information architect
would: looking for the user jobs that are buried, the content types that are
mixed together, the sections that exist because they made sense to the team
that wrote them rather than the users who need to navigate them.

The output has two parts. First, a diagnosis that names each structural problem,
quotes the specific navigation item or section that shows it, and explains the
reader impact. Second, a proposed restructured table of contents the writer can
adopt, adapt, or use as a starting point for a conversation with their team.

---

## Frameworks used

This skill combines two frameworks that address different dimensions of IA quality.

**Diátaxis** classifies content by what the reader is trying to do:
tutorials for learning, how-to guides for accomplishing specific tasks,
explanations for understanding, and reference for lookup. Mixing these types
on the same page or in the same navigation cluster is one of the most common
causes of documentation that feels hard to use even when it is technically complete.

**Task-oriented IA** organizes content around user jobs rather than product
structure. A navigation built around how the product is organized internally
makes sense to the team that built it. A navigation built around what users
are trying to accomplish makes sense to the users.

Read `references/ia-principles.md` in full before starting any audit. The
anti-patterns section and the restructuring heuristics are the two sections
to apply most carefully.

---

## Input handling

Writers may provide structure in many forms. Accept all of them without asking
for reformatting.

**Nested markdown list**
The most common format. Treat top-level items as sections and indented items
as subsections. Infer depth from indentation.

**Flat list of page titles**
No hierarchy is explicit. Infer groupings from naming patterns and topic proximity.
Note in the audit that hierarchy was inferred and ask the writer to confirm
before acting on the proposed structure.

**Sitemap or URL structure**
Parse the path segments as hierarchy levels. The domain and top-level path
are usually not meaningful for IA purposes. Start analysis from the first
meaningful path segment.

**Screenshot or description of navigation**
Work with what is provided. Note anything that could not be assessed due to
incomplete information.

**Heading structure from a single large document**
Treat H1 as the document title, H2 as top-level sections, H3 as subsections.
Flag if the document appears to contain content that should be split into
multiple pages.

**No structure provided, only a description of the problem**
Ask for the actual structure before running the audit. A description of
structural problems is not a substitute for seeing the structure itself.
One exception: if the writer describes the structure in enough detail to
reconstruct it, proceed and note what was reconstructed.

---

## How to run the audit

### Step 1: Read the IA principles reference

Before starting, read `references/ia-principles.md` in full. The anti-patterns
in Section 5, the documentation type profiles in Section 6, and the restructuring
heuristics in Section 7 are the primary tools for this audit. Do not run the
audit from general knowledge. Use the reference.

### Step 2: Identify the documentation type

Determine which documentation type profile applies from Section 6 of the reference:
API documentation and developer portals, product documentation and user guides,
or tutorial sites and learning hubs. If the structure spans multiple types,
note this and apply the most relevant profile as the primary frame, with notes
where the other profiles' conventions apply.

If the type cannot be determined from the structure alone, ask before proceeding
or note the assumption clearly at the top of the audit.

### Step 3: Classify existing content by Diátaxis type

Go through each section and page in the submitted structure. For each item,
identify which Diátaxis type it appears to be: tutorial, how-to, explanation,
or reference. Where the type is ambiguous from the title alone, note the
ambiguity.

Look specifically for:
- Pages that appear to mix types (flag for splitting)
- Content types that are missing from the structure entirely
- Content types that are scattered instead of grouped

### Step 4: Run the anti-pattern scan

Using Section 5 of the reference, scan the structure for each named anti-pattern:
the dumping ground section, the buried getting started, the feature-named hierarchy,
the monolith page, the orphan section, the duplicated path, the deep nesting trap,
and the undifferentiated list.

For each anti-pattern found:
- Name it
- Quote the specific section or pages where it appears
- Explain the reader impact

### Step 5: Apply the restructuring heuristics

Before drafting the proposed structure, run the seven heuristics from Section 7
of the reference against the current structure. Note which ones fail. The proposed
structure must pass all seven.

### Step 6: Draft the proposed structure

Produce a restructured table of contents using the following principles:
- Organize top-level sections around user jobs, not product features
- Group content by Diátaxis type within each section
- Ensure the entry point is at the top level and clearly named
- Keep hierarchy to 3 levels maximum unless reference material requires more
- Keep each section to 7 to 9 children maximum
- Use parallel naming conventions across items at the same level
- Eliminate or consolidate duplicated paths
- Remove intermediate organizational levels that add clicks without adding clarity

Present the proposed structure as a nested list that mirrors the format of
what the writer submitted, so they can compare the two directly.

### Step 7: Annotate the proposed structure

Add brief annotations to the proposed structure explaining the rationale for
significant changes. Not every item needs annotation. Annotate:
- New sections that did not exist before, explaining why they were created
- Items that were moved significantly, explaining where they came from
- Items that were split or merged, explaining what changed and why
- The entry point, confirming it passes the entry point test

---

## Output format

```
## Information Architecture Audit

**Documentation type:** [API docs / Product docs / Tutorial site / Mixed]
**Input format:** [Nested list / Flat list / Sitemap / Headings / Other]
**Framework applied:** Diátaxis + Task-Oriented IA

---

### Current Structure Assessment

[3 to 5 sentences on the overall state of the structure. What is the dominant
organizational logic: product-organized or task-organized? What content types
are present, missing, or mixed? What is the most significant structural problem
the user would feel when navigating this documentation? Be specific about the
pattern, not just the presence of problems.]

---

### Structural Diagnoses

**Problem [N]: [Anti-pattern name]**

> [Quote the specific section titles or navigation items where this appears]

**What is happening:** [Plain description of the structural issue]
**Reader impact:** [What a user experiences when they hit this problem, concretely]
**Diátaxis dimension:** [Which content type classification is relevant, if applicable]

---

[Repeat for each problem found. Target 3 to 7 diagnoses. Fewer than 3 may
mean the structure is fundamentally sound. More than 7 risks overwhelming
the writer before they see the proposed fix. If there are more than 7 real
problems, group related ones under a single diagnosis.]

---

### Content Type Map

[A quick classification of the existing content by Diátaxis type. Format as
a simple list or table. Flag any pages or sections where the type is ambiguous
or where types appear to be mixed. This gives the writer a picture of what
they have before the proposed structure shows what to do with it.]

---

### Proposed Structure

[The restructured table of contents as a nested list, matching the format
the writer submitted. Annotate significant changes inline with a brief note
in brackets after the item, e.g., "[moved from Miscellaneous]" or
"[new section: groups authentication how-tos previously scattered across 3 sections]"]

---

### What drove the restructuring

[3 to 5 sentences explaining the primary organizing decisions in the proposed
structure. What was the central shift: from product-organized to task-organized?
From mixed types to type-separated sections? From deep nesting to flatter hierarchy?
Name the principle, not just the change.]

### Implementation priority

[A short prioritized list of the changes that will have the most immediate
impact on users. Not everything in the proposed structure needs to happen at
once. Tell the writer what to do first. Maximum 5 items, ordered by impact.]
```

---

## Tone of the audit

Documentation IA problems are almost always the result of good intentions
accumulated over time, not careless work. A new section made sense when
someone added it six months ago. The navigation made sense when the product
had half the features it has now. The audit should be direct about what is
broken and why, but it should never frame the problems as failures of the
people who built the structure.

- Name the anti-pattern clearly. "The feature-named hierarchy" is more useful
  than "the navigation is confusing."
- Lead with reader impact. The reason to restructure is that users cannot find
  what they need, not that the structure offends IA principles.
- Make the proposed structure genuinely usable. A restructuring recommendation
  that requires a full documentation rewrite to implement is not actionable for
  most teams. Where possible, propose changes that can be implemented incrementally.
- Separate what is structurally wrong from what is a naming preference. Call out
  both, but be clear about which is which.

---

## Edge cases

**Structure is already well-organized**
Some structures are genuinely sound. If the anti-pattern scan turns up fewer
than 2 meaningful problems and the restructuring heuristics mostly pass, say
so directly. Note the 1 to 2 improvements that would strengthen an already
solid structure and explain what makes the current organization work.

**Structure is very large (50 or more pages)**
Audit at the section level rather than the individual page level. Diagnose
structural problems at the top 2 levels of the hierarchy. Note that a full
page-level audit would require reviewing each page's content, not just its title.

**Structure is very small (5 or fewer pages)**
The Diátaxis framework and deep hierarchy rules are less relevant at this scale.
Focus the audit on naming, entry point clarity, and content type mixing.
Note that IA concerns become more important as the documentation grows.

**Writer disagrees with a restructuring recommendation**
Do not immediately concede. Explain the principle behind the recommendation
and the specific reader impact it addresses. If the writer provides context
that changes the analysis (their users behave differently, their documentation
has constraints you could not see from the structure alone), acknowledge that
and adjust the recommendation. If the disagreement is about preference rather
than reader need, note both options and let the writer decide.

**Structure appears to be in active migration or transition**
Some structures mix old and new organizational patterns because a migration
is in progress. If this appears to be the case, note it and ask before
recommending changes that might conflict with the migration plan. If the writer
confirms a migration is underway, scope the recommendations to complement
rather than conflict with that plan.
