# Audience Profiles for Technical Writing

This reference defines the primary audience types that appear most often in developer
and technical content, plus guidance on handling mixed audiences. Each profile covers
who they are, what they already know, what they are trying to do, what frustrates them,
and the writing signals that match or mismatch them.

Use this reference as a lookup during analysis. Do not rely on general assumptions
about what "developers" or "researchers" want. The specifics here are what make
the analysis useful.

---

## Table of Contents

1. Developer (Engineer, Architect, DevOps)
2. Technical Practitioner (Data Scientist, ML Engineer, Researcher)
3. Technical Writer and Documentation Consumer
4. Non-Technical Reader and Beginner
5. Mixed and Layered Audiences
6. Mismatch Signal Library
7. Tone and Depth Calibration Matrix

---

## 1. Developer (Engineer, Architect, DevOps)

### Who they are

Builders. They read documentation to solve a specific problem, unblock themselves,
or evaluate whether a tool fits their existing stack. They are time-constrained and
outcome-oriented. They trust code over prose, and they will leave if the code is
buried or missing.

### What they already know

- Programming fundamentals: variables, loops, functions, data structures
- Version control, CI/CD, deployment pipelines
- REST APIs, authentication patterns, HTTP status codes
- At least one cloud platform (AWS, GCP, Azure) at a working level
- Common tooling: Docker, Git, bash, package managers

### What they are trying to do

- Get something working, as fast as possible
- Understand how a tool integrates with their existing stack
- Evaluate trade-offs between options (performance, cost, complexity)
- Find the one specific piece of information they are missing

### What frustrates them

- Long conceptual preambles before the first line of code
- Code examples that do not run or are missing critical context
- Being told things they have known for years
- Explaining what without showing how
- Inconsistent terminology between prose and code samples
- No clear path from reading to doing

### Writing signals that match this audience

- Code-first structure: working example early, explanation after
- Second person, imperative mood throughout instructions
- Precise technical vocabulary used correctly (do not avoid jargon; use it right)
- Prerequisites stated upfront: "This guide assumes you are running Node 18+"
- Explicit integration context: "If you are using Express, add this middleware..."
- Honest about limitations: "This approach does not scale beyond X"
- Clear next steps or integration path at the end

### Writing signals that mismatch this audience

- Explaining what an API is, what JSON is, or other fundamentals they mastered years ago
- Burying the first code block 5 or more paragraphs into the article
- Only pseudocode or partial snippets with no runnable example
- Marketing language: "powerful," "seamless," "best-in-class"
- No indication of where this fits in a real workflow
- Passive voice in instructions: "The endpoint should be called..."
- Performance claims with no data or experimental context

---

## 2. Technical Practitioner (Data Scientist, ML Engineer, Researcher)

### Who they are

Experimenters and analysts. They combine deep domain knowledge with coding ability,
but their mental model is research-first rather than engineering-first. They care about
methodology, reproducibility, and correctness above all else. They are comfortable
with ambiguity and with math. They will spot a hand-waved explanation immediately.

### What they already know

- Python (usually), R (sometimes), SQL
- Statistical concepts: distributions, metrics, evaluation frameworks
- ML fundamentals: training and inference, overfitting, embeddings, fine-tuning
- Research paper conventions and how to critically read them
- Jupyter notebooks, experiment tracking tools (MLflow, Weights and Biases), data pipelines

### What they are trying to do

- Understand the reasoning behind a design decision or algorithm
- Reproduce a result or a benchmark
- Evaluate a model, library, or framework against alternatives
- Apply a concept to their specific domain, dataset, or constraints

### What frustrates them

- Oversimplified explanations that lose the nuance they need to make decisions
- Benchmarks without methodology: "X is 3x faster" with no setup, no baseline, no dataset
- Conflating correlation with causation in examples
- Skipping mathematical intuition when it is directly relevant
- Not distinguishing between a research context and a production context
- Demo code that breaks on real data

### Writing signals that match this audience

- Leading with the problem, not the tool: "When your embeddings do not cluster cleanly..."
- Including methodology context for any benchmark: dataset size, hardware, comparison baseline
- Using precise ML vocabulary: do not say "accuracy" when you mean F1 score
- Showing failure cases and edge cases, not just the happy path
- Math presented when it adds clarity, not hidden behind "as you can see..."
- Linking to the original paper or source when referencing a technique
- Tables for multi-attribute comparisons, not prose

### Writing signals that mismatch this audience

- Treating all ML tasks as equivalent (classification is not generation is not retrieval)
- Claiming a tool is "state of the art" without a date or citation
- Hiding error handling in code examples
- Omitting hyperparameter values from examples (reproducibility is non-negotiable)
- Overselling: "our model achieves SOTA results" with nothing behind it
- Assuming a specific deployment environment without saying so

---

## 3. Technical Writer and Documentation Consumer

### Who they are

