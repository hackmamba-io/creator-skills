# Creator Skills: Claude Skills for Technical Writers

A collection of Claude skills built specifically for technical writers, developer educators, and anyone who creates content for technical audiences. Whether you are writing your first tutorial or auditing a documentation set that has been live for three years, these skills give you a structured, opinionated review process you can run on any draft.

These skills were built and refined through the content work we do at [Hackmamba](https://hackmamba.io). They reflect what actually goes wrong in technical writing across experience levels: code that breaks when readers copy it, documentation that quietly drifted out of date, articles that are aimed at the wrong reader, and prose that reads like it came from a machine rather than a practitioner. Every skill in this collection was designed to solve a specific, recurring problem.

---

## How to install a skill

1. Open Claude Desktop and navigate to your skills directory. On Mac, this is usually `~/Library/Application Support/Claude/skills/`. On Windows, it is usually `%APPDATA%\Claude\skills\`.
2. Copy the skill folder (for example, `style-guide-enforcer/`) into your skills directory. Make sure the folder contains both the `SKILL.md` file and the `references/` subfolder.
3. Restart Claude Desktop.
4. The skill is now active. Claude will use it automatically when your request matches the skill's trigger conditions, or you can invoke it directly by describing what you want to do.

---

## Skills in this collection

The collection is organized into three categories based on what each skill evaluates.

### content-quality

Skills for reviewing the craft and calibration of written content. These are the skills you run on a draft before it goes anywhere near a publishing queue.

---

#### style-guide-enforcer

**What it does:** Reviews any technical writing draft against a consolidated set of rules synthesized from four major style guides: the Google Developer Documentation Style Guide, the Microsoft Writing Style Guide, the Chicago Manual of Style, and the Apple Style Guide. For every flagged issue, it quotes the exact sentence, names the principle being violated, explains why it matters to the reader, and offers a specific rewrite.

**Who it is for:** Technical writers at any level, developers who write documentation, and editors reviewing content before publication. Writers who are new to technical writing will get explanations of each principle. Senior writers will get direct, peer-level feedback with alternative framings where relevant.

**Key benefits:**
- Covers voice and tone, grammar, word choice, punctuation, headings, lists, code elements, and inclusive language in a single pass
- Accepts optional company-specific style overrides that take precedence over the base rules
- Calibrates feedback to the writer's experience level
- Ends every review with a "One thing to focus on next" that identifies the writer's most recurring pattern as a habit to build, not just a list of mistakes to fix

**How to use it:** Paste your draft and ask Claude to review it. Optionally include your company's style rules or a description of your audience. The skill handles drafts of any length and works equally well on a single paragraph or a full article.

---

#### audience-analyzer

**What it does:** Reads a draft the way an experienced content strategist would, looking not just at what it says but at who it assumes is reading. It infers the actual audience from the text itself, compares that against the writer's stated intended audience if one is provided, and flags every place the draft fails to serve its reader. The output includes a full audience profile match, a mismatch report with exact quotes, and a tone and depth calibration assessment across six dimensions.

**Who it is for:** Technical writers at all experience levels, content strategists, and editors who want to evaluate whether a piece is pitched correctly for its audience.

**Audience types covered:**
- Developer (engineer, architect, DevOps)
- Technical Practitioner (data scientist, ML engineer, researcher)
- Technical Writer and Documentation Consumer
- Non-Technical Reader and Beginner (career changers, business stakeholders, students, adjacent professionals)
- Mixed and layered audiences

**Key benefits:**
- Works with a draft alone, a draft plus stated audience, or a draft plus a full content brief
- Surfaces the specific signals in the text that indicate audience miscalibration
- Provides a Tone and Depth Calibration Matrix that assesses jargon level, code presence, math and theory, structure preference, and benchmark standards

**How to use it:** Paste your draft and optionally describe your intended audience. If you have a content brief, include that too for the most targeted analysis.

---

#### deslop-reviewer

**What it does:** Reviews developer-facing technical content for the writing patterns that make prose read as AI-generated rather than authored by a practitioner. It flags filler language, mechanical transitions, marketing adjectives, narrated code, fake reader-journey framing, and structural tells. For every flag, it proposes a concrete rewrite that preserves the technical meaning exactly.

**Who it is for:** Anyone producing technical content with AI assistance who wants the output to read as human-generated. Also useful for editors reviewing AI-assisted drafts before publication.

**Key benefits:**
- Covers writing patterns specific to technical content, not just general prose problems
- Every rewrite preserves the original technical claim, so de-slopping never accidentally changes what a command does or what an API returns
- Groups findings by severity so writers know what to fix first
- Distinguishes between clean and bland writing

**How to use it:** Paste your draft or name the file to review. Ask Claude to review it for AI writing patterns, or ask it to fix the draft directly and return a cleaned version.

---

### structure

Skills for evaluating and improving documentation architecture. These skills operate at the level of navigation, hierarchy, and content organization rather than individual pages.

---

#### ia-auditor

**What it does:** Audits a table of contents, sitemap, heading structure, or navigation hierarchy and produces a diagnosis of every structural problem with the current organization, and a proposed restructured table of contents the writer can adopt or use as a starting point. The analysis is grounded in Diátaxis content classification and task-oriented IA principles, giving every recommendation a named reason rather than a personal preference.

**Who it is for:** Technical writers, documentation leads, and content strategists who are dealing with documentation that has grown organically and become hard to navigate. Also useful at the start of a new documentation project before any pages are written.

**Frameworks used:**
- Diátaxis (tutorials, how-to guides, explanations, reference): classifies content by reader need and flags where content types are being mixed
- Task-oriented IA: evaluates whether navigation is organized around what users do or around how the product team built things

**Named anti-patterns the skill detects:**
- The Dumping Ground Section
- The Buried Getting Started
- The Feature-Named Hierarchy
- The Monolith Page
- The Orphan Section
- The Duplicated Path
- The Deep Nesting Trap
- The Undifferentiated List

**Key benefits:**
- Accepts navigation input in any format: nested markdown, flat title lists, sitemap URLs, heading structures, or a description of the problem
- Covers API documentation, product documentation, user guides, tutorial sites, and learning hubs
- The proposed structure is always presented in the same format the writer submitted, so before and after are directly comparable
- Includes implementation priority guidance so changes can be made incrementally rather than requiring a full rewrite

**How to use it:** Paste your table of contents, sitemap, or heading structure in any format and ask for an IA audit. Optionally describe the documentation type and who your primary users are.

---

#### diataxis-scaffolder
**What it does:** Classifies the documentation intent and scaffolds a mode-appropriate skeleton with section headings, guidance notes, and explicit boundaries that keep the page from drifting into another mode. The writer fills in the content, the skill ensures the container is right before writing begins.

**Who it is for:** Technical writers starting a new documentation page, tutorial, guide, README section, or API page. Especially useful for writers who are unsure which of the four Diátaxis modes their topic belongs to.

**Modes covered:**
- Tutorial: learning through guided action, assumes no prior competence
- How-to guide: accomplishing a specific task, assumes a competent reader
- Reference: structured information for lookup while working
- Explanation: background, context, and understanding for readers who want to know why

**Key benefits:**
- Classifies the intent first, then scaffolds, so the structure follows the reader's need
- Flags the boundaries that would pull the page into a different mode, so writers know what to avoid as they draft
- Suggests cross-links to sibling pages in other modes, keeping each page focused while ensuring the full topic is covered
- Follows the principle of one page, one mode: if the topic genuinely needs two modes, it scaffolds two pages

**How to use it:** Describe the page you want to create or paste your topic. The skill will classify the intent, confirm its reading in one line, and generate the skeleton.

---

### technical

Skills for evaluating technical elements within content. These skills require domain knowledge to run effectively and cover things that prose-level feedback consistently misses.

---

#### code-quality-reviewer

**What it does:** Reviews code samples in technical content for correctness, completeness, runnability, security hygiene, and code-prose consistency. It checks both the code itself and the prose that surrounds it, with more weight on the code. Every flagged issue comes with an explanation of the reader impact and a corrected version of the code. The review ends with a readiness verdict: ready with minor fixes, needs revision before publication, or not publication-ready.

**Who it is for:** Technical writers reviewing code in their own articles, developers writing documentation or tutorials, and editors reviewing articles before publication.

**Language coverage:**

Tier 1 (full review with language-specific conventions): Python, JavaScript, TypeScript, Bash, SQL, YAML, Dockerfiles, Go

Tier 2 (universal rules): All other languages

**Universal rules cover:**
- Completeness: imports, prerequisites, scoping
- Runnability: real code vs pseudocode, placeholder formatting, version pinning
- Error handling: network calls, file operations, authentication, user input
- Security hygiene: hardcoded credentials, SQL injection, plaintext secrets
- Naming and clarity: descriptive variable names, code-prose terminology consistency, magic numbers
- Code block formatting: language labels, input and output separation

**Key benefits:**
- Explicitly flags AI-generated code patterns: plausible-looking but environmentally brittle, missing error handling, generic variable names, stale version assumptions
- Reviews code-prose integration: whether the prose before and after each block sets context, explains output, and matches the code's terminology

**How to use it:** Paste your full article, a single code block, or code blocks with surrounding prose. Optionally describe your audience or publication target for more calibrated feedback.

---

#### drift-detector

**What it does:** Compares existing documentation against a current source of truth and identifies every place the documentation no longer accurately reflects the product, API, or system it describes. Every flagged item is classified by drift type and assigned a severity level so writers can triage what to fix first. The report also confirms what is still accurate, so writers know which sections they can leave alone.

**Who it is for:** Every technical writer who has maintained documentation through at least one product update cycle. This is a universal problem that affects writers at all experience levels.

**Supported source of truth types:**
- OpenAPI or Swagger spec (most structured, most reliable)
- Changelog or release notes
- A newer version of the same document
- Informal update notes (engineer Slack messages, tickets, emails)

**Drift classification system:**
- Removed: something documented no longer exists
- Renamed: something exists under a different name
- Changed behavior: something works differently than documented
- Added but undocumented: something new exists with no corresponding documentation
- Structurally stale: cross-references, version numbers, or navigation that no longer reflects the current state

**Severity levels:** Critical, High, Medium, Low

**Key benefits:**
- Confirms what is still accurate alongside what is wrong, so writers do not unnecessarily rewrite correct content
- Includes recommended update order that accounts for dependencies between fixes
- Works with messy, informal inputs

**How to use it:** Provide your existing documentation and your source of truth. These can be pasted directly, described, or provided as file content.

---

## How these skills work together

Each skill covers a distinct dimension of technical content quality, so they are designed to be used in sequence. Here is a suggested workflow for reviewing a draft from scratch:

1. **Start with `audience-analyzer`** to confirm the draft is pitched at the right reader before investing time in other reviews.
2. **Run `style-guide-enforcer`** to catch prose-level issues across voice, grammar, word choice, and formatting.
3. **Run `deslop-reviewer`** to catch AI writing patterns that the style guide enforcer does not cover.
4. **Run `code-quality-reviewer`** if the draft contains code, to validate runnability, security, and prose integration.
5. **Use `ia-auditor`** when the draft is part of a larger documentation set and you want to evaluate where it fits structurally.
6. **Use `drift-detector`** when the draft updates existing documentation and you want to confirm nothing has been missed.
7. **Use `diataxis-scaffolder`** before writing begins to ensure the structure is right before the content is filled in.

---

## Contributing

This collection is maintained by Hackmamba. If you use one of these skills and find a gap, or a pattern it consistently misses, feel free to open an issue or submit a pull request.
When contributing a new skill, follow the existing structure: a `SKILL.md` with clear activation and deactivation triggers, a `references/` folder with the knowledge base the skill reads during a review, and placement in the correct category folder.

**If this skills helps you, please star the repo and share it. That is the main way other writers find it.**

---

## Get in touch

If you have questions about any of the skills or have ideas for new skills you would like to see in this collection, feel free to reach out to the maintainers directly.

- [Praise](https://www.linkedin.com/in/praise-james-608b91284)
- [Asjad](https://www.linkedin.com/in/asjad2001)

We are happy to help you get set up or talk through how to adapt a skill for your specific workflow.

---

## Join the Hackmamba Creators community

If you want to connect with other technical writers, share your experience using these skills, or learn from people who are doing the same kind of work you are, come join us in the Hackmamba Creators community on Discord. It is a space for technical writers at all levels to ask questions, share work, and grow together.

[Join the Hackmamba Creators Community](https://hackmamba.io/community/)

