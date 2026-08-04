# Information Architecture Principles for Technical Documentation

This reference defines the framework used to audit and restructure documentation.
It combines two complementary approaches: Diátaxis, which classifies content by
purpose and reader need, and task-oriented IA principles, which govern how content
is organized, named, and navigated. Neither framework alone is sufficient.
Diátaxis tells you what kind of content belongs where. Task-oriented IA tells you
how to arrange it so users can find it.

---

## Table of Contents

1. The Diátaxis Framework
2. Task-Oriented IA Principles
3. Navigation and Hierarchy Rules
4. Entry Point Principles
5. Common IA Anti-Patterns
6. Documentation Type Profiles
7. Restructuring Heuristics

---

## 1. The Diátaxis Framework

Diátaxis, developed by Daniele Procida, divides documentation into four distinct
types based on what the reader is trying to do and what kind of knowledge they need.
Mixing these types in a single page or treating them as interchangeable is one of
the most common structural failures in technical documentation.

### Tutorials

**Purpose:** Help a beginner succeed at something for the first time.
**Reader need:** "I am new to this. Show me how to get started."
**What it does:** Teaches through guided action. The reader learns by doing.
**What it does not do:** Explain every option, cover edge cases, or serve as reference.
**Structural signals:** Has a defined starting point, a defined end state, sequential
steps, and a working result the reader can verify.

Common misplacements:
- Tutorials that explain concepts instead of guiding action
- Tutorials with prerequisite knowledge that should be in a separate conceptual page
- Getting Started guides that are actually reference pages in disguise

### How-To Guides

**Purpose:** Help a practitioner accomplish a specific goal.
**Reader need:** "I know what I am doing. How do I do this specific thing?"
**What it does:** Provides steps for a real-world task. Assumes competence.
**What it does not do:** Explain the underlying concept or teach from scratch.
**Structural signals:** Goal-oriented title, direct instructions, minimal explanation
of things the reader should already know.

Common misplacements:
- How-tos that teach concept instead of providing steps
- How-tos buried inside tutorials
- FAQ pages that are actually collections of unlabeled how-tos

### Explanations (Conceptual Guides)

**Purpose:** Help readers understand how or why something works.
**Reader need:** "I want to understand this, not just do it."
**What it does:** Builds mental models, provides context, explains design decisions.
**What it does not do:** Give step-by-step instructions or serve as a reference.
**Structural signals:** Discursive prose, "why" framing, no numbered steps.

Common misplacements:
- Conceptual content buried inside how-tos where the reader just wants the steps
- Architecture overviews with no clear separation from tutorials
- "About" pages that mix explanation with reference material

### Reference

**Purpose:** Provide complete, accurate, structured information for lookup.
**Reader need:** "I know what I need. Just tell me the exact value, parameter, or behavior."
**What it does:** Describes the system exhaustively and consistently. Built for scanning.
**What it does not do:** Explain when to use something or how to accomplish a goal.
**Structural signals:** Consistent structure across entries, dense information, no
narrative flow, alphabetical or systematic ordering.

Common misplacements:
- API reference mixed with conceptual explanation in the same page
- Configuration reference buried inside a how-to guide
- Glossaries without clear separation from conceptual content

### Why Mixing Types Fails

When a page tries to be both a tutorial and a reference, or both a how-to and an
explanation, it serves neither need well. A developer who wants to look up a
parameter does not want to scroll past a 500-word conceptual overview to find it.
A beginner who needs a tutorial does not benefit from seeing every possible option
before they have written their first working example.

The test: can you describe this page in one sentence using only one of the four
type names? If not, it probably needs to be split.

---

## 2. Task-Oriented IA Principles

Task-oriented IA organizes content around what users are trying to accomplish,
not around how the product is built or how the team that wrote the docs is structured.

### The jobs-to-be-done lens

Users arrive at documentation with a job: "I need to authenticate my users,"
"I need to understand how billing works," "I need to migrate from v1 to v2."
They do not arrive thinking "I would like to read the Authentication section."

An IA that is organized around user jobs puts the navigation question as: what
is this person trying to do, and what is the shortest path from the nav to the
answer?

An IA that is organized around product structure puts the navigation question as:
where does this feature live in the codebase or product surface? This produces
navigation that makes sense to the team that built the product and is confusing
to everyone else.

### Signal that navigation is product-organized, not task-organized

- Top-level sections named after product features or modules
  ("Integrations," "Components," "API," "Settings")
- Navigation depth requires 3 or more clicks to reach actionable content
- "Getting Started" is a subsection instead of a top-level entry point
- Multiple sections cover the same user job from different angles
  with no cross-reference

### Signal that navigation is task-organized