Craft-oriented professionals who read technical content both as users (to learn a tool
or process) and as critics (evaluating structure, clarity, and information design). They
notice things other readers do not: heading hierarchy, information architecture, whether
a tutorial has a logical learning path. They bring a reader advocate's perspective.

### What they already know

- Documentation frameworks: Diátaxis (tutorials, how-tos, explanations, reference)
- Style guide conventions (Google, Microsoft, Chicago)
- Content types: API reference, conceptual docs, release notes, changelogs
- Variable technical depth, usually enough to follow developer-level content
- Publishing workflows: docs-as-code, static site generators, version control for docs

### What they are trying to do

- Learn a tool or concept accurately so they can write about it
- Evaluate whether content is worth recommending or citing
- Understand an information architecture they can model or critique
- Pick up techniques and patterns they can apply to their own work

### What frustrates them

- Inconsistent structure that makes the information architecture unclear
- Missing context about who the content is written for
- No clear content type signal (is this a tutorial? A how-to? A reference?)
- Vocabulary drift: three different terms used for the same thing
- No stated learning objective at the start
- Docs that show what a product does but never explain why someone would use it

### Writing signals that match this audience

- Clear content type signal, explicit or implied: "By the end of this tutorial, you will have..."
- Consistent terminology throughout, one term per concept
- Logical information hierarchy: overview, concept, task, reference
- An explicit audience statement at the start
- Examples that reflect real use cases, not contrived demos
- Cross-references that help readers navigate: "For X, see Y"
- Clean, minimal prose with no filler

### Writing signals that mismatch this audience

- No logical reading path; content feels arbitrarily ordered
- Over-reliance on screenshots instead of prose and code
- Inconsistent heading hierarchy or missing heading levels
- No stated prerequisites or audience assumption
- The same information repeated in multiple places without cross-referencing
- Verbose intros that bury the actual content

---

## 4. Non-Technical Reader and Beginner

### Who they are

People who are curious about a technical topic but do not yet have the vocabulary,
mental models, or hands-on experience to engage with it at a practitioner level.
This category is broader than it looks. It includes career changers exploring a
new field, business stakeholders trying to understand a product decision, students
encountering a concept for the first time, and experienced professionals from
adjacent disciplines who are learning something new. What they share is this: they
are motivated to understand, but easily lost when writers assume knowledge they do
not have.

Do not confuse "non-technical" with "not intelligent." These readers are often sharp
and analytical. They just do not have the specific background that technical writers
tend to assume.

### What they already know

This varies widely, so resist defaulting to a single baseline. A useful starting
assumption is:

- General familiarity with using software as a product (apps, websites, tools)
- A sense of why technology matters without a deep understanding of how it works
- Possibly some exposure to high-level concepts from news or popular media (AI,
  cloud, automation) without being able to explain the underlying mechanisms
- Little to no experience reading technical documentation, API references,
  or code

When the writer has provided audience context, use it. When they have not, err
on the side of assuming less background rather than more.

### What they are trying to do

- Understand what something is and why it matters, before worrying about how it works
- Build enough mental model to have an informed conversation, make a decision,
  or take a first step
- Feel confident rather than overwhelmed by the end of the piece
- Not be made to feel stupid for not already knowing this

### What frustrates them

- Undefined jargon used as though it needs no explanation
- Skipping the "why this matters" step and jumping straight into mechanics
- Assuming they know what an API, a model, a pipeline, or a token is
- Dense paragraphs with no visual breathing room
- Content that starts accessible and then suddenly shifts into expert territory
  without warning
- Condescension in the opposite direction: oversimplifying in a way that is
  clearly performative rather than genuinely helpful
- No clear path from "I read this" to "I can do or decide something"

### Writing signals that match this audience

- Leading with the real-world problem or outcome before introducing the concept:
  "When you search for something on Google and it understands what you mean, not
  just what you typed, that is semantic search at work."
- Defining every technical term on first use, even terms that feel obvious to
  the writer
- Using analogies that connect unfamiliar concepts to things the reader already
  understands in their daily life
- Short paragraphs, clear headings, and generous white space
- A stated scope: "This article explains what X is and when to use it. It does
  not cover implementation."
- A clear takeaway at the end: what the reader should now understand or be
  able to do
- Visuals or diagrams used to supplement, not replace, the explanation

### Writing signals that mismatch this audience

- Opening with a definition that uses more undefined terms than the one it defines:
  "A vector database is a type of database optimized for storing high-dimensional
  embedding vectors."
- Assuming the reader will google terms they do not know (they will leave instead)
- Using code examples without explaining what they represent or why they matter
- Switching abruptly from conceptual explanation to hands-on instructions without
  a bridge
- Referencing papers, benchmarks, or technical comparisons without establishing
  why any of that matters to this reader
- Writing for the reader the writer wishes they had rather than the reader who
  is actually there

---

## 5. Mixed and Layered Audiences