- Top-level sections named after what users do ("Build your first app,"
  "Manage your team," "Connect your data")
- Common tasks are reachable in 2 clicks or fewer from the homepage
- "Getting Started" or equivalent is the first or second top-level item
- Related tasks are grouped even if they span multiple product features

---

## 3. Navigation and Hierarchy Rules

### Depth limits

**Maximum 3 levels of hierarchy for most documentation.**
Level 1: Section (e.g., "Authentication")
Level 2: Topic (e.g., "OAuth 2.0")
Level 3: Subtopic (e.g., "Token refresh")

Content that requires a 4th level is either too granular to warrant its own page,
or the parent section is too broad and should be split.

Exception: Large reference documentation (full API references, configuration
references) may go to 4 levels if each level represents a meaningful categorical
distinction.

### Breadth limits

**A section with more than 7 to 9 direct children is too broad.**
Miller's Law (7 plus or minus 2) applies to navigation as much as working memory.
When a section has 12 subsections, users cannot scan it effectively. Audit for
groupings that can consolidate without losing meaning.

**A section with only 1 child is probably misstructured.**
Either the child should be promoted to the parent level, or the parent section
heading is wrong and needs to be renamed to reflect the actual content.

### Parallelism

Navigation items at the same level should be parallel in:
- Grammatical form (all nouns, all gerunds, all imperative phrases)
- Scope (do not mix high-level sections with low-level topics at the same level)
- Content type (do not mix tutorials and reference pages at the same nav level
  without clear labeling)

### Naming conventions

**Use the reader's language, not the product's language.**
If users call it "connecting an account" and the product team calls it
"OAuth integration," the navigation should say "Connect your account."

**Be specific enough to distinguish, general enough to stay stable.**
"Manage API keys" is better than "API Keys" (too vague) and better than
"Create, rotate, and revoke API keys" (too specific for a nav item).

**Avoid these navigation anti-patterns in naming:**
- "Miscellaneous" or "Other" as a nav item
- "Advanced" as a top-level section (advanced compared to what?)
- "Overview" as a child of a section that is itself an overview
- Numbered sections ("1. Getting Started," "2. Installation") in persistent
  navigation (numbering implies a fixed sequence that most users will not follow)

---

## 4. Entry Point Principles

The entry point is the first page a new user sees, or the first nav item they
encounter. It sets the contract for what the documentation is and who it is for.

### What a strong entry point does

- Answers "what is this product and what can I do with it" in under 30 seconds
- Gives users a clear path based on who they are and what they want to do
  ("If you are new, start here. If you are migrating from v1, start here.")
- Does not assume the user has read anything else first
- Links forward to the first action, not backward to background reading

### What a weak entry point does

- Describes the product's features instead of the user's starting actions
- Buries the "Get Started" link below marketing copy or conceptual overview
- Has no audience branching, treating all users as identical
- Is titled "Introduction" or "Welcome" with no indication of what comes next

### The 3-click rule

A user should be able to reach any page they commonly need within 3 clicks from
the entry point. More than 3 clicks usually signals that either the hierarchy is
too deep or the navigation labels are not clear enough to guide decisions.

This is a heuristic, not a hard rule. Apply it to high-frequency user jobs first.
Low-frequency reference material can be deeper.

---

## 5. Common IA Anti-Patterns

These are the structural problems that appear most often in documentation that
has grown organically without architectural review.

### The Dumping Ground Section

A section that accumulates everything that does not fit elsewhere. Usually named
"Miscellaneous," "Other," "General," "FAQs," or sometimes a product feature name
that the team uses as a catch-all.

**Signal:** The section has children that span multiple content types and user jobs
with no coherent grouping principle.
**Fix:** Audit every child page. Reclassify each by Diátaxis type and user job.
Distribute them to appropriate sections or create new sections to house clusters.

### The Buried Getting Started

The entry point for new users is nested inside a section rather than appearing
at the top level.

**Signal:** "Getting Started," "Quickstart," or "Installation" appears as a
subsection of something else, or does not appear in the top-level navigation at all.
**Fix:** Promote it to top-level, first or second position. New users should never
have to hunt for where to start.

### The Feature-Named Hierarchy

The entire navigation is organized around product features or internal team
structure rather than user jobs.

**Signal:** Top-level items read like a product spec or engineering roadmap:
"Authentication Module," "Data Layer," "Config Service," "Integrations."
**Fix:** Identify the 5 to 7 most common user jobs. Reorganize top-level navigation
around those jobs. Features become subsections within job-oriented sections.

### The Monolith Page

A single page that mixes tutorial content, conceptual explanation, how-to steps,
and reference material. Common in documentation that started as a single README
and was never restructured as it grew.