Some articles intentionally target multiple audience types. A tutorial aimed at both
ML engineers and the developers integrating their models is a legitimate example.
This is valid, but it requires deliberate structure. The problem arises when a writer
targets multiple audiences without realizing it, producing a draft that satisfies none.

### Signals that a draft is targeting a mixed audience unintentionally

- The first half reads like a conceptual explainer; the second half reads like a code
  walkthrough with no structural bridge between them
- Technical depth varies wildly between sections without signposting
- The introduction claims one audience but the body assumes another
- Some sections patronize; some sections exclude; the draft oscillates between both
  in the same piece

### How to handle mixed audiences well

When giving rewrite guidance, recommend the following:

- State the layered audience explicitly in the intro: "This article covers both the
  ML concepts and the implementation. Skip to [Implementation] if you are comfortable
  with the theory."
- Separate conceptual and procedural content into clearly labelled sections
- Use progressive disclosure: start accessible, add depth in later sections
- Do not try to satisfy every audience in every sentence; satisfy each group in
  their section

---

## 6. Mismatch Signal Library

Use this table during analysis to identify specific patterns that signal audience
miscalibration. Each entry names the signal, the audience being failed, and why.

| Signal in draft | Audience being failed | Why it is a mismatch |
|---|---|---|
| Explaining what an API is | Developer | They mastered this years ago. It reads as condescending. |
| "Simply run the following command" | All | Assumes ease. Alienates anyone who hits an error. |
| No runnable code example | Developer | They cannot verify or adapt what they cannot run. |
| Benchmark claim with no methodology | Technical Practitioner | Unverifiable. They will distrust the whole piece. |
| No stated content type | Technical Writer | They cannot evaluate structure without knowing what it is supposed to be. |
| Marketing adjectives: powerful, seamless, robust | All | None of these are informative. All read as ads. |
| Passive voice in instructions | Developer | Obscures who does what in a sequence. |
| Math skipped with "as you can see" | Technical Practitioner | Hand-waving on derivation signals the writer does not understand it. |
| No prerequisites stated | All | Reader cannot assess if the content is for them. |
| Screenshots of code | Developer, Technical Practitioner | Code must be copyable and searchable. |
| Vocabulary drift: three terms for one concept | Technical Writer | Signals carelessness. Undermines trust in the whole document. |
| No next steps or integration path | Developer | They need to know where this fits in their workflow. |
| Happy path only, no failure cases | Technical Practitioner | Real data breaks demo code. Omitting this is a trust issue. |
| Audience mismatch between intro and body | All | The intro promises one experience; the body delivers another. |
| Undefined jargon in the opening paragraph | Non-Technical, Beginner | Readers who do not know the term will not read past paragraph two. |
| Definition uses more undefined terms than the word it defines | Non-Technical, Beginner | Compounds confusion instead of resolving it. |
| Jumps from concept to implementation with no bridge | Non-Technical, Beginner | Skips the mental model building they need before they can follow the steps. |
| No analogy or real-world grounding for an abstract concept | Non-Technical, Beginner | Abstract concepts without anchoring examples do not stick for this reader. |
| No stated scope or learning outcome | Non-Technical, Beginner | They need to know upfront what they will understand by the end, or they will not start. |
| Code examples with no explanation of what they represent | Non-Technical, Beginner | Code without context is noise to a reader who cannot yet read it fluently. |

---

## 7. Tone and Depth Calibration Matrix

| Dimension | Developer | Technical Practitioner | Technical Writer | Non-Technical / Beginner |
|---|---|---|---|---|
| Jargon level | High, used correctly | Very high, domain-specific ML and stats terms expected | Medium, tech-literate but variable depth | Minimal; every term defined on first use |
| Code presence | Essential, lead with it | Important, must be reproducible with hyperparameters | Helpful but not required | Optional; if included, always explained line by line |
| Math and theory | Minimal, skip unless directly relevant | Welcome, include intuition and formulas | Summarize at a high level | Avoid or use only with plain-language intuition first |
| Structure preference | Task-oriented: get to the doing | Problem-oriented: start with the situation | Concept-first: what is this, then how | Outcome-first: what will I understand or be able to do |
| Tone | Direct, peer-to-peer, no hand-holding | Rigorous, precise, collegial | Clear, considered, information-design aware | Warm, patient, assumes no prior context |
| Ideal opening | Working code example or clear problem statement | Problem context and why existing approaches fall short | What this is, who it is for, what you will learn | A real-world scenario or question the reader has already wondered about |
| Benchmark standard | "In our testing with X setup..." | Full methodology: dataset, hardware, baseline, metric | "According to [source]..." with citation | Plain-language summary of what it means in practice; skip the numbers |
| Analogy use | Rarely needed | Rarely needed; precision over accessibility | Occasionally useful | Essential; use frequently and ground every abstract concept in something familiar |
| Length preference | As short as the task allows | As long as the depth requires | Appropriate to content type | As long as the concept needs; do not rush; white space matters |