**Signal:** The page is very long, has multiple H2 sections that serve different
purposes, and would require a reader to scroll past irrelevant content to find
what they need.
**Fix:** Split by Diátaxis type. Each type becomes its own page within a logically
grouped section.

### The Orphan Section

A section that has no clear relationship to anything else in the navigation,
usually added by a team member who needed to document something quickly and
created a new top-level section rather than finding the right home.

**Signal:** The section's content could logically live inside another section,
but it sits at the top level with no cross-references to or from related pages.
**Fix:** Identify the closest logical parent. Either nest it or merge it,
and add a cross-reference from wherever users might expect to find it.

### The Duplicated Path

The same user job is reachable through multiple different navigation paths
with no canonical page and no clear relationship between the paths.

**Signal:** Two or more sections cover overlapping topics with different names
("Webhooks" and "Event Notifications" covering the same feature from different
angles, or "Quickstart" and "Getting Started" existing as separate top-level items).
**Fix:** Consolidate to one canonical page. Use redirects or cross-references
to absorb the duplicated paths.

### The Deep Nesting Trap

Content that requires 4 or more levels of hierarchy to reach, almost always
because parent sections were created for organizational clarity rather than
user navigation.

**Signal:** A path like: Docs > API > Authentication > OAuth > Flows > Authorization Code.
**Fix:** Flatten by removing intermediate organizational layers that add clicks
without adding user value. If a section exists only to group things and has no
content of its own, its children can often be promoted.

### The Undifferentiated List

A section that presents 15 or more items at the same level with no grouping,
making scanning impossible.

**Signal:** A sidebar with a flat list of 20 guide titles, or a "How-To" section
with 25 ungrouped subtopics.
**Fix:** Group by theme, user job, or product area. Introduce an intermediate
level of organization that helps users scan to the right cluster before selecting
a specific page.

---

## 6. Documentation Type Profiles

Different documentation types have different IA conventions. Apply the universal
principles above and then check against the relevant profile below.

### API Documentation and Developer Portals

Expected top-level structure:
1. Getting Started or Quickstart (tutorial)
2. Guides or How-Tos (task-oriented)
3. Concepts or Architecture (explanations)
4. API Reference (reference, usually auto-generated)
5. SDKs and Libraries (reference)
6. Changelog or Release Notes (reference)
7. Support or Troubleshooting (how-to)

Common IA failures in API docs:
- API reference and conceptual guide mixed on the same page
- No Quickstart, or Quickstart buried inside a "Guides" section
- Authentication treated as a subsection when it is almost always
  the first thing new users need

### Product Documentation and User Guides

Expected top-level structure:
1. Overview or Getting Started
2. Core tasks, organized by user job
3. Settings and configuration
4. Integrations
5. Troubleshooting
6. Reference (keyboard shortcuts, field definitions, error codes)

Common IA failures in product docs:
- Navigation mirrors the product UI ("Dashboard," "Settings," "Profile")
  instead of user tasks
- Each product feature has its own top-level section regardless of frequency
  of use or user journey relationship
- Troubleshooting is an afterthought at the bottom with no cross-references
  from the pages where users encounter the relevant errors

### Tutorial Sites and Learning Hubs

Expected top-level structure:
1. Start Here or Learning Path
2. Tracks or paths organized by goal or skill level
3. Individual tutorials, grouped by topic or track
4. Projects or exercises
5. Reference material

Common IA failures in learning hubs:
- Tutorials organized by tool or technology instead of learning goal
- No clear progression path, leaving users to pick randomly from a flat list
- Beginner and advanced content mixed at the same level
- Projects and reference material mixed into tutorial sections

---

## 7. Restructuring Heuristics

When proposing a restructured IA, apply these heuristics to validate the proposal
before presenting it.

### The entry point test

Can a brand new user identify where to start within 10 seconds of looking at
the top-level navigation? If not, the entry point needs clarification.

### The user job test

For each top-level section, can you complete the sentence "This section is for
users who want to..."? If you cannot, the section may be organized around the
product rather than the user.

### The type purity test

For each page in the proposed structure, can you classify it as exactly one
Diátaxis type? If a page is doing two jobs, flag it for splitting.

### The duplication test

Does any user job appear in more than one place in the navigation? If so,
either consolidate or add clear cross-references and mark one as canonical.

### The depth test

Count the clicks from the entry point to the deepest content. Is it 3 or fewer
for the most common user jobs? If not, identify which intermediate levels can
be removed or flattened.

### The naming test

Read each navigation item aloud. Does it tell a user what they will find,
in language a user would use? Or does it describe the product's internal
structure in language only the team would use?

### The orphan test

For every section, identify at least one other section that links to it or
is logically adjacent to it. Any section with no logical neighbors is either
misplaced or should not exist as a standalone section.
